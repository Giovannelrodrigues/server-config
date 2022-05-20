<h1><span style="color:Purple">Sever config</span></h1>

<h4>Um server configuration, é uma api em que você define a configuração dos seus projetos, facilitando controlle de versões entre outras coisas.<h4>

<h4>Deve conter dependência.<h4>

```xml
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

Primeiro passo é colocar anotação @EnableConfigServer na classe de inicialização do spring.

Apos isso adicionaremos a porta da nossa api, geralmente usasse 8888 para server-config

Não obrigatório porém coloquei context-path, que toda requisição terá ser feita http://localhost:8888/server-config/

Definimos o nome da nossa aplicação e os profiles, nesse cado nativo.

Como no projeto estou usando subpastas teremos que mappear, passando a lista na propriedade search-locations

Para criar um arquvio de configuração ussase o nome do projeto - profile .yml ou .properties, exemplo:

<span style="color:pink">nomeprojeto-desenv.yml</span>

<span style="color:pink">nomeprojeto-desenv.properties</span>

```yml
server: 
  port: 8888
  servlet:
    context-path: /server-config
spring:
  application:
    name: server-config
  profiles:
    active:
    - native
  cloud:
    config:
      server:
        native:
          search-locations:
          - classpath:anotherapi/
          - classpath:
          - classpath:
          - classpath:
          - classpath:
```

Agora é so rodar a applicação, e consumir os arquivos via rota, por exemplo


http://localhost:8888/server-config/anotherapi/default

Para consumir é rota padrao + nome do arquivo + profile


<h1><span style="color:Purple">Sever Client</span></h1>

<h4>Deve conter dependência.<h4>

```xml
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-config-client</artifactId>
</dependency>
```

Deve definir no arquivo de configuração qual a rota que ele vai pegar as configurações

```yml
spring:
  cloud:
    config:
      uri: http://localhost:8888/server-config/
      profile: desenv
      name: anotherapi
```

Pronto você ja pode começar a utilizar, lembrando que para pegar as configurações o server-config precisa esta rodando.







