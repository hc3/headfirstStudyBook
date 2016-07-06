# Entendendo melhor os tipo de dados

-Tipos de dados em javascript, como já vimos nos capitulos anteriores o javascript possui tipo básicos como String, Numbers e Boolean e tem os Objetos
em javascript tudo são objetos, existe também NaN , undefined , null. e nesse capitulo vamos desvendar esse tipos de dados.

## undefined

  se acessarmos uma variável que não foi inicializada ou uma propriedade inexistente ou que foi deletada ou uma posição que não existem em um array vamos
receber o valor undefined, e podemos entender o undefined como um valor retornado quando algo não foi inicializado, segue o exemplo:

````js
var x;

if(x == undefined) {
  // x é undefined pois não foi incializada.
}
````

````js
var carro = {
  cor = "vermelho"
}

if(carro.ano == undefined) {
  // a propriedade ano não existe no objeto carro então é undefined
}
````

  quando não temos certeza se uma variável foi realmente inicializada ou uma propriedade que pode não existir em um objeto, devemos fazer a verificação
se o valor é undefined, o valor undefined é um tipo mas não é nem uma string, numero ou boolean, undefined é undefined.
existe o operador <b>typeof</b> que com esse operador conseguimos saber o tipo de uma variável como no exemplo:

````js
var cor = "vemelho"

var tipoCor = typeof cor;

console.log(tipoCor) 
// string
````

  criamos uma variável e atribuimos uma string a ela com o operador <b>typeof</b> conseguimos saber o tipo que no caso acima é uma string.

## null

  o null é bem parecido com undefined o que pode causar uma certa confusão, por exemplo quando tentamos pegar um elemento DOM com o getElementById
se esse elemento não existir a função vai retornar null, isso porque não existe o objeto, null é usado para objetos que não existem e undefined para 
pripriedade do objeto, na maioria das vezes vamos nos deparar com undefined, null vai ser o valor retornado por funções que retornam um objeto se esse
objeto não existir a função retornará null.

## NaN

  Not a Number ( não é um número ) podemos pensar em quando divimos 0/0 temos um NaN ou se multiplicarmos uma string "jose" * 20 temos um NaN, quando
o javascript não reconhece como um número existente ele retorna NaN ou seja NaN é usado para representar valores númericos que não podem ser representados
NaN é diferente de NaN ````js NaN != NaN ```` ou seja não é com um teste condicional usando if que testamos se é NaN, porque NaN não é igual a nada.
exemplo:

````js
if(myNum == NaN) {
  //vai dar merda aqui porque NaN é != de NaN
}
````

para testa se o valor é NaN usamos uma função especial chamada isNaN, exemplo;

````js
if(isNaN(myNum) {
  //opaaa agora simmm!
}
````

vamos não pense que NaN não é do tipo Number, segue o exemplo:

````js
var teste = 0/0

console.log(typeof teste)
//Number
````

## Operadores de igualdade  "==" e "==="

  como comprar valores no javascript? primeiro vamos ter o operador == que comprar se um valor é igual ao outro por exemplo:
  
````js
var n = 99;

if(n == 99) {
  // tudo tranquilo...
}
````

````js
var n = "99";

if(n == 99) {
  // tudo favorável...
}
````

veja que no exemplo acima mesmo usando uma string o javascript é esperto o suficiente para saber que a string "99" é igual o número 99, mas como?
o javascript faz uma pergunta os valores são do mesmo tipo e são iguais? se sim retorna true e se os valores não forem do mesmo tipo mas forem iguais?
ai ele converte e retorna true então o "99" fica 99 mesmo sendo uma string ele consegue fazer isso por nós, vamos aos exemplos:

comparar número e string
javascript converte a string para um número a string se torna um NaN que não é igual a 99
````js
99 == "vermelho"

99 == NaN

// false
````

compara boolean com outro tipo
nesse caso é algo simples de entender já que true = 1 e false = 0 então ele converte o número para boolean e testa.
````js
1 == true

1 == 1

// true
````
outro exemplo
nesse caso o boolean é convertido pra número depois a string é convertida pra número e então podemos comparar os dois.
````js
"1" == true

"1" == 1

1 == 1

// true
````

comprar null com undefined
e aqui temos que undefined e null são iguais ( haha ).
````js
undefined == null

// true
````

comprar número e string vazia
a string  vazia é convertida pra 0 e depois pode ser comprada com o número 1.
````js
1 == ""

1 == 0

// false
````

o operador == pode gerar retornos inesperados, se não entermos bem seu funcionamento.

  o segundo operador é o strict equality "===", isso mesmo três... com o operador "==" os valores são convertidos quando for preciso, com o operador "==="
  não eles tem que ser estritamente iguais tem que ter o mesmo <b>tipo</b> e o mesmo <b>valor</b>.
  
# contatenação 

  vamos falar um pouco sobre o operador + ( adição ) que é usado também para contatenar strings, e se tivermos um número e uma string usando o operador +
como que faz? então com o operador + tem que comprar feito porque ele vai converter então vamos ver como:

````js
var add = 3 + "4"  // aqui temos 34  haha

var add2 = "4" + 3 // aqui temos 43 haha
````

se colocarmos uma string e um número e usarmos o operador + ele vai na verdade converter o número em string e contatenar as duas strings resultantes
vamos ententer complicando um pouco a aritmética.

````js
var mult = 3 * "4" // 12

var div = 80 / "10" // 8

var mini = "10" - 5 // 5
````

pois é doidera vamos dizer que se usarmos o operador + o número vai ter preferencia de ser convertido, mas se usarmos os demais operadores, a string 
é que vai ser convertida.

# Objetos 

   e como determinar se dois objetos são iguais? quando vimos os operadores "==" e "===" entendemos a diferença entre os dois para se comprar valores 
mas quando a questão são objetos não importa, vai dar na mesma quanto testamos se dois objetos são iguais estamos testando se eles tem a mesma referencia
então se temos o obj1 e obj2 e as variáveis v1 para obj1 e b2 para obj2 v1 e v2 são diferentes pois são variáveis com referencia para dois objetos diferentes
mais ai criamos a variável v3 e referenciamos o obj1 e agora comparamos v1 e v3 são iguais!

# O que o javascript considera falso

  por padrão os valores falsos são
  
  undefined é falso.
  null é falso.
  0 é falso.
  string vazia é falso.
  NaN é falso.
  false é falso.
  
e para todos os outros o valor sera verdadeiro.

# Strings

  em javascript existem os tipo primitivos e os objetos, os primitivos são básicos eles recebem um valor e pronto, já os objetos são mais complexos além
de ter um valor eles podem também ter comportamentos, vamos um exemplo.

````js
var emot = "XOxxOO";
var hugs = 0;
var kisses = 0;
emot = emot.trim();
emot = emot.toUpperCase();
for(var i = 0; i < emot.length ; i++) {
  if (emot.charAt(i) === "X") {
    hugs++;
  } else if (emot.charAt(i) == "O") {
    kisses++;
  }
}
````
mais o que é isso se a string é um valor primitivo o que são esses métodos? <b>trim()</b>,<b>toUpperCase()</b>,<b>chatAt</b>? isso porque o javascript
suporta ambos a string tanto é um valor primitivo como um objeto, veja o exemplo:

````js
var name = "Jenny";
var phone = "867-5309";
var fact = "This is a prime number";
var songName = phone + "/" + name;
var index = phone.indexOf("-");
if (fact.substring(10, 15) === "prime") {
    alert(fact);
}
````
criamos três variáveis do tipo string, nesse momento são três valores primitivos depois criamos a variável <b>songName</b> que vai contatenar as strings
quando criamos a variável index, a variável phone que era um tipo primitivo é temporáriamente convertida para um objeto String e assim conseguimos acessar
o método indexOf desse objeto na linha subsequente temos a variável fact que sofre o mesmo processo e acessa o método substring e no final temos um alert
onde a variável fact voltou a ser um valor primitivo do tipo string.
confuso? hehe eu também fiquei quando li pela primeira vez, mas veja bem não precisamos nos preocupar com nada disso ao criarmos uma string temos que ter
em mente que temos um tipo com super poderes o javascript vai cuidar de todo o resto.

não vou me aprofundar nos métodos da String pq isso aqui é apenas um resumo e pra quem quiser saber mais é só procurar na web.