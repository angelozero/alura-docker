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