# java10-2022b-joaofrigo
java10-2022b-joaofrigo created by GitHub Classroom

![image](https://user-images.githubusercontent.com/92951251/199743869-3c75c367-b1c6-458b-a1de-0fed2bf61af8.png)

## Por que ocorre a inconsistência?

Aqui na imagem postada, pode se dar conta dos resultados incorretos em `Sharedtable`. O problema ocorreu primordialmente no trecho
de código `"addMark"` que está localizado em `SharedTable`. O problema ocorre por que considerando que o programa está rodando de forma
concorrente, ao colocar em table o char "c" e depois a função `"spendSomeTime"` (unicamente feita pra passar o tempo) ser acionada,
para logo depois aumentar o index e colocar outro "c", faz com que o resultado se torne inconsistente. As varias threads entram em
conflito nesse meio tempo que ocorre a função (principalmente culpa de `"spendSomeTime"`), e o resultado final então é extremamente improvável de estar correto. 
O jeito correto de resolver esse dilema, é sincronizar a função `addMark`, não apenas o `"spendSomeTime"` (por mais que seja o maior mal
da concorrência entrando em conflito). Ou ainda mais fácil, sem precisar utilizar "synchronized", é só não usar a função `"spendSomeTime"`,
assim o código `"addMark"` consegue rodar em "Mão unica" sem dificuldades.

## Indo além

Algo que me desperta o interesse nesse conceito, é o porquê. Por que utilizar threads? o que ganhamos com isso? resposta? basicamente, muita eficiência.
o fato da importância do multi-thread em otimização e aperfeiçoamento de códigos em mais larga escala é extremamente claro, sem sombra de duvidas é importante.
Um jogo que utiliza um meio de mão única para seu processamento, definitivamente não estaria utilizando nem perto de seu potencial verdadeiro para atingir uma
otimização boa e muito provavelmente teria taxa de quadros minuscula em comparação com multi-thread, tanto que mal conseguiria usar a placa de vídeo, que
entraria em conflito com o processador e serviriam como um funil de otimização um para o outro. Venho programando tudo em mão única, mas tenho certeza
que no mundo da programação para coisas com reais funcionalidedes, o multi-thread é a norma, pois não consigo nem imaginar um universo aonde ele não seria
utilizado para todos os tipos de programação, seria desperdiçar uma mina de diamantes de otimização. Fico impressionado na evolução ao longo dos anos tanto
na questão de hardware (pipeline por exemplo) tanto quanto na programação e suas artimanhas para o controle do hardware e seu verdadeiro potencial através
das threads, que definem tão fortemente o conceito de velocidade em programas cada vez maiores.
