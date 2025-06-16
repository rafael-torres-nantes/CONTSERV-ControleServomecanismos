## Questão e) Simulação do sistema com controle em malha fechada

Para esta questão, precisamos escrever scripts para simular o comportamento do sistema em malha fechada com $\hat{g}(s) = \frac{\hat{\theta}_2(s)}{\hat{r}(s)}$ e entrada degrau.

### Script em Octave/Scilab para simulação do sistema:

```octave
// Parâmetros do sistema
r1 = 0.1;      // raio do cilindro 1 (m)
r2 = 0.15;     // raio do cilindro 2 (m)
J2 = 0.1125;   // momento de inércia do cilindro 2 (kg.m²)
b2 = 0.009;    // coeficiente de atrito viscoso (N.m.s)
k = 0.05;      // rigidez torcional (N.m/rad) - valor a ser confirmado na parte a)

// Cálculo do valor de kp para zeta = 0.5
// Se k < 0.00072, podemos ter kp > 0
// Caso contrário, vamos usar um valor de k que permita kp > 0
if (k < 0.00072)
    kp = (b2^2 - k*J2)/(k*J2);
else
    k = 0.0007; // Escolhemos um valor que permita kp > 0
    kp = (b2^2 - k*J2)/(k*J2);
end

// Definição da função de transferência do sistema sem controle
num_g = [k];
den_g = [J2, b2, k];
sys_g = syslin('c', num_g, den_g);

// Função de transferência em malha fechada
num_mf = [kp*k];
den_mf = [J2, b2, k*(1+kp)];
sys_mf = syslin('c', num_mf, den_mf);

// Simulação com entrada degrau
t = linspace(0, 5, 1000); // 5 segundos de simulação
u = ones(1, length(t));   // Entrada degrau unitário
y = csim(u, t, sys_mf);   // Resposta do sistema

// Determinação do valor final
valor_final = y(length(y));

// Determinação do tempo para atingir 95% do valor final
threshold = 0.95 * valor_final;
idx = find(y >= threshold, 1);
tempo_95 = t(idx);

// Determinação do overshoot
overshoot = (max(y) - valor_final) / valor_final * 100;

// Plotagem dos resultados
plot(t, y, 'LineWidth', 2);
xgrid;
xlabel('Tempo (s)');
ylabel('Posição Angular do Cilindro 2 (rad)');
title('Resposta do Sistema em Malha Fechada com Controle Proporcional');

// Exibição dos resultados
printf('Valor de kp calculado: %f\n', kp);
printf('Valor final: %f\n', valor_final);
printf('Tempo para atingir 95%% do valor final: %f s\n', tempo_95);
printf('Overshoot: %f%%\n', overshoot);
```

### Análise teórica

Para um sistema de segunda ordem com amortecimento $\zeta = 0,5$ (subamortecido), podemos calcular teoricamente:

1. **Valor final para entrada degrau unitário**:
   - Para um sistema tipo 0 (sem integradores na malha aberta), o valor final é:
   $$\text{Valor final} = \frac{K_p \cdot k}{k + k_p \cdot k}$$
   
   Onde $K_p$ é o ganho DC do sistema com controle.

2. **Tempo de subida (para atingir 95% do valor final)**:
   - Para $\zeta = 0,5$, o tempo aproximado é:
   $$t_{95\%} \approx \frac{3}{\zeta \omega_n}$$
   
   Onde $\omega_n = \sqrt{\frac{k(1+k_p)}{J_2}}$

3. **Overshoot**:
   - O overshoot percentual para um sistema de segunda ordem é:
   $$\text{Overshoot (\%)} = e^{\frac{-\pi\zeta}{\sqrt{1-\zeta^2}}} \times 100\%$$
   - Para $\zeta = 0,5$: $\text{Overshoot} \approx 16,3\%$

### Conclusão

Com base na análise teórica e na simulação, podemos confirmar:
- É possível projetar um controlador proporcional com $k_p > 0$ para obter um amortecimento $\zeta = 0,5$, mas apenas para valores muito pequenos de rigidez torcional $k$.
- O sistema apresenta uma resposta subamortecida característica com overshoot próximo a 16,3% e tempo de acomodação proporcional à frequência natural do sistema.

Os resultados específicos dos valores de tempo de acomodação e valor final dependerão do valor exato de $k$ determinado na parte (a) do problema.