# 📘 Raízes para Sistemas de 2ª Ordem Superamortecidos

Nos sistemas de 2ª ordem superamortecidos, a equação característica tem duas raízes **reais e distintas**. Vou explicar como isso funciona.

Para um sistema de 2ª ordem, a equação característica é tipicamente da forma:

$$
s^2 + 2\zeta\omega_n s + \omega_n^2 = 0
$$

Onde:

- $ \zeta $ é o coeficiente de amortecimento  
- $ \omega_n $ é a frequência natural não-amortecida do sistema  

Um sistema é considerado **superamortecido** quando $ \zeta > 1 $. Neste caso, o discriminante da equação quadrática $ b^2 - 4ac $ é **positivo**, resultando em duas raízes reais e distintas.

Essas raízes podem ser calculadas pela fórmula:

$$
s_{1,2} = -\zeta\omega_n \pm \omega_n\sqrt{\zeta^2 - 1}
$$

Ou, simplificando:

- $ s_1 = -\omega_n(\zeta + \sqrt{\zeta^2 - 1}) $
- $ s_2 = -\omega_n(\zeta - \sqrt{\zeta^2 - 1}) $

Ambas as raízes são **negativas** (para sistemas estáveis), mas com valores diferentes. Isso faz com que a resposta do sistema seja uma **combinação de dois termos exponenciais decrescentes**, **sem oscilação**.

A resposta temporal de um sistema superamortecido é geralmente da forma:

$$
y(t) = A_1 e^{s_1 t} + A_2 e^{s_2 t}
$$

Onde $ A_1 $ e $ A_2 $ são constantes determinadas pelas condições iniciais do sistema.

---

# 🧮 Calcular as Raízes do Sistema Superamortecido

Para um sistema de 2ª ordem com:

- $ \zeta = 1.2 $
- $ \omega_n = 0.0333 $

Vamos calcular as raízes da equação característica:

$$
s^2 + 2\zeta\omega_n s + \omega_n^2 = 0
$$

Substituindo os valores:

$$
s^2 + 2(1.2)(0.0333)s + (0.0333)^2 = 0  
\Rightarrow s^2 + 0.07992s + 0.001109 = 0
$$

As raízes são calculadas pela fórmula:

$$
s_{1,2} = -\zeta\omega_n \pm \omega_n\sqrt{\zeta^2 - 1}
$$

Calculando:

- $ \zeta\omega_n = 1.2 \times 0.0333 = 0.03996 $
- $ \sqrt{\zeta^2 - 1} = \sqrt{1.44 - 1} = \sqrt{0.44} \approx 0.6633 $

Logo:

- $ s_1 = -0.03996 + 0.0333 \cdot 0.6633 = -0.01787 $
- $ s_2 = -0.03996 - 0.0333 \cdot 0.6633 = -0.06205 $

### ✅ Portanto, as raízes do sistema superamortecido são:

- $ s_1 = -0.01787 $
- $ s_2 = -0.06205 $

Ambas são **negativas**, como esperado para um sistema estável superamortecido, e por serem valores diferentes, a resposta do sistema será uma **combinação de duas exponenciais decrescentes sem oscilação**.

---

# ⏱️ Calcular o Tempo de Assentamento de 5% (t₅%)

Para calcular o **tempo de assentamento de 5%** (tempo para atingir 95% do valor final) em um sistema de 2ª ordem superamortecido, precisamos analisar a resposta temporal do sistema.

Para o sistema com as raízes:

- $ s_1 = -0.01787 $
- $ s_2 = -0.06205 $

A resposta ao **degrau unitário** tem a forma:

$$
y(t) = 1 - \left[K_1 e^{s_1 t} + K_2 e^{s_2 t}\right]
$$

Onde $ K_1 $ e $ K_2 $ são constantes determinadas pelas condições iniciais.

Para sistemas superamortecidos, o **tempo de assentamento** é principalmente determinado pela **raiz mais lenta** (a que está mais próxima do eixo imaginário), que no nosso caso é:

$$
s_1 = -0.01787
$$

O tempo para atingir 95% do valor final pode ser calculado com maior precisão usando:

$$
t_{5\%} = \frac{3}{|s_1|}
\Rightarrow t_{5\%} = \frac{3}{0.01787} \approx 167.8 \text{ segundos}
$$

Se usar o $3.3354$ ao invés do $3$, o resultado fica $186.8$ segundos.

### 🔍 Observação importante:

Enquanto a aproximação comum de t₅% ≈ 3/|s₁| fornece uma estimativa de 168 segundos, o valor mais preciso para sistemas superamortecidos considera a interação entre os dois modos exponenciais, resultando no valor de aproximadamente 186,8 segundos.

---