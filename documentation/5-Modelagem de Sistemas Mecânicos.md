# 📘 Modelagem de Sistemas Mecânicos

A modelagem de sistemas mecânicos segue o princípio de associar forças às posições ou movimentos dos corpos. Essa abordagem está diretamente relacionada à Segunda Lei de Newton:

## ⚙️ 1. **Massa (m) — Elemento Inercial**

### 💡 Intuição:
A massa resiste à mudança de velocidade. Ou seja, para mudar sua velocidade (aceleração), é preciso aplicar força.

### 🧠 Fórmula:
$$
F = m\ddot{x}
$$
- Onde:
  - $ F $: Força resultante aplicada
  - $ m $: Massa do corpo
  - $ \ddot{x} $: Aceleração do corpo

### 📦 Papel na modelagem:
- **Elemento acumulador de energia** (cinética): não dissipa nem gera energia.
- Responsável pelos **termos com aceleração** nas equações diferenciais.

---

## 🪗 2. **Mola Linear (k) — Elemento Restaurador**
### 💡 Intuição:
A mola tenta **retornar à sua posição de equilíbrio**. Quanto mais você comprime ou estica, maior a força que ela faz para retornar.

### 🧠 Fórmula:
$$
F = kx
$$
- Onde:
  - $ F $: Força restauradora
  - $ k $: Constante de rigidez da mola
  - $ x $: Deslocamento em relação à posição de repouso

### 📦 Papel na modelagem:
- Armazena **energia potencial elástica**
- Gera termos proporcionais ao **deslocamento** $ x $

---

## 💧 3. **Amortecedor Viscoso (b) — Elemento Dissipativo**
### 💡 Intuição:
Resiste ao movimento, como uma seringa com fluido. Quanto mais rápido se move, mais difícil é continuar o movimento.

### 🧠 Fórmula:
$$
F = b\dot{x}
$$
- Onde:
  - $ b $: Constante de amortecimento
  - $ \dot{x} $: Velocidade do corpo

### 📦 Papel na modelagem:
- **Dissipa energia** (em forma de calor)
- Gera **termos proporcionais à velocidade**
- Essencial para **estabilizar sistemas** e evitar oscilações infinitas

---

## 🧰 Combinação: Sistema Massa-Mola-Amortecedor

### 🧠 Equação:
$$
m\ddot{x} + b\dot{x} + kx = F(t)
$$

- É uma **equação diferencial de 2ª ordem**
- A resposta do sistema depende do tipo de entrada $ F(t) $: impulso, degrau, seno, etc.
- Pode ser resolvida analiticamente ou transformada em outros domínios (Laplace, Estado)

---

## 🚗 Exemplo: Suspensão Automotiva — Aplicação Prática

A suspensão automotiva pode ser modelada considerando as forças atuantes no sistema e aplicando a Segunda Lei de Newton. O sistema é composto por uma massa ($m$), uma mola ($k$), e um amortecedor ($b$). A entrada é o deslocamento do terreno $u(t)$, e a saída é o deslocamento da carroceria $y(t)$.

<p align="center">
  <img src="assets/section5/exemplo_suspensao_automotiva.png" alt="Exemplo de Suspensão Automotiva" />
</p>


#### 🧠 Forças no sistema:
- **Força da mola**: $F_{\text{mola}} = k(u - y)$
- **Força do amortecedor**: $F_{\text{amort}} = b(\dot{u} - \dot{y})$

#### ⚙️ Equação de movimento:
Aplicando a Segunda Lei de Newton:
$$
F_{\text{mola}} + F_{\text{amort}} = m\ddot{y}
$$
Substituindo as forças:
$$
k(u - y) + b(\dot{u} - \dot{y}) = m\ddot{y}
$$
Reorganizando:
$$
\ddot{y} + \frac{b}{m}\dot{y} + \frac{k}{m}y = \frac{b}{m}\dot{u} + \frac{k}{m}u
$$

#### 🛠️ Transformada de Laplace:
No domínio de Laplace, assumindo condições iniciais nulas:
$$
Y(s)\left(s^2 + \frac{b}{m}s + \frac{k}{m}\right) = U(s)\left(\frac{b}{m}s + \frac{k}{m}\right)
$$
A função de transferência do sistema é:
$$
G(s) = \frac{Y(s)}{U(s)} = \frac{\frac{b}{m}s + \frac{k}{m}}{s^2 + \frac{b}{m}s + \frac{k}{m}}
$$

#### 🧮 Representação no espaço de estados:
Definindo o vetor de estado $x = \begin{bmatrix} y \\ \dot{y} \end{bmatrix}$:
$$
\dot{x} =
\begin{bmatrix}
0 & 1 \\
-\frac{k}{m} & -\frac{b}{m}
\end{bmatrix}
x +
\begin{bmatrix}
0 \\
\frac{k}{m}
\end{bmatrix}
u
$$
$$
y = \begin{bmatrix} 1 & 0 \end{bmatrix} x
$$

#### 🔎 Observações:
- O sistema é de **segunda ordem** e pode ser analisado em termos de amortecimento e frequência natural.
- A resposta depende dos parâmetros $m$, $b$, e $k$, que determinam o comportamento do carro ao passar por irregularidades no terreno.

---

## 🌀 Sistemas Rotacionais — Analogias

| Linear       | Rotacional    |
|--------------|----------------|
| $ x $      | $ \theta $   |
| $ F $      | $ T $        |
| $ m $      | $ J $        |
| $ b $      | $ b_\theta $ |
| $ k $      | $ k_\theta $ |

### Mola rotacional:
$$
T = k\theta
$$

### Amortecedor rotacional:
$$
T = b\dot{\theta}
$$

⚠️ Importante manter a coerência de unidades (N·m, rad/s, etc.)

---

## ⛓️ Pêndulo Torcional Acoplado

Um sistema com dois discos interligados por uma mola:

$$
J_i\ddot{\theta}_i + b_i\dot{\theta}_i + (k_i + kr_i^2)\theta_i - r_ir_jk\theta_j = 0
$$

Esse modelo mostra como o **movimento de um disco** afeta o outro — **acoplamento mecânico**.

---

## 🧍‍♂️ Pêndulo Invertido (Linearizado)

Sistema clássico em controle:
- Um carrinho move uma haste vertical com um pêndulo
- Não é linear (envolve $ \sin(\theta) $), mas pode ser **linearizado para controle**

### Equações:
$$
\begin{cases}
(M + m)\ddot{x} + ml\ddot{\theta} = u \\
(J + ml^2)\ddot{\theta} + ml\ddot{x} - mgl\theta = 0
\end{cases}
$$

- Requer técnicas como **realimentação de estados, controle ótimo, LQR, etc.**