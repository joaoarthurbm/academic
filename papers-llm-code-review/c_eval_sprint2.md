
# Metadados

* **Título**: C-EVAL: A Multi-Level Multi-Discipline Chines Evaluation Suite for Foundation Models
* **Autores**: Yuzhen Huang, Yuzhuo Bai, Zhihao Zhu, Junlei Zhang, Jinghan Zhang, Tangjun Su, Junteng Liu, Chuancheng Lv, Yikai Zhang, Jiayi Lei, Yao Fu, Maosong Sun, Junxian He
* **Instituições**: Shanghai Jiao Tong University, Tsinghua University, University of Edinburgh, The Hong Kong University of Science and Technology
* **Local de publicação**: Advances in Neural Information Processing Systems, v. 36, 2024
* **Ano de publicação**: 2023
* **Link**: [https://arxiv.org/pdf/2305.08322](https://arxiv.org/abs/2305.08322)	

# Qual o problema?

Benchmarks recentes têm aprimorado e apresentado técnicas robustas para a avaliação de resultados de grandes modelos de linguagem (LLMs). Contudo, eles se baseiam na língua inglesa e tendem a exibir vieses geográficos em relação ao conhecimento interno das regiões que os produzem. Isso, portanto, limita o conhecimento sobre a capacidade dos LLMs com outros idiomas, incluindo poderosos LLMs baseados na língua chinesa, que é uma das mais faladas no mundo.

# Qual a solução?

## Como os autores tentam resolver o problema?

Os autores criaram o C-EVAL, primeiro conjunto de avaliação compreensiva do contexto chinês, que avalia minuciosamente o conhecimento avançado e as habilidades de raciocínio dos LLMs chineses. O C-EVAL consiste em questões de exame de múltipla escolha abrangendo diversas disciplinas. Além disso, os autores introduziram o C-EVAL HARD como um benchmark complementar, que é um subconjunto de disciplinas desafiadoras do C-EVAL, exigindo habilidades de raciocínio altamente avançadas para serem resolvidas.

## Quais são os detalhes técnicos dessa solução?

Foram coletadas 13.948 perguntas a partir de simulados e exames locais de pequena escala, visando desviar dos exames nacionais de fácil acesso que podem ter feito parte do pré-treinamento dos LLMS. Além disso, boa parte das amostras foram coletadas a partir de documentos PDF ou Microsoft Word na Internet, ao invés de perguntas estruturadas diretamente. Esses documentos foram analisados e anotados pelos autores para obter o formato estruturado final, processo que frequentemente envolveu conversão de equações em LATEX, o que minimizou ainda mais o risco de contaminação de dados.

Foram selecionadas apenas questões no formato de múltipla escolha, similar ao trabalho de Hendrycks et al. Isso porque a métricas está claramente definida (ou seja, precisão), e perguntas de múltipla escolha são uma forma simples, mas eficaz, de avaliar o potencial de habilidades avançadas desses modelos. As perguntas no C-EVAL abrangem 52 disciplinas diversas, que posteriormente foram agrupadas em categorias mais amplas como ciências exatas e tecnológicas, humanidades, ciências sociais e outras áreas. Cada pergunta tem 4 opções, sendo apenas uma a resposta correta. Os LLMs foram projetados para resolver essas perguntas por meio de instruções.

# Como foi avaliado?

Para fornecer uma visão abrangente do status dos LLMs no contexto da língua chinesa, foram avaliados 11 LLMs de alto desempenho capazes de processar entradas em chinês, abrangendo diversas organizações e variações de quantidade de parâmetros. Também foram incluídos LLMs desenvolvidos por instituições ou indivíduos chineses, voltados especificamente para o contexto chinês.

A performance desses LLMs foi avaliada em diferentes configurações de teste: Zero-shot e Five-shot. No Zero-shot, o modelo tenta responder às perguntas sem ver exemplos anteriores, enquanto no Five-shot, ele recebe cinco exemplos de perguntas/respostas como referência antes de responder a uma nova pergunta. Esses exemplos vêm de uma parte específica do conjunto de dados, chamada de divisão de desenvolvimento. Além disso, foram utilizadas expressões regulares para extrair as respostas geradas pelos modelos, visando garantir a identificação correta dessas respostas em quase todos os casos.

Além disso, foram medidos dois tipos de desempenho: Answer-only (AO) e Chain-of-Thought (COT). No AO, o modelo gera apenas a resposta, e isso foi testado tanto no Zero-shot quanto no Five-shot. Com o COT, o modelo explica seu raciocínio antes de dar a resposta, mas isso foi medido apenas no Five-shot, porque no Zero-shot o modelo tem mais dificuldade em seguir um padrão previsível, o que dificulta a extração correta das respostas.

# Quais são os resultados?

O GPT-4 foi o único modelo que superou 60% de precisão média por área de conhecimento, superando significativamente todos os outros modelos. O segundo melhor, o ChatGPT, ficou mais de 14 pontos percentuais atrás tanto nas configurações de Zero-shot quanto de Five-shot. Já entre os modelos voltados para o contexto chinês, o GLM-130B apresentou o melhor desempenho, ficando em quinto lugar tanto nas configurações zero-shot quanto five-shot, com uma diferença de 7,0 e 14,1 pontos atrás do ChatGPT, respectivamente. Modelos menores, apesar de passarem por ajuste de instruções, ainda tiveram dificuldade em alcançar 40% de precisão.

# Resenha crítica

* É interessante a ideia de utilizar uma base de dados de questões de múltipla escolha para avaliar o desempenho de LLMs em um contexto de linguagem específico. Algo semelhante poderia ser feito para avaliação em contextos de língua portuguesa, considerando que há diversas provas de concursos públicos brasileiros disponíveis na Internet.
* Uma das possíveis ameaças à validade é o viés presente na escolha de questões com 4 alternativas. As questões com menos alternativas foram descartadas, e as com 5 tiveram uma resposta errada descartada aleatoriamente. Também pode ter havido erro humano na conversão manual de fórmulas LÁTEX em texto comum. O uso de REGEX para extrair respostas automaticamente também apresenta um risco.
* Os autores sugerem que outros aspectos, que vão além da precisão, como segurança, viés e robustez, poderiam ser explorados em trabalhos futuros.
* Alguns dos autores têm lançado artigos recentes também sobre LLMs, como [este](https://arxiv.org/abs/2404.09937).

# Discussão

O experimento apresentado pelo artigo pode ser reaplicado em qualquer outro contexto de linguagem humana. A dificuldade do experimento se encontra na construção de uma base de dados específica para cada contexto, pois a extração de perguntas e respostas a partir de exames nacionais pode ser um processo bastante complexo e demorado.

# O que eu tenho a ver com isso?

Seria interessante construir uma base de dados semelhante ao do experimento, mas montada a partir de exames brasileiros, para avaliar o desempenho de LLMs recentes no contexto da língua portuguesa. Essa base também serviria para criar Embeddings do vocabulário português, que poderiam ser usados para treinar um LLM em português.

# Replicação

Toda a implementação do C-Eval está disponível neste [repositório](https://github.com/hkust-nlp/ceval).

