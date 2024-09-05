# Metadados

- Título
- Autores
- De que instituições são os autores?
- Onde foi publicado
- Ano de publicação
- link

# Qual o problema?

Privacy concerns are becoming more evident in most various sectors with recent data breaches and privacy scandals triggering the discussion. Regulations such as EU's General Data Protection Regulation (GDPR) are pressuring organizations to handle the individual's data with reinforced caution, specially PIIs (Personally Identifiable Information), which are informations that can be used to identify an individual. As information systems deal with increasingly large amounts of personal data, to comply with regulations and efficiently increase privacy assurances, it is necessary to develop mechanisms that can not only provide such privacy assurances but also with increased automation and reliability. However there is a lack of such mechanismsms to help organizations in protecting the data.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta?

Recent works have applied machine learning to identify PIIs, but the advances in deep learning present an opportunity to apply deep learning in this task. This work proposes ML and DL models to identify PII in unstructured text data. The models used were Support Vector Machine training using sequential minimal optimization and a LSTM neural network.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

The research used a synthetic email dataset , created using the tool mockaroo. It was created a multi-class dataset with eight classes, the total of created emails was 4796, where 4010 does not contains PIIs, and the other 786 contains PIIs. There were used three models, the model based on support vector machine classifier and two models based on LSTM (using two and three layers respectively).

It was done experiments with binary classification with the both kinds of models (SVM and LSTM) and multi-class classification with SVM. The dataset was splitted into 80% (3837 instances) and 20% (959 instances) for train and test respectively, the dataset was preprocessed and vectorized before being used to train the models.

# Como foi avaliado?

The author used the classic way to evaluate ML models, by calculating accuracy, precision, recall and f1-score.

# Quais são os resultados?

According to the research, all the models have shown promising results, with SVM being the most promising of the models with the highest accuracy level (93.6%), the SVM model also got greater values of precision, recall and f1-score.

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

Deixar aqui os comentários e insights importantes que surgiram durante a discussão do paper com o grupo.

# O que eu tenho a ver com isso?

- Colocar aqui ideias de trabalhos de pesquisa que podem ser feitas a partir desse trabalho. Por exemplo, experimentar com outra base, estender a análise para outro algoritmo, modelo etc. Colocar também como isso se relaciona com o que você está fazendo ou pretende fazer. O que dá para extrair, comparar, evoluir desse trabalho que tem relação com o seu.

# Replicação

- Onde estão os dados?
- Onde está o código?
- Conseguiu entender/rodar?
- Dá para replicar o experimento/estudo?
