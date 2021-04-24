# Snake Game

## Estrutura inicial

Para o desenvolvimento deste game começarei com a seguinte estrutura:

![Imagem01](../snake-game-images/01.png)

A ideia é separar os objetos JavaScript e folhas de estilo CSS. Ainda que o jogo seja bem simples acredito que é uma boa prática essa separação, portanto não poderia perder a oportunidade de exercitar!

## Canvas e o contexto gráfico
#### O Canvas
O elemento ```<canvas>``` foi criado com os atributos **width** e **height** (largura e altura respectivamente) e o id **snake-game**. O id é muito importante pois é através dele que o JavaScript localizará a referência ao elemento ```<canvas>``` que será manipulado.

O Canvas possui o seguinte sistema de coordenadas:

![Imagem02](../snake-game-images/02.png)

No canto superior esquerdo as coordenadas são (0,0).

#### Contexto gráfico
Para começar a desenhar é preciso utilizar referência do elemento HTML ```<canvas>```, que ficará armazenada em uma constante, e obter o seu contexto gráfico.
```JavaScript
    const canvas = document.getElementById('snake_game_canvas');
    const ctx = canvas.getContext('2d')
```
O contexto gráfico é um objeto da interface CanvasRenderingContext2D, é nele que desenhamos o que será exibido no elemento ```<canvas>```.

Abrindo o arquivo index.html (já estilizado) temos o seguinte:

![Imagem03](../snake-game-images/03.png)

Está concluído o ponto de partida do game.

## O jogo

O jogo da cobrinha é bastante simples, a base do jogo é construída com apenas três objetos:

* ####🔳 Área do jogo
* ####🐍 Cobra
* ####🍎 Maçã

A regra também é bastante simples, o jogador apens escolhe a direção que a cobra se movimenta com o objetivo de comer as maçãs. As maçãs aperecem em lugares aleatórios e cada vez que a cobra come uma maçã ela aumenta seu próprio comprimento. Se a cabeça da cobra colidir com a sua cauda o jogo é finalizado.

## 🔳 Área do jogo

O primeiro passo é definir o tamanho dos **tiles**. Com base na área do ```<canvas>``` que é de 500px x 500px vou definir cada **tile** com a dimensão de 10px.

No arquivo src/game.js inicio o objeto **game**:

```JavaScript
    let game = {
        tile : 10,
    }
```
E já faço o primeiro teste desenhando um tile na tela, para isso basta adicionar os seguintes comandos entre as tags ```<script></script>``` no corpo do documento html:

```html
    ctx.fillStyle = "tomato"
    ctx.fillRect(10, 10, game.tile, game.tile)
```

O resultado é esse primeiro quadrado com as dimensões de 10px x 10px nas coordenadas (10,10) do Canvas.

![Imagem04](../snake-game-images/04.png)

Esse foi apenas um teste para ver como as coisas estão indo. Começarei agora a definir o próximo objeto 🐍.

## 🐍 Cobra

A cobrinha é o objeto mais complexo neste jogo. Iniciarei esse objeto definindo os atributos **color**, **body**, **size**, **positionX**, **positionY** e **direction**.

No arquivo src/snake.js inicio o objeto **snake**`:

```JavaScript
    let snake = {
        color : "DarkGreen",
        body : [],
        size : 3,
        positionX : 10,
        positionY : 10,
        direction : "right",
    };
```

O primeiro atributo é a cor da cobrinha, logo após declaro um array vazio para o corpo, em seguida o comprimento e finalizo com as coordenadas iniciais e direção que a cobrinha se moverá assim que o jogo começar.

Foi necessário utilizar um array para o corpo da cobrinha pois ele nada mais é que um vetor de coordenadas (x,y) onde cada posição representa um bloco. A cada maça comida uma nova posição será adicionada ao final desse array.

Por enquanto isso basta, próxima etapa será a configuração da função principal.

## Controles e Movimentação

A principal função neste jogo é a **moveSnake()**, ela será responsável por verificar a tecla digitada pelo usuário, incrementar/decrementar as posições (x,y) da cobrinha e desenhar no Canvas.
As duas formas mais comumente utilizadas para controle desse fluxo são os métodos **setInterval()** ou **requestAnimationFrame()**. No desenvolvimento deste jogo utilizarei o **requestAnimationFrame()** que é um método do objeto **window**, ele irá delegar ao browser a tarefa de executar a sua animação.




