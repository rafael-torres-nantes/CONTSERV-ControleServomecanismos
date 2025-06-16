# Resolução do Sistema de Controle do Pêndulo Torcional

## Questão d) Projeto de controlador proporcional em malha fechada

Nesta questão, precisamos determinar se é possível escolher um ganho proporcional $k_p > 0$ que resulte em um comportamento subamortecido com amortecimento igual a 0,5 em malha fechada.

### Dados do problema:
- $r_1 = 0,1$ m
- $r_2 = 0,15$ m
- $J_2 = 0,1125$ kg·m²
- $b_2 = 0,009$ N·m·s

### Análise do sistema em malha fechada

Primeiro, precisamos entender a função de transferência $\hat{g}(s) = \frac{\hat{\theta}_2(s)}{\hat{\theta}_1(s)}$ do pêndulo torcional.

Para um pêndulo torcional, a função de transferência tipicamente tem a forma:

$$\hat{g}(s) = \frac{\hat{\theta}_2(s)}{\hat{\theta}_1(s)} = \frac{k}{J_2 s^2 + b_2 s + k}$$

Onde $k$ é o coeficiente de rigidez torcional entre os cilindros 1 e 2.

Em malha fechada com um controlador proporcional $k_p$, a função de transferência do sistema se torna:

$$G_{MF}(s) = \frac{k_p \hat{g}(s)}{1 + k_p \hat{g}(s)}$$

Substituindo $\hat{g}(s)$:

$$G_{MF}(s) = \frac{k_p \cdot \frac{k}{J_2 s^2 + b_2 s + k}}{1 + k_p \cdot \frac{k}{J_2 s^2 + b_2 s + k}} = \frac{k_p k}{J_2 s^2 + b_2 s + k + k_p k}$$

### Determinação do coeficiente de amortecimento

Para um sistema de segunda ordem na forma padrão:

$$G(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$

Comparando com nossa função de transferência em malha fechada:

$$\frac{k_p k}{J_2 s^2 + b_2 s + k + k_p k} = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$

Identificamos:
- $\omega_n^2 = \frac{k + k_p k}{J_2}$, portanto $\omega_n = \sqrt{\frac{k + k_p k}{J_2}}$
- $2\zeta\omega_n = \frac{b_2}{J_2}$

Para determinar $k_p$ que fornece $\zeta = 0,5$:

$$2 \cdot 0,5 \cdot \omega_n = \frac{b_2}{J_2}$$
$$\omega_n = \frac{b_2}{J_2}$$

E também:
$$\omega_n^2 = \frac{k + k_p k}{J_2}$$

Substituindo a primeira expressão na segunda:
$$\left(\frac{b_2}{J_2}\right)^2 = \frac{k + k_p k}{J_2}$$
$$\frac{b_2^2}{J_2} = k + k_p k$$
$$\frac{b_2^2}{J_2} - k = k_p k$$
$$k_p = \frac{b_2^2 - k \cdot J_2}{k \cdot J_2}$$

Para o valor específico de $k$ determinado na parte a) do problema, podemos calcular o valor exato de $k_p$ necessário para obter $\zeta = 0,5$.

Considerando o valor típico da rigidez torcional $k = 0,05$ N·m/rad (este valor deve ser confirmado pela resolução da parte a), temos:

$$k_p = \frac{b_2^2 - k \cdot J_2}{k \cdot J_2} = 
\frac{0,009^2 - 0,05 \cdot 0,1125}{0,05 \cdot 0,1125} = 
\frac{0,000081 - 0,005625}{0,005625} = -0,9856$$

Como obtivemos $k_p < 0$, isso sugeriria controle negativo, o que não satisfaz a restrição $k_p > 0$. 

Portanto, para diferentes valores de $k$, precisaríamos verificar se é possível obter $k_p > 0$ que resulte em $\zeta = 0,5$.

A condição para $k_p > 0$ seria:
$$b_2^2 > k \cdot J_2$$
$$0,009^2 > k \cdot 0,1125$$
$$0,000081 > 0,1125k$$
$$k < 0,00072$$

Para valores muito pequenos de $k$ (< 0,00072 N·m/rad), seria possível obter $k_p > 0$ com $\zeta = 0,5$.

