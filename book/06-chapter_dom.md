# Introdução ao DOM

o DOM ou document object model é uma arvore, com os elementos html de uma página web, que pode ser acessado pelo javascript e modificado dinamicamente podemos acessar diretamente um elemento do DOM através do <code>getElementById("id do element")</code> podemos acessar por exemplo uma div com o id="minhaDiv" da seguinte forma.

````js
var minhaDiv = document.getElementById("minhaDiv");
minhaDiv.innerHTML = "novo conteudo para a DIV";
alert(minhaDiv);
````

vamos entender o que está acontecendo aqui, temos uma div com o id <b>minhaDiv</b> que está sendo acessada através do objeto global <b>document</b> que tem o método <b>getElementById</b> que faz exatamente o que ele diz pega um elemento a partir do ID acessamos a propriédade innerHTML que existe em todos os elementos do DOM e setamos um novo texto para esse elemento.

precisamos levar em consideração que o DOM é criado quando a página web é lida ou carregada por assim dizer, então enquanto a página não foi carregada o javascript não tem acesso ao DOM porque o mesmo ainda não foi montado, existem outros objetos globais como o <b>window</b> que se refere ao browser esse objeto tem a propriedade <b>onload</b> ou seja essa pripriedade sera "chamada" após o carregamento da página podemos criar uma função e atribuir a essa propriedade.

````js
function init() {
	var minhaDiv = document.getElementById("minhaDiv");
	minhaDiv.innerHTML = "esse elemento foi alterado!";
}
window.onload = init;
````
lembrando que não usamos os parenteses da função pois não estamos chamando a função na propriedade, e sim estamos atribuindo o o valor da funçaõ a propriedade <b>onload</b>.

## Event , Callback

pare pra pensar como a propriedade <b>onload</b> sabe a hora exata de chamar a função init, porque ela só será executada após o carregamento da página e agora chegamos a um assunto muito importante do javascript que são os eventos, quando algo acontece os eventos são disparados, e isso acontece graças ao callback, ou seja quando a página for carregada, existe um listener que vai perceber o acontecimento do evento e vai chamar o método <b>init()</b>, callback e eventos são assuntos completos que serão abordados em assuntos posteriores, por hora pense que o javascript é muito poderoso devido aos eventos e callbacks que serão disparados a partir de um evento.

## Finalizando

esse capitulo foi uma pequena introdução ao DOM abordou o assunto de uma maneira muito superficial, além do <b>getElementById</b> , temos também o <b>setAttribute</b> e o <b>getAttribute</b>, entender o Document Object Model é a única forma de entender como o Javascript pode influênciar em uma página html.