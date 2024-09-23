## Questão 1 - 2018.1.1

Usando combinações de Máquinas de Turing, construa uma Máquina de Turing não determinística que aceite a seguinte linguagem:

$$L = \{1^m 1^n \mid m \text{ é divisível por } n\}$$

Máquinas que podem ser utilizadas: $NB$, $PB$, $Copy$, $Equal$, $Delete$, $Insert(\sigma)$, $M$, $R$, $G$, além de alguma que você implemente e possa utilizar como macro. Note ainda que $M$, $R$ e $G$ são respectivamente as Máquinas de Turing que efetuam a multiplicação, reverso e geração de uma string aleatória.

## Questão 6 - 2018.1.1

Apresente uma Máquina de Turing que aceite a linguagem

$$L = \{ww^Rw \mid w \in \{0, 1\}^*\}$$

## Questão 2 - 2019.1.1

Suponha que $M$ é uma Máquina de Turing aceitando a linguagem $L$. Descreva informalmente (mas de maneira precisa) como construir uma Máquina de Turing aceitando $L^*$.

Observação: relembre que $L^* = \{w_1\ldots w_n \mid n \ge 0 \text{ e } \forall i, w_i \in L\}$

## Questão 6 - 2019.1.1

Apresente uma Máquina de Turing que receba como entrada $\Delta x \Delta y$, em que $x, y \in \{a, b\}^*$, e pare em $h_a$ se e somente se $x$ é uma substring de $y$.

## Questão 1 - 2021.1.1

Seja

$$L = \{1^n \mid n \in \mathbb{N} \text{, e } n \text{ é a soma de dois quadrados perfeitos}\}$$

Apresente uma Máquina de Turing Não-Determinística com uma única fita que aceite a linguagem $L$. Nesta questão, você poderá fazer uso de Máquinas de Turing (macros) como $Insert(1)$, $Insert(\Delta)$, $NB$, $PB$, $Copy$, $Delete$, $Equal$. Além disso, você pode fazer uso da Máquina de Turing $G$ (que gera uma quantidade aleatória de 1's) e a Máquina de Turing $X^2$, que recebe como entrada $\underline{\Delta}1^x$ e retorna como saída $\underline{\Delta}1^{x^2}$ (em que a parte sublinhada indica a posição do caractere que está sendo lido naquele momento).

Exemplos: $\epsilon$, 1, 11, 1111, 11111 são exemplos de palavras que estão nessa linguagem.

## Questão 1 - 2023.1.1

Seja $M = (Q, \Sigma, \Gamma, q_0, \delta)$ a Máquina de Turing (com uma única fita) que aceita a linguagem $L$. Construa uma Máquina de Turing Não Determinística com uma única fita que aceita a linguagem

$$L^* = \{w_1 w_2 \ldots w_n \mid n \ge 0 \text{, e cada } w_i \in L \text{ com } i \in \{1,\ldots,n\}\}$$

Nesta questão, você pode fazer uso como macro somente a própria Máquina de Turing $M$ e $Insert(\sigma)$.

## Questão 3 - 2023.1.AF

Construa uma Máquina de Turing Não Determinística que reconheça a linguagem dos palíndromos sobre $\{a,b\}*$.