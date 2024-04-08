
# Observações

Este documento não é um resumo de um artigo específico, mas sim uma exploração dos tópicos relacionados à temática da "Semantic Search". Como tal, o modelo adotado será personalizado para melhor se adequar ao contexto em questão.


# Referências 

* BERNERS-LEE, Tim; HENDLER, James; LASSILA, Ora. A new form of Web content that is meaningful to computers will unleash a revolution of new possibilities. Scientific american, v. 284, n. 5, p. 34-43, 2001.

* GUHA, Ramanathan; MCCOOL, Rob; MILLER, Eric. Semantic search. In: Proceedings of the 12th international conference on World Wide Web. 2003. p. 700-709.

* MÄKELÄ, Eetu. Survey of semantic search research. In: Proceedings of the seminar on knowledge management on the semantic web. Department of Computer Science, University of Helsinki, Helsinki, 2005.

* KASSIM, Junaidah Mohamed; RAHMANY, Mahathir. Introduction to semantic search engine. In: 2009 International Conference on Electrical Engineering and Informatics. IEEE, 2009. p. 380-386.

* RENTERIA-AGUALIMPIA, Walter et al. Exploring the advances in semantic search engines. In: Distributed Computing and Artificial Intelligence: 7th International Symposium. Springer Berlin Heidelberg, 2010. p. 613-620.


# Qual o problema?

A diferença na comunicação entre seres humanos e computadores apresenta um desafio significativo para a eficácia das ferramentas de busca mais tradicionais. Enquanto as pessoas, sem necessariamente possuir conhecimento computacional, tendem a expressar suas consultas de pesquisa de maneira natural e contextualizada, os algoritmos de busca tradicionais muitas vezes interpretam essas consultas de forma literal e superficial, analisando apenas as palavras idênticas e ignorando nuances semânticas e contextuais. Isso pode resultar em retornos de pesquisa imprecisos ou irrelevantes.
Então, as buscas semânticas foram desenvolvidas para permitir que os sistemas de busca compreendam não apenas as palavras-chave específicas usadas na consulta, mas também a essência do que o usuário está buscando. Ao incorporar diversas estratégias para entender a consulta desejada e filtrar resultados que parecem ser mais relevantes, as buscas semânticas podem analisar o contexto, entender o significado das palavras em relação umas às outras e interpretar a intenção por trás da consulta do usuário. Isso minimiza frustrações e promove a eficácia das plataformas de busca.


# Qual a solução?

Antes de adentrar especificamente na discussão sobre Busca Semântica, é crucial abordar o tema da "Web Semântica". Este conceito utiliza ontologias e grafos para implementar estratégias como o Resource Description Framework (RDF) e o OWL (Web Ontology Language), a fim de atribuir significados aos metadados das informações encontradas na internet. Essas estratégias são fundamentais para o funcionamento da Busca Semântica.
A Busca Semântica surge como uma evolução natural da Web Semântica, devido às necessidades de melhorar os resultados obtidos em consultas mais tradicionais. Não há uma definição formal para o tema, mas sim estratégias que os buscadores semânticos podem ou não implementar.
Essas estratégias foram concebidas por diversos pesquisadores em trabalhos distintos, cada uma com seus benefícios e defeitos. No entanto, elas podem ser implementadas tanto de forma separada quanto em conjunto.
* Baseada em Grafos: Esta abordagem leva em consideração exclusivamente a estrutura do gráfico, utilizando algoritmos de busca de gráficos ponderados para determinar os resultados mais relevantes, considerando o peso das arestas;

* Pesquisas/Consultas Relacionadas: O sistema de busca recomenda outras pesquisas que estejam semanticamente relacionadas à pesquisa realizada pelo usuário, oferecendo resultados que compartilham um sentido semelhante;

* Busca em Anotações Semânticas/Sintáticas: Os usuários definem diretamente a semântica da pesquisa ao indicar o papel sintático que os termos pesquisados desempenham, permitindo uma busca mais precisa e contextualizada;

* Resultados da Anotação Semântica: O pesquisador retorna páginas ou documentos com uma alta presença de recursos definidos no texto, especialmente entidades nomeadas ou previamente definidas;

* Baseada em Ontologia: Nesta abordagem, o buscador compreende as relações hierárquicas de entidades e conceitos, utilizando classificações como taxonomias e relações mais complexas entre entidades;

* Web Semântica: Esta técnica captura relacionamentos de dados e retorna resultados com base nas informações obtidas nos metadados disponibilizados pelos dados consultados, promovendo uma pesquisa mais precisa e contextualizada;

* Resultados de Referência: O sistema de busca utiliza dicionários ou enciclopédias, como a Wikipédia, para extrair termos-chave sobre o tema buscado e fornecer resultados mais abrangentes e informativos;

* Similaridade de Texto Integral: A busca não se limita apenas a termos e palavras-chave específicas, mas também utiliza blocos de texto completos para encontrar resultados que correspondam ao conteúdo integral da pesquisa;

* Busca de Conceitos: O buscador identifica conceitos e termos presentes na busca, filtrando os resultados com base neles e em suas equivalências semânticas, proporcionando uma pesquisa mais precisa e relevante;

* Busca Facetada: Este sistema fornece resultados de acordo com um conjunto predefinido de categorias de alto nível, chamadas facetas, permitindo uma navegação mais refinada e organizada nos resultados da pesquisa;

* Agrupada: Esta abordagem agrupa os resultados de acordo com os interesses inferidos a partir dos tópicos extraídos dos resultados da pesquisa, facilitando a compreensão e a análise dos resultados;

* Linguagem Natural: Consiste em compreender a semântica por trás das questões e apresentar respostas em linguagem natural, tornando a interação com o sistema de busca mais intuitiva e eficaz.


# Demonstração

Para demonstrar o funcionamento das Buscas Semânticas, desenvolvemos um projeto que emprega estratégias de grafos para apresentar filmes com maior similaridade semântica à consulta realizada. Neste projeto, utilizamos ferramentas como TensorFlow para vetorizar as descrições dos filmes e a entrada da busca, além do PostgreSQL com a biblioteca pgvector para armazenar os vetores e realizar a busca de proximidade utilizando a métrica euclidiana.
Para obter mais informações ou replicar o projeto, consulte a seção "Replicação".


# Discussão

Ficou evidente que a criação de um buscador semântico pode ser relativamente simples, porém, há margem para evoluções que podem tornar o trabalho mais complexo e sofisticado. Além disso, em relação à ferramenta pgvector, surgiram diversas indagações sobre outras estratégias que poderiam ser implementadas, como, por exemplo, a busca por similaridade utilizando o cálculo do cosseno.

# O que eu tenho a ver com isso?

* Trabalhos futuros podem justamente verificar o comportamento do pgvector usando a estratégia de similaridade pelo cálculo do cosseno e comparar resultados, assim como, utilizar outros meios de vetorização das palavras para perceber se tem alguma diferença, ou até mesmo tentar implementar sistemas de busca com outras estratégias.

# Replicação

Acesse ao repositório https://github.com/IriedsonSouto/movie-search-pgvector
E leia as instruções descritas no README.md
