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

## Questão 1 - 2023.1.2

Demonstre através do Teorema de Rice que

$$A = \{x \in \mathbb{N} \mid W_x \text{ é um conjunto recursivo}\}$$

não é um conjunto recursivo.

Note que $W_x  = \{y \in \mathbb{N} \mid \Phi(y,x)\downarrow\}$

Observação: antes de aplicar o Teorema de Rice, o mais importante nesta questão é identificar corretamente o conjunto $\Gamma$ de tal forma que $A = R_{\Gamma} = \{p \in \mathbb{N} \mid \text{ p é o código de um programa que computa a função } h(z) \text{ e } h(z) \in \Gamma\}$