
## Questão b) Simulação e análise teórica

### Desenvolvimento teórico

Usando a função de transferência obtida:

$$G(s) = \frac{\Theta_2(s)}{\Theta_1(s)} = \frac{k}{J_2 s^2 + b_2 s + k}$$

Com os valores calculados:
- $k = 0,00015$ N·m/rad
- $J_2 = 0,1125$ kg·m²
- $b_2 = 0,009$ N·m·s
- $\zeta \approx 1,095$ (sobreamortecido)
- $\omega_n \approx 0,0365$ rad/s

Para um sistema sobreamortecido ($\zeta > 1$) com entrada degrau unitário, a resposta temporal é:

$$\theta_2(t) = 1 - \frac{e^{-\zeta\omega_n t}}{\sqrt{\zeta^2-1}}\left[e^{\omega_n t \sqrt{\zeta^2-1}} - e^{-\omega_n t \sqrt{\zeta^2-1}}\right]$$

O valor final da saída para um degrau unitário na entrada é:

$$\lim_{t \to \infty} \theta_2(t) = 1$$

O tempo para atingir 95% do valor final pode ser estimado resolvendo:

$$0,95 = 1 - \frac{e^{-\zeta\omega_n t}}{\sqrt{\zeta^2-1}}\left[e^{\omega_n t \sqrt{\zeta^2-1}} - e^{-\omega_n t \sqrt{\zeta^2-1}}\right]$$

Para sistemas sobreamortecidos, uma aproximação comum é:

$$t_{95\%} \approx \frac{3}{\zeta\omega_n}$$

Calculando:
$$t_{95\%} \approx \frac{3}{1,095 \cdot 0,0365} \approx 75,1 \text{ segundos}$$

### Script em Octave/Scilab para simulação

```octave
// Parâmetros do sistema
r1 = 0.1;      // raio do cilindro 1 (m)
r2 = 0.15;     // raio do cilindro 2 (m)
J2 = 0.1125;   // momento de inércia do cilindro 2 (kg.m²)
b2 = 0.009;    // coeficiente de atrito viscoso (N.m.s)
k = 0.00015;   // rigidez torcional escolhida (N.m/rad)

// Cálculo de parâmetros do sistema
wn = sqrt(k/J2);        // Frequência natural
zeta = b2/(2*sqrt(k*J2)); // Coeficiente de amortecimento

// Definição da função de transferência do sistema
num = [k];
den = [J2, b2, k];
sys = syslin('c', num, den);

// Simulação com entrada degrau
t = linspace(0, 200, 2000);  // Tempo suficiente para estabilização
u = ones(1, length(t));      // Entrada degrau unitário
y = csim(u, t, sys);         // Resposta do sistema

// Determinação do valor final
valor_final = y(length(y));

// Determinação do tempo para atingir 95% do valor final
threshold = 0.95 * valor_final;
idx = find(y >= threshold, 1);
tempo_95 = t(idx);

// Plotagem dos resultados
plot(t, y, 'LineWidth', 2);
xgrid;
xlabel('Tempo (s)');
ylabel('Posição Angular do Cilindro 2 (rad)');
title('Resposta ao Degrau do Pêndulo Torcional');

// Exibição dos resultados
printf('Coeficiente de amortecimento (zeta): %f\n', zeta);
printf('Frequência natural (wn): %f rad/s\n', wn);
printf('Valor final teórico: 1.0\n');
printf('Valor final simulado: %f\n', valor_final);
printf('Tempo para atingir 95%% do valor final: %f s\n', tempo_95);
printf('Tempo teórico para 95%%: %f s\n', 3/(zeta*wn));
```

### Análise dos resultados

Com o sistema sobreamortecido ($\zeta \approx 1,095 > 1$):
1. O valor final da saída para um degrau unitário é 1.
2. O tempo para atingir 95% do valor final é aproximadamente 75,1 segundos.
3. A resposta não apresenta overshoot (característica de sistemas sobreamortecidos).
4. A resposta é relativamente lenta devido ao alto valor de amortecimento e baixa frequência natural.

Este comportamento é característico de sistemas sobreamortecidos, que apresentam respostas mais lentas, porém sem oscilações.