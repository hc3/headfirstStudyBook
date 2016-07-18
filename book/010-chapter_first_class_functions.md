## funções de primeira classe

First Class Functions
- as funções em javascript podem ser declaradas de duas formas:
Function declaration :
````
function quack(num) {
  for (var i = 0; i < num; i++) {
    console.log("Quack!");
  }
}
quack(3);
````
Function experession :
````
var fly = function(num) {
  for (var i = 0; i < num; i++) {
    console.log("Flying!");
  }
};
fly(3);
````
Aqui podemos pensar que temos apenas mais do mesmo, já que no final são duas funções que irão fazer o que lhes foi mandado, então qual é a diferença entre function declaration e function expression?, veja bem a function declaration ela é lida antes do código vamos entender bem isso aqui, quando o browser é carregado as functions declarations são lidas e carregadas no caso a cima seria criado uma variável **quack** que receberia a referência para função, mas isso seria feito antes do browser carregar qualquer parte do código, na function expression não o valor para a variável fly será a referência para função anonima para qual a mesma foi atribuida, mas esse valor só será criado após o código ser lido.

<h5> Funções são valores! </h5>

quando criamos uma função seja com function declaration ou function expression estamos declarando uma variável que irá ser a referência para acessarmos essa função, então podemos atribuir funções a variáveis.

````
function quack(num) {
  for (var i = 0; i < num; i++) {
  console.log("Quack!");
  }
}

var fly = function(num) {
  for (var i = 0; i < num; i++) {
  console.log("Flying!");
  }
}

var superFly = fly;
superFly(2);

var superQuack = quack;
superQuack(3);
````
declaramos novamente as duas funções sendo a primeira uma function declaration e a segunda uma function expression, nos dois casos serão criadas duas variáveis **quack** e **fly** que irão armazenar as referências para suas respectivas funções, depois passamos a referência que está na variável **fly** para **superFly** e invocamos **superFly** usando os parênteses, depois fazemos o mesmo com a variável **quack** o que quero que seja entendido aqui é que **referências são apenas referências tanto com declarations ou experessions**

<h5> Funções de primeira classe Javascript! </h5>
vimos anteriormente que funções são valores em javascript, podendo ser atribuidas as suas referências as variáveis, mas funções são executadas e ai que está a difereça entre funções e valores, podemos passar funções para variáveis, retornar funções de dentro de funções, armazenar objetos e arrays em funções, passar funções por paramêtro para outras funções.
**FIRST CLASS FUNCTIONS** esse é o termo usado para denomoinar esse tipo de função que tem:

* Atribuir o valor da função a variável ou armazenear em arrays e objetos.
* Passar por parâmetro para outras funções
* Retornar funções de dentro de funções.
