# 🗳️ Correção Preditiva e Análise de Viés de Amostragem — Pesquisa Literary Digest (1936)

Este repositório contém o projeto desenvolvido o objetivo principal de investigar as causas do histórico erro preditivo cometido pela revista The Literary Digest na eleição presidencial dos EUA em 1936 e aplicar técnicas modernas de Machine Learning e Engenharia de Atributos para corrigir o viés de amostragem dos dados.

📌 Contexto Histórico e O Problema

Em 1936, a revista The Literary Digest realizou a maior pesquisa eleitoral de intenção de voto até então registrada, enviando cerca de 10 milhões de questionários postais e obtendo quase 2,4 milhões de respostas. Com base nessa quantidade massiva de dados, a publicação previu a vitória esmagadora do candidato republicano Alf Landon (57% contra 43%).

No entanto, o resultado real da eleição deu a vitória a Franklin D. Roosevelt com 62% dos votos populares (vencendo em 46 dos 48 estados da época), no que se tornou o maior colapso preditivo da história estatística.

As causas do viés:

Viés de Amostragem (Sampling Bias): As listas de entrevistados foram montadas a partir de listas de assinantes de listas telefônicas e proprietários de automóveis — um grupo de alta renda desproporcionalmente conservador em pleno contexto da Grande Depressão.

Viés de Não-Resposta (Non-response Bias): A taxa de resposta foi de apenas ~23,8%, distorcida por eleitores insatisfeitos que responderam em maior proporção.

🎯 Objetivo do Projeto

O objetivo fundamental foi provar que a qualidade e a representatividade dos dados são mais críticas do que a quantidade de registros.

Utilizando algoritmos de Aprendizado de Máquina (Support Vector Machines - SVM) calibrados por um histórico de eleições anteriores (1924, 1928 e 1932), o projeto buscou:

Eliminar a distorção da escala populacional de cada estado.

Capturar a migração real do eleitorado (Swing eleitoral).

Construir um modelo preditivo capaz de superar o viés da revista e prever corretamente o vencedor da eleição de 1936.

🛠️ Metodologia e Engenharia de Atributos

1. Pré-processamento e Engenharia de Shares

Para evitar que o modelo sofresse distorções causadas por estados mais populosos (como New York) em comparação com estados menores (como Wyoming), transformamos contagens absolutas de votos em proporções relativas (Shares):

$$\text{RepShare} = \frac{\text{Votos Rep. (Pesquisa)}}{\text{Total de Pesquisas do Estado}}$$

$$\text{DemShare} = \frac{\text{Votos Dem. (Pesquisa)}}{\text{Total de Pesquisas do Estado}}$$

2. Swing Eleitoral

Calculamos a variação proporcional entre as intenções de voto atuais e o histórico eleitoral prévio:

$$
\text{SwingDem} = \text{DemShare}_{\text{atual}} - \text{DemShare}_{\text{histórico}}
$$

3. Pipeline do Modelo

Algoritmo: Support Vector Classifier (SVC) com Kernel RBF.

Normalização: StandardScaler integrado ao Pipeline do Scikit-Learn.

Tratamento de Desbalanceamento: class_weight='balanced'.

Hiperparâmetros Ideais: C = 100.0, gamma = 'scale'.

Validação: Treinamento em dados temporais passados (1924–1932) e teste cego na eleição de 1936.

📊 Resultados Obtidos

Acurácia Geral: 79,17% (38 de 48 amostras estaduais classificadas corretamente).

Métricas por Classe (Teste de 1936):

Classe Democrata: Precisão = 1.00 | Recall = 0.78 | F1-Score = 0.88

Classe Republicana: Precisão = 0.17 | Recall = 1.00 | F1-Score = 0.29
