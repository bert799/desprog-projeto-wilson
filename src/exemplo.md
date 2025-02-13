Algoritmo de Wilson para Construção de Labirintos
======

Um pouco de teoria dos grafos
---------

!!! Atenção

Comece o handout **após** a exposição inicical sobre grafos.

!!!


??? Checkpoint 1

Esse exemplo demonstra como um grafo pode representar objetos e como esses objetos se relacionam

Digamos que seis pessoas estão indo para uma festa logo apos uma semana cansativa de provas e projetos. Quando chegam à festa, a pessoa **A** comprimenta as pessoas **E** e **F**, **B** comprimenta **C**, e **F** comprimenta **B** e **E**. 

Como ficaria a representação dessas seis pessoas na festa e com quem cada uma interagiu?

::: Esquema
: graph
:::

::: Expressão Final
$$G = \left (\left\{A, B, C, D, E, F\right\}, \left\{\left\{A, E\right\}, \left\{A, F\right\}, \left\{B, C\right\}, \left\{F, B\right\}, \left\{F, E\right\}\right\}\right )$$
:::

???


Árvores Geradoras
---------

Agora que ja sabemos o que é um grafo, fica fácil de definir o conceito de árvore geradora (ou Spanning Tree).

Basicamente, para tornar um grafo uma árvore geradora basta escolher um subconjunto das arestas de forma que entre qauisquer dois vertices existe um, e **apenas um**, caminho. Ou seja não seria possível ir de um vértice ao outro de duas maneiras diferentes, muito parecido com o conceito de um **labirinto** não é mesmo?

Ou seja, uma Árvore Geradora é quase a mesma coisa que um grafo simples, mas existem apenas dois "poréns":

1. Esse grafo precisa conter **todos** os vértices.
    - Não podem existir vértices "soltos".
2. Todos os vértices possuem a **quantidade mínima** de arestas (não podem existir "ciclos").
    - Não pode ser possível ir de um vértice ao outro de duas maneiras diferentes.


![](spanning_tree_gif.gif)

??? Checkpoint 2

No caso do primeiro *checkpoint*, seu grafo final poderia ser considerado uma árvore geradoras?

::: Gabarito
**Não**, já que ele não contém todos os seus vértices (deixando **D** de fora), e é possível ir de um vértice ao outro de duas maneiras diferentes, representando um ciclo (**A**, **E**, e **F**).
:::

???

??? Checkpoint 3

Dado abaixo os vértices de um grafo, como poderiam ser conectados de forma a se tornar uma árvore geradora? (lembrando que existe mais de um jeito possível)

![](nodes.png)

::: Gabarito
Aqui está **uma** solução possível:

:spanning_tree
:::

???

Com o exemplo acima, deve ficar mais claro ainda a semelhança de árvores geradoras com *__caminhos__*, e ainda por cima, caminhos *__únicos__*. E dessa ideia, surgiram inúmeras aplicações para esse tipo de grafo, como, por exemplo, no design de redes elétricas, computadores ou até mesmo de *__labirintos__*. Essa visão sobre *__caminhos únicos__* será muito importante no proximo tópico para o algorítimo que iremos introduzir!



Algoritmos de criação de labirintos
---------

Mas qual é a finalidade de construir labirintos por meio de um algoritmo?

* Construção de labirintos para entusiastas, deixando-os mais complexos;
* Criação de estruturas de dados enormes para testar e treinar algoritmos de *path finding*.

----------------------------------------------------------------------------

E como vamos montar o **grafo** para este algoritmo?

Para a construção de algoritmos, o grafo possui uma estrutura em formato de {red}(quadriculado), ou seja, os vértices são os centros dos quadrados, e as arestas entre quadrados são as arestas do grafo. Caso **não existam**, serão formadas paredes entre os vértices, **caso existam** será considerado um caminho válido.

![](Grafo_labirinto.png)

Para o {blue}(input), todas essas arestas entre os vérticies do grafo existem, ou seja, **todo vértice sabe quem são seus vizinhos**, e também possui uma variável responsável por saber se este já foi visitado ou não.

``` c
typedef struct {
    char visitado;
    int vizinhos[];
} vertice;
```

Nosso objetivo agora é construir os caminhos que serão passagens e esconder aqueles que não são, de modo a se transformarem em paredes. Para isso, vamos pensar em um exemplo muito simples na vida real:

Em um quarto muito amplo, precisamos construir nossas paredes do labirinto, mas só podemos andar nas **direções cardeais**. Para prosseguir, devemos escolher uma direção que {red}(não) seja parede ou um ponto no quarto que já se passou. Quando o movimento ocorrer, deve-se erguer uma parede para todo o resto do quarto que não conhecemos. Essa escolha de movimento deve ser aleatória, como tentativa de ser o mais difícil possível de encontrar uma saída.

Este processo de andar aleatóriamente e ir construindo paredes é conhecido como [Random Walk](https://en.wikipedia.org/wiki/Random_walk). Mas para a nossa aplicação isso não é suficiente.

??? Checkpoint 4:

Sabendo que um caminho {red}(não) pode passar por vértices já visitados, o que deve acontecer quando o vértice **não possui mais vizinhos**?

**Obs.:** Neste momento não é necessário desenvolver o código, somente uma resposta de como ele funcionaria.

::: Gabarito

Deve ser criada uma **`md pilha` com os vértices que estão sendo visitados**, caso o vértice seguinte não possua mais vizinhos, deve-se retirar os vértices da pilha até encontrar um vértice com vizinhos não visitados e denominá-lo de vértice atual. Então definido, deve-se continuar o caminho a partir dele.

:::

???

Agora que a ideia do percurso foi montado, a animação abaixo mostra o funcionamento desta ideia na prática, como a teoria do {red}(Random Walk) mais a {red}(Pilha de Posições) para construir o caminho do labirinto:

:randomWalk

Esta construção de ligações sequenciais entre os elementos, garantindo a existência de um só caminho entre dois pontos, cria, ao final, uma árvore geradora!

!!! Atenção

Não continue pelo handout até entender completamente a ideia de labirinto e como pensar em sua construção, qualquer dúvida não hesite em pedir ajuda

!!!

----------------------------------------------------------------------------

**Agora vamos pensar...**

A ideia do RandomWalk é interessante, porém, se você testar construir alguns labirintos diferentes, vai se deparar com um problema, existe um padrão que nós não queremos: este algoritmo *sem querer* tem a preferência pela construção de `md caminhos longos`.

Isso é um problema porque estamos procurando por algoritmos **{green}(perfeitos)**, ou seja, assim como na árvore geradora uniforme, devem existir **chances iguais** para a construção de `md qualquer configuração` de caminhos possíveis. Como o algoritmo possui uma preferência, essa regra não é mais válida!

Para solucionar esse problema, foram então criados alguns algoritmos para evitar esse problema, um deles é o **Algoritmo de Wilson**, que será explicado mais à frente. Vamos entender um outro algoritmo primeiro, de modo a ser possível realizarmos algumas comparações; este é o *Algoritmo de Aldous-Broder*.

Algoritmo de Aldous-Broder
---------

Depois que entendemos e trabalhamos um pouco com o *Random Walk*, vamos começar pelo algoritmo de **{green}(Aldous-Broder)**.

Para garantir a aleatoriedade do sistema, este algoritmo escolhe aleatoriamente qualquer direção a percorrer, ou seja, não existe nenhuma proibição de avanço.

Pensando na estrutura do *Random Walk*, no algoritmo de Broder a escolha de que caminho seguir **não é levado em consideração os vizinhos já percorridos ou paredes criadas**, e, por isso, na maioria das vezes existem 4 caminhos possíveis para seguir.

??? Checkpoint 5

Pensando no funcionamento aleatório do sistema, qual é o grande problema causado por este quando a malha do labirinto é muito grande?

::: Gabarito

Pensando em uma malha maior de vértices disponíveis, embora ele percorra por vértices não visitados rapidamente no início, com o passar das iterações fica cada vez **mais difícil de encontrar um vértice que não esteja preenchido** de modo aleatório, o que indica o {red}(crescimento exponencial) dessa descoberta.

:::
???

Fica difícil de entender como este funciona e como essa aleatoriedade se torna preocupante com o tempo. Por isso recomendamos que vocês percebam este fator [neste vídeo](https://www.youtube.com/watch?v=-EZwuFdkJes&ab_channel=Ferenc).

Em relação ao funcionamento de preenchimento, quando o vértice a ser encontrado ainda não foi visitado, o algoritmo cria o caminho baseado naquele tomado para lá chegar. Caso esse vértice já tenha sido visitado, a parede continuará como separados do caminho.

![](AldousBroder.png)


Algoritmo de Wilson
---------

O algoritmo de Broder, parte da idéia de ir construindo o labirinto a partir de uma árvore geradora, com os ramos conectados a ela crescendo, que como vimos apresenta o problema de ser muito lento no final, mas e se houvesse um programa que primeiro construísse estes ramos pelos pontos desconectados, e depois os "espetassem" na árvore?

??? Checkpoint 6

Qual uma possível vantagem desse método em relação ao algoritmo de Aldous-Broder? Pense nas diferenças de comportamento nas operações finais de ambos.

::: Gabarito
Neste caso não haveria a lentidão do algoritmo de Aldous-Broder nas operações finais, já que ele não teria que percorrer as áreas já preenchidas previamente.
:::

???

Como elaborar estes ramos? Primeiro será necessário escolher aleatóriamente um ponto de ínicio deste ramo que não tenha faça parte da árvore geradora, a partir deste ponto o ramo é incrementado até encontrar as áreas já pertencentes a árvore, quando é "espetado" e passa a fazer parte desta. Este processo se repete até todos os pontos do grafo pertencerem a árvore geradora.

Abaixo temos um exemplo da construção de um destes ramos.

:WilsonWay

??? Checkpoint 7

Se queremos evitar o mesmo problema do algoritmo de Aldous-Broder, que medida pode ser tomada para evitar percorrer pontos no qual o ramo já passou?

::: Gabarito
Podemos marcar todos os pontos percorrido e fazer com que o programa os evite.
:::

???

Com essa idéia vamos pensar neste método para a construção de labirintos.

??? Checkpoint 8

Essa ideia parece ser boa, mas introduz um problema, qual? Lembre que queremos que o algoritmo gere labirintos de forma imparcial, ou seja, que não haja preferência para um tipo específico de labirinto.

::: Gabarito
Ao "desviar" de pontos já percorridos tenderemos a criar caminhos muito longos o que eliminaria um das vantagens de um labirinto gerado a partir de *random-walk* que é a imparcialidade dos tipos de labirintos que são possíveis. Já que deste modo tenderia obter labirintos com corredores muito grandes.
:::

???

Então como é possível usar esse método e manter a imparcialidade de geração? sabemos que não podemos evitar os caminhos já percorridos, e não podemos deixar que os dois caminhos se encontrem, já que neste caso  eles criariam um loop como pode-se ver na imagem abaixo. Isso não é bom já que quebra o desejo do labirinto ser perfeito, por termos mais de um caminho entre dois pontos, porém podemos usar pensar evento para nos ajudar.


![](Loop.png)

??? Checkpoint 9

Que outra estratégia podemos usar para evitar a criação de um loop? Pense que queremos preservar um ramo linear.

Dica.: A ídeia pode ser mas simples do que pensa. 

::: Gabarito
Podemos apagar o loop, continuando a partir de sua base.
:::

???

Assim, mantemos o comportamento de *random-walk* até encontrarmos o ramo, preservamos a imparcialidade e não percorremos o mesmo caminho mais de uma vez!

Esta ideia é chamade de *loop-erased random walk*!

Abaixo temos uma demonstração do *loop-erased random walk* em ação, caso não tenha entendido algum passo retorne para a explicação acima.

:loopErasedRandomWalk

??? Checkpoint 10

Embora esse método apresente estas vantagens, ele introduz um problema, qual? Pense nas primeiras operações quando o labirinto é pequeno.

::: Gabarito
Nas primeiras operações pode ser que o algoritmo demore para "encontrar" o labirinto já que há muitos espaços vazios e poucos preenchidos.
:::

???

??? Desafio

A desvantagem acima pode acabar sendo relativamente benigna para a velocidade do algoritmo, porque?

::: Gabarito
Quando qualquer uma das operações inicias for demorada, a chance é relativamente alta que o resultado seja um caminho longo, que facilitará todas as operações seguintes
já que haverá muitos mais pontos para os ramos serem "espetados".
:::

???

A ideia de David Bruce Wilson para um algoritmo deste tipo é resumidamente, um programa que recebe
como entrada um grafo e escolhe um vértice não preenchido aleatório de início, então começa o 
*loop-erased random walk*, com este caminho sendo adicionado ao resto do labirinto quando encontra 
um de seus pontos já definidos. O processo se repete até ele ser completamente preenchido.

As vantagens dessa estratégia é que como resultado obtem-se um labirinto perfeito. Outro benefício do algoritmo de Wilson, mencionado previamente,
é que pelo caminho ser definido aleatóriamente as chances de gerar qualquer tipo de labirinto é uniforme, ou seja não existe viés para tipos especificos 
de árvores geradoras, um problema presente em outros algoritmos de geração de labirintos como se pode ver nas duas figuras abaixo:

![](DepthFirstSearchMaze.png)

![](WilsonMaze.png)

A acima temos um labirinto gerado pelo algoritmo *depth-first search* que tem um viés para gerar labirintos com corredores longos e em baixo temos o algoritmo de Wilson.

Agora que tem uma ideia de como o algorimo funciona, que tal ver uma animação dele em ação? Temos o GIF abaixo e este [site](https://bl.ocks.org/mbostock/11357811) que contém um código que gera um novo labirinto toda vez que você carrega a tela.

![](wilson.gif)

Complexidade do algoritmo de Wilson e comparação com Aldous-Broder
---------
Pelo fato de ser um programa probabilistico, a complexidade do algoritmo de Wilson não é algo simples de ser definida, então vamos colocar os números de lado no momento
("Ufa, engenharia já tem números o suficiente.") e compará-lo com o algoritmo que vimos anteriormente, o algoritmo de Aldous-Broder. De ínicio vamos falar de sua similaridade, ambos utilizam alguma forma de *random walk* para ir preenchendo a árvore geradora, assim, no pior dos casos ambos vão ter a complexidade igual, porém isso
não significa que seus tempos de rodar são iguais na prática. 

??? Checkpoint 12

Pense nos comportamentos e características de cada um dos dois e aponte quem deve ser o mais rápido na média e porque.

Dica: Pense também no que ocorre com o número de pontos pelos quais ambos os algoritmos podem percorrer conforme o labirinto é preenchido.

::: Gabarito
Embora o algoritmo de Aldous-Broder seja mais rápido no começo ele sempre trabalha com todos os pontos do labirinto, enquanto o Wilson sempre melhora as suas chances de encontrar alguma parte dele conforme vai preenchendo diminuindo o número de pontos pelo qual pode percorrer. Portanto o algoritmo mais rápido na prática será o de Wilson.
:::

???

??? Desafio

Qual seria uma implementação possível de melhor desempenho que o algoritmo de Wilson e o algoritmo de Aldous-Broder?

Obs.: A resposta é mais óbvia do que você pode pensar.

::: Gabarito
Como os algoritmos tem desvantagens opostas em relação ao tempo das operações iniciais e finais, podemos criar um algoritmo híbrido que usa o Aldous-Broder para preencher uma árvore geradora inicial já que é mais rápido que o algoritmo de Wilson no começo e transita para o algoritmo de Wilson no meio para o fim já que o Wilson é melhor nestes casos. Como fica evidente no gráfico abaixo:

![](complexImg.png)

:::

???