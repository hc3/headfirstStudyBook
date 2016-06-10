# Escrevendo um código de verdade

nesse capitulo sera criado um jogo de batalha naval, sera um jogo bem básico fazendo uso do que foi introduzido no capitulo 1, e o jogo será evoluido
com o passar tempo.

## vamos construir o jogo.

- o jogo consiste em acertar os navios que estão dispostos na grid, mas é claro que não estão visiveis, a grid tem 7x7.

1 - Usuário inicia o jogo</br>
  A - Jogo coloca os navios em lugares aleatorios.
2 - Jogo começa, e repete essa ação até alguem vencer encontrar todos os navios
  A - usuário coloca as tentativas ( de 1 a 7 )
  B - verifica se o usuário acertou ou errou e retorna a informação (hit , miss ou sink)
3 - Fim do jogo o vencedor será quem tiver mais hit.