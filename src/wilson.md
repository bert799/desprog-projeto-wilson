Banana
======

Algoritmo de Wilson
---------

A ideia de David Bruce Wilson para um algoritmo deste tipo é resumidamente, um programa que recebe
como entrada um grafo e escolhe um ponto não preenchido aleatório de início, então começa o *loop-erased random walk*
terminando cada caminho uma vez que este encontra uma parte já preenchida do grafo. O processo se repete
até obter-se um labirinto completamente preenchido.

O mecanismo essencial do algoritmo é o *loop-erased random walk*, que é semelhante ao *random walk*, entretanto,
caso o percurso cruze a si mesmo, o "loop" formado é apagado e o processo continua do ponto imediamente anterior 
ao cruzamento. O caminho só é considerado preenchido uma vez que encontra outra parte previamente preenchida.

**INSERIR ANIMAÇÃO DE EXEMPLO**

As vantagens dessa estratégia é que como resultado obtem-se um labirinto perfeito, ou seja, todos os pontos são acessíveis, e 
entre dois pontos há apenas um caminho. Outro benefício do algoritmo de Wilson é que pelo caminho ser definido aleatóriamente
ele é imparcial entre caminhos curtos ou longos, um problema de alguns outro algoritmos de geração de labirintos como se pode ver
nas duas figuras abaixo:

![](DepthFirstSearchMaze.png)
![](WilsonMaze.png)

A esquerda temos um labirinto gerado pelo algoritmo *depth-first search* que tem um viés para gerar corredores longos e a esquerda temos o algoritmo de Wilson.

Agora que tem uma ideia de como o algorimo funciona que tal ver uma animação dele em ação? este [site](https://bl.ocks.org/mbostock/11357811) contém um código 
que toda vez que você carrega a página um novo labirinto começa a ser gerado.






