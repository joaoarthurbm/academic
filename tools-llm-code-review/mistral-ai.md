# Metadados

* Mistral AI
* Founded in April 2023 by previous employees of Meta Platforms and Google DeepMind
* [Site](https://mistral.ai/)

# Qual a solução?

## Como os autores tentam resolver o problema? Criando um algoritmo novo? uma metodologia? uma ferramenta? 

Exemplo: Os autores apresentam uma nova estratégia de cache específica para lidar com transações. Nessa estratégia, a ideia é levar em consideração a natureza "tudo-ou-nada" das transações. Como prova de conceito, é apresentada um sistema de cache de alta performance chamado dtox, que ...

## Quais são os detalhes técnicos dessa solução? O que chama mais atenção? Qual a ideia geral e o que deve ser discutido em mais detalhes?

Exemplo: os autores agrupam objetos de uma transação utilizando uma análise de grafos acíclicos de dependência, através de uma heurística que funciona da seguinte maneira: ...

# Resultados

## Mistral 7B

We compared Mistral 7B to the Llama 2 family, and re-run all model evaluations ourselves for fair comparison.

![bars](https://mistral.ai/images/news/announcing-mistral-7b/230927_bars.png)

*Performance of Mistral 7B and different Llama models on a wide range of benchmarks. For all metrics, all models were re-evaluated with our evaluation pipeline for accurate comparison. Mistral 7B significantly outperforms Llama 2 13B on all metrics, and is on par with Llama 34B (since Llama 2 34B was not released, we report results on Llama 34B). It is also vastly superior in code and reasoning benchmarks.*

The benchmarks are categorized by their themes:

- Commonsense Reasoning: 0-shot average of Hellaswag, Winogrande, PIQA, SIQA, OpenbookQA, ARC-Easy, ARC-Challenge, and CommonsenseQA.
- World Knowledge: 5-shot average of NaturalQuestions and TriviaQA.
- Reading Comprehension: 0-shot average of BoolQ and QuAC.
- Math: Average of 8-shot GSM8K with maj@8 and 4-shot MATH with maj@4
- Code: Average of 0-shot Humaneval and 3-shot MBPP
- Popular aggregated results: 5-shot MMLU, 3-shot BBH, and 3-5-shot AGI Eval (English multiple-choice questions only)

![table](https://mistral.ai/images/news/announcing-mistral-7b/230927_table.png)

An interesting metric to compare how models fare in the cost/performance plane is to compute “equivalent model sizes”. On reasoning, comprehension and STEM reasoning (MMLU), Mistral 7B performs equivalently to a Llama 2 that would be more than 3x its size. This is as much saved in memory and gained in throughput. 

![effective_sizes](https://mistral.ai/images/news/announcing-mistral-7b/230927_effective_sizes.png)

*Results on MMLU, Commonsense Reasoning, World Knowledge and Reading comprehension for Mistral 7B and Llama 2 (7B/13/70B). Mistral 7B largely outperforms Llama 2 13B on all evaluations, except on knowledge benchmarks, where it is on par (this is likely due to its limited parameter count, which restricts the amount of knowledge it can compress).*

## Mixtral 8X7B

We compare Mixtral to the Llama 2 family and the GPT3.5 base model. Mixtral matches or outperforms Llama 2 70B, as well as GPT3.5, on most benchmarks.

![overview](https://mistral.ai/images/news/mixtral-of-experts/overview.png)

On the following figure, we measure the quality versus inference budget tradeoff. Mistral 7B and Mixtral 8x7B belong to a family of highly efficient models compared to Llama 2 models.

![scaling](https://mistral.ai/images/news/mixtral-of-experts/scaling.png)

The following table give detailed results on the figure above.

![open_models](https://mistral.ai/images/news/mixtral-of-experts/open_models.png)

**Hallucination and biases.** To identify possible flaws to be corrected by fine-tuning / preference modelling, we measure the base model performance on BBQ/BOLD.

![bbq_bold](https://mistral.ai/images/news/mixtral-of-experts/bbq_bold.png)

Compared to Llama 2, Mixtral presents less bias on the BBQ benchmark. Overall, Mixtral displays more positive sentiments than Llama 2 on BOLD, with similar variances within each dimension.

**Language.** Mixtral 8x7B masters French, German, Spanish, Italian, and English.

![multilingual](https://mistral.ai/images/news/mixtral-of-experts/multilingual.png)

# Discussão

Deixar aqui os comentários e insights importantes que surgiram durante a discussão do paper com o grupo. Colocar aqui ideias de trabalhos de pesquisa que podem ser feitas a partir desse trabalho. Por exemplo, experimentar com outra base, estender a análise para outro algoritmo, modelo etc.

# Replicação

* Pesos: [Open-weight models](https://docs.mistral.ai/models/)
* Modelos: [Mistral AI_](https://huggingface.co/mistralai)
* Conseguiu entender/rodar? Sim, foi possível utilizar a API do Hugging Face para fazer inferências.
