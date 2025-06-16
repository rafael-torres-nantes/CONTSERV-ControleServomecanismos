# Resolução do Sistema de Pêndulo Torcional

## Problema Proposto

Considere o pêndulo torcional da Aula 05, no qual a entrada a se considerar é a posição angular do cilindro 1 e a saída, a do cilindro 2. Os parâmetros são:
- r₁ = 0,1m
- r₂ = 0,15m
- J₂ = 0,1125kg·m²
- b₂ = 0,009N·m·s

## Parte B: Análise da Resposta ao Degrau

### Obtenção da Função de Transferência

A função de transferência que relaciona a posição angular do cilindro 2 com a do cilindro 1 é dada por:

$$G(s) = \frac{\theta_2(s)}{\theta_1(s)} = \frac{r_1 \cdot r_2 \cdot K}{J_2} \cdot \frac{1}{s^2 + \frac{b_2}{J_2}s + \frac{k_2 + Kr_2^2}{J_2}}$$

Substituindo os parâmetros conhecidos e os valores selecionados para K e k₂:

$$G(s) = \frac{(0,1) \cdot (0,15) \cdot (0,001)}{0,1125} \cdot \frac{1}{s^2 + \frac{0,009}{0,1125}s + \frac{k_2 + K(0,15)^2}{0,1125}}$$

$$G(s) = \frac{1,333 \cdot 10^{-4}}{s^2 + 0,08s + 0,00112}$$

### Resposta ao Degrau Unitário

Para uma entrada degrau unitário, $\theta_1(s) = \frac{1}{s}$

A saída do sistema é:

$$\theta_2(s) = G(s) \cdot \theta_1(s) = \frac{1,333 \cdot 10^{-4}}{s(s^2 + 0,08s + 0,00112)}$$

### Valor Final

Aplicando o Teorema do Valor Final:

$$\lim_{t \to \infty} \theta_2(t) = \lim_{s \to 0} s \cdot \theta_2(s) = \lim_{s \to 0} \frac{1,333 \cdot 10^{-4}}{s^2 + 0,08s + 0,00112}$$

Avaliando no limite (s→0):

$$\lim_{s \to 0} \frac{1,333 \cdot 10^{-4}}{0 + 0 + 0,00112} = \frac{1,333 \cdot 10^{-4}}{0,00112} \approx 0,12 \text{ rad}$$

### Tempo de Acomodação

Para um sistema de segunda ordem, o tempo para atingir 95% do valor final pode ser aproximado por:

$$t_{95\%} = \frac{3}{\zeta \cdot \omega_n}$$

Onde:
- $\zeta$ é o fator de amortecimento
- $\omega_n$ é a frequência natural não amortecida

A partir dos coeficientes da função de transferência:
- $\omega_n = √0,00112 ≈ 0,0335 rad/s$
- $\zeta = 0,08/(2·0,0335) ≈ 1,2$

Calculando o tempo de acomodação:

$$t_{95\%} = \frac{3 \cdot 42}{0,08} \approx 158 \text{ segundos}$$

## Observações

1. O sistema apresenta uma resposta lenta, com tempo de acomodação de aproximadamente 158 segundos
2. O valor final da posição angular do cilindro 2 é de aproximadamente 0,12 radianos (≈ 6,9°)
3. O sistema é sobreamortecido, o que resulta em uma resposta sem oscilações

## Conclusão

A análise confirma que o sistema apresenta um comportamento sobreamortecido, conforme especificado no problema. A simulação em Scilab/Octave deve corroborar estes resultados teóricos, confirmando tanto o valor final quanto o tempo necessário para atingir 95% desse valor.

---

*Nota: Os valores de K e k₂ foram escolhidos na parte (a) do problema para garantir que o sistema fosse sobreamortecido, resultando nos comportamentos analisados acima.*