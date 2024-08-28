## Questão 4 - 2016.1.1

Sejam $A = \{s_1, s_2\}$ e

$$
f(w_1, w_2) =
\left\{
\begin{array}{ll}
w_1 & \text{se } w_1 \text{ vem antes de } w_2 \text{ de acordo com a ordem alfabética de } A\\
w_2 & \text{caso contrário}
\end{array}
\right.
$$

Mostre que a função $f$ é computável em $\mathscr{L}_2$.

## Questão 1 - 2021.1.1

Sejam $\Sigma_3 = \{s_1, s_2, s_3\}$ e

$$
f(w_1, w_2) =
\left\{
\begin{array}{ll}
s_1 & \text{se } w_1 \text{ é uma substring de } w_2\\
\epsilon & \text{caso contrário}
\end{array}
\right.
$$

Mostre que $f(x)$ é computável em $\mathscr{L}_3$ (a nossa linguagem de programação baseada em strings cujo alfabeto é $\Sigma_3$), construindo um programa em $\mathscr{L}_3$ e justificando que esse programa sempre para. Além de mostrar esse programa, você deve explicar com as suas próprias palavras a sua intução e explicar através de um exemplo a execução do seu programa.

Nesta questão, você poderá fazer uso das seguintes macros:

```
IF V != 0 GOTO L
V ← 0
GOTO L
V ← V'
```

Observação: A palavra vazia $\epsilon$ é substring de qualquer palavra; qualquer palavra $w$ é substring de si mesma, ou seja, $w$ é substring de $w$.

## Questão 2 - 2021.1.2

Sejam $\Sigma_2 = \{s_1, s_2\}$ e

$$
f(x) =
\left\{
\begin{array}{ll}
s_1 & \text{se } x = ww^R\\
\epsilon & \text{caso contrário}
\end{array}
\right.
$$

em que $w \in \Sigma_{2}^{*}$ e $w^R$ é o reverso de $w$, isto é, se $w = a_1a_2\ldots a_{m-1}a_m$, então $w^R = a_m a_{m-1} \ldots a_2 a_1$. Mostre que $f(x)$ é computável em $\mathscr{L}_2$ (a nossa linguagem de programação baseada em strings cujo alfabeto é $\Sigma_2$), construindo um programa em $\mathscr{L}_2$ e justificando que esse programa sempre para.

## Questão 3 - 2023.1.1

Sejam $\Sigma_3 = \{s_1, s_2, s_3\}$ e

$$
f(w_1,w_2) =
\left\{
\begin{array}{ll}
s_1 & \text{se } w_1 \leq_a w_2\\
\epsilon & \text{caso contrário}
\end{array}
\right.
$$

em que $w_1 \leq_a w_2$ se e somente se $w_1 = w_2$ ou $w_1$ vem antes de $w_2$ pela ordem alfabética.

Mostre que $f(x)$ é computável em $\mathscr{L}_3$ (a nossa linguagem de programação baseada em strings cujo alfabeto é $\Sigma_3$), construindo um programa em $\mathscr{L}_3$ e justificando que esse programa sempre para.

Exemplos:

- $f(\epsilon, w_2) = s_1$ para qualquer $w_2$, pois a palavra vazia vem antes de qualquer outra palavra pela ordem alfabética.

- $f(w, w) = s_1$ para qualquer $w$.

- $f(s_1s_2, s_2) = s_1$

- $f(s_2s_1, s_1) = \epsilon$

- $f(s_1s_1, s_1) = \epsilon$

## Questão 2 - 2023.1.2

Sejam $\Sigma_3 = \{s_1, s_2, s_3\}$ e

$$
f(x) =
\left\{
\begin{array}{ll}
y & \text{se } x = \sigma y \text{ em que } \sigma \in \Sigma_3\\
\epsilon & \text{se } x = \epsilon
\end{array}
\right.
$$

ou seja, $f(x)$ retorna a string $x$ sem a primeira letra se $x$ não é a string vazia. Caso $x$ seja a string vazia, $f(x)$ retorna a própria string vazia.

Mostre que $f(x)$ é computável em $\mathscr{L}_3$ (a nossa linguagem de programação baseada em strings cujo alfabeto é $\Sigma_3$), construindo um programa em $\mathscr{L}_3$ e justificando que esse programa sempre para.