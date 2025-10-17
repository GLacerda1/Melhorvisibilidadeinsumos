# Melhorvisibilidadeinsumos

## Explicação do uso das estruturas e algoritmos no contexto do problema

No notebook, utilizamos três abordagens de **Programação Dinâmica (PD)** para modelar o problema de controle de estoque de insumos em unidades de diagnóstico:

---

### Função de transição (`proximo_estado_e_custo`)

- **Descrição:** recebe o estoque atual, a quantidade pedida e a demanda diária; retorna o **custo total imediato** e o **novo estado do estoque**.  
- **Uso no contexto:** modela o consumo diário dos insumos, os custos de pedido, armazenagem, falta e desperdício.  
- **Importância:** é a base de todas as versões de PD — define como a decisão de pedir insumos afeta o custo futuro e a evolução do estoque.

---

### Versão Recursiva Pura (`V_recursivo`)

- **Descrição:** calcula o valor ótimo de cada estado de forma recursiva, explorando todas as combinações possíveis de pedidos e demandas, sem memorização.  
- **Uso no contexto:** permite entender a formulação teórica do problema e serve como referência conceitual.  
- **Limitação:** cresce exponencialmente com o horizonte `H` e o tamanho do estoque, tornando-se impraticável para problemas reais.

---

### Versão Recursiva com Memorização (`V_memo`)

- **Descrição:** mesma lógica da recursiva pura, mas utiliza `@lru_cache` para armazenar resultados intermediários.  
- **Uso no contexto:** reduz drasticamente o tempo de execução, evitando recalcular estados já visitados.  
- **Importância prática:** permite resolver problemas de tamanho moderado (estoque e horizonte maiores) rapidamente, mantendo a exatidão da solução.

---

### Versão Iterativa (Bottom-Up) (`V_iterativo`)

- **Descrição:** preenche uma tabela `V[t][s]` de forma reversa, do horizonte final até o início, calculando o valor ótimo de cada estado para cada período.  
- **Uso no contexto:** fornece solução eficiente e escalável para qualquer combinação de estoque e horizonte, garantindo **consistência e rapidez**.  
- **Vantagem:** evita a sobrecarga da pilha de chamadas da recursiva e mantém controle total sobre o espaço de estados.

---

### Função de medição de desempenho (`medir`)

- **Descrição:** mede **tempo de execução** e **uso de memória** de cada algoritmo usando `time.perf_counter()` e `tracemalloc`.  
- **Uso no contexto:** permite comparar o desempenho das versões memoizada e iterativa, identificando a abordagem mais eficiente para aplicações reais em unidades de diagnóstico.

---

### Controle de Reprodutibilidade

- **Descrição:** fixamos as sementes dos geradores aleatórios (`random.seed(42)` e `np.random.seed(42)`).  
- **Uso no contexto:** garante que a simulação das demandas seja **consistente** entre execuções, permitindo resultados confiáveis e comparáveis para testes e relatórios.

---

### Estrutura de decisão e loops

- Loops sobre pedidos possíveis (`q`) e demandas (`d`) permitem avaliar **todas as decisões viáveis**, calculando o custo esperado.  
- Essa abordagem garante que a **decisão ótima de reposição diária** minimize custos totais ao longo do horizonte.

---

**Resumo:**  

Cada estrutura e algoritmo foi projetado para capturar a dinâmica do estoque, os custos associados e a aleatoriedade da demanda, equilibrando **precisão e eficiência**.  
- **Recursiva pura:** conceito teórico.  
- **Recursiva memoizada:** equilíbrio entre exatidão e desempenho.  
- **Iterativa bottom-up:** solução prática e escalável para aplicações reais.
