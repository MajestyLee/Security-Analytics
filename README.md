# Project

Use different ML methods to analyze and compare these two methods

## Intro to NSL Kdd Dataset

NSL-KDD is a data set suggested to solve some of the inherent problems of the KDD'99 data set which are mentioned in. Although, this new version of the KDD data set still suffers from some of the problems discussed by McHugh and may not be a perfect representative of existing real networks, because of the lack of public data sets for network-based IDSs, we believe it still can be applied as an effective benchmark data set to help researchers compare different intrusion detection methods.(https://www.unb.ca/cic/datasets/nsl.html)

Snapshoot of training data(`raw/KDDTest+.txt`):
```
0,tcp,http,SF,181,5450,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,8,8,0.00,0.00,0.00,0.00,1.00,0.00,0.00,9,9,1.00,0.00,0.11,0.00,0.00,0.00,0.00,0.00,normal,16
0,tcp,http,SF,239,486,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,8,8,0.00,0.00,0.00,0.00,1.00,0.00,0.00,19,19,1.00,0.00,0.05,0.00,0.00,0.00,0.00,0.00,normal,21
0,tcp,http,SF,235,1337,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,8,8,0.00,0.00,0.00,0.00,1.00,0.00,0.00,29,29,1.00,0.00,0.03,0.00,0.00,0.00,0.00,0.00,normal,21
0,tcp,http,SF,219,1337,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,6,6,0.00,0.00,0.00,0.00,1.00,0.00,0.00,39,39,1.00,0.00,0.03,0.00,0.00,0.00,0.00,0.00,normal,21
0,tcp,http,SF,217,2032,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,6,6,0.00,0.00,0.00,0.00,1.00,0.00,0.00,49,49,1.00,0.00,0.02,0.00,0.00,0.00,0.00,0.00,normal,21
0,tcp,http,SF,217,2032,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,6,6,0.00,0.00,0.00,0.00,1.00,0.00,0.00,59,59,1.00,0.00,0.02,0.00,0.00,0.00,0.00,0.00,normal,21
0,tcp,http,SF,212,1940,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,1,2,0.00,0.00,0.00,0.00,1.00,0.00,1.00,1,69,1.00,0.00,1.00,0.04,0.00,0.00,0.00,0.00,normal,14
0,tcp,http,SF,159,4087,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,5,5,0.00,0.00,0.00,0.00,1.00,0.00,0.00,11,79,1.00,0.00,0.09,0.04,0.00,0.00,0.00,0.00,normal,21
```

## Prerequisite

* Python 3.7
* [Scikit-learn tool](http://scikit-learn.org/stable/)
* Mongodb

## Usage


Fork first and then execute `Preprocessing.py` file to do:

1. To deal with the dataset better, the dataset is divided into four main attack categories.
2. store in the mongoDB for further process


### For Decision Tree

```
.
├── CART_Predictor.py
├── CART_Runner.py
├── CART_Trainer.py
├── CART_all.py
├── __init__.py
└── output
    ├── CART.pkl
    └── tree-vis.pdf
```

```
cd CART
python CART_Runner.py
```

**Output**:

1. Confusion matrix:

```
[[ 6027    51    10   153   127]
 [   44   699     4     0    62]
 [  355    24 41341     0     0]
 [    0     1     0     0     2]
 [ 1075     6     0    14     5]]
```

2. Performance report:

```
            precision    recall  f1-score   support

           0       0.80      0.95      0.87      6368
           1       0.90      0.86      0.88       809
           2       1.00      0.99      1.00     41720
           3       0.00      0.00      0.00         3
           4       0.03      0.00      0.01      1100

   micro avg       0.96      0.96      0.96     50000
   macro avg       0.54      0.56      0.55     50000
weighted avg       0.95      0.96      0.96     50000
```

* export to `CART/output/tree-vis.pdf`：

* the model is stored in `CART/output/CART.pkl`

### For MLP

```
.
├── MLP_Predictor.py
├── MLP_Predictor.pyc
├── MLP_Runner.py
├── MLP_Trainer.py
├── MLP_Trainer.pyc
├── __init__.py
└── output
    ├── MLP.pkl
    └── decision-tree.pkl
```

```
cd MLP
python MLP_Runner.py
```

**Output**:

1. Confusion matrix:

  ```
[[ 6327    35     6     0     0]
 [    3   801     5     0     0]
 [  368     2 41350     0     0]
 [    2     0     1     0     0]
 [ 1098     1     0     1     0]]
  ```
2. Performance report:
   ```
                precision    recall  f1-score   support

           0       0.81      0.99      0.89      6368
           1       0.95      0.99      0.97       809
           2       1.00      0.99      1.00     41720
           3       0.00      0.00      0.00         3
           4       0.00      0.00      0.00      1100

   micro avg       0.97      0.97      0.97     50000
   macro avg       0.55      0.59      0.57     50000
    weighted avg       0.95      0.97      0.96     50000
    ```


* the model is stored in `MLP/output/MLP.pkl`

## Structure

```
.
├── CART
│   ├── CART_Predictor.py
│   ├── CART_Predictor.pyc
│   ├── CART_Runner.py
│   ├── CART_Trainer.py
│   ├── CART_Trainer.pyc
│   ├── CART_all.py
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── CART_Predictor.cpython-37.pyc
│   │   └── CART_Trainer.cpython-37.pyc
│   └── output
│       ├── CART.pkl
│       ├── trained_text.txt
│       └── tree-vis.pdf
├── MLP
│   ├── MLP_Predictor.py
│   ├── MLP_Predictor.pyc
│   ├── MLP_Runner.py
│   ├── MLP_Trainer.py
│   ├── MLP_Trainer.pyc
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── MLP_Predictor.cpython-37.pyc
│   │   └── MLP_Trainer.cpython-37.pyc
│   └── output
│       └── MLP.pkl
├── Mongo_Con.py
├── Mongo_Con.pyc
├── Preprocessing.py
├── Preprocessing.pyc
├── Preprocessing_all.py
├── README.md
├── Variable.py
├── Variable.pyc
├── __init__.py
├── __init__.pyc
├── __pycache__
│   ├── Mongo_Con.cpython-37.pyc
│   └── Variable.cpython-37.pyc
├── data
│   ├── KDDTest+.txt
│   ├── nsl.kdd.data.txt
│   └── nsl.kdd.data_20_percent.txt
└── raw
    ├── KDDTest+.txt
    ├── KDDTrain+.txt
    └── KDDTrain+_20Percent.txt
```
