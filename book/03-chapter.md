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

# Oque podemos passar para uma função.

podemos passar boolean, strings, números e variáveis.

# parametros x argumentos.

quando definimos uma função podemos especifar os parametros e na chamada da função vamos colocar os argumentos

DEFINIÇÃO DA FUNÇÃO
````
function cook(degrees, mode, duration) {
// your code here
}
````
CHAMADA DA FUNÇÃO
````
cook(425.0, "bake", 45);
````

# passagem por valor.

é muito importante entender a passagem de valores para uma função no javascript essa passagem é feita pass by value.
se criarmos uma variável
````
var age = 10;
````
e declararmos uma função que adiciona 1 ao valor passado
````
function addOne(x) {
  x = x + 1;
}
````
e agora passarmos a variável na chamada da função
````
addOne(age);
````
vamos entender o que acontece aqui, o valor de age não sera alterado o que vai ser alterado é o valor x o valor de age é copiado para a variável x
que está como parametro da função addOne, na execução da função o valor de x é alterado e o valor de age se mantem.

# um pouco mais sobre argumentos de função.

se passarmos menos argumentos do que a função tem como parametro os argumentos que não foram passados se tornam undefined:
````
function makeTea(cups, tea) {
console.log("Brewing " + cups + " cups of " + tea);
}
makeTea(3);
//console : Brewing 3 cups of undefined
````

se passarmos mais argumentos do que a função tem como parametro os argumentos a mais serão ignorados:
````
function makeTea(cups, tea) {
console.log("Brewing " + cups + " cups of " + tea);
}
makeTea(3, "Earl Grey", "hey ma!", 42);
//console : Brewing 3 cups of Earl Grey
````

se a função não tiver parametros, ah isso é normal :
````
function barkAtTheMoon() {
console.log("Woooooooooooooo!");
}
barkAtTheMoon();
//console : Woooooooooooooo!
````

# funções podem retornar valores
funcções podem retornar valores como por exemplo
````
function calculaIdade(idade) {
  var message = "";
  if(idade > 18) {
    message = "idade é maior que 18";
  } else {
    message = "idade menor que 18";
  }
  return message;
}

calculaIdade(20);
````
e aqui chegamos a um ponto importante a variável ````message```` ela é local e só é acessível no escopo da função.
##Global e Local variáveis

se declaramos uma variável fora da função ela é global e pode ser acessada em qualquer parte do código, mas quando declaramos uma variável
dentro de uma função ela é local sendo ela acessível apenas dentro da função que foi declarada.
107
