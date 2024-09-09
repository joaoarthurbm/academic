# Metadados

- **Title:** Privacy-Preserving PII Label Detection Using Machine Learning
- **Autores:** Jaikishan Jaikumar, Mohana and Pavankumar Suresh
- **Researches Institution:** RV College of Engineering and VIT Vellore
- **Where it was published:** 15th International Conference on COMmunication Systems & NETworkS (COMSNETS)
- **Year of publication:** 2023
- [link](https://ieeexplore.ieee.org/document/10041388)

# Qual o problema?

In the digital age, where data has become a central driver of numerous aspects of our lives, safeguarding PIIs (Personally Identifiable Information), which are informations that can be used to identify an individual, has emerged as a critical concern. Unauthorized exposure os misuse of this kind of data can result in severe privacy breaches, identify theft, and other consequences, so it is important to safeguard this informations, even to follow regulations such as the General Data Protection Regulation (GDPR). The primary objective of PII label identification is to develop models capable of identifying and labelling PII. In order to create these models it is used Machine Learning and NLP techniques. The objective of the paper is to exhibit a novel methodology for detecting and labelling PII in a privacy-preserving manner using ML.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta?

This work trains classic Machine Learning models such as Support Vector Machine (SVM), Gaussian Nayve Bayes and Random Forest fot the task of PII identification and labelling, and reinforce the results by using regular expressions (regex) in the end of the proposed pipeline.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

The initial step was collecting the data, in order to perform this task, the authors used the python library faker to generate synthetic data of various types, in the end of this step they had a dataset composed of 70K lines, where they generated 10K lines for each type of PII they used in their research. After this step, there was a preprocessing step where they perform tasks such as tokenization, remving stopwords, stemming, lemmatization and entity recognition. The next two steps were applying TF-IDF vectorization and SMOTE to deal with imbalanced data respectively, followed by training the models (SVM, Random Forest and Gaussian Nayve Bayes) with a 20% portion for test. In the end of the pipeline it was used regular expressions to enhance the performance metrics.

# Como foi avaliado?

The author used the classic way to evaluate ML models, by calculating accuracy. They did not mention any other metrics.

# Quais são os resultados?

According to the paper the model with the best results was Random Forest, reaching to 96.6% fo accuracy and 95.91% of cross validation score, which indicates a good generalization capability. The Random Fortest model also has the lowest standard deviation (0.0051), which means it is stable and robust.

# Resenha crítica

This article is relevant in the context of PII identification in unstructured text, which is probably the main goal of my future research, to train a model to perform this task considering Brazillian data.

My research can be a future work, by trying to use the same models over Brazillian PIIs, but since we are seeing the boom of LLMs, it can be another possible path for the research.

The methodology was very simple, the author just executed the models with 20% of the dataset being destinated for the testing stage and evaluate the results only with accuracy. I believe that they could have used others metrics to enhance the evaluation section, and they also could have detailed more how they conduct the experiment, for instance, they did not talk about the format of the data they generated.

# Discussão

Deixar aqui os comentários e insights importantes que surgiram durante a discussão do paper com o grupo. [TODO]

# O que eu tenho a ver com isso?

The used methodology was simple, but we could verify if it is possible to use the same tool to generate data, since private data is not available on the internet.

# Replicação

- The data used was not found
- The code used was not Found
- Since the code of the models used is apparently easy to replicate, we could try replicate the methodology with another dataset.
