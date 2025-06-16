# Roteiro para Relatório 01

## c) Variáveis de estado e sua interpretação física

As variáveis de estado para este sistema podem ser escolhidas como:
- $x_1 = θ₂$ (posição angular do cilindro 2)
- $x_2 = dθ₂/dt$ (velocidade angular do cilindro 2)

As equações de estado seriam:
- $dx_1/dt = x_2$
- $dx_2/dt = (k·θ₁ - b_2·x_2 - (k+k_2)·x_1)/J_2$

Fisicamente:
- $x_1$ representa a posição angular do cilindro 2, medida em radianos
- $x_2$ representa a velocidade angular do cilindro 2, medida em radianos por segundo

Estas variáveis são importantes para descrever completamente o estado dinâmico do sistema a qualquer momento.