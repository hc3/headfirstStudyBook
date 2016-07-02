## Introdução a Objetos

Por mas que digam que o javascript não é uma linguagem Orientada a Objetos, e eu mesmo não sei porque de tanta zuada por conta disso, é claro que além de Orienta a Ojetos o javascript tem sua orientação a objetos baseadas em prototipos o que deixa algo meio confuso, pra alguém como eu veio do Java por exemplo, pode ser meio complicado entender os Objetos em javascript são uma coleção de chave e valor e quando essa chave receve uma função como valor temos meio que uma emulação de um método e ai a coisa fica tensa mas esse capitulo vai abordar apenas uma introdução a objetos.

## Iniciando
- como podemos pensar sobre um objeto, por exemplo um carro é um objeto e um carro tem uma cor , um tamanho , um peso , tem algumas ações como ligar, podemos criar um objeto que representa um carro assim:
````
var astra = {
  cor : "vermelho",
  ano : 199
};
````
astra é um objeto a criação de objetos em javascript se da de forma dinâmica então não precisamos de uma classe para que um objeto seja criado a partir dela.
para acessarmos o valor de uma variável podemos usar a seginte notação  <code>astra.cor</code> e para remover uma propriedade podemos usar a palavra reservada <code>delete</code>.
para entender melhor a variável astra é uma referencia para um objeto.

## Objetos e Funções
- Objetos podem ser passados por parametros para funções
````
var livro = {
	desc: "A ilha",
	author: "desconhecido",
	numPag: 300,
	tema:"Action"
};

function escolheLivros(book) {
	if(book.numPag > 250) {
		console.log("livro tem mais q 250 paginas");
	}
}

escolheLivros(livro);
````
o objeto livro foi passado para função escolheLivros(), o que foi passado foi a refencia do objeto, isso significa que se dentro dessa função alguma propriedade do objeto fosse alterada iria repercutir no objeto original segue o exemplo.

````
function alteraTema(book,newTema) {
	book.tema = newTema;
}

alteraTema(livro,"Ação");
```` 

## OH BEHAVE! comportamentos... ações "métodos".
- Sim é claro que Objetos tem ações e é claro que vamos aprender como implementar essas ações e as ações são feitas com funções como no exemplo

````
var fiat = {
	make: "Fiat",
	model: "500",
	year: 1957,
	color: "Medium Blue",
	passengers: 2,
	convertible: false,
	mileage: 88000,
	drive: function() {
		alert.log("Zoom zoom!");
	}
};

fiat.drive();
````
podemos alterar o método drive.

````
var fiat = {
	make: "Fiat",
	model: "AT200",
	year: 1990,
	color: "Black",
	passengers: 4,
	started: false,

	start: function() {
		started = true;
	},

	stop: function() {
		started = false;
	},

	drive: function() {
		if(started) {
			console.log("Zom zom!");
		} else {
			console.log("precisa dar partida no carro!");
		}
	}
};
````

essa abordagem não vai funcionar porque no monento em que o if procurar o valor em started ele irá fazer isso primeiramente em alguma variável local da função, como não existe ele vai procurar alguma variável global que também não existe porque o valor de started está no proprio objeto e para dizer isso a função devemos usar o operador <h4>this</h4>

````
var fiat = {
	make: "Fiat",
	model: "AT200",
	year: 1990,
	color: "Black",
	passengers: 4,
	started: false,

	start: function() {
		this.started = true;
	},

	stop: function() {
		this.started = false;
	},

	drive: function() {
		if(this.started) {
			console.log("Zom zom!");
		} else {
			console.log("precisa dar partida no carro!");
		}
	}
};
````


## Como funciona o <h3>THIS</h3>

o this pode ser entendido como uma palavra reservada que diz procure essa referencia aqui mesmo, como no caso acima acaba que sendo explicito a variável <b>started</b> é uma propriedade do objeto fiat e o this está deixando isso explicito.

