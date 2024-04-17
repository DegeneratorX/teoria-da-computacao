A partir de agora, caso você for demonstrar que uma função é parcialmente computável ou computável através de um programa, você vai utilizar a linguagem $\mathscr{L}$.

### Variáveis

A linguagem $\mathscr{L}$ possui as seguintes variáveis:

- Variáveis de entrada: $X_1$, $X_2$, $X_3$, …

- Variável de saída: $Y$

- Variáveis auxiliares: $Z_1$, $Z_2$, $Z_3$, …

Por convenção, assume-se que o valor inicial das variáveis auxiliares e da variável de saída é 0.

### Rótulos

A linguagem $\mathscr{L}$ possui rótulos:

$A_1$, $B_1$, $C_1$, $E_1$,...

### Instruções e Declarações

As únicas declarações que podem ser feitas em $\mathscr{L}$ são:

- $V \leftarrow V + 1$ // Incrementa 1 ao valor de V

- $V \leftarrow V - 1$ //Decrementa 1 ao valor de V

- $V \leftarrow V$ // O valor de V fica inalterado

- IF $V \neq 0$ GOTO $L$ // Se o valor de $V \neq 0$, executa-se a instrução com rótulo $L$; caso contrário, executa-se a próxima instrução na lista.

onde $V$ é uma variável e $L$ é um label/rótulo.

Uma instrução é uma declaração (instrução não-rotulada) ou $[L]$ seguido por uma declaração (instrução rotulada).

Um programa é uma lista finita de instruções.

### Macros

A linguagem $\mathscr{L}$ pode também possuir macros. Mas irei solicitar se você deve ou não usar macros. Por padrão, NÃO USE.

### Exemplo de programa

Esse programa

$$
\begin{array}{ll}
\text{[} A \text{]}\quad & X \leftarrow X - 1\\
  & Y \leftarrow Y + 1\\
  & \text{IF } X \neq 0 \text{ GOTO } A
\end{array}
$$

computa a função

$$
f(x) = \begin{cases} 
1 & \text{se } x = 0 \\
x & \text{caso contrário} 
\end{cases}
$$

### Exemplo de programa

Esse programa

$$
\begin{array}{ll}
\text{[} A \text{]}\quad  & \text{IF } X \neq 0 \text{ GOTO } B\\
  & Z \leftarrow Z + 1\\
  & \text{IF } Z \neq 0 \text{ GOTO } E\\
\text{[} B \text{]}\quad & X \leftarrow X - 1\\
  & Y \leftarrow Y + 1\\
  & Z \leftarrow Z + 1\\
  & \text{IF } Z \neq 0 \text{ GOTO } A
\end{array}
$$

computa a função $f(x) = x$.

### Sua tarefa

A sua tarefa agora é responder questões envolvendo criação de programas nessa linguagem. Use primeiro o dataset que lhe forneci, junto com essas informações da linguagem. Responda todas as questões usando o seu "Searching my knowledge".