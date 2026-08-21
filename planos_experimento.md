# Projeto de Experimento

Disclaimer: há muita literatura sobre isso e que vai muito mais a fundo na elaboração de projetos de experimento. Há também diferentes formas de projetar um experimento a depender do que você quer investigar. Aqui estão regras mais gerais e que são mais adequadas ao contexto dos estudos em Engenharia de Software que costumo conduzir.

## 1. Questões de pesquisa

Todo projeto de experimento deve começar pelas questões de pesquisa que se quer responder. Essa é a primeira a se pensar. Note que nesse estágio você já passou pelo momento de identificar e entender o problema que você quer resolver.

O erro mais comum é formular perguntas que podem ser respondidas com um simples sim ou não. Uma questão de pesquisa precisa ser complexa o suficiente para exigir uma resposta elaborada. Por exemplo, em um trabalho que avalia a capacidade de modelos de linguagem em refatorar código Clojure com *smells*, uma pergunta ruim seria "Os modelos são capazes de refatorar código com *smells*?". 

Uma pergunta mais adequada seria algo como "Quão eficientes são os modelos na refatoração de código com *smells*?". Note a diferença: a segunda pergunta exige caracterização, medição e análise, não apenas uma resposta curta.

As questões de pesquisa podem ser gerais, como no exemplo acima, mas também podem ser mais descritivas e específicas. Na minha experiência, costumo orientar meus alunos a estruturarem uma questão geral, que dá o norte do trabalho, acompanhada de subquestões mais granulares, que decompõem essa questão geral em aspectos investigáveis de forma mais direta. Essa estrutura de "uma geral + algumas específicas" facilita tanto o desenho do experimento quanto a análise dos resultados, porque cada subquestão pode apontar para uma métrica, uma análise estatística ou uma dimensão de comparação diferente, enquanto a questão geral aponta o norte do trabalho.

Voltando ao exemplo da refatoração de código Clojure com *smells*, a questão geral "Quão eficientes são os modelos na refatoração de código com *smells*?" pode se desdobrar em questões como:

- **QP1.** Em que medida as refatorações propostas pelos modelos removem o *smell* original sem introduzir novos *smells* ou quebrar o comportamento do código?
- **QP2.** Como a eficiência dos modelos varia entre diferentes tipos de *smell* (por exemplo, duplicação de código versus função com excesso de responsabilidades)?
- **QP3.** Como o tamanho e a complexidade do trecho de código afetam a qualidade das refatorações geradas?
- **QP4.** Que diferenças de desempenho existem entre modelos distintos na mesma tarefa de refatoração?

Cada uma dessas questões aponta para uma forma diferente de medir e analisar os dados coletados no experimento, o que já começa a indicar, lá na fase de definição das questões, que tipo de métrica e que tipo de análise estatística o aluno pode/vai precisar planejar mais à frente.

Por que essa decomposição funciona bem nesse tipo de trabalho? Em estudos que avaliam LLMs realizando alguma tarefa de engenharia de software, uma decomposição que costuma render um conjunto forte de subquestões é separar correção (o resultado funciona?), qualidade (o resultado é bom?), preservação de comportamento (o resultado não quebrou nada que já funcionava?) e características do processo (em que situações o modelo vai bem, e em quais vai mal?). É essencialmente essa lógica que orienta as questões acima. 

Vamos além, podemos também investigar a complexidade da tarefa, com perguntas como:

- **QP5.** Quais características dos trechos de código estão associadas ao sucesso ou ao fracasso das refatorações geradas pelos modelos?

- **QP6.** Quais características dos tipos de *smell* estão associadas ao sucesso ou ao fracasso das refatorações geradas pelos modelos?


Essas últimas perguntas tendem a produzir um resultado bem mais interessante do que simplesmente reportar "o modelo A acertou 70% das vezes", porque explica o porquê do desempenho, não só o quanto.

Em trabalhos de pesquisa em Engenharia de Software, eu considero que perguntas que envolvem o porquê e como são potencialmente mais relevantes/desafiadoras do que perguntas que envolvem o que e quanto.


- **QP1 (enxuta).** Qual é a taxa de sucesso dos modelos na refatoração de código Clojure com *smells*?
- **QP2 (enxuta).** Em que medida as refatorações preservam o comportamento do programa e melhoram a qualidade estrutural do código?
- **QP3 (enxuta).** Como o desempenho dos modelos varia de acordo com o tipo e a dificuldade do *smell* sendo corrigido?

Essa sequência de perguntas é boa porque cria um fio, que gosto muito de usar: primeiro pergunta-se se o modelo consegue fazer a tarefa, depois se ele faz bem feito, e por fim em que situações funciona ou falha.

Importante: seu trabalho não precisa ter 6 questões de pesquisa. Não há um número definido para isso, nem um padrão. Tudo vai depender fo que você quer investigar e com qual profundidade. Contudo, meus trabalhos costumam ter entre duas e quatro questões de pesquisa. De novo, isso não é uma regra.


### Reconhecendo uma questão de pesquisa fraca

- **Muito ampla e com respostas monossilábicas.** "LLMs são capazes de refatorar código Clojure?" é vago demais: uma única refatoração correta já poderia, tecnicamente, ser apontada como evidência de capacidade. Uma possível solução seria trocar "capazes" por algo que dá para medir "Qual é a taxa de sucesso dos modelos em diferentes tarefas de refatoração em Clojure?".

- **Já inclui a conclusão.** "Quão melhores são os modelos que os desenvolvedores humanos na refatoração de Clojure?"  que os modelos são melhores, além de deixar "melhores" sem definição. Uma questão de pesquisa não deveria antecipar o resultado que só o experimento pode revelar.

- **É uma métrica disfarçada de questão.** "Qual modelo possui a maior taxa de acerto?" é mais uma pergunta de análise do que uma questão de pesquisa: ela cabe dentro de uma QP maior, como "Como diferentes modelos diferem quanto à correção das refatorações produzidas?", mas sozinha corre o risco de transformar o trabalho inteiro numa competição entre modelos, sem nenhuma reflexão sobre o fenômeno por trás dos números.

- **Dependente demais de um modelo específico.** "O modelo X consegue refatorar código Clojure?" amarra a contribuição do trabalho a uma ferramenta pontual, que em pouco tempo pode ser substituída por uma versão nova. Se o interesse é estudar o fenômeno de modelos de linguagem aplicados à refatoração, a questão deveria ser formulada no nível do fenômeno, deixando o modelo específico como uma variável independente dentro do projeto de experimento, não como o sujeito da pergunta. Contudo, para trabalhos com menor profundidade, como TCC, talvez a gente possa adotar essa forma.

- **Subjetiva.** "As refatorações geradas pelos modelos são boas?" não diz o que significa "boa". Boa em quê? A versão científica precisa basear o julgamento em algo concreto, uma métrica. Uma boa alternativa seria "Em que medida as refatorações geradas pelos modelos melhoram métricas de qualidade estrutural sem alterar o comportamento do programa?".

- **Confunde processo com resultado.** "Como os modelos pensam para refatorar código Clojure?" Pede algo que dificilmente se consegue responder de forma empírica só observando o código produzido, já que o processo interno do modelo pode não ser diretamente observável. Se for, uma boa alternativa pode ser "Quais estratégias ou padrões observáveis no processo de refatoração estão associados ao sucesso dos modelos?".

- **Tautológica.** "Os modelos conseguem realizar refatorações corretamente?" acaba sendo, na prática, apenas "quantas refatorações passam nos testes?", assim que "corretamente" é operacionalizado. Não é necessariamente inútil como objetivo de coleta de dados, mas é fraca demais para ser a questão central de um trabalho.

Um ponto que sempre reforço: como o exemplo já tem um recorte específico (Clojure e *smells*), vale explorar isso a fundo em vez de tratar a refatoração de forma genérica. Para trabalhos mais densos e profundos, como doutorado, o objetivo é subir a barra e tentar adicionar um tempero de generalização. Por exemplo, subir o nível para investigar mais representantes de linguagens funcionais, ao invés de somente Clojure.

## 2. Variáveis e métricas

Depois que as questões de pesquisa estão bem definidas, o próximo passo é traduzir cada uma delas em algo que pode ser efetivamente medido. Essa é a etapa em que se identifica o que vamos variar, o que vamos medir e como vamos medir. 

O ponto de partida é sempre separar as variáveis independentes das variáveis dependentes. As variáveis independentes são aquelas que a gente varia ou controla no experimento (o fator que se está testando). As variáveis dependentes são aquelas que se observa como resultado, e é sobre elas que as métricas são definidas. Um erro comum nessa etapa é listar variáveis de forma vaga, sem deixar claro o que está sendo manipulado e o que está sendo medido como consequência.

Voltando ao exemplo da refatoração de código Clojure com *smells*, as variáveis independentes seriam, por exemplo, o modelo de linguagem utilizado, o tipo de *smell* presente no código e o tamanho ou complexidade do trecho analisado. Já as variáveis dependentes seriam coisas como a corretude da refatoração, a preservação do comportamento do código e a qualidade do código resultante.

O passo seguinte é decidir com quais métricas cada variável dependente será medida. Não basta dizer "vou medir a qualidade da refatoração": é preciso definir precisamente como, ou seja, qual a métrica. No nosso caso, as métricas poderiam ser:

- Para a QP1 (remoção do *smell* sem quebrar o comportamento): proporção de refatorações em que o *smell* original desaparece, proporção de casos em que a suíte de testes original continua passando após a refatoração, e contagem de novos *smells* introduzidos.

- Para a QP2 (variação entre tipos de *smell*): as mesmas métricas anteriores, mas segmentadas por categoria de *smell*, permitindo comparação entre grupos.

- Para a QP3 (efeito do tamanho e da complexidade): correlação entre métricas de complexidade do trecho original (por exemplo, complexidade ciclomática ou número de linhas) e a taxa de sucesso da refatoração.

- Para a QP4 (comparação entre modelos): as mesmas métricas de corretude e qualidade, agora comparadas entre modelos. Aqui também requer a necessidade de um teste estatístico de comparação entre grupos.

Independente da métrica escolhida, **ela sempre precisa ser justificada**, não apenas citada. Se for usar complexidade ciclomática como *proxy* de qualidade de código, é preciso argumentar por que essa métrica é adequada para o fenômeno que está sendo estudado, e reconhecer as limitações dela. Métricas mal escolhidas, ou escolhidas só porque "é o que todo mundo usa", costumam ser o ponto mais frágil de defender.

## 3. Procedimento/método

Com as questões de pesquisa, variáveis e métricas já definidas, é preciso descrever como o experimento vai ser conduzido.

O procedimento deve ser descrito em etapas claras, cada uma com suas atividades específicas, e sempre que possível ligada explicitamente à questão de pesquisa que ela ajuda a responder. Insisto aqui sempre em ter uma figura que represente a metodologia.

No exemplo da refatoração de código Clojure, uma estrutura típica seria:

- **Etapa 1, seleção da amostra.** Definição do conjunto de trechos de código Clojure com *smells*, incluindo critérios de inclusão (por exemplo, projetos open source ativos, com testes automatizados) e a origem dos dados (dataset público, ou minerado pelo próprio aluno em repositórios do GitHub). Essa etapa dá suporte a todas as QPs, já que define o material sobre o qual tudo o mais será medido.
- **Etapa 2, execução das refatorações.** Cada modelo recebe o mesmo trecho de código e o mesmo prompt padronizado, e gera uma proposta de refatoração. É nessa etapa que o plano precisa deixar explícitas todas as decisões de prompt e de contexto fornecido ao modelo: o texto exato do prompt (e, se houver variações testadas, quais são e por quê), se há um *system prompt* separado, se são fornecidos exemplos no próprio prompt (*few-shot*) ou não, quanto do contexto do projeto é passado ao modelo além do trecho com o *smell* (só a função isolada? o arquivo inteiro? dependências relacionadas?), e os parâmetros de geração usados (temperatura, *top-p*, número máximo de tokens, entre outros). Essas decisões afetam diretamente o resultado e precisam ser fixadas e documentadas antes da execução, exatamente como se faz com qualquer outro parâmetro experimental, e não deixadas em aberto ou decididas "na mão" durante a coleta.

- **Etapa 3, avaliação das refatorações.** Aplicação das métricas definidas (precisão e revocação na detecção do *smell*, execução da suíte de testes, contagem de novos *smells*), possivelmente combinada com avaliação manual por especialistas quando a métrica automática não é suficiente. 

- **Etapa 4, análise estatística.** Comparação dos resultados entre tipos de *smell*, entre tamanhos de trecho e entre modelos. Essa etapa é a que fornece respostas concretas para as QPs.

Por fim, essa é a etapa em que é preciso antecipar as principais ameaças à validade do experimento e, mais importante, tomar decisões de projeto que as mitiguem, em vez de apenas listá-las como limitação no final do trabalho. No exemplo da refatoração, algumas ameaças típicas e as decisões correspondentes seriam:

- **Ameaça à validade de conclusão** (o resultado ser fruto do acaso). Mitigada por execuções repetidas, por exemplo, combinadas com teste estatístico adequado.
- **Ameaça à validade de construto** (a métrica não capturar de fato o que se quer medir). Mitigada, por exemplo, complementando a métrica automática de detecção de *smell* com uma avaliação manual por dois ou mais especialistas, reportando a concordância entre eles (*kappa* de Cohen).
- **Ameaça à validade interna** (viés introduzido pelo próprio desenho do experimento). No caso dos modelos de linguagem, um cuidado central é garantir que os trechos de código usados no teste não façam parte dos dados de treinamento dos modelos, o que contaminaria o resultado (*data leakage*). Outro cuidado é padronizar o prompt entre modelos, para que a comparação não seja, na prática, uma comparação de habilidade em seguir instruções específicas de cada modelo.
- **Ameaça à validade externa** (o quanto o resultado generaliza para além da amostra). Mitigada ampliando a diversidade da amostra de código (múltiplos projetos, múltiplos tipos de *smell*, diferentes tamanhos de trecho), e sendo explícito, na discussão dos resultados, sobre os limites do que foi testado (por exemplo, se só Clojure foi avaliado, não se pode generalizar para outras linguagens funcionais sem ressalvas).

As decisões são parte do projeto de experimento desde o início, e devem aparecer descritas junto com as etapas.
