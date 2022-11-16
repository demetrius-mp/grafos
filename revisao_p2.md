# Revisão P2

## Árvores

- Quaisquer $2$ vértices estão ligados por um único caminho.
- Ao adicionar uma aresta nova em uma árvore, o grafo resultante possui um único circuito
- $|E| = |V| - 1$, ou seja, o número de arestas é igual ao número de vértices $- 1$.
- Árvores com $|V| \geq 3$ possuem pelo menos 2 vértices de grau 1.

## Aresta de corte

- $e$ é aresta de corte $\implies$ $w(G-e) > w(G)$, ou seja, se $e$ é aresta de corte, ao removê-la de um grafo, o número de componentes aumenta.
- $e$ é aresta de corte $\iff$ não existe caminho ligando seus extremos em $G-e$.
- $e$ é aresta de corte $\iff$ $e$ é o único caminho ligando seus extremos.
- $e$ é aresta de corte $\iff$ não existe circuito contendo $e$.
- Um grafo $G$ é conexo e árvore $\iff$ toda aresta em $G$ é de corte.
- Remover uma aresta de corte de um grafo aumenta o número de componentes em no máximo 1, visto que uma aresta liga no máximo 2 componentes distintas.

## Árvore geradora

- $H$ é subgrafo gerador de $G$ $\implies$ $V(H) = V(G)$. Ou seja, um grafo $H$ é subgrafo gerador de $G$ se $H$ possui todos os vértices de G.

- $H$ é subgrafo gerador de $G$, e $H$ é árvore $\implies$ $H$ é árvore geradora.

## Vértice de corte

- $v$ é de corte $\implies$ $w(G-v) > w(G)$
- Remover um vértice de corte de um grao aumenta o número de componentes em uma quantidade arbitrária, visto que um vértice pode ligar diversas componentes distintas.

## Como obter uma árvore geradora de custo mínimo (Algoritmo de Kruskal)

Em cada passo, selecione a aresta de menor custo, e que não forma circuito.

Ou seja:

1. Ordene as arestas pelo custo.
1. Itere sobre elas.
1. Em cada iteração, caso a aresta não forme circuito na solução, inclua ela na solução.

## Grafos eulerianos

- Uma trilha é um passeio que não repete arestas.
- Uma trilha de euler passa por todas as arestas.
- Se um grafo possui uma trilha de euler fechada (uma trilha de euler que inicia e termina no mesmo vértice), ele é chamado de grafo euleriano.
- $G$ é euleriano $\iff$ todo vértice tem grau par.

Intuição de $G$ é euleriano $\implies$ todo vértice tem grau par:

Ao fixar qualquer vértice da trilha, notamos que a trilha utiliza 2 arestas incidentes neste vértice: 1 para "chegar" no vértice, e outra para "sair" (ou vice-versa).

- União de $n$ trilhas fechadas resulta em uma trilha fechada. Este resultado é utilizado para provar que: todo vértice tem grau par $\implies$ $G$ é euleriano.
- Se existe vértice $v$ tal que $d(v) \ge 2$ (grau do vértice é maior ou igual a 2), então o grafo possui uma trilha fechada que contém $v$.
- Um grafo $G$ tem uma trilha de euler $\iff$ $G$ possui no máximo 2 vértices de grau ímpar.

### Algoritmo de Fleury

O algoritmo de Fleury encontra uma trilha de euler em um grafo que possui no máximo 2 vértices de grau ímpar.

Execução:
Em cada passo seleciona uma aresta que não seja de corte no grafo restante, a menos que não haja alternativa. A aresta a ser selecionada deve ser adjacente ao vértice atual.

Ou seja:

1. Crie um grafo $S$ que será a solução
1. Inicie em um vértice de grau ímpar.
1. Escolha uma aresta que não seja de corte, a menos que não haja alternativa.
1. Inclua essa aresta na solução, e remova ela do grafo original.
1. Repita o passo 3, partindo do outro vértice incidente a aresta escolhida, até incluir todas as arestas.

### Encontrando trilha de euler fechada de custo mínimo em um grafo $G$ qualquer

1. Crie um grafo completo auxiliar $K_n$ onde $n$ é o número de vértices de grau ímpar.
1. Neste grafo, defina o pesoa da aresta $e = uv$ como sendo o custo do menor caminho ligando $u$ a $v$ no grafo original $G$.
1. Encontre a $m$-upla de pares de vértices com a menor soma possível, onde $m = \frac{n}{2}$. As arestas da $m$-upla não podem ser adjacentes, ou seja, não pode haver vértices repetidos.
1. No grafo original $G$, duplique as arestas que ligam os vértices escolhidos na $m$-upla.
1. Execute o algoritmo de Fleury no grafo resultante.

## Grafos Hamiltonianos

- Um circuito (passeio que começa e termina no mesmo vértice, sem repetição de vértice) hamiltoniano, é um circuito que contém todos os vértices.
- Um grafo é hamiltoniano se ele contém um circuito hamiltoniano.
- Grafos com vértice de corte não podem ser hamiltonianos.

Intuição: o circuito começa em uma das "componentes" ligadas a $v$. Para chegar na outra componente, o circuito utiliza o vértice $v$, o que torna impossível retornar a component inicial para fechar o circuito, sem repetir o vértice $v$.

Generalização: Se existe conjunto não vazio $S \subseteq V(G)$, tal que $w(G-S) > |S|$, $G$ não é hamiltoniano. Ou seja, se existe um conjunto de $n$ vértices de corte, cuja remoção faz com que o número de componentes do grafo resultante seja maior que $n$, $G$ não é hamiltoniano.

Vale destacar que esta confição não é suficiente, ou seja, a recíproca não é verdadeira.

- Seja $G$ simples com $n$ vértices. Se existem vértices $u$ e $v$ não adjacentes tal que $d(u) + d(v) \geq n$, entao $G$ é hamiltoniano $\iff$ $G + (u,v)$ é hamiltoniano. Ou seja, se existir par de vértices não adjacentes cuja soma dos graus seja maior que o número de vértices, ao adicionar uma aresta ligando esse par, o grafo resultante mantém a propriedade de ser hamiltoniano ou não.
- Se $G$ é simples com $n \geq 3$ vértices, e $\delta \geq \frac{n}{2}$, então $G$ é hamiltoniano.
- Também é possível provar que um grafo não é hamiltoniano utilizando contradição:
Assumindo por contradição que existe um circuito contendo todos os vértices, e mostrando que isso contradiz alguma propriedade do grafo original.
- Um caminho hamiltoniano é um caminho que contém todos os vértices, mas não começa e termina no mesmo vértice.
