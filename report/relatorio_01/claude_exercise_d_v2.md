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

$$\hat{g}(s) 
= 
\frac{\hat{\theta}_2(s)}{\hat{\theta}_1(s)} 
= 
\frac{r_1 \cdot r_2 \cdot K}{J_2} \cdot \frac{1}{J_2 s^2 + b_2 s + k}
=
\frac{\frac{r_1 \cdot r_2 \cdot K}{J_2}}{s^2 + \frac{b_2}{J_2}s + \frac{k_2 + Kr_2^2}{J_2}}
$$

$$\hat{g}(s) 
=  
\frac{\frac{(0,1) \cdot (0,15) \cdot (0,001)}{0,1125} }{s^2 + \frac{0,009}{0,1125}s + \frac{k_2 + K(0,15)^2}{0,1125}}
= 
\frac{1,333 \cdot 10^{-4}}{s^2 + 0,08s + 0,00112}
$$

Onde $k$ é o coeficiente de rigidez torcional entre os cilindros 1 e 2.

Em malha fechada com um controlador proporcional $k_p$, a função de transferência do sistema se torna:

$$G_{MF}(s) = \frac{k_p \hat{g}(s)}{1 + k_p \hat{g}(s)}$$

Substituindo $\hat{g}(s)$:
$$G_{MF}(s) = \frac{k_p \cdot \frac{1,333 \cdot 10^{-4}}{s^2 + 0,08s + 0,00112}}{1 + k_p \cdot \frac{1,333 \cdot 10^{-4}}{s^2 + 0,08s + 0,00112}} = \frac{1,333 \cdot 10^{-4} k_p}{s^2 + 0,08s + 0,00112 + 1,333 \cdot 10^{-4} k_p}$$

### Determinação do coeficiente de amortecimento

Para um sistema de segunda ordem na forma padrão:

$$G(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$

Comparando com nossa função de transferência em malha fechada:

$$\frac{1,333 \cdot 10^{-4} k_p}{s^2 + 0,08s + 0,00112 + 1,333 \cdot 10^{-4} k_p} = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$

Identificamos:
- $\omega_n^2 = 0,00112 + 1,333 \cdot 10^{-4} k_p$, portanto $\omega_n = \sqrt{0,00112 + 1,333 \cdot 10^{-4} k_p}$
- $2\zeta\omega_n = 0,08$

Para determinar $k_p$ que fornece $\zeta = 0,5$:

$$2 \cdot 0,5 \cdot \omega_n = 0,08$$
$$\omega_n = 0,08$$

E também:
$$\omega_n^2 = 0,00112 + 1,333 \cdot 10^{-4} k_p$$

Substituindo a primeira expressão na segunda:
$$0,08^2 = 0,00112 + 1,333 \cdot 10^{-4} k_p$$
$$0,0064 = 0,00112 + 1,333 \cdot 10^{-4} k_p$$
$$1,333 \cdot 10^{-4} k_p = 0,0064 - 0,00112$$
$$1,333 \cdot 10^{-4} k_p = 0,00528$$
$$k_p = \frac{0,00528}{1,333 \cdot 10^{-4}}$$
$$k_p \approx 39,6$$

Portanto, para $\zeta = 0,5$, o ganho proporcional necessário é aproximadamente $k_p \approx 39,6$.