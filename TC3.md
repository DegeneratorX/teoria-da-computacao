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

Seja $M = (Q, \Sigma, \Gamma, q_0, \delta)$ uma MT, e $L \subseteq \Sigma^*$. Então $L$ é recursivamente enumerável se

$$L = L(M) = \{w \in \Sigma^* \mid w \text{ é aceita por } M\}$$

ou seja, $w \in L$ produz o seguinte resultado na MT:

$$q_0 \Delta w \vdash_M^* x h_a y$$

onde $h_a$ é o estado de aceitação que indica que $w \in L$. Ou seja, se chegou em $h_a$, é porque $w$ atende a propriedade de $L$ e foi aceita por $M$.

É fácil traçar o paralelo entre conjuntos numéricos r.e. e linguagens r.e.:

Se $L$ é exclusivamente um conjunto r.e. e não é recursiva, dada uma MT, eu não tenho garantia se uma palavra $w$ qualquer não pertence a linguagem. Ou seja, uma MT que recebe $w$ como argumento e possivelmente não está em $L$ poderia simplesmente entrar em loop e eu não obter a resposta.

Outro ponto a destacar é que, por convenção, para indicar que um elemento está na linguagem, mandamos para um estado de aceitação. O estado de rejeição também faz a MT parar, porém ele só ganha importância nas linguagens recursivas, pois é puramente um metadado. Pode-se substituir o estado de aceitação por rejeição e isso não muda, pois a MT continua parando para a entrada que esteja em L.

**OBSERVAÇÃO:** A simbologia $\Sigma^*$ representa o conjunto infinito de todas as palavras possíveis que podem ser formadas com esse alfabeto. Exemplo: $\Sigma = \{a, b\}$. Então $\Sigma^* = \{\epsilon, a, b, aa, bb, bab, aaab, \ldots\}$, onde $\epsilon$ é uma palavra vazia.

## Definição 5.6: Linguagem Recursiva (ou Turing-Decidível)

Seja $M = (Q, \Sigma, \Gamma, q_0, \delta)$ uma MT, $L \subseteq \Sigma^*$. Então $L$ é recursiva se

$$L \cup \overline{L} = \{w \in \Sigma^* \mid w \text{ é decidida por } M\}$$

Ou seja, a MT sempre para se a palavra pertencer ou não a linguagem. Nesse caso, por convenção, em caso da MT parar indicando que a palavra não atende a propriedade da linguagem, nós trocamos o estado de aceitação por rejeição para facilitar a identificação (informação importante!), afinal isso seria apenas um metadado, pois os dois estados são estados de parada, e eu escolho para onde vai. Assim a MT pode produzir esses dois possíveis resultados:

$$
q_0 \Delta w \vdash_M^* =
\left\{
\begin{array}{ll}
x h_a y & \text{se } w \in L\\
k h_r z & \text{se } w \notin L
\end{array}
\right.
$$

Onde $h_a$ é o estado de aceitação que indica que $w \in L$, e $h_r$ é o estado de rejeição que indica que $w \notin L$.

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

Esse é um caso de linguagem r.e., mas caso eu consiga implementar uma rejeição a palavra $x$, a MT ainda assim para, e portanto $L$ será também recursiva.

A ideia é construir uma MT que reconheça essa linguagem, onde a MT para e aceita $x$ se $x = ww$,rejeita caso contrário. Seja uma função $f$ computada pela MT:

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

Duas fitas ou mais introduzidas em uma MT representam memórias adicionais para simplificar operações de comparação ou cópia, mas podem representar também dois parâmetros de entrada. Porém no curso iremos ver múltiplas fitas como auxiliares, e parâmetros da MT passados na fita principal, que se trata da Definição 5.10.

## Definição 5.10 Computando Funções Parciais

Seja uma MT $M = (Q, \Sigma, \Gamma, q_0, \delta)$, $k \in \mathbb{N}$, e $f$ uma função parcial tal que $f : (\Sigma^*)^k \longrightarrow \Gamma^*$. Dizemos que $M$ computa $f$ se para todo $(x_1, x_2, \ldots, x_k)$ no domínio de $f$,

$$q_0 \Delta x_1 \Delta x_2 \Delta x_3 \ldots \Delta x_k \vdash_M^* \Delta f(x_1, x_2, \ldots, x_n)$$

e nenhuma outra entrada que é uma K-TUPLA em $(\Sigma^*)^k$ é aceita por $M$. Nesse caso, dizemos que $f$ é turing-decidível, turing-computável, ou simplesmente computável.

Basicamente essa definição 1 diz que se eu tenho uma ou mais entradas sendo passadas na fita em formato alternado com branco:

```
[q0 Δ] x1 Δ x2 Δ ... Δ xk Δ ...
```

então eu consigo em $n$ passos retornar, na mesma fita, o valor de uma função $f$ total que a MT computa:

```
[ha Δ] f(x1, ..., xk) Δ ...
```

Eu retorno o cabeçote para o início durante o estado de aceitação, para que essa MT seja útil para macros, algo que veremos depois.

### Exemplo 5.4: Como eu computo a função $f(x1, x2) = x_1 + x_2$?

Essa é a função $SOMA(x_1, x_2)$, que é primitiva recursiva, e portanto computável. Para mostrar a nível de hardware, basta concatenar as duas entradas. Se a entrada é de acordo com a Definição 5.10, então temos duas entradas, que na fita estarão assim:

```
[q0 Δ] 1 1 1 1 1 Δ 1 1 1 Δ ... // 5, 3
```

A soma nesse caso é apenas concatenção:

```
[q0 Δ] 1 1 1 1 1 1 1 1 Δ ... // 8
```

Intuição:

- Vá até o símbolo em branco após as 2 entradas;
- Volte uma casa e apague o 1 que estiver lá;
- Volte até o símbolo em branco entre as entradas e troque por 1;
- Volte até o branco inicial (somente para uso em macros futuras).

A implementação da MT segue:

- $\delta(q_0, \Delta) = (q_1, \Delta, R)$

- $\delta(q_1, 1) = (q_1, 1, R)$
- $\delta(q_1, \Delta) = (q_2, \Delta, R)$

- $\delta(q_2, 1) = (q_2, 1, R)$
- $\delta(q_2, \Delta) = (q_3, \Delta, L)$

- $\delta(q_3, 1) = (q_4, \Delta, L)$
- $\delta(q_3, \Delta) = (q_5, \Delta, L)$

- $\delta(q_4, 1) = (q_4, 1, L)$
- $\delta(q_4, \Delta) = (q_5, 1, L)$

- $\delta(q_5, 1) = (q_5, 1, L)$
- $\delta(q_5, \Delta) = (h_a, \Delta, S)$

## Definição 5.11: Predicado Decidível (Computável)

Um predicado computável (decidível) é uma função que pode ser computada (decidida) por uma MT, que para o cabeçote no estado de parada com apenas 1 caractere se a propriedade do predicado é verdadeira, e para no estado de parada retornando tudo branco caso contrário.

Isso é equivalente, a nível de programa, a dizer que o programa retorna 1 se a propriedade do predicado é verdadeira, e retorna 0 caso contrário.

Um predicado computável é total, portanto sempre está definida para qualquer domínio da função.

**OBSERVAÇÃO:** O estado de parada pode ser tanto aceitação quanto rejeição. O importante é o conteúdo final da fita, e não o metadado de onde parou.

### Exemplo 5.5: Verificar se o número $x$ é ímpar

Isso é o predicado $ÍMPAR(x)$. É equivalente a dizer se a quantidade de caracteres na fita de entrada é ímpar ou par. A ideia é computar o resto de $x/2$. A fita retorna apenas 1 caractere se $x$ for ímpar, e retorna a fita branca caso contrário.

Seja $\Sigma = \{1\}$ e $IMPAR(x)$ o predicado computado pela seguinte MT:

- $\delta(q_0, \Delta) = (q_1, \Delta, R)$

- $\delta(q_1, 1) = (q_1, 1, R)$
- $\delta(q_1, \Delta) = (q_2, \Delta, L)$

- $\delta(q_2, 1) = (q_3, \Delta, L)$
- $\delta(q_2, \Delta) = (h_a, \Delta, S)$

- $\delta(q_3, 1) = (q_2, \Delta, L)$
- $\delta(q_3, \Delta) = (q_4, \Delta, R)$

- $\delta(q_4, \Delta) = (h_a, 1, L)$

Veja que para ambos os casos ele para no estado de aceitação, importando apenas o conteúdo da fita.

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

Para todas as transições que mandavam para o estado de aceitação, eu converto o estado de aceitação em (1) por uma checagem em (2) para saber se a fita está com 1 caractere ou mais ao final da execução ou a fita está totalmente branca. Se estiver com pelo menos 1 caractere, manda para aceitação. Se a fita estiver branca, manda para rejeição, assim consigo retornar uma informação (metadado) útil se $x$ está ou não em $L$.

## Definição 5.12: Combinando Máquinas de Turing

Sejam $M_1 = (Q_1, \Sigma, \Gamma, q_0, \delta_1)$ e $M_2  = (Q_2, \Sigma, \Gamma, q_0', \delta_2)$ duas MTs tal que $Q_1 \cap Q_2 = \emptyset$. Constrói-se a MT $M = (Q, \Sigma, \Gamma, q_0, \delta)$ resultante da combinação de $M_1$ com $M_2$, em que

- $Q = Q_1 \cup Q_2$;
- $\Sigma$ é o mesmo alfabeto por uma questão inicial didática, mas pode ser diferente;
- $q_0$ de $M$ é o mesmo $q_0$ de $M_1$;
- As transições de $\delta$ são todas as transições de $M_2$ e todas as transições de $M_1$ que não vão para $h_a$.

Para cada transição em $M$,

- $\delta(p,X) = (h_a, Y, D)$

onde $D$ é a direção que o cabeçote se move, vamos incluir em $M$ a transição

- $\delta(p,X) = (q_0', Y, D)$

Resumindo, para combinar 2 MTs, eu tiro o $h_a$ de $M_1$, e coloco o $q_0'$ (estado inicial) de $M_2$. Por isso é importante, no $h_a$ de uma máquina qualquer, que o cabeçote esteja no início da fita, para que a combinação possa ser possível, assim conseguimos utilizar macros, que é basicamente uma combinação.

### Notação para chamar uma MT

Para indicar que a MT $M_1M_2$ é composta pelas MTs $M_1$ e $M_2$, mas sem exibir os estados:

- $M_1 \rightarrow M_2$

Já para representar a transição de um estado qualquer $p$ para uma MT $M$ ao ler um símbolo atual (por exemplo, $a$), utiliza essas três notações, que são equivalentes:

- $\delta(p, a) = M$
- $\delta(p, a) = (M, a, S)$
- $\delta(p, a) = (q, a, S)$, onde $q$ já é um estado qualquer de $M$.

Ja essa notação significa que eu executo a MT $M_1$. Se $M_1$ para em $h_a$ com símbolo corrente $a$, então execute a MT $M_2$. As três formas equivalentes de mostrar a transição entre duas MTs é:

- $\delta(M_1, a) = M_2$
- $\delta(M_1, \sigma) = (p, a, D) \rightarrow \delta(p, a) = (M_2, a)$
- $\delta(M_1, \sigma) = (p, a, D) \rightarrow \delta(p, a) = (q, a, S)$, onde $q$ já é um estado qualquer de $M_2$.

### Exemplo 5.6

Se eu tenho

- $\delta(M_1, a) = M_2$
- $\delta(M_1, b) = M_3$
- $\delta(M_1, \Delta) = M_4$

Com estado inicial em $M_1$, lê-se: Se estou em $M_1$ e parei no $a$, $b$ ou $\Delta$, então eu inicio $M_2$, $M_3$ ou $M_4$, respectivamente.

## Definição 5.13: Macros

Macros são uma forma de simplificar repetição de operações, assim como na linguagem $\mathscr{L}$ de programação.

Para usar macros com segurança, é preciso se perguntar:

- Qual a configuração inicial esperada pela macro?
- Qual a configuração de saída é produzida pela macro?

### Next-Blank (NB)

Se eu tiver

```
Δ a [q0 b] b a Δ b b a Δ ...
```

Eu qeuro ler o próximo símbolo branco:

```
Δ a b b a [ha Δ] b b a Δ ...
```

A MT que computa isso é:

- $\delta(q, s_i) = (q', s_i, R)$
- $\delta(q, \Delta) = (q', \Delta, R)$

- $\delta(q', s_i) = (q', s_i, R)$
- $\delta(q', \Delta) = (q', \Delta, S)$

### Previous-Blank (PB)

Lê o próximo símbolo branco para trás.

- $\delta(q, s_i) = (q', s_i, L)$
- $\delta(q, \Delta) = (q', \Delta, L)$

- $\delta(q', s_i) = (q', s_i, L)$
- $\delta(q', \Delta) = (q', \Delta, S)$

Tanto em NB quanto em PB param em $\Delta$ e estarão preparadas para a próxima ação para a próxima MT que se ligar com $h_a$ dessas macros.

### Copy

Se eu tiver

```
[q Δ] x Δ ...
``` 
 
eu faço uma cópia do bloco $x$ para frente, resultando em

```
[q Δ] x Δ x Δ ...
```

**OBSERVAÇÃO:** Esse macro espera 1 argumento apenas. Se fosse $[q \Delta]x\Delta x\Delta \ldots$ como entrada do macro, ele não vai agir conforme esperado. Agora se eu tiver $\Delta x[q\Delta] x\Delta\ldots$, ele vai funcionar tranquilamente, afinal o cabeçote está adiantado, ele vai ler o primeiro parâmetro que vier na fita e o que vem depois é tudo branco. É como se dali para frente tivesse somente 1 argumento, mesmo que na fita toda aparentemente tenha dois. Tudo depende da posição do cabeçote.

-$\delta(q_0, \Delta) = (q_1, \Delta, R)$

-$\delta(q_1, a) = (q_2, A, R)$
-$\delta(q_1, b) = (q_6, B, R)$
-$\delta(q_1, \Delta) = (q_8, \Delta, L)$

-$\delta(q_2, a) = (q_2, a, R)$
-$\delta(q_2, b) = (q_2, b, R)$
-$\delta(q_2, \Delta) = (q_3, \Delta, R)$

-$\delta(q_3, a) = (q_3, a, R)$
-$\delta(q_3, b) = (q_3, b, R)$
-$\delta(q_3, \Delta) = (q_4, a, L)$

-$\delta(q_4, a) = (q_3, a, L)$
-$\delta(q_4, b) = (q_3, b, L)$
-$\delta(q_4, \Delta) = (q_5, \Delta, L)$

-$\delta(q_5, a) = (q_3, a, L)$
-$\delta(q_5, b) = (q_3, b, L)$
-$\delta(q_5, A) = (q_1, A, R)$
-$\delta(q_5, B) = (q_1, B, R)$

-$\delta(q_6, a) = (q_6, B, R)$
-$\delta(q_6, b) = (q_6, B, R)$
-$\delta(q_6, \Delta) = (q_7, \Delta, R)$

-$\delta(q_7, a) = (q_7, a, R)$
-$\delta(q_7, b) = (q_7, b, R)$
-$\delta(q_7, \Delta) = (q_4, b, L)$

-$\delta(q_8, A) = (q_8, a, L)$
-$\delta(q_8, B) = (q_8, b, L)$
-$\delta(q_8, \Delta) = (h_a, \Delta, S)$

### Delete

Apaga o caractere atual. Veja que ele espera $a, b, \Delta \in \Gamma$. ALém disso, dá um shift de toda a fita na parte direita do caractere que foi apagado para a esquerda.

Exemplo:

```
Δ a b [q a] a b b Δ ...
``` 

Ao apagar, fica

```
Δ a b [q a] b b Δ Δ ...
```

A macro termina com o cabeçote posicionado para o próximo caractere.

### $Insert(\sigma)$

Insere o caractere $\sigma$ na string.

```
Δ w1 [q σ] w2 Δ ...
```

### Equal

Se eu tiver uma fita

$$\Delta x_1 \Delta x_2 \Delta \ldots \rightarrow h_a \iff x_1 = x_2$$

### Erase

$$\Delta w_1\# w_2 \Delta \ldots \rightarrow \Delta\Delta\Delta\Delta\ldots$$

Onde $\#$ é um caractere aleatório apenas para representar que absolutamente tudo será apagado.

### Exemplo 5.7: Checar se $w = w^R$

- $COPY \rightarrow NB \rightarrow R \rightarrow PB \rightarrow EQUAL$

Essa máquina checa se $w = w^R$, ou seja, checa se $w$ é um palíndromo. A máquina $R$ reverte a palavra.

## Definição 5.14: Máquina de Turing com Múltiplas Fitas

Uma MT com duas fitas é uma tupla $\delta : Q \times(\Gamma \cup \{\Delta\})^2 \longrightarrow (Q \cup \{h_a, h_r\}) \times (\Gamma \cup \{\Delta\})^2 \cup (\{R, L, S\}^2)$.

O que muda aqui é o $\delta$.

Exemplo, se eu tenho em uma fita $delta(q, \sigma) = (q', \sigma', L)$, em duas fitas eu tenho algo mais abrangente, um exemplo é $\delta(q, (a,b)) = (q', (b, \Delta), (R, L))$.

Basicamente um estado rastreia ações nas duas fitas.

### Estado Inicial

Se eu tenho a 1° fita $[q_0\Delta] x_1 \Delta x_2 \Delta \ldots$ e a segunda fita $[q_0\Delta] \Delta \ldots$, a configuração inicial é $(q_0, \Delta x, \Delta)$.

### Exemplo 5.8: Decidir $L = \{ww \mid w \in \{a, b\}^*\}$ utilizando duas fitas

- $\delta(q_0, (\Delta, \Delta)) = (q_1, (\Delta, \Delta), (R, R))$

- $\delta(q_1, (a, \Delta)) = (q_2, (a, \Delta), (R, S))$
- $\delta(q_1, (b, \Delta)) = (q_2, (b, \Delta), (R, S))$
- $\delta(q_1, (\Delta, \Delta)) = (q_3, (\Delta, \Delta), (L, L))$

- $\delta(q_2, (a, \Delta)) = (q_2, (a, X), (R, R))$
- $\delta(q_2, (b, \Delta)) = (q_2, (b, X), (R, R))$

- $\delta(q_3, (a, \Delta)) = (q_4, (a, \Delta), (L, S))$
- $\delta(q_3, (b, \Delta)) = (q_4, (b, \Delta), (L, S))$
- $\delta(q_3, (a, X)) = (q_3, (\Delta, a), (L, L))$
- $\delta(q_3, (b, X)) = (q_3, (\Delta, b), (L, L))$
- $\delta(q_3, (\Delta, \Delta)) = (h_a, (\Delta, \Delta), (S, S))$

- $\delta(q_4, (a, \Delta)) = (q_4, (a, \Delta), (L, S))$
- $\delta(q_4, (b, \Delta)) = (q_4, (b, \Delta), (L, S))$
- $\delta(q_4, (\Delta, \Delta)) = (q_5, (\Delta, \Delta), (R, R))$

- $\delta(q_5, (a, a)) = (q_5, (a, a), (R, R))$
- $\delta(q_5, (b, b)) = (q_5, (b, b), (R, R))$
- $\delta(q_5, (\Delta, \Delta)) = (h_a, (\Delta, \Delta), (S, S))$

## Definição 5.15: Máquina de Turing Não-Determinística

Não exite algoritmos não determinísticos. Porém, podemos construir MTs que simulam o não-determinismo. Isso é semelhante com o que fizemos com a função STEP, na segunda parte do curso. Basicamente são threads paralelas que escolhem por conta própria decidir caminhos de forma inteligente.

O não determinismo é útil para testar. Operações do tipo concatenação não é útil, por exemplo, pois a concatenação não faz testes.

### Exemplo 5.9: Decidir $L = \{ww \mid w \in \{a, b\}^*\}$ com MT não determinística

O não determinismo ocorre em $q_1$.

- $\delta(q_0, \Delta) = (q_0, \Delta, R)$

- $\delta(q_1, a) = (q_1, a, R)$
- $\delta(q_1, b) = (q_1, b, R)$
- $\delta(q_1, a) = (q_2, A, L)$
- $\delta(q_1, b) = (q_2, B, L)$

- $\delta(q_2, a) = (q_2, a, L)$
- $\delta(q_2, b) = (q_2, b, L)$
- $\delta(q_2, \Delta) = (q_3, \Delta, R)$

- $\delta(q_3, a) = (q_4, \Delta, R)$
- $\delta(q_3, b) = (q_7, \Delta, R)$

- $\delta(q_4, a) = (q_4, a, R)$
- $\delta(q_4, b) = (q_4, b, R)$
- $\delta(q_4, X) = (q_4, X, R)$
- $\delta(q_4, A) = (q_5, X, R)$

- $\delta(q_5, a) = (q_6, A, L)$
- $\delta(q_5, b) = (q_6, B, L)$

- $\delta(q_6, a) = (q_6, a, L)$
- $\delta(q_6, b) = (q_6, b, L)$
- $\delta(q_6, X) = (q_6, X, L)$
- $\delta(q_6, \Delta) = (q_6, \Delta, R)$

- $\delta(q_7, a) = (q_7, a, R)$
- $\delta(q_7, b) = (q_7, b, R)$
- $\delta(q_7, X) = (q_7, X, R)$
- $\delta(q_7, A) = (q_8, X, R)$

- $\delta(q_8, a) = (q_6, A, L)$
- $\delta(q_8, b) = (q_6, B, L)$
- $\delta(q_8, \Delta) = (q_9, \Delta, L)$

- $\delta(q_9, X) = (q_9, X, L)$
- $\delta(q_9, \Delta) = (h_a, \Delta, S)$

### Exemplo 5.10: Gerar um número aleatório de 1's na fita

- $\delta(q_0, \Delta) = (q_1, \Delta, R)$

- $\delta(q_1, \Delta) = (q_1, 1, R)$
- $\delta(q_1, \Delta) = (q_2, \Delta, L)$

- $\delta(q_2, 1) = (q_2, 1, L)$
- $\delta(q_2, \Delta) = (h_a, \Delta, S)$

### Exemplo 5.11: Gerar um número aleatório de 1's na fita, mas $\ge 2$ na fita é garantido ($G_2$)

- $\delta(q_0, \Delta) = (q_1, \Delta, R)$
- $\delta(q_1, \Delta) = (q_2, 1, R)$
- $\delta(q_2, \Delta) = (q_3, 1, R)$

- $\delta(q_3, \Delta) = (q_2, 1, R)$
- $\delta(q_3, \Delta) = (q_2, \Delta, L)$

- $\delta(q_4, 1) = (q_4, 1, L)$
- $\delta(q_4, \Delta) = (h_a, \Delta, S)$

### Exemplo 5.11: Verifica se o número na fita não é primo

-$NB \rightarrow G_2 \rightarrow NB \rightarrow G_2 \rightarrow PB \rightarrow MULT \rightarrow PB \rightarrow EQUAL$

A $MULT$ é uma multiplicação $\Delta w_1 \Delta w_2 \Delta \ldots \rightarrow \Delta w_1 \cdot w_2 \Delta \ldots$.