# Cobertura de Código - Só para testes unitários?

Antes de discutir cobertura de código, uma rápida recapitulação:

- **Cobertura de código**: Uma métrica que indica a efetividade dos testes feitos em uma aplicação. Expressa em termos de porcentagem do código-fonte da aplicação, mostra extaamente o quanto da aplicação foi testada durante uma dada bateria de testes;
- **Testes Unitários**: Pequenas rotinas (tipicamente escritas na mesma linguagem de programação do sistema que será testado) que descrevem regras de negócios e outros comportamentos conhecidos e esperados do sistema. Os testes unitários invocam rotinas e outras pequenas porções de código do sistema-alvo, suprindo parâmetros com valores pré-definidos e analisando o comportamento resultante, que deve estar de acordo com a regra de negócio ou comportamento esperado em questão.

Para que os testes unitários sejam efetivos, eles devem cobrir o maior número possível de “caminhos” no código da aplicação. A cobertura de código visa a responder justamente o quanto desses caminhos foi realmente testado. Veja um exemplo (totalmente fictício, hein?!) que ilustra tudo isso:

**Regra de Negócio:** _Para o cálculo do salário líquido de um funcionário, dados:_ 1. _O valor do salário bruto; _ 2. _Um "flag" indicando a adesão ao plano de saúde; _ 3. _Um "flag" indicando a adesão ao vale-refeição;_ _Deve ser efetuado o seguinte cálculo:_ 1. _Descontar o imposto de renda de acordo com com as seguintes faixas: _ 1. _R$0 - R$1000: Isento; _ 2. _R$1001 - R$2000: 5%;_ 3. _R$2001 - R$3000: 15%;_ 4. _R$3001 em diante: 25._ 2. _Descontar 10% de INSS;_ 3. _10% do salário bruto, caso tenha aderido ao plano de saúde; _ 4. _5% do salário bruto, caso tenha aderido ao vale-refeição._ **Código-fonte da aplicação:** 1: public class Empregado </br> 2: { </br> 3: public static double CalcularSalario(double salarioBruto, bool temPlanoSaude, bool temValeRefeicao) </br> 4: { </br> 5: var salarioLiquido = salarioBruto; </br> 6: </br> 7: // Cálculo do imposto de renda </br> 8: </br> 9: if (salarioBruto > 1000 && salarioLiquido <= 2000) </br> 10: { </br> 11: salarioLiquido -= (salarioBruto * .05); </br> 12: } </br> 13: else if (salarioBruto > 2000 && salarioBruto <= 3000) </br> 14: { </br> 15: salarioLiquido -= (salarioBruto * .15); </br> 16: } </br> 17: else if (salarioBruto > 3000) </br> 18: { </br> 19: salarioLiquido -= (salarioBruto * .25); </br> 20: } </br> 21: </br> 22: // Cálculo do plano de saúde </br> 23: </br> 24: if (temPlanoSaude) </br> 25: { </br> 26: salarioLiquido -= (salarioBruto * .10); </br> 27: } </br> 28: </br> 29: // Cálculo do vale-refeição </br> 30: </br> 31: if (temValeRefeicao) </br> 32: { </br> 33: salarioLiquido -= (salarioBruto * .05); </br> 34: } </br> 35: </br> 36: return salarioLiquido; </br> 37: } </br> 38: } **Teste Unitário:** public void CalcularSalarioTest() { // "Valores conhecidos". São arbitrários; posso usar qualquer valor double salarioBruto = 1500; bool temPlanoSaude = false; bool temValeRefeicao = true; // "Valor esperado". Deve estar de acordo com a regra de negócio e com // os valores dados acima double expected = 1350; // "Valor real". É o valor que será retornado pela minha rotina de cálculo; // se tudo der certo, deve ser igual ao "valor esperado" double actual; // Executa a rotina passando os valores acima como parâmetros actual = Empregado.CalcularSalario(salarioBruto, temPlanoSaude, temValeRefeicao); // Confere se os resultados ("valor esperado", "valor real") são iguais; se forem, // o teste é considerado bem-sucedido Assert.AreEqual(expected, actual); }

Compare a regra de negócio, o código-fonte da aplicação e o teste unitário:

- A rotina de cálculo está atendendo a todas as premissas da regra de negócio? No exemplo acima, sim.
- O teste unitário está testando todas as variações possíveis da rotina de cálculo? No exemplo acima, não está:
  - Não foram feitos testes para todas as faixas de salários (para garantir que o IRPF está sendo calculado corretamente);
  - Não foram testadas outras variações para “plano de saúde” e “vale-refeição”.

É justamente nesse momento que entra a cobertura de código. Ela nos ajuda a identificar quais pontos da rotina não foram testados:

[![image](http://nlj65q.blu.livefilestore.com/y1poI8emIhb0ejPZ9ov4-Q8nP7Q8KFKorXAbmC6LEBmG6vutcMq1ZhH-WTAoCAru_1E8jwGjMXQoPAkEcWuws7S4j1hrA4OH8fk?PARTNER=WRITER)](http://nlj65q.blu.livefilestore.com/y1poI8emIhb0ei5Zdo7i8tQ4_EcU7DjE_mNqwxFKImT6FwmxvDXORC9LpWV60tt2AXdeLvUam6mhlW8OfRMpiOcqvxrPc7h9KN4?PARTNER=WRITER)

Viu? A cobertura de código é quase indispensável quando estamos trabalhando com testes unitários. Ela nos dá a medida da eficácia do teste que escrevemos e acabamos de executar. Daí vem uma dúvida bastante comum quando discutimos cobertura de código e testes unitários no Team System. Tipicamente esses dois recursos são mostrados em conjunto - e por isso há quem acredite que são parte da mesma funcionalidade, e que portanto cobertura de código significa “porcentagem do código testado pelos *testes unitários*”, quando na verdade significa “porcentagem do código ***testado\***”!

# Cobertura de Código e outros testes

| Veja como a cobertura de código se comporta em conjunto com alguns dos outros testes disponíveis no Team System. Para isso, crie uma solução com dois projetos: uma Web Application e um Test Project. Não se esqueça de ativar a cobertura de código para seu projeto Web Application (Test | Edit Test Run Configurations | Local Test Run): |
| ------------------------------------------------------------ | ---------------------------- | ---------------- |
|                                                              |                              |                  |

[![image](http://nlj65q.blu.livefilestore.com/y1poI8emIhb0eh3bbRs_2JSW78Oi9blKWQvLhlo9rOARLSR_eZlVXn2KdflEuJk0tZLghWS7YYpIxXL1JTsCdn8dS4-BPzzHfb-?PARTNER=WRITER)](http://nlj65q.blu.livefilestore.com/y1poI8emIhb0ehpqzAfnD2qHDrwL2O17p07YVT1V2ckdHGs_yhwwQdA2iCP5rWd2pGhx0-9QZ6ZcCGMKq5N8Ra_gb6Hmy8DXPpC?PARTNER=WRITER)

## Testes Manuais

Faça uma experiência: adicione um teste manual e execute-o. Enquanto ele estiver em execução, abra o seu web site (que deve ter sido carregado automaticamente pelo Visual Studio). Navegue à vontade pelas páginas de teste que você deve ter criado (espero que sim!). Depois, no Visual Studio, marque o teste manual como concluído:

![image](http://blu1.storage.msn.com/y1p17xCeMqAcTuwtABiHjGsK5bgJD4zQnh0VOZCpgC_Lz7r4v1IvI7BW6lhIl6WwahkNMmQm5sVA9wQnG0fJHixaXZG5vUEH_dt?PARTNER=WRITER)

| Ao clicar numa das opções acima (e em seguida em Apply) você terá concluído o teste. Inspecione agora a janela de resultado da cobertura de código (Test | Windows | Code Coverage Results). Veja como a cobertura de código foi corretamente preenchida de acordo com as páginas que você navegou: |
| ------------------------------------------------------------ | ------- | ------------------------------------------------------------ |
|                                                              |         |                                                              |

[![image](http://nlj65q.blu.livefilestore.com/y1poI8emIhb0eikbms-WAJnI7T8mh5jNg6teK3Vb1MYp4NH2he5Uc2G_ogkJqu9lPFIuTyEvr4b54mpJcobTjoILPyw6gSsZzLH?PARTNER=WRITER)](http://nlj65q.blu.livefilestore.com/y1poI8emIhb0ei7tfqCvahG4ZZTfvxYJxYqOFppgtm39y3wvoKgj_hVqW3siI8lywQGZMSzl4qo3tn4aNptL0jf1n0giX-SG7gJ?PARTNER=WRITER)

## Testes Web e Testes de Carga

Testes Web (*Web Test*) e Testes de Carga (*Load Test*) também alimentam a cobertura de código. Faça seus testes e confira!

## Outros tipos de testes

Veja como alguns dos outros tipos de teste disponíveis no Team System se comportam quanto à cobertura de código:

- **Testes Unitários de Banco de Dados**: Esses testes nada mais são que o teste unitário convencional com algumas facilidades para a execução de T-SQL. Na verdade, por baixo dos panos eles são .NET puro. Assim, se por acaso invocarem trechos da sua aplicação então a cobertura de código refletirá tal fato;
- **Testes Ordenados**: Como estes são nada mais que agrupadores de outros testes, estarão sujeitos às regras aplicáveis a cada um dos “sub-testes” que os compõem;
- **Testes Genéricos**: Esses testes existem para que possamos testar componentes não- .NET ou que sejam externos à nossa aplicação. Assim, não faz sentido esperar que esses testes “sensibilizem” a cobertura de código.

# Conclusão

A cobertura de código é um recurso muito importante da Test Edition do Visual Studio Team System, e está disponível para a maioria dos tipos de testes - não só para testes unitários. Use e abuse da cobertura de código!