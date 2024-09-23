## Questão 2 - 2018.1.1

Seja $M = (Q, \Sigma, \Gamma, q_1, \delta)$ uma Máquina de Turing Determinística com uma fita que sempre se desloca à direita, em que $Q = \{q_1, _2, \ldots, q_n\}$ e $\Sigma = \{a, b\}$. Dada uma entrada vazia para $M$, a partir de quantos movimentos será possível determinar com absoluta certeza que $M$ entro em "loop"?

Dica: observe que o estado inicial é $q_1$.

## Questão 1 - 2019.1.1 (Fácil)

Encontre uma Máquina de Turing Determinística com uma fita que compute a função

$$resto(x_1, x_2)$$

que retorna o resto da divisão de $x_1$ por $x_2$.

Exemplos: $resto(x_1, 0)\uparrow$, $resto(5,3) = 2$,  $resto(6,3) = 0$

## Questão 3 - 2020.1.AF

Encontre uma Máquina da Turing Determinística (e sem usar macros) que aceite a linguagem

$$\{a^i b^j c^k \mid i \leq j \leq k\}$$

## Questão 2 - 2021.1.1

Encontre uma Máquina de Turing Determinística com uma fita que compute na notação unária a função

$$\left| x_1 - x_2 \right|$$

que retorna a diferença absoluta entre $x_1$ e $x_2$. Nesta questão, você poderá fazer uso de Máquinas de Turing (macros) como $Insert(\sigma)$, $Delete$, $NB$, $PB$, $Equal$.

Exemplos: $\left| 0 - x_2 \right| = x_2$, $\left| 3 - 5 \right| = 2$, $\left| 5 - 3 \right| = 2$.

## Questão 2 - 2023.1.1

Encontre uma Máquina de Turing Determinística com uma fita que compute a função $f : \{a,b\}^* \rightarrow \{0, 1\}$, em que

$$
f(w) =
\left\{
\begin{array}{ll}
1 & \text{se } n_a(w) = 2n_b(w)\\
0 & \text{caso contrário}
\end{array}
\right.
$$

Isso quer dizer que a Máquina de Turing vai receber como entrada uma string em $\{a, b\}^*$ (podendo ser a string vazia) e retornar como saída 1 ou 0. Nesta questão, você não poderá usar macros.
