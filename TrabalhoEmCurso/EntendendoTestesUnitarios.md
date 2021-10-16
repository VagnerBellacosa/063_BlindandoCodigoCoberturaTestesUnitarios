# Entendendo os Testes Unitários

por [Fernando Sousa](https://souforce.cloud/author/fernando-sousasouforce-cloud/) | 2 setembro, 2017 | [Apex](https://souforce.cloud/categorias/apex/), [Beginner](https://souforce.cloud/categorias/salesforce/beginner/), [IDE](https://souforce.cloud/categorias/ide/), [Salesforce](https://souforce.cloud/categorias/salesforce/), [Salesforce Developer](https://souforce.cloud/categorias/salesforce/salesforce-developer/), [Trailhead](https://souforce.cloud/categorias/trailhead/) | [0 Comentários](https://souforce.cloud/entendendo-os-testes-unitarios/#respond)

![img](https://souforce.cloud/wp-content/uploads/2017/09/trailblazer.jpg)

Se você é um [desenvolvedor Salesforce](https://souforce.cloud/categorias/salesforce/salesforce-developer), posso afirmar que você já sofreu com a cobertura de 75% dos testes unitários exigidas pelo Salesforce, não é mesmo?

O Apex nos fornece uma estrutura de teste que nos permite escrever testes unitários, executar os testes, verificar resultados dos testes unitários e também ver o resultados de cobertura de código.

 

### **Entendendo os Testes Unitários**

Testes são sem dúvidas a chave para o sucesso da sua aplicação. Os testes unitários nos permite validar que tudo funciona como esperado, evitando assim comportamentos inesperados, recomento fortemente que você use um processo de desenvolvimento orientado a testes, ou seja, faça o desenvolvimento dos seus testes unitários ao mesmo tempo que realiza o desenvolvimento dos seus códigos, evitando ao máximo deixar tudo para última hora.

Existem duas maneiras de realizar um teste na sua aplicação. Uma delas é através da interface do usuário do Salesforce, que sem dúvida é muito importante, mas apenas o teste através da interface do usuário não irá capturar todos os casos de uso do seu sistema. O outro caminho é testar a funcionalidade de forma automatizada, ou seja, escrever um código de testes que passe por todo o código que você escreveu, ou ao menos boa parte dele, acredite, você vai comemorar sempre que conseguir atingir 100% de cobertura nos seus testes unitários, rs.

Podemos dizer que um sistema raramente está concluído. Você terá versões adicionais, e muita, mas muitas melhorias e novas funcionalidade. Se você escreveu os testes unitários para todas as classes e triggers que criou até entregar a primeira versão do seu sistema, então você poderá garantir que nenhum novo problema surgirá, ao realizar a inclusão de uma nova funcionalidade, afinal você não vai querer ouvir do seu cliente ou chefe, “*mas isso estava funcionando antes!* Depois que você mexeu parou de funcionar!”.

Antes que você possa implantar seu código em produção ou criar um pacote para distribuir o seu aplicativo na [AppExchange](https://appexchange.salesforce.com/), tenha em mente que:

- Pelo menos 75% do seu código Apex deve ser coberto por testes unitários, e todos esses testes devem ser concluídos com sucesso.

  Observe o seguinte.

  - Ao implantar o Apex para uma organização de produção, cada teste de unidade no namespace da sua organização é executado por padrão.
  - Chamadas para **System.debug** Não contam como parte da cobertura do código Apex.
  - Os métodos de teste e as classes de teste não são contados como parte da cobertura do código Apex.
  - Pelo menos 75% do seu código Apex deve ser coberto por testes, seu foco não deve estar na porcentagem do código coberto. Em vez disso, você deve certificar-se de que cada caso de uso do seu sistema esteja coberto, incluindo casos positivos e negativos, bem como registros em massa e únicos. Isso deve levar a 75% ou mais do seu código.

- Todas as triggers devem ter alguma cobertura de teste.

- Todas as classes e triggers devem ser compilados com sucesso.

O **Salesforce** executa todos os testes em todas as organizações que possuem código Apex para verificar se nenhum comportamento foi alterado antes de realizar qualquer atualização na Plataforma.

 

### **Mas afinal, o que Testar?**

O Salesforce recomenda que você escreva testes para:

###### **Ação única**

Teste para verificar se um único registro produz o resultado esperado.

###### **Ações em massa (Bulk)**

Qualquer código Apex, seja uma trigger, uma classe ou uma extensão, pode ser invocado de 1 a 200 registros. Você deve testar não só o caso de registro único, mas também os casos em massa.

###### **Comportamento positivo**

Teste para verificar se o comportamento esperado ocorre através de todas as permutações esperadas, ou seja, que o usuário completou tudo corretamente e não ultrapassou os limites da plataforma, você pode encontrar a tabela completa com os [limites do Apex aqui](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_gov_limits.htm).

###### **Comportamento negativo**

A plataforma Salesforce [impõe alguns limites](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_gov_limits.htm), você deve garantir que os seus testes não vão ultrapassar esses limites, por exemplo uma única chamada APEX não pode realizar mais do que 100 consultas SOQL. Você deve testar o caso negativo e verificar se as mensagens de erro são produzidas corretamente, bem como para os casos positivos, dentro dos limites.

###### **Usuário restrito**

Teste se um usuário com acesso restrito aos sObjects usados em seu código vê o comportamento esperado. Ou seja, se eles podem executar o código ou receber mensagens de erro.

> Os operadores condicionais e ternários não são considerados executados, a menos que os ramos positivo e negativo sejam executados.

 

### **Melhoras Praticas**

- Se o código usa lógica condicional (incluindo operadores ternários), você deve execute cada ramo.

- Faça chamadas para métodos que utilizem entradas válidas e inválidas.

- Complete com sucesso sem lançar exceções, a menos que esses erros sejam esperados e capturados em um try… catch.

- Manuseie sempre todas as exceções que são capturadas, em vez de apenas capturar as exceções.

- Evite ao máximo utilizar nos seus códigos:

  | 123  | **if** (!Test.isRunningTest()) {  *//Do something*} |
  | ---- | --------------------------------------------------- |
  |      |                                                     |

- Use os métodos  System.assert para provar que o resultado do seu código se comporta adequadamente.

- Use o runAs como método para testar seu aplicativo em diferentes contextos de usuário.

- Nos testes de trigger em massa – use pelo menos 20 registros em seus testes.

- Use o ORDER BY para garantir que os registros sejam retornados na ordem esperada.

- Nunca considere que as IDs de registro estão em ordem seqüencial.

- Evite ao máximo a execução de testes utilizando a anotação:

  | 1    | *@isTest*(SeeAllData=**true**) |
  | ---- | ------------------------------ |
  |      |                                |

  

  

- As IDs de registro não são criadas em ordem crescente, a menos que você insira vários registros com a mesma solicitação. Por exemplo, se você criar uma conta A e receber a ID001D000000IEEmT, então crie a conta B, a ID da conta B pode ou não ser seqüencialmente maior.

- Configurar dados de teste:

  - Crie os dados necessários nas classes de teste, portanto, os testes não precisam confiar em dados em uma determinada organização.
  - Crie todos os dados de teste antes de chamar o método  Test.startTest.
  - Você não precisará excluir nenhum dado criado no seus testes, o Apex se encarrega de fazer isso sozinho, a menos que seja um teste de remoção de registro.

- Teste as classes em sua aplicação individualmente. Nunca teste sua aplicação inteira em um único teste.

 

No post de hoje, vimos um pouco das considerações do Salesforce sobre testes, e porque devemos realizar eles, no próximo post, vou trazer exemplos práticos de testes unitários, mas, se não quer esperar até lá, da uma olhada no post que falo sobre [como criar um Mock para as chamadas Http](https://souforce.cloud/implementando-o-httpcalloutmock-nos-seus-testes-unitarios/) nos seus testes unitários.

[![img](https://souforce.cloud/wp-content/uploads/2017/09/Trailhead_Apex_Test.png)](https://trailhead.salesforce.com/content/learn/modules/apex_testing)

Sugiro ainda, que você de uma olhada no Trailhead, existe [um módulo especifico para Testes Apex](https://trailhead.salesforce.com/content/learn/modules/apex_testing), se você ainda não sabe o que é Trailhead, então de uma olhada no post que falo [um pouco mais sobre o Trailhead](https://souforce.cloud/porque-voce-deve-fazer-o-trailhead/).

 

Um forte abraço e até o próximo post :)

![Fernando Sousa](https://souforce.cloud/wp-content/uploads/2018/11/48363146_2083149215085558_8462956108686819328_o.jpg)

#### Fernando Sousa

Senior Salesforce Developer

**Bacharel em Sistemas da Informação** pela *Universidade de Taubaté (UNITAU) e* **MBA** em **Projeto de Aplicações para Dispositivos Móveis** pelo *IGTI – Instituto de Gestão em Tecnologia da Informação*. 

Comecei a programar bem cedo, por volta de 10 anos de idade, de maneira auto-didata passei por várias linguagens.

Em 2015 me conectei a plataforma **Salesforce** pela primeira vez, para fazer una integração entre um **Aplicativos Mobile** em android e o **Salesforce Platform.** 

Atualmente com as certificações [**Salesforce Certified Platform Developer I**](https://trailblazer.me/id/ifernandosousa), [**Salesforce Certified Platform App Builder**](https://trailblazer.me/id/ifernandosousa), [**Salesforce Certified Platform Developer II**](https://trailblazer.me/id/ifernandosousa), **[Salesforce Administrator](https://trailblazer.me/id/ifernandosousa) e [Sharing and Visibility](https://trailblazer.me/id/ifernandosousa).**

Acompanhe meu [Trailhead aqui](https://trailblazer.me/id/ifernandosousa).