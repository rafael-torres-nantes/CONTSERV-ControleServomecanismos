# 🎯 **O que é o Espaço de Estado?**

O **Espaço de Estado** é uma abordagem moderna para a modelagem e análise de sistemas dinâmicos, usada principalmente para sistemas que variam no tempo (em tempo contínuo ou discreto) e, especialmente, sistemas de múltiplas entradas e saídas (MIMO). Diferente da abordagem clássica baseada em funções de transferência (muito focada na resposta em frequência), o modelo de espaço de estado descreve o **comportamento interno** do sistema por meio de **variáveis de estado**.

---

# 📘 **Definições Importantes (segundo Ogata):**

## 🔹 Estado
É o **conjunto mínimo de variáveis** (chamadas de **variáveis de estado**) que, junto com as entradas futuras do sistema, determina **completamente** o comportamento do sistema para $ t \geq t_0 $.

## 🔹 Variáveis de Estado
São as variáveis escolhidas para representar o estado do sistema. Costumam ser quantidades físicas como velocidade, posição, corrente, etc.

## 🔹 Espaço de Estado
É o espaço $ \mathbb{R}^n $, onde cada eixo representa uma variável de estado. O vetor de estado $ \mathbf{x}(t) \in \mathbb{R}^n $ define a posição do sistema nesse espaço a cada instante.

---

# 🧮 **Equações do Espaço de Estado (Forma Geral)**

A forma padrão para sistemas lineares invariantes no tempo (SLIT-C) é:

$$
\begin{aligned}
\dot{\mathbf{x}}(t) &= A \mathbf{x}(t) + B \mathbf{u}(t) \\
\mathbf{y}(t) &= C \mathbf{x}(t) + D \mathbf{u}(t)
\end{aligned}
$$

## Onde:
- $ \mathbf{x}(t) \in \mathbb{R}^n $: vetor de estado  
- $ \mathbf{u}(t) \in \mathbb{R}^m $: vetor de entrada (controle)  
- $ \mathbf{y}(t) \in \mathbb{R}^p $: vetor de saída  
- $ A \in \mathbb{R}^{n \times n} $: matriz de dinâmica do sistema  
- $ B \in \mathbb{R}^{n \times m} $: matriz de entrada  
- $ C \in \mathbb{R}^{p \times n} $: matriz de saída  
- $ D \in \mathbb{R}^{p \times m} $: matriz de transmissão direta (feedthrough)

---

# 🧰 **Exemplo Clássico: Sistema Massa-Mola-Amortecedor**


Esse é um modelo físico muito comum em engenharia e controle de sistemas. Consiste em uma **massa** $ m $ ligada a uma **mola** com constante elástica $ k $, e a um **amortecedor** com constante de amortecimento $ b $. O sistema está sujeito a uma **força externa de entrada** $ u(t) $.

<p align="center">
    <img src="assets/section4/sistema_massa_mola_amortecedor.png" alt="Sistema Massa-Mola-Amortecedor">
</p>

### 🔁 **Modelagem Física (Equação Diferencial)**

Pela **segunda lei de Newton**, a soma das forças agindo sobre a massa é igual à massa vezes a aceleração:

$$
m\ddot{y}(t) = -ky(t) - b\dot{y}(t) + u(t)
$$

Organizando os termos:

$$
m\ddot{y} + b\dot{y} + ky = u(t)
$$

Onde:
- $\ddot{y} $: aceleração
- $ \dot{y} $: velocidade
- $ y $: deslocamento
- $ u(t) $: força externa aplicada

---

### 🔁 **Escolhendo as Variáveis de Estado**

Queremos reescrever esse sistema como um sistema de **equações de primeira ordem**, que é a forma usada em sistemas de controle e análise moderna.

Definimos:
$$
x_1 = y \quad \text{(posição)} \\
x_2 = \dot{y} \quad \text{(velocidade)}
$$

Dessa forma:
- $ \dot{x}_1 = x_2 $
- $ \dot{x}_2 = \ddot{y} = \frac{1}{m}(u - b\dot{y} - ky) = \frac{1}{m}(u - bx_2 - kx_1) $

---

### 🔢 **Sistema em Forma de Estado**

Agora escrevemos o sistema em **forma de estado** (vetorial/matricial):

$$
\dot{x} = 
\begin{bmatrix}
\dot{x}_1 \\
\dot{x}_2
\end{bmatrix}
=
\begin{bmatrix}
0 & 1 \\
-\frac{k}{m} & -\frac{b}{m}
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2
\end{bmatrix}
+
\begin{bmatrix}
0 \\
\frac{1}{m}
\end{bmatrix}
u
$$

E a saída (posição do bloco, $ y = x_1 $) é:

$$
y =
\begin{bmatrix}
1 & 0
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2
\end{bmatrix}
$$

---

### 📌 **Resumo das Forças no Sistema**

- **Força da mola** (lei de Hooke):  
  $$
  F_\text{mola} = -k y
  $$  
  Quanto mais a mola for esticada/comprimida, maior a força restauradora.

- **Força do amortecedor** (atrito viscoso):  
  $$
  F_\text{amortecedor} = -b \dot{y}
  $$  
  Essa força depende da **velocidade**: quanto mais rápido o movimento, maior a resistência.

- **Força externa** aplicada:  
  $$
  u(t)
  $$

---

# 🔄 **Ligação com a Função de Transferência**

Se aplicarmos a **Transformada de Laplace** nas equações do espaço de estado com **condições iniciais nulas**, podemos obter a **função de transferência**.

## 🧮 **Equações do Espaço de Estado**
As equações do espaço de estado de um sistema dinâmico linear podem ser escritas como:

1. **Equação de estado**:
   $$ \dot{x}(t) = A x(t) + B u(t) $$

2. **Equação de saída**:
   $$ y(t) = C x(t) + D u(t) $$

Aqui:
- $ x(t) $: vetor de estado
- $ u(t) $: entrada do sistema
- $ y(t) $: saída do sistema
- $ A, B, C, D $: matrizes que descrevem o sistema

## 🔄 **Aplicando a Transformada de Laplace**
Ao aplicar a **Transformada de Laplace** (com condições iniciais nulas), obtemos:

1. Da equação de estado:
   $$ s \hat{x}(s) = A \hat{x}(s) + B \hat{u}(s) $$

   Rearranjando para resolver $ \hat{x}(s) $:
   $$ \hat{x}(s) = (sI - A)^{-1} B \hat{u}(s) $$

   Aqui, $ (sI - A)^{-1} $ é chamada de **resolvante** da matriz $ A $.

2. Substituímos $ \hat{x}(s) $ na equação de saída:
   $$ \hat{y}(s) = C \hat{x}(s) + D \hat{u}(s) $$

   Substituindo $ \hat{x}(s) $:
   $$ \hat{y}(s) = C (sI - A)^{-1} B \hat{u}(s) + D \hat{u}(s) $$

## 📊 **Definição da Função de Transferência**
A função de transferência $ G(s) $ é definida como a relação entre a saída $ \hat{y}(s) $ e a entrada $ \hat{u}(s) $ no domínio de Laplace, assumindo condições iniciais nulas:

$$
G(s) = \frac{\hat{y}(s)}{\hat{u}(s)} = C (sI - A)^{-1} B + D
$$

## 🔎 **Observações Importantes**
- Os **pólos** da função de transferência $ G(s) $ são os **autovalores da matriz $ A $**, pois são os valores de $ s $ que tornam $ (sI - A) $ singular (não invertível).
- Essa fórmula é válida tanto para sistemas **SISO** (Single Input, Single Output) quanto para sistemas **MIMO** (Multiple Input, Multiple Output).

---

# ⚙️ **Vantagens da Representação em Espaço de Estado:**

1. **Modela sistemas MIMO naturalmente**.
2. É aplicável a sistemas **não lineares e variantes no tempo**.
3. Permite fácil análise de **controlabilidade** e **observabilidade**.
4. Permite o uso de técnicas modernas de projeto como **realimentação de estados** e **observadores de estado**.

---

# 📐 **Diagrama de Blocos do Espaço de Estado**

O sistema pode ser representado com um diagrama de blocos com as interações das matrizes $ A, B, C, D $, mostrando como as variáveis de estado são atualizadas e como influenciam as saídas.

Claro, Rafael! Aqui está o exemplo do sistema representado no espaço de estado adicionado ao seu README, seguindo o estilo que você já estava utilizando e mantendo a estrutura didática:

---

# 📊 **Exemplo: Espaço de Estado a partir de Diagrama de Blocos**

Vamos obter uma representação em **espaço de estado** para o sistema definido pelo seguinte diagrama de blocos:

<p align="center">
  <img src="assets/section4/exemplo_espaco_estado.png" alt="Diagrama de Blocos - Compensador + Planta + Sensor" />
</p>

Este sistema possui três blocos em série:

- **Compensador**: $ \displaystyle \frac{1}{s} $

- **Planta**: $ \displaystyle \frac{1}{s + a} $

- **Sensor**: $ \displaystyle \frac{1}{s + b} $

A entrada do sistema é $ \hat{r}(s) $ e a saída $ \hat{y}(s) $.  
O sinal de realimentação é negativo, típico de sistemas com **controle de realimentação**.

---

## 🧠 **Escolha das Variáveis de Estado**

Escolhemos as **saídas intermediárias dos blocos** como variáveis de estado:

- $ x_1(s) $: saída do primeiro bloco $ \displaystyle \frac{1}{s} $

- $ x_2(s) $: saída do segundo bloco $ \displaystyle \frac{1}{s + a} $

- $ x_3(s) $: saída do terceiro bloco $ \displaystyle \frac{1}{s + b} $


<p align="center">
  <img src="assets/section4/exemplo_espaco_estado_v2.png" alt="Diagrama de Blocos - Compensador + Planta + Sensor" />
</p>

Com isso:

$$
\hat{y}(s) = x_2(s)
$$

E temos:

$$
\begin{aligned}
x_1(s) &= \frac{1}{s}[\hat{r}(s) - x_3(s)] \\
x_2(s) &= \frac{1}{s + a} x_1(s) \\
x_3(s) &= \frac{1}{s + b} x_2(s)
\end{aligned}
$$

---

## 🧮 **Derivadas das Variáveis de Estado**

Multiplicando ambos os lados por seus denominadores, obtemos:

$$
\begin{aligned}
s x_1(s) &= \hat{r}(s) - x_3(s) \Rightarrow \dot{x}_1(t) = r(t) - x_3(t) \\
s x_2(s) &= x_1(s) - a x_2(s) \Rightarrow \dot{x}_2(t) = x_1(t) - a x_2(t) \\
s x_3(s) &= x_2(s) - b x_3(s) \Rightarrow \dot{x}_3(t) = x_2(t) - b x_3(t)
\end{aligned}
$$

---

## 🧾 **Sistema em Forma de Estado**

Organizando as equações anteriores no formato matricial:

### 🔹 Vetor de estado:
$$
\mathbf{x}(t) = 
\begin{bmatrix}
x_1(t) \\
x_2(t) \\
x_3(t)
\end{bmatrix}
$$

### 🔹 Equação de Estado:
$$
\dot{\mathbf{x}}(t) =
\begin{bmatrix}
0 & 0 & -1 \\
1 & -a & 0 \\
0 & 1 & -b
\end{bmatrix}
\mathbf{x}(t)
+
\begin{bmatrix}
1 \\
0 \\
0
\end{bmatrix}
r(t)
$$

### 🔹 Equação de Saída:
Como a saída é $ y(t) = x_2(t) $, temos:

$$
y(t) =
\begin{bmatrix}
0 & 1 & 0
\end{bmatrix}
\mathbf{x}(t)
$$

---

## 📌 **Resumo Final**

- **Variáveis de estado**: $ x_1 = \text{saída do 1º bloco} $, $ x_2 = \text{saída do 2º bloco (é também a saída do sistema)} $, $ x_3 = \text{saída do sensor} $
- **Entrada**: $ r(t) $
- **Saída**: $ y(t) = x_2(t) $
- **Modelo de Espaço de Estado**:

$$
\begin{aligned}
\dot{x}(t) &= A x(t) + B r(t) \\
y(t) &= C x(t)
\end{aligned}
$$

Com:

$$
A =
\begin{bmatrix}
0 & 0 & -1 \\
1 & -a & 0 \\
0 & 1 & -b
\end{bmatrix},
\quad
B =
\begin{bmatrix}
1 \\
0 \\
0
\end{bmatrix},
\quad
C =
\begin{bmatrix}
0 & 1 & 0
\end{bmatrix}
$$

---

### 🧩 Observação

> Essa não é a única forma de representar o sistema no espaço de estado! Outras representações podem ser obtidas escolhendo diferentes variáveis de estado. A flexibilidade na escolha das variáveis de estado é uma característica poderosa dessa abordagem.

Se quiser, posso montar também o diagrama de blocos com os estados marcados ou criar outros exemplos alternativos. Deseja isso?