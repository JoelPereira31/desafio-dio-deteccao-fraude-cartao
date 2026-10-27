# Detector de Fraudes em Cartão de Crédito 💳🤖

Projeto prático desenvolvido para treinar modelos de Machine Learning em um cenário de **alto desbalanceamento de dados** (apenas 0,17% de fraudes).

## 1. O Problema e o Desafio da Acurácia
Em problemas de fraude, a acurácia é uma métrica ilusória. Se um modelo prever que *nenhuma* transação é fraude, ele terá 99,83% de acurácia, mas falhará completamente no seu propósito. O foco aqui foi priorizar o **Recall** (quantas fraudes reais conseguimos pegar) e equilibrar a **Precisão** (para evitar falsos alarmes em clientes legítimos).

## 2. Preparação dos Dados
- **Transformação:** Aplicação de log (`np.log1p`) na coluna `Amount` para suavizar a distribuição de valores.
- **Divisão Estratificada:** Uso do `stratify=y` no `train_test_split` para garantir que a proporção minúscula de fraudes fosse mantida idêntica nos dados de treino e de teste.
- **Padronização:** Normalização das variáveis com `StandardScaler`.

## 3. Modelagem e Resultados
- **Modelo Utilizado:** Regressão Logística com `class_weight='balanced'`.
- **Desempenho Inicial (Limiar 0.5):** 
  - Recall da Fraude: **88%** (pegou a grande maioria das fraudes).
  - Precisão: **6%** (gerou muitos falsos alarmes).
- **Ajuste de Limiar (Threshold para 0.7):**
  - Ao exigir 70% de certeza, a precisão dobrou (subiu para **12%**, cortando os falsos alarmes pela metade) enquanto o recall se manteve alto (**85%**).

## 4. Explicabilidade com SHAP
Utilizamos a biblioteca SHAP para gerar um gráfico de importância de atributos (*Summary Plot*), permitindo entender quais variáveis mais pesaram nas previsões do modelo e garantindo interpretabilidade para as decisões de segurança.

## 5. Como Executar
1. Clone o repositório.
2. Abra o arquivo de notebook correspondente no Google Colab.
3. Execute todas as células em ordem.
