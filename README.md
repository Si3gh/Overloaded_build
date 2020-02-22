# Overloaded 
### Overloaded_build 
##### Projeto integrador - 2019

Alunos: Luiz Henrique Montanher, João Pedro Broietti Pissolito, Marvin Tomizawa, Vitor Barbosa. 

P.S: Este repositório apenas contêm a aplicação gerada(build) na plataforma Unity. 

Um jogo educacional que foca no conteúdo de sistemas operacionais. 
Buscando facilitar o entedimento de um sistema operacional, como no funcionamento/gerência de processos no sistema

## Ideia do jogo:

O jogo se passa dentro do computador em um ambiente imaginário onde é possivel visualizar os processos como blocos solidos, as peças existentes no computador como mobilias e possuir deste modo uma abstração de como funciona o computador por dentro.

O jogador joga no papel de um dispatcher que é responsável por fornecer as instruções para o processador a medida que lhe for solicitado, tentando manter o programa funcionando sem travar, para que a experiencia do usuário seja a melhor possivel e continue utilizando o programa.

Neste desafio de manter a aplicação do usuário o jogador irá enfrentar dificuldades para entregar todas as instruções necessárias, no tempo necessário para que seu programa continue funcionando e continue sendo utilizado pelo usuário.

## Visão técnica do jogo:

O jogo será 3D com uma visão de cima fixa no centro do mapa, contendo vários mapas diferentes e temas diferentes com mecânica escalavel.

Assim toda fase irá adicionar uma nova mecanica que irá refletir como funciona o computador por dentro.

## Mecanicas a serem implementadas:

### **Movimentação do jogador**

O jogador irá se mover utilizando as as letras do teclado (WASD), as teclas direcionais ou os direcionais do controle.<br>
Conforme a direção que o jogador estiver se movimentando será a direção que ele estará olhando. <br>
O jogador só pode interagir com um item por vez.

### **Comportamento das mesas:**

Cada processo será um bloco que poderá ser encaixado em cima das mesas, cada mesa poderá conter apenas um bloco por vez.<br>
É possivel possuir várias mesas uma do lado da outra para poder colocar mais blocos por vez.<br>
Cada mesa poderá ser representada tanto pela memória primaria (RAM) quanto pelo processador assim podendo encaixar os itens nestas mesas assim que sentir necessidade.

### **Jogador movimentar os itens:**

O jogador poderá pegar os itens no chão ou nas mesas utilizando a tecla (Espaço) ou o botão (X no playstation ou A no Xbox) do controle, e larga-los utilizando o mesmo botão.<br>
Enquanto o jogador estiver segurando o bloco ele irá carrega-lo na frente do corpo enquanto se movimenta.

### **Comportamento básico dos itens:**

O itens poderão ser movimentados pelos jogadores ao serem pegos das mesas ou ao estarem no chao poderão ser empurrados pelo corpo do jogador.

Os itens precisam, obrigatoriamente, passar pela memória RAM para chegar ao processador.

Dentro da RAM, o processo é dividido em partes para que seja possível ser processado pelo processador, pois o processador não tem espaço suficiente para trabalhar com um processo inteiro.

Os itens ao serem largados no chão permanecerão lá por poucos segundos e irão retornar para a ultima mesa que estavam presentes.<br>
_Caso a mesa já possua outro item em cima este item será removido e o jogador receberá uma penalidade._

Os itens ao serem largados em cima de uma mesa tentarão se encaixar nela.<br>
_Caso o espaço daquela mesa ja esteja ocupado o item agirá como se estivesse no chão._

O item ao ser encaixado em um slot deverá dar um feedback de luz.

Um item colocado no processador não pode ser retirado para ser processado posteriormente.

### **Disco rigido e spawn de processos:**

Os processos irão permanecer no disco, então este será a fonte onde possuirá uma cópia de todos os processos daquela fase.<br>
Quando o jogador retirar um processo deste local ele irá gerar outro igual dando a ideia de sempre possuir aquele processo em específico.<br>
Este objeto deverá ser posicionado o mais distante possivel do processador.

O spawn do processo deverá ser instantaneo.

## **Processador e tempo de processamento de cada item:**

O processador será responsável por processar todos os itens colocados nele.<br>
No começo a implementação do processador será single thread, então o processador conseguira apenas processar um item por vez.<br>
Cada item possuirá um tempo especifico para ser processado, este tempo significa quanto tempo ele irá permanecer no processador.

O tempo que cada item leva para ser processado deverá variar de acordo com a dificuldade do jogo.

### **Satisfação do usuário:**

A satisfação do usuário servirá como uma barra de vida, caso ela chegue a zero o jogo irá finalizar e o jogador perderá a fase.<br>
Esta satisfação influenciará na pontuação do jogador.<br>
A quantidade de satisfação será um valor inteiro onde será decrementado a cada penalidade que o jogador receber.

### **Escalonamento de processos FIFO e prioridades dos itens:**

Deverá ser apresentado na tela uma fila que indicará quais itens deverão ser processados juntamente com o nome do tipo de escalonamento.<br>
Quando o escalonamento for do tipo FIFO o processador deverá processar os itens que chegaram primeiro nele, caso não seja processado a satisfação do usuário irá diminuir.

Cada item deverá possuir um identificador unico que irá afetar em sua aparencia, a partir deste identificador será apresentado qual item deverá ser processado na ordem.<br>

### Condição de vitória:
O jogador deverá entregar todos os processos que foram sorteados na fila.

### **Preempção por tempo:**

Toda vez que um item é gerado na fila de processos ele deverá também possuir um contador indicando em quanto tempo ele deve ser processado.<br>
O valor do primeiro item será um tempo fixo(definido pela velocidade que leva para o jogador ir e voltar do disco até o processador) + o tempo que o item leva para ser processado.<br>
O valor do segundo item será metade do tempo total do primeiro item + o tempo fixo descrito acima + seu tempo de processamento.

Este contador irá ir decrementando conforme o tempo, caso chegue a zero a satisfação do jogador irá diminuir.<br>
Caso o processo esteja dentro do processador quando o tempo for zerado ele será ejetado para fora caindo no chão.

### **Capacidade do processador:**

Um processador terá uma quantidade específica que aguentará por vez, esta quantidade está ligada ao peso do processo.<br>
Caso o processo esteja cheio ou adicionar o processo no processador ultrapaçaria sua capacidade total o processo é rejeitado e será informado para o jogador que o processador está cheio.

### **Velocidade de movimentação entre Disco-MemoriaRam e MemoriaRam-Processador:**

A velocidade do jogador ficará dependente de qual secção ele está.<br>
Entre o disco rigido e a memória RAM o jogador será mais lento.<br>
Entre a memória RAM e o processador o jogador andará em sua velocidade normal.

O jogador apenas terá sua velocidade impactada quando estiver segurando um processo.

__Caso o jogador não estiver segurando um processo sua velocidade não será afetada.__

## Ideias futuras:

- Memoria swap.
- Virtualização da memória.
- Processos em estado de espera
- Particionamento de processo
- Escalonamento de processos SJF
- Escalonamento de processos circular
- Raid => duplica ou quebrar o dado em mandar em processadores diferentes
- Processador multi-thread
- Peso de cada processo
