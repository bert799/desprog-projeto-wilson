Placeholder
======

Algoritmo de Wilson
---------

Vamos introduzir agora a ideia do labirinto perfeito, onde todos os seus pontos são acessíveis, e 
entre dois deles há apenas um caminho. 

??? Checkpoint

Pensando na ideia acima, um algoritmo usando *random walk* **sempre** geraria labirintos perfeitos?

::: Gabarito
Não, porque pode acontecer de dois caminhos se cruzarem o que geraria um loop, permitindo assim que mais 
de uma rota existisse entre dois pontos!
:::

???

Como poderiamos prevenir a criação de loops? Precisariamos saber quando um vértice a ser preenchido cruza outro 
já definido e impedir que se encontrem.

??? Checkpoint

A ideia acima é um bom começo, mas apresenta um problema, qual?

::: Gabarito
Pode ocorrer o caso em que o vértice está "encurralado" e não tem para onde ir, entrando em um loop infinito. 
:::

???

Para começar a resolver este impasse mudamos um pouco o funcionamento do programa, ao invés de ir preenchendo um caminho
de uma raiz definida e avançando vértice por vértice, podemos escolher qualquer um marcado como vazio e ir construindo um
caminho, ainda não preenchido, até cruzarmos um vértice já definido que é quando preenchemos todo o caminho.

??? Checkpoint

A esquemática do algoritmo já esta começando a ser formada, porém ainda não resolvemos o problema do caminho ser
"encurralado" em um loop com si mesmo, como resolveriamos isso?

::: Gabarito
Quando ocorre o cruzamento apagamos o loop e então seguimos o caminho a partir de sua base. 
:::

???

Esta ideia que desenvolvemos é o *loop-erased random walk*, a peça vital do algoritmo de Wilson.

Abaixo temos uma demonstração do *loop-erased random walk* em ação.

:loopErasedRandomWalk

A ideia de David Bruce Wilson para um algoritmo deste tipo é resumidamente, um programa que recebe
como entrada um grafo e escolhe um vértice não preenchido aleatório de início, então começa o 
*loop-erased random walk*. O processo se repete até obter-se um labirinto completamente preenchido.

As vantagens dessa estratégia é que como resultado obtem-se um labirinto perfeito, ou seja, todos os vértices são acessíveis, e 
entre dois deles há apenas um caminho. Outro benefício do algoritmo de Wilson é que pelo caminho ser definido aleatóriamente
ele é imparcial entre caminhos curtos ou longos, um problema de alguns outro algoritmos de geração de labirintos como se pode ver
nas duas figuras abaixo:

![](DepthFirstSearchMaze.png)

![](WilsonMaze.png)

A acima temos um labirinto gerado pelo algoritmo *depth-first search* que tem um viés para gerar corredores longos e em baixo temos o algoritmo de Wilson.

Agora que tem uma ideia de como o algorimo funciona que tal ver uma animação dele em ação? este [site](https://bl.ocks.org/mbostock/11357811) contém um código 
que toda vez que você carrega a página um novo labirinto começa a ser gerado.

Complexidade do algoritmo de Wilson
---------

Pelo fato de ser um programa probabilistico, a complexidade do algoritmo de Wilson não é algo simples de ser definida, entretanto
podemos chegar a um numero esperado médio que leva para o grafo ser preenchido.

A probabilidade do programa ficar preso em um loop infinito é nula, requerindo que nunca encontre algum ponto pré definido o que é impossível já que sempre existe esta probabilidade. A probabilidade de percorrer apenas algumas vezes todos os vértices é maior, e conforme o grafo é preenchido ela só cresce. Assim é de se esperar que o tempo que leva para percorrer é diretamente proporcional ao tamanho do grafo portanto pelas regras de simplificação nos que a conclusão que a complexidade do algorítmo de Wilson é O(n).

