# Introdução..

javascript inicialmente criado para executar no browser e criar interações para páginas estaticas na web, para executar um código javascript no seu html devemos usar a tag **<script></script>** e partir da ai já temos uma iteração entre as páginas.
````html
<script>
  alert("Hello World");
</script>
````

### como fazer uma declaração de variável.

quando criamos componentes html normalmente fazemos marcações onde queremos editar criando uma class, e com isso acessamos as propriedades de estilo de qualquer tag e aplicados estilo a ela usando css.

````html
<h1 class="top">Aqui temos um cabeçalho marcado com a classe top</h1>
<p>esse cabeçalho pode ser alterado usando css </p>
<style>
h1.top {
  color:red;
}
p {
  color:blue;
}
</style>
````

dentro de uma tag script podemos fazer o mesmo com o javascript, e assim como usamos o css para aplicar estilo a elementos html usaremos o javascript para executar lógica. Com o javascript podemos criar declarações que podem por exemplo fazer uma verificação.

````js
var idade = 25;

if(idade > 18) {
  alert("maior de idade!");
} else {
  alert("menor de idade");
}
````

algo interessante do javascript é que não é uma linguagem fortemente tipada onde precisamos declarar o tipo da variável. No javascript é preciso declarar apenas o nome da variável e com isso atribuir seu valor.

````js
var idade = 10;
var nome = "jose";
var isValid = true;
````

### Loop e estruturas condicionais 

o javascript tem também algumas formas de executar loops ou decisões.

>while

````js
var idade = 1;
while(idade < 18) {
  alert("menor de idade");
  idade = idade + 1; // ou idade++
}
````

>if

````js
if(idade < 18) {
  alert("menor de idade");
} else if(idade > 60) {
  alert("idoso");
}
````

>switch

````js
switch (new Date().getDay()) {
    case 0:
        day = "Sunday";
        break;
    case 1:
        day = "Monday";
        break;
    case 2:
        day = "Tuesday";
        break;
    case 3:
        day = "Wednesday";
        break;
    case 4:
        day = "Thursday";
        break;
    case 5:
        day = "Friday";
        break;
    case 6:
        day = "Saturday";
}
````

### Resumo

Capitulo de introdução bem leve, fala sobre variáveis e como declarar e atribuir valores as mesmas, faz uma pequena introdução aos loops e condições.
