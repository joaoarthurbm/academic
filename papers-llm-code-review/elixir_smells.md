
# Metadados

* "Understanding code smells in Elixir functional language"
* Autores: Lucas Francisco da Matta Vegi, Marco Tulio Valente
* Instituição(ões) envolvidas na pesquisa: Departamento de Ciência da Computação, UFMG, Belo Horizonte, Brazil
* Empirical Software Engineering (2023)
* Ano de publicação: 2023
* [Link](https://drive.google.com/file/d/1gsiK-rznKEqKNLAStBFddSxh13L6pd78/view?usp=drive_link)

# Qual o problema?

O problema que o artigo aborda é o pouco
aprofundamento/entendimento sobre as melhores práticas de
programação com a linguagem funcional Elixir, devido à escassa
quantidade de estudos e trabalhos conduzidos acerca das melhores
maneiras de se trabalhar com ela, bem como a identificação de
seus *bad smells*. 

# Qual a solução?

A solução proposta pelo estudo foi a criação de um catálogo de
*bad smells* de Elixir, através
de uma análise das práticas de programação de diversos profissionais
que utilizam a linguagem, visando documentar e validar os mais importantes
*smells* e boas práticas de código. 

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta? 

Os autores aprofundam a literatura sobre *bad smells* de Elixir,
propondo a documentação e catalogação de *code smells* específicos, utilizando como base as 
impressões/preferências e códigos da comunidade de desenvolvedores profissionais da
linguagem como meio de validação.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

Os autores utilizaram uma abordagem metodológica mista, para
documentar, catalogar e validar *code smells* em Elixir. Para
capturar os diferentes problemas de qualidade de código, os
autores utilizaram da mescla de três estratégias:

* *Grey literature review* : consiste na busca manual no Google e
em canais informais, seleção minuciosa dos documentos
relevantes, utilizando os critérios *Garousi et al.* e por fim, 
a extração manual das discussões sobre o tema.

* Interação com a comunidade: criação de um repositório público
no GitHub onde o catálogo inicial é compartilhado e os
desenvolvedores são estimulados a contribuir.

* MSR(*Mining Software Repositories*): busca automatizada no
GitHub, aplicação do critério de autoridade de *Garousi* para
filrar *artifacts* confiáveis e a leitura e análise manual dos
selecionados.

# Como foi avaliado?

O processo consiste na tentativa de responder duas RQs(*Research
questions*):
* Desenvolvedores de Elixir discutem *code smells* tradicionais?
* Desenvolvedores de Elixir discutem *code smells* específicos?

Os questionamentos tem sua origem em um estudo realizado pelos
mesmos autores. Foi analisado o mesmo tema, ou seja, o artigo
atual deu
sequência a um trabalho anterior, fundamentando melhor as conclusões
ao utilizar grupos e contextos mais abrangentes que o estudo
anterior. Três métodos foram aplicados em sequência para definir a
categorização de outros *bad smells* na linguagem:


Primeiramente, no estudo original, foi feita uma busca manual em
*grey literature* e no GitHub, selecionando os documentos utilizando critérios de
relevância para o contexto das duas RQs. A partir disso, foi
proposto um catálogo de *bad smells* de natureza empírica, se dividindo em específicos e
tradicionais. 

Segundamente, os autores publicaram os resultados e catálogo em
um repositório público no GitHub. Em seguida, convidaram os desenvolvedores
de Elixir a abrir *issues* e *pull requests* no projeto, que se tornou popular,
ranqueando entre os 100 projetos de Elixir mais acessados no
GitHub. Dessa forma, 25 documentos - 13 *issues* e 12 *pull
requests* - foram criados na comunidade e 20 foram validados pelos
autores do artigo, resultando em 27 melhorias no catálogo.

Na sequência, para expandir o catálogo, foram minerados, no GitHub,
repositórios a procura de *artifacts* - *issues*, *pull requests*,
*commits* e arquivos - referentes a *code smells*. Os artifacts foram
identificados utilizando o
método de mineração de *Dabic et al*. Ao fim desta etapa, foram
detectados 301
*artifacts*, dos quais 41 foram selecionados, utilizando
critério *Garousi’s Authority of the Producer* (*Garousi et al.*
2019)".

Por último, o primeiro autor leu e analisou em detalhes o
conteúdo de cada *artifact*, a fim de caracterizar *code smells* em
Elixir - tradicionais ou específicos. Na sequência, o segundo
autor validou todas as propostas, no entanto, 8 destas resultaram
em um desacordo entre os autores.

# Quais são os resultados?

Os resultados do estudo foram a catalogação de 35 *smells*,
com 12 deles sendo *smells* tradicionais e 23 *smells* específicos da
linguagem Elixir. Nesse contexto, 97% dos *smells* catalogados foram
elencados como no mínimo *mid-relevance*, ou seja, tem impacto
direto na legibilidade, manutenção e na melhoria do código em
Elixir. Além disso, 54% deles possuem o chamado *mid-prevalence*,
indicando que mais da metade deles são indentificáveis nos
códigos em produção.
O estudo também destacou que os *smells* específicos tendem a ser
mais relevantes do que os tradicionais e apontou alguns como os
mais críticos:
* *Complex Branching*
* *Working with invalid data*
* *Shotgun Surgery (Traditional smell)*

# Resenha crítica

O artigo trouxe literatura útil e relevante para o contexto tanto
da linguagem Elixir quanto linguagens funcionais como um todo.
Anteriormente ao seu lançamento, o
tema era pouco explorado entre os desenvolvedores de Elixir. No
entanto, a catalogação parece ser o caminho para desenvolver
padrões e códigos melhores e os autores tiveram êxito em propor
cerca de 35 *smells* para o catálogo da linguagem.

No entanto, é importante destacar as possíveis ameaças à validade do
artigo. O método utilizado para determinar quão relevante para
construção de um código de qualidade depende de uma clara análise
subjetiva dos desenvolvedores profissionais da linguagem. Além
disso, a validação de *smells* também conta com a aprovação dos
autores, que por sua vez também é uma análise subjetiva.

O artigo também abre espaço para algumas questões pendentes a
serem exploradas. Apesar da catalogação ter sido feita usando
métodos de mineração, não foi desenvolvida uma ferramenta
automática de deteccão dos *smells*, que auxiliaria numa análise
com maior quantidade de dados. Assim, seria possível quantificar
melhor a recorrência dos problemas de código que foram
documentados.

Em resumo, o artigo representa uma contribuição significativa para a compreensão e documentação de 
*code smells* em sistemas escritos na linguagem Elixir, demonstrando a viabilidade e eficácia de 
uma abordagem baseada em métodos mistos para identificar e categorizar esses problemas.

# Replicação

* Onde estão os dados? Os repositórios do GitHub são públicos.
* Onde está o código? Não foi fornecido - o artigo é descritivo e os códigos utilizados são de repositórios públicos no GitHub
* Conseguiu entender/rodar? Não — o artigo é apenas descritivo.
* Dá para replicar o experimento/estudo? 
