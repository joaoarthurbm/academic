# Metadados

* tinyBenchmarks: evaluating LLMs with fewer examples
* Felipe Maia Polo, Lucas Weber, Leshem Choshen, Yuekai Sun, Gongjun Xu, Mikhail Yurochkin
    - Department of Statistics, University of Michigan, USA
    - Department of Translation and Language Sciences, University of Pompeu Fabra, Spain 
    - IBM Research
    - MIT 
    - MIT-IBM Watson AI Lab. 
* INTERNATIONAL CONFERENCE ON MACHINE LEARNING
* 2024
* [Article](https://arxiv.org/pdf/2402.14992)

# Qual o problema?

Para que possamos considerar uma LLM como sendo eficiente e promissora, é necessário realizar avaliações sobre o texto que é gerado pelo modelo. Atualmente, é muito comum que essas avaliações sejam feitas através de _datasets_ de _benchmark_, porém esses conjuntos de dados geralmente são muito grandes o que torna a avaliação dos modelos muito custosa.

Diante disso, uma ideia proposta é de que não seja necessário ter milhares de exemplos de testes para avaliar uma LLM, mas sim um conjunto menor, com cerca de centenas de exemplos, buscando manter a qualidade das avaliações com um custo computacional bem reduzido.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta? 

O objetivo principal é encontrar a menor quantidade possível de exemplos que ainda permita estimar o desempenho de um novo modelo de LLM de forma precisa. Ou seja, ao invés de avaliar o modelo em todos os exemplos do benchmark (o que seria custoso), a ideia é escolher de maneira inteligente um subconjunto desses exemplos que seja suficiente para garantir que a avaliação continue sendo representativa. Dessa forma, a avaliação do LLM pode ser realizada de maneira mais eficiente, reduzindo o tempo e o custo de processamento, sem comprometer significativamente a qualidade da avaliação.

Os autores propõem uma nova metodologia para otimizar a avaliação de LLMs em benchmarks grandes e variados. A metodologia combina técnicas de **amostragem estratificada** e **agrupamento (clustering)** para escolher exemplos representativos de diferentes subcenários, minimizando a quantidade de exemplos necessários para avaliar um LLM sem comprometer a precisão. Além disso, eles utilizam a **Teoria de Resposta ao Item (IRT)** para ajustar e melhorar a estimativa do desempenho com base nas respostas dos modelos a esses exemplos selecionados. Essa metodologia oferece uma maneira eficiente de realizar avaliações com menos custo computacional, mantendo a qualidade dos resultados.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

A solução se baseia no uso de técnicas como:

- Métodos de amostragem e agrupamento:
    - Random Stratified Sampling: separa os exemplos dos benchmarks de maneira aleatória em grupos e os seleciona de forma proporcional, buscando garantir uma quantidade justa para cada cenário. 
    - Clustering: os exemplos são colocados em grupos de características semelhantes. Nesse caso, os exemplos são agrupados com base nos padrões de acerto e erro observados em modelos de treinamento anteriores. Durante o processo são definidos alguns _pontos âncora_. Esses pontos (exemplos) são aqueles em que o desempenho do modelo indicaria como ele se sairia em exemplos semelhantes, reduzindo a necessidade de avaliar todos os exemplos do benchmark.
- Teoria de Resposta ao Item:
    - Usada em duas frentes, sendo uma para separar exemplos de acordo com sua dificuldade e as habilidades exigidas dos modelos, que teve como resultado a definição dos pontos âncora; e a outra sendo para modelar a probabilidade de uma LLM responder um exemplo do benchmark com base na habilidade estimada e na dificuldade da tarefa.
    - Tanto a habilidade quanto a dificuldade da tarefa são ajustadas durante o treinamento dos modelos IRT.
    - p-IRT: é uma versão adaptada do IRT que foi usada para estimar o desempenho de uma LLM em exemplos que não foram diretamente avaliados considerando as respostas que já foram obtidas.
        - Ex: Imagine que você quer descobrir se um aluno passaria em uma prova com 100 questões, mas ele só respondeu 20 delas até agora. O p-IRT observa as respostas que ele já deu e faz uma previsão de quantas das 80 perguntas restantes ele provavelmente acertaria, com base nas suas habilidades até o momento e na dificuldade das perguntas.
    - gp-IRT: é uma versão mais avançada do p-IRT. Esse método combina as respostas dadas pela LLM com as previsões do p-IRT (como provavelmente o modelo responderias às perguntas que ele ainda não viu) e busca equilibrar essas duas fontes de informação para tentar melhorar a precisão da previsão. Esse equilibrio é feito com base na quantidade de respostas já feitas pela LLM. 
        - Ex: Considerando o aluno que respondeu apenas 20 das 100 questões: o gp-IRT combina as respostas que o aluno já deu com as previsões sobre as outras 80 questões (feitas pelo p-IRT). Se o aluno respondeu muitas perguntas até agora, o gp-IRT vai confiar mais nas respostas reais. Se ele respondeu poucas, vai confiar mais nas previsões.


# Como foi avaliado?

Coletaram-se dados de desempenho de vários LLMs que já haviam sido avaliados em benchmarks como Open LLM Leaderboard, MMLU, HELM e AlpacaEval 2.0.

Foram criados conjuntos de exemplos usando as técnicas de amostragem mencionadas anteriormente.

Separaram os modelos em dois grupos: Uma abordagem dividiu modelos aleatoriamente entre splits de treino e teste e outra abordagem usou os modelos mais recentes como conjunto de teste, representando melhor a aplicação prática do método em novos LLMs.

O desempenho das LLMs foi estimado considerando os dados dos grupos gerados através das amostragens. Existem 3 formas de amostragem simples que são:

- **random** (amostragem aleatória estratificada),
- **correctness** (agrupamento com base no acerto dos modelos no conjunto de treino)
- **IRT** (agrupamento das representações dos exemplos obtidas a partir do modelo IRT ajustado no conjunto de treino).

Para cada estratégia, tem-se uma variação "++", que ajusta essa estimativa usando o modelo IRT. Os grupos contem cerca de 100 exemplos por cenário. Os resultados foram comparados ao desempenho completo dos modelos em todos os exemplos do benchmark.

A métrica principal que usada foi a diferença percentual entre o desempenho real de um LLM e a previsão dos modelos usando o exemplos das amostras.


# Quais são os resultados?

De acordo com o artigo, as estratégias propostas são eficazes para reduzir os custos de avaliação. Foi possível identificar que as melhores estratégias de avaliação alcançam um erro de estimativa inferior a 2% em todos os benchmarks, com apenas 100 exemplos ou menos por cenário. 

Um ponto importante é que mesmo considerando uma grande diferença entre a data de existência dos modelos as estratégias ainda funcionam bem para ambos, ou seja, as torna aplicáveis em cenários futuros.

Além disso, todos os métodos baseados em IRT, especialmente as variações com IRT++ (gp-IRT), tiveram desempenho consistente em todos os benchmarks e divisões de teste-treino.

Todos os resultados foram médias calculadas sobre cinco execuções para garantir que as estimativas fossem robustas e consistentes, não dependendo de uma única execução específica.

# Resenha crítica

Esse artigo está relacionado com avaliações de LLMs, mais especificamente em estratégias para diminuir a quantidade de exemplos necessários para conseguir avaliar bem o desempenho de um modelo. 

Um ponto interessante seria tentar replicar alguma dessas estratégias quando formos iniciar as avaliações dos modelos, pois apesar de todos os benchmarks serem em inglês, as estratégias não dependem do idioma encontrado nos dados, o que permitiria que pudéssemos reutilizar a ideia.

Os autores disponibilizaram a implementação desse estudo no github, considerando código para replicar o processo e também o que eles chamaram de *tinydatasets*, que já são conjuntos de dados menores de benchmarks grandes.

# O que eu tenho a ver com isso?

Acredito que a ideia principal seria tentar replicar esse processo usando benchmarks para pt-BR. Como tem o código disponível, talvez seja possível mudar apenas a fonte dos dados e rodar. Se conseguirmos usar a quantidade de dados sugeridos pelo artigo (cerca de 100 exemplos por cénario) para avaliar o desempenho de uma LLM, com certeza economizaríamos bastante custo computacional e tempo de execução.

# Replicação

Todo processo descrito no artigo está implementado e disponibilizado em [tinyBenchmarks](https://github.com/felipemaiapolo/tinyBenchmarks) no GitHub.