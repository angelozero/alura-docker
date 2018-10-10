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
- Para usar o terminal do sistema operacional
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
        docker run -d -P -e AUTHOR="Solid Snake is David" dockersamples/static-site
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
        
        **Comandos**
        - *docker ps* - exibe todos os containers em execução no momento.
        - *docker ps -a* ---------------------------------------------------- exibe todos os containers, independente de estarem em execução ou não.
        - *docker run -it NOME_DA_IMAGEM* ----------------------------------- conecta o terminal que estamos utilizando com o do container.
        - *docker start ID_CONTAINER* --------------------------------------- inicia o container com id em questão.
        - *docker stop ID_CONTAINER* ---------------------------------------- interrompe o container com id em questão.
        - *docker start -a -i ID_CONTAINER* --------------------------------- inicia o container com id em questão e integra os terminais, além de permitir interação entre ambos.
        - *docker rm ID_CONTAINER* ------------------------------------------ remove o container com id em questão.
        - *docker container prune* ------------------------------------------ remove todos os containers que estão parados.
        - *docker rmi NOME_DA_IMAGEM* --------------------------------------- remove a imagem passada como parâmetro.
        - *docker run -d -P --name NOME dockersamples/static-site* ---------- ao executar, dá um nome ao container.
        - *docker run -d -p 12345:80 dockersamples/static-site* ------------- define uma porta específica para ser atribuída à porta 80 do container, neste caso 12345.
        - *docker run -d -e AUTHOR="Fulano" dockersamples/static-site* ------ define uma variável de ambiente AUTHOR com o valor Fulano no container criado.
    ```
