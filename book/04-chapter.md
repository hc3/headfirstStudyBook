#Introdução a Arrays.

Arrays nesse primeiro momento podemos ver que os arrays em javascript podem armazenar uma coleção de valores,
diferente de uma variável que recebe um valor int,String ou boolean o array armazena uma sequencia de valores que pode ser acessada através de um index.
````js
var exArray = ["Brasil","Venezuela","EUA"];
````
"Brasil" está na posição 0 , "Venezuela" , ta na posição 1 e assim por diante podemos acessar usando a notação
````js
var arr = exArray[0];
````
esse valor pode ser atualizado também
````js
exArray[1] = "Paraguai";
````
nesse momento no lugar de "Venezuela" a primeira posição do array vai ter o valor "Paraguai".

como em outras linguagens os Arrays tem a propriedade length onde com ela podemos saber o tamanho atual do array, é claro que além dessa propriedade existem outras, que não vão ser abordadas nesse capitulo, nesse momento vamos começar a juntar conhecimentos de outros capitulos como no exemplo a seguir vamos fazer um loop percorrendo os dados de um array e exibindo na tela.
````js
var numeros = [20,25,38,40,99,80,85];
var output;

var i = 0;

while(i< numeros.length) {
  output = "olha ai os valores sendo percorridos "+i
  +" esse é o valor do index "+numeros[i] + "esse é o valor atual do array";
  console.log(output);
  i++;
}
````
