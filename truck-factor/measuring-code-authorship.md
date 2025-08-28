# Metadados

* Measuring and analyzing code authorship in 1 + 118 open source projects
* Guilherme Avelino, Leonardo Passos, Andre Hora, Marco Tulio Valente
* Universidade Federal do Piauí (UFPI), University of Waterloo, Universidade Federal de Minas Gerais (UFMG)
* ScienceDirect
* 2019
* Link: https://www.sciencedirect.com/science/article/pii/S0167642318300388

# Qual o problema?

O artigo aborda a necessidade de entender melhor a autoria de código em projetos de software de código aberto em grande escala. Os autores argumentam que a autoria de código é uma informação que pode revelar insights importantes sobre a organização e a evolução de projetos de software, mais especificamente, o artigo destaca a importância de ir além das contagens de commits e considerar a contribuição real de cada desenvolvedor nos arquivos de um repositório. Isso é crucial porque a autoria de código em softwares é dinâmica e evolui ao longo do tempo, diferente da autoria estática em livros ou artigos científicos. Um bom exemplo disso é imaginarmos um arquivo criado por um desenvolvedor, mas que foi alterado por muitos outros ao longo do tempo; apenas contar o número de commits pode indicar que várias pessoas trabalharam no arquivo, mas não mostra quem teve o maior impacto no seu conteúdo final.

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta? 

Os autores utilizam uma métrica existente chamada Grau de Autoria ($DOA$), dividido em Grau de Autoria Absoluto ($DOAₐ$) e Grau de Autoria Normalizado ($DOAₙ$) objetivando determinar quais desenvolvedores fizeram as contribuições mais significativas para um arquivo, estes sendo definidos pelo termo "autores". Essas métricas foram utilizadas para analisar a autoria de código no kernel Linux e em outros 118 projetos de código aberto. Um desenvolvedor é considerado autor de um arquivo se o seu $DOAₙ$ for maior que 0,75 e o seu $DOAₐ$ for maior ou igual a 3,293; esses limiares foram estabelecidos em trabalhos anteriores que utilizaram a $DOA$ para estimar o truck factor de um projeto e para recomendar mantenedores para arquivos de código.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

**Grau de Autoria Aboluto:**
$DOAₐ(d, f) = 3.293 + 1.098 ∗ FA + 0.164 ∗ DL − 0.321 ∗ ln(1 + AC)$

**Grau de Autoria Normalizado:**
$DOAₙ (d, f) = DOAₐ (d, f)/max({DOAₐ (d', f) | d' ∈ changed(f)})$

Onde $d$ e $f$ são o desenvolvedor e um arquivo de código, respectivamente. Já $changed(f)$ é o conjunto de desenvolvedores que editaram um arquivo $f$ até determinada snapshot (uma release, por exemplo).

O $DOAₐ(d,f)$ leva em conta fatores como criação do arquivo e modificações subsequentes para quantificar a contribuição de cada desenvolvedor. Perceba que suas variáveis são:
* Autoria inicial ($FA$): se o desenvolvedor criou o arquivo, $FA$ = 1, caso contrário, $FA$ = 0.
* Número de entregas ($DL$): número de alterações feitas pelo desenvolvedor no arquivo.
* Número de aceitações ($AC$): número de alterações feitas por outros desenvolvedores no arquivo.

Já o $DOAₙ(d, f)$ atribui um valor entre 0 e 1 para cada desenvolvedor que modificou um arquivo. O valor 1 é atribuído ao desenvolvedor com a maior contribuição absoluta ($DOAₐ$), enquanto em outros casos, esse valor será menor que 1.

Por fim, os autores de um arquivo $f$ são dados por: $authors(f) = [d | d ∈ changed(f) ∧ DOAₙ(d, f) > 0.75 ∧ DOAₐ(d,f) >= 3.293]$. **É através desta função que conhecemos os autores de um arquivo**, ou seja, os desenvolvedores mais vitais. Perceba que para definirmos um autor, precisamos calcular o $DOAₐ(d,f)$, $DOAₙ(d, f)$ e o $authors(f)$ para todos os arquivos do repositório.

# Como foi avaliado?

Os autores analisaram a contribuição de desenvolvedores em 66 versões estáveis do kernel Linux (v.2.6.12 até v.4.17) obtidas do repositório de Linus Torvalds no GitHub e as compararam com um dataset adicional composto por 118 projetos open source populares do GitHub, implementados em seis linguagens de programação diferentes. Essa análise utilizou as métrica supracitadas para identificar autores de arquivos e teve como objetivo entender *authorship patterns* comuns em diferentes projetos de programação.

Para entender melhor a dinâmica de colaboração, os autores construíram e analisaram redes de coautoria. Essas redes são grafos, onde cada vértice representa um autor e as arestas conectam os vértices e representam a colaboração entre dois autores em um mesmo arquivo. Essa colaboração é filtrada para incluir apenas as relações onde houve sobreposição temporal na autoria do arquivo, ou seja, a conexão existe apenas se os autores trabalharam no arquivo durante o período em que ambos estavam ativos no projeto. Essa representação visual ajuda a entender o número médio de colaboradores por autor (no Linux kernel, por exemplo, um autor colabora, em média, com outros 3,39 autores); coeficiente de agrupamento (clustering), que indica a probabilidade de dois autores que colaboraram com um terceiro também terem colaborado entre si; e por fim, a tendência de autores com muitos colaboradores trabalharem com outros autores que também possuem muitos colaboradores.

Não obstante, foram efetuadas decomposições arquitetônicas em subsistemas (apenas no kernel Linux), limpeza de arquivos irrelevantes, detecção de aliases de autores e criação de filtros para remover projetos pequenos e garantir a viabilidade das métricas. As métricas usadas incluíram a proporção de autores, distribuição de arquivos por autor, especialização de trabalho e propriedades da rede de coautoria. Para análise estatística, foram utilizados métodos como média, desvio padrão, coeficientes de Gini, coeficientes de agrupamento e assortatividade, além de boxplots para visualizar a distribuição de autores e arquivos.

# Quais são os resultados?

Com os resultados obtidos, fora verificado que os mesmos *authorship patterns* que existem no Linux kernel estão presentes no dataset com os 118 sistemas open source. Tanto no Kernel quanto no dataset, a proporção de desenvolvedores que são autores é baixa (cerca de 26%), sugerindo que a maioria do trabalho de desenvolvimento é feita por uma pequena parcela de programadores e essa característica se mantém estável ao longo do tempo. Nos dois conjuntos de dados, a distribuição de arquivos por autor é altamente desigual com poucos autores concentrando a autoria da maior parte dos arquivos, o que é indicado por altos coeficientes de Gini. Para se ter uma ideia, no Linux kernel, só 2% dos desenvolvedores são autores e responsáveis por centenas de arquivos, enquanto a maioria dos autores (75%) é responsável por no máximo 10 arquivos (na análise do dataset não há porcentagens específicas, mas o coeficiente de Gini é alto também). Além disso, a especialização — onde autores se dedicam a áreas específicas — também é comum em ambos, incentivada pela modularidade nos projetos de software. Há ainda um padrão de mentoria na coautoria de arquivos, ou seja, durante analises das redes de coautoria (mencionadas na seção anterior), descobriu-se um padrão em que autores com alto número de conexões colaboram com autores com menos conexões; esse padrão, evidenciado por coeficientes de assortatividade negativos, sugere que desenvolvedores mais experientes (com mais conexões) orientam e colaboram com desenvolvedores menos experientes.

# Resenha crítica

O artigo contribui para a compreensão dos padrões de autoria em projetos open source e revela tendências consistentes em diferentes projetos; não obstante, a disponibilização de uma ferramenta em Java (denominada *truckfactor-tool*) capaz de executar esse trabalho facilita a possível expansão de estudos relacionados a autoria em projetos, o que é excelente. Há possíveis ameaças à validade na avaliação: a presença de aliases de desenvolvedores podem afetar os cálculos das métricas, no entanto, na ferramenta disponibilizada pelos autores, um arquivo "aliases.txt" pode ser preenchido, o que resolve o problema. Outra possível ameaça são as refatorações baseadas no git-blame, haja vista que elas impactam na mensuração de autorias (por exemplo, a simples mudança de nome de uma variável é registrada como alteração no histórico do git, mas não reflete uma contribuição significativa). É importante perceber que a ferramenta não considera forks que não foram integrados ao repositório principal e não considera a granularidade das mudanças (número de linhas de código alteradas, removidas ou adicionadas), nem o tipo de alteração realizada (correções de bugs, novas funcionalidades ou refatoração), ou seja, todos os commits têm o mesmo peso.

Os autores do artigo - Guilherme Avelino, Leonardo Passos, Andre Hora e Marco Tulio Valente - possuem um histórico de publicações em áreas como mineração de repositórios de software, análise de código-fonte e desenvolvimento open source e seus trabalhos abordam temas como identificação de especialistas, estimativa de truck factors, análise de código legado e compreensão de padrões de colaboração. Eles têm por objetivo, como trabalhos futuros, a validação dos resultados apresentados no artigo com os desenvolvedores dos sistemas open source analisados, além da investigação dos padrões de autoria em sistemas comerciais, comparando-os com os resultados obtidos em projetos open source. Por fim, o impacto da experiência dos desenvolvedores é um bom tema a ser abordado futuramente, haja vista que o paper não leva em consideração a experiência dos desenvolvedores ao analisar os padrões de autoria.

# O que eu tenho a ver com isso?

É possível replicar o estudo para análise de código IaC (Infrastructure as Code) em repositórios públicos, repositórios privados e/ou em datasets utilizando as métricas apresentadas no artigo. Essa análise pode consistir principalmente no entendimento da distribuição do trabalho de equipes de desenvolvimento IaC.

# Replicação

* Os dados extraídos do Linux kernel e do dataset podem ser visualizados [aqui](https://github.com/gavelino/scp_data/tree/master/data).
* A versão mais atualizada da ferramenta *truckfactor-tool* pode ser obtida [aqui](https://github.com/aserg-ufmg/Truck-Factor/releases/tag/v1.2).
* Consegui entender e rodar. Agora darei ênfase na modificação da ferramenta através de um fork.
* É possível replicar.
