# Metadados

- Título: Using Architecture Decision Records in Open Source Projects—An MSR Study on GitHub
- Autores: Georg Buchgeher, Stefan Schöberl, Verena Geist, Bernhard Dorninger, Philipp Haindl e Rainer Weinerich
- De que instituições são os autores? Karriere.at GmbH, Software Competence Center Hagenberg GmbH, St. Pölten University of Applied Sciences e Johannes Kepler University Linz
- Onde foi publicado: IEEE Access
- Ano de publicação: 2023
- Link: [Using Architecture Decision Records in Open Source Projects](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10155430)

# qual o problema?

O problema central abordado pelo artigo é a falta de evidências sobre a adoção prática de Architecture Decision Records (ADRs) em projetos de software, apesar de sua proposta como solução leve para documentar decisões arquiteturais. Os autores destacam que, embora os ADRs tenham sido sugeridos em 2011 para combater a "vaporização do conhecimento arquitetural" (perda do contexto das decisões tomadas ao longo do tempo).

Exemplo: "Em um projeto que migra de uma arquitetura monolítica para microsserviços, as decisões sobre as tecnologias, padrões de comunicação ou critérios de escalabilidade podem ser documentadas inicalmente, mas, sem um método estruturado, esse conhecimento se perde ao longo do tempo. Isso leva a retrabalho, incertezas e dificuldades para novos integrantes entenderem o raciocínio das escolhas. O artigo também identifica barreiras práticas para a documentação das decisões, como a falta de ferramentas adequadas, alto esforço necessário para capturar o conhecimento de arquitatura e interrupções do fluxo de desenvolvimento."

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta?

Os autores apresentam um estudo de minenação de repositórios de software (MSR) para analisar o uso de ADRs em projetos open sources no GitHub. O objetivo é se e em que grau as ADRs são usadas na prática e obter insights sobre as práticas atuais de seu uso. Para isso, eles desevolvem critérios de busca pra identificar repositórios que utilizam ADRs, coletam dados de repositórios e analisam padrões quantitativos e qualitativos. Para atingir os objetivos de pesquisa, foi definido as seguintes perguntas:

- Como a adoção de ADRs evoluiu ao longo do tempo?
- Qual o estado da prática do uso de ADRs em repositórios de código aberto?

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

Para executar o estudo, os autores precisaram localizar e extrair ADRs armazenados em projetos open source hospedados no GitHub. Esse processo teve diversas limitações técnicas e práticas. A principal delas está relacionada ao uso da GitHub Search API, que apresenta restrições importantes. Especialmente a API impõe limites á quantidade de resultados retornados por consulta, ao número de requisições por hora, e não permite buscas estruturadas que combinem critários como tipo de arquivo, nome de diretório e padrão textual no conteúdo de forma precisa. Além disso, a API possui uma limitação de corte de resultados, retornando no máximo 1.000 itens por busca, o que impede a extração exaustiva de dados em pesquisas maiores.

Tendo esse cenário, os autores não confiaram apenas na API, mas realizaram uma busca inicial no próprio buscador na página web do GitHub, utilizando os termos "archtecture decision record" e "adr" para identificar repositórios potencialmente relevantes. Eles também buscaram por repostórios que apresentassem nomenclaturas padronizadas de arquivos ou diretório, como adr, adrs, archtecture/decisions, docs/adr, entre outros. Essa metodologia consistiu em uma inspeção manual inicial dos resultados para evitar falsos positivos.

Após essa triagem inicial, os pesquisadores criaram um crawler automatizado para clonar localmente repostórios selecionados. Com esses repostórios, foi possível realizar uma varredura local e mais aprofundada dos arquivos contidos neles. Nessa fase, foram analisados os caminhos dos arquivos, extensões, nome e conteúdo textual. Os autores destacam que embora existam propostas do uso da extensão .adr para identificar esses arquivos, essa prática ainda não é adotada na comunidade open source. Na maioria dos casos os ADRs usam extensões .md (Markdown), o que dificulta a busca. Para contornar isso, os pesquisadores optaram por aplicar heurísticas de conteúdo textual, verificando manualmente se o arquivo segue algum dos templates de ADRs conhecidos, como o de Michael Nygarb ou o MADR (Markdown Architectural Decision Records).

O arquivos candidatos a possíveil ADR foram processados para extrair informações como título da decisão, data de criação, autores envolvidos (via histórico de commits), tempo entre o primeiro e o último commit (para avaliar manuntenção), além de indicadores como frenquência de modificaçãoe e adoção de templates utilizados. A análise também incluiu a contagem de arquivos ADR por respositório, dentre outras informações.

Por fim, os autores criaram um dataset próprio com os repositórios validados, contendo metadados e métricas extraídas. Embora o código fonte do crawler ultilizado não tenha sido disponibilizado no artigo, os dados coletados foram apresentados de foram apresentados nas análises e os repositórios estão listados para consulta.

# Como foi avaliado?

A avaliação do estudo seguiu uma abordagem voltada a ver como funciona na prática, baseada em técnicas de minenação de Repositórios de Software (MSR). Os autores definiram duas perguntas de pesquisa principais: a primeira buscava entender como a adoção de ADRs evoluiu ao logo do tempo, e a segunda, como esses registros são usados na prática. Para responder a essas perguntas, os pesquisadores coletaram dados de 921 repositórios open source do GitHub, previamente identificados como contendo ADRs válidos. Essa coleta combinou a automação com a validação manual.

A análise consistiu em extrair e observar métricas como o número de ADRs por repositório, tempo de vida dos registros (do primeiro ao último commit), frenquência de modificações dos arquivos e quantidade de colaboradores distintos. Também foram identificados so templates adotados, como o de Nygard e MADR, além da verificação da existência de índices de ADRs e da continuidade da prática em cada projeto. Embora o estudo não tenha se aprofundado em técnicas estatísticas avançadas, os autores utilizam análises descritiva e visualização para comparar grupos de projetos (com poucos ADRs vs muitos ADRs) e identificar padrões de adoção.

# Quais são os resultados?

Os resultados revelam que embora a prática de registrar decisões arquiteturais com ADRs venham crescendo desde 2017, sua adoção em larga escala ainda é limitada. Mais da metade dos repositórios analisados possui entre 1 e 5 ADRs, indicando uma aplicação pontual da prática, sem continuidade. Apenas 47 projetos tem mais de 20 ADRs, sugerindo uma adoção consistente ao longo do tempo.

Em relação á autoria, os dados mostram que a documentação tende a ser mais centralizada: em cerca de 50% dos casos, os ADRs foram criados por um único desenvolvedor. Por outro lado, os repositórios com maior número de ADRs tendem a ter mais autores envolvidos, o que indica que uma prática mais colaborativa. A análise também identificou que a maioria dos registros segue o template proposto por Michael Nygard, demostrando certa padronização na forma como as decisões são descritas.

Os ADRs são raramente modificados: cerca de 70% dos arquivos possuem apenas um commit, e poucos são atualizados após sua criação. Além disso, mais de 300 repostórios mantiveram a prática por pelo menos seis meses, o que sugere um esforço de continuidade em alguns projetos. No entanto a ausência de links entre ADRs e outros arterfatos, como código fonte, issues ou pull requests, indica que a integração dessas decisões com o restante do projeto ainda é fraca ou negligenciada.

# Resenha crítica

O artigo mostra uma contribuição importante ao trazer uma visão mais ampla, baseada em dados concretos, sobre o uso de ADRs em projetos open source. Ao explorar uma amostra considerável de repositórios e adotar uma metodologia de mineração bem elaborada, os autores fornecem evidências empíricas que mostram a importância da prática de documentar decisões arquiteturais. Isso é particulamente útil para desenvolvedores, arquitetos e pesquisadores que buscam entender como decisões técnicas são comunicadas e preservadas em ambientes colaborativos.

Uma limitação importante é a ausência de análise textual dos ADRs. Embora o artigo categorize a adoção, frenquência e estrutura dos registros, ele não investiga quais tipos de decisões são mais comuns, quais tecnologias aparecem com mais frenquência, ou como as justificativas são formuladas. Além disso, os autores não disponibilizam publicamente o código fonte de coleta e análise, o que dificulta dar continuidade ao estudo, mesmo que os repositórios estejam acessíveis.

No contexto do meu trabalho, esse artigo é diretamente aplicável, tendo em vista que oferece um ponto de partida com dados concretos, e um conjunto inicial de repositórios na qual me fez ter uma compreensão da diversidade e informações da prática de ADRs. A leirura me mostrou uma direção que eu já vinha pesando para a minha pesquisa. A proposta de centralizar ADRs e torná-los acessíveis de forma organizada, mas agora exergo com mais clareza como posso ir além do que foi abordado no artigo. Enquanto os autores focaram na presença e estrutura de ADRs, percebi que tem um espaço para explorar o conteúdo dessas decisões mais detalhadamente.
