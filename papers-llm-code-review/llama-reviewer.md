# Metadados

* LLaMA-Reviewer: Advancing Code Review Automation with Large Language Models through Parameter-Efficient Fine-Tuning
* Junyi Lu, Lei Yu, Xiaojia Li, Li Yang, Chun Zuo
* Institute of Software, Chinese Academy of Sciences, Beijing, China
University of Chinese Academy of Sciences, Beijing, China
School of Software, Tsinghua University, Beijing, China
Sinosoft Company Limited, Beijing, China
* 34th IEEE International Symposium on Software Reliability Engineering (ISSRE 2023)
* 2023
* [arxiv.org/abs/2308.11148](arxiv.org/abs/2308.11148)

# Qual o problema?

A revisão de código desempenha um papel essencial na Engenharia de Software, melhorando a qualidade do código, identificando defeitos e promovendo a troca de conhecimento. Entretanto, a revisão de código é uma tarefa manual, que consome tempo e gera uma grande carga de trabalho para os desenvolvedores.

Para abordar essa questão, a automação da revisão de código surgiu como uma solução promissora. Contudo, tradicionalmente, essa automação foi proposta por meio de modelos pré treinados para domínios específicos, que demandam uma grande quantidade de recursos computacionais e de tempo para o pré treinamento do modelo a partir do zero.


# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta? 

Os autores apresentam o LLaMA-Reviewer, um novo framework baseado no modelo LLaMA, uma LLM popular, para automação da revisão de código. Para atingir esse desempenho, os autores utilizaram métodos de Parameter-Efficient Fine-Tuning (PEFT) para realizar ajustes finos necessários no modelo inicial. Além disso, ao aplicar modelos de tipo plugin, os autores reduziram significativamente a quantidade de armazenamento necessário.

O grande diferencial desse modelo é que é possível atingir uma performance competitiva à de modelos pré treinados para domínios específicos, porém utilizando muito menos recursos computacionais e tempo de treinamento.

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

Os autores utilizaram dois métodos de Parameter-Efficient Fine-Tuning: Zero-init attention prefix-tuning e LoRA para realizar ajustes finos, balanceando a eficiência de parâmetros e a performance do modelo.

Para adaptar o modelo LLaMA para tarefas relacionadas à revisão de código, os autores utilizaram uma técnica de ajuste de instruções voltada especialmente para o domínio de programação. Eles seguiram um processo semelhante ao do Stanford Alpaca, mas utilizando os métodos de ajuste fino eficiente em parâmetros.

Uma das técnicas de ajuste fino utilizada pelos autores, Zero-init attention prefix-tuning, funciona por meio da adição de tokens de prefixo adicionais nas camadas superiores do transformer do LLaMA. Esses prompts são concatenados com os tokens originais e introduz-se um novo fator que controla a importância desses tokens em relação aos originais. Inicialmente, esse fator é definido como zero, o que significa que o modelo não dá muita ênfase aos tokens adicionados. No entanto, ao longo do treinamento, esse fator é ajustado gradualmente até atingir o valor ideal.

Outra técnica utilizada, Low-Rank Adaptation (LoRA), mantém os pesos originais do modelo e incorpora matrizes de baixo rank treináveis às camadas transformer do modelo. Essa adição reduz o rank da matriz original, diminuindo o número de parâmetros que precisam ser atualizados durante o ajuste fino, ao mesmo tempo em que preserva o máximo de informações possíveis. Dessa forma, é possível simular um ajuste de pesos completo, algo que demanda muito mais recursos, de forma mais eficiente computacionalmente.


# Como foi avaliado?

Os autores adotaram métricas específicas para cada tarefa de revisão de código. A previsão da necessidade de revisão foi abordada como um problema de classificação binária, usando precisão, recall e F1-score para quantificar a precisão da categorização do modelo. Já para as tarefas de geração de comentários de revisão de código e refinamento de código utilizou-se o BLEU-4 score. 

Para todas as tarefas os autores levaram em consideração o resultado principal (top-1 result), concentrando-se nos feedbacks mais relevantes. Os resultados obtidos foram comparados com modelos de referência de estudos anteriores.

Os autores utilizaram dois datasets de revisão de código: o dataset do CodeReviewer de Li et al. e o dataset de Tufano et al. O dataset de Li et al. é multi linguagem e é proveniente de repositórios do Github, além disso é dividido em três subconjuntos, cada um dedicado a um aspecto específico da revisão de código. Já o dataset de Tufano et al. é específico da linguagem Java e combina dados do GitHub e do Gerrit.

A primeira questão de pesquisa avalia a performance do LLaMA-Reviewer, sendo dividida em três sub-questões, que avaliam a performance do modelo em prever a necessidade de revisão, em gerar comentários de revisão e em refinar código, respectivamente.

Para a primeira subquestão, foi utilizado apenas o dataset de Li et al., com aproximadamente 226k observações para treino, 31k para validação e 31k para teste do modelo. Já para a segunda subquestão foram empregados ambos os datasets: aproximadamente 134k observações para treino, 17k para validação e 17k para teste do dataset de Tufano et al. e aproximadamente 118k observações para treino, 10k para validação e 10k para teste do dataset de Li et al. Para a terceira sub questão os autores também utilizaram ambos os datasets, com aproximadamente 134k observações para treino, 17k para validação e 17k para teste, para o dataset de Tufano et al. e aproximadamente 150k observações para treino, 13k para validação e 13k para teste, para o dataset de Li et al.

A segunda questão de pesquisa investiga a influência da representação dos dados de input, avaliando em suas duas subquestões o impacto da formatação de código e o papel do label de linguagem no input. Para avaliar o impacto da formatação de código os autores utilizaram ambos os datasets, examinando o resultado das tarefas de geração de comentários de revisão e de refinamento de código. Como os datasets apresentam formatações diferentes a performance do modelo foi avaliada comparando os resultados obtidos em cada dataset distinto. Para avaliação do papel do label de linguagem no input, os autores utilizaram apenas o dataset de Li et al., já que ele inclui múltiplas linguagens de programação.

A terceira questão avalia o impacto do ajuste de instruções. Para responder essa questão foram realizados experimentos com e sem o estágio preliminar de ajuste de instruções, empregando tanto o Zero-init attention prefix-tuning quanto o Low-rank Adaptation. As três sub questões exploram as consequências desse ajuste para  o Zero-init attention prefix-tuning e para o LoRA, e também qual a influência dos diferentes tipos de instrução na performance do modelo.

Por fim, a quarta questão explora a influência dos métodos de Parameter-Efficient Fine-Tuning (PEFT). Para isso, foram conduzidos experimentos adicionais, ajustando o rank r do LoRA especificamente para 8 e para 16. As três sub questões comparam os métodos de PEFT, analisam o impacto do rank r no LoRA e discutem a eficiencia dos métodos PEFT.

# Quais são os resultados?

Os resultados encontrados para a questão de pesquisa número um indicam que o LLaMA-Reviewer se destaca na geração de comentários de revisão de código em linguagem natural e identifica mais trechos de código problemático, na previsão da necessidade de revisão. Além disso, o modelo mantém uma performance competitiva na tarefa de refinamento de código.

Para a segunda questão de pesquisa, os autores chegaram à conclusão de que o modelo tem uma melhor performance quando a representação de input é similar àquela usada no pré treinamento. O uso de labels de linguagem não trouxe uma melhora de performance na fase inicial de refinamento de instruções, entretanto, após a implementação do refinamento de instruções, o uso de label contribuiu positivamente para a performance do modelo.

Os resultados encontrados para a terceira questão de pesquisa evidenciam que o ajuste de instruções pode potencialmente aumentar a performance do modelo, entretanto, essa melhoria é limitada devido à diferença na forma como as palavras são utilizadas nos diferentes conjuntos de dados.

Por fim, para a quarta questão de pesquisa, os autores concluíram que entre os métodos de PEFT o LoRA é mais adequado para automatizar as tarefas de revisão de código. Ao escolher um rank apropriado para o LoRA, o modelo pode atingir uma performance competitiva, com menos de 1% dos parâmetros treináveis e com necessidade de espaço de armazenamento reduzida.


# Resenha crítica

O artigo aborda um tema relevante e contemporâneo - o uso de modelos de linguagem de grande escala na revisão de código - uma área ainda vastamente inexplorada na literatura. A análise da utilização desses modelos para automatização da revisão de código é fundamental, considerando a crescente escala dos projetos de software modernos e a sobrecarga gerada pela revisão de código nos desenvolvedores, muitas vezes tornando-se um gargalo no fluxo de produção de software.

A revisão bibliográfica do artigo é notavelmente atualizada, refletindo o grande potencial de novas pesquisas sobre o assunto. No âmbito da minha própria investigação sobre o uso dos modelos de linguagem de grande escala na automatização da revisão de código, este artigo se revela como uma adição interessante à bibliografia da minha pesquisa. Os autores empregam referências recentes, que enriquecem a discussão sobre o tema e também possibilitam comparações com estudos anteriores.

No entanto, é importante reconhecer possíveis ameaças à validade do artigo, como indicado pelos próprios autores. A métrica BLEU-4 utilizada para avaliar a performance dos modelos em algumas tarefas, embora amplamente utilizada, não é universalmente reconhecida como a métrica definitiva para essa finalidade. Ademais, a avaliação dos métodos de parameter-efficient fine-tuning foi restrita a apenas dois métodos, o que limita a generalização dos resultados.

A utilização do menor tamanho do modelo LLaMA pelos autores pode subestimar a capacidade dos modelos de linguagem de grande escala atuais. Além disso, os resultados obtidos podem não ser generalizáveis para além dos dois datasets utilizados.

O artigo abre espaço para questões a serem exploradas em trabalhos futuros, seria pertinente uma comparação mais abrangente entre diferentes métodos de ajuste fino eficiente em parâmetros(PEFT), assim como a utilização de datasets adicionais para validar os resultados, em tarefas em que a experimentação foi realizada utilizando apenas um conjunto de dados. Outro possível trabalho futuro relevante seria uma pesquisa em que há experimentação com modelos de diferentes tamanhos e tipos.

Os autores deste artigo têm pesquisas publicadas sobre diversos temas de ciência da computação. Junyi Lu, tem trabalhos sobre temas variados, incluindo engenharia de software, análise de redes sociais, recuperação da informação e inteligência artificial. Da mesma forma, Lei Yu possui um grande histórico de publicações abrangendo aprendizado de máquina, mineração de dados, redes de computadores, processamento de imagens e computação em nuvem. Além disso, demais autores também têm publicações em tópicos diversos incluindo big data, blockchain, engenharia de software e machine learning.
