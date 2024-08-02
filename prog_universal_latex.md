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