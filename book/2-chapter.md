# Escrevendo um código de verdade

nesse capitulo sera criado um jogo de batalha naval, sera um jogo bem básico fazendo uso do que foi introduzido no capitulo 1, e o jogo será evoluido
com o passar tempo.

## vamos construir o jogo.

- o jogo consiste em acertar os navios que estão dispostos na grid, mas é claro que não estão visiveis, a grid tem 7x7.
<ul>
  <li>Usuário inicia o jogo</br>-o jogo coloca os navios em lugares aleatorios</li>
  <li>Jogo começa, e repete essa ação até alguem vencer encontrar todos os navios
    </br> -usuário coloca as tentativas ( de 1 a 7 )
    </br>-verifica se o usuário acertou ou errou e retorna a informação (hit , miss ou sink)</li>
  <li>Fim do jogo o vencedor será quem tiver mais hit.</li>
</ul>

- mais detalhes.
o jogo começa com a criação de um grid virtual com 7 espaços que vão de 0 a 6 o navio vai estar localizado em três desses 7 blocos, em seguida uma tela
de prompt vai abrir e solicitar um input do usuário esse input corresponde ao local onde o navio está, o jogo verificará se o usuário aceitou a tentativa
se sim ele ganha um acerto são necessários três acertos para o fim do jogo.

## construindo o pseudocódigo.
o pseudocódigo t

DECLARE três variáveis que serão a localização dos navios chame-as de loc1 , loc2 , loc3.
DECLARE uma variável para segurar o número de tentativas corrente chame-a de guess.
DECLARE uma variável para segurar o número de acerto chame-a de hit, e incialize-a com 0.
DECLARE uma variável para segurar o número final de tentativas, chame-a de guesses e inicialize-a com 0.
DECLARE uma variável para manter se o navio foi afundado ou não, chame-a de sunk e inicialize-a com false.

LOOP: enquanto o navio não for sunk
  PEGUE a tentativa do usuário ( guess )
  COMPARE se o valor do usuário é um input válido
  SE o valor for invalido
    RETORNE MENSAGEM para o usuário inserir um valor válido
  SE NÂO 
    ADICIONE valor a variável guesses ( tentativas )
    SE usuário acertou a localização 
      ADICIONE valor a variável hit
      SE o valor de git for 3 
        SETAR o valor true a variável sunk 
        RETORNE MENSAGEM parabéns você venceu
      FIM SE
    FIM SE
  FIM ELSE 
FIM LOOP
RETORNE MENSAGEM status do usuário.
