## Questão 2 - 2016.1.1

Uma função parcialmente computável $h_1(x)$ é estendível se há uma função computável $h_2(x)$ tal que $h_1(x) = h_2(x)$ para todo $x$ para os quais $h_1(x)\downarrow$. Ademais, seja $P(z)$ o seguinte predicado:

$$
P(z) =
\left\{
\begin{array}{ll}
1 & \text{se } \Phi_z(x) \text{ é estendível}\\
0 & \text{caso contrário}
\end{array}
\right.
$$

Usando o Teorema de Rice, mostre que $P(z)$ não é computável.

### Resposta:

Seja $A = \{z \in \mathbb{N} \mid P(z) = 1\}$, onde $z$ é o código de um programa.

Se reduzirmos $A = R_{\Gamma}$, podemos definir o $\Gamma$ da seguinte forma

$$\Gamma = \{f \mid f \text{ é parcialmente computável e estendível}\}$$

- $f(x) = 0 \in \Gamma$. Ele é estendível porque podemos definir a função total computável $h_2(x) = 0$ para todos os $x$. Aqui, $h_1(x) = f(x) = 0$ para todos os $x$ onde $f(x)$ está definido.

- $g(x) = \Phi(x, x) \notin \Gamma.$

Portanto, $P(z)$ não é computável.

## Questão 2 - 2021.1.1

Com relação aos conjuntos abaixo, demonstre que eles não são recursivos através do Teorema de Rice

(a) $A = \{y \in \mathbb{N} \mid \forall x[\Phi(x, y)\downarrow \wedge \Phi(x, y) > x]\}$

(b) $B = \{x \in \mathbb{N} \mid \overline{W_x} \text{ é infinito}\}$

Em que $W_x = \{y \in \mathbb{N} \mid \Phi(y, x)\downarrow\}$ Repare ainda que $\overline{W_x}$ é o complemento de $W_x$.

## Questão 3 - 2021.1.2

Com relação aos conjuntos abaixo, demonstre que eles não são recursivos através do Teorema de Rice

(a) $A = \{x \in \mathbb{N} \mid \left|W_x\right| \ge 5\}$

(b) $B = \{x \in \mathbb{N} \mid \overline{W_x} \neq \emptyset\}$

Em que $W_x = \{y \in \mathbb{N} \mid \Phi(y,x)\downarrow\}$. Repare ainda que $\left|W_x\right| \ge 5$ significa que o conjunto $W_x$ possui pelo menos 5 elementos, e $\overline{W_x}$ é o complemento de $W_x$.

## Questão 2 - 2023.1.1

Com relação aos conjuntos abaixo, demonstre que eles não são recursivos através do Teorema de Rice:

(a) $A = \{x \in \mathbb{N} \mid \Phi(y, x)\downarrow \text{ para todo }y\text{ que é um número primo}\}$.

(b) $B = \{x \in \mathbb{N} \mid 5 \leq \left| W_x \right|\}$, em que $\left|W_x\right|$ representa o número de elementos (cardinalidade) de $W_x$.

Observação: para cada item acima, antes de aplicar o Teorema de Rice, você deve apresentar o que é o conjunto $\Gamma$ correspondente de funções parcialmente computáveis.

### Resposta:

- (a) $A = \{x \in \mathbb{N} \mid \Phi(y, x)\downarrow \text{ para todo }y\text{ que é um número primo}\}$

Seja $PRIMO(x)$ uma função computável que é definida como

$$
PRIMO(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \text{ é primo}\\
0 & \text{caso contrário}
\end{array}
\right.
$$

Passo 1: Defino $\Gamma = \{f \mid f \text{ é P.C. e } f(x)\downarrow \text{ sempre que } x \text{ é primo}\}$

Passo 2:

Escolho $f(x)$ como sendo

$$
f(x) =
\left\{
\begin{array}{ll}
1 & \text{se } PRIMO(x) = 1\\
\uparrow & \text{caso contrário}
\end{array}
\right.
$$

Veja que $f(x) \in \Gamma$.

Agora escolho $g(x)$ como sendo

$\forall x g(x)\uparrow$

Então $g(x) \notin \Gamma$.

Portanto, $A$ não é recursivo.

- (b) $B = \{x \in \mathbb{N} \mid 5 \leq \left| W_x \right|\}$, em que $\left|W_x\right|$ representa o número de elementos (cardinalidade) de $W_x$.

$x \in B$ se e somente se existem pelo menos 5 valores distintos de $y$ tal que $\Phi(y, x)\downarrow$.

Defino $\Gamma = \{f \mid f(x) \text{ está definida para pelo menos 5 valores distintos de } x\}$

Busco um exemplo de $f(x) \in \Gamma$:

$$
f(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \text{ é par}\\
\uparrow & \text{caso contrário}
\end{array}
\right.
$$

Busco um exemplo de $g(x) \notin \Gamma$:

$$
g(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x = 0\\
\uparrow & \text{caso contrário}
\end{array}
\right.
$$

Portanto, $B$ não é recursivo.

## Questão 1 - 2023.1.2

Demonstre através do Teorema de Rice que

$$A = \{x \in \mathbb{N} \mid W_x \text{ é um conjunto recursivo}\}$$

não é um conjunto recursivo.

Note que $W_x  = \{y \in \mathbb{N} \mid \Phi(y,x)\downarrow\}$

Observação: antes de aplicar o Teorema de Rice, o mais importante nesta questão é identificar corretamente o conjunto $\Gamma$ de tal forma que $A = R_{\Gamma} = \{p \in \mathbb{N} \mid \text{ p é o código de um programa que computa a função } h(z) \text{ e } h(z) \in \Gamma\}$

### Resposta:

$$\Gamma = \{f(x) \mid f \text{ é parcialmente computável e } Dom(x) \text{ é um conjunto recursivo}\}$$

Um exemplo de $g(x)$ que pertence a $\Gamma$ é 

- $g(x) = 0$, pois $Dom(g) = \mathbb{N}$, então $g(x) \in \Gamma$

- $h(x) = \Phi(x,x)$, pois $Dom(h) = K$, então $h(x) \notin \Gamma$

Portanto, $A = R_{\Gamma}$ não é recursivo.