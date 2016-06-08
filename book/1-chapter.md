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
````
var idade = 25;

if(idade > 18) {
  alert("maior de idade!");
} else {
  alert("menor de idade");
}
````
algo interessante do javascript é que não é uma linguagem fortemente tipada onde precisamos declarar o tipo da variável, no javascript a variável ela tem
a função de "guardar valores" como por exemplo
````
var idade = 10;
var nome = "jose";
var isValid = true;
````
cada variável recebeu um valor idade recebeu 10 como seu valor nome recebeu jose e isValid recebeu true e a declaração da variável e feita nesse padrão
palavra reservada **var** seguida do nome da variável sinal de igualdade e o valor a ser atribuido a essa variável e por fim o nosso amado **;**, mas é
claro que pode ser opcional podemos declarar uma variável assim ```` var idade; ```` sem incializar, o nome das variáveis não pode inciar com números 
ou ser alguma das palavras reservadas do javascript que é uma lista que você encontra fácil na [web](www.google.com.br).

PAGINA 13 -