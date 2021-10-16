# Teste unitário com JUnit e ComplexGraph

## Veja nesse artigo como aplicar teste unitário com auxílio de uma ferramenta de medição de complexidade, o JUnit e o ComplexGraph.



Por que eu devo ler este artigo:Os testes unitários são uma importante prática de teste que analisa em nível de código-fonte o funcionamento de um determinado algoritmo. Porém, identificar os casos de teste necessários para o teste unitário não é uma tarefa simples.

Tire sua dúvidaMarcar como concluídoAnotar

[Artigos](https://www.devmedia.com.br/artigos/)Teste unitário com JUnit e ComplexGraph

Os casos de teste precisam ter valores apropriados para uma maior eficiência ao encontrar defeitos no código, e também garantir uma cobertura aceitável para o código-fonte em questão. Com o objetivo de auxiliar e agilizar a identificação dos casos de teste é que a ferramenta ComplexGraph será utilizada e demonstrada neste artigo em um estudo de caso. Depois de identificados os casos de teste, a [ferramenta JUnit](https://www.devmedia.com.br/junit-tutorial/1432) será utilizada para executá-los. Por fim, será utilizada uma ferramenta de teste de cobertura para verificar o grau de cobertura que os casos de teste geraram.

A competitividade no mercado de desenvolvimento de software vem aumentando nos últimos anos e manter-se competitivo nesse mercado vem exigindo das empresas maior qualidade nos produtos e serviços oferecidos. Uma etapa fundamental no desenvolvimento de software que ajuda a detectar defeitos ainda não percebidos pelos programadores, e que verifica sua conformidade aos requisitos, é a etapa de teste de software. Essa etapa está se consolidando cada vez mais através de sofisticadas técnicas automatizadas de teste.

Naturalmente, quando se termina de escrever um código-fonte começa o processo de revisão à procura de algum defeito no algoritmo. Em alguns casos, compara-se o código com a especificação e com o projeto a fim de garantir se todas as funcionalidades foram devidamente implementadas. Depois, o código é compilado e são corrigidos problemas de sintaxe. Por fim, são criados casos de teste para mostrar que a entrada submetida ao algoritmo retorna a saída esperada. **O teste unitário segue essas etapas com o objetivo de identificar os defeitos antes que os mesmos se transformem em falhas durante a utilização pelos usuários**.

**O teste unitário, também conhecido como teste caixa-branca ou estrutural**, é um processo de teste onde o conhecimento da estrutura interna do sistema deve ser bem conhecido. Seu principal objetivo é testar as unidades de codificação de um software. Em sistemas orientados a objetos representam os métodos de cada classe, podendo ser até parte do método, dependendo de sua complexidade. Mas, para que o teste unitário tenha um bom desempenho, é necessário um bom planejamento dos testes, no qual leva-se em consideração a criação de uma quantidade razoavelmente boa de casos de teste que atinjam uma cobertura de código-fonte desejável. No entanto, identificar esses casos de teste não é uma tarefa simples e, caso seja feita de maneira errada, podem comprometer a qualidade do teste.

### Complexidade Ciclomática

Uma maneira de identificar os casos de teste é utilizando uma métrica conhecida como complexidade ciclomática. Essa métrica foi desenvolvida por Thomas McCabe em 1976 e tem como finalidade medir a complexidade lógica de uma aplicação baseando-se em uma representação do fluxo de controle, também chamado de grafo da complexidade ciclomática. Através desse grafo é possível visualmente identificar os caminhos de execução do código e que vão se tornar casos de teste.

A métrica da complexidade ciclomática, além de classificar o código-fonte quanto ao seu nível de complexidade, também pode ser utilizada no processo de elaboração dos casos de teste utilizados na **técnica de teste unitário**. O número da complexidade ciclomática também corresponde ao total de caminhos independentes do código-fonte e representa o total de casos de testes que devem ser realizados para cobrir totalmente o código, **garantindo que todas as instruções sejam executadas pelo menos uma vez durante o teste unitário**. Outro benefício ligado a essa métrica está na etapa de manutenção, pois com ela é possível quantificar o quanto a complexidade de um código foi alterada durante o processo de mudança. Muitos desenvolvedores analisam o impacto de alguma mudança sobre o número ciclomático, pois se alguma manutenção é feita e isso eleva muito esse número, talvez seja necessário rever toda a manutenção realizada.

O grafo da complexidade ciclomática descreve o fluxo de controle do programa, onde cada nó do grafo corresponde a um trecho de código e as arestas representam os fluxos de controle. Os fluxos podem variar dependendo da estrutura de código-fonte analisado, por exemplo, quando o nó corresponde a um comando if abrem-se duas arestas, ou seja, dois caminhos diferentes que possibilitam execuções diferentes durante a execução do código-fonte. A **Figura 1** ilustra um exemplo de grafo da complexidade ciclomática.

![Exemplo de Grafo da Complexidade Ciclomática](https://arquivo.devmedia.com.br/revistas/es/imagens/70/8/image004.png)**Figura 1**: Exemplo de Grafo da Complexidade Ciclomática.

O grafo da complexidade ciclomática tem suas bases na teoria dos grafos e oferece uma métrica de software extremamente útil. Existem três métodos para se achar o número da complexidade ciclomática do grafo da **Figura 1**. O primeiro método é contar a quantidade de regiões do grafo (representadas na Figura 1 por R1, R2, R3 e R4), totalizando quatro regiões. Portanto, o número da complexidade ciclomática é quatro. Outro método também utilizado é aplicando a fórmula: C = A - V + 2, onde A é o número de arestas e V o número de nós do grafo. Aplicando a fórmula na Figura 1, tem-se: C = 10 - 8 + 2, totalizando 4, que é o valor da complexidade ciclomática. Por fim, tem-se outra fórmula: C = P + 1, onde P é o número de componentes conexos ou comandos de desvio, ou seja, o número de nós que geram duas saídas (as condições). Aplicando essa fórmula ao exemplo tem-se: C = 3 + 1, totalizando 4.

Pode-se observar, comparando o grafo e código, que torna muito mais fácil encontrar no código os pontos onde se encontram seus caminhos de execução, facilitando a identificação dos casos de testes a serem feitos. Os casos de teste agora são construídos com o objetivo de passar por todas as arestas do grafo, garantindo assim uma cobertura maior dos testes.

**Após ser aplicado o teste unitário, é essencial que seja utilizada uma ferramenta para aferir o grau de cobertura dos testes unitários**. Esse processo é chamado de teste de cobertura. Esse teste verifica, no código-fonte, os caminhos percorridos pelos testes unitários e, assim, ajuda a identificar as áreas que não estão sendo cobertas pelos testes. Ao final, o teste informa o grau de cobertura dos testes unitários e cabe ao responsável pelo teste avaliar esse grau segundo as necessidades de qualidade que necessitam ser alcançadas.

[Saiba maisGuia **Testes de Software**](https://www.devmedia.com.br/guia/testes-de-software/34403)

O objetivo deste artigo é demonstrar como se pode facilitar a obtenção dos casos de teste e **garantir um maior grau de cobertura do teste unitário** utilizando uma ferramenta de apoio. Essa ferramenta é chamada de ComplexGraph. Com ela será possível, a partir de um código-fonte, gerar automaticamente o grafo e o número da complexidade ciclomática. Neste artigo demonstraremos como usufruir dos benefícios dessa ferramenta e realizar o **teste unitário utilizando a ferramenta JUnit** a partir do estudo de caso. Por fim, será executado o teste de cobertura utilizando a ferramenta Eclemma para conferir o grau de cobertura gerado pelo **uso da ComplexGraph com JUnit**.

### Estudo de Caso

Para exemplificar o uso das ferramentas propostas neste artigo, será utilizado um estudo de caso simples e de fácil entendimento, que consiste em calcular a aprovação de um aluno de graduação. O código-fonte foi escrito em Java utilizando a IDE Eclipse. O estudo de caso consiste em uma classe chamada AplicAprovacao cujo principal método explorado é o calcularAprovacao apresentado na **Listagem 1**. Serão passados como parâmetro para esse método a nota1, nota2, nota final e frequência do aluno e, ao final, o método retornará se o aluno foi aprovado ou não.

O método funciona da seguinte maneira: primeiramente ele verifica se o aluno possui frequência maior que 75%, caso não tenha, ele já é reprovado direto. Se o aluno tiver frequência maior ou igual a 75, serão analisadas suas notas. Caso o aluno tenha média menor que 30 pontos, ele também é reprovado. Se a média for maior ou igual a 70 pontos, ele é aprovado. Se o aluno obtiver média maior ou igual a 30 e menor que 70 pontos, ele terá que fazer uma prova final. Portanto, será analisada sua média considerando a média anterior e a nota da prova final. Se esse novo resultado for maior ou igual a 50 pontos, o aluno está aprovado, caso contrário estará reprovado.

**Listagem 1.** Método calcularAprovacao.

```
01 public boolean calcularAprovacao(float nota1, float nota2,
02    float notafinal, int frequencia){
03    float media;
04
05    if (frequencia < 75){
06        resultado = false;
07    }
08    else{
09        media = (nota1 + nota2) / 2;
10        if (media < 30){
11            resultado = false;
12        }
13        else if (media >= 70){
14            resultado = true;
15        }
16        else if ((media + notafinal)/2 >= 50){
17            resultado = true;
18        }else{
19            resultado = false;
20        }
21    }
22
23    return resultado;
24 }
```

### Obtendo a Complexidade Ciclomática

Apresentado o estudo de caso, o objetivo agora é obter o número e grafo da complexidade ciclomática antes de **iniciar o teste unitário**. A ferramenta utilizada neste processo chama-se ComplexGraph, versão 1.0 (veja seção Links). Após executar a ferramenta, deve ser criada uma nova análise através do menu de opções. O sistema irá permitir inserir o código manualmente em uma tela conforme mostrada **Figura 2**, ou também permite localizar o arquivo da classe onde o método está contido.

![Inserção do código-fonte na ferramenta ComplexGraph](https://arquivo.devmedia.com.br/revistas/es/imagens/70/8/image009.jpg)**Figura 2**: Inserção do código-fonte na ferramenta ComplexGraph.

Após confirmada a inserção do código-fonte, deve-se dar início à análise clicando no botão “Iniciar Análise”. A ferramenta irá fazer a leitura do código-fonte fornecido e irá retornar o grafo da complexidade ciclomática em uma nova tela conforme ilustrado na **Figura 3**.

![Grafo da complexidade ciclomática gerado pela ferramenta ComplexGraph](https://arquivo.devmedia.com.br/revistas/es/imagens/70/8/image010.jpg)**Figura 3**: Grafo da complexidade ciclomática gerado pela ferramenta ComplexGraph.

Podem ser observadas no grafo da complexidade ciclomática da **Figura 3** cinco regiões. O que corresponde a uma complexidade ciclomática igual a 5. Isso significa que o algoritmo possui 5 caminhos de execução diferentes e, portanto, necessita para ser testado com 100% de cobertura, 5 casos de testes que façam o teste percorrer todos esses caminhos.

Pode ser observado que cada nó do grafo corresponde a um comando de desvio que pode ser if, else, case, for, while, entre outros. Além disso, cada aresta possui um intervalo de números que correspondem às linhas de código-fonte referente àquele fluxo, o que pode facilitar na localização no código-fonte. Na tela principal da ferramenta, conforme mostra a **Figura 4**, pode ser observado o código-fonte e o resultado da métrica da complexidade ciclomática.

![Resultados da métrica calculada pela ferramenta ComplexGraph](https://arquivo.devmedia.com.br/revistas/es/imagens/70/8/image011.jpg)**Figura 4:** Resultados da métrica calculada pela ferramenta ComplexGraph.

Agora pode-se iniciar o processo de criação dos casos de teste. Para o primeiro caminho, tem-se um if que corresponde à verificação de frequência. Essa situação se refere ao caso de teste 1, onde tem-se como entrada o valor da frequência valendo 74, o que fará que o teste retorne como saída reprovado.

Para o segundo caminho, tem-se um outro if correspondente à verificação da média menor que 30 e com frequência maior ou igual a 75. Esse será o caso de teste 2, que terá como entrada *Nota1* igual a 29 e *Nota2* igual a 30, sendo o valor limite para a obtenção de média menor que 30 e, além disso, terá como entrada *frequência* igual a 75. Com esses dados, espera-se uma saída igual a *reprovado*.

Curso: [O que é teste unitário?](https://www.devmedia.com.br/curso/o-que-e-teste-unitario/2235)

O caso de teste 3 refere-se à verificação da média maior ou igual a 70, com frequência maior ou igual a 75. O caso de teste terá as variáveis *Nota1* e *Nota2* valendo 70, resultando numa média igual a 70. Além disso, a *frequência* será igual a 75.

O próximo caminho representa quando o aluno não conseguiu média para passar e está de final. O caso de teste 4 deverá considerar como entrada *Nota1* e *Nota2* iguais a 30 e *notafinal* igual a 70. Calculando os resultados, a média final resultará em 50, que faz com que o método retorne aprovado.

Por fim, o último caminho representa o aluno sendo reprovado com média final menor que 50. Para isso, o caso de teste 5 terá como entrada *Nota1* e *Nota2* iguais a 30 e *notafinal* igual a 69, sendo suficiente para ter média final menor que 50, retornando assim o aluno sendo reprovado.

Resumindo, a **Tabela 1** apresenta a configuração dos casos de teste.

| Casos de Teste  | Entradas                                             | Saída     |
| --------------- | ---------------------------------------------------- | --------- |
| Caso de Teste 1 | Frequência = 74                                      | Reprovado |
| Caso de Teste 2 | Frequência = 75 Nota1 = 29 Nota2 = 30                | Reprovado |
| Caso de Teste 3 | Frequência = 75 Nota1 = 70 Nota2 = 70                | Aprovado  |
| Caso de Teste 4 | Frequência = 75 Nota1 = 30 Nota2 = 30 NotaFinal = 70 | Aprovado  |
| Caso de Teste 5 | Frequência = 75 Nota1 = 30 Nota2 = 30 NotaFinal = 69 | Reprovado |

**Tabela 1**: Casos de Teste

Nesta seção pode-se observar que o cálculo da complexidade ciclomática e o grafo podem auxiliar mais rapidamente a identificação dos casos de teste dentro do código-fonte, percorrendo todos os caminhos de execução do código, garantindo um grau de cobertura maior para o teste unitário.

### Executando o Teste Unitário

Com os casos de teste definidos é possível dar início ao teste unitário. Para realizar o teste unitário em Java foi aqui utilizada a plataforma Eclipse com o JUnit 4.0 (ver seção links).

Depois, será criado dentro do projeto um diretório com descrição test. Dentro desse diretório será criado um pacote com nome academico.test. Dentro desse pacote pode-se clicar em **File >> New >> JUnit Test Case**. Nesse momento, foi criado o arquivo que irá armazenar e executar os casos de teste cujo nome será AplicAprovacaoTest e que é apresentado na **Listagem 2**.

**Listagem 2**: Casos de Teste

```
01 public class AplicAprovacaoTest {
02
03    public AplicAprovacaoTest() {
04    }
05
06    @BeforeClass
07    public static void setUpClass() throws Exception {
08    }
09
10    @AfterClass
11    public static void tearDownClass() throws Exception {
12    }
13
14    @Before
15    public void setUp() {
16    }
17
18    @After
19    public void tearDown() {
20    }
21
22    /**
23     * Test of calcularAprovacao method, of class EstudoCaso1.
24     */
25    @Test
26    public void testFrequenciaMenor75() {
27        // Frequencia < 75
28        int frequencia = 74;
29        int nota1 = 0;
30        int nota2 = 0;
31        int notafinal = 0;
32        EstudoCaso1 instance = new EstudoCaso1();
33        boolean expResult = false;
34        boolean result = instance.calcularAprovacao(nota1, nota2,
35                                          notafinal, frequencia);
36        assertEquals(expResult, result);
37    }
38
39    @Test
40    public void testMediaMenor30() {
41        // Media < 30
42        int frequencia = 75;
43        int nota1 = 29;
44        int nota2 = 30;
45        int notafinal = 0;
46        EstudoCaso1 instance = new EstudoCaso1();
47        boolean expResult = false;
48        boolean result = instance.calcularAprovacao(nota1, nota2,
49                                          notafinal, frequencia);
50        assertEquals(expResult, result);
51    }
52
53    @Test
54    public void testMediaMaior70() {
55        // Media >= 70
56        int frequencia = 75;
57        int nota1 = 70;
58        int nota2 = 70;
59        int notafinal = 0;
60        EstudoCaso1 instance = new EstudoCaso1();
61        boolean expResult = true;
62        boolean result = instance.calcularAprovacao(nota1, nota2,
63                                          notafinal, frequencia);
64        assertEquals(expResult, result);
65    }
66
67    @Test
68    public void testMediaFinalMaior50() {
69        // (Nota Final + Média)/ 2 >= 50
70        int frequencia = 75;
71        int nota1 = 30;
72        int nota2 = 30;
73        int notafinal = 70;
74        EstudoCaso1 instance = new EstudoCaso1();
75        boolean expResult = true;
76        boolean result = instance.calcularAprovacao(nota1, nota2,
77                                          notafinal, frequencia);
78        assertEquals(expResult, result);
79    }
80
81    @Test
82    public void testMediaEntre30e70eMediaFinalMenor50() {
83        // Media entre 30 e 70 e Média na Prova Final < 50
84        int frequencia = 75;
85        int nota1 = 30;
86        int nota2 = 30;
87        int notafinal = 69;
88        EstudoCaso1 instance = new EstudoCaso1();
89        boolean expResult = false;
90        boolean result = instance.calcularAprovacao(nota1, nota2,
91                                          notafinal, frequencia);
92        assertEquals(expResult, result);
93    }
94 }
```

Após criar a classe AplicAprovacaoTest, automaticamente será registrada a importação dos pacotes da ferramenta. Além disso, é necessário que seja inserida a importação da classe a ser testada para que possa ser criado o objeto.

Analisando o código gerado pela criação da classe de teste, tem-se um método chamado setUp. Ele é responsável pela inicialização do teste, como a instanciação do objeto, por exemplo. Pode ser observado que acima do método existe a anotação @BeforeTest, significando que esse método deve ser executado pelo JUnit antes de cada método de teste. Já o método tearDown é responsável por finalizar o teste podendo ser usado para liberar memória ocupada pelo objeto instanciado, por exemplo. Nesse método tem-se a anotação @AfterTest, que indica ao JUnit que o método deve ser executado logo após cada teste ser concluído.

Os demais métodos apresentados no código são os casos de teste. Para os métodos de caso de teste foi utilizada a anotação @Test que indica ao JUnit que o método a seguir é um caso de teste. O método possui a seguinte estrutura: primeiro criam-se os atributos correspondentes aos parâmetros do método calcularAprovacao que será testado, depois será instanciado o objeto do tipo AplicAprovacao, logo após será invocado o método calcularAprovacao passando todos os atributos como parâmetros, por fim, será chamado o método assertEquals do JUnit que vai comparar o resultado do método com o resultado esperado.

No primeiro caso de teste, na linha 26, é definido um aluno que foi reprovado por insuficiência de frequência, tendo somente o atributo frequência igual a 74. Já na linha 36, é invocado o método assertEquals que foi configurado com o resultado esperado e o resultado obtido pelo método. Caso esse método encontre divergência, o teste unitário acusará um defeito. Para o primeiro caso de teste, o resultado esperado é false.

O segundo caso de teste apresenta um aluno sendo reprovado por ter tido média menor que 30 pontos. Para isso, são definidos frequência igual a 75, nota1 igual a 29 e nota2 igual a 30. O valor esperado para esse teste é false.

O terceiro caso de teste cobrirá a opção do aluno ser aprovado por possuir média maior ou igual a 70. Para isso, é definida a variável frequência igual a 75, a nota1 e nota2 iguais a 70. O valor esperado para esse teste é true.

Para o quarto caso de teste é configurado um aluno que está de final e que foi aprovado por ter média de final maior ou igual a 50. A frequência é mantida igual a 75, as notas 1 e 2 iguais a 30 e a notafinal igual a 70. Espera-se que o aluno seja aprovado. Logo, o método assertEquals é configurado para comparar o resultado com true.

Por fim, tem-se o caso de teste 5, que representa o aluno que não conseguiu média e não conseguiu nota suficiente na prova final. Com isso, sua frequência é 75, as notas 1 e 2 iguais a 30 e a nota final igual a 69, resultando false.

A classe Assert apresenta também outros métodos para definição de valores esperados além do assertEqual. Os principais são: assertFalse, se o parâmetro definido é false; assertTrue, se o parâmetro definido é verdadeiro; assertSame, se os parâmetros são iguais; assertNotNull, se o parâmetro definido não é nulo; e assertNull, se o parâmetro é nulo.

Para executar o teste unitário, basta executar a classe AplicAcademicoTest. Logo em seguida, irá aparecer uma interface da ferramenta JUnit contendo o resultado do teste. Na **Figura 5**, pode-se observar o resultado do teste unitário aplicado para os casos de teste criados. Segundo o resultado apresentado, todos os casos de teste foram executados com sucesso, ou seja, para os valores de entrada fornecidos, o método de aferição de aprovação do aluno reagiu como o esperado.

![Resultado do Teste Unitário](https://arquivo.devmedia.com.br/revistas/es/imagens/70/8/image012.jpg)**Figura 5**: Resultado do Teste Unitário.

Entretanto, deve-se prestar bastante atenção ao elaborar casos de teste, pois se forem estipulados valores de entrada incorretos, pode-se comprometer a validade do teste. Além disso, se forem configuradas as saídas esperadas do teste de maneira errada, a qualidade do teste também estará comprometida. Por isso, os testes devem ser bem planejados.

Por exemplo, suponha que na linha 13 da Listagem 1 a média, em vez de ser >= 70, tenha sido codificada de forma errada, somente > 70. Ao execute o teste novamente, o teste unitário irá acusar um erro no caso de teste 3, pois quando a média valer 70, o método irá retornar false e o esperado seria true. Esse caso representa um defeito por um descuido na comparação da média, que não seria identificado se os casos de teste não tivessem sido bem definidos, utilizando os valores corretos através da comparação dos limites das condições. A **Figura 6** apresenta o resultado da ferramenta com esse defeito inserido no código-fonte.

![Resultado da JUnit com um defeito detectado](https://arquivo.devmedia.com.br/revistas/es/imagens/70/8/image013.jpg)**Figura 6**: Resultado da JUnit com um defeito detectado.

### Aplicando o Teste de Cobertura

Após aplicado o teste de unidade, é importante que seja executado o teste de cobertura para avaliar o grau de cobertura dos casos de teste executados pelo teste de unidade. O principal objetivo desse teste é ajudar a identificar áreas que não estão sendo cobertas pelos casos de teste e, assim, alertar ao desenvolvedor que faltam áreas no código a serem testadas. Para efetuar o teste de cobertura será utilizada a ferramenta Eclemma (ver seção Link), que é fornecida como *plugin* para o Eclipse.

Após a instalação do *plugin* deve-se habilitá-lo no teste acessando o menu “Run >> Covarage...”, depois clica-se em “Coverage” e observa-se os resultados. O teste irá sinalizar no código-fonte a área que foi coberta pelo teste unitário e, neste caso, o trecho irá ficar verde. A área que ficar vermelha representa que o teste não executou aquele caminho do código-fonte, podendo o desenvolvedor identificar, criar o caso de teste que faltou, ou corrigir o código-fonte e executar o teste unitário novamente. Esse processo pode repetir-se até que o desenvolvedor atinja uma cobertura desejável.

Na **Figura 7** pode ser observado o resultado do teste de cobertura para o estudo de caso proposto. Todo o trecho do código ficou verde, ou seja, os casos de teste elaborados cobriram 100% o código-fonte, garantindo assim um teste de unidade mais eficiente e de qualidade. Na **Figura 8** é exibida a porcentagem de cobertura de cada método da classe.

![Resultado do Teste de Cobertura](https://arquivo.devmedia.com.br/revistas/es/imagens/70/8/image014.jpg)**Figura 7**: Resultado do Teste de Cobertura.

![Resultado do Teste de Cobertura com o percentual de cada classe](https://arquivo.devmedia.com.br/revistas/es/imagens/70/8/image015.jpg)**Figura 8**: Resultado do Teste de Cobertura com o percentual de cada classe.

Este artigo apresentou a aplicação do teste unitário utilizando a ferramenta JUnit com o apoio das ferramentas ComplexGraph e Eclemma. Foi possível perceber que a ComplexGraph fornece para o teste unitário o número e o grafo da complexidade ciclomática de um código-fonte favorecendo na identificação dos casos de teste necessários para executar o teste unitário. Ao final, foi executado o teste de cobertura com a ferramenta Eclemma para verificar o grau de cobertura do teste unitário. Ao final do estudo de caso, o teste de cobertura resultou em um grau de cobertura de 100% devido a todos os casos de testes terem sidos rodados corretamente em todos os caminhos de execução do código-fonte.

A ferramenta ComplexGraph ainda possui algumas limitações, mas pode ser observado seu benefício para o estudo de caso aplicado. Ter uma ferramenta que informe o número de casos de teste que devem ser construídos e gerar um grafo para que o desenvolvedor localize no código-fonte os caminhos de execução, pode ajudar e facilitar na criação dos casos de teste.

- [Ferramenta ComplexGraph](https://code.google.com/archive/p/complexgraph/downloads)
- [Ferramenta JUnit](https://junit.org/junit5/)
- [Ferramenta Eclemma](https://www.eclemma.org/)

------

##### Saiu na DevMedia!

- [Teste unitário: Descubra erros no código antes que ele falhe!](https://www.devmedia.com.br/teste-unitario/):
  O teste unitário é uma metodologia que procura aferir a corretude do código, em sua menor fração. Em linguagens orientadas a objetos, essa menor parte do código pode ser um método de uma classe.
- [Primeiros passos com Java](https://www.devmedia.com.br/primeiros-passos-java/):
  Esta é a série de porta de entrada na tecnologia Java, uma linguagem orientada a objetos e baseada em classes com a qual podemos escrever programas para a web, desktop e dispositivos móveis.

------

#### Saiba mais sobre Teste Unitário ;)

- [E aí? Como você testa seus códigos?](https://www.devmedia.com.br/e-ai-como-voce-testa-seus-codigos/39478):
  O programador está sempre escrevendo testes. Neste DevCast falamos um pouco sobre uma das metodologias mais utilizadas e fundamentais, o teste unitário.
- [Testes Unitários em Java](https://www.devmedia.com.br/testes-unitarios-em-java/1549):
  Neste artigo iremos comentar sobre a implementação de testes unitários no Java.