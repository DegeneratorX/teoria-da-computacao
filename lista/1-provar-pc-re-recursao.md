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