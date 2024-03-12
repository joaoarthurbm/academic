Template para guiar a leitura de artigos.

# Metadados

- Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks
- Patrick Lewis, Ethan Perez, Aleksandra Piktus, Fabio Petroni, Vladimir Karpukhin, Naman Goyal, Heinrich Küttler, Mike Lewis, Wen-tau Yih, Tim Rocktäschel, Sebastian Riedel, Douwe Kiela
- Facebook AI Research, University College London, New York University
- Advances in Neural Information Processing Systems 33 (NeurIPS 2020)
- 2020
- [link](https://arxiv.org/pdf/2005.11401.pdf)

# Qual o problema?

LLMs pré-treinados tem mostrado conseguir armazenar conhecimento factual oriundo dos dados em seus parâmetros. No entanto, sua habilidade de acessar e precisamente manipular conhecimento ainda é limitada. Conseguir prover uma origem para as decisões dos modelos, ou seja, fornecer alguma base sólida ou origem para as respostas geradas pelo modelo e atualizar seu conhecimento de mundo ainda é um problema de pesquisa em aberto. Além disso, os modelos pré-treinados são muito generalistas e precisam de mais contexto para solucionar melhor os problemas. Modelos pré-treinados com um mecanismo de acesso à memória não-paramétrica podem superar esse problema, no entanto, foram investigados apenas em problemas de Question Answering de domínio aberto.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta?

Os autores reforçaram os modelos pré-treinados, ou seja, que possuem memória paramétrica com uma memória não-paramétrica através de uma abordagem de fine tuning de propósito geral a qual eles se referem como Retrieval-Augmented Generation (RAG). Eles construíram modelos RAG onde a memória paramétrica é um Transformer Seq2Seq pré-treinado e a memória não-paramétrica é um índice de vetores densos da Wikipedia acessados utilizando um recuperador nerual pré-treinado.

O mecanismo de recuperar documentos retorna os documentos mais relevantes para um dado input, então o modelo Seq2Seq (BART) utiliza esses documentos junto ao input passado para gerar o output. Foi utilizada uma configuração onde ambas os componentes: paramétrico e não-paramétrico são pré-treinados com conhecimento extensivo.

A técnica utilizada é interessante, pois a memória não-paramétrica pode ser atualizada conforme o conhecimento do mundo evolui. Além disso, quando um fine tuning convencional é utilizado, atualizando os pesos do modelo pré-treinado, é possível que o modelo perca parte do conhecimendo adquirido durante o seu pré-treino, no entanto, a técnica do RAG apenas complementa o conhecimento que o modelo já possui.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

Conceito importante: marginalizar consiste em somar as probabilidades condicionais variando os valores de uma variável para entender a contribuição marginal.

Os autores propõe duas formas de marginalizar sobre os documentos recuperados para produzir uma distribuição sobre o texto gerado, são elas o RAG-Token e o RAG-Sequence.

No RAG-Sequence, para cada um dos top K documentos recuperados o gerador produz uma probabilidade da sequência de output que então são marginalizadas.

No RAG-Token, podemos utilizar um documento diferente para cada token alvo, o que permite que o gerador escolher conteúdo de diversos documentos quando produz o output. Os top K documentos são recuperados e o gerador produz uma distribuição para o próximo token do output para cada um dos documentos antes de marginalizar, então repete o processo para o próximo token do output.

O componente recuperador é baseado em Dense Passage Retrieval (DPR) que segue uma arquitetura bi-encoder formada por dois modelos BERT base, um como document encoder e outro como query encoder que buscam os top K documentos com as maiores probabilidades. Esse problema é um MIPS (Maximum Inner Product Search). Foi utilizando um bi-encoder pré-treinado do DPR para inicializar o recuperador e construir o índice de documentos. O recuperador foi treinado para recuperar documentos que contém respostas para questões do TriviaQA.

O componente gerador utilizado foi um BART-large, um transformer Seq2Seq pré-treinado com 400M de parâmetros. Para combinar o input com os documentos recuperados, foi utilizado apenas a concatenação desses conteúdos.

Os componentes recuperador e gerador foram treinados sem nenhuma supervisão direta quanto a qual documento deveria ser recuperado. Dado um corpus de treino com pares (input, output), foi minimizado o marginal negativo log-likelihood de cada alvo usando gradiente descendente estocástico.

# Como foi avaliado?

Os experimentos com RAG foram realizados em knowledge-intensive tasks. Em todos os experimentos foi utilizada a mesma base de documentos da Wikipedia como fonte de conhecimento não-paramétrica. O dump utilizado foi de 2018 e cada artigo da Wikipedia foi quebrado em chunks de 100 palavras formando uma base de 21M de documentos. Foi utilizado um document encoder para computar os embeddings para cada um dos documentos e construir um único índice MIPS.

Open-domain question answering

Questões e respostas foram tratadas como pares textuais de input e output o modelo RAG foi treinado através da minimização do log-likelihood negativo das respostas. O modelo RAG foi comparado com os paradigmas populares de extração para QA, onde as respostas são spans extraídos dos documentos recuperados utilizando apenas memória não-paramétrica. RAG foi comparado também com soluções fechadas de QA, onde as respostas são gerados, mas utilizando apenas o conhecimento paramétrico. Foram considerados 4 open-domain QA datasets: Natural Questions (NQ), TriviaQA (TQA), WebQuestions (WQ) e CuratedTrec (CT). Como CT e WQ são pequenos foi utilizado DPR inicializando os modelos de CT e WQ com o NQ RAG.

Abstractive Question Answering

Para testar a geração de linguagem natural do RAG foi utilizada uma task que consiste de questões, 10 passagens de ouro recuperadas de uma engine de busca para cada questão e uma sentença de resposta completa. Para tratar a task como uma abstractive QA task, foram utilizadas apenas as perguntas e respostas.

Jeopardy Question Generation

Para avaliar o RAG em uma configuração non-QA, foi estudado um domínio aberto de geração de questões Jeopardy. Jeopardy é um formato não usual que consiste em tentar adivinhar uma entidade por um fato sobre aquela entidade. Questões Jeopardy são precisos e factuais, logo gerar Questões Jeopardy condicionadas a suas entidades de resposta é uma knowledge-intensive task. Os dados do SearchQA foram divididos em 100K para treino, 14K para dev e 27K para testes. O modelo BART foi treinado para comparação e o modelo foi avaliado usando a métrica SQuAD-tuned Q-BLEU-1. Além disso, foram realizadas duas avaliações humanas: uma para verificar se uma sentença pode ser corroborada com fontes externas confiáveis e outra para avaliar a dependência mútua entre o input e o output.

Fact verification

Verificar fatos e decidir se eles são suportados ou refutados por documentos recuperados da Wikipedia, ou mesmo se não há informação suficiente para decidir. É uma tarefa interessante para veirificar a capacidade do RAG de classificação e não de geração. As classes suportado, refutado e infomação insuficiente foram mapeadas para tokens e então o modelo foi treinado com pares de sentenças e classes. Os autores não utilizaram supervisão sobre os documentos recuperados, pois em muitos casos do mundo real essas labels não estão disponíveis. Foram exploradas duas variantes do modelo: uma com todas as três classes e outra com apenas duas classes (suportado e refutado).

# Quais são os resultados?

Open-domain question answering

Nos dataset testados, o RAG alcançou resultados de estado da arte em todos sem um custo alto de pré-treino. Existem vantagens em gerar a respostas mesmo quando é possível extrair elas, pois documentos com pistas sobre as respostas, mas que não contém a resposta em si, ainda assim podem contribuir para gerar uma resposta correta. Um resultado foi de que o modelo tem uma acurácia de 11.8% quando a resposta correta não está em nenhum dos documentos recuperados, enquanto um modelo de extração teria uma acurácia de 0%.

Abstractive Question Answering

RAG-Sequence supera o BART em Open MS-MARCO NLG por 2.6 Bleu points e 2.6 Rouge-L points e alcança performance de estado da arte considerando que algumas perguntas não podem ser respondidas sem as gold passages e que nem todas as questões podem ser respondidas apenas com conhecimento da Wikipedia.

Jeopardy Question Generation

RAG-Token teve desempenho melhor que RAG-Sequence na geração de questões Jeopardy e ambos superaram o BART na métrica Q-BLEU-1. A avaliação humana descobriu que em mais de 452 pares gerados pelo BART e RAG-Token, apenas em 7.1% dos casos o BART foi melhor que o RAG, enquanto RAG foi melhor que o BART em 42.7% e ambos os modelos tiveram bons resultados em 17% dos casos, mostrando a eficiência do RAG em relação um modelo de geração de estado da arte. Avaliadores entenderam as gerações do RAG mais específicas por uma grande margem.

Fact Verification

Para a 3-way classification, RAG alcançou 4.3% dos modelos estado da arte. Para 2-way classification, ele foi comparado com o trabalho realizado em "Elastic weight consolidation for better bias inoculation", onde o modelo foi treinado para classificar a sentença como verdadeira ou falsa dada a sentença de ouro. RAG conseguiu uma acurácia com 2.7% desse modelo.

# Resenha crítica

De maneira geral achei o artigo bastante complexo e difícil de acompanhar, e apesar de ter entendido a ideia geral do artigo, ao meu ver esse artigo precisa de um background muito bom para entender com mais segurança. Como se trata de uma forma de melhorar o desempenho de modelos LLMs usando contexto para dar mais infornações ao modelo, é um tema bem relevante para os estudos e experimentos dos modelos.

Achei que a avaliação do modelo foi explicada de maneira superficial.

# Discussão

Deixar aqui os comentários e insights importantes que surgiram durante a discussão do paper com o grupo. Colocar aqui ideias de trabalhos de pesquisa que podem ser feitas a partir desse trabalho. Por exemplo, experimentar com outra base, estender a análise para outro algoritmo, modelo etc.

# Replicação

- Onde estão os dados? Eles utilizaram dados da Wikipedia, mas não especificaram como recuperar
- Onde está o código? Foi feita uma release na biblioteca HuggingFace e o código pode ser encontrado no GitHUb do HuggingFace
- Conseguiu entender/rodar? Não houve tempo para estudar o código e executar experimentos ainda, mas como está disponível no HuggingFace, devemos conseguir executar com a API da biblioteca
- Dá para replicar o experimento/estudo? Como não há informações suficientes sobre os dados e como recuperá-los da Wikipedia provavelmente não com os mesmo dados, mas como o modelo está disponível no HuggingFace, então podemos rodar com outros dados
