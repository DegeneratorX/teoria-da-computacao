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

### Resposta:

Decifrando $A$: Conjunto de programas para os quais param com entrada sendo o próprio código, e que retornam um número par

Suponha por absurdo que $A$ é recursivo. Então

$$
P_A(x) =
\left\{
\begin{array}{ll}
1 & \text{se } \Phi(x,x)\downarrow \wedge \Phi(x,x) = z \text{, com z par}\\
0 & \text{caso contrário}
\end{array}
\right.
$$

A função característica $P_A$ é computável, portanto posso usar como macro de um programa $\mathcal{P'}$:

```
    IF P_A(X) GOTO A
    GOTO B
[A] Y ← 1
    GOTO E
[B] Y ← 2
```

Fazendo $\Psi_{\mathcal{P'}}(x)$, temos dois possíveis resultados

Se $P_A(X) = 1$, $x \in A$, ou seja

- $\Phi(x,x) = \text{par}$ e $\Psi_{\mathcal{P'}}(x) = \text{impar}$

Se $P_A(X) = 0$, $x \notin A$, ou seja

- $\Phi(x,x) = \text{impar}$ e $\Psi_{\mathcal{P'}}(x) = \text{par}$

Só que se eu passo o próprio código de $\mathcal{P'} = p'$ como entrada de $\Psi_{\mathcal{P'}}(p')$:

Se $P_A(p') = 1$, $p' \in A$, ou seja

- $\Phi(p',p') = \text{par}$, mas no programa $\Psi_{\mathcal{P'}}(p') = \text{impar}$

Se $P_A(p') = 0$, $p' \notin A$, ou seja

- $\Phi(p',p') = \text{impar}$, mas no programa $\Psi_{\mathcal{P'}}(p') = \text{par}$

Absurdo. Portanto, $A$ não é recursivo.

## Questão 5 - 2023.1.1

Prove por diagonalização que o conjunto

$$A = \{x \in \mathbb{N} \mid x > 0 \text{ e } \Phi(x-1, x)\downarrow\}$$

não é recursivo.

Observação: $\Phi(x-1,x)$ é a função universal, que é parcialmente computável e retorna o que o programa de código $x$ com entrada $x-1$ retorna. Ademais, temos que $\Phi(x-1,x)\downarrow$ significa que o programa de código $x$ com entrada $x-1$ para.

### Resposta:

Suponha por absurdo que $A$ é recursivo. Como $A$ é recursivo, temos que 

$$
P_A(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x > 0 \wedge \Phi(x-1,x)\downarrow\\
0 & \text{caso contrário}
\end{array}
\right.
$$

Onde $P_A$ é a função característica de $A$, e $P_A$ é computável.

Considere o programa $\mathcal{P}$, onde $\#(\mathcal{P}) = p$:

```
    Z ← X + 1
[A] IF P_A(Z) GOTO A
```

Iremos mostrar por diagonalização que $\Psi_P$ não está na enumeração de todos os programas computáveis $\Psi_0, \Psi_1, \Psi_2, \ldots$.

$$
\Psi_{\mathcal{P}}(p-1) =
\left\{
\begin{array}{ll}
0 & \text{se } \neg P_A(p)\\
\uparrow & \text{se } P_A(p)
\end{array}
\right.
$$

**Caso 1: $\Psi(p-1) = 0$** 

Como $\Psi(p-1) = 0$, temos que $\neg P_A(p) \Rightarrow p \leq 0 \vee \Phi(p-1, p)\uparrow$. Como $p = \#(P)$, temos que $p \neq 0$. Temos também que $\Phi(p-1, p)\uparrow$, porém note que $\Phi(p-1, p) = \Psi_P(p-1) = 0$, um absurdo.

**Caso 2: $\Psi(p-1)\uparrow$**

Como $\Psi(p-1)\uparrow$, temos que $P_A(p) \Rightarrow p > 0 \wedge \Phi(p-1, p)\downarrow$. Em particular, temos que $\Phi(p-1, p)\downarrow = \Psi(p-1)\downarrow$. Um absurdo, pois $\Psi_P(p-1)\uparrow$.

Concluimos então que $P_A$ não é computável, pois $\Psi_P \notin \{\Psi_0, \Psi_1, \Psi_2, \ldots\}$. E como $P_A$ não é computável,temos que $A$ não é recursivo.

### Resposta Alternativa:

Decifrando A: Conj. programas que não são vazios e que param com entrada do próprio código -1.

Por absurdo, suponha "A" recursivo.

$$
P_A(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x > 0 \wedge \Phi(x-1,x)\downarrow\\
0 & \text{caso contrário}
\end{array}
\right.
$$

Posso usar como macro em $\#(P') = p'$

```
    Z ← X + 1
[A] IF P_A(Z) GOTO A
```

Fazendo $\Psi_{\mathcal{P'}}(x)$, temos dois possíveis resultados

Se $P_A(Z) = 1$, $x \in A$, ou seja

- $\Phi(x-1,x)\downarrow \wedge x > 0$, e o programa $\mathcal{P'}$ entra em loop com $\Psi-{\mathcal{P'}}(x-1)$.

Se $P_A(X) = 0$, $x \notin A$, ou seja

- $\Phi(x-1,x)\uparrow \vee x \leq 0$, e o programa $\mathcal{P'}$ para com $\Psi-{\mathcal{P'}}(x-1)$.

Só que se eu passo o próprio código de $\mathcal{P'} = p'$ como entrada de $\Psi_{\mathcal{P'}}(p')$:

Se $P_A(p') = 1$, $p' \in A$, ou seja

- $\Phi(p'-1,p')\downarrow \wedge p' > 0$, mas $\mathcal{P'}$ entra em loop com $\Psi-{\mathcal{P'}}(p'-1)$.

Se $P_A(p') = 0$, $p' \notin A$, ou seja

- $\Phi(p'-1,p')\uparrow \vee x \leq 0$, mas $\mathcal{P'}$ para com $\Psi-{\mathcal{P'}}(x-1)$.

Absurdo. Portanto, essa função $\Psi_{\mathcal{P'}}$ não está na lista de programas, e portanto não é recursivo.

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

### Resposta:

Note que $\#(\mathcal{P}) = p \in B$, uma vez que para cada $n \in \mathbb{N}$, é possível definir uma função parcialmente computável $f_n$ computada por $q$ tal que $W_q$ seja finito ($P_B(q) = 0$). Seja ela

$$
f_n(x) =
\left\{
\begin{array}{ll}
0 & \text{se } x \leq n\\
\uparrow & \text{caso contrário}
\end{array}
\right.
$$

E o programa que computa

```
[A] IF X > n GOTO A
```

Logo, $\Phi(x, p)$ está definido para uma quantidade infinita de entradas ($W_p$ é infinito). Por outro lado, dada uma enumeração $p_1, p_2, \ldots$ dos programas de $B$, não é possível determinar se $\Psi_P(x)$ difere de cada um deles em pelos menos uma entrada, uma vez que a saída de $\Psi_P(x)$ não é condicionada pelo retorno do programa de código $x$, como tradicionalmente ocorre nas demonstrações por diagonalização.