# Classificação de Score de Crédito com Machine Learning: Data Girls Finance

![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine_Learning-orange.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-Ensemble-red.svg)
![LIME](https://img.shields.io/badge/LIME-Explainable_AI-green.svg)
![Status](https://img.shields.io/badge/Status-Concluído-success.svg)

## 1. Resumo Executivo e Objetivo do Projeto
Este projeto visa otimizar, escalar e trazer inteligência orientada a dados para o processo de análise de crédito da fintech fictícia **Data Girls Finance**[cite: 1]. 

Atualmente, a avaliação dos clientes depende de análises manuais que são demoradas e sujeitas a inconsistências[cite: 1]. O objetivo principal foi desenvolver um modelo preditivo robusto capaz de classificar automaticamente o score de crédito de clientes (*Poor, Standard, Good*) com base em seu histórico de pagamentos, perfil de crédito e comportamento financeiro[cite: 1].

## 2. Metodologia e Pipeline de Ciência de Dados
O projeto seguiu um fluxo de trabalho rigoroso para garantir a confiabilidade do modelo, a prevenção de vazamento de dados e o cumprimento de regras de negócio:

1. Ingestão e Governança: Utilização do dataset "Credit Score Classification" proveniente do Kaggle[cite: 1], com remoção imediata de dados sensíveis (LGPD).
2. Separação de Dados: Divisão estratificada em Treino (80%) e Teste (20%) garantindo isolamento total antes de qualquer transformação matemática.
3. Engenharia e Limpeza: Construção de esteiras automatizadas (`ColumnTransformer`) para tratamento de nulos e conversão de variáveis textuais via `OrdinalEncoder`.
4. Análise Exploratória: Investigação de distribuições, identificação de outliers e validação de multicolinearidade através de Mapas de Calor.
5. Modelagem Avançada: Treinamento, *tuning* e comparação de três algoritmos de naturezas matemáticas distintas (Linear, Bagging e Boosting)[cite: 1].

## 3. Principais Achados e Insights de Negócio
A Análise Exploratória de Dados revelou padrões comportamentais cruciais para a capacidade de pagamento dos clientes[cite: 1]:
* Dívida Pendente: A variável `Outstanding_Debt` demonstrou a maior correlação com a inadimplência. A mediana de dívida do grupo "Poor" é superior à do grupo "Good".
* Pagamento Mínimo: Clientes que possuem o comportamento de pagar apenas o valor mínimo da fatura apresentam uma alta probabilidade de rebaixamento de Score para a classe "Poor"[cite: 1].
* Multicolinearidade: O cruzamento de variáveis validou que comportamentos de consumo (número de contas e número de cartões) caminham de forma redundante em muitos perfis, exigindo algoritmos capazes de lidar com alta complexidade.

## 4. Performance da Modelagem Preditiva
Para garantir a melhor qualidade de modelagem, testamos e comparamos modelos baseados em métricas de classificação (*Accuracy, Precision, Recall e F1-Score*)[cite: 1]:

* Regressão Logística (Baseline Linear): ~59% de Acurácia. Falhou em capturar a não-linearidade do comportamento financeiro humano.
* XGBoost (Ensemble Boosting): ~72% de Acurácia.
* Random Forest (Campeão via GridSearchCV): **~78% de Acurácia.**

**Conclusão de Risco:** O Random Forest foi eleito o modelo de produção não apenas pela acurácia superior, mas por ser um modelo conservador. A Matriz de Confusão comprovou que ele comete raríssimos Falsos Positivos críticos, previnindo o caixa da instituição contra calotes passivos[cite: 1].

## 5. Explicabilidade e Compliance (LIME) - Bônus
Para garantir que a Inteligência Artificial não atue como uma "caixa preta", implementei a biblioteca LIME[cite: 1]. 

* Transparência Legal: O modelo consegue explicar visualmente e de forma individualizada o porquê de cada decisão[cite: 1]. Isso permite à equipe de negócios explicar claramente ao cliente as razões de uma recusa de crédito, respeitando o direito do consumidor e facilitando a comunicação para pessoas não técnicas[cite: 1].

## 6. Recomendações Práticas (Plano de Ação)
Com base nos resultados, é recomendado à Data Girls Finance as seguintes ações estratégicas[cite: 1]:
1. **Automação da Esteira (Triage):** Integrar o modelo via API para aprovar diretamente os clientes preditos como "Good" e negar os perfis "Poor", reduzindo custos operacionais.
2. **Foco da Equipe Humana:** Redirecionar os analistas de crédito para avaliar manualmente apenas os casos classificados como "Standard" [cite: 1].
3. **Ações Preventivas de Marketing:** Disparar campanhas de renegociação de dívidas ou educação financeira para clientes que começarem a pagar apenas o mínimo da fatura, antes que se tornem inadimplentes.

## 7. Estrutura do Repositório
```text
📦 Projeto_Credito
 ┣ 📂 data
 ┃ ┣ 📂 raw          # Dados originais (Ignorados no Git)
 ┃ ┗ 📂 processed    # Dados limpos
 ┣ 📂 notebooks      # Jupyter Notebook com a EDA e Modelagem Completa
 ┣ 📂 images         # Gráficos e painéis gerados pelo LIME e Matriz de Confusão
 ┣ 📜 README.md      # Apresentação do projeto
 ┗ 📜 requirements.txt # Dependências