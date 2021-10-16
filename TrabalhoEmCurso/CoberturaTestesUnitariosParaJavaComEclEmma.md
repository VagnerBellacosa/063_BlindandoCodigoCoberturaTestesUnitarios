# Cobertura de testes unitários para Java com EclEmma

100 visualizaçõesCOMPARTILHE!

### [DIEGO PINHO](https://imasters.com.br/perfil/diegopinho)

Tem [100 artigos](https://imasters.com.br/agile/cobertura-de-testes-unitarios-para-java-com-eclemma#) publicados com[ 127198 visualizações](https://imasters.com.br/agile/cobertura-de-testes-unitarios-para-java-com-eclemma#) desde [2013](https://imasters.com.br/agile/cobertura-de-testes-unitarios-para-java-com-eclemma#)



[![Diego Pinho](https://static.imasters.com.br/wp-content/uploads/2018/05/30171243/diego-pinho.jpg)](https://imasters.com.br/perfil/diegopinho)



Bacharel em Ciência da Computação pela PUCSP e MBA em Gestão da Tecnologia da Informação na FIAP. Autor do livro ECMAScript 6 - Entre de cabeça no futuro do JavaScript. Cofundador da Code Prestige e Community Manager no iMasters.

[LEIA MAIS](https://imasters.com.br/perfil/diegopinho)

18 JAN, 2019

### [Gerando PDFs com JS](https://imasters.com.br/front-end/gerando-pdfs-com-js)

14 JAN, 2019

### [Aprendendo a usar branches (e o resto!) no Git](https://imasters.com.br/desenvolvimento/aprendendo-usar-branches-e-o-resto-no-git)

10 JAN, 2019

### [Lidando com o tempo usando o Day.js](https://imasters.com.br/desenvolvimento/lidando-com-o-tempo-usando-o-day-js)

Todo bom desenvolvedor tem consciência de que os testes unitários são uma grande arma para evitar a introdução de novos bugs na aplicação e garantir que tudo continue funcionando como deveria, mesmo depois de fazer uma refatoração no código, incluir uma nova funcionalidade ou qualquer outra modificação.

Foi com este pensamento, que a técnica de desenvolvimento orientado a testes, o famoso TDD (*Test Driven Development*) – o desenvolvimento guiado a testes – ganhou força, ainda mais hoje que trabalhamos com metodologias ágeis, como o SCRUM, onde tudo tem um prazo muito curto e as coisas precisam ser desenvolvidas rapidamente.

Não estou aqui para falar tudo sobre TDD, mas unicamente sobre parte uma dele, os testes unitários. Este tipo de teste é a menor unidade de teste que teremos no nosso sistema e está a cargo do desenvolvedor criá-los. Um teste unitário deve ser capaz de examinar o comportamento do código em várias condições diferentes, garantindo a sua funcionalidade. Entretanto, muitas vezes fica difícil saber se nossos testes unitários estão testando realmente todos os cenários possíveis para a funcionalidade que estamos implementando.“*Testei todos os casos que eu lembrei… mas será que são todos os casos possíveis?*”. Acredito que você já tenha tido um pensamento deste tipo, e este artigo está aqui para ajudá-lo.

Hoje vou apresentá-los uma ferramenta muito bacana chamada [EclEmma](http://www.eclemma.org/).

## **EclEmma**

O EclEmma é uma ferramenta de cobertura de código para Java. De forma resumida, ele te mostra qual a porcentagem do seu código seus testes estão cobrindo. Com esta ferramenta fica muito claro descobrir que aquele cenário X que pensamos na hora de codificar (o famoso if no meio do caminho) não está sendo coberto em nenhum dos seus testes unitários. Interessante, não?

O EclEmma é um plugin gratuito, disponível para o Eclipse sob a *Eclipse Public License*. A ferramenta foi inspirada na biblioteca EMMA desenvolvida por [Vlad Roubtsov](https://www.linkedin.com/in/vladr). A partir da versão 2.0, foi baseada na biblioteca JaCoCo de “cobertura de código”. O JaCoCo está disponível para qualquer desenvolvedor que tenha interesse em criar sua própria ferramenta e está disponível no site oficial. Até o momento em que escrevo deste artigo, a última versão disponível é a 2.3.3.

Dentre as principais características que posso citar da ferramenta, a principal delas é que o EclEmma funciona de forma independente do seu projeto e pode ser executado a qualquer momento. Além disso, ela também dá suporte a diversos frameworks de testes, tais como:

- JUNit
- TestNG
- SWTbot

Neste artigo, vou te mostrar como executar um teste de cobertura com o JUnit.

## **Instalando no Eclipse**

Vou utilizar o Eclipse Mars para fazer as demonstrações, mas já utilizei o EclEmma em versões mais antigas como o Juno, Índigo e Helios sem problemas. A instalação não tem nenhum segredo. É possível instalar a ferramenta de três maneiras:

- Instalação pelo Eclipse Marketplace Client
- Instalação pelo site de update
- Instalação e download manuais

O site oficial mostra com detalhes cada uma das maneiras, vamos adotar a segunda.

\1. Inicie o seu Eclipse e então vá ao menu *Help* > *Install New Software
*

![img1](https://static.imasters.com.br/wp-content/uploads/2016/12/img1-620x386.png)

2 . No campo *Work With* digite http://update.eclemma.org/ e clique em Add

![img2](https://static.imasters.com.br/wp-content/uploads/2016/12/img2-620x431.png)

3 . Selecione a última versão do EclEmma e clique em Next.

4 . Siga os próximos passos aceitando os termos de uso e reinicie o Eclipse.

## **Exemplo de uso**

Agora vou utilizar um exemplo bem simples para mostrar como a ferramenta funciona. Primeiramente, vamos criar uma classe chamada *Calculadora* com o seguinte código:

```java
public class Calculadora {

    public int dividir(int a, int b) {
        if (b == 0) {
            throw new RuntimeException("divisão por zero!");
        }

        return a / b;
    }

}
```

Agora vamos criar uma segunda classe chamada *CalculadoraTest* para testar o método da classe acima:

```java
public class CalculadoraTest {

    private Calculadora calculadora = new Calculadora();

    @Test
    public void testeDivisao() {
        int dividendo = 3;
        int divisor = 1;
        assertTrue(this.calculadora.dividir(dividendo, divisor) > 0);
    }

    @Test(expected = RuntimeException.class)
    public void testeDivisaoPorZero() {
        int dividendo = 3;
        int divisor = 0;
        this.calculadora.dividir(dividendo, divisor);
    }

}
```

 

Com as duas classes criadas, vá até a classe *CalculadoraTest* e clique com o botão direito em cima do primeiro teste, *testeDivisao()*. Perceba que agora você possui a opção *Coverage as*. Selecione a opção *JUnit Test* e aguarde o resultado.

![img3](https://static.imasters.com.br/wp-content/uploads/2016/12/img3-620x260.png)

Seu código ficou colorido, não ficou? Vamos entender o que significa cada uma das cores:

- Verde: Código executado
- Amarelo: Ponto de decisão
- Vermelho: Código não executado

Agora também preste atenção na aba Coverage:

![img4](https://static.imasters.com.br/wp-content/uploads/2016/12/img4-620x216.png)

Podemos notar que somente 64,3% da nossa classe Calculadora foi testada com este teste. Se olharmos a classe Calculadora, veremos que há um trecho em vermelho:

![img5](https://static.imasters.com.br/wp-content/uploads/2016/12/img5-620x262.png)

O que aconteceu foi que somente o primeiro teste não foi capaz de testar o caso onde o dividendo tem o valor zero. Para isso, temos o segundo teste. Agora, execute os dois testes juntos, clicando com o botão direito no nome da classe e selecionando Coverage as… > JUnit Test. Pronto?

Agora vamos avaliar nossa aba Coverage de novo.

![img6](https://static.imasters.com.br/wp-content/uploads/2016/12/img6-620x204.png)

Olha só que maravilha, 100% dos casos da classe foram testados!

## **Conclusão**

O objetivo era mostrar, através de um exemplo realmente simples, como podemos utilizar a ferramenta de cobertura de testes EclEmma. Perceba que, com esta ferramenta, fica claro os casos que podem existir e que ainda não foram testadas. Neste exemplo obtivemos um percentual de 100%, mas em casos reais, isso é muito difícil alcançar. O nível recomendado é de pelo menos 80% de cobertura. Com o uso da técnica TDD, fica ainda mais fácil alcançar estes valores.