# Docker

![Docker](https://www.logolynx.com/images/logolynx/40/4050ef3e853e2301e16863bb3a187ed3.jpeg)


### Comandos
- Verificar os containers que estão sendo executados no momento:

    ```java
        docker ps
    ```

- Para ver todos containers executados:
    ```java
        docker ps -a
    ```

(Usando uma imagem do Ubuntu)
- Para usar o terminal do sistema operacional ( usando a flag *-it* )
    ```java
        docker run -it ubuntu
    ```

- Para sair da execução do docker
    ```java
        CTRL + D
    ```

- Para executar o mesmo docker ja executado
    ```java
        docker start 05025384675e( ID da imagem )
    ```

- Para parar o docker em execução
    ```java
        docker stop 05025384675e( ID da imagem )
    ```

- Flags: -a, de attach, para integrar os terminais, e -i, de interactive, para interagirmos com o terminal:
    ```java
        sudo docker start -a -i 05025384675e
    ```

- Remover um container por ID
    ```java
        docker rm 05025384675e ( ID do container )
    ```

- Remover todos os containers
    ```java
        docker container prune
    ```

- Visualizar todas as imagens
    ```java
        docker images
    ```

- Remover uma imagem especifica 
    ```java
        docker rmi hello-world ( nome do REPOSITORY )
    ```

- Simples site estatico para teste executando em segundo plano ( usando a flag -d )
    ```java
        docker run -d dockersamples/static-site
    ```

- Simples site estatico associando uma porta para acesso via browser ( usando a flag -P ( P ---> maiúsculo) )
    ```java
        docker run -d -P dockersamples/static-site
    ```

- Para ver as portas utilizadas
    ```java
        docker port 989e4d7d3638
    ```

- Para nomear um container, substituindo o id por um nome ( usando a flag --name ) 
    ```java
        docker run -d -P --name SEU-NOME-QUALQUER dockersamples/static-site

        // para parar o container use o comando
        docker stop SEU-NOME-QUALQUER

    ```

- Para definir uma porta específica ( usando a flag --p ( p ---> minusculo) ) 
    ```java
        docker run -d -p 12345:80 dockersamples/static-site
    ```

- Atribuindo uma variável de ambiente
    ```java
        docker run -d -P -e AUTHOR="Solid Snake is Angelo" dockersamples/static-site
    ```

- Para ver todos os containers rodando apenas pelo ID
    ```java
        docker ps -q
    ```

- Parando todos os containers de uma só vez, *docker ps -q* retorna o ID e *docker stop* para o container. Para cada ID retornado ele executa o comando de parar o container. A flag *-t 0* é o tempo que determinamos para que o docker pare o container, por default sempre será 10 segundos.
    ```java
        docker stop -t 0 $(docker ps -q)
    ```

- Resumo
    ```java
        - rodar o container dockersamples/static-site
        - mapear a porta usando o parâmetro -P ou -p
        - definir um nome para o container com o parâmetro --name
        - rodar o container no modo detached com o parâmetro -d
        - listar, parar e remover containers
        
        Comandos
        - docker ps - exibe todos os containers em execução no momento.
        - docker ps -a ---------------------------------------------------- exibe todos os containers, independente de estarem em execução ou não.
        - docker run -it NOME_DA_IMAGEM ----------------------------------- conecta o terminal que estamos utilizando com o do container.
        - docker start ID_CONTAINER --------------------------------------- inicia o container com id em questão.
        - docker stop ID_CONTAINER ---------------------------------------- interrompe o container com id em questão.
        - docker start -a -i ID_CONTAINER --------------------------------- inicia o container com id em questão e integra os terminais, além de permitir interação entre ambos.
        - docker rm ID_CONTAINER ------------------------------------------ remove o container com id em questão.
        - docker container prune ------------------------------------------ remove todos os containers que estão parados.
        - docker rmi NOME_DA_IMAGEM --------------------------------------- remove a imagem passada como parâmetro.
        - docker run -d -P --name NOME dockersamples/static-site ---------- ao executar, dá um nome ao container.
        - docker run -d -p 12345:80 dockersamples/static-site ------------- define uma porta específica para ser atribuída à porta 80 do container, neste caso 12345.
        - docker run -d -e AUTHOR="Solid Snake is Angelo" dockersamples/static-site ------ define uma variável de ambiente AUTHOR com o valor Fulano no container criado.
    ```
---

### Criando um Container, trabalhando com volumes e usando o Docker Host
- Quando escrevemos em um container, assim que ele for removido, os dados também serão. Mas podemos criar um local especial dentro dele, e especificamos que esse local será o nosso volume de dados. Quando criamos um volume de dados, o que estamos fazendo é apontá-lo para uma pequena pasta no Docker Host. Então, quando criamos um volume, criamos uma pasta dentro do container, e o que escrevermos dentro dessa pasta na verdade estaremos escrevendo do Docker Host. Isso faz com que não percamos os nossos dados, pois o container até pode ser removido, mas a pasta no Docker Host ficará intacta.

- Para usar o Docker Host, no Terminal crie um container com o docker run, mas dessa vez utilize a flag -v para criar um volume, seguido do nome do mesmo ( a flag *-v* serve para criar um volume ):
    ```java
        docker run -v "/var/www" ubuntu
    ```
- No exemplo acima, criamos o volume /var/www, mas a que pasta no Docker Host ele faz referência? Para descobrir, podemos inspecionar o container, executando o comando docker inspect, passando o seu id para o mesmo, após o comando verifique a informação de saída na chave  *Mounts[... "Destination":"valor/aonde/sera/salvo/os/arquivos"]*:
    ```java
        docker inspect ID_DO_CONTAINER
    ```

 - **EXEMPLO: Gerando um arquivo no container e salvando na sua area de trabalho**

    ```java
        // docker run -it -v "/home/CIT/angelof/workspace/docker/angelo/alura-docker/files-container/:/var/www/" ubuntu
        - docker run -it -v "C:\Users\NOME_USUARIO\Desktop:/var/www" ubuntu ( isso vai abrir o terminal do unbutu referente ao container criado )

        // Acesse a pasta var/www/
        - root@abd0286c0083:/# cd /var/www/

        // Crie um arquivo de exemplo
        - root@abd0286c0083:/var/www# touch arquivo-teste.txt

        // Altere o arquivo e salve ele
        root@abd0286c0083:/var/www# echo "Este é um arquivo de teste" > novo-arquivo.txt
    ```

- Executando uma simples aplicação em nodejs usando o Docker
    ```java
        // Especifique a pasta que contem sua aplicação em Node e informe usando o -w aonde ela sera executada.
        // Como especifiquei que minha aplicação esta em .../volume-exemplo:/var/www/ então o node vai buscar a aplicação dentro de /var/www/
        // -d para não travar o terminal
        // -p para especificar a porta ( quando subir a aplicação em vez de buscar por localhost:3000 busque por localhost:8080 )
        // -v é o volume aonde sera salvo seus arquivos e/ou aonde sera lido a aplicação
        // -w para especificar a pasta para executar o comando npm start
        - docker run -d -p 8080:3000 -v "/home/CIT/angelof/workspace/docker/angelo/alura-docker/volume-exemplo/:/var/www/" -w "/var/www/"  node npm start

        // Se no terminal você ja estiver na pasta da aplicação, você pode substituir o caminho da pasta por " $(pwd) "
        - docker run -d -p 8080:3000 -v "$(pwd):/var/www/" -w "/var/www/"  node npm start
    ```
---

### Criando um Dockerfile


---