# 🔧 Diagramas de Blocos: Conceito e Aplicações

## 📌 Definição
Diagramas de Blocos (DBs) são **representações gráficas** que mostram **como os elementos de um sistema interagem entre si**, com foco nas **relações funcionais** entre as variáveis de entrada e saída de cada componente.

Cada **bloco** representa uma **operação matemática** (geralmente expressa por uma função de transferência no domínio de Laplace, como \( \hat{g}(s) \)) que transforma o sinal de entrada \( \hat{u}(s) \) em uma saída \( \hat{y}(s) \):

$$
\hat{y}(s) = \hat{g}(s) \cdot \hat{u}(s)
$$

> ⚠️ Importante: Assim como as funções de transferência, **os diagramas de blocos descrevem o comportamento dinâmico** do sistema, **mas não revelam sua estrutura física**. Diferentes sistemas físicos podem ter o mesmo DB.

---

# 📘 Componentes de um Diagrama de Blocos

## 🔹 Blocos
Representam funções de transferência \( \hat{g}(s) \), ou outras operações matemáticas.

## 🔹 Pontos de Soma (Σ)
Permitem a combinação de sinais (adição/subtração):
$$
\hat{w}(s) = \hat{u}(s) + \hat{v}(s) - \hat{z}(s)
$$

## 🔹 Pontos de Ramificação
Usados quando o mesmo sinal precisa ser enviado para múltiplos blocos.

---

# 🔄 Sistemas em Malha Fechada

## ▶ Realimentação Unitária
Sistema com um bloco de planta \( \hat{g}(s) \) realimentado pela própria saída:

$$
\varepsilon(s) = \hat{r}(s) - \hat{y}(s) \quad \text{e} \quad \hat{y}(s) = \hat{g}(s)\varepsilon(s)
$$

Isolando \( \hat{y}(s) \):
$$
\frac{\hat{y}(s)}{\hat{r}(s)} = \frac{\hat{g}(s)}{1 + \hat{g}(s)} \tag{3.1}
$$

---

# 🔁 Sistema com Sensor de Realimentação \( \hat{h}(s) \)

## 📌 Função de Transferência de Malha Aberta (FTMA):
$$
FTMA(s) = \hat{g}(s)\hat{h}(s) \tag{3.2}
$$

## 📌 Função de Transferência Feedforward (FTFF):
$$
FTFF(s) = \hat{g}(s) \tag{3.3}
$$

## 📌 Função de Transferência da Malha Fechada:
$$
\frac{\hat{y}(s)}{\hat{r}(s)} = \frac{\hat{g}(s)}{1 + \hat{g}(s)\hat{h}(s)} \tag{3.4}
$$

---

# 🌪️ Sistemas com Perturbação \( \hat{d}(s) \)

## ▶ Quando \( \hat{d}(s) \neq 0 \) e \( \hat{r}(s) = 0 \):
$$
\frac{\hat{y}(s)}{\hat{d}(s)} = \frac{\hat{g}(s)}{1 + \hat{c}(s)\hat{g}(s)\hat{h}(s)} \tag{3.6}
$$

## ▶ Quando \( \hat{d}(s) = 0 \) e \( \hat{r}(s) \neq 0 \):
$$
\frac{\hat{y}(s)}{\hat{r}(s)} = \frac{\hat{c}(s)\hat{g}(s)}{1 + \hat{c}(s)\hat{g}(s)\hat{h}(s)} \tag{3.5}
$$

## 🔧 Resultado geral:
$$
\hat{y}(s) = \left[ \frac{\hat{c}(s)\hat{g}(s)}{1 + \hat{c}(s)\hat{g}(s)\hat{h}(s)} \quad \frac{\hat{g}(s)}{1 + \hat{c}(s)\hat{g}(s)\hat{h}(s)} \right]
\begin{bmatrix}
\hat{r}(s) \\
\hat{d}(s)
\end{bmatrix} \tag{3.7}
$$

> ✅ Se \( |\hat{c}(s)\hat{g}(s)\hat{h}(s)| \gg 1 \), então o sistema **rejeita a perturbação** e segue a referência: \( \hat{y}(s) \approx \frac{\hat{r}(s)}{\hat{h}(s)} \)

---

# 🧩 Operações com Blocos

## 1. Série:
Blocos \( \hat{g}_1(s) \) e \( \hat{g}_2(s) \) em série:
$$
\hat{y}(s) = \hat{g}_1(s)\hat{g}_2(s)\hat{u}(s) \tag{3.8}
$$

## 2. Paralelo:
Somas de blocos aplicados ao mesmo sinal:
$$
\hat{y}(s) = [\hat{g}_1(s) + \hat{g}_2(s)] \cdot \hat{u}(s)
$$

## 3. Realimentação:
Redução da malha:
$$
\frac{\hat{g}(s)}{1 + \hat{g}(s)\hat{h}(s)}
$$

---

# 🧠 Dicas para Simplificação

- Só associe blocos em série se **não houver influência mútua**.
- Mantenha:
  - o **produto das FTs no caminho direto**;
  - o **produto das FTs no laço de realimentação**.

> Exemplo clássico: sistemas RC em série (com cargas acopladas) **não podem ser diretamente representados por dois blocos em série**, pois o segundo afeta a resposta do primeiro.