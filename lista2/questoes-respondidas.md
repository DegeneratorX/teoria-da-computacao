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

Por absurdo, suponha $A$ recursivo.

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

## Questão 4 - 2023.1.1

Utilizando o método da redução, mostre que o conjunto

$$A = \{x \in \mathbb{N} \mid \Phi(1,x) \ge 5\}$$

não é recursivo. Para tal, você vai mostrar que $K \leq_m A$, em que $K = \{x \in \mathbb{N} \mid \Phi(x,x)\downarrow\}$.

### Resposta:

Tento reduzir $K \leq_m A$.

Baseado na definição,

$$x \in K \iff f(x) \in A$$

para alguma função computável.

**Etapa do "Se e somente se"**

Faremos de trás para frente a operação de se e somente se.

$f(x_2) \in A \iff \Phi(1, f(x_2)) \ge 5 \iff \Phi(1, S_1^1(x_2, p)) \ge 5 \iff \Phi(1, x_2, p) \ge 5 \iff \forall x_1 \Phi(x_1, x_2, p)\downarrow \iff \Psi_P(x_1, x_2)\downarrow \text{ e } \Psi_P(x_1, x_2) \ge 5 \iff \Phi(x_2, x_2)\downarrow \iff x_2 \in K$

Para que $\Psi_P(x_1, x_2)\downarrow \text{ e } \Psi_P(x_1, x_2) \ge 5 \iff \Phi(x_2, x_2)\downarrow$ faça sentido, eu preciso construir um programa que mostre que isso é verdade.

Seja $\mathcal{P}$ o programa

```
     Z ← Phi(X2,X2)
     Y ← Y + 5
```

Como $K \leq_m A$, temos que $A$ não é recursivo.

## Questão 5 - 2023.1.2

Utilizando o método da redução, mostre que o conjunto

$$C = \{x \in \mathbb{N} \mid W_x \text{ NÃO é um conjunto recursivo}\}$$

não é recursivo. Para tal, você vai mostrar que $K \leq_m C$, em que $K = \{x \in \mathbb{N} \mid \Phi(x,x)\downarrow\}$.

Dica: nesta questão, assuma que $k \in \mathbb{N}$ é um número natural tal que $W_k$ não é um conjunto recursivo.

### Resposta:

Definiremos uma função de conversão $\psi_{\mathcal{P}}(x_1,x_2)$ de modo que, ao fixarmos a entrada $x_2$, o programa $\mathcal{P}$ apresente a propriedade de $C$ se e somente se $x_2 \in K$.

Seja $\mathcal{P}$ o seguinte programa de código $p$:

```
     Z ← Phi(X_2,X_2)
     Z ← Phi(X_1,X_1)
```

**Etapa do "Se e somente se"**

Temos, pelo teorema do parâemtro e por $p$ ser constante, que:

$$\psi_{\mathcal{P}}(x_1,x_2) = \Phi(x_1,x_2,p)=\Phi(x_1,S^1_1(x_2,p))=\Phi(x_1,f(x_2))$$

Logo:

- $x_2 \in K \iff \Phi(x_1, f(x_2))\downarrow \iff x_1 \in K \iff W_{f(x_2)} = K \text{ (não recursivo) } \iff f(x_2) \in C$

- $x_2 \notin K \iff \Phi(x_1, f(x_2))\uparrow \forall x_1 \in \mathbb{N} \iff W_{f(x_2)} = \emptyset \text{ (recursivo, faça } P_{\emptyset} = 0 \text{) } \iff f(x_2) \notin C$

Ou seja, $x_2 \in K \iff f(x_2) \in C$. Logo, $K \leq_m C$ e $K$ não é recursivo, logo $C$ não é recursivo.

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