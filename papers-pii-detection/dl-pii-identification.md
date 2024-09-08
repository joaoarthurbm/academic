# Metadados

- **Title:** Deep Learning Application - Identifying PII (Personally Identifiable Information) to Protect
- **Autores:** Anil K. Makhija
- **Researches Institution:** Ohio State University and Fisher College of Business
- **Where it was published:** Journal of Accounting, Finance, Economics, and Social Sciences
- **Year of publication:** 2020
- [link](https://cam-ed.edu.kh/wp-content/uploads/2024/04/2_Deep-Learning-Application-Identifying-PII.pdf)

# Qual o problema?

Privacy concerns are becoming more evident in most various sectors with recent data breaches and privacy scandals triggering the discussion. Regulations such as EU's General Data Protection Regulation (GDPR) are pressuring organizations to handle the individual's data with reinforced caution, specially PIIs (Personally Identifiable Information), which are informations that can be used to identify an individual. As information systems deal with increasingly large amounts of personal data, to comply with regulations and efficiently increase privacy assurances, it is necessary to develop mechanisms that can not only provide such privacy assurances but also with increased automation and reliability. However there is a lack of such mechanisms to help organizations in protecting the data.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta?

Recent works have applied machine learning to identify PIIs, but the advances in deep learning present an opportunity to apply deep learning in this task. This work proposes ML and DL models to identify PII in unstructured text data. The models used were Support Vector Machine training using sequential minimal optimization and a LSTM neural network.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

The research used a synthetic email dataset, created using the tool mockaroo. It was created a multi-class dataset with eight classes, the total of created emails was 4796, where 4010 does not contains PIIs, and the other 786 contains PIIs. There were used three models, the model based on support vector machine classifier and two models based on LSTM (using two and three layers respectively).

It was done experiments with binary classification with the both kinds of models (SVM and LSTM) and multi-class classification with SVM. The dataset was splitted into 80% (3837 instances) and 20% (959 instances) for train and test respectively, the dataset was preprocessed and vectorized before being used to train the models.

# Como foi avaliado?

The author used the classic way to evaluate ML models, by calculating accuracy, precision, recall and f1-score.

# Quais são os resultados?

According to the research, all the models have shown promising results, with SVM being the most promising of the models with the highest accuracy level (93.6%), the SVM model also got greater values of precision, recall and f1-score. All the models reached accuracy values between 93 and 94 percent.

# Resenha crítica

This article is relevant in the context of PII identification in unstructured text, which is probably the main goal of my future research, to train a model to perform this task considering Brazillian data.

My research can be a future work, by trying to use the same models over Brazillian PIIs, but since we are seeing the boom of LLMs, it can be another possible path for the research.

The methodology was very simple, the author just executed the models with 20% of the dataset being destinated for the testing stage and evaluate the results with classic metrics like accuracy.

# Discussão

Deixar aqui os comentários e insights importantes que surgiram durante a discussão do paper com o grupo. [TODO]

# O que eu tenho a ver com isso?

The used methodology was simple, but we could verify if it is possible to use the same tool to generate data, since private data is not available on the internet.

# Replicação

- The data used was not found
- The code used was not Found
- Since the code of the models used is apparently easy to replicate, we could try replicate the methodology with another dataset.
