# **Cobertura de Testes de aplicações Java no Jenkins**

[![Alysson Pereira](https://miro.medium.com/fit/c/96/96/1*R3zXZ2F8nj1Y1DBCgrC4ow.png)](https://alyssonpereira.medium.com/?source=post_page-----dd326153faa2--------------------------------)

[Alysson Pereira](https://alyssonpereira.medium.com/?source=post_page-----dd326153faa2--------------------------------)Follow

[Dec 7, 2020](https://medium.com/equals-lab/cobertura-de-testes-de-aplicações-java-no-jenkins-dd326153faa2?source=post_page-----dd326153faa2--------------------------------) · 7 min read













![Agueda, Portugal. © Patrícia Almeida](https://miro.medium.com/max/1400/1*o2Kp-49E_tI3YtbNGig9Uw.png)

Agueda, Portugal. © Patrícia Almeida

Essa imagem te chamou atenção? O que guarda-chuvas tem a ver com a cobertura de Testes? Pois bem, falaremos um pouco mais sobre isso durante nosso conteúdo.

# **Cobertura de Testes**

Em virtude de mantermos a qualidade das aplicações e a integridades das mesmas, fiz um estudo relacionado a formas de extrairmos os dados relacionados aos testes unitários de projetos Java e suas respectivas coberturas dentro do código do sistema, integrando esses testes com a execução dos builds na ferramenta de integração contínua Jenkins.

# **Jenkins, o que é?**

Em uma visão geral, o Jenkins é uma ferramenta de integração contínua que surgiu à partir do Hudson da Sun (Oracle), onde trabalha com o objetivo de facilitar o trabalho de Build das aplicações, executando testes e gerando artefatos de um projeto de software. Como o objetivo não é explicitamente demonstrar como o Jenkins funciona, disponibilizarei links de acesso no fim deste artigo, caso queira conhecer um pouco mais sobre o assunto.

# **Testes Unitários**

Em um projeto de desenvolvimento de software, o teste unitário é uma fase onde partes individuais do sistema são testadas de forma isolada, pensando em um fluxo do requisito em si e o que é esperado dele. A responsabilidade de sua criação é do desenvolvedor, que cria os testes unitários pensando sempre nas menores unidades, sempre que uma nova função/classe é desenvolvido (na prática pode não ser bem assim kkkk).

# **Cobertura de Testes**

Ao criarmos e executarmos testes unitários a ideia de seu criador é sempre tentar abranger tudo aquilo que foi desenvolvido, abrangendo desde classes e métodos a funções, laços e condições, passando pelo máximo de linhas de código possível. Por isso, os testes unitários devem ser bem planejados e executados para que possa dar suporte àquilo que foi desenvolvido e evitando ao máximo os bugs.

Mas, ao criarmos os testes unitários como sabemos se ele está cobrindo tudo? Nesse ponto, utilizaremos a cobertura de testes dos quais são geradas através de um plugin, auxiliando na análise de onde aplicar mais testes e verificando pontos que possam ter passado despercebidos.

Agora, voltemos a imagem inicial da leitura. Qual a relação do guarda-chuvas com a cobertura de testes? Então, cobertura de testes é mais ou menos como a imagem, temos vários guarda-chuvas cobrindo o espaço mas logicamente não conseguiremos cobrir todo o espaço com os mesmos. A ideia é sempre tentar desenvolver e melhorar os testes unitários para que essa *cobertura* aumente e os testes possam cobrir mais código ao longo dos ciclos de desenvolvimento, garantindo uma maior qualidade ao projeto.

Analisando as possibilidades de plugins existentes para verificarmos a cobertura de testes para as aplicações desenvolvidas na linguagem Java, foram encontradas e mais indicadas duas opções:

**1- JaCoCo Maven Plugin**

- https://mvnrepository.com/artifact/org.jacoco/jacoco-maven-plugin
- https://www.jacoco.org/jacoco/trunk/doc/

**2- Code Coverage API**

- https://plugins.jenkins.io/code-coverage-api/
- http://cobertura.github.io/cobertura/

Para a avaliação das duas possibilidades, foi realizada a instalação e configuração de ambas no Jenkins e configurados os builds em um projeto que já possuía o JaCoCo integrado ao mesmo.

# **Análise das Ferramentas**

**1- JaCoCo Maven Plugin**

O JaCoCo apresenta as informações de cobertura de testes baseadas em uma visão geral, por pacotes e número total de linhas, mas apresenta um design meio ultrapassado.

![img](https://miro.medium.com/max/60/0*yZRDBR7ao07KdW0l?q=20)

![img](https://miro.medium.com/max/630/0*yZRDBR7ao07KdW0l)

A partir de um build de uma Branch, os dados de cobertura de testes são armazenados e informados em um gráfico histórico por build, conforme imagem abaixo.

![img](https://miro.medium.com/max/60/0*thSEFqVF5n6yXYlV?q=20)

![img](https://miro.medium.com/max/450/0*thSEFqVF5n6yXYlV)

**2- Code Coverage API**

O Code Coverage é mais bonito e mais estruturado que o JaCoCo, mas apresentou alguns problemas de configuração no projeto Java.

Ele foi adicionado ao projeto e configurado conforme o esperado. Quando realizamos o Build da aplicação, grande parte dos testes unitários tiveram erros e o Build não foi finalizado com sucesso.

Pesquisando um pouco mais sobre os erros encontrados, foi verificado que o Code Coverage não era compatível com algumas versões do Java e consequentemente, não rodou em nosso projeto.

![img](https://miro.medium.com/freeze/max/60/1*nq5qf2QonnYpTAdQkTukog.gif?q=20)

![img](https://miro.medium.com/max/630/1*nq5qf2QonnYpTAdQkTukog.gif)

Code Coverage API, Coverage Chart — © [Shenyu Zheng](https://www.jenkins.io/blog/authors/shenyu_zheng)

# **Configurações**

**1- JaCoCo Maven Plugin**

Para a instalação do Jacoco Maven Plugin no Jenkins, basta acessar o gerenciador de plugins do mesmo e pesquisar por *Jacoco Plugin.*

![img](https://miro.medium.com/max/60/0*TUlJDFMLPTZJhvQR?q=20)

![img](https://miro.medium.com/max/630/0*TUlJDFMLPTZJhvQR)

Já nas configurações do projeto cujo há a utilização do Maven, o mesmo deverá ser importado no *pom.xml* do projeto.

![img](https://miro.medium.com/max/60/0*piRoTQ9jLpkzkeoj?q=20)

![img](https://miro.medium.com/max/339/0*piRoTQ9jLpkzkeoj)

Configuração do Plugin no pom.xml do projeto

Ao realizar o build do projeto, serão gerados os dados de cobertura de testes relacionados aos testes unitários do projeto. Esses arquivos estão disponíveis no diretório do projeto (“projeto/target/site/jacoco”).

Para realizar a configuração de cobertura no projeto, basta alterar as configurações pós-build do projeto.

![img](https://miro.medium.com/max/60/0*p8KrXKGtA4AKWDmF?q=20)

![img](https://miro.medium.com/max/630/0*p8KrXKGtA4AKWDmF)

Configurações de um projeto

No Pipeline do projeto, basta adicionar as configurações do JaCoCo:

- jacoco execPattern: “**/target/jacoco.exec”

![img](https://miro.medium.com/max/60/0*kHq92UKWpW4-uG74?q=20)

![img](https://miro.medium.com/max/630/0*kHq92UKWpW4-uG74)

Configurações do Jacoco em ações pós-build

Ao finalizar o Build, serão disponibilizadas as informações de cobertura de testes no menu lateral esquerdo, na página principal do projeto e nos detalhes do build realizado.

![img](https://miro.medium.com/max/60/0*ybVTRdE3RipnMemX?q=20)

![img](https://miro.medium.com/max/630/0*ybVTRdE3RipnMemX)

Resultado dos Builds no projeto

# **Resultados**

Os resultados são gerados após a execução do build, demonstrando os resultados de acordo em cima dos testes unitários realizados no projeto. Dentre eles, temos:

**1- JaCoCo Coverage Trend**

Nesse gráfico, são demonstradas as linhas cobertas e as linhas não cobertas pelos testes unitários em relação ao Build, armazenando o histórico dos resultados por cada Build efetuado e demonstrando no gráfico a cobertura de cada execução.

![img](https://miro.medium.com/max/60/0*RrQycXOEkiOMtNws?q=20)

![img](https://miro.medium.com/max/446/0*RrQycXOEkiOMtNws)

Jacoco Coverage Trend — Cobertura por Build

**2- Overall Coverage Sumary**

Nesse gráfico, são demonstrados os valores relacionados a cobertura das classes em diferentes categorias:

- Instruções;
- Branch;
- Complexidade;
- Linhas;
- Métodos;
- Classes;

Na legenda, o “C” significa “*Coverage*” e o “M” significa “*Missed*”. Assim, conseguimos observar o quão coberto o código está através dos testes unitários realizados na aplicação em relação a categorias e não apenas linhas.

Assim, é possível focar esforços de desenvolvimento dos testes unitários a trechos de códigos com baixa cobertura, tendo explícito quais classes e métodos possuem uma menor cobertura.

![img](https://miro.medium.com/max/60/0*Rw3_rC6MTZ00LJDc?q=20)

![img](https://miro.medium.com/max/346/0*Rw3_rC6MTZ00LJDc)

Overall Coverage Summary — Dados exclusivos por Build

**3- Coverage Breakdown By Package**

Nesse gráfico, são demonstradas as informações no mesmo formato que o relatório anterior, mas agora serão descritas por pacotes.

![img](https://miro.medium.com/max/60/0*sxxzyydggbPDL1i6?q=20)

![img](https://miro.medium.com/max/610/0*sxxzyydggbPDL1i6)

Coverage Breakdown — Cobertura de Testes por pacote

Ao clicar em um pacote, haverá um detalhamento histórico dos builds desse pacote, assim como na visão do relatório *“Coverage Trend”.* Nessa visão, conseguimos verificar o histórico da cobertura dos testes de um pacote pelo número de linhas do mesmo ao longo dos builds do projeto.

![img](https://miro.medium.com/max/60/0*RuDApfYZzNQF2rn6?q=20)

![img](https://miro.medium.com/max/412/0*RuDApfYZzNQF2rn6)

Cobertura de testes (histórico) por linhas de código de um pacote

Há também a possibilidade de detalhar um pouco mais essa cobertura, acessando o pacote e demonstrando os o relatório por arquivos, detalhando cada arquivo em específico.

![img](https://miro.medium.com/max/60/0*AUZJL6fynkjQINmq?q=20)

![img](https://miro.medium.com/max/630/0*AUZJL6fynkjQINmq)

Cobertura de testes por aquivo

É possível também visualizar os trechos de código cujo os testes unitários cobriram e quais não tiveram cobertura, entrando cada vez mais nos detalhes da cobertura.

![img](https://miro.medium.com/max/60/0*LyrAo5-SSkJuEPk4?q=20)

![img](https://miro.medium.com/max/596/0*LyrAo5-SSkJuEPk4)

Cobertura de Testes em um arquivo

# **Visão Geral dos Projetos**

Na visão geral dos projetos no Jenkins, há a possibilidade de adicionar uma coluna informativa relacionada a cobertura dos testes a nível de número de linhas, informando o resultado do último Build (em percentual de cobertura). Isso demonstra uma visão mais macro da cobertura total dos testes a nível de projetos, podendo avaliar os dados e focar esforços nos projetos que possuem uma menor cobertura.

![img](https://miro.medium.com/max/60/0*9WQZsZpSXoHFRppz?q=20)

![img](https://miro.medium.com/max/630/0*9WQZsZpSXoHFRppz)

Percentual de Cobertura de Testes na visão de projetos no Jenkins

# **Conclusão**

O JaCoCo Plugin apresentou ser a melhor opção por sua facilidade em configurações e simplicidade na demonstração dos dados. A forma como são demonstrados os dados é de fácil interpretação e um histórico é gravado ao longo do tempo.

Enfim, o objetivo proposto com essa integração é melhorarmos a cada dia a cobertura dos testes unitários e consequentemente diminuirmos o número de bugs no sistema, aumentando cada vez mais a visibilidade dos testes ao longo dos Builds executados dos projetos.

# **Links e Referências**

[https://www.devmedia.com.br/automatizando-a-geracao-de-pacotes-com-o-jenkins/33655#:~:text=O%20Jenkins%20C.I.,de%20um%20projeto%20de%20software](https://www.devmedia.com.br/automatizando-a-geracao-de-pacotes-com-o-jenkins/33655#:~:text=O Jenkins C.I.,de um projeto de software).

https://medium.com/@allyxcristiano/jenkins-from-zero-to-deploy-e54a627f055a

[https://medium.com/assertqualityassurance/teste-unit%C3%A1rio-e-qualidade-de-software-acce7b9c537](https://medium.com/assertqualityassurance/teste-unitário-e-qualidade-de-software-acce7b9c537)

https://www.jenkins.io/blog/2018/08/17/code-coverage-api-plugin-1/