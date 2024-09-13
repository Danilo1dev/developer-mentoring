# Bean Overview - Spring Framework

## Visão Geral
No Spring, os beans são objetos gerenciados pelo contêiner de Inversão de Controle (IoC). O contêiner Spring cria, configura e gerencia esses beans com base nas definições fornecidas (XML, anotações ou código Java). Um **BeanDefinition** encapsula informações essenciais sobre a classe do bean, seu escopo, métodos de inicialização/destruição, e dependências. A definição pode ser ajustada com propriedades como o escopo de **singleton** (instância única) ou **prototype** (nova instância a cada solicitação).

É possível registrar beans manualmente, e a sobrescrição de beans será desativada em versões futuras. Configurações personalizadas podem ser aplicadas para lançar exceções quando houver tentativas de sobrescrição. Isso é importante para garantir a previsibilidade do sistema e evitar problemas durante o tempo de execução.

## Como funciona
Os beans podem ser configurados e registrados por meio de arquivos XML ou anotações como @Bean** e @Configuration em código Java. O contêiner IoC gerencia automaticamente o ciclo de vida dos objetos, garantindo que as dependências sejam resolvidas no momento correto, com a flexibilidade de escolher diferentes escopos para o ciclo de vida do bean.

## Exemplo prático de definição de Bean com anotação
Abaixo está um exemplo básico de como definir um bean usando anotação e injeção de dependências:

```java
@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
```

Neste exemplo, AppConfig define um bean chamado myService, e o Spring IoC gerencia seu ciclo de vida.

## Tópicos importantes:

- **Bean**: um objeto gerenciado pelo contêiner IoC do Spring.
- **BeanDefinition**: define o escopo, dependências e ciclo de vida de um bean.
- **Escopo**: pode ser singleton ou prototype.
- **@Bean**: define um bean em métodos de configuração Java.
- **@Configuration**: classes que declaram beans com @Bean.
- **Inversão de Controle (IoC)**:design pattern onde a responsabilidade de gerenciar objetos é delegada ao contêiner.

## Exemplo funcional:

```java
import org.springframework.context.annotation.*;

@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}

public interface MyService {
    void execute();
}

public class MyServiceImpl implements MyService {
    public void execute() {
        System.out.println("Serviço executado.");
    }
}

public class Application {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        MyService service = context.getBean(MyService.class);
        service.execute();
    }
}
```

Esse exemplo demonstra como o contêiner Spring gerencia o ciclo de vida de um bean e injeta suas dependências automaticamente.

## Referência
Essa explicacao está completa no site [Spring](https://docs.spring.io/spring-framework/reference/core/beans/definition.html).
