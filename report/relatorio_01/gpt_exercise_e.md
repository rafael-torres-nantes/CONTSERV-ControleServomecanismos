# Roteiro para Relatório 01

## e) Scripts para simulação em malha fechada

Para o sistema em malha fechada, a função de transferência é:

$$\hat{g}_{MF}(s) = \frac{k \cdot kp}{J_2s^2 + b_2s + k + k_2 + k \cdot kp}$$

Com kp = 6, o ganho estático será:

$$K_{MF} = \frac{k \cdot kp}{k + k_2 + k \cdot kp} = \frac{0,0001 \cdot 6}{0,000125 + 0,0001 \cdot 6} = \frac{0,0006}{0,000725} \approx 0,83$$

Para um sistema de segunda ordem subamortecido com ζ = 0,5, o overshoot pode ser calculado:

$$OS\% = e^{-\pi\zeta/\sqrt{1-\zeta^2}} \times 100\% = e^{-\pi \cdot 0,5/\sqrt{1-0,25}} \times 100\% \approx 16,3\%$$

E o tempo de pico é aproximadamente:

$$t_p = \frac{\pi}{\omega_n\sqrt{1-\zeta^2}}$$

Com $\omega_n = \sqrt{\frac{k + k_2 + k \cdot kp}{J_2}} = \sqrt{\frac{0,000725}{0,1125}} \approx 0,08$ rad/s

Portanto, $t_p \approx \frac{\pi}{0,08 \cdot \sqrt{1-0,25}} \approx 45,6$ segundos

O tempo para atingir 95% do valor final pode ser aproximado para sistemas subamortecidos como:

$$t_{95\%} \approx \frac{3}{\zeta\omega_n} = \frac{3}{0,5 \cdot 0,08} \approx 75 \text{ segundos}$$

Aqui está o script para a simulação:

```octave
// Parâmetros do sistema
r1 = 0.1;       // m
r2 = 0.15;      // m
J2 = 0.1125;    // kg.m²
b2 = 0.009;     // N.m.s
k = 0.0001;     // N.m/rad
k2 = 0.000025;  // N.m/rad
kp = 6;         // Ganho proporcional

// Função de transferência em malha fechada
num_mf = [k*kp];
den_mf = [J2, b2, k+k2+k*kp];
sys_mf = syslin('c', num_mf, den_mf);

// Simulação da resposta ao degrau
t = 0:0.1:200;  // Tempo suficiente para estabilizar
y_mf = csim('step', t, sys_mf);

// Valor final teórico
K_mf = (k*kp)/(k+k2+k*kp);
disp('Valor final teórico em malha fechada:');
disp(K_mf);

// Determinando o tempo para 95% do valor final
valor_95_mf = 0.95*K_mf;
for i=1:length(t)
    if y_mf(i) >= valor_95_mf && all(y_mf(i:min(i+100, length(y_mf))) >= valor_95_mf)
        t_95_mf = t(i);
        break;
    end
end
disp('Tempo para atingir 95% do valor final em malha fechada:');
disp(t_95_mf);

// Calculando o overshoot
[max_val, idx] = max(y_mf);
overshoot = (max_val - K_mf) / K_mf * 100;
t_pico = t(idx);
disp('Overshoot (%):');
disp(overshoot);
disp('Tempo de pico (s):');
disp(t_pico);

// Gráfico da resposta
plot(t, y_mf);
xgrid();
xlabel('Tempo (s)');
ylabel('Posição angular do cilindro 2 (rad)');
title('Resposta ao degrau em malha fechada');
```

---------------------
```
// Parâmetros do sistema
r1 = 0.1;       // m
r2 = 0.15;      // m
J2 = 0.1125;    // kg.m²
b2 = 0.009;     // N.m.s
k = 0.0001;     // N.m/rad
k2 = 0.000025;  // N.m/rad
kp = 6;         // Ganho proporcional

// Função de transferência em malha fechada
num_mf = [k*kp];
den_mf = [J2, b2, k+k2+k*kp];
sys_mf = syslin('c', num_mf, den_mf);

// Simulação da resposta ao degrau
t = 0:0.1:200;  // Tempo suficiente para estabilizar
y_mf = csim('step', t, sys_mf);

// Valor final teórico
K_mf = (k*kp)/(k+k2+k*kp);
disp('Valor final teórico em malha fechada:');
disp(K_mf);

// Determinando o tempo para 95% do valor final
valor_95_mf = 0.95*K_mf;
for i=1:length(t)
    if y_mf(i) >= valor_95_mf && all(y_mf(i:min(i+100, length(y_mf))) >= valor_95_mf)
        t_95_mf = t(i);
        break;
    end
end
disp('Tempo para atingir 95% do valor final em malha fechada:');
disp(t_95_mf);

// Calculando o overshoot
[max_val, idx] = max(y_mf);
overshoot = (max_val - K_mf) / K_mf * 100;
t_pico = t(idx);
disp('Overshoot (%):');
disp(overshoot);
disp('Tempo de pico (s):');
disp(t_pico);

// Gráfico da resposta
plot(t, y_mf);
xgrid();
xlabel('Tempo (s)');
ylabel('Posição angular do cilindro 2 (rad)');
title('Resposta ao degrau em malha fechada');