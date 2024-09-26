
# Metadados

Título: *"LLM-based NLG Evaluation: Current Status and Challenges"*
Autores: *Mingqi Gao, Xinyu Hu, Jie Ruan , Xiao Pu , Xiaojun Wan*
Instituição(ões) envolvida(s) na pesquisa: *Peking University*
* Ano de publicação: *2024*
* Link para acesso: [LLM-based NLG Evaluation: Current Status and Challenges](https://arxiv.org/pdf/2402.01383)

# Qual o problema?
O artigo discute a inadequação das métricas convencionais de avaliação de Geração de Linguagem Natural (NLG) para avaliar com exatidão a qualidade do texto produzido por modelos de linguagem, especialmente em um cenário onde as expectativas e os critérios de avaliação estão em constante mudança. As métricas tradicionais, como BLEU e ROUGE, não conseguem capturar sutilezas semânticas e a qualidade do conteúdo, resultando em uma correlação insuficiente com as avaliações humanas. Métricas baseadas em modelos de Deep Learning, como BertScore e BartScore, foram propostas para resolver esse problema, mas ainda são insuficientes para a avaliação de escopos mais amplos, como os de NLG em LLMs.

O BertScore, por exemplo, é uma métrica válida para tarefas específicas de NLG, mas não é ideal para casos envolvendo LLMs, pois avalia a qualidade do texto gerado calculando a distância de cosseno entre a sentença gerada e a sentença de referência, o que exige dados anotados para avaliação, limitando assim o seu escopo de aplicação.

Além disso, há uma demanda urgente por dados de avaliação de alta qualidade e em grande quantidade, que incluam uma ampla gama de tarefas de NLG e técnicas de avaliação, particularmente para idiomas de baixo recurso e novos contextos de tarefa.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta? 

Os autores analisam diferentes abordagens que envolvem o uso de LLMs como avaliadores e as comparam utilizando um sistema de prós e contras. As metodologias baseadas em LLMs são categorizadas em quatro tipos principais: **métricas derivadas de LLMs**, **prompting de LLMs**, **fine-tuning de LLMs** e **avaliação colaborativa humano-LLM**.  
Essa nova perspectiva busca aproveitar as capacidades avançadas dos LLMs para realizar avaliações mais robustas e alinhadas ao julgamento humano, superando as limitações das abordagens tradicionais.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?
1.  **Métricas Derivadas de LLMs**:
    
    -   **Métricas Baseadas em Embeddings**: Utilizam representações semânticas para calcular a similaridade entre textos. Por exemplo, o BERTScore mede a qualidade do texto com base na similaridade semântica.
    -   **Métricas Baseadas em Probabilidades**: Avaliam a qualidade do texto com base na probabilidade de sua geração por um modelo. O BARTScore é um exemplo que compara a probabilidade condicional do texto gerado.
2.  **Prompting de LLMs**:
    
    -   Esta abordagem envolve a formulação de prompts que guiam os LLMs na avaliação, onde as instruções e o texto a ser avaliado são apresentados juntos. Os resultados são gerados diretamente pelos modelos.
3.  **Fine-tuning de LLMs**:
    
    -   Modelos pré-treinados são ajustados com dados rotulados específicos para melhorar suas capacidades de avaliação em tarefas específicas.
4.  **Avaliação Colaborativa Humano-LLM**:
    
    -   Combina as forças dos avaliadores humanos e dos LLMs, permitindo uma avaliação mais rica e detalhada.


# Como foi avaliado?

O artigo utiliza uma abordagem metodológica abrangente para avaliar as diferentes técnicas discutidas. Os passos metodológicos incluem:

-   **Revisão da Literatura**: Uma análise detalhada da literatura existente sobre a avaliação de NLG utilizando LLMs.
-   **Comparação de Métodos**: Os autores comparam as quatro categorias principais de avaliação, discutindo suas vantagens e desvantagens.
-   **Métricas Utilizadas**: As principais métricas incluem a correlação com avaliações humanas, eficiência computacional e robustez sob ataques adversariais.
-   **Natureza dos Dados**: O artigo se concentra em dados textuais gerados por modelos NLG e em suas respectivas avaliações por humanos. Para cada uma das abordagens, os dados divergem em nível de idioma e estrutura.

# Quais são os resultados?
Os resultados indicam que os métodos baseados em LLMs demonstram uma correlação significativamente maior com as avaliações humanas quando comparados às métricas tradicionais. O prompting de LLMs continua sendo a métrica mais utilizada entre as quatro principais categorias, embora o artigo aponte que o uso de uma avaliação colaborativa possa funcionar melhor.

Um resultado relevante é o relatório de prós e contras de cada abordagem, sendo eles:

1.  **Métricas Derivadas de LLMs**:
    
    -   **Prós**:
        -   Diferente de muitas métricas tradicionais de NLG, sentenças com diferentes expressões, mas com o mesmo significado, convergem para o mesmo sentido.
    -   **Contras**:
        -   O autor menciona pesquisas que indicam a alta vulnerabilidade dessas métricas em diferentes cenários de estresse, além de experimentações com erros propositais, que não são considerados por essa abordagem.
        -   Essa abordagem consome muito tempo e exige alto poder computacional.
        -   O autor cita estudos que mostram que métricas derivadas de LLMs tendem a ter mais viés social do que métricas tradicionais.
2.  **Prompting de LLMs**:
    
    -   **Prós**:
        -   Possui grande flexibilidade, podendo facilmente alterar os parâmetros de avaliação.
        -   Alta interpretabilidade, sendo capaz de gerar relatórios detalhados para cada avaliação.
    -   **Contras**:
        -   Em casos de comparação, é muito suscetível a viés de posição, onde a ordem de exibição dos textos tende a alterar o resultado.
        -   Em casos de sumarização e comparação, possui viés de linguagem, sendo mais propenso a preferir textos com erros factuais do que textos curtos ou com erros gramaticais.
        -   O autor cita um estudo que demonstra que, em tarefas de ranking, línguas não latinas, como mandarim ou japonês, tendem a obter pontuações mais altas.
3.  **Fine-tuning de LLMs**:
    
    -   **Prós**:
        -   Modelos menores (7B-13B) apresentam desempenho semelhante ao GPT-4.
        -   Possuem boa reprodutibilidade, já que a maioria dos modelos base é open-source.
    -   **Contras**:
        -   Os estudos utilizaram o GPT-4 para gerar as bases, o que fez com que os modelos herdassem viéses presentes nesses dados.
4.  **Avaliação Colaborativa Humano-LLM**:
    
    -   **Prós**:
        -   LLMs podem acelerar o processo de avaliação, permitindo que os humanos se concentrem em aspectos mais complexos, que exigem julgamento humano.
        -   A interação humana pode ajudar a mitigar os viéses dos LLMs, resultando em avaliações mais equilibradas.
        -   Pode ser adaptada para diferentes tipos de tarefas de NLG.
    -   **Contras**:
        -   A necessidade de envolvimento humano ainda pode tornar o processo mais caro e demorado em comparação com métodos totalmente automatizados.
        -   A avaliação ainda pode ser afetada por preconceitos humanos.
        -   Não é facilmente escalável.
# Resenha crítica
O artigo está intrinsecamente ligado às necessidades do projeto no que diz respeito a métodos de avaliação. O fato de destacar pontos positivos e negativos de cada abordagem deixa claras as diferenças entre elas e sua aplicabilidade no mundo real.

Mesmo sendo uma survey, o artigo busca, além de elencar, fazer um comparativo das abordagens sem refazer os experimentos, utilizando unicamente os resultados reportados por cada artigo citado. Isso pode ser problemático devido às características distintas de cada experimento, mesmo quando utilizam a mesma abordagem. O próprio autor ressalta que uma comparação horizontal das soluções não é justa; entretanto, ao longo do texto, ele faz esse tipo de comparação.

Os autores continuam pesquisando o uso de LLMs. Publicações interessantes incluem [Better than Random: Reliable NLG Human Evaluation with Constrained Active Sampling](https://arxiv.org/abs/2406.07967) e [Using Bilingual Knowledge and Ensemble Techniques for Unsupervised Chinese Sentiment Analysis](https://aclanthology.org/D08-1058.pdf).


# Discussão
Muitas conclusões interessantes podem ser retiradas do artigo e de suas citações o que podem guiar discussões interessantes, como por exemplo:
- Usar LLMs para melhorar critérios de avaliação tende a beneficiar o processo como um todo;
- Não há diferença relevante entre o uso de prompting zero-shot e one-shot nos cenários em que há descrição de tarefas e passos de avaliação.
- GPT-3.5 e GPT-4 já atingiram o estado da arte para tarefas de avaliação de qualidade de tradução;
- GPT-3.5 e GPT-4 superam métricas baseadas em encoders para avaliação de ranking;

# O que eu tenho a ver com isso?

As experimentações em bases PT-BR não são mencionadas em nenhum dos artigos citados, o que pode representar um estudo interessante. São descritos meios de amostragem de dados a partir de seeds utilizando LLMs, como o GPT-4; esse método pode ser útil, dado o déficit de bases em PT-BR para avaliação em larga escala.

Não foi relatada nenhuma preocupação com vieses culturais, o que pode ser um desafio para a reprodutibilidade de muitas das técnicas ao serem aplicadas no contexto brasileiro, que apresenta diversas peculiaridades linguísticas, as quais variam dentro do próprio território.

# Replicação

O artigo cita diversos outros estudos. Apenas uma parte deles possui bases de código aberto.
