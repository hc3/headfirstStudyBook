## Construindo um app

Falaa galera, nesse post vou criar um jogo de batalha naval com HTMl , CSS e Javascript, usando HTML para
estrutura o CSS aplicando um style e o Javascript dando uma dose de comportamento, vamos ver um pouco de HTMl e CSS e tentar partir de algo básico que vai avançando aos poucos, esse post foi baseado no capitulo 8 do livro Head First Javascript Programming.

vamos esquecer um pouco o javascript e pensar no design do jogo, vai ser basicamente HTML e CSS, primeiro de tudo vamos fazer o download das imagens que vão ser usadas no jogo, [aqui](), feito o download podemos começar a brincar, rs.

<h4>Criando página HTML</h4>

-Primeiro <br/>
primeiro de tudo devemos colocar o background do html com a imagem de fundo com o radar e os desenhos das áreas que podem ser atingidas.

-Segundo <br/>
vamos criar um table html por cima da imagem onde fica as célula cada tabela vai representar uma célula
que vai ter um valor.

-Terceiro <br/>
vamos criar um html form para receber as entradas do jogador por exemplo "A3" e vamos também adicionar uma área para mensagens como "você acertou sua tentativa".

-Quarto <br/>
e finalmente vamos colocar as imagens do barco e do MISS para quando o jogador não acertar a jogada.
<br/>


- Primeiro passo, devemos aqui criar uma página html, com isso suponho que você leitor já tenha conhecimento mesmo que básico de html, se não tiver pode ler o livro Head First HTML e CSS ( use a cabeça HTML e CSS).
<br/>
````html
<!doctype html>

<html>
	<head>
		<meta charset="UTF-8">
		<title>Batalha naval</title>
		<style>
			body {
				background-color: black;
			}

			div#board {
				position : relative;
				width: 1024px;
				height: 863px;
				margin: auto;
				background: url("board.jpg") no-repeat;
			}
		</style>
	</head>
	<body>
		<div id="board">

		</div>
		<script src="jogo.js"></script>
	</body>
</html>
````
essa é a estrutura básica do jogo, podemos ver aplicação de estilo no corpo da página setando o background para cor preta, nos queremos também que o display do jogo fique centralizado e para isso setando width e heigth , margin auto colocamos também a imagem com o layout do jogo e setamos para que ela não se repita isso tudo vai estar contido na div que tem o id="board" e setamos também um arquivo javascript com o nome de jogo.js que por enquanto vai estar vazio.
<br/>

-Segundo passo vamos criar uma tabela, a tabela vai ser o lugar onde os navios vão estar escondidos cada célula será presentada por um <td> , cada célula vai ter um ID que vamos manipular com CSS e Javascript, vamos entender outra coisa aqui, cada linha vai representar uma letra e cada coluna é um número então a nossa board vai ficar assim.

````html
<div id="board">
  <table>
    <tr>
      <td id="00"></td>
      <td id="01"></td>
      <td id="02"></td>
      <td id="03"></td>
      <td id="04"></td>
      <td id="05"></td>
      <td id="06"></td>
    </tr>
    <tr>
      <td id="10"></td>
      <td id="11"></td>
      <td id="12"></td>
      <td id="13"></td>
      <td id="14"></td>
      <td id="15"></td>
      <td id="16"></td>
    </tr>
    <tr>
      <td id="20"></td>
      <td id="21"></td>
      <td id="22"></td>
      <td id="23"></td>
      <td id="24"></td>
      <td id="25"></td>
      <td id="26"></td>
    </tr>
    <tr>
      <td id="30"></td>
      <td id="31"></td>
      <td id="32"></td>
      <td id="33"></td>
      <td id="34"></td>
      <td id="35"></td>
      <td id="36"></td>
    </tr>
    <tr>
      <td id="40"></td>
      <td id="41"></td>
      <td id="42"></td>
      <td id="43"></td>
      <td id="44"></td>
      <td id="45"></td>
      <td id="46"></td>
    </tr>
    <tr>
      <td id="50"></td>
      <td id="51"></td>
      <td id="52"></td>
      <td id="53"></td>
      <td id="54"></td>
      <td id="55"></td>
      <td id="56"></td>
    </tr>
    <tr>
      <td id="60"></td>
      <td id="61"></td>
      <td id="62"></td>
      <td id="63"></td>
      <td id="64"></td>
      <td id="65"></td>
      <td id="66"></td>
    </tr>
  </table>
</div>
````
podemos ver aqui que criamos 7 <tr> com 7 <td> cada.
<br/>

-Terceiro precisamos de um lugar para o usuário colocar suas entradas como "A4","E2", vamos precisar também de um lugar para colocar as mensagens como "você acertou um navio" e para isso vamos usar <form> com um <input> e <div> para as mensagens.

````html
<div id="board">
<div id="messageArea"></div>
<table>
...
</table>
  <form action="">
    <input type="text" id="guessInput" placeholder="A0">
    <input type="button" id="fireButton" value="Fire!">
  </form>
</div>
````
omitindo o conteúdo da table, temos a inclusão de uma div para área de mensagens e um form que vai pegar entrada do usuário e o botão que vai enviar essa entrada.<br/>
-Vamos adicionar um pouco de estilo na mensagem e no input, as células por sua vez vão precisar de um tamanho vamos começar com a messageArea:

````css
body {
	background-color: black;
}

div#board {
	position : relative;
	width: 1024px;
	height: 863px;
	margin: auto;
	background: url("board.jpg") no-repeat;
}
div#messageArea {
	position:absolute;
	top:0px;
	left:0px;
	color: rgb(83, 175, 19);
}
````
veja que foi adicionado o estilo a <div id="messageArea"> position absolute se refere ao fato de que ela está dentro da <div id="board"> com isso ela fica no canto esquerdo com top e left com 0px.<br/>

e depois é adicionado o css completo com todos os elementos:

````css
body {
	background-color: black;
}

div#board {
	position : relative;
	width: 1024px;
	height: 863px;
	margin: auto;
	background: url("board.jpg") no-repeat;
}
div#messageArea {
	position:absolute;
	top:0px;
	left:0px;
	color: rgb(83, 175, 19);
}
table {
	position: absolute;
	left: 173px;
	top: 98px;
	border-spacing: 0px;
}
td {
	width: 94px;
	height: 94px;
}
form {
	position: absolute;
	bottom: 0px;
	right: 0px;
	padding: 15px;
	background-color: rgb(83, 175, 19);
}
form input {
	background-color: rgb(152, 207, 113);
	border-color: rgb(83, 175, 19);
	font-size: 1em;
}
````
primeiro de tudo foi adicionado a <table> a position absolute e colocamos no lugar exato de onde fica os quadrados na imagem, depois adicionamos um determinado espaço para o <td> com widtg: 94px e heigth: 94px, um quadrado, que podemos ver perfeitamente acessando o console do navegador com F12 o próximo é o form e o input que são estilizados para ficar no canto inferior direto (<b>uma nota que gostaria de fazer ao terminar o css entrar no console e navegar pelo dom percebendo onde cada elemento ficou e como foi aplicado estilo ao mesmo</b>).
<br/>

-Quarto passo, posicionar os navios e as tentativas ou podemos chamar de misses que são as imagens que vão aparecer dependendo da jogada se o jogador acertou um <b>navio</b> se não um <b>misses</b>
