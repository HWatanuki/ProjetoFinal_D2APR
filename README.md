# ProjetoFinal_D2APR
Projeto Final da disciplina D2APR - Aprendizagem de máquina do curso de Especialização em Ciência de Dados do IFSP Campinas.

# Aluno: 
- Hugo Martinelli Watanuki

# Credit Risk Analysis

![image](https://github.com/HWatanuki/ProjetoFinal_D2APR/assets/50485300/8d289689-d71a-46b9-9817-1c19c6d03124)

The objective of this project is to identify, through statistical techniques and learning machine, a prediction model based on attributes of individuals that allows measuring the risk of a credit application. The main questions to be answered are:

1) What variables can be used to establish credit risk at the moment of a loan request?

2) What are the characteristics of the statistical model capable of predicting credit risk?

# a) The dataset

The dataset being leveraged in this notebook contains Lending Club historical data from 2007 to 2020 and is available from kaggle: https://www.kaggle.com/datasets/ethon0426/lending-club-20072020q1/

LendingClub is a financial services company headquartered in San Francisco, California. It was the first peer-to-peer lender to register its offerings as securities with the Securities and Exchange Commission (SEC), and to offer loan trading on a secondary market. At its height, LendingClub was the world's largest peer-to-peer lending platform. The company reported that $15.98 billion in loans had been originated through its platform up to December 31, 2015.

LendingClub enabled borrowers to create unsecured personal loans between $1,000 and $40,000. The standard loan period was three years. Investors were able to search and browse the loan listings on LendingClub website and select loans that they wanted to invest in based on the information supplied about the borrower, amount of loan, loan grade, and loan purpose. Investors made money from the interest on these loans. LendingClub made money by charging borrowers an origination fee and investors a service fee.

![image](https://github.com/HWatanuki/ProjetoFinal_D2APR/assets/50485300/af8cf438-5ace-4b00-86bd-2082ba8e6c01)

The dataset contains almost 3 Million records where each instance represents a loan request that was accepted by Lending Club. The loans could then be honored by the requestors (non-default) or not (default).

![image](https://github.com/HWatanuki/ProjetoFinal_D2APR/assets/50485300/e8d89b5f-a349-40ed-b298-2fe1487ed315)

Each loan request contains 141 atributes and the data dictionary for the dataset can be accessed here: https://github.com/HWatanuki/ProjetoFinal_D2APR/blob/main/LCDataDictionary.xlsx 

![image](https://github.com/HWatanuki/ProjetoFinal_D2APR/assets/50485300/8471fe7d-124c-4925-9bdc-12035251d711)

Due to its considreable size (1.7GB) the dataset cannot be loaded using the regular free google colab platform and therefore it is suggested that this notebook is executed in a computer with sufficient memory (16GB at a minimum).

# b) Exploratory data analysis

![image](https://github.com/HWatanuki/ProjetoFinal_D2APR/assets/50485300/571ed8b6-bb06-4119-af49-1032f2f19474)

Although not an usual approach, in this study the size of the raw dataset made impractical to conduct an exploratory data analysis without first performing some cleanup on information that is not useful for the end goal of the project. 

Therefore, a parallel approach was adopted during the exploratory data analysis: whenever a certain record or attribute was identified as not important for determining the risk of the loan request, the record or attribute was removed from the raw dataset in order to enable the subquesent analysis in the exploratory data analysis pipeline.

After exploring the dataset, the following findings can be highlighted along with their respective remediation:

* There are features that should not be known during the moment of the loan request (such as payments received so far) that need to be removed from the dataset before training the model.

* The dataset has a 4:1 ratio of loan request that have been successfully paid vs. not paid, i.e., the dataset is extremely unbalanced. Undersampling can be a potential approach to address this unbalance.

* There are no duplicated records in the dataset.

* Several features have a severe rate of missing values that need to be treated accordingly. Literature suggests that a 10% rate of missing values can bias the training while values above 40% can be impractical.

* There are 57 numeric features and 16 non numeric features to be used for training the model.

* The order of magnitude of the numeric features varies considerably. Feature scaling is recommended depending of the machine learning algorithm selected.

* Box plot analysis of the numeric features has revealed that several features contain outliers but the will be kept as they represent real values and not noise.

* Few non numeric features such as interest rate are percentage values that need to be cleaned (i.e., remove the percentage % character).

* Most of the non numeric features have a categorical nature and will need to be encoded for the machine learning training.

# c) Cleaning and preprocessing the dataset

The exploratory data analysis has provided important insights for the cleaning and preprocessing of the dataset. 

In this step the dataset was sliced and reduced only to the attributes that help predict the risk of loan request. This should contribute to a more efficient training of the models:

* The features with percentage values were cleaned and correctly typed as numeric features so their values can be considered quantitatively in the training.

* The class imbalance was addressed via undersampling and since the dataset had a very large number of records, the missing value issue was addressed via undersampling as well by only selecting records with non null values.

* Training and test samples were extracted before enconding and feature scalling to avoid data leakage from the training into the test sample. A Stratified sampling approach was used to make sure the class imbalance was maintained in the training and test samples.

* The categorical features were enconded and converted into numerical values so they can be considered for the subsequent training of the machine learning model.

* A robust scalling approach was used for feature scalling of the numeric fatures to ensure that they are robust to the outliers indentified during the exploratory data analysis.

Taken together, all the actions performed during the preprocessing and cleaning step should contribute to a more efficient and precise training of the machine learning model.

![image](https://github.com/HWatanuki/ProjetoFinal_D2APR/assets/50485300/7743df5e-24a0-4f94-b618-59c8dbbe5285)

# d) Training and validation of the model

![image](https://github.com/HWatanuki/ProjetoFinal_D2APR/assets/50485300/9f74c8fd-1139-4db5-ab22-e312bbfaebf1)

Since the objective of the machine learning model is to predict one of the two classes that correspond whether the individual requesting a loan will fully paid it or not (i.e., a binominal classification), the following machine learning algorithms were selected the training of the model: KNN, SVM, Logistic Regression and Decision Tree.

For cross validation, each algorithm was subjected to five (5) training sets randomly splitted with no stratification (i.e. five folds). Therefore each algorithm was used for training and evaluation five times, picking a different fold (validation set) for evaluation every time and training on the other 4 folds (train-dev set). The result is an array containing the 5 evaluation scores.

Therefore, a function was created to print the cross validation results, i.e., the accuracy scores, their mean and standard deviation. The mean and standard deviation values were used to compare the four algorithms.

# e) Results and discussion

The first model using KNN has shown an mean accuracy value of 74.8% which was the lowest among the four models evaluated. This could be due to the fact that in high dimensional settings as the one being investigated, the accuracy of KNN are affected by nuisance features. Therefore, this algorithm was not considered for further analysis.

The second model trained using SVM has demonstrated a better mean accuracy value of 83.3%, marginally superior to the mean accuracy of the Decision Tree of 82.3%. However, the Decision Tree model has emerged as a superior alternative given that it not only deals better with categorical data (almost 30% of the features are categorical), but it also converged much faster than SVM, thus making the Decision Tree model more efficient from a computing resources perspective.

Lastly, the model trained using Logistic Regression has shown the higher mean accuracy value (88.5%), suggesting that this algorithm could be the best one among the four algorithms being tested. However, since all the model are still somewhat underfitted, a fine-tuning step was suggested in an attempt to improve the accuracy of the Logistic Regression model by leveraging only the most important features according to the Decision Tree model.

![image](https://github.com/HWatanuki/ProjetoFinal_D2APR/assets/50485300/a4c99054-ee0a-4103-bd93-e89c71320f0e)

This notebook has suggested that the five main variables that can be used to determine credit risk at the moment of a loan request are the following, in order of importance:

1) last_fico_range_high: The upper boundary range the borrower’s last FICO pulled belongs to.

2) last_fico_range_low: The lower boundary range the borrower’s last FICO pulled belongs to.

3) installment: The monthly payment owed by the borrower if the loan originates

4) dti: A ratio calculated using the borrower’s total monthly debt payments on the total debt obligations, excluding mortgage and the requested LC loan, divided by the borrower’s self-reported monthly income.

5) emp_title: The job title supplied by the Borrower when applying for the loan.

