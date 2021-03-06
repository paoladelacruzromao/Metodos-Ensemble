# Métodos-Ensemble
Machine Learning Metodos Ensemble

## 1.- Bagging Classifier
Bagging é usado para construção de múltiplos modelos (normalmente do mesmo tipo) a partir de diferentes subsets no dataset de treino.
Um classificador Bagging é um meta-estimador ensemble que faz o fit de classificadores base, cada um em subconjuntos aleatórios do conjunto de dados original e, em seguida, agrega suas previsões individuais (por votação ou por média) para formar uma previsão final.

Tal meta-estimador pode tipicamente ser usado como uma maneira de reduzir a variância de um estimador (por exemplo, uma árvore de decisão), introduzindo a randomização em seu procedimento de construção e fazendo um ensemble (conjunto) a partir dele.

A Bagging classifier is an ensemble meta-estimator that fits base classifiers each on random subsets of the original dataset and then aggregate their individual predictions (either by voting or by averaging) to form a final prediction. Such a meta-estimator can typically be used as a way to reduce the variance of a black-box estimator (e.g., a decision tree), by introducing randomization into its construction procedure and then making an ensemble out of it.

This algorithm encompasses several works from the literature. When random subsets of the dataset are drawn as random subsets of the samples, then this algorithm is known as Pasting [1]. If samples are drawn with replacement, then the method is known as Bagging [2]. When random subsets of the dataset are drawn as random subsets of the features, then the method is known as Random Subspaces [3]. Finally, when base estimators are built on subsets of both samples and features, then the method is known as Random Patches
![image](https://user-images.githubusercontent.com/87387315/165098797-255cd282-c3e3-40fb-8db0-dacb678fdddb.png)

  a.-Os conjuntos de dados de treinamento consistem em amostras de dados representadas usando cores diferentes.
  
  b.-Amostras aleatórias são retiradas com reposição. Isso significa essencialmente que pode haver dados duplicados em cada uma das amostras.
  
  c.-Cada amostra é usada para treinar diferentes estimadores (regressores) / classificadores representados usando classificador 1, classificador 2, …, classificador n
  
  d.-É criado um classificador/regressor ensemble que pega as previsões de diferentes classificadores/regressores e faz a previsão final com base na votação ou na média, respectivamente.
  
  e.-O desempenho do classificador ensemble é testado usando o conjunto de dados de treinamento.

### Parameters : 
base_estimator : default = None
O estimador de base para treinar em subconjuntos aleatórios do conjunto de dados. Em caso de não ser especificado None, o estimador base é o DecisionTreeClassifier.

The base estimator to fit on random subsets of the dataset. If None, then the base estimator is a DecisionTreeClassifier.

n_estimators: int, default=10
Número de estimadores base no emsemble o default é 10.
The number of base estimators in the ensemble.

max_samples: int or float, default=1.0
O número de amostras a serem extraídas de X para treinar cada estimador de base
The number of samples to draw from X to train each base estimator

Outros parámetros:

http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.BaggingClassifier.html

### Beneficios do Bagging? / Bagging classifier Help
Ajuda a **reduzir a variância de estimadores individuais**, introduzindo a randomização no estágio de treinamento de cada um dos estimadores e fazendo um conjunto de todos os estimadores.

Helps reducing the variance of individual estimators by introducing randomization into the training stage of each of the estimators and making an ensemble out of all the estimators.

### Quando usar Bagging Classifier? / When to use Bagging Classifier?
Bagging Classifier é usado em modelos onde existe uma alta variância e baixo vies, conseguindo um alto beneficio em modelos de árvores de decisão, modelos lineares de baixa variância podem não se beneficiar muito com o uso de esta técnica. 

O método ensemble pode ser criado usando vários estimadores que podem ser treinados usando diferentes técnicas de amostragem:
 **pasting:** amostras extraídas sem amostragem.
 
 **bagging or bootstrap aggregation:** amostras extraídas com substituição.
 
 **random subspaces:** características aleatórias são extraídas.
 
 **random patches:** amostras e recursos aleatórios são desenhados.

Bagging classifier helps reduce the variance of unstable classifiers (having high variance). The unstable classifiers include classifiers trained using algorithms such as decision tree which is found to have high variance and low bias.

The ensemble classifier which is created using multiple estimators which can be trained using different sampling techniques including :
**pasting:** (samples drawn without sampling), 

**bagging or bootstrap aggregation:** (samples drawn with replacement),

**random subspaces:** (random features are drawn), 

**random patches:** (random samples & features are drawn).

Variancia e vies : https://vitalflux.com/bias-variance-concepts-interview-questions/

![image](https://user-images.githubusercontent.com/87387315/165101994-92be56ac-d761-422f-8375-615cb3b8e982.png)

### Example

**BaggingClassifier.ipynb**


## 2.- Extremely Randomized Trees (ExtraTrees)

Essa classe implementa um meta estimador que ajusta várias árvores de decisão aleatórias (também conhecidas como árvores extras) em várias subamostras do conjunto de dados e usa a média para melhorar a precisão preditiva e controlar o 
"Over-fitting"

This class implements a meta estimator that fits a number of randomized decision trees (a.k.a. extra-trees) on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control over-fitting.


### Parameters : 
n_estimators: int, default=100
Número de árvores da floresta
The number of trees in the forest.

criterion: {“gini”, “entropy”}, default=”gini”
A função para medir a qualidade de uma divisão. Os critérios suportados são “gini” para a impureza Gini e “entropia” para o ganho de informação.
The function to measure the quality of a split. Supported criteria are “gini” for the Gini impurity and “entropy” for the information gain.

Outros parametros:
https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.ExtraTreesClassifier.html

### Beneficios do Extratress? / Extremely Randomized Trees Help
Seu principal diferencial está no fato deste processo ser extremamente aleatório, contribuindo assim para modelos mais generalizáveis.
Ele escolhe as variáveis e amostras randomicamente, e também o threshold para spilt dos dados de maneira randômica.

Its main differential is the fact that this process is extremely random, not assimilable to more generalizable models.
It chooses the variables and samples randomly, as well as the threshold for spilt data randomly.

### ExtraTress vs RandomForest
**Arvore de Decisão**

Em primeiro lugar, vamos lembrar o que Random Forest tem de diferente das Árvores de Decisão. Quando vamos construir uma árvore de decisão, o algoritmo tenta encontrar a melhor variável para começar a construção do nó; depois ele escolhe o melhor ponto para fazer o split dos dados, o melhor ponto para separar os dados: uma parte para um lado, e outra para outro. E a partir disso, vai construindo a árvore, sempre procurando a melhor condição possível, o melhor threshold, baseado no ganho de informação ou no índice Gini.

First, let's remember what makes Random Forest different from Decision Trees. When we are going to build a decision tree, the algorithm tries to find the best variable to start building the node; then he chooses the best point to split the data, the best point to separate the data: one part for one side, the other for the other. And from that, it builds the tree, always looking for the best possible condition, the best threshold, based on the information gain or the Gini index.

**Random Forest**

No algoritmo Random Forest algumas amostras dos dados de treino(linhas do dataset) serão selecionadas de maneira aleatória, sendo que as árvores criadas pelo algoritmo não conterão a totalidade dos dados utilizados na construção do modelo. Para definir a estrutura de cada árvore teremos a seleção aleatória de algumas variáveis, para que – dentre as selecionadas – aconteça a escolha daquela que estará no primeiro nó. Assim temos duas etapas importantes do processo acontecendo de maneira aleatória, tanto a seleção de variáveis quanto a seleção de amostras.

n the Random Forest algorithm, some training data samples (dataset lines) will be randomly selected, and the trees created by the algorithm will not contain all the data used in the construction of the model. To define the structure of each tree, we will have a random selection of some variables, so that – among the selected ones – the choice of the one that will be in the first node happens. Thus, we have two important stages of the process happening randomly, both the selection of variables and the selection of samples.

***ExtraTrees**

Já com o ExtraTrees, esse processo se torna ainda mais aleatório, justificando o termo “extremamente” empregado em seu nome. As etapas mencionadas acima continuam existindo, e mais um fator de aleatoriedade é adicionado. Após a seleção aleatória das variáveis candidatas para o nó inicial, os dados existentes em cada uma destas variáveis serão separados (split dos dados) também de maneira aleatória. Após estas escolhas os cálculos necessários para otimização da árvore podem começar.

With ExtraTrees, this process becomes even more random, justifying the term “extremely” used in its name. The steps mentioned above continue to exist, and one more randomness factor is added. After the random selection of candidate variables for the initial node, the existing data in each of these variables will be separated (data split) also randomly. After these choices, the necessary calculations for tree optimization can begin.

![image](https://user-images.githubusercontent.com/87387315/165314855-77cabde7-95ee-4d5f-823d-0cb18b6435fd.png)

### Cuidados com o ExtraTrees

É evidente que um processo mais aleatório também tem os seus prós e contras, seu lado positivo e negativo. A parte positiva é que cria um modelo menos enviesado, conforme abordamos anteriormente; e a parte negativa é que, se por acaso, existirem muitas variáveis que não estão ajudando no nosso problema e, por consequência, não deveriam estar ali, o algoritmo poderá acabar escolhendo essas variáveis para começar os nós, dando a elas um destaque grande e indevido. Então, nesse cenário, onde se tem muitas variáveis ruins que poderiam ter sido eliminadas, o ExtraTrees pode ter uma performance pior que a do Random Forest.

No caso do ExtraTrees, então, o pré-processamento ganha ainda mais importância. Onde, eventualmente, se faça uma seleção das variáveis, eliminando as indesejadas, que só acrescentam ruídos e não ajudam a classificar os dados.

**ExtraTrees care**

It is evident that a more random process also has its pros and cons, its positive and negative sides. The positive part is that it creates a less biased model, as we discussed earlier; and the negative part is that, if by chance, there are many variables that are not helping our problem and, therefore, shouldn't be there, the algorithm may end up choosing these variables to start the nodes, giving them a big highlight and improper. So, in this scenario, where you have a lot of bad variables that could have been eliminated, ExtraTrees may have a worse performance than Random Forest.

In the case of ExtraTrees, then, pre-processing becomes even more important. Where, eventually, a selection of variables is made, eliminating unwanted ones, which only add noise and do not help classify the data.

![image](https://user-images.githubusercontent.com/87387315/165319217-676398d7-7976-4ce9-b666-f0315b987f03.png)

## 2.- Adaboost

Um classificador AdaBoost é um meta-estimador que começa ajustando um classificador no conjunto de dados original e depois ajusta cópias adicionais do classificador no mesmo conjunto de dados, mas onde os pesos das instâncias classificadas incorretamente são ajustados para que os classificadores subsequentes se concentrem mais em casos difíceis.

An AdaBoost [1] classifier is a meta-estimator that begins by fitting a classifier on the original dataset and then fits additional copies of the classifier on the same dataset but where the weights of incorrectly classified instances are adjusted such that subsequent classifiers focus more on difficult cases.

### Parameters : 
base_estimator : default = None

O estimador de base para treinar em subconjuntos aleatórios do conjunto de dados. Em caso de não ser especificado None, o estimador base é o DecisionTreeClassifier.

The base estimator to fit on random subsets of the dataset. If None, then the base estimator is a DecisionTreeClassifier.

n_estimators: int, default=50

O número máximo de estimadores em que o reforço é encerrado. Em caso de ajuste perfeito, o processo de aprendizagem é interrompido precocemente.

The maximum number of estimators at which boosting is terminated. In case of perfect fit, the learning procedure is stopped early.

Learning Rate : float, default=1.0

Peso aplicado a cada classificador em cada iteração de reforço. Uma taxa de aprendizado mais alta aumenta a contribuição de cada classificador. Há um trade-off entre os parâmetros learning_rate e n_estimators.

Weight applied to each classifier at each boosting iteration. A higher learning rate increases the contribution of each classifier. There is a trade-off between the learning_rate and n_estimators parameters

## 3.- Gradient Boosting 

Gradient Boosting ou Gradient Boostted Regression Trees (GBRT) é uma técnica de aprendizagem estatística não-paramétrica usada para problemas de classificação e regressão.
Para um melhor entendimento podemos usar o seguinte material:http://deeplearningbook.com.br/aprendizado-com-a-descida-do-gradiente/

Gradient Boosting = Gradient Descent + Boosting.

Tres etapas são realizadas na construção do modelo:

1- Gera um regressor: O gradient boostinfg sempre vai criar um regressor independente do modelo ser classificador ou uma regressão

2- Computa o erro residual: Os residuos são os erros do modelo valor observado - valor previsto

3- Aprende a prever o resíduo: Aprendendo a prever o residuo o modelo vai ter um nivel de presição maior. Pois vai encontrar a melhor função alvo, reducindo os residuos.

### Como funciona o Gradient Boosting:

1 - Realiza um conjunto de previsões (y)

2- Calcula o erro das previsões (j)

3- Tenta ajustar y reduzindo o erro (através de alpha (taxa de aprendizado))

4- Para cada estimador base, é estimado o gradiente da função de perda

5- Estimadores subsequentes estimam o erro residual dos estimadores anteriores, lembra no bagging estimamos a media no boosting pegamos a saida do estimador base aprendiendo dos erros passados

6- Aplica o Gradient Descent para reduzir j

7- Soma os resultados dos estimadores, dando peso a cada passo de acordo com o valor de alfa (alfa vai ser um hiperparametro)


7- Soma os resultados dos estimadores, dando peso a cada passo de acordo com o valor de alfa

http://scikit-learn.org/stable/modules/ensemble.html#gradient-boosting


### a.- Gradient Boosting Classifier:(additive model ina fordward stage wish fashion)

Gradient Boosting for classification.

GB builds an additive model in a forward stage-wise fashion; it allows for the optimization of arbitrary differentiable loss functions. In each stage n_classes_ regression trees are fit on the negative gradient of the binomial or multinomial deviance loss function. Binary classification is a special case where only a single regression tree is induced.

http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingClassifier.html

```sh
# Imports
from sklearn.datasets import make_hastie_10_2
from sklearn.ensemble import GradientBoostingClassifier

# Define dados para x e y
X, y = make_hastie_10_2(random_state = 0)
X_train, X_test = X[:2000], X[2000:]
y_train, y_test = y[:2000], y[2000:]

# Cria o classificador
clf = GradientBoostingClassifier(n_estimators = 100, learning_rate = 1.0, random_state = 0)

# Treina o classificador
clf.fit(X_train, y_train)

# Calcula a acurácia (score)
clf.score(X_test, y_test)  
```

### b.-Gradient Boosting Regressor

Gradient Boosting for regression.

GB builds an additive model in a forward stage-wise fashion; it allows for the optimization of arbitrary differentiable loss functions. In each stage a regression tree is fit on the negative gradient of the given loss function.

http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html

```sh
# Imports
import numpy as np
from sklearn.metrics import mean_squared_error
from sklearn.datasets import make_friedman1
from sklearn.ensemble import GradientBoostingRegressor

# Define dados para x e y
X, y = make_friedman1(n_samples = 1200, random_state = 0, noise = 1.0)
X_train, X_test = X[:200], X[200:]
y_train, y_test = y[:200], y[200:]

# Cria o regressor
est = GradientBoostingRegressor(n_estimators = 100, learning_rate = 0.1, max_depth = 1, random_state = 0, loss = 'ls')

# Treina o regressor
est.fit(X_train, y_train)

# Calcula o erro médio ao quadrado
mean_squared_error(y_test, est.predict(X_test))    

```
### Binomial emsembled Question

![image](https://user-images.githubusercontent.com/87387315/167133657-50e7f414-ec7c-4e8c-8360-cf32218a2c7e.png)
