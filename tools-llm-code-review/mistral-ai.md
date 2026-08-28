# Metadados

* [Mistral AI](https://mistral.ai/)
* Founded in April 2023 by previous employees of Meta Platforms and Google DeepMind

# Introdução

Mistral AI é uma empresa francesa que comercializa produtos de inteligência artificial (IA). A empresa levantou €385 milhões em outubro de 2023 e em dezembro de 2023 foi avaliada em mais de $2 bilhões.

Ela produz modelos de linguagem de código aberto, citando a importância fundamental do software de código aberto e como resposta aos modelos proprietários.

Até março de 2024, dois modelos foram publicados e estão disponíveis como pesos. Três modelos adicionais, *Small*, *Medium* e *Large*, estão disponíveis apenas via API.

# Mistral 7B

Mistral 7B é um modelo de linguagem com 7,3 bilhões de parâmetros que utiliza a arquitetura de transformers. O modelo foi lançado sob a licença Apache 2.0. A postagem no blog de lançamento afirma que o modelo supera o LLaMA 2 13B em todos os benchmarks testados e está em pé de igualdade com o LLaMA 34B em muitos dos benchmarks testados.

O Mistral 7B utiliza uma arquitetura semelhante ao LLaMA, mas com algumas mudanças no mecanismo de *attention*. Em particular, ele utiliza a *Grouped-query attention* (GQA) destinada a uma inferência mais rápida e a *Sliding Window Attention* (SWA) destinada a lidar com sequências mais longas.

A *Sliding Window Attention* (SWA) reduz o custo computacional e de memória para sequências mais longas. Na *Sliding Window Attention*, cada token só pode atender a um número fixo de tokens da camada anterior em uma "janela deslizante" de 4096 tokens, com um comprimento total de contexto de 32768 tokens. No momento da inferência, isso reduz a disponibilidade de cache, levando a uma latência mais alta e a uma menor taxa de transferência. Para amenizar esse problema, o Mistral 7B utiliza um *rolling buffer cache*.

Tanto um modelo base quanto um modelo "instruct" foram lançados, sendo que este último recebeu ajustes adicionais para seguir prompts de estilo de conversa. O modelo *tunado* é destinado apenas para fins de demonstração e não possui *guardrails* ou *moderation* incorporados.

# Mixtral 8x7B

Ao contrário do Mistral 7B, o Mixtral 8x7B utiliza uma arquitetura de *sparse mixture of experts*. O modelo possui 8 grupos distintos de "especialistas", dando ao modelo um total de 46,7 bilhões de parâmetros utilizáveis. Cada token único pode utilizar apenas 12,9 bilhões de parâmetros, portanto, proporcionando a velocidade e o custo que um modelo de 12,9 bilhões de parâmetros incorreria.

Os testes da Mistral AI mostram que o modelo supera tanto o LLaMA 70B quanto o GPT-3.5 na maioria dos benchmarks.

# Avaliação e Resultados

## Mistral 7B

O Mistral 7B foi comparado com a família Llama 2 e todas as avaliações dos modelos foram re-executadas para uma comparação justa.

![bars](https://mistral.ai/images/news/announcing-mistral-7b/230927_bars.png)

*Desempenho do Mistral 7B e diferentes modelos Llama em uma ampla gama de benchmarks. Para todas as métricas, todos os modelos foram reavaliados com o pipeline de avaliação para uma comparação precisa. O Mistral 7B supera significativamente o Llama 2 13B em todas as métricas e está em pé de igualdade com o Llama 34B (já que o Llama 2 34B não foi lançado, os resultados são relatados no Llama 34B). Também é vastamente superior em benchmarks de code e reasoning.*

OS benchmarks são categorizados por tema:

- Commonsense Reasoning: média de 0-shot de Hellaswag, Winogrande, PIQA, SIQA, OpenbookQA, ARC-Easy, ARC-Challenge e CommonsenseQA.
- World Knowledge: média de 5-shot de NaturalQuestions e TriviaQA.
- Reading Comprehension: média de 0-shot de BoolQ e QuAC.
- Math: Média de 8-shot GSM8K com maj@8 e 4-shot MATH com maj@4
- Code: Média de 0-shot Humaneval e 3-shot MBPP
- Popular aggregated results: 5-shot MMLU, 3-shot BBH e 3-5-shot AGI Eval (apenas perguntas de múltipla escolha em inglês)

![table](https://mistral.ai/images/news/announcing-mistral-7b/230927_table.png)

Uma métrica interessante para comparar como os modelos se saem no eixo custo/desempenho é calcular "tamanhos de modelo equivalentes". Em reasoning, comprehension e STEM reasoning (MMLU), o Mistral 7B tem desempenho equivalente a um Llama 2 que seria mais de 3x seu tamanho. Isso equivale a economia de memória e ganho de *throughput*.

![effective_sizes](https://mistral.ai/images/news/announcing-mistral-7b/230927_effective_sizes.png)

*Resultados no MMLU, Commonsense Reasoning, World Knowledge e Reading comprehension para Mistral 7B e Llama 2 (7B/13/70B). O Mistral 7B supera amplamente o Llama 2 13B em todas as avaliações, exceto nos benchmarks de knowledge, onde está em pé de igualdade (isso provavelmente é devido à sua contagem de parâmetros limitada, que restringe a quantidade de conhecimento que pode ser comprimida).*

## Mixtral 8X7B

O Mixtral foi comparado com a família Llama 2 e o modelo base GPT3.5. O Mixtral corresponde ou supera o Llama 2 70B, assim como o GPT3.5, na maioria dos benchmarks.

![overview](https://mistral.ai/images/news/mixtral-of-experts/overview.png)

Na figura a seguir, observamos o *tradeoff* entre qualidade e orçamento de inferência. O Mistral 7B e o Mixtral 8x7B pertencem a uma família de modelos altamente eficientes em comparação com os modelos Llama 2.

![scaling](https://mistral.ai/images/news/mixtral-of-experts/scaling.png)

A tabela a seguir fornece resultados detalhados sobre a figura acima.

![open_models](https://mistral.ai/images/news/mixtral-of-experts/open_models.png)

**Alucinação e vieses.** Para identificar possíveis falhas a serem corrigidas por *fine-tuning* / *preference modelling*, foi medido o desempenho do modelo base no BBQ/BOLD.

![bbq_bold](https://mistral.ai/images/news/mixtral-of-experts/bbq_bold.png)

Comparado ao Llama 2, o Mixtral apresenta menos viés no benchmark BBQ. No geral, o Mixtral exibe mais sentimentos positivos do que o Llama 2 no BOLD, com variâncias semelhantes dentro de cada dimensão.

**Idiomas**. Mixtral 8x7B domina francês, alemão, espanhol, italiano e inglês.

![multilingual](https://mistral.ai/images/news/mixtral-of-experts/multilingual.png)

# Discussão

- Podemos utilizar esses modelos em nossos trabalhos, tendo em vista que, com eles, conseguimos realizar tarefas como classificação, embeddings e RAG.

# Replicação

* Pesos: [Open-weight models](https://docs.mistral.ai/models/)
* Modelos: [Mistral AI_](https://huggingface.co/mistralai)
* Conseguiu entender/rodar? Sim, foi possível utilizar a API do Hugging Face para fazer inferências.
