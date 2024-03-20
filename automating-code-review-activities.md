# Metadados

* **Título**: Automating Code Review Activities by Large-Scale Pre-training
* **Autores**: Zhiyu Li, Shuai Lu, Daya Guo, Nan Duan, Shailesh Jannu, Grant Jenks, Deep Majumder, Jared Green, Alexey Svyatkovskiy, Shengyu Fu, Neel Sundaresan
* **Instituição(ões) envolvida(s) na pesquisa**: Microsoft Research Asia,  Peking University, Sun Yat-sen University, LinkedIn, Microsoft DevDiv
* **Ano de publicação**: 2022
* **Link para acesso**: [Automating Code Review Activities by Large-Scale Pre-training](https://arxiv.org/pdf/2005.11401.pdf)

# Qual o problema?

O problema que o artigo tenta abordar é a sobrecarga de trabalho enfrentada pelos desenvolvedores durante o processo de revisão de código. 
Embora a revisão de código seja uma parte essencial do ciclo de desenvolvimento de software, ela consome muito tempo e esforço dos desenvolvedores, 
pois eles precisam entender e avaliar logicamente, funcionalmente, e estilisticamente as alterações de código feitas por seus colegas. 

# Qual a solução?

A automação desse processo é vista como uma solução necessária para lidar com essa sobrecarga de trabalho, e o artigo se concentra em utilizar técnicas de pré-treinamento para essa automação.


## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta? 

Eles propõem três tarefas de automação de revisão de código: 
* Estimação da Qualidade da Mudança de Código,
* Geração de Revisão de Código;
* Refinamento de Código.

Essas tarefas são formuladas e definidas formalmente para fornecer uma estrutura clara para o desenvolvimento de algoritmos de automação. Em suma, os autores propõem o desenvolvimento de modelos de aprendizado de máquina para automatizar as tarefas específicas relacionadas à revisão de código.


## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

Um aspecto que chama bastante atenção é a coleta de dados. Os autores coletam dados de solicitações de _pull (pull requests)_ de repositórios de código-fonte 
abertos, priorizando projetos populares em nove das linguagens de programação mais populares no GitHub. 
Além disso, eles realizam um processamento cuidadoso dos dados para construir conjuntos de dados adequados para as tarefas específicas de revisão de código.

Outro ponto relevante é a arquitetura do modelo **CodeReviewer**, que é baseada no Transformer e consiste em 12 camadas de codificador e 12 camadas de 
decodificador. O modelo é inicializado com os parâmetros do CodeT5 e posteriormente pré-treinado com as quatro tarefas de pré-treinamento projetadas pelos 
autores.

A ideia geral da solução é utilizar técnicas de aprendizado de máquina e pré-treinamento para construir um modelo capaz de automatizar algumas tarefas 
específicas do processo de revisão de código, como:

* Estimar a qualidade das mudanças de código
* Gerar comentários de revisão;
* Refinar o código com base nos comentários recebidos.

Essa solução tem o potencial de reduzir a carga de trabalho dos desenvolvedores durante o processo de revisão de código, melhorando a eficiência e 
a qualidade do processo como um todo.

Os detalhes técnicos incluem:

* A coleta de dados,
* O _design_ da arquitetura do modelo **CodeReviewer**;
* As tarefas de pré-treinamento específicas para revisão de código;
* Processamento dos dados para construir conjuntos de dados adequados para treinar e avaliar o modelo.

Cada aspecto desses detalhes técnicos pode ser discutido em mais detalhes para entender melhor como a solução foi implementada e avaliada.

# Como foi avaliado?

Para a tarefa de estimativa de qualidade da mudança de código, foram utilizadas métricas como:

* **Precision**,
* **Recall**;
* **F1-score**;
* **Accuracy**.

A acurácia foi calculada considerando as mudanças de código com problemas (que exigem comentários e atualizações) como a classe positiva.


Na tarefa de geração de comentários de revisão, foi calculado o escore BLEU (Bilingual Evaluation Understudy) para avaliar a qualidade dos comentários 
gerados automaticamente. Além disso, foi realizada uma avaliação humana dos comentários gerados, considerando sua informatividade e 
relevância para a mudança de código correspondente.

Já na tarefa de refinamento de código, foram calculados o escore BLEU entre o código gerado e o código alvo, 
além da taxa de correspondência exata (exact match) entre o código gerado e o código alvo. 
O _score BLEU_ avalia a similaridade entre a previsão e o alvo, enquanto a correspondência exata é uma métrica mais importante nesta tarefa, 
pois indica se a previsão é exatamente igual ao alvo.





# Quais são os resultados?


Os resultados da tarefa de refinamento de código são os seguintes:

| Modelo              | BLEU Score | Taxa de Correspondência Exata (%) |
|---------------------|------------|------------------------------------|
| NaïveCopy           | 58.75      | 0.00                               |
| T5 (6)              | 77.03      | 15.08                              |
| CodeT5 (12)         | 80.82      | 24.41                              |
| CodeReviewer (12)   | 82.61      | 30.32                              |


Estes resultados demonstram que o modelo **CodeReviewer** é capaz de gerar código reparado exatamente igual ao código de referência 
**em mais de 30% dos casos**, o que é duas vezes mais do que o resultado obtido pelo modelo T5 e 25% mais do que o resultado do modelo CodeT5, 
evidenciando a capacidade superior do **CodeReviewer** em entender comentários de revisão e refinar o código com base neles. 
O **CodeReviewer** também obteve um _score BLEU_ mais alto do que os modelos de referência T5 e CodeT5, 
indicando uma melhor qualidade geral das correções geradas.

# Resenha crítica

O artigo apresenta um estudo abrangente sobre a automação do processo de revisão de código, propondo uma abordagem baseada em modelos de 
linguagem pré-treinados, especificamente o CodeReviewer, construído sobre a arquitetura Transformer. 
O trabalho aborda três tarefas principais: estimativa de qualidade de mudança de código, geração de comentários de revisão e refinamento de código, 
demonstrando resultados promissores em cada uma delas.

Uma das principais forças do artigo é a abordagem metódica na construção do conjunto de dados, garantindo sua qualidade e representatividade ao coletar 
informações de solicitações de _pull_ de projetos de código aberto populares em nove linguagens de programação distintas. 
Além disso, os autores realizam uma análise detalhada dos resultados experimentais, demonstrando claramente a 
eficácia do modelo proposto em comparação com baselines e destacando a importância das tarefas de pré-treinamento na melhoria do desempenho.

No entanto, algumas limitações e oportunidades para trabalhos futuros também podem ser identificadas. 
Por exemplo, embora o modelo tenha apresentado melhorias significativas em comparação com as _baselines_, a análise detalhada dos erros cometidos 
pelo modelo em casos específicos poderia fornecer ideias para refinamentos adicionais. Além disso, a aplicação prática do modelo em cenários do mundo real e 
sua integração em ambientes de desenvolvimento de software podem ser exploradas em estudos futuros para avaliar sua usabilidade e eficácia em situações reais.

Em resumo, o artigo representa uma contribuição significativa para a automação de processos de revisão de código, 
demonstrando a viabilidade e eficácia de abordagens baseadas em modelos de linguagem pré-treinados. A metodologia detalhada, conjuntos de dados com qualidade e 
resultados experimentais sólidos tornam este trabalho valioso para a comunidade de pesquisa em engenharia de _software_ e aprendizado de máquina.
