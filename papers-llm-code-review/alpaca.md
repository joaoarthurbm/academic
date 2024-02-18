# Metadados

Título: *“Alpaca: A Strong, Replicable Instruction-Following Model”*

Autores: [*Rohan Taori](https://www.rohantaori.com/)*, [Ishaan Gulrajani](https://ishaan.io/), [Tianyi Zhang](https://tiiiger.github.io/), [Yann Dubois](https://yanndubs.github.io/), [Xuechen Li](https://www.lxuechen.com/), [Carlos Guestrin](https://guestrin.su.domains/), [Percy Liang](https://cs.stanford.edu/~pliang/), [Tatsunori B. Hashimoto](https://thashim.github.io/);*

Instituição(ões) envolvida(s) na pesquisa: *Stanford*

Ano de publicação: *2023*

Link para acesso: <https://crfm.stanford.edu/2023/03/13/alpaca.html> 

# Qual o problema abordado pelo artigo?

Apesar da constante evolução dos modelos, a utilização desses ainda é uma atividade que requer muitos recursos computacionais. Além disso, no contexto de modelos do tipo *“instruction-following”*, existem ainda muitas deficiências, como: 
- Geração de falsa informação;
- Reprodução de estereótipos;
- Linguagem imprópria.

Na época em que esta pesquisa foi desenvolvida não haviam modelos específicos *open-source* que se equiparavam aos modelos *closed-source*, como por exemplo o *text-davinci-003 (GPT 3.5)*. Por serem projetos de cunho privado, os modelos *closed-source* só eram disponíveis para utilização mediante pagamento e com o hardware necessário para isso, o que é um custo significativo para as linhas de pesquisa. Além disso, existe também a falta de informações disponíveis sobre o treinamento e o funcionamento desses modelos, impossibilitando pesquisadores de obterem dados confiáveis.

Dessa forma, o intuito dos autores desse artigo é construir um modelo open-source desenvolvido para uma atividade específica e que seja comparável aos grandes modelos *closed-source* treinados a partir de uma quantidade consideravelmente menor de dados e exigindo menos recursos.

# Qual a solução?

  A solução encontrada pelos pesquisadores de *Stanford* foi o modelo Alpaca, derivado do *LLaMA* *7B*, do tipo *instruction-following*, treinado com uma menor quantidade de dados e com menos recursos computacionais envolvidos. Assim, a ideia central acerca da construção desse modelo é a de poder acessibilizar o acesso aos modelos e auxiliar novos pesquisadores da área em pesquisas futuras.

# Como o modelo foi treinado?

  O Alpaca foi treinado com um conjunto de dados composto por 52 mil demonstrações do tipo *instruction-following,* geradas no text-davinci-003, utilizando 175 exemplos criados por humanos. Assim, o treinamento do modelo só foi possível devido ao lançamento da Meta no início do ano de 2023, o LLaMA 7B. 
  Como um dos nortes da pesquisa, utilizaram o seguinte artigo “*Self-Instruct: Aligning Language Models with Self-Generated Instructions”*, que sugere uso de um bom modelo para a geração dos dados de treinamento. As 175 demonstrações escritas por humanos foram retiradas do artigo mencionado acima e estão disponíveis neste link: <https://github.com/yizhongw/self-instruct> 
  Assim, o ajuste fino do LLaMA se deu utilizando os seguintes recursos e estratégias:
- Framework de treinamento do Hugging Face <https://huggingface.co/docs/transformers/training> 
- Técnica Fully Sharded Data Parallel <https://engineering.fb.com/2021/07/15/open-source/fsdp/>  <https://huggingface.co/docs/accelerate/usage_guides/fsdp> 
- Técnica Mixed Precision Training <https://arxiv.org/abs/1710.03740> 

Por fim, foram necessárias 3 horas para fazer o ajuste fino do LLaMA 7B utilizando 8 80G A100 da NVIDIA. Ao todo, foram necessários menos de 600 dólares para a pesquisa, sendo boa parte do dinheiro gasto no consumo da API da Open AI para gerar o conjunto de dados de treinamento.

# Como o modelo foi avaliado?

  A avaliação foi feita manualmente por 5 autores do projeto a partir dos inputs do conjunto de dados de validação do artigo de Self-Instruct. Dessa forma, foram comparadas as saídas do modelo *text-davinci-003* e do Alpaca 7B. Ainda mais, no intuito de evitar viés na análise, ela foi realizada de forma com a qual os avaliadores não sabiam qual modelo estavam avaliando.

# Quais são os resultados?

  A avaliação manual revelou que o Alpaca 7B e o *text-davinci-003* possuem performance similar. O Alpaca 7B ganhou do *text-davinci-003* por 90 a 89. Entretanto, como eles não avaliaram o modelo para muitas saídas, foi lançada uma versão demo em que você poderia interagir com o Alpaca de sua máquina, a fim de entender melhor o comportamento do modelo lançado. Porém, esta demo encontra-se atualmente fora do ar com a justificativa de que passou um tempo considerável no ar e que a faculdade iria poupar os recursos de mantê-la disponível para acesso.

# Resenha Crítica

O Alpaca 7B trouxe novas perspectivas e avanços para a área de LLMs, mesmo com tantas limitações. Ao tempo de seu lançamento não haviam modelos *open-source* construídos por pesquisadores que pudessem atingir o mesmo nível que os *closed-source* (financiados por empresas privadas que não disponibilizam informações públicas suficientes). Dessa forma, o grupo de pesquisa conseguiu obter êxito na tarefa desempenhada, além de conseguir contribuir com novos estudos acerca do funcionamento e treinamento de modelos LLM. 

A parte a qual pecaram se dá pelo fato de não terem publicado um artigo que contivesse mais detalhes sobre o processo de treinamento do modelo, apenas foi exemplificado quais estratégias foram utilizadas. Além disso, outro ponto fraco deste artigo se dá ao fato da forma como as avaliações foram feitas. Um dos grandes empecilhos na área é a forma de como podemos avaliar as respostas geradas pelo modelo que criamos, e, com toda certeza, a avaliação puramente manual desses dados não gera resultados muito confiáveis.

Em contrapartida, a forma como esse modelo foi treinado e as técnicas utilizadas, além das referências ao artigo citado, conseguem nortear outros pesquisadores em pesquisas futuras. Assim, apesar de conter falhas no desenvolvimento do artigo, este foi um passo importante para a área de pesquisas em LLMs.


