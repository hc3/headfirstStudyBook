# Introdução..

javascript inicialmente criado para executar no browser e criar interações para páginas estaticas na web, para executar um código javascript no seu html
usamos a tag **<script></script>**.
````html
<script>
  alert("Hello World");
</script>
````
### como fazer uma declaração de variável.

quando criamos componentes html normalmente fazemos marcações onde queremos editar por exemplo
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
com o javascript podemos criar declarações que podem por exemplo fazer uma verificação 
````js
var idade = 25;

if(idade > 18) {
  alert("maior de idade!");
} else {
  alert("menor de idade");
}
````
algo interessante do javascript é que não é uma linguagem fortemente tipada onde precisamos declarar o tipo da variável, no javascript a variável ela tem
a função de "guardar valores" como por exemplo
````js
var idade = 10;
var nome = "jose";
var isValid = true;
````
cada variável recebeu um valor idade recebeu 10 como seu valor nome recebeu jose e isValid recebeu true e a declaração da variável e feita nesse padrão
palavra reservada **var** seguida do nome da variável sinal de igualdade e o valor a ser atribuido a essa variável e por fim o nosso amado **;**, mas é
claro que pode ser opcional podemos declarar uma variável assim ```` var idade; ```` sem incializar, o nome das variáveis não pode inciar com números 
ou ser alguma das palavras reservadas do javascript que é uma lista que você encontra fácil na [web](www.google.com.br).

### Loop e estruturas condicionais 

o javascript tem também algumas formas de executar loops ou decisões.
<h3>while</h3>
````js
var idade = 1;
while(idade < 18) {
  alert("menor de idade");
  idade = idade + 1; // ou idade++
}
````
a estrutura while faz uma pergunta enquanto a idade for menor que 18 o bloco de código que está entre as chaves sera executado, podemos notar também que
a variável que da condição para que o loop seja executado é incrementada a cada volta do loop isso é feito para não gerar um loop infinito dado que se a
idade for sempre menor que 18 a função alert sera chamada infinitas vezes.

<h3>if</h3>
````js
if(idade < 18) {
  alert("menor de idade");
} else if(idade > 60) {
  alert("idoso");
}
````
a condicional if ou se, faz outra pergunta se idade é menor que 18 então execute o primeiro bloco se não se for maior que 60 execute o segundo bloco essa
condicional diferente do loop while executa apenas uma vez não sendo necessário incrementar a variável idade.

### Resumo

Capitulo de introdução bem leve, fala sobre variáveis e como declarar e atribuir valores as mesmas, faz uma pequena introdução aos loops e condições.