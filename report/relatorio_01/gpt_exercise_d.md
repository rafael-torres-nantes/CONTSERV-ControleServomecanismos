# Roteiro para Relatório 01

## d) Sistema em malha fechada: comportamento subamortecido

Para o sistema em malha fechada com ganho proporcional kp, a função de transferência se torna:

$$\hat{g}_{MF}(s) = \frac{k \cdot kp}{J_2s^2 + b_2s + k + k_2 + k \cdot kp}$$

Comparando com a forma padrão:

$$\frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$

Temos:
- $\omega_n^2 = \frac{k + k_2 + k \cdot kp}{J_2}$
- $2\zeta\omega_n = \frac{b_2}{J_2}$

Portanto:
$\zeta = \frac{b_2}{2 \cdot \sqrt{J_2 \cdot (k + k_2 + k \cdot kp)}}$

Para $\zeta = 0,5$ (subamortecido):

$0,5 = \frac{0,009}{2 \cdot \sqrt{0,1125 \cdot (0,000125 + 0,0001 \cdot kp)}}$

Resolvendo para kp:

$0,5 \cdot 2 \cdot \sqrt{0,1125 \cdot (0,000125 + 0,0001 \cdot kp)} = 0,009$
$\sqrt{0,1125 \cdot (0,000125 + 0,0001 \cdot kp)} = 0,009$
$0,1125 \cdot (0,000125 + 0,0001 \cdot kp) = (0,009)^2$
$0,000014 + 0,00001125 \cdot kp = 0,000081$
$0,00001125 \cdot kp = 0,000067$
$kp \approx 5,96$

Sim, é possível escolher kp > 0 para ter comportamento subamortecido. O valor aproximado é kp = 6.

