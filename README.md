Template para guiar a leitura de artigos.

# Metadados

* Título
* Autores
* De que instituições são os autores?
* Onde foi publicado
* Ano de publicação
* link

# Seu resumo

Escreva o resumo **curto** do artigo. Siga esse template  [aqui](https://medium.com/@joaoarthurbm/projeto-de-trabalho-de-conclus%C3%A3o-de-curso-como-escrever-o-resumo-da-proposta-3ee806694797)

# Qual o problema?

Aqui é importante ser claro e conciso sobre o problema que o artigo aborda. Claro, pode haver mais de um ou desdobramentos do mesmo, mas tipicamente é muito claro o problema que os autores estão tentando resolver. Cuidado aqui para não cair na armadilha de responder algo como "um sistema de recomendação para..." ou "um algoritmo para... " ou "construir uma ferramenta para...". Esses não são problemas, são soluções. Problema tipicamente é "lentidão do algoritmo XPTO"; "dificuldade em revisar grandes PRs"; etc.

Exemplo: "Existing policies fail to capture the all-or-nothing property of transactions: all objects requested in parallel must be present in cache, or there will be little performance improvement because latency is dictated by the slowest access."
	
Uma tarefa importante para mostrar que entendeu o problema é explicá-lo com suas próprias palavras e descrever um exemplo. Nesse caso, teríamos algo do tipo: "Tipicamente, estratégias de cache como LRU e LFU são otimizadas para hit rate. Contudo, no caso de transações, pode ser que muitos objetos da transação estejam no cache, mas outros não e, portanto, a latência é ditada por esses que não estão. Veja um exemplo na figura abaixo..."

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta? 

Exemplo: Os autores apresentam uma nova estratégia de cache específica para lidar com transações. Nessa estratégia, a ideia é levar em consideração a natureza "tudo-ou-nada" das transações. Como prova de conceito, é apresentada um sistema de cache de alta performance chamado dtox, que ...

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

Exemplo: os autores agrupam objetos de uma transação utilizando uma análise de grafos acíclicos de dependência, através de uma heurística que funciona da seguinte maneira: ...

# Como foi avaliado?

O importante aqui é deixar claras as questões de pesquisa respondidas e o método científico utilizado. Quais foram os passos metodológicos? que métricas foram utilizadas? que métodos estatísticos foram utilizados para amparar as observações? Qual a natureza dos dados? quantas observações foram utilizadas? etc

# Quais são os resultados?

Descrever de forma sucinta os resultados. Direto ao ponto.

Exemplo: O algoritmo proposto é 3x mais eficiente, em termos de tempo de execução, do que as abordagens similares avaliadas. Além disso, o algoritmo proporcionou um ganhou de 70% de throughput.


# Resenha crítica

Aqui é um espaço para você opinar sobre o artigo e levantar questões importantes para a discussão que você terá sobre ele. São tarefas importantes:
	
* identificar a relação dele com o que você está estudando e como você pode usar/reusar/combinar o que foi feito no artigo com o seu trabalho;
* identificar possíveis ameaças à validade na avaliação;
* identificar se a implementação (quando for o caso), está disponível e se você teve tempo/chance de experimentar com ela;
* identificar possíveis importantes questões não respondidas;
* identificar trabalhos futuros;
* relacionar esse trabalho com outros trabalhos similares/relacionados;
* levantar rapidamente/superficialmente as publicações dos autores e o que eles tem feito.

# Discussão

Deixar aqui os comentários e insights importantes que surgiram durante a discussão do paper com o grupo. 

# O que eu tenho a ver com isso?

* Colocar aqui ideias de trabalhos de pesquisa que podem ser feitas a partir desse trabalho. Por exemplo, experimentar com outra base, estender a análise para outro algoritmo, modelo etc. Colocar também como isso se relaciona com o que você está fazendo ou pretende fazer. O que dá para extrair, comparar, evoluir desse trabalho que tem relação com o seu.

# Replicação

* Onde estão os dados?
* Onde está o código?
* Conseguiu entender/rodar?
* Dá para replicar o experimento/estudo?
