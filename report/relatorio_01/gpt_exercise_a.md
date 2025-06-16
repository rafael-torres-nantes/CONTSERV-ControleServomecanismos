# Roteiro para Relatório 01

## a) Sistema sobreamortecido: escolha de k e k2

Para determinar se é possível que o sistema seja sobreamortecido, precisamos analisar a equação dinâmica do sistema e relacionar com a forma padrão de segunda ordem.

Para um pêndulo torcional, a equação de transferência é:

$$\hat{g}(s) = \frac{\hat{\theta}_2(s)}{\hat{\theta}_1(s)} = \frac{k}{J_2s^2 + b_2s + k + k_2}$$

Onde:
- $k$ é a constante de rigidez da mola que conecta os cilindros
- $k_2$ é a constante de rigidez da mola que conecta o cilindro 2 à base
- $J_2$ é o momento de inércia do cilindro 2
- $b_2$ é o coeficiente de amortecimento

Comparando com a forma padrão de segunda ordem:

$$\frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$

Obtemos:
- $\omega_n^2 = \frac{k + k_2}{J_2}$
- $2\zeta\omega_n = \frac{b_2}{J_2}$

Para o sistema ser sobreamortecido, precisamos que $\zeta > 1$.

Usando os valores dados:
- $J_2$ = 0,1125 kg·m²
- $b_2$ = 0,009 N·m·s

Calculamos:

$2\zeta\omega_n = \frac{b_2}{J_2} = \frac{0,009}{0,1125} = 0,08$

Agora, para garantir $\zeta > 1$, podemos escolher $\zeta = 1,2$ (por exemplo) e calcular $\omega_n$:

$\omega_n = \frac{0,08}{2 \times 1,2} = \frac{0,08}{2,4} = \frac{1}{30} \approx 0,0333$ rad/s

Com $\omega_n$ e $\zeta$ escolhidos, podemos determinar os valores de $k$ e $k_2$:

$\omega_n^2 = \frac{k + k_2}{J_2}$

Portanto:
$k + k_2 = J_2 \times \omega_n^2 = 0,1125 \times (0,0333)^2 \approx 0,000125$ N·m/rad

Podemos escolher, por exemplo:
- $k$ = 0,0001 N·m/rad
- $k_2$ = 0,000025 N·m/rad

Sim, é possível escolher valores de $k$ e $k_2$ para que o sistema seja sobreamortecido.