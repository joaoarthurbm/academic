Template para guiar a leitura de artigos.

# Metadados

- Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks
- Patrick Lewis, Ethan Perez, Aleksandra Piktus, Fabio Petroni, Vladimir Karpukhin, Naman Goyal, Heinrich Küttler, Mike Lewis, Wen-tau Yih, Tim Rocktäschel, Sebastian Riedel, Douwe Kiela
- Facebook AI Research, University College London, New York University
- Advances in Neural Information Processing Systems 33 (NeurIPS 2020)
- 2020
- [link](https://arxiv.org/pdf/2005.11401.pdf)

# Qual o problema?

LLMs pré-treinados tem mostrado conseguir armazenar conhecimento factual oriundo dos dados em seus parâmetros. No entanto, sua habilidade de acessar e precisamente manipular conhecimento ainda é limitada. Conseguir prover uma origem para as decisões dos modelos, ou seja, fornecer alguma base sólida ou origem para as respostas geradas pelo modelo e atualizar seu conhecimento de mundo ainda é um problema de pesquisa em aberto. Modelos pré-treinados com um mecanismo de acesso à memória não-paramétrica podem superar esse problema, no entanto, foram investigados apenas em problemas de Question Answering de domínio aberto.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta?

Os autores reforçaram os modelos pré-treinados, ou seja, que possuem memória paramétrica com uma memória não-paramétrica através de uma abordagem de fine tuning de propósito geral a qual eles se referem como Retrieval-Augmented Generation (RAG). Eles construíram modelos RAG onde a memória paramétrica é um Transformer Seq2Seq pré-treinado e a memória não-paramétrica é um índice de vetores densos da Wikipedia acessados utilizando um recuperador nerual pré-treinado.

O mecanismo de recuperar documentos retorna os documentos mais relevantes para um dado input, então o modelo Seq2Seq (BART) utiliza esses documentos junto ao input passado para gerar o output. Foi utilizada uma configuração onde ambas os componentes: paramétrico e não-paramétrico são pré-treinados com conhecimento extensivo.

A técnica utilizada é interessante, pois a memória não-paramétrica pode ser atualizada conforme o conhecimento do mundo evolui. Além disso, quando um fine tuning convencional é utilizado, atualizando os pesos do modelo pré-treinado, é possível que o modelo perca parte do conhecimendo adquirido durante o seu pré-treino, no entanto, a técnica do RAG apenas complementa o conhecimento que o modelo já possui.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

Os autores propõe duas formas de marginalizar sobre os documentos recuperados para produzir uma distribuição sobre o texto gerado, são elas o RAG-Token e o RAG-Sentence.

No RAG-Sentence, para cada um dos top K documentos recuperados o gerador produz uma probabilidade da sequência de output que então são marginalizadas.

No RAG-Token, podemos utilizar um documento diferente para cada token alvo, o que permite que o gerador escolher conteúdo de diversos documentos quando produz o output. Os top K documentos são recuperados e o gerador produz uma distribuição para o próximo token do output para cada um dos documentos antes de marginalizar, então repete o processo para o próximo token do output.

O componente recuperador é baseado em Dense Passage Retrieval (DPR) que segue uma arquitetura bi-encoder formada por dois modelos BERT base, um como document encoder e outro como query encoder que buscam os top K documentos com as maiores probabilidades. Esse problema é um MIPS (Maximum Inner Product Search). Foi utilizando um bi-encoder pré-treinado do DPR para inicializar o recuperador e construir o índice de documentos. O recuperador foi treinado para recuperar documentos que contém respostas para questões do TriviaQA.

O componente gerador utilizado foi um BART-large, um transformer Seq2Seq pré-treinado com 400M de parâmetros. Para combinar o input com os documentos recuperados, foi utilizado apenas a concatenação desses conteúdos.

Os componentes recuperador e gerador foram treinados sem nenhuma supervisão direta quanto a qual documento deveria ser recuperado. Dado um corpus de treino com pares (input, output), foi minimizado o marginal negativo log-likelihood de cada alvo usando gradiente descendente estocástico.

# Como foi avaliado?

Os experimentos com RAG foram realizados em knowledge-intensive tasks. Em todos os experimentos foi utilizada a mesma base de documentos da Wikipedia como fonte de conhecimento não-paramétrica. O dump utilizado foi de 2018 e cada artigo da Wikipedia foi quebrado em chunks de 100 palavras formando uma base de 21M de documentos. Foi utilizado um document encoder para computar os embeddings para cada um dos documentos e construir um único índice MIPS.

Open-domain question answering

Questões e respostas foram tratadas como pares textuais de input e output o modelo RAG foi treinado através da minimização do log-likelihood negativo das respostas. O modelo RAG foi comparado com os paradigmas populares de extração para QA, onde as respostas são spans extraídos dos documentos recuperados utilizando apenas memória não-paramétrica. RAG foi comparado também com soluções fechadas de QA, onde as respostas são gerados, mas utilizando apenas o conhecimento paramétrico. Foram considerados 4 open-domain QA datasets: Natural Questions (NQ), TriviaQA (TQA), WebQuestions (WQ) e CuratedTrec (CT). Como CT e WQ são pequenos foi utilizado DPR inicializando os modelos de CT e WQ com o NQ RAG.

Abstractive Question Answering

Para testar a geração de linguagem natural do RAG foi utilizada uma task que consiste de questões, 10 passagens de ouro recuperadas de uma engine de busca para cada questão e uma sentença de resposta completa.

# Quais são os resultados?

Descrever de forma sucinta os resultados. Direto ao ponto.

Exemplo: O algoritmo proposto é 3x mais eficiente, em termos de tempo de execução, do que as abordagens similares avaliadas. Além disso, o algoritmo proporcionou um ganhou de 70% de throughput.

# Resenha crítica

Aqui é um espaço para você opinar sobre o artigo e levantar questões importantes para a discussão que você terá sobre ele. São tarefas importantes:

- identificar a relação dele com o que você está estudando e como você pode usar/reusar/combinar o que foi feito no artigo com o seu trabalho;
- identificar possíveis ameaças à validade na avaliação;
- identificar se a implementação (quando for o caso), está disponível e se você teve tempo/chance de experimentar com ela;
- identificar possíveis importantes questões não respondidas;
- identificar trabalhos futuros;
- relacionar esse trabalho com outros trabalhos similares/relacionados;
- levantar rapidamente/superficialmente as publicações dos autores e o que eles tem feito.

# Discussão

Deixar aqui os comentários e insights importantes que surgiram durante a discussão do paper com o grupo. Colocar aqui ideias de trabalhos de pesquisa que podem ser feitas a partir desse trabalho. Por exemplo, experimentar com outra base, estender a análise para outro algoritmo, modelo etc.

# Replicação

- Onde estão os dados?
- Onde está o código?
- Conseguiu entender/rodar?
- Dá para replicar o experimento/estudo?
