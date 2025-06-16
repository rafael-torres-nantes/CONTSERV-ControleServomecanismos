# Roteiro para Relatório 01

## b) Scripts para simulação e análise da resposta ao degrau

Para o sistema com função de transferência:

$$\hat{g}(s) = \frac{k}{J_2s^2 + b_2s + k + k_2}$$

O ganho estático (valor final para entrada degrau) é:

$$K = \frac{k}{k + k_2} = \frac{0,0001}{0,000125} = 0,8$$

Ou seja, para uma entrada degrau unitário, o valor final da saída será 0,8.

Para um sistema de segunda ordem sobreamortecido, o tempo para atingir 95% do valor final pode ser aproximado por:

$$t_{95\%} \approx \frac{3}{\zeta\omega_n} = \frac{3}{1,2 \times 0,0333} \approx 75 \text{ segundos}$$

Aqui está um script em Octave/Scilab para simular a resposta:

```octave
// Parâmetros do sistema
r1 = 0.1;       // m
r2 = 0.15;      // m
J2 = 0.1125;    // kg.m²
b2 = 0.009;     // N.m.s
k = 0.0001;     // N.m/rad
k2 = 0.000025;  // N.m/rad

// Função de transferência
num = [k];
den = [J2, b2, k+k2];
sys = syslin('c', num, den);

// Simulação da resposta ao degrau
t = 0:0.1:150;  // Tempo suficiente para estabilizar
y = csim('step', t, sys);

// Valor final teórico
K = k/(k+k2);
disp('Valor final teórico:');
disp(K);

// Determinando o tempo para 95% do valor final
valor_95 = 0.95*K;
for i=1:length(t)
    if y(i) >= valor_95
        t_95 = t(i);
        break;
    end
end
disp('Tempo para atingir 95% do valor final:');
disp(t_95);

// Gráfico da resposta
plot(t, y);
xgrid();
xlabel('Tempo (s)');
ylabel('Posição angular do cilindro 2 (rad)');
title('Resposta ao degrau do pêndulo torcional');
```

------------------------------------------------

```scilab
// Parâmetros do sistema
r1 = 0.1;       // m
r2 = 0.15;      // m
J2 = 0.1125;    // kg.m²
b2 = 0.009;     // N.m.s
k = 0.0001;     // N.m/rad
k2 = 0.000025;  // N.m/rad

// Função de transferência
num = [k];
den = [J2, b2, k+k2];
sys = syslin('c', num, den);

// Simulação da resposta ao degrau
t = 0:0.1:150;  // Tempo suficiente para estabilizar
y = csim('step', t, sys);

// Valor final teórico
K = k/(k+k2);
disp('Valor final teórico:');
disp(K);

// Determinando o tempo para 95% do valor final
valor_95 = 0.95*K;
for i=1:length(t)
    if y(i) >= valor_95
        t_95 = t(i);
        break;
    end
end
disp('Tempo para atingir 95% do valor final:');
disp(t_95);

// Gráfico da resposta
plot(t, y);
xgrid();
xlabel('Tempo (s)');
ylabel('Posição angular do cilindro 2 (rad)');
title('Resposta ao degrau do pêndulo torcional');
```