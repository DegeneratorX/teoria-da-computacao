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

### Resposta:

Considere o programa $\mathcal{P}$:

```
     Z1 ← W1
     Z2 ← W2

[A]  Z3 ← STARTOF(Z1)
     IF Z3 = e GOTO D
     Z4 ← STARTOF(X2)
     IF Z4 = e GOTO E
     IF Z3 ENDS s_i GOTO Bi   // 1 <= i <= 3

[Bi] IF Z4 ENDS s_1 GOTO C    // INICIO DO BLOCO Bi, 1 <= i <= 3
     IF Z4 ENDS s_2 GOTO C    //
     IF Z4 ENDS s_2 GOTO C    //
     IF Z4 <= s_i GOTO E      // 1 <= I <= 3
     GOTO D                   // FIM DO BLOCO Bi, 1 <= i <= 3

[C]  Z1 ← -Z1
     Z2 ← -Z2
     GOTO A

[D]  Y ← s_1
```

O programa sempre para, pois todos os seus $GOTO$'s não terminais (isto é, $GOTO$'s onde a label é diferente de $[E]$ e $[D]$, pois $[D]$ claramente encerra o programa após a sua execução) estão em funções das linhas

```
     Z1 ← -Z1
```

e

```
     Z2 ← -Z2
```

Estamos decrementando o tamanho de $Z_1$ e $Z_2$ e sempre chegaremos a algum $GOTO$ terminal eventualmente.

Macros utilizadas (obrigatório):

- $STARTOF(V)$:
```
     Z1 ← V
     IF Z1 = e GOTO E
[A]  Z2 ← Z1
     Z1 ← Z1-
     IF Z1 != e GOTO A
     Y ← Z2
```

- $\leq$
```
     Z1 ← STARTOF(X1)
     X2 ← STARTOF(X2)
     IF Z1 != e GOTO A

[D]  Y ← s_1
     GOTO E

[A]  IF Z2 != e GOTO B
     GOTO E

[B]  IF Z1 ENDS s_1 GOTO D
     IF Z1 ENDS s_2 GOTO B2
     IF Z1 ENDS s_3 GOTO B3

[B2] IF Z2 ENDS s_1 GOTO E
     GOTO D

[B3] IF Z2 ENDS s_1 GOTO E
     IF Z2 ENDS s_2 GOTO E
     GOTO D
```

- $V ← -V$

```
     IF Z1 ENDS s_i GOTO Ai   // 1 <= i <= 3
[B]  Y ← Z2
     GOTO E

[Ai] Z1 ← Z1-
     IF Z1 = e GOTO B
     Z2 ← s_iZ2
     GOTO B
```

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

### Resposta:

Nosso programa seguirá a seguinte lógica: manteremos na variável $Z$ o último símbolo lido da entrada, e concatenaremos a saída somente no caso da entrada não tiver sido inteiramente esgotada. Desse modo, o programa terá o efeito de remover o primeiro símbolo entrado.

Segue o programa:

```
[D]  IF X ENDS s_1 GOTO A1
     IF X ENDS s_2 GOTO A2
     IF X ENDS s_3 GOTO A3
     GOTO E

[A1] X ← X-
     IF Z ENDS s_1 GOTO B1
     IF Z ENDS s_2 GOTO B2
     IF Z ENDS s_3 GOTO B3
     GOTO C

[B1] Y ← s_1Y
     Z ← 0
[C]  Z ← s_1Z
     GOTO D

[A2] X ← X-
     IF Z ENDS s_1 GOTO B1
     IF Z ENDS s_2 GOTO B2
     IF Z ENDS s_3 GOTO B3
     GOTO C

[B2] Y ← s_2Y
     Z ← 0
[C]  Z ← s_2Z
     GOTO D

[A3] X ← X-
     IF Z ENDS s_1 GOTO B1
     IF Z ENDS s_2 GOTO B2
     IF Z ENDS s_3 GOTO B3
     GOTO C

[B3] Y ← s_3Y
     Z ← 0
[C]  Z ← s_3Z
     GOTO D
```

O programa para uma vez que cada iteração do seu único laço $[D]$ retiramos o último símbolo da entrada e sua condição de parada é justamente que ela esteja vazia.