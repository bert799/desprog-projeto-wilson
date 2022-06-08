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

Ou seja, se contássemos o numero total de arestas de uma árvore geradoras, ela sempre será igual a *__n - 1__*, onde *__n__* seria o número de vértices.

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
Aqui está uma solução possível:

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

Para a construção de algoritmos, o grafo possui uma estrutura em formato de {red}(quadriculado), ou seja, os vértices são os centros dos quadrados, e as arestas entre quadrados são as arestas do grafo caso **não existam** ou indicam que não há ligação, paredes, **caso existam**.

Para o {blue}(input), todas essas arestas entre os vérticies do grafo existem, ou seja, **todo vértice sabe quem são seus vizinhos**, e também possui uma variável responsável por saber se este já foi visitado ou não.

``` c
typedef struct {
    char visitado;
    int vizinhos[];
} vertice;
```

??? Checkpoint 4:

Sabendo que para construir um labirinto os caminhos devem ser escolhidos aleatoriamente para garantir que existam vários tipos de construção para a mesma estrutura, como você construiria a função que percorre pelos vértices do grafo para marcar o caminho?

**Obs. 1:** Neste momento não é necessário desenvolver o código, somente uma resposta de como ele funcionaria.

**Obs. 2:** Esta função deve ser pensada para rodar por vértice, então pense como funcionaria dentro de um deles.

::: Gabarito

O código deve, a partir de um determinado vértice, escolher `md aleatoriamente` um **vizinho** que será o próximo a ser analisado, marcando o atual como um vértice já visitado. Depois devemos redefinir os vizinhos para serem somente o anterior a ele e o próximo escolhido, de modo a formar o caminho por onde o labirinto passa.

:::

???

Este conceito de varredura aleatória para a construção de labirintos é conhecido como [Random Walk](https://en.wikipedia.org/wiki/Random_walk), mas possui uma diferença:

??? Checkpoint 5:

Sabendo que um caminho {red}(não) pode passar por vértices já visitados, o que deve acontecer quando o vértice **não possui mais vizinhos**?

**Obs.:** Neste momento não é necessário desenvolver o código, somente uma resposta de como ele funcionaria.

::: Gabarito

Deve ser criada uma **`md pilha` com os vértices que estão sendo visitados**, caso o vértice seguinte não possua mais vizinhos, deve-se retirar os vértices da pilha até encontrar um vértice com vizinhos não visitados e denominá-lo de vértice atual. Então definido, deve-se continuar o caminho a partir dele.

:::

???

Agora que a ideia do percurso foi montado, a animação abaixo mostra o funcionamento desta ideia na prática, como a teoria do {red}(Random Walk) mais a {red}(Pilha de Posições) para construir o caminho do labirinto:

:randomWalk

!!! Atenção

Não continue pelo handout até entender completamente a ideia do algoritmo, qualquer dúvida não hesite em pedir ajuda

!!!

----------------------------------------------------------------------------

Agora, com a ideia do algoritmo compreendida, vamos montar o **{red}(código)**!

Pensando em toda a construção feita até agora sobre este algorítmo, vamos dividir também as funções do código. A que estamos particularmente interessados é na procura dos vértices e a sequência aleatória do percurso.

??? Checkpoint 6

Construa a função **{green}(proximo_vertice(vertice *atual))** para procurar no vértice atual os vizinhos disponíveis e escolher aleartoriamente, entre estes, qual é o próximo vértice no caminho do labirinto e substituir o vértice atual por esse selecionado.

**DICA:** Procure pela função ```c rand()``` para ajudar na escolha aleatória.

::: Gabarito

```c
void proximo_vertice(vertice *atual){
    possíveis vértices <- array para guardar possíveis vértices
    para cada vizinho do array{
        verificar se já foi visitado
            se não, adicionar no array de possíveis vértices
    }
    usar a função rand() para escolher um aleatório
    marca como visitado o atual
    *atual <- próximo vértice
    return
}
```
:::

???

Avaliando a função, encontramos o problema já resolvido teoricamente, o que acontece quando {red}(não) temos nenhum vizinho disponível?

??? Checkpoint 7

Implemente na função a pilha de vértices percorridos

**DICA:** Passe como argumento da função o ponteiro para a pilha

::: Gabarito

```c
void proximo_vertice(vertice *atual, stack_int *s){
    anterior <- recebe ponteiro do vértice anterior
    possíveis vértices <- array para guardar possíveis vértices
    n possíveis vértices <- número de possíveis vértices
    para cada vizinho do array{
        verificar se já foi visitado
            se não, adicionar no array de possíveis vértices
            n possíveis vértices ++
    }
    se n < 1{
        vértice *atual = pop( *s )
        return
    }
    usar a funcao rand() para escolher um aleatório
    marca como visitado o atual
    push(*s, *atual)
    *atual <- próximo vértice
    return
}
```

:::

???

Algoritmo de Aldous-Broder
---------

Depois que entendemos e trabalhamos um pouco com o *Random Walk*, vamos começar pelo algoritmo de **{green}(Aldous-Broder)**.

Para garantir a aleatoriedade do sistema, este algoritmo escolhe aleatoriamente qualquer direção a percorrer, ou seja, não existe nenhuma proibição de avanço.

Pensando na estrutura do *Random Walk*, no algoritmo de Broder a escolha de que caminho seguir **não é levado em consideração os vizinhos já percorridos ou paredes criadas**, e, por isso, na maioria das vezes existem 4 caminhos possíveis para seguir.

??? Checkpoint X

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

O algoritmo de Broder, parte da idéia de ir construindo o labirinto a partir da árvore geradora, com os ramos conectados a ela crescendo, que como vimos apresenta o problema de ser muito lento no final, mas e se houvesse um programa que primeiro construísse estes ramos, pelos pontos desconectados, e depois os "espetassem" na árvore?

??? Checkpoint X

Qual uma possível vantagem desse método em relação ao algoritmo de Aldous-Broder? Pense nas diferenças de comportamento nas operações finais de ambos.

::: Gabarito
Neste caso não haveria a lentidão do algoritmo de Aldous-Broder nas operações finais, já que ele não teria que percorrer as áreas já preenchidas previamente.
:::

???

Como elaborar estes ramos? Primeiro será necessário escolher aleatóriamente um ponto de ínicio deste ramo que não tenha faça parte da árvore geradora, a partir deste ponto o ramo é incrementado até encontrar as áreas já pertencentes a árvore, quando é "espetado" e passa a fazer parte desta. Este processo se repete até todos os pontos do grafo pertencerem a árvore geradora.

Abaixo temos um exemplo da construção de um destes ramos.

:WilsonWay

??? Checkpoint X

Se queremos evitar o mesmo problema do algoritmo de Aldous-Broder, que medida pode ser tomada para evitar percorrer caminhos no qual o ramo já passou?

::: Gabarito
Podemos marcar todos os pontos percorrido e fazer com que o programa os evite.
:::

???

??? Checkpoint X

Essa ideia parece ser boa, mas introduz um problema, qual? Lembre que queremos que o algoritmo gere labirintos de forma imparcial, ou seja, que não haja preferência para um tipo específico de labirito.

::: Gabarito
Ao "desviar" de pontos já percorridos tenderemos a criar caminhos muito longos o que eliminaria um das vantagens de um labirinto gerado a partir de *random-walk* que é a imparcialidade dos tipos de labirintos que são possíveis. Já que deste modo tenderia obter labirintos com corredores muito grandes.
:::

???

PENSAR EM ATIVIDADE PARA OBTER LOOP-ERASED

Então como é possível usar esse método e manter a imparcialidade de geração? Para isso vamos pensar no que acontece quando uma parte do ramo encontra outra, elas criam um loop! Assim se apagamos (*erase*) este *loop* e continuamos o ramo a partir de sua base mantendo o comportamento de *random-walk* até encontrarmos o ramo preservamos a imparcialidade e não percorremos o mesmo caminho mais de uma vez!

Esta ideia é chamade de *loop-erased random walk*!

Abaixo temos uma demonstração do *loop-erased random walk* em ação, caso não tenha entendido algum passo retorne para a explicação acima.

:loopErasedRandomWalk

??? Checkpoint X

Embora esse método apresente estas vantagens, ele introduz um problema, qual? Pense nas primeiras operações quando a árvore geradora é pequena.

::: Gabarito
Nas primeiras operações pode ser que o algoritmo demore para "espetar" na árvore já que há muitos espaços vazios e poucos preenchidos.
:::

???

A ideia de David Bruce Wilson para um algoritmo deste tipo é resumidamente, um programa que recebe
como entrada um grafo e escolhe um vértice não preenchido aleatório de início, então começa o 
*loop-erased random walk*. O processo se repete até obter-se uma árvore geradora completamente preenchida.

As vantagens dessa estratégia é que como resultado obtem-se um labirinto perfeito, ou seja, todos os vértices são acessíveis, e 
entre dois deles há apenas um caminho. Outro benefício do algoritmo de Wilson, mencionado previamente, é que pelo caminho ser definido aleatóriamente
as chances de gerar qualquer tipo de labirinto é uniforme, ou seja não existe viés para tipos especificos de árvores geradoras, um problema presente em outros 
algoritmos de geração de labirintos como se pode ver nas duas figuras abaixo:

![](DepthFirstSearchMaze.png)

![](WilsonMaze.png)

A acima temos um labirinto gerado pelo algoritmo *depth-first search* que tem um viés para gerar labirintos com corredores longos e em baixo temos o algoritmo de Wilson.

Agora que tem uma ideia de como o algorimo funciona, que tal ver uma animação dele em ação? Temos o GIF abaixo e este [site](https://bl.ocks.org/mbostock/11357811) que contém um código que gera um novo labirinto toda vez que você carrega a tela.

![](wilson.gif)

Complexidade do algoritmo de Wilson e comparação com Aldous-Broder
---------
Pelo fato de ser um programa probabilistico, a complexidade do algoritmo de Wilson não é algo simples de ser definida, então vamos colocar os números de lado no momento
("Ufa, engenharia já tem números o suficiente.") e compará-lo com o algoritmo que vimos anteriormente, o algoritmo de Aldous-Broder. De ínicio vamos falar de sua similaridade, ambos utilizam alguma forma de *random walk* para ir preenchendo a árvore geradora, assim, no pior dos casos ambos vão ter a complexidade igual, porém isso
não significa que seus tempo de rodar são iguais. 

Para perceber isso basta analisar suas diferenças, o algoritmo de Aldous-Broder caminha tanto pelas células preenchidas quanto aquelas vazias, preenchendo-as no processo. Isso faz com que o preenchimento seja bem rápido no começo, já que há várias células vazias e poucas preenchidas, o que reduz as chances de já passar por caminho já traçado. Essa mesma qualidade causa o oposto quando esta próximo do fim, quando a maior parte do labirinto já está preenchida o que acaba resultando em várias caminhadas "sem rumo" onde nenhuma célula é adicionada ao labirinto.

O algoritmo de Wilson tem algumas mudanças como vimos, primeiramente os caminhos são apenas traçados por células vazias, só sendo preenchidas quando este encontra alguma célula definida, isto tem o comportamento inverso do Aldous-Broder, sendo mais devagar no começo, quando uma pequena parte do labirinto esta definida sendo difícil de ser encontrada pelo caminho do *loop-erased random walk*, e sendo muito mais rápida no final, quando as chances de encontrar um vértice já definido são muito maiores. 

Entretando embora os comportamentos sejam opostos não significa que ambos demorem o mesmo. O algoritmo de Wilson sempre está diminuindo as suas células disponíveis para percorrer com todas sendo válidas conforme vai preenchendo a árvore geradora. Enquanto o Aldous-Broder sempre tem ```n``` espaços para percorrer com 
o número de células válidas a serem preenchidas diminuindo gradativamente. Isso resulta que, na prática, que o algoritmo de Wilson seja bem mais rápido que o algoritmo de Aldous-Broder tornando-o mais atrativo já que ambos também apresentam as mesmas caracteristicas benéficas de gerarem labirintos perfeitos e com chances uniformes de serem gerados.


Para compravar a análise empirica, podemos ver o gráfico de complexidade de Wilson comparado com outro algoritmo de geração de labirintos: **Aldous-Broder**.

![](complexImg.png)