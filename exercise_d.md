# Solução das Questões (d) e (e)

## Introdução e Contexto

Suponha que tenhamos um pêndulo torcional cujas equações de estado e parâmetros foram discutidos nos itens anteriores (a), (b) e (c). Agora, nos itens (d) e (e), introduzimos um **controlador de realimentação** cujo ganho é $ k_b $. O objetivo é:

1. **(Questão d)** Verificar se é possível escolher $ k_b > 0 $ para tornar o sistema mais rápido **sem alterar o grau de estabilidade**. Em outras palavras, analisar se há um intervalo de valores de $ k_b $ que melhore a **dinâmica transitória** (menor tempo de acomodação, menor sobressinal, etc.) e permaneça estável. Depois, **calcular a dinâmica** em malha fechada quando a entrada de referência for $ r(t) = 0{,}5 $.

2. **(Questão e)** Elaborar *scripts* em Scilab ou Octave e, também, simular em Xcos (ou ferramenta equivalente), para:
   - Obter a resposta angular de um dos cilindros (ou do pêndulo) partindo de um valor inicial até o valor final.
   - Verificar se ocorre uma atenuação de 95% do valor final em até **3 segundos**.
   - Repetir a simulação em *malha fechada* e constatar o comportamento do sistema.

---

## (d) Escolha de $ k_b $ e Análise via Lugar das Raízes

### 1. Modelo em Malha Aberta

Suponha que o sistema em malha aberta possua uma função de transferência genérica:
$$
G(s) = \frac{Y(s)}{U(s)},
$$
onde:
- $ U(s) $ é o sinal de entrada,
- $ Y(s) $ é a saída de interesse (por exemplo, o ângulo do cilindro 2).

No *diagrama de blocos* indicado no enunciado, há uma realimentação **proporcional** de ganho $ k_b $. Assim, a malha fechada pode ser representada por:

$$
\text{Malha Fechada}:\quad
\frac{Y(s)}{R(s)} 
= \frac{k_b\,G(s)}{1 + k_b\,G(s)}.
$$

### 2. Condição de Estabilidade e Grau de Estabilidade

Para verificar a **estabilidade** do sistema, analisamos o **polinômio característico** em malha fechada:
$$
1 + k_b\,G(s) = 0.
$$
Via método do **Lugar das Raízes (Root Locus)**, observamos como as raízes do polinômio característico se deslocam no plano $s$ à medida que $ k_b $ varia de $ 0 $ a $ +\infty $.

- **Se o sistema é estável em malha aberta** (ou pelo menos se não houver polos em RHP ($ \text{Re}(s) > 0 $) para $ k_b=0 $), podemos identificar, por meio do diagrama de lugar das raízes, **quais valores de $ k_b $** mantêm o sistema no semiplano esquerdo ($ \text{Re}(s) < 0 $).
- **O grau de estabilidade** está relacionado à quantidade de polos no semiplano esquerdo (SLE). Se o lugar das raízes não cruzar o eixo imaginário em nenhum ponto, o grau de estabilidade não muda.

Portanto, **a resposta** à pergunta **“É possível escolher $ k_b>0 $ para melhorar o regime transitório sem alterar o grau de estabilidade?”** costuma ser **“Sim”**, desde que exista um **intervalo de valores** para $ k_b $ nos quais todos os polos permaneçam no semiplano esquerdo e ao mesmo tempo se tornem mais rápidos (mais negativos).

> **Comentário:** Em geral, aumentar $ k_b $ tende a **deslocar os polos** para a esquerda (tornando o sistema mais ágil) até certo ponto; se $ k_b $ cresce demais, eventualmente alguns polos podem migrar para o semiplano direito, comprometendo a estabilidade. Daí a necessidade de uma faixa de valores ótima.

### 3. Cálculo da Dinâmica para $ r(t) = 0{,}5 $

Uma vez **escolhido** um valor de $ k_b $ satisfatório (por exemplo, a partir de um projeto preliminar ou de simulações do lugar das raízes), obtemos a função de transferência em malha fechada:

$$
G_{CL}(s) \;=\; \frac{Y(s)}{R(s)} 
\;=\; \frac{k_b\,G(s)}{1 + k_b\,G(s)}.
$$

Para uma **entrada degrau** de amplitude $0{,}5$, a entrada no domínio de Laplace é:

$$
R(s) = \frac{0{,}5}{s}.
$$

Logo, a saída $ Y(s) $ em regime transitório é:

$$
Y(s) = G_{CL}(s) \cdot R(s)
      = \frac{k_b\,G(s)}{1 + k_b\,G(s)} 
        \times \frac{0{,}5}{s}.
$$

No domínio do tempo, esta saída será a **resposta ao degrau** de 0,5. Isso pode ser analisado:
- **Analiticamente** (caso as equações de estado sejam de fácil resolução).
- **Por simulação** (com Scilab, Octave, MATLAB, etc.).

---

## (e) Scripts para Simulação e Verificação dos 95% em 3 s

Para **validar** a escolha de $ k_b $ (ou de outros parâmetros do controlador) e comprovar que o sistema atinge 95% do valor final em até 3 segundos, podemos usar **Scilab**, **Octave** ou **MATLAB**. A seguir, apresentamos um roteiro **exemplificativo** em *pseudo-código* para Scilab/Octave. 

### 1. Definição do Modelo

Vamos supor que tenhamos a função de transferência do sistema em malha aberta:
```scilab
// Exemplo meramente ilustrativo
s = poly(0, 's');
numG = 1.2;           // Numerador de G(s)
denG = [1, 5, 6];     // Denominador de G(s) -> G(s) = 1.2 / (s^2 + 5s + 6)
G = syslin('c', numG, denG);
```

> **Observação:** Os valores acima são apenas ilustrativos. Substitua-os pelos valores reais do problema (por exemplo, aqueles obtidos na questão (b) ou (c)).

### 2. Escolha de $ k_b $ e Função de Transferência em Malha Fechada

```scilab
kb = 10;  // Exemplo de ganho escolhido
// Malha fechada usando feedback unitário:
Gmf = feedback(kb*G, 1);  // Gmf(s) = k_b*G(s) / [1 + k_b*G(s)]
```

### 3. Simulação no Domínio do Tempo

Digamos que queiramos simular por 5 segundos a resposta ao degrau de amplitude 0,5:

```scilab
t = 0:0.01:5;                 // Vetor de tempo, passo de 0.01 s
r = 0.5*ones(t);              // Degrau de amplitude 0,5
y = csim(r, t, Gmf);          // Resposta do sistema Gmf(s) ao sinal r(t)

// Plotando
plot(t, y, 'b-');
xlabel("Tempo (s)");
ylabel("Saída y(t)");
title("Resposta ao degrau de 0,5 em malha fechada");
```

### 4. Verificando o Critério de 95% em 3 s

Para dizer que a resposta atinge 95% do valor final (que, para um degrau de 0,5, seria $ 0{,}95 \times 0{,}5 = 0{,}475 $) em até 3 segundos, **podemos**:

```scilab
finalValue = 0.5;           // Valor final esperado do degrau
threshold = 0.95*finalValue; // 95% do valor final => 0.475
indice_3s = find(t>=3);     // Índice onde t >= 3
indice_3s = indice_3s(1);   // Primeiro índice em que t=3

if y(indice_3s) >= threshold then
    disp("O sistema atinge pelo menos 95% do valor final em até 3 segundos.");
else
    disp("O sistema NÃO atinge 95% do valor final em 3 segundos.");
end
```

### 5. Simulação no Xcos (ou Simulink/Octave/Outra Ferramenta)

- **Xcos** (Scilab) ou **Simulink** (MATLAB) permite desenhar blocos representando:
  - Fonte de degrau (Amplitude = 0,5)
  - Bloco de função de transferência (Gmf(s))
  - Bloco *Scope* para visualizar a saída
- Ajustar os **parâmetros de simulação** (tempo final = 5 s, por exemplo).
- Executar a simulação e **verificar graficamente** o tempo de acomodação até 95%.

---

## Conclusões

1. **(Questão d)** 
   - É **possível** sim escolher $ k_b>0 $ para acelerar a resposta sem alterar o grau de estabilidade, **desde que** identifiquemos, via **Lugar das Raízes**, o intervalo de $ k_b $ no qual todos os polos do sistema fechado continuam no **semiplano esquerdo**.
   - Para um valor específico de $ k_b $, a dinâmica de **resposta ao degrau** de amplitude $0{,}5$ pode ser obtida **analiticamente** ou via **simulação**. A tendência é o sistema acomodar **mais rapidamente** (menor tempo de subida/acomodação) comparado a $ k_b=0 $.

2. **(Questão e)** 
   - Os *scripts* exemplificados em Scilab/Octave permitem verificar se, de fato, em **3 segundos** o sistema alcança **95%** da resposta final (ou outro critério de desempenho estipulado).
   - A **simulação em Xcos** (ou ferramenta análoga) confirma de modo **visual** e **numérico** o comportamento do sistema em malha fechada.

---

## Referências e Observações Finais

- [1] Ogata, K. *Modern Control Engineering*. Prentice Hall.
- [2] Dorf, R. C., Bishop, R. H. *Sistemas de Controle Modernos*. LTC.
- [3] Documentação do [Scilab/Xcos](https://www.scilab.org/) e [GNU Octave](https://octave.org/).

**Obs.:** Os valores numéricos (massas, inércias, constantes de amortecimento, etc.) devem ser substituídos pelos **dados específicos** do enunciado do problema (questões anteriores). A estrutura aqui serve como **guia geral** para chegar às respostas de (d) e (e).
```

Esperamos que este passo a passo **clarifique** como conduzir a análise via **Lugar das Raízes** para escolher $ k_b $ e como **simular** o sistema tanto em Scilab/Octave (scripts) quanto em Xcos (para visualização gráfica). Desse modo, respondemos às questões (d) e (e) de forma integrada e completa.