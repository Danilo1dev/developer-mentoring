# Container Overview - Spring Framework

## Visão Geral

O **Spring Container** é responsável por criar, configurar e gerenciar os objetos que compõem a aplicação, conhecidos como **beans**. O contêiner usa o padrão de projeto de **Injeção de Dependências (DI)**, permitindo que as dependências sejam fornecidas automaticamente durante a execução da aplicação. Dessa forma, o desenvolvedor não precisa se preocupar em inicializar ou configurar manualmente os objetos, resultando em um código desacoplado e mais fácil de manter.
O contêiner pode ser configurado através de **XML** ou usando **anotações** no código-fonte. As anotações são amplamente utilizadas nas versões mais recentes do Spring para simplificar o desenvolvimento, com a ajuda de anotações como **@Component** e **@Autowired**, que permitem ao Spring gerenciar os beans de forma automática.

## Como funciona
Os beans são declarados no contêiner, que gerencia o ciclo de vida desses objetos. Um ponto central dessa gestão é a interface **ApplicationContext**, que é usada para acessar os beans em tempo de execução. Além disso, os beans podem ser configurados em diferentes **escopos** (por exemplo, **singleton** ou **prototype**), permitindo controle sobre a criação e reutilização de instâncias.

## Exemplo prático de Injeção de Dependências
Aqui está um exemplo básico de como a injeção de dependências funciona usando anotações no Spring:

```java
@Component
public class UserService {
    public void registerUser() {
        System.out.println("Usuário registrado com sucesso.");
    }
}

@Component
public class UserController {

    private final UserService userService;

    @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }

    public void register() {
        userService.registerUser();
    }
}
```

## Tópicos importantes:

- **Spring Container**: responsável por gerenciar o ciclo de vida e as dependências dos objetos (beans).
- **Injeção de Dependências (DI)**: técnica usada para fornecer dependências em tempo de execução.
- **@Component**: anotação usada para declarar uma classe como bean do Spring.
- **@Autowired**: anotação usada para injetar dependências automaticamente.
- **ApplicationContext**: interface que fornece acesso aos beans.
- **Escopo**: diferentes configurações para controle de instâncias, como **singleton** e **prototype**.


## Exemplo funcional:
Abaixo um exemplo funcional que ilustra o uso do contêiner Spring e a injeção de dependências:

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.stereotype.Component;

@Component
class MessageService {
    public String getMessage() {
        return "Olá, Spring!";
    }
}

@Component
class MessagePrinter {
    private final MessageService messageService;

    @Autowired
    public MessagePrinter(MessageService messageService) {
        this.messageService = messageService;
    }

    public void printMessage() {
        System.out.println(messageService.getMessage());
    }
}

public class Application {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(Application.class.getPackage().getName());
        MessagePrinter printer = context.getBean(MessagePrinter.class);
        printer.printMessage();
    }
}
```

## Conclusão
O contêiner Spring é uma peça essencial do framework, facilitando o gerenciamento de dependências e o ciclo de vida dos objetos, promovendo uma arquitetura mais limpa e desacoplada. O uso de anotações como **@Component** e **@Autowired** torna o desenvolvimento mais ágil e menos propenso a erros manuais.

## Referência
Essa explicacao está completa no site [Spring](https://docs.spring.io/spring-framework/reference/core/beans/basics.html).
