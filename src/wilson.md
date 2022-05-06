バナナ
======

Um pouco de teoria dos grafos
---------

O que é um grafo?

Um grafo de teoria dos grafos, em particular, é um assunto essêncial para entender o handout de hoje. Na teoria dos grafos, um grafo é um par ordenado que consiste em um conjunto de vértices e, em seguida, em um conjunto de arestas. 

$$G = \left ( v, e \right )$$

Os grafos são frequentemente representados como diagramas, com pontos ou circulos representando vértices e linhas representando arestas. Cada aresta une dois vértices, de modo que as linhas no diagrama de um grafo vão de um vértice a outro vértice. Então, o conjunto de arestas de um grafo consiste em subconjuntos de dois elementos do conjunto de vértices, pois em um grafo simples, cada aresta é inteiramente definida pelos vértices que une. 

![](simpleGraph.png)

$$G = \left ( \left\{ 1, 2, 3, 4 \right\}, \left\{ \left\{ 1, 2 \right\}, \left\{ 1, 3 \right\}, \left\{ 1, 4 \right\}, \left\{ 2, 3 \right\} \right\} \right )$$

Ah, a propósito, estamos falando apenas de grafos simples, que são os tipos de grafos mais bem estudados na teoria dos grafos, e geralmente são chamados apenas de grafos. Entre outras restrições, grafos simples não permitem loops, multi-arestas ou arestas direcionadas. Para ficar mais facil a compreensão, veja o exemplo abaixo:


??? Checkpoint 1

Esse exemplo demonstra como um grafo pode representar objetos e como esses objetos se relacionam

Digamos que seis pessoas estão indo para uma festa logo apos uma semana cansativa de provas e projetos. Quando chegam à festa, a pessoa **A** comprimenta as pessoas **E** e **F**, **B** comprimenta **C**, e **F** comprimenta **B** e **E**. 

Como ficaria a representação dessas seis pessoas na festa e com quem cada uma interagiu?

::: Esquema
: graph
:::

::: Equação Final
$$G = \left (\left\{A, B, C, D, E, F\right\}, \left\{\left\{A, E\right\}, \left\{A, F\right\}, \left\{B, C\right\}, \left\{F, B\right\}, \left\{F, E\right\}\right\}\right )$$
:::

???


Arvores de Extensão
---------

Agora que ja sabemos o que é um grafo, fica fácil de definir o conceito de Arvore de Extensão (ou Spanning Tree).

Uma Arvore de Estensão, também chamada de sub-grafo de extenção, é quase a mesma coisa que um grafo simples, mas existem apenas dois "poréns":

1. Esse grafo precisa conter **todos** os vértices.
2. Todos os vértices possuem a **quantidade mínima** de arestas (não podem existir "ciclos").

Ou seja, se contássemos o numero total de arestas de uma árvore de extensão, ela sempre será igual a *__n - 1__*, onde *__n__* seria o número de vértices.

![](spanning_tree_gif.gif)

??? Checkpoint 2

No caso do primeiro *checkpoint*, seu grafo final poderia ser considerado uma árvore de extensão?

::: Gabarito
**Não**, já que ele não contém todos os seus vértices (deixando **D** de fora), e seus vértices não possuem a quantidade mínima de arestas, representando um ciclo (**A**, **E**, e **F**).
:::

???

??? Checkpoint 3

Dado abaixo os vértices de um grafo, como poderiam ser conectados de forma a se tornar uma árvore de extensão (lembrando que existem mais de um jeito possível)?

![](nodes.png)

::: Gabarito
Aqui está uma solução possível:
: spanning_tree
:::

???

Se parar para pensar, uma característica muito interessante das árvores de extensão é que se parecem muito com *__caminhos__*, e ainda por cima, *__únicos__*. E dessa ideia, surgiram inúmeras aplicações para esse tipo de grafo, como, por exemplo, no design de redes elétricas ou até mesmo de computadores. Essa visão sobre *__caminhos únicos__* será muito importante no proximo tópico para o algorítimo que iremos introduzir.