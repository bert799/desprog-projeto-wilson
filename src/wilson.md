Banana
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


??? Checkpoint:

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


Arvore de Extensão
---------