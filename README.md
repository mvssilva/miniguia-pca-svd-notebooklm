# miniguia-pca-svd-notebooklm
# Redução de Dimensionalidade com PCA e SVD

## Contexto e Objetivos
O objetivo desse caderno é aprofundar meu conhecimento em um tema importante da ciencia de dados, que é a redução da dimensionalidade, como isso afeta os resultados obtidos em projetos, e quais são as principais técnicas pra solucionar esses problemas.

## Curadoria de Fontes
1. aula_pca.ipynb e aula_svd.ipynb: Notas de aulas disponibilizadas pelo professor de Introdução a ciência de dados, que apresentou a maldição da dimensionalidade e como isso afeta o estudo nessa área;
2. Data Mining and Machine Learning: Livro bem conceituado sobre os principais algoritmos de ciencia de dados, como são aplicados e como foram desenvolvidos.
3. Projection Matrix -- from Wolfram MathWorld: Fundamento algebrico de como toda esses algoritmos foram desenvolvidos.

## Engenharia de Prompts e "Cicatrizes"

**Tentativa 1: Entendendo o problema base**
- **O Prompt:** "Explique o que é a maldição da dimensionalidade e como técnicas como o PCA ajudam."
- **A Resposta da IA:** A IA explicou de forma detalhada os impactos da alta dimensionalidade. Ela destacou a esparsidade dos dados, a perda de utilidade das medidas de distância (prejudicando algoritmos como KNN), o aumento do custo computacional e o alto risco de *overfitting*. A resposta concluiu sugerindo o uso do PCA para manter a essência dos dados eliminando ruídos.
- **A Cicatriz (Troubleshooting):** Embora a resposta tenha sido teoricamente correta e muito rica, ela foi abstrata demais. O texto parecia um livro didático e não ajudava na prática. Percebi que faltou conectar esses conceitos com a etapa real de Análise de Importância e Seleção de Variáveis. A resposta não explicava como aplicar o PCA para agregação e geração de novas métricas antes de treinar um modelo de classificação. 

**Tentativa 2: Refinando para a prática (O Ajuste)**
- **O Novo Prompt:** (Aqui entrará o seu próximo prompt, focado na prática)
