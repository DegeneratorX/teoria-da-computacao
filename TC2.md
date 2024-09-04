## Definição 2.1: Função de Pareamento

$$z = \underbrace{\left< x, y \right>}_{\mathit{PR}} = \underbrace{2^x (2y + 1) ∸ 1}_{\mathit{PR}}$$

É uma função que retorna um código baseado na fórmula acima. A função é bijetiva, e qualquer alteração de $x$ ou $y$, o retorno é diferente.

A operação $∸$ significa a subtração natural, e é definida por:

$$
a∸b = \begin{cases} 
a-b & \text{, se } a \ge b \\
0 & \text{, se a < b} 
\end{cases}
$$

Para extrair o lado **esquerdo** e **direito** da função de pareamento, usamos as funções left $l(z)$ e right $r(z)$, que recebe o número codificado $z$ e retorna $x$, que é o primeiro número ou $y$, que é o segundo número, respectivamente:

$l(z) = \min_{x \leq z}[(\exists y)_{\leq z}(z = \left< x, y \right>)]$

$r(z) = \min_{y \leq z}[(\exists x)_{\leq z}(z = \left< x, y \right>)]$

Repare que tudo isso são funções primitivas recursivas.

## Definição 2.2: Número de Gödel

É uma função primitiva recursiva definida como

$$[a_1,...,a_n] = \prod_{i=1}^{n}p_i^{a_i}$$

onde $p$ é um primo, e $p_i$ é o i-ésimo primo.

**EXEMPLO**

$[3,1,5,4,6] = 2^3 \cdot 3^1 \cdot 5^5 \cdot 7^4 \cdot 11^6$

Essa função me garante listar não só um par, mas $n$ elementos e uma codificação mais extensa, porém ainda bijetiva, dado que toda fatoração é única.

Pra achar o i-ésimo elemento específico na lista, uso essa função primitiva recursiva, que recebe como argumento o Número de Gödel:

$$(x)_i = \min_{t \leq x}\neg(P_i^{t+1}|x)$$

Onde $x$ é o número final a ser decodificado, $i$ é o índice do elemento da lista que desejo obter, e $P_i$ é o i-ésimo primo correspondente ao índice da lista.

Isso aqui basicamente tá fatorando na força bruta o número

### Comprimento do Número de Gödel

É uma função primitiva recursiva que retorna o tamanho da lista ao receber o Número de Gödel.

$$Lt(x) = \min_{i \leq x}[(x)_i \neq 0 \wedge (\forall j)_{\leq x}(j \leq i \vee (x)_j = 0)]$$

## Codificando um programa - introdução

Lembrar das instruções básicas da linguagem $\mathscr{L}$:

**Variáveis**

A linguagem $\mathscr{L}$ possui as seguintes variáveis:

- Variáveis de entrada: $X_1$, $X_2$, $X_3$, …

- Variável de saída: $Y$

- Variáveis auxiliares: $Z_1$, $Z_2$, $Z_3$, …

Por convenção, assume-se que o valor inicial das variáveis auxiliares e da variável de saída é 0.

**Rótulos**

A linguagem $\mathscr{L}$ possui rótulos:

$A_1$, $B_1$, $C_1$, $E_1$,...

**Instruções e Declarações**

As únicas declarações que podem ser feitas em $\mathscr{L}$ são:

- $V \leftarrow V + 1$ // Incrementa 1 ao valor de V

- $V \leftarrow V - 1$ //Decrementa 1 ao valor de V

- $V \leftarrow V$ // O valor de V fica inalterado

- IF $V \neq 0$ GOTO $L$ // Se o valor de $V \neq 0$, executa-se a instrução com rótulo $L$; caso contrário, executa-se a próxima instrução na lista. Se o rótulo não existe, então encerra o programa/macro

onde $V$ é uma variável e $L$ é um label/rótulo.

Se eu quero codificar uma linha, a linha equivale a $\left< a, \left< b, c\right>\right>$, onde
- $a$ é o código de um label;
- $b$ é o código dos 4 tipos de instrução
- $c$ é o código da variável subtraindo 1.

**Códigos de um label ($a$)**

- Sem label possui código 0
- $A_1$ possui código 1
- $B_1$ possui código 2
- $C_1$ possui código 3
- $D_1$ possui código 4
- $E_1$ possui código 5
- $A_2$ possui código 6
- $B_2$ possui código 7
- $C_2$ possui código 8
- $D_2$ possui código 9
- $E_2$ possui código 10

Exemplo: o código de C1 é 3. Ou seja, $\#(C1) = 3$. O código $\#(E3) = 15$.

**Código da instrução ($b$)**

- $V \leftarrow V$ possui código $0$
- $V \leftarrow V+1$ possui código $1$
- $V \leftarrow V-1$ possui código $2$
- IF $V \neq 0$ GOTO $L$ possui código $2 + \#(L)$

Exemplo: $\#(\text{IF } V \neq 0 \text{ GOTO } D2) = 11$

**Código de uma variável ($c$)**

- $Y$ é a variável de saída do programa $\mathscr{L}$, e possui código 1
- $X_1$ possui código 2
- $Z_1$ possui código 3
- $X_2$ possui código 4
- $Z_2$ possui código 5
- $X_3$ possui código 6
- $Z_3$ possui código 7
- $X_4$ possui código 8
- $Z_4$ possui código 9

Os $X_i$ são as variáveis de entrada e $Z_i$ são variáveis auxiliares do programa. Eu alterno pra incluir todas as variáveis sem falta. Se eu sequencio $X_i$ sem alternar com $Z_i$ até o infinito, eu nunca vou chegar em $Z$.

Exemplo: $\#(X_{10}) = 20$. Pra eu achar o $c$, eu subtraio $-1$. Ou seja, $c = \#(X_{10})∸1 = 19$. Outro exemplo, $c = \#(Z_{6})∸1 = 12$. E outro exemplo, $c = \#(Y)∸1 = 0$.

Perceba também que $\#(X_i) = 2i$, e $\#(Z_i) = 2i + 1$.

### Codificação do programa completo

Pra codificar um programa P, uso Número de Gödel com função de pareamento. Assim:

$$\#(P) = [\#(I_1) \text{ } \#(I_2) \text{ } \#(I_3) \ldots \#(I_n)] ∸ 1$$

, onde $I_1,\ldots ,I_n$ são as instruções do programa, e $\#(I_1),\ldots,\#(I_n)$ são os respectivos códigos das instruções, no formato $\left< a, \left< b, c\right>\right>$.

**Exemplo:** como codifico

```
[A]  X ← X + 1
     IF X ≠ 0 GOTO A
```

Perceba que

- Com $a = 1$, $b = 1$ e $c = 2 ∸ 1 = 1$, tem-se que $\#(I_1) = \#([A]  X \leftarrow X + 1) = \left< 1, \left< 1, 1\right>\right> = \left<1, 2^1(2 \cdot 1 + 1) ∸ 1 \right> = \left<1,5\right> = 2^1(2\cdot 5 + 1)∸ 1 = 21$
- Com $a = 0$, $b = 3$ e $c = 2 ∸ 1 = 1$, tem-se que $\#(I_2) = \#(\text{IF } X \neq 0 \text{ GOTO } A) = \left<0,\left<3, 1\right>\right> = \left<0, 23\right> = 46$

Portanto, $\#(P) = [\#(I_1) \text{ } \#(I_2)] ∸ 1 = [21 \text{ } 46] ∸ 1 = 2^{21} \cdot 3^{46} ∸ 1$.

**Exemplo:** como eu decodifico 199?

Faço a operação inversa, veja que a equação:

$\#(P) = 199 = [\ldots] ∸ 1$, eu passo o $∸1$ pro outro lado e fica positivo, assim descubro o Número de Gödel isolado: $[\ldots] = 200$.

Agora eu fatoro o 200 e descubro $2^3 \cdot 3^0 \cdot 5^2 = [3 \text{ } 0 \text{ } 2]$. Agora eu faço o passo a passo de trás pra frente, ou seja, de fora pra dentro: 

- $3 = \left<2, 0\right> = \left<2,\left<0,0\right>\right>$.

- $0 = \left<0,\left<0,0\right>\right>$

- $2 = \left<0, 1\right> = \left<0,\left<1,0\right>\right>$

Isso equivale ao programa

```
[B]  Y ← Y
     Y ← Y
     Y ← Y + 1
```

**Exemplo:** número 21 é um código derivado de uma instrução. Como eu recupero a instrução?

Poderia aplicar as funções $l(21)$ e $r(21)$:

$l(21) = \min_{x \leq 21}[(\exists y)_{\leq 21}(z = \left< x, y \right>)]$

$r(21) = \min_{y \leq 21}[(\exists x)_{\leq 21}(21 = \left< x, y \right>)]$

Porém, isso é força bruta. Poderia implementar na linguagem $\mathscr{L}$ para automatizar o processo. Mas a ideia é manualmente fazer. Por isso posso também fatorar:

- $21 = \left<x,\left<x',y'\right>\right> = 2^x(2y + 1)∸1$. Se eu somar $+1$, eu tenho o componente $2^x(2y + 1) = 22$. Se eu fatorar 22, obtenho $2 \cdot 11$. Portanto, eu sei que $2^1 \cdot (2\cdot 5 + 1) = 22$. Ou seja, agora sei quem é o $y$ e $x$: $\left<1,5\right>$. Porém, $5 = \left<x', y'\right>$. Então faço o mesmo processo, somo $+1$, fatoro (ou seja, fatoro 6), e descubro que $2^1(2\cdot 1 + 1) = 6$. Com isso, tenho que $x' = 1$ e $y' = 1$. Portanto, a instrução possui código $\left<1,\left<1,1\right>\right>$, que equivale a instrução $[A] X \leftarrow X + 1$.

## Definição 2.3: Problema da Parada

A função do problema da parada é um predicado, ou seja, uma função total que é definida como

$$
HALT(x,y) = \begin{cases} 
1 & \text{, se o programa de código } y \text{ com entrada } x \text{ para} \\
0 & \text{, caso contrário.} 
\end{cases}
$$

Pra provar que $HALT()$ não é computável, assumimos que é para chegar em um absurdo. Assumindo que seja, tem um programa, e pode ser usado como macro por outro programa. Vou chamar esse programa de $P$:

```
[A]  IF HALT(x, x) GOTO A
```

Pouco me importa o segundo parâmetro. Se o código do programa que quero passar em $HALT$ é $\#(P) = p$, ou seja, ele mesmo, eu posso passar $P$ como segundo argumento, mas poderia ser qualquer número:

```
[A]  IF HALT(p, p) GOTO A
```

Observe que se $HALT(p, p) = 1$, pela definição de $HALT$, o programa $p$ para com entrada $p$. Mas no programa $P$ acima que construí, o programa $P$ entra em loop com entrada $p$. Já se $HALT(p, p) = 0$, pela definição de $HALT$, o programa $p$ entra em loop com entrada $p$, mas no programa $P$ acima, ele para com entrada $p$. Absurdo, afinal, a definição diz uma coisa, mas o programa faz outra. Se eu chamar por recursão o próprio predicado, eu acabo tendo uma contradição. Ou seja, não há como construir um programa que compute $HALT$. A ideia segue o mesmo princípio do Teorema da Incompletude de Gödel.

## Definição 2.4: Programa Universal

O programa universal é definido como

$$\Phi^{(n)}(x_1, x_2, \ldots, x_n, x_{n+1}) = \psi_P^{(n)}(x_1,x_2,\ldots ,x_n)$$

, onde $x_{n+1} = \#(P)$, $(n)$ é uma notação indicando o número de argumentos usados no programa $\psi$.

O programa universal é o que o computador faz. O computador é a materialização física do que a função universal faz.

### Teorema 2.1: a função $\Phi^{(n)}$ é parcialmente computável, com $n > 0$.

**Prova:**

Se é Parcialmente Computável, tem um programa que computa. O programa vai ser demonstrado depois.

## Definição 2.5: codificação de estados

Posso usar Número de Gödel pra codificar estados da seguinte forma:

$$[Y \text{ } X_1 \text{ } Z_1 \text{ } X_2 \text{ } Z_2 \text{ } X_3 \text{ } Z_3 \text{ } \ldots]$$

**Exemplo:** O programa tá no estado inicial e possui entradas $X_1 = 20$, $X_2 = 3$ e $X_3 = 65$. Qual o código correspondente a esse estado?

- O código é o $[0 \text{ } 20 \text{ } 0 \text{ } 3 \text{ } 0 \text{ } 65] = 3^{20} \cdot 7^3 \cdot 13^{65}$.

Perceba que no estado inicial, $Y$ e os auxiliares $Z$ iniciam com 0, que são as posições ímpares.

## Instruções do Programa Universal

Sabendo que

$$\Phi^{(n)}(x_1, x_2, \ldots, x_n, x_{n+1}) = \psi_P^{(n)}(x_1,x_2,\ldots ,x_n)$$

O programa universal recebe as mesmas variáveis de entrada do programa $P$, e retorna a mesma coisa que o programa $P$ retorna.

$
\begin{array}{ll}
\ & Z \leftarrow X_{n+1} + 1 \\
\ & S \leftarrow \prod_{i=1}^{n}(p_{2i})^{X_i}\\
\ & K \leftarrow 1 \\
\text{[} C \text{]}\ & \mathit{IF }\ K = Lt(Z) + 1 \vee K = 0 \text{ }\mathit{ GOTO }\ F\\
\ & U \leftarrow r((Z)_k) \\
\ & P \leftarrow p_{r(U)+1} \\
\ & \mathit{IF }\ l(U) = 0 \text{ }\mathit{GOTO }\ N\\
\ & \mathit{IF }\ l(U) = 1 \text{ }\mathit{GOTO }\ A\\
\ & \mathit{IF }\ ¬(P | S) \text{ }\mathit{GOTO }\ N\\
\ & \mathit{IF }\ l(U) = 2 \text{ }\mathit{GOTO }\ M\\
\ & K \leftarrow \min_{i \leq \mathit{Lt}(Z)} \left[ l((Z)_i) + 2 = l(U) \right]\\
\ & \mathit{GOTO }\ C \\
\text{[} M \text{]} & S \leftarrow \left\lfloor S / P \right\rfloor\\
\ & \mathit{GOTO }\ N \\
\text{[} A \text{]} & S \leftarrow S \cdot P \\
\text{[} N \text{]}
 & K \leftarrow K + 1 \\
\ & \mathit{GOTO }\ C \\
\text{[} F \text{]} & Y \leftarrow (S)_1 \\
\end{array}
$

**Explicação breve:** 

- $Z \leftarrow X_{n+1} + 1$: Z recebe o programa em Número de Gödel $[pos_1 \text{ } pos_2 \text{ } \ldots]$. A soma $+1$ é para compensar a subtração natural feita para obter o código $\#(P)$.

- $S \leftarrow \prod_{i=1}^{n}(p_{2i})^{X_i}$: S recebe o estado inicial preparado, com auxiliares $Z$ e output $Y$ zerados.

- $K \leftarrow 1$: K é um pivô que mantém o track da linha do programa $P$ lido.

- $\text{[} C \text{]}\ \mathit{IF }\ K = Lt(Z) + 1 \vee K = 0 \text{ }\mathit{ GOTO }\ F$: Verifica se o programa deve parar. É o início do passo a passo da computação.

- $U \leftarrow r((Z)_k)$: $U$ armazena a função de pareamento $\left<b, c\right>$ da linha $K$ atual.

- $P \leftarrow p_{r(U)+1}$: $r(U)$ armazena o $c$, já o $P$ armazena a variável a ser trabalhada da linha atual.

- $\mathit{IF }\ l(U) = 0 \text{ }\mathit{GOTO }\ N$: Verifica o $b = 0$, se for, é a instrução $V \leftarrow V$, se for, manda pra $N$, que é a operação de ir para a próxima linha. Não muda nada.

- $\mathit{IF }\ l(U) = 1 \text{ }\mathit{GOTO }\ A$: Verifica o $b = 1$, se for, faz um incremento.

- $\mathit{IF }\ ¬(P | S) \text{ }\mathit{GOTO }\ N$: Verifica se V = 0 após os dois IFs anteriores não serem verdadeiros. Se $P$ não divide $S$, significa que o Número de Gödel $S$ que armazena o estado não possui um primo com expoente diferente de 0, ou seja, não é um fator, e se não é, S não é divisível por P. Portanto, $V = 0$ e não é possível decrementar ou atender ao condicional IF, ou seja, pula para a próxima linha através da label $N$.

- $\mathit{IF }\ l(U) = 2 \text{ }\mathit{GOTO }\ M$ e $\text{[} M \text{]} S \leftarrow \left\lfloor S / P \right\rfloor$: Verifica o $b$ para fazer o decremento.

- $K \leftarrow \min_{i \leq \mathit{Lt}(Z)} \left[ l((Z)_i) + 2 = l(U) \right]$: Se chegou até aqui, então a instrução atual é um condicional IF. Verifico o label pra ser saltado. E se chegou aqui, $V \neq 0$ com certeza.

## Definição 2.6: Função STEP - Introdução

A função $STP$, conhecida coo  a função STEP, é definida como:

$$
STP^{(n)}(x_1,\ldots,x_n, y, i) = \begin{cases} 
1 & \text{, se o programa de código } y \text{ com entradas } x_1,\ldots,x_n \text{ para em até } i \text{ passos.} \\
0 & \text{, caso contrário.} 
\end{cases}
$$

Esse predicado é primitivo recursivo, portanto computável. A prova é extensa. Farei algumas definições antes.

### Codificando um snapshot

Snapshot é um par $(i, \sigma)$, onde $i$ é a linha e o $\sigma$ é o estado do programa. Posso transformar esse par numa função de pareamento, onde

$$x = \left<i, \sigma\right>$$

### Capturando valores do programa através de funções primitivas recursivas

Seja $y$ o código de um programa.

Defino algumas funções:

- $LABEL(i, y) = l((y+1)_i)$: extrai o label da i-ésima linha de $y$, que corresponde ao $a$ da função de pareamento.

- $VAR(i, y) = r(r(y+1)_i) + 1$: extrai a variável da i-ésima linha de $y$, que corresponde ao $c + 1$ da função de pareamento.

- $INSTR(i, y) = l(r(y+1)_i)$: extrai o tipo de instrução da i-ésima linha de $y$, que corresponde ao $b$ da função de pareamento.

- $LABELIF(i, y) = l(r(y+1)_i)∸2$: extrai o label $L$ da instrução $\text{IF } V \neq 0 \text{ GOTO } L$ da i-ésima linha de $y$. Retorna 0 se não tiver o IF.

Para verificar se é possível fazer operações, e sendo $x$ o código do snapshot, defino os predicados:

$$
INCR(x, y) = \begin{cases} 
1 & \text{, se } INSTR(l(x), y) = 1 \\
0 & \text{, caso contrário.} 
\end{cases}
$$

Retorno 1 se pode incrementar.

$$
DECR(x, y) = \begin{cases} 
1 & \text{, se } [INSTR(l(x), y) = 2] \wedge [p_{var(l(x),y)}|r(x)] \\
0 & \text{, caso contrário.} 
\end{cases}
$$

Retorno 1 se pode decrementar.

$$
SKIP(x, y) = \begin{cases} 
1 & \text{, se } [[INSTR(l(x), y) = 0] \wedge [l(x) \leq Lt(y+1)]] \vee [[INSTR(l(x), y) \geq 2]\wedge [\neg(p_{var(l(x),y)}|r(x))]] \\
0 & \text{, caso contrário.} 
\end{cases}
$$

Retorno 1 se é para ignorar a linha.

$$
BRANCH(x, y) = \begin{cases} 
1 & \text{, se } [INSTR(l(x), y) > 2] \wedge [p_{VAR(l(x), y)}|r(x)] \wedge [(\exists i)_{\leq Lt(y+1)} LABEL(i, y) = LABELIF(l(x), y)] \\
0 & \text{, caso contrário.} 
\end{cases}
$$

Retorno 1 se dá pra saltar para alguma label. Se a label não existir, retorna 0.

### Funções de execução

**Função sucessor**

$$
SUCC(x, y) = \begin{cases} 
\left<l(x) + 1, r(x)\right> & \text{, se } SKIP(x, y) \\
\left<l(x) + 1, r(x) \cdot p_{VAR(l(x), y)}\right> & \text{, se } INCR(x, y) \\
\left<l(x) + 1, \left\lfloor r(x) \div p_{VAR(l(x), y)}\right\lfloor \right> & \text{, se } DECR(x, y) \\
\left<\min_{i \leq Lt(y+1)}[LABEL(i, y) = LABELIF(l(x), y), r(x)]\right> & \text{, se } BRANCH(x, y) \\
\left<Lt(y+1) + 1, r(x)\right>  & \text{, caso contrário.} 
\end{cases}
$$

Essa é a função principal da computação. Ou seja, a materialização do que seria o passo a passo da computação.

**Função de configuração do snapshot inicial**

A computação é impossível sem um estado inicial. Portanto:

$$INITSNAP^{(n)}(x_1,...,x_n) = \left<1, \prod_{i = 1}^{n}(p_{2i})^{x_i}\right>$$

**Função de snapshot atual**

Agora que temos o snapshot inicial, podemos fazer o passo a passo atualizando o snapshot atual:

$$SNAP^{(n)}(x_1,...,x_n, y, 0) = INITSNAP^{(n)}(x_1,...,x_n)$$

$$SNAP^{(n)}(x_1,...,x_n, y, i+1) = SUCC(SNAP^{(n)}(x_1,...,x_n, y, i), y)$$

**Predicado se o programa terminou**

$$
TERM(x, y) = \begin{cases} 
1 & \text{, se } l(x) > Lt(y + 1) \\
0 & \text{, caso contrário.} 
\end{cases}
$$

## Definição 2.6: Função STEP - Final

Agora podemos formular a função STEP, que retorna 1 se o programa parou com $i$ passos, ou 0 caso contrário. Ele analisa frame por frame cada passo da computação através do snapshot e verifica se a linha atual do snapshot após $i$ passos é $Lt(y+1)+1$, ou seja, depois da contagem de linhas do programa.

$$
STP(x_1,...,x_n,y,i) = \begin{cases} 
1 & \text{, se } TERM(SNAP(x_1,...,x_n,y,i),y) = 1 \\
0 & \text{, caso contrário.} 
\end{cases}
$$

Todas as funções mostradas aqui são primitivas recursivas.

## Definição 3.1: Conjunto Recursivamente Enumerável

O conjunto $B \subseteq \mathbb{N}$ é r.e. se há uma função parcialmente computável $g(x)$ tal que

$$B = \{ x \in \mathbb{N} \mid g(x) \downarrow\}$$

- Se $\mathcal P$ é o programa que computa $g$, então $B$ é o conjunto com todas as entradas para as quais $\mathcal P$ para.
- $\mathcal P$ proporciona um programa para determinar se um elemento pertence a $B$.
- Procedimentos de semidecisão: determinam o que pertence a $B$, mas entram em loop infinito para elementos que não estejam em $B$.

### Teorema 3.1: Se $B$ e $C$ são r.e., então $B \cup C$ e $B \cap C$ também são r.e.

**Prova:**

Por definição, se $B$ e $C$ são r.e.,

$$B = \{ x \in \mathbb{N} \mid g(x) \downarrow\}$$

$$C = \{ x \in \mathbb{N} \mid h(x) \downarrow\}$$

em que $g$ e $h$ são parcialmente computáveis.

Seja $f(x)$ a função computada pelo programa

$$
\begin{array}{l}
Y \leftarrow g(X)\\
Y \leftarrow h(X)\\
\end{array}
$$

Agora para provar que $B \cap C$ são r.e., veja que $f(x)$ para se e somente se $g(x)$ e $h(x)$ estão definidos. Ou seja,

$$B \cap C = \{ x \in \mathbb{N} \mid f(x) \downarrow\}$$

Interseção provada que é r.e., mas agora para provar que $B \cap C$ é r.e., façamos o seguinte:

- Sejam $g$ computado por um programa $\mathcal P$ e $h$ por $\mathcal Q$.
- Se tem programa, tem código. Então posso codificar de forma que $\#(\mathcal P) = p$ e $\#(\mathcal Q) = q$.

Seja $k(x)$ a função computada por

```
[A]  IF STP(X, p, T) GOTO E
     IF STP(X, q, T) GOTO E
     T ← T + 1
     GOTO A
```

Nesse caso T é o número de passos. Ou seja, usa o predicado do STEP, se parar em T passos, o programa retorna 1, se não, retorna 0. Eu faço uma verificação paralela. Veja que não é total, ou seja, o elemento pode não estar em $B$ ou $C$, dando margem para um loop infinito.

Veja que $k(x)$ para se e somente se $g(x)$ ou $h(x)$ estão definidos.

Ou seja, $B \cup C = \{ x \in \mathbb{N} \mid k(x) \downarrow\}$. Portanto, $B \cup C$ é r.e.

## Definição 3.2: Associando predicados a conjuntos

Sejam $P$ um predicado, $S$ um conjunto e $R \subseteq S$. Diz-se que $P$ é a função característica de $R$ se, e somente se

$$R = \{ a \in S \mid P(a) \}$$

e que $P$ é definido a partir de $S$ sse existe $R \subseteq S$ tal que

$$
P(x) = 
\left\{
\begin{array}{ll}
1 & \text{se } x \in R\\
0 & \text{caso contrário}
\end{array}
\right.
$$ 

**Exemplo:**

O predicado $HALT(x,y)$ é a função característica do conjunto 

$$\{ (x, y) \in \mathbb{N}^2 \mid  HALT(x,y) \}$$

**OBSERVAÇÃO**

- $B$ é um conjunto computável se $P(x_1,\ldots,x_m)$ é computável.

- $B$ é um conjunto primitivo recursivo se $P(x_1, \ldots, x_m)$ é primitivo recursivo.

## Definição 3.3: Conjunto Recursivo (Computável)

Um conjunto $C \subseteq \mathbb{N}$ é recursivo se a função característica $P_C$ é computável.

Ou seja, a função característica é exclusiva aos conjuntos recursivos, e $P_C(x)$ é definida como

$$
P_C(x) = \begin{cases} 
1 & \text{ se } x \in C \\
0 & \text{ se } x \notin C
\end{cases}
$$

### Teorema 3.2: Se $B$ é um conjunto recursivo (computável), então $B$ é recursivamente enumerável

**Prova:**

Considere o programa $\mathcal P$ 

```
[A]  IF ¬(X in B) GOTO A
```

Como $B$ é recursivo, o predicado $x \in B$ é computável. Agora suponha que $\mathcal P$ compute a função $h(x)$. Consequentemente 

$$B = \{ x \in \mathbb{N} \mid h(x) \downarrow \}$$

Ou seja, $h(x)$ para se $x \in B$, e entra em loop se $x \notin B$.

### Teorema 3.3: o conjunto $B$ é recursivo se e somente se ambos $B$ e $\overline{B}$ forem r.e.

**Prova ida:**

O seguinte teorema pode ser usado para provar que $\overline{B}$ é um conjunto recursivo: sejam os conjuntos $B$ e $D$ que pertençam a uma classe $C$ Primitiva Recursivamente Fechada. Então $B \cup C$, $B \cap D$ e $\overline{B}$ também pertencem a $C$.

Sabendo disso, dado que $B$ e $\overline{B}$ são recursivos, pelo teorema 3.2 anterior, $B$ e $\overline{B}$ são recursivamente enumeráveis.

**Prova volta:**

Por definição, se $B$ e $\overline{B}$ são recursivamente enumeráveis, então

$$B = \{ x \in \mathbb{N} \mid g(x) \downarrow\}\\$$
$$\overline{B} = \{ x \in \mathbb{N} \mid h(x) \downarrow\}$$

Sejam $g$ computado por um programa $\mathcal P$ e $h$ por um programa $\mathcal Q$. E sejam $\#(\mathcal P) = p$ e $\#(\mathcal Q) = q$ as codificações desses programas.

Posso mostrar que existe um programa que computa o conjunto $B$.

```
[A]  IF STP(X, p, T) GOTO C
     IF STP(X, q, T) GOTO E
     T ← T + 1
     GOTO A
[C]  Y ← 1
```

Esse programa é suficiente para provar a volta. Veja que STEP é um predicado total, e P.R., ou seja, computável. Ele sempre irá parar e retornar algo. Portanto, se o elemento está em $B$, retorna 1, mas se tiver em $\overline{B}$, retorna 0.

## Definição 3.4: O conjunto $W_n$

Definimos o conjunto $W_n$ da seguinte forma:

$$W_n = \{ x \in \mathbb{N} \mid \Phi(x, n) \downarrow\}$$

Onde

- $\Phi$ é a função universal
- $n$ é o código do programa
- $x$ é uma entrada qualquer

Basicamente essa definição diz que $W_n$ é um conjunto com as possíveis entradas $x$ que fazem o programa universal com código $n$ parar.


**Outras definições**

Aqui vou definir algumas coisas a mais para ajudar nos próximos teoremas.

- $W_0$, $W_1$, $W_2$, $\ldots$ é uma enumeração de todos os conjuntos r.e.
- $n \in W_n$ se e somente se $\Phi(n, n) \downarrow$ se e somente se $HALT(n, n)$.
- $K = \{ n \in \mathbb{N} \mid n \in W_n \} = \{ n \in \mathbb{N} \mid \Phi(n.n) \downarrow \}$

### Teorema 3.4: Teorema da Enumeração - Um conjunto $B$ é r.e. se e somente se há um $n$ para o qual $B = W_n$.

**Prova:**

Veja que $B$ é um conjunto r.e. se e somente se $$B = \{ x \in \mathbb{N} \mid g(x) \downarrow\}$, ou seja, $g(x)$ para.

Seja $n = \#(P)$ o código do programa que computa $g(x)$.

Logo, $B$ é um conjunto recursivamente enumerável se e somente se $B = \{ x \in \mathbb{N} \mid \Phi(x, n) \downarrow\}$

### Teorema 3.5: $K$ é recursivamente enumerável, mas não é recursivo.

**Prova:**

Como $K = \{ n \in \mathbb{N} \mid \Phi(n.n) \downarrow \}$ e $g(n)$ = $\Phi(n, n)$, é parcialmente computável, $K$ é r.e.

Por absurdo, suponha que $\overline{K}$ também seja r.e.

Pelo teorema 3.4 da enumeração, para algum $i$, $\overline{K} = W_i$. Então

$$i \in K \Leftrightarrow i \in W_i \Leftrightarrow i \in \overline{K}$$

Perceba a contradição. $i \in K$ ao mesmo tempo que $i \in \overline{K}$, pertence ao seu complemento.

### Teorema 3.6: seja $B$ r.e. Então há um predicado recursivo $R(x,t)$ tal que $B = \{x \in \mathbb{N} \mid (\exists t)R(x,t)\}$

**Prova:**

Seja $B = W_n$. Isto é, $B = \{x \in \mathbb{N} \mid \Phi(x, n)\downarrow\}$. Então

$$B = \{x \in \mathbb{N} \mid (\exists t)STP(x, n, t)\}$$

### Teorema 3.7: seja um conjunto $S$ r.e. não vazio. Então há uma função primitiva recursiva $f(u)$ tal que $S = \{f(n) \mid n \in \mathbb{N}\} = \{f(0), f(1), f(2), \ldots\}$.

**Prova:**

Pelo teorema 3.6, $S = \{x \mid (\exists t)R(x,t)\}$. Seja $x_0$ algum número qualquer de $S$. Considere a função:

$$
f(u) = \begin{cases} 
l(u) & \text{ se } R(l(u), r(u)) \\
x_0 & \text{ caso contrário. } 
\end{cases}
$$

Pelo teorema da definição por casos, $f$ é primitiva recursiva.

Provando que $f(u) \in S$ para cada $u \in \mathbb{N}$:


- Se $R(l(u), r(u))$ é falso, então $f(u) = x_0 \in S$.
- Se $R(l(u), r(u))$ é verdadeiro, então $(\exists t) R(l(u), t)$ é verdadeiro.
- Com isso, $f(u) = l(u) \in S$.

Provando que se $x \in S$, $R(x, t_0)$ é verdadeiro para algum $t_0$:

- Se $x \in S$, então $R(x, t_0)$ é verdadeiro para algum $t_0$.
- Logo $f(\left< x, t_0 \right>) = l(\left< x, t_0 \right>) = x$.
- Isso quer dizer que $x = f(u)$ para $u = \left< x, t_0 \right> $.

### Teorema 3.8: Sejam $f(x)$ uma função parcialmente computável e $S = \{ f(x) \mid f(x) \downarrow \}$ Então $S$ é r.e.

**Prova:**

Seja

$$
g(x) =
\left\{
\begin{array}{ll}
0 & \text{se } x \in S\\
\uparrow & \text{caso contrário}
\end{array}
\right.
$$

Como $S = \left\{ x \mid g(x)\downarrow \right\}$, é suficiente mostrar que $g(x)$ é parcialmente computável. Mas posso também mostrar um programa $P$ que computa $f$. Se tem programa $P$, posso codificar de forma que $\#(P) = p$.

```
[A]  IF ¬STP(Z,p,T) GOTO B
     V ← f(Z)
     IF V = X GOTO E
[B]  Z ← Z+1
     IF Z <= T GOTO A
     T ← T+1
     Z ← 0
     GOTO A
```

### Teorema 3.9: Suponha que $S \neq \empty$. Então (1) $S$ é r.e., (2) é a imagem de uma função primitiva recursiva, (3) é a imagem de uma função computável e (4) é a imagem de uma função parcialmente computável.

**Prova:**

- Pelo teorema 3.7, (1) implica (2);
- É sabido que (2) implica (3) e obviamente (3) implica (4),
- Pelo teorema 3.8, (4) implica (1).

## Definição 3.5: Diagonalização de Cantor

É um tipo de prova por absurdo para provar que um conjunto **não é recursivo** ou **não é recursivamente enumerável**.

### Exemplo 3.1: seja o conjunto $K$ novamente tal que $K = \{x \in \mathbb{N} \mid \Phi(x,x)\downarrow \}$. Mostre que $K$ não é recursivo.

**PASSO 1:** Seja $\psi_{\mathcal{P}_0} \text{ } \psi_{\mathcal{P}_1} \text{ } \psi_{\mathcal{P}_2} \text{ } \ldots$ a lista de todos os programas existentes, sendo o índice numérico o código dos respectivos programas $\mathcal{P}$. Assumo por absurdo que $K$ é recursivo. Logo

$$
P_K(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \in K\\
0 & \text{se } x \notin K
\end{array}
\right.
$$

é uma função característica de $K$.

**PASSO 2:** Seja $\mathcal{P}'$ o seguinte programa:

```
[A]  IF P_k(X) GOTO A
```

Para mostrar que $\mathcal{P}'$ é diferente de todos da lista, basta eu mostrar que para a mesma entrada, produza resultados diferentes.

**PASSO 3:** Se $\mathcal{P}'$ tem programa, tem código. A ideia é verificar se o código de $\mathcal{P}'$ é igual a qualquer um da lista.

Seja $\#(\mathcal{P}') = p'$.

Testo primeiro para $x = 0$. Se $x = 0$, então $\Phi(0,0)$, ou seja, testo se o segundo argumento, $p'$ é de fato igual a $0$ para esse caso.

```
[A]  IF P_k(0) GOTO A
```

**Para $x = 0$, será que $p' = 0$?**

Veja que $\psi_{\mathcal{P}'}(0)$ pode implicar em dois casos:

- $P_K(0) = 1$ significa que $0 \in K$, ou seja, $\Phi(0,0)\downarrow$, ou seja, $\psi_{P_0}(0)\downarrow$, o que atende perfeitamente a definição de K. Mas, olhando para o programa, $\psi_{P'}(0)\uparrow$.

- $P_K(0) = 0$ significa que $0 \notin K$, ou seja, $\Phi(0,0)\uparrow$, ou seja, $\psi_{P_0}(0)\uparrow$, o que atende perfeitamente a definição de K. Mas, olhando para o programa, $\psi_{P'}(0)\downarrow$.

**Para $x = 1$, será que $p' = 1$?**

Veja que $\psi_{\mathcal{P}'}(1)$ pode implicar em dois casos:

- $P_K(1) = 1$ significa que $1 \in K$, ou seja, $\Phi(1,1)\downarrow$, ou seja, $\psi_{P_1}(1)\downarrow$, o que atende perfeitamente a definição de K. Mas, olhando para o programa, $\psi_{P'}(1)\uparrow$.

- $P_K(1) = 0$ significa que $1 \notin K$, ou seja, $\Phi(1,1)\uparrow$, ou seja, $\psi_{P_1}(1)\uparrow$, o que atende perfeitamente a definição de K. Mas, olhando para o programa, $\psi_{P'}(1)\downarrow$.


**Para $x = i$, será que $p' = i$?**

Veja que $\psi_{\mathcal{P}'}(i)$, para qualquer $i$, pode implicar em dois casos:

- $P_K(i) = 1$ significa que $i \in K$, ou seja, $\Phi(i,i)\downarrow$, ou seja, $\psi_{P_i}(i)\downarrow$, o que atende perfeitamente a definição de K. Mas, olhando para o programa, $\psi_{P'}(i)\uparrow$.

- $P_K(i) = 0$ significa que $i \notin K$, ou seja, $\Phi(i,i)\uparrow$, ou seja, $\psi_{P_i}(i)\uparrow$, o que atende perfeitamente a definição de K. Mas, olhando para o programa, $\psi_{P'}(i)\downarrow$.

**Conclusão**

Veja que a definição de $K$ diz que o programa com elemento que está em $K$ para, e fazemos essa verificação através da função característica $P_K(i)$. Se $i$ pertence a $K$, então o programa $\mathcal{P}$ de código $i$ (ou seja, $P_i$) deve parar com entrada $i$. Porém, $\mathcal{P}'$ faz o contrário, entra em loop. E isso acontece para qualquer valor que $i$ assuma. Ou seja, $\mathcal{P}'$ não é nenhum dos programas da lista, pois $\mathcal{P}' \neq \mathcal{P}_0$, $\mathcal{P}' \neq \mathcal{P}_1$, $\mathcal{P}' \neq \mathcal{P}_2$, $\ldots$.

O fato deles produzirem resultados diferentes, ou seja, $\mathcal{P}_i$ e $\mathcal{P}'$ tem resultados diferentes para todo $i$, $\mathcal{P}'$ não está na lista. Um absurdo, pois a lista de programas lista todos os programas possíveis, mas não inclui $\mathcal{P}'$. Ou seja, $K$ não é recursivo.

### Exemplo 3.2: Prove que $TOT = \{z \in \mathbb{N} \mid (\forall x)\Phi(x,z)\downarrow\}$ não é r.e..

Intuição: $TOT$ é o conjunto de códigos de programas que não entram em loop, não importa a entrada. Ou seja, o conjunto de programas totais.

**PASSO 1:** Vamos assumir, por absurdo, que $TOT$ é recursivamente enumerável. Logo, pelo teorema 3.7, existe uma função primitiva recursiva $g(x)$ tal que

$$TOT = \{g(0), g(1), g(2), \ldots\}$$

**PASSO 2:** Seja $h(x) = \Phi(x, g(x)) + 1$. O desafio é encontrar essa função $h$ para gerar o absurdo. Sempre é bem situacional. E normalmente o $+1$ é boa prática para gerar absurdos.

Perceba que $g(x)$ nunca entra em loop, pois é primitivo recursivo. Já $Phi(x, g(x))$ é parcialmente computável, mas retorna o que $g(x)$ retorna. Ou seja, nesse caso $\Phi(x, g(x))$ é total, e portanto $h(x)$ é total, portanto computável.

**PASSO 3:** O código do programa $\mathcal{P}$ que computa $h(x)$ tem que estar em $TOT$, pois $h$ nesse momento é total. Portanto, $\#(P) = p \in TOT$.

Então existe um $i$ tal que $g(i) = p$. Pois se $p$ tá no $TOT$, tem algum $i$ que é entrada de $g$ que resulta em $p$, pois $p$ tá em $TOT$.

Usando o passo 2, temos que

$$h(i) = \Phi(i, g(i))+1 = \Phi(i, p) + 1 = h(i) + 1$$

Ou seja, $h(i) = h(i) + 1$, um absurdo. A substituição de $\Phi(i, p)$ por $h(i)$ é devido ao fato de que \Phi(i, p)$ retorna o que $h(i)$ retorna.

Portanto, o conjunto $TOT$ não é recursivamente enumerável.

## Definição 3.6: Redução

É um tipo de prova para provar que os conjuntos são ou não são recursivos, são ou não são r.e. ou se certas funções são ou não são computáveis.

Sejam $A$ e $B$ conjuntos. $A \leq_m B$ (A reduz-se para B) se há um função computável $f$ tal que 

$$A = \left\{ x \in \mathbb{N} \mid f(x) \in B \right\}$$

A intuição aqui é usar a redução de muitos para um, representado pela letra $m$. Nós dizemos que $A$ reduz-se a $B$ se há uma função $f$ computável tal que $x \in A$ se e somente se $f(x) \in B$. Isso significa que testar que $x \in A$ não é mais difícil do que testar que $y \in B$. Ou seja, testar que $x \in A$ é mais fácil ou igualmente difícil do que testar se $y \in B$.

**OBSERVAÇÃO:** Esse operador $\leq_m$ não é o mesmo da artimética tradicional! Ele se aplica apenas a conjuntos, e possui outro significado. 

### Teorema 3.10: Dado que $A \leq_m B$, Se $B$ é recursivo, então $A$ é recursivo.

**Prova:** Como $A \leq_m B$, então 

$x \in A$ se e somente se $f(x) \in B$, sendo $f$ computável.

Seja $P_B(x)$ a função característica de $B$. Logo,

$$
P_B(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \in B\\
0 & \text{se } x \notin B
\end{array}
\right.
$$

Então a gente pode afirmar que $x \in A \iff f(x) \in B \iff P_B(f(x)) = 1$.

Como $f$ é computável, então toda essa composição $P_B(f(x))$ é computável.

Agora seja $P_A(x)$ a seguinte função:

$$
P_A(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \in A\\
0 & \text{se } x \notin A
\end{array}
\right.
$$

Veja que pelo "se e somente se" acima, $x \in A \iff P_B(x) = 1$. Então eu posso substituir, fazendo

$$
P_A(x) =
\left\{
\begin{array}{ll}
1 & \text{se } P_B(f(x))\\
0 & \text{caso contrário}
\end{array}
\right.
$$

Como $P_A(x)$ é computável, logo $A$ é recursivo.

### Teorema 3.11: Dado que $A \leq_m B$, Se $B$ é recursivamente enumerável, então $A$ é recursivamente enumerável.

**Prova:** Se $B$ é r.e., então $B = \{x \in \mathbb{N} \mid g(x)\downarrow\}$, onde $g$ é parcialmente computável.

Pela definição de redução, $x \in A \iff f(x) \in B \iff g(f(x))\downarrow$. Se eu chamar essa composição $g(f(x))$ de $h(x)$ por hora, tenho que 

$$x \in A \iff f(x) \in B \iff g(f(x))\downarrow \iff h(x) \downarrow$$ 

Perceba que $h(x)$ é parcialmente computável devido a composição incluindo $g$. Se eu pegar, dessa equivalência, somente o $x \in A \iff h(x)\downarrow$, tenho a exata definição de um conjunto recursivamente enumerável. Veja que ele é exatamente o conjunto $A$:

$$A = \{A \in \mathbb{N} \mid h(x)\downarrow\}$$

Logo, $A$ é r.e.

### Teorema 3.12: Dado que $A \leq_m B$, se $A$ não é recursivo, então $B$ não é recursivo. E se $A$ não é r.e., então $B$ não é r.e..

**Prova:** só fazer a contrapositiva do teorema 3.10 e 3.11.

### Exemplo 3.3: Uso do $K$ e $\overline{K}$

Agora eu posso pegar o exemplo de $K$ e $\overline{K}$ para mostrar que um conjunto não é recursivo ou não é r.e..

**Para mostrar que não é recursivo, utilize $K$:** 

- $K \leq_m B $ implica em $x \in K \iff f(x) \in B$

**Para mostrar que não é r.e., utilize $\overline{K}$:** 

- $\overline{K} \leq_m B $ implica em $x \in \overline{K} \iff f(x) \in B$

Esse $f$ é uma função desconhecida computável. Para descobrir, é preciso do teorema 3.13 seguinte:

### Teorema 3.13 (Teorema do Parâmetro): Para cada $m, n > 0$, há uma função primitiva recursiva $S^{n}_{m}(u_1, u_2, \ldots, u_n, y)$ tal que $\Phi^{(m+n)}(x_1,\ldots,x_m,u_1,\ldots,u_n,y) = \Phi^{(m)}(x_1,\ldots,x_m,S^{n}_{m}(u_1,\ldots,u_n,y))$, onde $S^{n}_{m}(u_1,\ldots,u_n,y)$ é um programa $q$.

A utilidade desse teorema é descobrir quem é esse $f$ do exemplo anterior.

A prova é extensa e não provarei. Basta saber que esse $S$ vira nosso $f$ que buscamos. A função $S$ retorna um Número de Gödel.

**Exemplo:** $\Phi^{(2)}(x_1, x_2, y) = \Phi^{(1)}(x_1, S^1_1(x_2, y))$

### Teorema 3.14: O conjunto $EMPTY = \{x \in \mathbb{N} \mid W_x = \emptyset\}$ não é recursivamente enumerável.

**Prova:** Veja que $W_x = \{z \in \mathbb{N} \mid \Phi(z,x)\downarrow\}$

A interpretação do $EMPTY$ é a seguinte: um conjunto de (código de) programas onde o conjunto das entradas que fazem esses programas parerem não existem. Ou seja, é o conjunto de programas que sempre entram em loop infinito.

Lembrar que como ele está pedindo para provar que não é r.e., então devemos usar o $\overline{K}$ para reduzir a $EMPTY$. Ou seja, é suficiente, pra esse caso, provar que $\overline{K} \leq_m EMPTY$.

Sabendo que $K = \{x \in \mathbb{N} \mid \Phi(x,x)\downarrow\}$, o complemento $\overline{K}$ é $\overline{K} = \{x \in \mathbb{N} \mid \Phi(x, x)\uparrow\}$.


E pela definição de $\overline{K} \leq_m EMPTY$, temos que

$$x \in \overline{K} \iff f(x) \in EMPTY$$

Ora, mas quem é $f(x)$? O $f(x)$ é um código de programa, pois pertence a $EMPTY$. Nós temos essa informação, portanto:

- $x \in \overline{K} \iff f(x) \in EMPTY$

Resulta em

- $\Phi(x, x)\uparrow \iff W_{f(x)}=\emptyset$

**PASSO 1 - Preparando o terreno:**

Nesse passo, temos que construir o programa na linguagem $\mathscr{L}$. Este programa vai ser fundamental para fazer essa redução. Então toda a dificuldade da demonstração vai ser encontrar esse programa.

Uma vez que você construir um bom programa, o resto vai ficar mais fácil.

Seja $\mathcal{P}$ o programa

```
     Z ← Phi(X_2,X_2)
```
A engenhosidade aqui é usar a variável $X_2$ e deixar a variável $X_1$ totalmente sem uso.

Se esse programa $\Phi$ para, ele vai parar para qualquer valor de $X_1$, e se ele entra em loop, ele vai entrar em loop para qualquer valor de $X_1$. Nesse momento se percebe a ligação com o $EMPTY$.

O código do programa $\mathcal{P}$ é $\#(\mathcal{P}) = p$.

**PASSO 2**

Dado este programa, temos as seguintes relações:

- $\Phi(x_2, x_2)\uparrow \iff \forall x_1 \Phi(x_1,x_2,p)\uparrow$
- $\Phi(x_2, x_2)\downarrow \iff \forall x_1 \Phi(x_1,x_2,p)\downarrow$

Veja que essa equivalência lógica é verdade, pois se a função universal tem o comportamento da esquerda, não importa a entrada de $x_2$, não vai mudar o resultado da função universal da direita, e isso causa o mesmo resultado para ambas. Afinal, $x_1$ nunca vai ser usado por $\mathcal{P}$ para qualquer valor que $x_1$ assuma.

Outro detalhe é que essa relação só foi possível por conta do programa que escolhemos. Se o programa fosse outro, essa relação já não seria possível.

**PASSO 3:**

Atenção a seguinte relação passo a passo:

$$x_2 \in \overline{K} \iff \Phi(x_2, x_2) \uparrow \iff \forall x_1 \Phi(x_1,x_2,p)\uparrow \iff \forall x_1 \Phi(x_1, S^1_1(x_2,p))\uparrow \text{( Teorema do Parâmetro)} \iff W_{S^1_1(x_2, p)} = \emptyset \iff S^1_1(x_2, p) \in EMPTY \iff f(x_2) \in EMPTY$$

Perceba que $x_2 \in \overline{K} \iff f(x_2) \in EMPTY$ Portanto, $EMPTY$ não é r.e..

## Definição 3.7: Teorema de Rice e Conjunto $\Gamma$

Seja $\Gamma$ uma coleção de funções parcialmente computáveis $\Gamma = \{f_1, f_2,\ldots\}$. Define-se

$$R_{\Gamma} = \{t \in \mathbb{N} \mid \Phi_t \in \Gamma\}$$

O $t$ nesse caso representa o código dos programas que estão em $R_{\Gamma}$. Além disso, $\Gamma$ NÃO pode ser vazio, e precisa ter pelo menos um $f$.

Observe que $R_{\Gamma}$ é recursivo se há um predicado computável $g(t)$ tal que

$$g(t) \iff \Phi_t \in \Gamma$$

- $\Gamma$ é o conjunto de funções computáveis;
- $\Gamma$ é o conjunto de funções primitivas recursivas;
- $\Gamma$ é o conjunto de funções parcialmente computáveis que não estão definidas para um número finito de valores de $x$.

### Teorema 3.15 (Teorema de Rice): Seja $\Gamma$ uma coleção de funções parcialmente computáveis de uma variável. Sejam $f(x)$ e $g(x)$ funções parcialmente computáveis tais que $f(x) \in \Gamma$ e $g(x) \notin \Gamma$. Então $R_{\Gamma}$ não é recursivo.

O teorema tem uma prova extensa. Ele é muito útil para provar dois casos:

- Se o conjunto não é recursivo;
- Se o conjunto possui elementos que são códigos de um programa.

### Corolário 3.1: Seja $\Gamma$ um dos casos: $\Gamma$ é o conjunto de funções computáveis ou $\Gamma$ é o conjunto de funções primitivas recursivas ou $\Gamma$ é o conjunto de funções parcialmente computáveis que não estão definidas para um número finito de valores de $x$. Não há algoritmo para testar para um programa $\mathcal{P}$ da linguagem $\mathscr{L}$ se $\psi_{\mathcal{P}}^{(1)}(x) \in \Gamma$.

**Prova:** Para provar esse resultado, é suficiente mostrar as funções parcialmente computáeis $f(x)$ e $g(x)$ tal que $f(x) \in \Gamma$ e $g(x) \notin \Gamma$:

- $f(x) = u_1^1(x)$
- $g(x) = 1-x$

### Exemplo 3.4: Prove que $TOT = \{t \in \mathbb{N} \mid \forall x \Phi(x,t)\downarrow\}$ não é recursivo.

Veja que as duas condições são potencialmente atendidas:

- O exemplo pede para mostrar que não é recursivo, e portanto posso usar Teorema de Rice;
- O conjunto $TOT$ possui elementos que são códigos de um programa.

Então posso reduzir a um conjunto $R_{\Gamma}$. E logo em seguida o passo 1, que é achar o $\Gamma$ do problema:

**PASSO 1: Achar o $\Gamma$**

$$TOT = R_{\Gamma} \Rightarrow \Gamma = \{f \mid f \text{ é parcialmente computável, e } \forall x \in \mathbb{N} \text{, temos que } f(x)\downarrow\}$$

**PASSO 2:**

Agora eu preciso achar um exemplo de $f(x)$ que esteja em $\Gamma$, ou seja, que atenda a propriedade do conjunto acima, e um $g(x)$ que não esteja em $\Gamma$.

A propriedade diz que $f$ precisa ser total. Então se eu tiver um caso, é suficiente.

- $f(x) = 0$, ou  $f(x) = x$. Para todo $x$, a função sempre retorna algo.$

- $g(x) = \frac{x}{0}$. Para qualquer $x$, a função é parcial, ou seja, não está definida.

Portanto, $f(x) \in \Gamma$ e $g(x) \notin \Gamma$. Portanto, $TOT$ não é recursivo.

### Exemplo 3.5: Prove que $FIN = {t \in \mathbb{N} \mid W_t \text{ é finito}}$ não é recursivo.

Esse conjunto é o conjunto de programas que param para um conjunto finito de entradas.

Lembrar que $W_t = \{x \in \mathbb{N} \mid \Phi(x, t)\downarrow\}$.

**PASSO 1:**

Fazemos $FIN = R_{\Gamma}$. Vamos achar o $\Gamma$:

$$\Gamma = \{f \mid f \text{ é P.C. e está definida para um número finito de entradas}\}$$

**PASSO 2:**

$$
f(x) =
\left\{
\begin{array}{ll}
0 & \text{se } x = 0\\
\uparrow & \text{se } x \neq 0
\end{array}
\right.
$$

$$g(x) = 5032$$

Veja que $f(x) \in \Gamma$, pois está definido para o número zero apenas como entrada, e $g(x) \notin \Gamma$ pois está definido para um conjunto infinito de entradas.

Logo, $FIN$ não é recursivo.

### Exemplo 3.6: Mostre que $A = \{y \in  \mathbb{N} \mid \forall x [\Phi(x,y)\downarrow \wedge \Phi(x,y) > x]\}$ não é recursivo.

**PASSO 1:**

Reduzo $A = R_{\Gamma}$, tenho que o $\Gamma$ pode ser

$$\Gamma = \{f \mid f \text{ é P.C. e }\forall x f(x)\downarrow \text{ e } f(x) > x\}$$

**PASSO 2:**

- $f(x) = x+1 \in \Gamma$
- $g(x) = x \notin \Gamma$, pois por mais que para todo $x$ o $g(x)$ está definido, o $g(x)$ nunca será maior que $x$.

Logo, $A$ não é recursivo.

### Exemplo 3.7: Casos onde não é possível aplicar Teorema de Rice

Veja que o conjunto $A = \{x \in \mathbb{N} \mid \Phi(x, 1000)\downarrow\}$ não é recursivo, mas para mostrar, não consigo aplicar, pois perceba:

$$\Gamma = \{f \mid f \text{ é P.C. e é computado pelo programa de código 1000}\}$$

E o conjunto $R_{\Gamma} = \{1000, 72084819, 137723, \ldots\}$

Significa que existem infinitos programas que computam $f$. Não necessariamente nesse caso esses números resultariam em programas iguais, mas é um exemplo intuitivo, até porque posso criar programas $\mathcal{P}_1, \mathcal{P}_2, \mathcal{P}_3, \ldots$ que poderiam computar $f$ com as mesmas entradas que resultariam nas mesmas saídas, apenas com instruções rearranjadas de forma diferente. Ou seja, códigos diferentes. Porém, não tem como $A = R_{\Gamma}$, pois $A$ não é um conjunto infinito, muito menos conjunto que contém código de programas. Lembrar que Rice só se aplica para códigos. Veja que $x$ é uma entrada de $f$.

Outro caso é não ser possível aplicar o Teorema de Rice em $K = \{x \in \mathbb{N} \mid \Phi(x,x)\downarrow\}$, pois não há possibilidade de encontrar $\Gamma$. E esse é um caso onde mistura entrada com código, e o teorema só trabalha apenas com código de programas.

## Definição 4.1: Computação com Strings

Até agora a computação foi feita com números. O que mostrarei é que é possível computar com strings, e é tão poderoso quanto.

Baseado nisso, o que for computável com números, pode ser computado com strings e vice-versa.

A linguagem de programação adotada para strings será a $\mathscr{L}_n$, onde toda linguagem desse tipo possui um alfabeto $\Sigma_n = \{s_1,\ldots,s_n\}$, onde $s_i$ é uma letra do alfabeto.

As variáveis continuam sendo as mesmas:

- Variáveis de entrada: $X_1$, $X_2$, $X_3$, …

- Variável de saída: $Y$

- Variáveis auxiliares: $Z_1$, $Z_2$, $Z_3$, …

As variáveis $Y$ e $Z$ iniciam como strings vazias. Por hora são representadas como zero.

Os rótulos continuam sendo os mesmos:

- $A_1$, $B_1$, $C_1$, $E_1$,...

### Instruções de $\mathcal{L}_n$

As instruções são muito parecidas.

Para cada símbolo $\sigma$ no alfabeto $\Sigma$ ($\sigma$ é representado no código formatado abaixo pela letra $o$), essa operação coloca o símbolo $\sigma$ na esquerda da string que possui valor $V$.

```
     V ← oV
```

Essa operação deleta o símbolo final da string que tem valor $V$. Se o valor de $V$ é 0, deixa inalterado

```
     V ← V-
```

Para cada símbolo $\sigma$ no alfabeto $\Sigma$, e para cada label $L$, se o valor de $V$ termina com o símbolo $\sigma$, executa a primeira instrução rotulada como $L$. Se não, vai para a próxima instrução.

```
     IF V ENDS o GOTO L
```

## Definição 4.2: Macros

### $\text{IF } V \neq \epsilon \text{ GOTO } L$

Essa macro (Se $V$ for diferente da palavra vazia, vai para o rótulo L)

```
     IF V != e GOTO L
```

Pode ser desmembrada da seguinte forma:


```
     IF V ENDS s_1 GOTO L
     IF V ENDS s_2 GOTO L
     .
     .
     .
     IF V ENDS s_n GOTO L
```

Essa macro permite verificar se a palavra é vazia (representado pelo $e$ no programa, mesma coisa do $\epsilon$). Ou seja, quando é que ele não vai ser vazio? Quando ele terminar em alguma letra. Chego todas as letras do alfabeto $\Sigma_n$.

### $V \leftarrow 0$

Essa macro (V recebe a string vazia)

```
     V ← e
```

Pode ser desmembrada da seguinte forma:

```
[A]  V ← V-
     IF V != e GOTO A
```

Ela vai eliminando letra por letra da palavra até ela ficar vazia.

### $\text{GOTO } L$

Essa macro

```
GOTO L
```

Pode ser desmembrada da seguinte forma:

```
     Z ← e
     Z ← s_1Z
     IF Z ENDS s_1 GOTO L
```

### $V' \leftarrow V$

Essa macro

```
     V' ← V
```

Pode ser desmembrada da seguinte forma:

```
     Z ← e
     V' ← e

[A]  IF V ENDS s_1 GOTO B1
     IF V ENDS s_2 GOTO B2
     ...
     IF V ENDS s_n GOTO Bn
     GOTO C

[Bi] V ← V-    // INÍCIO DO BLOCO Bi, i = 1,...,n
     V' ← s_iV' //
     Z ← s_iZ  //
     GOTO A    // FIM DO BLOCO Bi, i = 1,...,n

[C]  IF Z ENDS s_1 GOTO D1
     IF Z ENDS s_2 GOTO D2
     ...
     IF Z ENDS s_n GOTO Dn
     GOTO E

[Di] Z ← Z-    // INÍCIO DO BLOCO Di, i = 1,...,n
     V ← s_iV  //
     GOTO C    // FIM DO BLOCO Di, i = 1,...,n
```

Observação: o conjunto de instruções

```
[A]  IF V ENDS s_1 GOTO B1
     IF V ENDS s_2 GOTO B2
     ...
     IF V ENDS s_n GOTO Bn
     GOTO C
```

Pode ser resumido em

```
[A]  IF V ENDS s_i GOTO Bi     // 1 <= i <= n
     GOTO C
```

Além disso, o início e fim do bloco marcam as repetições para o código não ficar extenso. Ou seja, para todo $i$ de 1 até $n$, o código será repetido de bloco em bloco, demarcado pelo comentário com duas barras.

### Macro sucessor: $X \leftarrow X + 1$

Essa macro

```
     X ← X + 1
```

Pode ser desmembrada da seguinte forma:

```
[B]  IF X ENDS s_i GOTO Ai    // 1 <= i <= n
     Y ← s_1Y
     GOTO E

[Ai] X ← X-         // INÍCIO DO BLOCO Ai, 1 <= i < n
     Y ← s_{i+1}Y   //
     GOTO C         // FIM DO BLOCO Ai, 1 <= i < n

[An] X ← X-
     Y ← s_1Y
     GOTO B

[C]  IF X ENDS s_i GOTO Di    // 1 <= i <= n
     GOTO E

[Di] X ← X-    // INÍCIO DO BLOCO Di, 1 <= i <= n
     Y ← s_iY  //
     GOTO C    // FIM DO BLOCO Di, 1 <= i <= n
```

Essa macro é útil para pegar a palavra e obter o sucessor dela, na ordem alfabética.

Por exemplo, suponha $\Sigma_3 = \{a, b, c\}$. Ao aplicar o sucessor para esses 4 casos, eu tenho:

- $acc + 1 = baa$
- $bab + 1 = bac$
- $aab + 1 = aac$
- $cc + 1 = aaa$

### Macro predecessor: $X \leftarrow X ∸ 1$

Essa macro

```
     X ← X - 1
```

Pode ser desmembrada da seguinte forma:

```
[B]  IF X ENDS s_i GOTO Ai
     GOTO E

[Ai] X ← X-         // INÍCIO DO BLOCO Ai, 1 < i <= n
     Y ← s_{i-1}Y   //
     GOTO C         // FIM DO BLOCO Ai, 1 < i <= n

[A1] X ← X-
     IF X != e GOTO C2
     GOTO E

[C2] Y ← s_nY
     GOTO B

[C]  IF X ENDS s_i GOTO Di    // 1 <= i <= n
     GOTO E

[Di] X ← X-    // INICIO DO BLOCO Di, 1 <= i <= n
     Y ← s_iY  //
     GOTO C    // FIM DO BLOCO Di, 1 <= i <= n
```

Essa macro é útil para pegar a palavra e obter o predecessor dela, na ordem alfabética.

Por exemplo, suponha $\Sigma_3 = \{a, b, c\}$. Ao aplicar o predecessor para esses 4 casos, eu tenho:

- $baa ∸ 1 = acc$
- $bac ∸ 1 = bab$
- $aac ∸ 1 = aab$
- $aaa ∸ 1 = cc$

### Exemplo 4.1: Crie a macro $V \leftarrow V\sigma$ (adicionar a letra ao final da palavra)

Suponha um alfabeto $\Sigma_n = \{s_1, \ldots, s_n\}$.

```
     V' ← e
     V' ← oV'

[B]  IF V ENDS s_i GOTO Ai    // 1 <= i <= n
     V ← V'
     GOTO E

[Ai] V ← V-         // INICIO DO BLOCO Ai, 1 <= i <= n
     V' ← s_iV'     //
     GOTO B         // FIM DO BLOCO Ai, 1 <= i <= n
```

### Exemplo 4.2: Crie a macro $V \leftarrow -V$ (retira a primeira letra da string)

Suponha um alfabeto $\Sigma_n = \{s_1, \ldots, s_n\}$.

```
     V ← e

[B]  IF V ENDS s_i GOTO Ai    // 1 <= i <= n

[C]  V ← V'
     GOTO E

[Ai] V ← V-              // INICIO DO BLOCO Ai, 1 <= i <= n
     IF V = e GOTO C     //
     V' ← s_iV'          //
     GOTO B              // FIM DO BLOCO Ai, 1 <= i <= n
```
