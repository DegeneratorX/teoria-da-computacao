## Definição 5.1: Máquina de Turing

Uma Máquina de Turing (MT) é definida da seguinte forma:

$$M = (Q, \Sigma, \Gamma, q_0, \delta)$$

Onde

- $Q$: Conjunto finito de estados. Os estados de parada $h_a$ (aceitação) e $h_r$ (rejeição) pertencem a $Q$;

- $\Sigma$: Alfabeto de entrada;

- $\Gamma$: Alfabeto da fita. Um detalhe importante é que $\Sigma \subseteq \Gamma$. Útil para listar as variáveis auxiliares;

- $q_0$: Estado Inicial da MT. Para a computação existir, seja na linguagem $\mathscr{L}$ de instruções ou na MT, é preciso ter um estado inicial.

- $\delta$: Uma função de comando do tipo $\delta : \underbrace{Q \times(\Gamma \cup \{\Delta\})}_{\text{Entrada}} \longrightarrow \underbrace{(Q \cup \{h_a, h_r\}) \times (\Gamma \cup \{\Delta\}) \cup (\{R, L, S\})}_{\text{Saída}}$, onde $\Delta$ é um símbolo em branco.

Uma função $\delta(q, \sigma) = (q', \sigma', \text{direção})$ representa a função definida $\delta$ acima. 

- $q$ e $q'$: estados quaisquer;

- $\sigma$ e $\sigma'$: Quaisquer símbolos $\in \Gamma \cup \{\Delta\}$;

- $\text{direção}$: Pode ser $L$ (move o cabeçote para esuqerda), $R$ (move o cabeçote para a direita) ou $S$ (stationary, não desloca o cabeçote).

Se eu tiver esse comando, com $\Sigma = \{a, b\}$:

$$\delta(q_2, b) = (q_3, a, L)$$

Lê-se: Se a máquina está no estado $q_2$ lendo o símbolo $b$,  eu vou para o estado $q_3$, vou trocar a letra que leio por $a$, e ando 1 casa a esquerda na fita.

**OBSERVAÇÃO 1:** Se o resultado produzido for $(h_a \text{ou} h_r, a, L)$, então a máquina deve parar.

**OBSERVAÇÃO 2:** A notação de $\delta$ é equivalente a notação $f : \mathbb{N} \longrightarrow \mathbb{N}$.

**OBSERVAÇÃO 3:** Uma MT não precisa ler toda a aentrada para aceitar (parar) ou rejeitar (parar). Já um autômato sim.

## Definição 5.2: Configuração (Snapshot)

Uma configuração (Snapshot) pode ser representada de várias formas. A mais completa é em forma de string.

### Exemplo 5.1: Suponha $\Sigma = \{a, b\}$ sendo o alfabeto de entrada, e $\Gamma = \{a, b, A, B\}$ o alfabeto da fita.

Seja uma fita

```
Δ a b [q2 a] b B Δ Δ ...
```

Onde $\Delta$ são símbolos em branco, e $[q2 a]$ é o momento onde está sendo lido.

A configuração que representa essa fita é a seguinte: $a b q_2 a b B$.

O cabeçote é representado pelo estado atual, e na string fica logo antes do caractere que o cabeçote está posicionado na fita. Símbolos em branco APENAS no começo e fim são ignorados.

Eu posso representar a string também da seguinte forma:

- $abq_2 abB \Rightarrow xq_2 y$

Onde

- $x = "ab"$, toda a string que vem antes da representação do estado.

- $y = "abB"$, toda a string que aparece após a representação do estado.

Isso é apenas uma forma de generalizar tudo que vem antes ou depois do cabeçote.

## Definição 5.3: Passo de uma MT

Se $q_o \in Q$ e $q_j \in Q \cup \{h_a, h_r\}$, então

$$xq_i y \vdash_M zq_j w$$

representa 1 passo na computação, onde a máquina M mudou da primeira configuração para a segunda configuração. Além disso

$$xq_i y \vdash_M^* zq_j w$$

representa 0, 1 ou $n$ passos para chegar da primeira para a segunda configuração.

### Exemplo 5.1

Suponha as transições

```
Δ a b [q3 a] a b Δ ...
```

```
Δ a [q4 b] A a b Δ ...
```

```
Δ [ha a] b A a b Δ ...
```

Como eu represento de $q_3$ para $q_4$?

$$abq_3 ab \vdash_M aq_4 bAab$$

Como eu represento de $q_3$ para $h_a$?

$$abq_3 ab \vdash_M^* h_a abAab$$

**OBSERVAÇÃO:** Na definição 5.3, $q_i$ NÃO está em $\{h_a, h_r\}$, pois se ele vai para $q_j$, ele não poderia sair desses dois estados. Ou seja, não há computação, pois a MT já parou.

## Definição 5.4: Configuração (Snapshot) inicial

A configuração (snapshot) inicial de uma MT para uma entrada qualquer $w$ na fita é

$$q_0\Delta w$$

Ou seja, na fita a configuração inicial é representada assim:

```
[q0 Δ] σ0 σ1 σ2 σ3 σ4 ...
```

Com $\sigma_i \in \Gamma \cup \{\Delta\}$, e $w = \sigma_0 \sigma_1 \sigma_2 \sigma_3 \sigma_4 \ldots$ é a entrada da fita. Inclui também os brancos infinitos para a direita. Exemplo: $w = bab(\Delta\Delta\Delta\ldots)$.

Para todo caso, a MT terá essa configuração inicial. Ou seja, começa em um símbolo branco.

## Definição 5.5: Linguagem Recursivamente Enumerável (ou Turing-Reconhecível, ou Semi-Decidível)

Assim como os conjuntos numéricos serviram para os Programas, o conjunto de linguagens servem para as Máquinas de Turing.

Seja $M = (Q, \Sigma, \Gamma, q_0, \delta)$ uma MT, e $w \in \Sigma^*$. Então $w$ é aceita por $M$ se

$$q_0 \Delta w \vdash_M^* x h_a y$$

A linguagem $L \subseteq \Sigma^*$ é r.e. (reconhecida) por $M$ se

$$L = L(M) = \{w \in \Sigma^* \mid w \text{ é aceita por } M\}$$

**OBSERVAÇÃO:** A simbologia $\Sigma^*$ representa o conjunto infinito de todas as palavras possíveis que podem ser formadas com esse alfabeto. Exemplo: $\Sigma = \{a, b\}$. Então $\Sigma^* = \{\epsilon, a, b, aa, bb, bab, aaab, \ldots\}$, onde $\epsilon$ é uma palavra vazia.

É fácil perceber o paralelo entre conjuntos numéricos r.e. e linguagens r.e. Se $L$ é um conjunto r.e., eu não tenho garantia se uma palavra $w$ não pertence a linguagem $L$. Ou seja, não teria a certeza se ela iria para o estado de rejeição, que equivale, nos conjuntos numéricos, a retornar zero. Nesse caso a MT pode ter simplesmente entrado em loop infinito.

## Definição 5.6: Linguagem Recursiva (ou Turing-Decidível)

Seja $M = (Q, \Sigma, \Gamma, q_0, \delta)$ uma MT, $w \in \Sigma^*$ e $L \subseteq \Sigma^*$. Então $w$ é decidida por $M$ se a MT sempre para, seja em $h_a$ ou $h_r$.

Ou seja, a MT sempre para se a string pertencer ou não a linguagem. Se a linguagem é recursiva, então ela é r.e..

## Definição 5.7: Convertendo autômatos em MTs

MTs são representadas visualmente através de grafos, onde cada aresta representa uma transição de estado.

Autômatos finitos sempre leem a string em uma direção só, sempre param, não possuem memória, não é possível escrever e trabalham com gramáticas regulares.

MT podem ler a string e mover o cabeçote para várias direções ($L$, $R$, $S$), podem parar ou não, a fita infinita funciona como uma memória, é possível escrever, e trabalham com gramáticas irrestritas.

Por conta da gramática regular GR ser um subconjunto das gramáticas irrestritas GI, então todo autômato pode ser convertido para uma máquina de turing determinística.

### Exemplo 5.2: Converter o seguinte autômato para uma MT:

- $\delta(q_0, a) = q_1$
- $\delta(q_0, b) = q_2$
- $\delta(q_1, a) = q_1$
- $\delta(q_1, b) = h_a$
- $\delta(q_2, a) = q_3$
- $\delta(q_2, b) = q_2$
- $\delta(q_3, a) = q_1$
- $\delta(q_3, b) = h_a$

Conversão:

- $\delta(q_0, \Delta) = (q_1, \Delta, R)$
- $\delta(q_1, a) = (q_4, a, R)$
- $\delta(q_1, b) = (q_2, b, R)$
- $\delta(q_2, a) = (q_3, a, R)$
- $\delta(q_2, b) = (q_2, b, R)$
- $\delta(q_3, a) = (q_4, a, R)$
- $\delta(q_3, b) = (q_5, b, R)$
- $\delta(q_3, \Delta) = (h_a, \Delta, R)$
- $\delta(q_4, a) = (q_4, a, R)$
- $\delta(q_4, b) = (q_5, b, R)$
- $\delta(q_5, a) = (q_5, a, R)$
- $\delta(q_5, b) = (q_5, b, R)$
- $\delta(q_5, \Delta) = (h_a, \Delta, R)$

 Lembrar que a fita sempre terá como primeiro caractere o branco. Além disso, um autômato só lê para a direita e sempre para, não podendo voltar na fita.

 **OBSERVAÇÃO:** Para não poluir, por convenção, se houver transições faltantes, então por convenção elas levam para o estado de rejeição:

 - $\delta(q_1, \Delta) = (h_r, \Delta, R)$
 - $\delta(q_2, \Delta) = (h_r, \Delta, R)$
 - $\delta(q_4, \Delta) = (h_r, \Delta, R)$

Normalmente não se deve listar elas a não ser que seja necessário evidenciar.

## Definição 5.8: Algoritmos para a Máquina de Turing

### Exemplo 5.3: Seja uma MT $M = (Q, \Sigma, \Gamma, q_0, \delta)$ uma MT, $w \in \Sigma^*$ com uma única fita. Construir essa MT para aceitar/reconhecer a linguagem $L = \{ww \mid w \in \Sigma^* =  \{a, b\}^*\}$ (ou seja, aceita se a entrada tem o padrão $ww$, rejeita ou entra em loop se não tem esse padrão).

Se a questão diz para construir uma MT que reconheça a linguagem $L$, logo $L$ é recursivamente enumerável. Se chamarmos a entrada de $x$, então

$$L = \{x \in \Sigma^* \mid x \text{ é aceita por MT, ou seja, } \downarrow\}$$

Esse é um caso de linguagem r.e., mas caso eu rejeite a palavra $x$, a MT ainda assim para, e portanto $L$ pode ser também recursiva.

A ideia é construir uma MT que reconheça essa linguagem, onde a MT para e aceita $x$ se $x = ww$, rejeita caso contrário. Seja uma função "f" computada pela MT:

$$
f(x) =
\left\{
\begin{array}{ll}
\downarrow \text{ no estado } h_a & \text{se } x = ww\\
\downarrow \text{ no estado } h_r \text{ ou } \uparrow & \text{caso contrário}
\end{array}
\right.
$$

A intuição é achar o padrão $ww \in L \iff w \in \Sigma^*$. Primeiro faço a iteração para achar o meio da palavra $x$. Depois, analiso caractere por caractere. A seguinte MT reconhece a linguagem:

- $\delta(q_0, \Delta) = (q_1, \Delta, R)$

- $\delta(q_1, a) = (q_2, A, R)$
- $\delta(q_1, b) = (q_2, B, R)$
- $\delta(q_1, A) = (q_5, A, L)$
- $\delta(q_1, B) = (q_5, B, L)$
- $\delta(q_1, \Delta) = (h_a, \Delta, S)$

- $\delta(q_2, a) = (q_2, a, R)$
- $\delta(q_2, b) = (q_2, b, R)$
- $\delta(q_2, A) = (q_3, A, L)$
- $\delta(q_2, B) = (q_3, B, L)$
- $\delta(q_2, \Delta) = (q_3, \Delta, L)$

- $\delta(q_3, a) = (q_4, A, L)$
- $\delta(q_3, b) = (q_4, B, L)$

- $\delta(q_4, a) = (q_4, a, L)$
- $\delta(q_4, b) = (q_4, b, L)$
- $\delta(q_4, A) = (q_1, A, R)$
- $\delta(q_4, B) = (q_1, B, R)$

- $\delta(q_5, A) = (q_5, a, L)$
- $\delta(q_5, B) = (q_5, b, L)$
- $\delta(q_5, \Delta) = (q_6, \Delta, R)$

- $\delta(q_6, a) = (q_7, A, R)$
- $\delta(q_6, b) = (q_8, B, R)$
- $\delta(q_6, \Delta) = (h_a, \Delta, S)$

- $\delta(q_7, a) = (q_7, a, R)$
- $\delta(q_7, b) = (q_7, b, R)$
- $\delta(q_7, A) = (q_9, \Delta, L)$
- $\delta(q_7, \Delta) = (q_7, \Delta, R)$

- $\delta(q_8, a) = (q_8, a, R)$
- $\delta(q_8, b) = (q_8, b, R)$
- $\delta(q_8, B) = (q_9, \Delta, L)$
- $\delta(q_8, \Delta) = (q_8, \Delta, R)$

- $\delta(q_9, a) = (q_9, a, L)$
- $\delta(q_9, b) = (q_9, b, L)$
- $\delta(q_9, A) = (q_6, A, R)$
- $\delta(q_9, B) = (q_6, B, R)$
- $\delta(q_9, \Delta) = (q_9, \Delta, L)$

Não é possível criar um autômato para esse caso. Não tem como ver onde fica a metade da string. Mas em uma MT é possível.

A saída da fita não importa. A fita fica poluída, sim, mas o que importa é a MT estar no estado de aceitação ou rejeição.

Ou seja, temos que para esse caso, $h_a \in L$ e $h_r \notin L$.

Quando a linguagem é recursiva, eu sei quando pertence ou não a linguagem, usando $h_a$ ou $h_r$ (equivalente a 1 ou 0 a nível de programa). Quando não é recursivo, não tenho certeza se para. Essa linguagem em particular é recursiva.

Lembrar que quase todas as funções matemáticas conhecidas são computáveis, portanto, é possível construir funções características para a maioria dos problemas. Do mesmo modo isso ocorre para construir MTs decidíveis para uma linguagem.

Tudo isso é mais detalhado na frente

## Definição 5.9: Máquina de Turing Universal

A linguagem é como um conjunto numérico qualquer. Por exemplo, o conjunto $K = \{x \in \mathbb{N} \mid \Phi(x, x)\downarrow\}$ funciona como uma linguagem. O programa universal, a nível de hardware, é representado pela Máquina de Turing Universal. A codificação de uma MT é complexa e é representada em uma string guardada em uma fita, com seus respectivos estados e transições codificados em Número de Gödel.

Normalmente, duas fitas ou mais representam dois ou mais parâmetros a nível de programa de uma função, mas é possível passar várias entradas em uma fita só, porém pode ficar complexo.

## Definição 5.10 Computando Funções Parciais

Seja uma MT $M = (Q, \Sigma, \Gamma, q_0, \delta)$, $k \in \mathbb{N}$, e $f$ uma função parcial tal que $f : (\Sigma^*)^k \longrightarrow \Gamma^*$. Dizemos que $M$ computa $f$ se para todo $(x_1, x_2, \ldots, x_k)$ no domínio de $f$,

$$q_0 \Delta x_1 \Delta x_2 \Delta x_3 \ldots \Delta x_k \vdash_M^* \Delta f(x_1, x_2, \ldots, x_n)$$

e nenhuma outra entrada que é uma K-TUPLA em $(\Sigma^*)^k$ é aceita por $M$. Nesse caso, dizemos que $f$ é turing-decidível, turing-computável, ou simplesmente computável.

Basicamente essa definição 1 diz que se eu tenho várias entradas sendo passadas na fita em formato alternado com branco:

```
[q0 Δ] x1 Δ x2 Δ ... Δ xk Δ ...
```

então eu consigo em $n$ passos retornar, na mesma fita, o valor de uma função $f$ que a MT computa:

```
[ha Δ] f(x1, ..., xk) Δ ...
```

Eu retorno o cabeçote para o início durante o estado de aceitação, para que essa MT seja útil para macros, algo que veremos depois.

## Definição 5.11: Predicado Decidível (Computável)

Um predicado computável (decidível) é uma função que pode ser computada (decidida) por uma MT, que para o cabeçote no estado de aceitação com apenas 1 caractere se a propriedade do predicado é verdadeira, e para no estado de aceitação retornando tudo branco caso contrário.

Isso é equivalente, a nível de programa, a dizer que o programa retorna 1 se a propriedade do predicado é verdadeira, e retorna 0 caso contrário.

Um predicado computável é total, portanto sempre está definida para qualquer domínio da função.

## Definição 5.11: Função Característica de uma Linguagem

Seja $L$ uma Linguagem Recursiva. Para uma linguagem $L \subseteq \Sigma$, a função característica de $L$ é a função total $\mathcal{X} : \Sigma^* \longrightarrow \{0, 1\}$ definida por

$$
\mathcal{X}_L(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \in L\\
0 & \text{se } x \notin L
\end{array}
\right.
$$

Até agora vimos duas utilidades das MTs:

- Reconhecer uma linguagem $L$;
- Computar uma função $f$.

### Teorema 5.1: Dada uma MT que computa $\mathcal{X}_L$, é possível construir uma MT que reconhece uma linguagem $L$.

**Prova:** 

Dado que $L$ é recursivo, posso construir uma MT que sempre para. Naturalmente de início construímos mandando para o estado de aceitação para toda entrada da seguinte forma:

$$
\Delta x \Delta\Delta \ldots \vdash_M^*
\left\{
\begin{array}{ll}
\Delta 1 \Delta \ldots & \text{se } x \in L\\
\Delta \Delta \Delta \ldots & \text{se } x \notin L
\end{array}
\right.
$$

Seja a função característica de $L$:

$$
\mathcal{X}_L(x) =
\left\{
\begin{array}{ll}
1 & \text{se } x \in L\\
0 & \text{se } x \notin L
\end{array}
\right.
$$

Baseado no que a função característica pede, a ideia é fazer uma mudança no estado de aceitação para o caso em que a string $x$ não pertence a linguagem $L$, que anteriormente iria pra aceitação. Ou seja, p/ todo caso onde a MT para e não está em L, eu troco o estado de aceitação por um estado de rejeição.

Tome como exemplo essa transição:

- $\delta(q, ?) = (h_a, ?, S)$ (1)

Troco por

- $\delta(q, ?) = (q', ?, S)$
- $\delta(q', \Delta) = (q'', \Delta, R)$ (2)
- $\delta(q'', \Delta) = (h_r, \Delta, S)$
- $\delta(q'', 1) = (h_a, 1, S)$

Para todas as transições que mandavam para o estado de aceitação, eu converto o estado de aceitação em (1) por uma checagem em (2) para saber se a fita está com 1 caractere ao final da execução ou a fita está totalmente branca. Se estiver com pelo menos 1 caractere, manda para aceitação. Se a fita estiver branca, manda para rejeição, assim consigo retornar uma informação útil se $x$ está ou não em $L$.