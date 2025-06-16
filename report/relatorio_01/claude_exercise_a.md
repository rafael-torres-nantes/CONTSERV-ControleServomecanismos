# Resolução do Sistema de Pêndulo Torcional

## Questão a) Análise de sobreamortecimento

Nesta questão, precisamos determinar se é possível escolher valores de $k$ e $k_2$ para que o sistema seja sobreamortecido, e calcular os valores correspondentes de $\zeta$ e $\omega_n$.

### Dados do problema:
- $r_1 = 0,1$ m
- $r_2 = 0,15$ m
- $J_2 = 0,1125$ kg·m²
- $b_2 = 0,009$ N·m·s
- $ G(s) = \frac{\Theta_2(s)}{\Theta_1(s)} = $

### Análise do sistema

Para um pêndulo torcional, a equação diferencial que descreve o movimento do segundo cilindro é tipicamente:

$$J_2 \ddot{\theta}_2 + b_2 \dot{\theta}_2 + k(\theta_2 - \theta_1) = 0$$

Onde $k$ representa a rigidez torcional entre os cilindros.

Reorganizando a equação e considerando $\theta_1$ como entrada:

$$J_2 \ddot{\theta}_2 + b_2 \dot{\theta}_2 + k\theta_2 = k\theta_1$$

Aplicando a transformada de Laplace com condições iniciais nulas:

$$J_2 s^2 \Theta_2(s) + b_2 s \Theta_2(s) + k \Theta_2(s) = k \Theta_1(s)$$

A função de transferência é:

$$G(s) = \frac{\Theta_2(s)}{\Theta_1(s)} = \frac{k}{J_2 s^2 + b_2 s + k}$$

Esta é uma função de transferência de segunda ordem na forma:

$$G(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$

Comparando os coeficientes:
- $\omega_n^2 = \frac{k}{J_2}$, portanto $\omega_n = \sqrt{\frac{k}{J_2}}$
- $2\zeta\omega_n = \frac{b_2}{J_2}$, portanto $\zeta = \frac{b_2}{2J_2\omega_n} = \frac{b_2}{2\sqrt{k \cdot J_2}}$

### Condição de sobreamortecimento

Para que o sistema seja sobreamortecido, precisamos $\zeta > 1$. Isso significa:

$$\frac{b_2}{2\sqrt{k \cdot J_2}} > 1$$
$$b_2 > 2\sqrt{k \cdot J_2}$$
$$b_2^2 > 4k \cdot J_2$$
$$\frac{b_2^2}{4J_2} > k$$

Substituindo os valores:

$$\frac{0,009^2}{4 \cdot 0,1125} > k$$
$$\frac{0,000081}{0,45} > k$$
$$0,00018 > k$$

Portanto, para que o sistema seja sobreamortecido, devemos escolher $k < 0,00018$ N·m/rad.

### Seleção de valores para $k$ e $k_2$

Escolhendo $k = 0,00015$ N·m/rad (menor que o limite calculado):

- $\omega_n = \sqrt{\frac{k}{J_2}} = \sqrt{\frac{0,00015}{0,1125}} \approx 0,0365$ rad/s
- $\zeta = \frac{b_2}{2\sqrt{k \cdot J_2}} = \frac{0,009}{2\sqrt{0,00015 \cdot 0,1125}} \approx 1,095 > 1$

Isso confirma que o sistema é sobreamortecido.

Para o valor de $k_2$, assumindo que ele representa um segundo parâmetro de rigidez em uma configuração mais complexa do pêndulo torcional, podemos selecioná-lo como um valor que mantém a condição de sobreamortecimento. Como não há informações explícitas sobre como $k_2$ afeta a dinâmica, vamos considerá-lo como uma fração de $k$.

Escolhendo $k_2 = 0,00010$ N·m/rad (menor que $k$).

### Seleção de valores para $k$ e $k_2$ com $\zeta = 1.2$
Escolhendo $\zeta = 1.2$, podemos determinar os valores de $k$ e $k_2$ a partir das equações fornecidas.

Sabemos que:

$$\zeta = \frac{b_2}{2\sqrt{k \cdot J_2}}$$

Reorganizando para $k$:

$$k = \frac{b_2^2}{4 \cdot J_2 \cdot \zeta^2}$$

Substituindo os valores:

$$k = \frac{0,009^2}{4 \cdot 0,1125 \cdot 1,2^2} = 
\frac{0,000081}{4 \cdot 0,1125 \cdot 1,44} 
\approx \frac{0,000081}{0,648}
\approx 0,000125 Nm/rad$$ 

Agora, calculamos $\omega_n$:

$$\omega_n = \sqrt{\frac{k}{J_2}} = \sqrt{\frac{0,000125}{0,1125}} \approx 0,0333 rad/s$$

Para $k_2$, assumindo que ele é uma fração de $k$, podemos escolher:

$$k_2 = 0,00008 N·m/rad$$

Assim, os valores selecionados são:

- $k = 0,000125$ N·m/rad
- $k_2 = 0,00008$ N·m/rad
- $\zeta = 1.2$
- $\omega_n \approx 0,0333$ rad/s

### Calcular a FT de $G(s)$
### Função de Transferência $G(s)$

A função de transferência $G(s)$ é dada por:

$$G(s) = \frac{\Theta_2(s)}{\Theta_1(s)} = \frac{k}{J_2 s^2 + b_2 s + k}$$

Substituindo os valores calculados para $k$, $J_2$, e $b_2$:

- $k = 0,000125$ N·m/rad
- $J_2 = 0,1125$ kg·m²
- $b_2 = 0,009$ N·m·s

Temos:

$$G(s) = \frac{0,000125}{0,1125 s^2 + 0,009 s + 0,000125}$$

Simplificando:

$$G(s) = \frac{0,000125}{0,1125 s^2 + 0,009 s + 0,000125} = \frac{1}{900 s^2 + 72 s + 1}$$

Portanto, a função de transferência final é:

$$G(s) = \frac{1}{900 s^2 + 72 s + 1}$$