# Resolução da Questão c) - Simulação em XCOS e Análise das Variáveis de Estado

## Questão c) Simule o sistema em xcos. Plote o comportamento das variáveis de estado ao longo do tempo. O que representam fisicamente as variáveis de estado neste sistema?

### Abordagem da simulação em XCOS

Para simular o pêndulo torcional no XCOS (ambiente de simulação do Scilab), precisamos primeiro identificar um modelo em espaço de estados do sistema. Vamos implementar esta simulação e analisar o que as variáveis de estado representam fisicamente.

### Modelagem em Espaço de Estados

A equação diferencial de segunda ordem que descreve o movimento do pêndulo torcional é:

$$J_2 \ddot{\theta}_2 + b_2 \dot{\theta}_2 + k(\theta_2 - \theta_1) = 0$$

Reescrevendo para colocar em forma padrão:

$$\ddot{\theta}_2 = -\frac{b_2}{J_2}\dot{\theta}_2 - \frac{k}{J_2}\theta_2 + \frac{k}{J_2}\theta_1$$

Para converter para espaço de estados, definimos:
- $x_1 = \theta_2$ (posição angular do cilindro 2)
- $x_2 = \dot{\theta}_2$ (velocidade angular do cilindro 2)

Assim, as equações de estado ficam:
- $\dot{x}_1 = x_2$
- $\dot{x}_2 = -\frac{b_2}{J_2}x_2 - \frac{k}{J_2}x_1 + \frac{k}{J_2}\theta_1$

Em forma matricial:

$$\begin{bmatrix} \dot{x}_1 \\ \dot{x}_2 \end{bmatrix} = 
\begin{bmatrix} 0 & 1 \\ -\frac{k}{J_2} & -\frac{b_2}{J_2} \end{bmatrix}
\begin{bmatrix} x_1 \\ x_2 \end{bmatrix} +
\begin{bmatrix} 0 \\ \frac{k}{J_2} \end{bmatrix} \theta_1$$

$$y = \begin{bmatrix} 1 & 0 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$$

### Script Scilab para gerar o diagrama XCOS

```scilab
// Parâmetros do sistema
r1 = 0.1;      // raio do cilindro 1 (m)
r2 = 0.15;     // raio do cilindro 2 (m)
J2 = 0.1125;   // momento de inércia do cilindro 2 (kg.m²)
b2 = 0.009;    // coeficiente de atrito viscoso (N.m.s)
k = 0.00015;   // rigidez torcional escolhida (N.m/rad)

// Matrizes do espaço de estados
A = [0, 1; -k/J2, -b2/J2];
B = [0; k/J2];
C = [1, 0];
D = [0];

// Criação de um novo arquivo XCOS
xcos_diagram = scicos_diagram();

// Tempo de simulação
t_final = 200;

// Adicionar bloco de entrada degrau
blk_degrau = STEP_FUNCTION('define');
blk_degrau.graphics.exprs = ['0'; '1'];
blk_degrau.model.rpar = [0; 1];
blk_degrau.graphics.pout = 1;
xcos_diagram = scs_m.objs($+1) = blk_degrau;

// Adicionar bloco de sistema contínuo (espaço de estados)
blk_sys = CSSLTI4('define');
blk_sys.model.A = A;
blk_sys.model.B = B;
blk_sys.model.C = C;
blk_sys.model.D = D;
blk_sys.graphics.pin = 1;
blk_sys.graphics.pout = 2;
xcos_diagram = scs_m.objs($+1) = blk_sys;

// Adicionar bloco de osciloscópio para visualização
blk_oscilo = CSCOPE('define');
blk_oscilo.graphics.pin = 2;
blk_oscilo.model.ipar = [1; 1; 1; 0; 0; 0; 0; 1];
blk_oscilo.model.rpar = [0; t_final; -1.5; 1.5];
xcos_diagram = scs_m.objs($+1) = blk_oscilo;

// Adicionar conexões entre os blocos
// Conexão do degrau para o sistema
xcos_diagram = scs_m.objs($+1) = CLKSOM('define');
// Conexão do sistema para o osciloscópio
xcos_diagram = scs_m.objs($+1) = CLKSOM('define');

// Configurar o diagrama para simulação
xcos_diagram.props.tf = t_final;
xcos_diagram.props.context = "r1 = " + string(r1) + "; " + ...
                            "r2 = " + string(r2) + "; " + ...
                            "J2 = " + string(J2) + "; " + ...
                            "b2 = " + string(b2) + "; " + ...
                            "k = " + string(k) + "; ";

// Abrir o diagrama XCOS
xcos(xcos_diagram);
```

### Simulação alternativa usando Scilab (sem XCOS)

Alternativamente, podemos simular o sistema diretamente em Scilab:

```octave
// Parâmetros do sistema
r1 = 0.1;      // raio do cilindro 1 (m)
r2 = 0.15;     // raio do cilindro 2 (m)
J2 = 0.1125;   // momento de inércia do cilindro 2 (kg.m²)
b2 = 0.009;    // coeficiente de atrito viscoso (N.m.s)
k = 0.00015;   // rigidez torcional escolhida (N.m/rad)

// Matrizes do espaço de estados
A = [0, 1; -k/J2, -b2/J2];
B = [0; k/J2];
C = [1, 0; 0, 1]; // Saída para ambas as variáveis de estado
D = [0; 0];

// Criar sistema em espaço de estados
sys_ss = syslin('c', A, B, C, D);

// Simulação com entrada degrau
t = linspace(0, 200, 2000);  // 200 segundos de simulação
u = ones(1, length(t));      // Entrada degrau unitário
y = csim(u, t, sys_ss);      // Resposta do sistema

// Separar as variáveis de estado
theta2 = y(1,:);  // Posição angular (primeira variável de estado)
omega2 = y(2,:);  // Velocidade angular (segunda variável de estado)

// Plotar as variáveis de estado
subplot(2,1,1);
plot(t, theta2, 'LineWidth', 2);
xgrid;
xlabel('Tempo (s)');
ylabel('θ₂ (rad)');
title('Posição Angular do Cilindro 2');

subplot(2,1,2);
plot(t, omega2, 'LineWidth', 2);
xgrid;
xlabel('Tempo (s)');
ylabel('ω₂ (rad/s)');
title('Velocidade Angular do Cilindro 2');

// Determinação do valor final da posição angular
valor_final = theta2(length(theta2));

// Determinação do tempo para atingir 95% do valor final
threshold = 0.95 * valor_final;
idx = find(theta2 >= threshold, 1);
tempo_95 = t(idx);

// Exibição dos resultados
printf('Valor final da posição angular: %f rad\n', valor_final);
printf('Tempo para atingir 95%% do valor final: %f s\n', tempo_95);

```

### Interpretação Física das Variáveis de Estado

As variáveis de estado no sistema do pêndulo torcional têm interpretações físicas diretas:

1. **Primeira variável de estado (x₁ = θ₂)**:
   - **Interpretação física**: Representa a posição angular do cilindro 2 em radianos.
   - **Significado**: Indica o deslocamento angular do segundo cilindro em relação à sua posição de equilíbrio.
   - **Comportamento esperado**: Para um sistema sobreamortecido com entrada degrau, esta variável aumentará gradualmente até atingir o valor final sem oscilações.

2. **Segunda variável de estado (x₂ = ω₂ = dθ₂/dt)**:
   - **Interpretação física**: Representa a velocidade angular do cilindro 2 em radianos por segundo.
   - **Significado**: Indica a taxa de variação da posição angular do segundo cilindro.
   - **Comportamento esperado**: Parte de zero, atinge um valor máximo e depois diminui gradualmente até zero quando o sistema estabiliza.

### Justificativa da escolha das variáveis de estado

Estas variáveis são escolhidas porque:
1. São grandezas físicas diretamente mensuráveis no sistema
2. Fornecem uma descrição completa do estado dinâmico do sistema a qualquer momento
3. Permitem reconstruir o comportamento completo do sistema quando conhecidas suas condições iniciais e a entrada aplicada
4. Representam a energia armazenada no sistema:
   - A posição angular (θ₂) relaciona-se com a energia potencial elástica armazenada na mola torcional
   - A velocidade angular (ω₂) relaciona-se com a energia cinética armazenada no cilindro em rotação

### Comportamento esperado na simulação

1. **Para θ₂ (posição angular)**:
   - Inicia em zero
   - Aumenta monotonicamente (sem oscilações, já que o sistema é sobreamortecido)
   - Estabiliza em um valor final igual ao valor da entrada degrau (1 radiano)
   - O tempo para atingir 95% do valor final deve ser aproximadamente 75 segundos, conforme calculado anteriormente

2. **Para ω₂ (velocidade angular)**:
   - Inicia em zero
   - Aumenta rapidamente até um valor máximo
   - Depois diminui gradualmente até zero quando o sistema atinge o estado estacionário
   - Permanece sempre positiva (sem troca de sinal, característica de sistema sobreamortecido)

Esta análise completa das variáveis de estado nos permite compreender completamente a dinâmica do pêndulo torcional e interpretar fisicamente os resultados da simulação.