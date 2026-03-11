# Miniguia: Redução de Dimensionalidade com PCA e SVD

## Contexto e Objetivos
O objetivo deste repositório é documentar meus estudos sobre redução de dimensionalidade, um desafio muito comum que tenho encontrado ao trabalhar com bases de dados complexas. Quero sair apenas da teoria e entender na prática como a "maldição da dimensionalidade" afeta o desempenho e o custo computacional dos modelos preditivos, focando em como aplicar técnicas como PCA e SVD na etapa de engenharia de *features* e seleção de variáveis.

## Curadoria de Fontes
Para montar este material, utilizei uma base que mistura teoria acadêmica com fundamentos matemáticos:
1. **`aula_pca.ipynb` e `aula_svd.ipynb`:** Notas de aula disponibilizadas pelo meu professor de Introdução à Ciência de Dados, que apresentam o problema da maldição da dimensionalidade e seus impactos.
2. **Data Mining and Machine Learning:** Livro de referência sobre os principais algoritmos de *machine learning*, focando em como são desenvolvidos e aplicados na prática.
3. **Projection Matrix (Wolfram MathWorld):** Documentação técnica essencial para revisar os fundamentos algébricos por trás da construção desses algoritmos.

## Engenharia de Prompts e "Cicatrizes"

**Tentativa 1: Entendendo o problema base**
- **O Prompt:** *"Explique o que é a maldição da dimensionalidade e como técnicas como o PCA ajudam."*
- **A Resposta da IA:** A IA explicou detalhadamente os impactos da alta dimensionalidade, destacando a esparsidade dos dados, a perda de utilidade no cálculo de distâncias (o que prejudica algoritmos como o KNN) e o risco de *overfitting*. Concluiu sugerindo o PCA para manter a essência dos dados e eliminar ruídos.
- **A Cicatriz (Troubleshooting):** A resposta veio muito teórica. Explicou bem o conceito, mas parecia um trecho de livro didático. Não me ajudou a entender como aplicar isso no código, especialmente na hora de fazer a agregação de variáveis e gerar novas métricas antes de treinar o modelo. Faltou foco na prática.

**Tentativa 2: Refinando para a prática (O Ajuste)**
- **O Novo Prompt:** *"Atue como um cientista de dados sênior. Deixando a teoria matemática de lado, me dê um exemplo prático de como aplicar o PCA na etapa de 'Análise de Importância e Seleção de Variáveis' em um dataset complexo (como dados de e-commerce). Foque em como posso usar o PCA especificamente para a etapa de processamento, agregação e geração de novas métricas antes de treinar um modelo de classificação binária."*
- **A Resposta da IA:** A ferramenta entregou um passo a passo mais voltado para o pipeline de dados. Explicou a obrigatoriedade da padronização prévia, como o PCA agrupa variáveis correlacionadas em "Componentes Principais" e a regra de reter apenas os componentes que explicam cerca de 95% da variância. 
- **O Resultado (Avaliação e Aprendizado):** Aqui a resposta melhorou muito. A IA focou na engenharia de *features* e me deu um alerta importante: como o PCA é não-supervisionado, ele é "cego" em relação à variável alvo. Isso significa que existe o risco de ele descartar (como se fosse ruído) justamente os detalhes que o meu classificador binário precisaria para separar as classes corretamente. A resposta também deixou um ótimo gancho para estudar o SVD como alternativa para matrizes esparsas.

  ## Miniguia de Estudo

### 1. Resumo Estruturado: Pipeline de Redução de Dimensionalidade
Aqui está o passo a passo prático de como algoritmos como o PCA e o SVD funcionam nos bastidores para atuar como o nosso "espremedor de dados". Esse é o fluxo de trabalho (pipeline) típico aplicado antes de treinar um modelo de inteligência artificial:

** Preparação da Régua (Pré-processamento e Padronização)**
Antes de o algoritmo procurar padrões, você precisa garantir que todas as informações estejam na mesma escala de medida.
*   **O que é feito:** Subtrai-se a média de cada variável (centralização) e divide-se pelo desvio padrão. 
*   **Por que é vital:** Se você não fizer isso, uma coluna com valores numéricos naturalmente grandes (como "Salário em Reais") vai ofuscar completamente uma coluna com números pequenos (como "Idade"), enganando o algoritmo.
*   *Nota prática:* Se a sua planilha for gigante e quase vazia (matriz esparsa, cheia de zeros), você pula a etapa de centralizar a média e usa o algoritmo SVD diretamente para não estourar a memória do computador.

** Mapeamento dos Padrões (Cálculo de Covariância e Autovetores)**
É aqui que o nosso "fotógrafo de dados" começa a procurar o melhor ângulo da informação.
*   **O que é feito:** O sistema calcula como todas as colunas da sua planilha variam umas em relação às outras. Em seguida, ele usa o motor matemático (como a Decomposição Espectral ou o SVD) para encontrar as direções ocultas de maior variação nos dados.
*   **O resultado:** Ele gera os chamados **Componentes Principais** (ou autovetores), que são as novas "super-métricas" descorrelacionadas, e os **Autovalores**, que são notas que medem a "força" ou a quantidade de informação que cada componente conseguiu capturar.

** O Corte e Seleção (Ranking de Importância)**
Você não vai usar todos os padrões encontrados, caso contrário, não haveria compressão.
*   **O que é feito:** O algoritmo ordena essas novas super-métricas da mais forte (a que capturou mais variância) para a mais fraca. 
*   **A Regra de Bolso:** Você define um limite de quanta informação original quer salvar (por exemplo, 95% da essência dos dados). O sistema retém apenas a quantidade de componentes principais no topo do ranking necessária para bater essa meta, descartando o resto como se fosse "lixo" ou ruído.

** O Achatamento (Projeção dos Dados)**
Agora que escolhemos os melhores ângulos, tiramos a foto final.
*   **O que é feito:** A planilha original (que poderia ter milhares de colunas) é matematicamente projetada e reconstruída usando apenas aqueles poucos componentes fortes que você selecionou no passo anterior.
*   **O resultado:** Você ganha um banco de dados novo, extremamente leve, compactado e muito mais fácil de ser interpretado.

** O Teste Prático (Treinamento do Modelo de Machine Learning)**
Com o banco de dados comprimido em mãos, você finalmente o entrega para o seu algoritmo de classificação (como uma Regressão Logística).
*   **Atenção ao *Trade-off*:** Nesse passo, o modelo roda muito mais rápido e fica protegido contra o aluno que "decora" (*overfitting*). No entanto, como você jogou fora uma porcentagem da informação no Passo 3, você deve monitorar se o seu modelo não perdeu precisão ao ficar "cego" para algum micro-detalhe importante que foi descartado.


### 2. Glossário Prático
* **Redução de Dimensionalidade:** É o processo de "espremer" um conjunto de dados gigante para diminuir o número de características (colunas), guardando apenas a essência da informação. Isso ajuda a evitar o sobreajuste (overfitting), economiza capacidade de processamento e melhora a visualização dos dados, descartando o que é ruído ou redundância.
* **Maldição da Dimensionalidade:** É o problema do "excesso de detalhes". Acontece quando os dados possuem tantas dimensões que a informação se espalha excessivamente, criando espaços vazios. Na prática, isso atrapalha o aprendizado da máquina, deixa o processamento muito caro e faz com que a tentativa de medir semelhanças (distâncias geométricas) entre os pontos de dados deixe de fazer sentido.
* **PCA (Análise de Componentes Principais):** Funciona como um "fotógrafo de dados" buscando o melhor ângulo. É um algoritmo famoso que resume os dados descobrindo as direções onde eles possuem a maior variação (variância). Ao achar esse "melhor ângulo", o PCA projeta os dados em um espaço menor, preservando o máximo possível das características originais.
* **SVD (Decomposição em Valores Singulares):** É o "espremedor matemático" de dados. Trata-se de uma técnica de álgebra linear que quebra uma matriz complexa e gigante em três blocos menores e essenciais, revelando o que chamamos de baixo rank efetivo. É ideal para trabalhar com matrizes gigantes e esparsas (cheias de zeros), sendo muito usado na compressão de imagens digitais e na recomendação de filmes, como faz a Netflix.
* **Autovetores e Autovalores (Eigenvectors e Eigenvalues):** Podem ser vistos como a "bússola" e a "régua" dos algoritmos. Durante cálculos de redução (como o PCA), o autovetor aponta a direção exata onde os dados têm o seu padrão de maior variação, enquanto o autovalor é o número que mede a "força" dessa variação, indicando a quantidade de informação que aquela direção específica conseguiu capturar.

### 3. Prompts Reutilizáveis
Se eu precisar revisar esse tema ou aplicar em um novo projeto, estes prompts geram respostas excelentes na IA:
* *"Analise este conjunto de variáveis: [colar lista de colunas]. Tenho muitos dados correlacionados e alguns com muitos zeros. Me recomende, com justificativa técnica, se devo usar PCA ou Truncated SVD para reduzir a dimensionalidade antes de treinar um classificador binário."*
* *"Atue como um revisor de código sênior. Revise este trecho de código em Python usando `scikit-learn` onde aplico PCA. Verifique se estou cometendo o erro de vazamento de dados (data leakage) entre meus conjuntos de treino e teste durante a etapa de `fit_transform`."*
* *"Explique o conceito matemático de 'Autovetores e Autovalores' usando uma analogia simples do mundo real, focando apenas em como eles definem a direção e a força dos Componentes Principais no PCA."*
