## Questão 6 2016.1.1 e Questão 5 2021.1.1

Mostre se há algo de errado ou não com a seguinte prova por diagonalização; Justifique sua resposta!

Nós iremos mostrar uma função parcialmente computável $f : \mathbb{N} \rightarrow \mathbb{N}$ que não está enumerada em $\Phi_0, \Phi_1, \ldots$. Para tanto, define-se:

$$f(n) = \Phi(n,n) + 1$$

Ora, é fácil ver que $f(n)$ é parcialmentte computável, pois é baseada na composição de duas funções parcialmente computáveis. Isso quer dizer que há um programa $\mathcal{P}$ que computa $f$. Fazendo $\#(\mathcal{P}) = p$, tem-se que

$$f(p) = \Phi(p,p) + 1$$

Ocorre que

$$\Phi(p,p) = f(p)$$

Das duas equações anteriores, conclui-se que

$$f(p) = f(p) + 1$$

Um absurdo! Logo, para todo $i$, $f(x) \neq \Phi(x, i)$, ou seja, há uma função parcialmente computável $f$ que não está enumerada em $\Phi_0, \Phi_1, \ldots$.

## Questão 4 - 2021.1.2

Mostre por Diagonalização que o conjunto

$$A = \{x \in \mathbb{N} \mid \Phi(x,x)\downarrow \text{ e } \Phi(x,x) = z \text{, em que } z \text{ é um número par}\}$$

não é recursivo.

## Questão 5 - 2023.1.1

Prove por diagonalização que o conjunto

$$A = \{x \in \mathbb{N} \mid x > 0 \text{ e } \Phi(x-1, x)\downarrow\}$$

não é recursivo.

Observação: $\Phi(x-1,x)$ é a função universal, que é parcialmente computável e retorna o que o programa de código $x$ com entrada $x-1$ retorna. Ademais, temos que $\Phi(x-1,x)\downarrow$ significa que o programa de código $x$ com entrada $x-1$ para.

## Questão 4 - 2023.1.2

Numa tentativa de provar por diagonalização que

$$B = \{x \mid W_x \text{ é infinito}\}$$

não é recursivo, foi redigido o seguinte esborço:

Por absurdo, vamos assumir que $B$ é recursivo. Isso significa que a função

$$
P_B(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \in B\\
0 & \text{caso contrário}
\end{array}
\right.
$$

é computável. Logo, podemos construir o seguinte programa $\mathcal{P}$:

```
[A] IF P_B(X1) = 1 GOTO A
```

A partir deste programa $\mathcal{P}$, seria possível chegar a um absurdo usando o argumento da diagonalização e com isso, concluir que $B$ não é recursivo? Justifique sua resposta.