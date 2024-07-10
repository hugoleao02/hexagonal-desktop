# Projeto de Arquitetura Hexagonal - Transferência Bancária com JavaFX

Este projeto demonstra a implementação de uma aplicação de transferência bancária utilizando a arquitetura hexagonal, com um adaptador front-end JavaFX para interação com o usuário.

## Estrutura do Projeto

### Módulos

- **Core:** Contém as interfaces e classes que definem a regra de negócio do sistema, como a transferência de valores entre contas. Não depende de tecnologias específicas.
  
- **Adaptadores:** Implementa as interfaces do core usando tecnologias específicas, como o adaptador de conta fake e a porta de transferência. Conecta o core ao mundo externo, como bancos de dados ou interfaces gráficas.
  
- **Drivers:** Fornecem implementações concretas para tecnologias específicas, como o driver JDBC para banco de dados ou a biblioteca Swing para interfaces gráficas. São utilizados pelos adaptadores para interagir com as tecnologias.

### Pacotes Importantes

- **conta.tela:** Contém as classes responsáveis por desenhar a interface gráfica de transferência bancária usando JavaFX, como `AdaptadorJavaFx` e `TransferenciaFrm`.
  
- **conta.sistema:** Contém o domínio do sistema, incluindo entidades como `Conta` e serviços como `ServicoTransferencia`.
  
- **conta.adaptador:** Implementa adaptadores concretos para o sistema, como `AdaptadorContaFakeImp` e `PortaTransferenciaImp`.

## Funcionamento do Adaptador JavaFX

### Adaptador JavaFX

A classe `AdaptadorJavaFx` inicializa o contexto do Spring e mostra a interface gráfica de transferência.

### TransferenciaFrm

A classe `TransferenciaFrm` desenha a tela de transferência utilizando JavaFX. Ela utiliza injeção de dependência para obter a `PortaTransferencia` e realiza as operações de obtenção de conta e transferência de valores.

## Utilização

Para utilizar o adaptador JavaFX em sua aplicação, execute a classe `AdaptadorJavaFx`:

```java
public class AdaptadorJavaFx extends Application {
  private ApplicationContext spring;

    @Override
    public void init() {
        System.out.println("iniciando spring..");
        spring = new AnnotationConfigApplicationContext(Build2.class);
    }

    @Override
    public void start(Stage stage) {
        var form = spring.getBean(TransferenciaFrm.class);
        form.mostrar(stage);
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```
A interface gráfica permitirá ao usuário informar as contas débito e crédito, o valor a ser transferido e realizar a operação de transferência.

Executando o Projeto
Para executar o projeto com JavaFX, certifique-se de ter configurado o ambiente com as dependências necessárias do Spring e JavaFX. Em seguida, execute a classe AdaptadorJavaFx.
