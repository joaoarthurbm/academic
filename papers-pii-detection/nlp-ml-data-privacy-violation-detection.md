# Metadados

- **Title:** Using NLP and Machine Learning to Detect Data Privacy Violations
- **Autores:** Paulo Silva, Carolina Gonçalves, Carolina Godinho, Nuno Antunes, Marilia Curado
- **Researches Institution:** Department of Informatics Engineering, University of Coimbra
- **Where it was published:** IEEE Conference on Computer Communications Workshops, INFOCOM Wksps
- **Year of publication:** 2020
- [link](https://ieeexplore.ieee.org/abstract/document/9162683)

# Qual o problema?

Privacy concerns are becoming more evident in most various sectors with recent data breaches and privacy scandals triggering the discussion. Regulations such as EU's General Data Protection Regulation (GDPR) are pressuring organizations to handle the individual's data with reinforced caution, specially PIIs (Personally Identifiable Information), which are informations that can be used to identify an individual. As information systems deal with increasingly large amounts of personal data, to comply with regulations and efficiently increase privacy assurances, it is necessary to develop mechanisms that can not only provide such privacy assurances but also with increased automation and reliability. However there is a lack of such mechanisms to help organizations in protecting the data.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta?

As it was said previously, individual's personal data should be autonomously and effectively monitored not only because of its nature, but also its size when considering big data. As the data can be released in and unstructured format, like text, the usage ML models and NLP is naturally elegible for the task, specially NER (Named Entity Recognition). The work proposes and evaluate the usage of NER to identify, monitor and validate PIIs. The author used three well-known NLP tools in his experiment (NLTK, Stanford CoreNLP and spaCy).

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

The methodology to determine to which extent NLP and NER can effectively be used to reliably detect and identify PII was divided in three parts:

The first part used Generic data already tagged with named entities that was found in Kaggle. In order to evaluate the performance of the tools and its models the data was partitioned in smaller chunks, in way that made possible to evaluate how the dataset size impact the models. The dataset had 1.354.149 tokens (can be words, ponctuations or numbers) and was sliced in portions (5%, 10%, 20%, 30%, 40%, 50%, 60%, 70%, 80%, 90% and 100%). The experiment was executed with all the portions, and each one of them was divided in train and test with a portion of 30% to test.

The second part had an identical procedure to the first part, but with another dataset. This time, the dataset was built out of publicly available data containing PII, like contracts available in online sites and contracts from the U.S Department of Defense (DoD). After retrieving the contracts as PDF files, it was necessary to extract the information and converting it to text. Finally it was possible to tokenize the text and perform manual tagging of entities, with 68% of the entities in the dataset being tagged during the manual tagging process.

The third part also had an identical procedure, but mixing datasets, additionally using U.S voters' registration data the author built a dataset composed of 120K lines of voters' data and 50K lines of the generic dataset. The main goal was to address the generalization capabilities of the models. The datasets used in train and validation steps were different, for instance, models trained with generic datasets were validated with context-specific datasets.

# Como foi avaliado?

The author used the classic way to evaluate ML models, by identifying the number of True Positives (TP), True Negatives (TN), False Positives (FP) and False Negatives (FN). Then used this information to calculate accuracy, precision, recall and f1-score.

# Quais são os resultados?

Using the entire generic dataset the Stanford CoreNLP and spaCy obtained the best results: 0.84 and 0.86 values of f1-score respectively. The amount of time needed for training Stanford CoreNLP and spaCy was 120 and 2000 minutes respectively. The worst result was from NLTK with 0.67 of f1-score, but it was the fastest model, training in 75 seconds.

Using the public available data with PII, the Stanford CoreNLP and spaCy reached the best results, that was approximately 0.90 of f1-score. It was necessary a great amount of time to train the models. The greatest time of training was 6500 seconds with spaCy. The less positive aspect was the time necessary to hand-labeling the data before fedding it to the model, each document took an average of 4.75 hours of work. One of the results is that the models perform similarly regardless of having generic or PII-specific content.

Using the mixed dataset, the only tool used was spaCy, since it was the only one that supported re-training. The results were not good when validating with 20% of the generic dataset. Using a validation dataset that resembles more to the re-training dataset shows better results.

# Resenha crítica

I could not understand quite well the results of the execution of the models over the mixed dataset, because the author explains that the only model used was spaCy, because it was the only one that supports re-training, but I could not find in teh article other place where they talk about re-train models.

They could have detailed more how was the process of labelling the data and the final format of the data, in order to make it easier to replicate.

This article is relevant in the context of PII identification in unstructured text, which is probably the main goal of my future research, to train a model to perform this task considering Brazillian data. I believe that the experiment methodology can be re-used in a future experiment during my own research.

My research can be a future work, by trying to use the same methodology, maybe even the same models over Brazillian PIIs, but since we are seeing the boom of LLMs, it can be another possible path for the research.

We could search sources of public available data, as the authors have done in their research.

# Discussão

Deixar aqui os comentários e insights importantes que surgiram durante a discussão do paper com o grupo. [TODO]

# O que eu tenho a ver com isso?

I believe that the methodoloy can be re-used in my own research in order to train models to detect Brazillian PIIs in unstructured text.

# Replicação

- The data used was not found
- The code used was not Found
- Since the code of the models used is apparently easy to replicate, we could try replicate the methodology with another dataset.
