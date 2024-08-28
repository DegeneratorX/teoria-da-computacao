## Questão 3 - 2016.1.1

Encontre uma função parcialmente computável $k(x)$ tal que

$$
h(x, t) =
\left\{
\begin{array}{ll}
\Phi(x,x) + 1 & \text{se } \Phi(t,t)\downarrow\\
k(x) & \text{caso contrário}
\end{array}
\right.
$$

Seja também parcialmente computável. Justifique sua resposta.

### Resposta:

Veja que $k(x)\uparrow$ já satisfaz.

Se $k(x)$ é parcialmente computável, tem programa. Se eu quero que entre sempre em loop, então

```
[A] GOTO A
```

É o programa que computa $k$. Assim temos

$$
h(x, t) =
\left\{
\begin{array}{ll}
\Phi(x,x) + 1 & \text{se } \Phi(t,t)\downarrow\\
\uparrow & \text{se } \Phi(t,t) \uparrow
\end{array}
\right.
$$

Como $\Phi(x,x) + 1$ e $k(x)$ são parcialmente computáveis, então $h(x,t)$ também é parcialmente computável.

## Questão 1 - 2020.1.AF

Sejam $A$, $B$, $C$ subconjuntos de $\mathbb{N}$ tais que $A \cap B = B \cap C = C \cap A = \emptyset$. Ademais, assuma que há três funções parcialmente computáveis $f_1$, $f_2$ e $f_3$ com as seguintes propriedades:

$$
f_1(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \in A \cup B\\
2 & \text{se } x \in C\\
\uparrow & \text{caso contrário}
\end{array}
\right.
$$

$$
f_2(x) =
\left\{
\begin{array}{ll}
\uparrow & \text{se } x \in A \cup C\\
0 & \text{caso contrário}
\end{array}
\right.
$$

$$
f_3(x) =
\left\{
\begin{array}{ll}
\uparrow & \text{se } x \in B \cup C\\
0 & \text{caso contrário}
\end{array}
\right.
$$

Prove que 

$$
P_B(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \in B\\
0 & \text{se } x \notin B
\end{array}
\right.
$$

é computável.

Observação: Note que não é garantido que $A \cup B \cup C = \mathbb{N}$.

## Questão 4 - 2020.1.AF e Questão 4 2023.1.1 AF

Prove ou refute os seguintes resultados

(a) Se $A$ é r.e. e $B$ não é r.e., então $A \cup B$ é r.e.

(b) Se $A$ é r.e. e $B$ não é r.e., então $A \cup B$ não é r.e.

Justifique cada uma de suas respostas.

## Questão 6 - 2020.1.AF

O conjunto $A = \{x \in \mathbb{N} \mid 3 \leq \left|W_x\right|\}$ é recursivamente enumerável? Justifique sua resposta.

Observação: por definição, $W_x = \{y \in \mathbb{N} \mid \Phi(y,x)\downarrow\}$, e $\left|W_x\right|$ representa o número de elementos de $W_x$.

## Questão 3 - 2021.1.1

Mostre que a função

$$
f(x) =
\left\{
\begin{array}{ll}
HALT(x, x) & \text{se } x > 0\\
\uparrow & \text{se x = 0}
\end{array}
\right.
$$

não é parcialmente computável.

## Questão 1 - 2021.1.2

O conjunto

$$A = \{\left<x, y\right> \mid \Phi(x, y) = x + y\}$$

é recursivamente enumerável? Justifique sua resposta.

Obsevação: $\left<x, y\right> = 2^x(y+1) ∸ 1$ é uma função de pareamento.

## Questão 1 - 2023.1.1

Mostre que o conjunto $A = \{x \in \mathbb{N} \mid \{0,1,\ldots,x\} \subseteq W_x\}$ é recursivamente enumerável.

Observação: $W_x = \{y \in \mathbb{N} \mid \Phi(y,x)\downarrow\}$.

### Resposta:

Se $A$ é r.e., então temos que $A = \{x \in \mathbb{N} \mid h(x)\downarrow\}$, onde $h$ é parcialmente computável.

Considere o programa $\mathcal{P}$:

```
[A] Z1 ← X
    Z2 ← Phi(Z1, X)
    IF X = 0 GOTO E
    Z1 ← Z1 -1
    GOTO A
```

Note que o programa para sempre que $\Phi(0, X),\ldots,\Phi(X,X)$ estão definidos, e entra em loop caso contrário. O programa $\mathcal{P}$ portanto computa a função parcialmente computável $h$, e portanto $A$ é recursivamente enumerável.

## Questão 3 - 2023.1.2

Sejam $A$, $B$ e $C$ subconjuntos de $\mathbb{N}$ tais que $A \cap B = B \cap C = C \cap A = \emptyset$. Ademais, assuma que há as funções parcialmente computáveis $\Phi(x, p)$ e $\Phi(x, q)$ com as seguintes propriedades:

$$
\Phi(x,p) =
\left\{
\begin{array}{ll}
0 & \text{se } x \in A \cup C\\
1 & \text{se } x \in B\\
\uparrow & \text{caso contrário}
\end{array}
\right.
$$

$$
\Phi(x,q) =
\left\{
\begin{array}{ll}
\uparrow & \text{se } x \in A \cup B\\
0 & \text{caso contrário}
\end{array}
\right.
$$

(a) Mostre que $B$ é recursivamente enumerável

(b) Com base na informação disponível, é possível assegurar que o conjunto $A$ é recursivamente enumerável? Justifique.

Observações:
- Não é garantido que $A \cup B \cup C = \mathbb{N}$
- $p, q \in \mathbb{N}$ são constantes e representam códigos de programas.
- A função $\Phi(x,y)$ é a função universal, que é parcialmente computável e retorna o que o programa de código $y$ com entrada $x$ retorna.

### Resposta:

- (a) $B$ é recursivamente enumerável, dado que podemos construir o seguinte programa que para se e somente se sua entrada está em $B$:

```
    Z ← Phi(X, p)
[A] IF Z = 0 GOTO A
```

- (b) Nem mesmo a execução em paralelo dos programas $p$ e $q$ seria suficiente para determinar se $x \in A$, visto que nesse caso, $\Phi(x, p) = 0$, o que indica apenas que $x \in A \cup C$. Logo, resta-nos ainda determinar qual deses conjuntos $x$ pertence, de modo que a única possibilidade restante é recorrer a execução de $q$ na esperança de obter mais informações acerta de $x$. No entando, se $x \in A$, então $\Phi(x, q)\uparrow$, e o programa entra em loop infinito.

## Questão 6 - 2023.1.AF

Determine se o conjunto $A = \{x \in \mathbb{N} \mid W_x \ge 2\}$ é r.e.

Observação: $W_x = \{y \in \mathbb{N} \mid \Phi(y, x)\downarrow\}$, ou seja, o conjunto de entradas para as quais o programa de código $x$ está definido.