# ProjetoFinal_D2APR
Projeto Final da disciplina D2APR - Aprendizagem de máquina do curso de Especialização em Ciência de Dados do IFSP Campinas.

# Aluno: 
- Hugo Martinelli Watanuki

# Credit Risk Analysis
The objective of this project is to identify, through statistical techniques and learning machine, a prediction model based on attributes of individuals that allows measuring the risk of a credit application. The main questions to be answered are:

What variables can be used to establish credit risk at the moment of a loan request?
What are the characteristics of the statistical model capable of predicting credit risk?

# a) The dataset

The dataset being leveraged in this notebook is available from kaggle: https://www.kaggle.com/datasets/ethon0426/lending-club-20072020q1/

The dataset contains almost 3 Million records where each instance represents a loan request between the years of 2007 and 2020. Each loan request contains 141 atributes and the data dictionary for te dataset can be accessed here:

Due to its considreable size (1.7GB) the dataset cannot be loaded using the regular free google colab platform and therefore it is suggested that this notebook is executed in a computer with sufficient memory (16GB at a minimum).

# b) Exploratory data analysis

Although not an usual approach, in this study the size of the raw dataset made impractical to conduct an exploratory data analysis without first performing some cleanup on information that is not useful for the end goal of the project. 

Therefore, a parallel approach was adopted during the exploratory data analysis: whenever a certain record or attribute was identified as not important for determining the risk of the loan request, the record or attribute was removed from the raw dataset in order to enable the subquesent analysis in the exploratory data analysis pipeline.

After exploring the dataset, the following findings can be highlighted along with their respective remediation:

* There are features that should not be known during the moment of the loan request (such as payments received so far) that need to be removed from the dataset before training the model.

* The dataset has a 4:1 ratio of loan request that have been successfully paid vs. not paid, i.e., the dataset is extremely unbalanced. Undersampling can be a potential approach to address this unbalance.

* There are no duplicated records in the dataset.

* Several features have a severe rate of missing values that need to be treated accordingly. Literature suggests that a 10% rate of missing values can bias the training while values above 40% can be impractical.

* There are 57 numeric features and 23 non numeric features to be used for training the model.

* The order of magnitude of the numeric features varies considerably. Feature scaling is recommended depending of the machine learning algorithm selected.

* Box plot analysis of the numeric features has revealed that several features contain outliers but the will be kept as they represent real values and not noise.

* Few non numeric features such as interest rate are percentage values that need to be cleaned (i.e., remove the percentage % character).

* Most of the non numeric features have a categorical nature and will need to be encoded for the machine learning training.

# c) Metadados
A base de dados utilizada no trabalho foi a da Comissão de Taxi e Limousine da cidade de Nova York (https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page). 

Essa base contém registros de viagens de passageiros de taxi da cidade de Nova York com os seguintes atributos:
- Local, data e hora da partida e chegada de cada viagem
- Distância, custo, tarifa e número de passageiros de cada viagem

Para as análises foram selecionados 2 datasets correspondendo às viagens realizadas entre os meses de Janeiro e Fevereiro de 2017, bem como um dataset contendo os códigos e descrições das áreas da cidade de Nova York.

Os datasets utilizados estão disponíveis aqui: 

A descrição mais detalhada dos dados está disponível aqui:

# d) Scripts de consulta dos dados
Os códigos utilizados para consultas SQL dos dados estão disponíveis aqui:

# e) Visualizações
As visualizações das consultas mais relevantes estão disponíveis aqui:


