### Definição: Função de Pareamento

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

### Definição: Número de Gödel

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

### Codificando um programa - introdução

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

### Definição: Problema da Parada

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

### Definição: Programa Universal

O programa universal é definido como

$$\Phi^{(n)}(x_1, x_2, \ldots, x_n, x_{n+1}) = \psi_P^{(n)}(x_1,x_2,\ldots ,x_n)$$

, onde $x_{n+1} = \#(P)$, $(n)$ é uma notação indicando o número de argumentos usados no programa $\psi$.

O programa universal é o que o computador faz. O computador é a materialização física do que a função universal faz.

### Teorema: a função $\Phi^{(n)}$ é parcialmente computável, com $n > 0$.

**Prova:**

Se é Parcialmente Computável, tem um programa que computa. O programa vai ser demonstrado depois.

### Definição: codificação de estados

Posso usar Número de Gödel pra codificar estados da seguinte forma:

$$[Y \text{ } X_1 \text{ } Z_1 \text{ } X_2 \text{ } Z_2 \text{ } X_3 \text{ } Z_3 \text{ } \ldots]$$

**Exemplo:** O programa tá no estado inicial e possui entradas $X_1 = 20$, $X_2 = 3$ e $X_3 = 65$. Qual o código correspondente a esse estado?

- O código é o $[0 \text{ } 20 \text{ } 0 \text{ } 3 \text{ } 0 \text{ } 65] = 3^{20} \cdot 7^3 \cdot 13^{65}$.

Perceba que no estado inicial, $Y$ e os auxiliares $Z$ iniciam com 0, que são as posições ímpares.

### Instruções do Programa Universal

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

### Definição: Função STEP - Introdução

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

### Definição: Função STEP - Final

Agora podemos formular a função STEP, que retorna 1 se o programa parou com $i$ passos, ou 0 caso contrário. Ele analisa frame por frame cada passo da computação através do snapshot e verifica se a linha atual do snapshot após $i$ passos é $Lt(y+1)+1$, ou seja, depois da contagem de linhas do programa.

$$
STP(x_1,...,x_n,y,i) = \begin{cases} 
1 & \text{, se } TERM(SNAP(x_1,...,x_n,y,i),y) = 1 \\
0 & \text{, caso contrário.} 
\end{cases}
$$

Todas as funções mostradas aqui são primitivas recursivas.

### Definição: Conjunto Recursivamente Enumerável

Um conjunto $B \subseteq \mathbb{N}$ é recursivamente enumerável (abreviação r.e.) se há uma função parcialmente computável $g(x)$ tal que

$$
g(x) = \begin{cases} 
\downarrow & \text{, se } x \in B \\
\uparrow  & \text{, se } x \notin B 
\end{cases}
$$

Em outras palavras,

$$B = {x \in \mathbb{N} | g(x)\downarrow}$$

, onde $\uparrow$ significa que o programa entra em loop infinito, e $\downarrow$ significa que o programa para.

### Definição: Conjunto Recursivo (Computável)

Um conjunto $B \subseteq \mathbb{N}$ é recursivo se há uma função computável g(x) tal que

$$
g(x) = \begin{cases} 
1 & \text{, se } x \in B \\
0  & \text{, se } x \notin B 
\end{cases}
$$

Eu posso chamar $g(x)$ de **função característica de $B$**, que implementa o predicado *pertence*:

$$
g(x) = P_B(x) = \begin{cases} 
1 & \text{, se } x \in B \\
0  & \text{, se } x \notin B 
\end{cases}
$$