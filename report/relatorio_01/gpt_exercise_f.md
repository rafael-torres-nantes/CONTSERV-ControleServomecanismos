# Roteiro para Relatório 01

## f) Simulação em Xcos para o sistema em malha fechada

Para implementar o sistema em Xcos, você pode usar os blocos:
- Fonte constante (degrau unitário)
- Somador (para o erro)
- Ganho (para kp)
- Função de transferência
- Osciloscópio para visualizar as saídas

Além disso, para implementar a representação em espaço de estado em Xcos:
1. Crie um bloco de diagrama contínuo no espaço de estado
2. Configure as matrizes A, B, C e D:
   - A = [0, 1; $-(k + k_2)/J_2$, $-b_2/J_2$]
   - B = [0; $k/J_2$]
   - C = [1, 0]
   - D = [0]
3. Conecte os blocos de entrada e saída apropriados

Este sistema é relativamente lento (constantes de tempo grandes), portanto você precisará configurar um tempo de simulação longo (200-300 segundos) para visualizar adequadamente a resposta completa.