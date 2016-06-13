#Introdução a funções

nesse capitulo sera abordado de forma inicial o assunto de funções que podemos dizer ser o mais importante da linguagem javascript, aqui vamos entender
onde as funções nos ajudam com reuso de código, deixando o código mais gerenciavel e abstrato, será um capitulo introdutório mas esse é um assunto que
será muito abordado nos próximos capitulos.

vamos analisar esse código :

````
var dogName = "rover";
var dogWeight = 23;
if (dogWeight > 20) {
    console.log(dogName + " says WOOF WOOF");
} else {
    console.log(dogName + " says woof woof");
}
dogName = "spot";
dogWeight = 13;
if (dogWeight > 20) {
    console.log(dogName + " says WOOF WOOF");
} else {
    console.log(dogName + " says woof woof");
}
dogName = "spike";
dogWeight = 53;
if (dogWeight > 20) {
    console.log(dogName + " says WOOF WOOF");
} else {
    console.log(dogName + " says woof woof");
}
dogName = "lady";
dogWeight = 17;
if (dogWeight > 20) {
    console.log(dogName + " says WOOF WOOF");
} else {
    console.log(dogName + " says woof woof");
}
````
podemos ver no código acima o quanto ele se repete sem motivo, temos uma estrutura condicional que testa se a altura do dog é maior que 20 sendo ela verdadeira
o o latido do cachorro é alterado de minúsculo para maiúsculo, e porque tem que ser assim e se tivessemos que fazer isso para 1500 dogs? é ai que entra a função

<b>aqui temos uma função</b>
````
function bark(name, weight) {
  if (weight > 20) {
    console.log(name + " says WOOF WOOF");
  } else {
    console.log(name + " says woof woof");
  }
}

bark("rover", 23);
bark("spot", 13);
bark("spike", 53);
bark("lady", 17);
````
isolamos o código que se repete em uma função a cada chamada da função alteramos os valores a função recebe como parâmetros o name e weight e faz uma comparação
e retorna um console log, deu pra notar o quanto que o código ficou mais fácil de ler entender e usar, pois bem essa é a função ou functions.

# Oque podemos passar para uma função



