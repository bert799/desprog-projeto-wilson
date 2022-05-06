Algoritmo de Wilson para Construção de Labirintos
======

Algoritmos de criação de labirintos
---------

Mas qual é a finalidade de construir labirintos por meio de um algoritmo?

* Construção de labirintos para entusiastas, deixando-os mais complexos;
* Criação de estruturas de dados enormes para testar e treinar algoritmos de *patch finding*.

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

??? Exercício 1:

Sabendo que para construir um labirinto os caminhos devem ser escolhidos aleatoriamente para garantir que existam vários tipos de construção para a mesma estrutura, como você construiria a função que percorre pelos vértices do grafo para marcar o caminho?

**Obs. 1:** Neste momento não é necessário desenvolver o código, somente uma resposta de como ele funcionaria.

**Obs. 2:** Esta função deve ser pensada para rodar por vértice, então pense como funcionaria dentro de um deles.

::: Gabarito

O código deve, a partir de um determinado vértice, escolher `md aleatoriamente` um **vizinho** que será o próximo a ser analisado, marcando o atual como um vértice já visitado. Depois devemos redefinir os vizinhos para serem somente o anterior a ele e o próximo escolhido, de modo a formar o caminho por onde o labirinto passa.

:::

???

Este conceito de varredura aleatória para a construção de labirintos é conhecido como [Random Walk](https://en.wikipedia.org/wiki/Random_walk), mas possui uma diferença:

??? Exercício 2:

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

??? Exercício 3

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

??? Exercicio 4

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
