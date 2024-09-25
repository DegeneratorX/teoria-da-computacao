## Questão 3 - 2018.1.1

Determine qual a linguagem gerada pela gramática irrestrita $\Gamma = (V, \Sigma, R, S)$ abaixo, em que $V = \{S, A, L, R, X, Y, Z\}$, $\Sigma = \{a\}$, e

$$
R = \begin{Bmatrix}
S \rightarrow LAYR && ZA \rightarrow aAZ \\
Za \rightarrow aZ && ZR \rightarrow AAYR \\
aY \rightarrow Ya && AY \rightarrow YA \\
LY \rightarrow LZ\ && YR \rightarrow X \\
aX \rightarrow Xa && AX \rightarrow Xa \\
LX \rightarrow \epsilon & 
\end{Bmatrix}
$$

Justifique a sua resposta (respostas sem justificativas serão sumariamente ignoradas!).

## Questão 4 - 2018.1.1

Encontre uma gramática que gere a linguagem

$$L = \{www \mid w \in \{a, b\}^*\}$$

## Questão 3 - 2019.1.1

Suponha que $G_1 = (V_1, \Sigma, S_1, \delta_1)$ e $G_2 = (V_2, \Sigma, S_2, \delta_2)$ são gramáticas irrestritas gerando $L_1$ e $L_2$, respectivamente. Usando $G_1$ e $G_2$, defina uma Gramática Irrestrita $G = (V, \Sigma, S, \delta)$ que gere $L_1 L_2$.

## Questão 4 - 2019.1.1 (Fácil)

Encontre uma Gramática Irrestrita que gere a linguagem

$$L = \{a^m b^m a^n b^n \mid 0 \leq m \leq n\}$$

## Questão 5 - 2020.1.AF

Encontre uma gramática irrestrita que aceite a linguagem

$$\{a^n b^n a^n b^n \mid n \ge 0\}$$

## Questão 5 - 2021.1.1 e Questão 5 - 2023.1.1

Dado que a Gramática Irrestrita:

- $S \rightarrow LaR$
- $L \rightarrow LD$
- $Da \rightarrow aaD$
- $DR \rightarrow R$
- $L \rightarrow \epsilon$
- $R \rightarrow \epsilon$

gera a linguagem $\{a^{2^n} \mid n \ge 0\}$, que mudanças você poderia fazer para obter uma gramática que gere a linguagem

$$L = \{a^{2^n + n} \mid n \ge 0\}$$

Nesta questão, além da Gramática, explique a sua intuição.

Observação: $a^{2^n + n}$ quer dizer uma sequência de $2^n + n$ $a$'s. Exemplo: $a$, $aaa$, $aaaaaa$ e $a^{11}$ são exemplos de palavras que estão em $L$.

## Questão 5 - 2023.1.1

Encontre uma Gramática Irrestrita que gera a linguagem

$$L = \{a^{2^n + n} \mid n \ge 0\}$$

Nesta questão, além da Gramática, explique a sua intuição.

Observação: $a^{2^n} + n$ quer dizer uma sequência de $2^n + n$ $a$'s. Exemplo: $a$, $aaa$, $a^6$ e $a^11$ são exemplos de palavras que estão em $L$.

## Questão 5 - 2023.1.AF

Encontre uma gramática irrestrita que gere a linguagem

$$\{w \in \{a,b,c\}* \mid n_a(w) < n_b(w) < 2n_c(w)\}$$