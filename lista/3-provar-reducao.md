## Questão 1 - 2016.1.1

Seja

$$FIN = \{x \in \mathbb{N} \mid W_x \text{ é finito}\}$$

Mostre que $\overline{K} \leq_m FIN$, em que $\overline{K} = \{x \in \mathbb{N} \mid \Phi(x,x)\uparrow\}$.

## Questão 4 - 2021.1.1

Utilizando o método da redução, mostre que o conjunto

$$A = \{x \in \mathbb{N} \mid \Phi(x,x)\downarrow \wedge \Phi(x,x) > x\}$$

não é recursivo.

## Questão 5 - 2021.1.2

Utilizando o método da redução, mostre que o conjunto

$$A = \{x \in \mathbb{N} \mid \exists y(\Phi(y,x)\downarrow)\}$$

não é recursivo.

## Questão 4 - 2023.1.1

Utilizando o método da redução, mostre que o conjunto

$$A = \{x \in \mathbb{N} \mid \Phi(1,x) \ge 5\}$$

não é recursivo. Para tal, você vai mostrar que $K \leq_m A$, em que $K = \{x \in \mathbb{N} \mid \Phi(x,x)\downarrow\}$.

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

Temos, pelo teorema do parâemtro e por $p$ ser constente, que:

$$\psi_{\mathcal{P}}(x_1,x_2) = \Phi(x_1,x_2,p)=\Phi(x_1,S^1_1(x_2,p))=\Phi(x_1,f(x_2))$$

Logo:

- $x_2 \in K \iff \Phi(x_1, f(x_2))\downarrow \iff x_1 \in K \iff W_{f(x_2)} = K \text{ (não recursivo) } \iff f(x_2) \in C$

- $x_2 \notin K \iff \Phi(x_1, f(x_2))\uparrow \forall x_1 \in \mathbb{N} \iff W_{f(x_2)} = \emptyset \text{ (recursivo, faça } P_{\emptyset} = 0 \text{) } \iff f(x_2) \notin C$

Ou seja, $x_2 \in K \iff f(x_2) \in C$. Logo, $K \leq_m C$ e $K$ não é recursivo, logo $C$ não é recursivo.