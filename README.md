# Metadados

* **Título**: BEYOND METRICS: A CRITICAL ANALYSIS OF THE VARIABILITY IN LARGE LANGUAGE MODEL EVALUATION FRAMEWORKS.
* **Autores**: Marco AF Pimentel, Clément Christophe, Tathagata Raha, Prateek Munjal, Praveen K Kanithi e Shadab Khan.
* **De que instituições são os autores?**  Os autores são da M42, uma organização localizada em Abu Dhabi, Emirados Árabes Unidos.
* **Onde foi publicado**: ArXiv Accessibility Forum
* **Ano de publicação**: 2024
* **Link**: [BEYOND METRICS - LLMs](https://arxiv.org/abs/2407.21072)

# Qual o problema?
O artigo destaca a dificuldade em avaliar grandes modelos de linguagem (LLMs) e aponta a crescente demanda por benchmarks mais rigorosos, além disso, embora existam diversas metodologias e frameworks de avaliação, há uma carência de padronização e consistência nos métodos de cálculo das métricas de desempenho. Essa falta de uniformidade gera variabilidade nos resultados, o que pode levar a interpretações divergentes sobre o desempenho de um modelo, dependendo da metodologia utilizada.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? Uma metodologia? Uma ferramenta?
Os autores do artigo realizaram uma análise comparativa de três frameworks de avaliação populares: OpenCompass, LM Evaluation Harness e HELM. Em vez de criar uma nova ferramenta, eles investigam como as diferenças nos métodos de cálculo das métricas de desempenho, como a comparação de probabilidade de tokens ou a geração de texto, podem afetar os resultados.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?
A solução proposta pelos autores envolve a padronização e maior transparência na forma como as métricas são calculadas, destacando que a falta de consistência nas abordagens de avaliação pode enviesar a escolha de respostas corretas ou influenciar a performance percebida dos modelos. O uso de normalizações diferentes, como por tokens ou por bytes, é um dos fatores que mais impactam as avaliações, podendo favorecer respostas mais curtas ou mais longas. Esta abordagem mostra-se interessante, visto que avaliar uma LLM com frameworks que usam diferentes métricas de desempenho pode impactar nos resultados obtidos, logo, não podemos considerar avaliar um modelo usando apenas uma ferramenta se não houver padronização das métricas.

# Como foi avaliado?
Para avaliar o desempenho dos LLMs, os autores utilizaram quatro métricas de precisão( OC accuracy, Raw accuracy, T-norm accuracy e B-norm accuracy) derivadas dos frameworks OpenCompass e Eval Harness. Essas métricas foram aplicadas em benchmarks amplamente reconhecidos(HellaSwag, MedQA, MMLU e OpenBookQA), com o objetivo de medir como a metodologia de avaliação influencia o desempenho dos modelos. A análise envolveu um total de 25.857 observações, abrangendo diferentes tarefas de compreensão e raciocínio.

O método científico utilizado incluiu a comparação do desempenho dos LLMs em diferentes abordagens de avaliação, explorando como as variações nos métodos de cálculo, especialmente em relação à normalização de probabilidades, impactam os resultados. Dessa forma, foi realizado a comparação entre as métricas, mas também foi analisado como essas variações podem enviesar a escolha de respostas corretas ou alterar a performance percebida dos modelos.

# Quais são os resultados?
Os resultados mostram que entre os modelos analisados (Mistral-7B, Llama2-7B, Llama2-13B e Llama2-70B), o Llama2-70B apresentou desempenho consistentemente superior em todos os conjuntos de dados de referência, superando suas variantes menores e o Mistral-7B. Além disso, a investigação sugere que o desempenho dos LLMs é fortemente influenciado pela metodologia de avaliação e pelos detalhes de implementação utilizados, evidenciando a importância de escolher cuidadosamente os frameworks de avaliação para garantir comparações justas e precisas entre modelos.

# Resenha crítica
O artigo aborda uma questão crucial que, até então, parece ter sido negligenciada por muitos pesquisadores ao avaliar LLMs: a falta de padronização nas métricas de avaliação. Ao invés de focar na criação de novas ferramentas, o trabalho destaca a importância de uma padronização metodológica para evitar avaliações enviesadas, onde um modelo pode se destacar em um benchmark e não em outro, dependendo apenas da métrica utilizada. Isso é altamente relevante para a área de pesquisa da equipe, pois proporciona um guia valioso para realizar avaliações mais justas e consistentes, evitando comparações enganosas entre diferentes modelos.

No entanto, o artigo poderia ter explorado com mais profundidade como cada métrica de avaliação influencia os resultados, possivelmente identificando padrões ou destacando o impacto específico de cada uma. Esse aprofundamento permitiria uma análise mais detalhada sobre a sensibilidade dos modelos a diferentes abordagens de normalização e cálculo de probabilidade. Outra limitação é a ausência de código ou implementação disponível. Embora os benchmarks utilizados sejam acessíveis e o experimento seja descrito de forma reproduzível, a falta de uma implementação direta limita a possibilidade de experimentação imediata por outros leitores.

Quanto aos autores, eles possuem outro trabalho relevante(todos autores presentes neste artigo, também fazem parte desse outro citado), intitulado “Med 42 -- Evaluating Fine-Tuning Strategies for Medical LLMs: Full-Parameter vs. Parameter-Efficient Approaches”, publicado em abril de 2024, que explora estratégias de fine-tuning para modelos médicos baseados na arquitetura Llama-2.

Trabalhos futuros poderiam expandir o estudo da padronização de métricas, desse modo, seria possível analisar a avaliação dos modelos da forma citada no artigo e isto permitiria uma comparação entre resultados padronizados e não-padronizados.

# Discussão

* A falta do código é um fator que não contribuiu para uma boa avaliação do artigo;
* A ideia é interessante, mas não houve um aprofundamento no que eles pesquisaram, citou brevemente o que foi encontrado e os detalhes da metodologia;

# O que eu tenho a ver com isso?
Este artigo é interessante em vários aspectos, entre eles pode-se citar:

* Utilizar esta abordagem em outros artigos/estudos que realizam a avaliação de LLMs, dessa forma, poderia ser possível validar ou refutar os resultados que os autores obtiveram sobre um determinado modelo;

* Realizar um experimento focado na padronização das métricas de avaliação para melhorar a consistência nos resultados. Embora o artigo levante a importância da padronização, ele não realiza esse experimento diretamente;

* Estender a análise para outros modelos;

O artigo pode contribuir na extração de insights sobre os modelos e no entendimento de quais benchmarks um determinado modelo possui melhores resultados.

# Replicação
O experimento é passível de replicação, mas o código não está disponível. No entanto, os benchmarks estão disponíveis na página onde o artigo foi publicado: [BEYOND METRICS - LLMs](https://arxiv.org/abs/2404.14779).