# Metadados

* Measuring and analyzing code authorship in 1 + 118 open source projects
* Guilherme Avelino, Leonardo Passos, Andre Hora, Marco Tulio Valente
* Universidade Federal do Piauí (UFPI), University of Waterloo, Universidade Federal de Minas Gerais (UFMG)
* ScienceDirect
* 2019
* Link: https://www.sciencedirect.com/science/article/pii/S0167642318300388

# Qual o problema?

O artigo aborda a necessidade de entender melhor a autoria de código em projetos de software de código aberto em grande escala. Os autores argumentam que a autoria de código é uma informação crucial, mas muitas vezes negligenciada, que pode revelar insights importantes sobre a organização e a evolução de projetos de software. Especificamente, o artigo destaca a importância de ir além das simples contagens de commits e considerar a contribuição real de cada desenvolvedor nos arquivos de um repositório. Isso é crucial porque a autoria de código em softwares é dinâmica e evolui ao longo do tempo, diferente da autoria estática em livros ou artigos científicos. Para ilustrar, imagine um arquivo criado por um desenvolvedor, mas que foi alterado por muitos outros ao longo do tempo; apenas contar o número de commits pode indicar que várias pessoas trabalharam no arquivo, mas não mostra quem teve o maior impacto no seu conteúdo final.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta? 

Os autores utilizam uma métrica existente chamada Grau de Autoria ($DOA$), dividido em Grau de Autoria Absoluto ($DOAₐ$) e Grau de Autoria Normalizado ($DOAₙ$) objetivando determinar quais desenvolvedores fizeram as contribuições mais significativas para um arquivo. Ambos foram utilizados para analisar a autoria de código no kernel Linux e em outros 118 projetos de código aberto. Um desenvolvedor é considerado autor de um arquivo se o seu $DOAₙ$ for maior que 0,75 e o seu $DOAₐ$ for maior ou igual a 3,293. Esses limiares foram estabelecidos em trabalhos anteriores que utilizaram a $DOA$ para estimar o truck factor de um projeto e para recomendar mantenedores para arquivos de código.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

**Grau de Autoria Aboluto:**
$DOAₐ(d, f) = 3.293 + 1.098 ∗ FA + 0.164 ∗ DL − 0.321 ∗ ln(1 + AC)$

**Grau de Autoria Normalizado:**
$DOAₙ (d, f) = DOAₐ (d, f)/max({DOAₐ (d', f) | d' ∈ changed(f)})$

Onde $d$ e $f$ são o desenvolvedor e um arquivo de código, respectivamente. Já $changed(f)$ é o conjunto de desenvolvedores que editaram um arquivo $f$ até determinada snapshot (uma release, por exemplo).

O $DOAₐ(d,f)$ visa quantificar a contribuição real de cada desenvolvedor para um arquivo, levando em conta não apenas a criação do arquivo, mas também as modificações subsequentes. Perceba que suas variáveis são:
* Autoria inicial ($FA$): se o desenvolvedor criou o arquivo, $FA$ = 1, caso contrário, $FA$ = 0.
* Número de entregas ($DL$): número de alterações feitas pelo desenvolvedor no arquivo.
* Número de aceitações ($AC$): número de alterações feitas por outros desenvolvedores no arquivo.

Já o $DOAₙ(d, f)$ atribui um valor entre 0 e 1 para cada desenvolvedor que modificou um arquivo. O valor 1 é atribuído ao desenvolvedor com a maior contribuição absoluta ($DOAₐ$), enquanto em outros cassos, esse valor será menor que 1.

Por fim, os autores de um arquivo $f$ são dados por: $authors(f) = [d | d ∈ changed(f) ∧ DOAₙ(d, f) > 0.75 ∧ DOAₐ(d,f) >= 3.293]$

# Como foi avaliado?

Os autores analisaram a contribuição de desenvolvedores em 66 versões estáveis do kernel Linux (v.2.6.12 até v.4.17) obtidas do repositório de Linus Torvalds no GitHub e as compararam com um dataset adicional composto por 118 projetos open source populares do GitHub, implementados em seis linguagens de programação diferentes. Essa análise utilizou a métrica de Grau de Autoria ($DOA$) e teve como objetivo entender *autorship patterns* comuns em diferentes projetos de programação.

Não obstante, foram efetuadas decomposições arquitetônicas em subsistemas (apenas no kernel Linux), limpeza de arquivos irrelevantes, detecção de aliases de autores e criação de filtros para remover projetos pequenos e garantir a viabilidade das métricas.

As métricas usadas incluíram a proporção de autores, a distribuição de arquivos por autor, a especialização de trabalho, e propriedades da rede de coautoria. Para análise estatística, foram utilizados métodos como média, desvio padrão, coeficientes de Gini, coeficientes de agrupamento e assortatividade. O estudo também utilizou boxplots para visualizar a distribuição de autores e arquivos.

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

# O que eu tenho a ver com isso?

Podemos usar o $DOAₐ$ = ... para o contexto de IaC. Trabalhando com dataset.

* Colocar aqui ideias de trabalhos de pesquisa que podem ser feitas a partir desse trabalho. Por exemplo, experimentar com outra base, estender a análise para outro algoritmo, modelo etc. Colocar também como isso se relaciona com o que você está fazendo ou pretende fazer. O que dá para extrair, comparar, evoluir desse trabalho que tem relação com o seu.

# Replicação

* Onde estão os dados?
* Onde está o código?
* Conseguiu entender/rodar?
* Dá para replicar o experimento/estudo?
