<p align="center">
    <a href="https://github.com/luowensheng"><img src="https://i.ibb.co/0FmPqfm/logo1a.png"></a>
</p>

<h1 align="center">Seq2Seq Neural Network for Grammatical Error Correction
</h1>
<p align="center">
    <a href="https://jupyter.org/"><img src="https://img.shields.io/badge/Made with-Jupyter Notebook-Orange.svg"></a>
    <a href="https://github.com/luowensheng/NLP_Seq2seq-Neural-Network-for-grammatical-error-correction/pulse"><img src="https://img.shields.io/badge/Maintained%3F-yes-green.svg"></a>
    <a href="https://github.com/luowensheng"><img src="https://badges.frapsoft.com/os/v2/open-source.svg?v=103"></a>
</p>

<p align="center">
  <a href="#Introduction">Introduction</a> •
  <a href="#Goal">Goal</a> •
  <a href="#Results">Results</a> •
  <a href="#Questions">Questions</a>
</p>

___

<br>

# Introduction
[(Back to top :arrow_up_small:)](#Seq2Seq-Neural-Network-for-Grammatical-Error-Correction)

## **Seq2Seq Examples**
* [Character-based NMT.](https://keras.io/examples/lstm_seq2seq/)
* [Keras pre-trained word embedding.](https://blog.keras.io/using-pre-trained-word-embeddings-in-a-keras-model.html)

## **Neural Network Structure**
<p align="center">
<img src="https://i.ibb.co/VpQqtCR/1.jpg" alt="1" border="0"></a>
</p>

## **Keras Layers**
<p align="center">
<b>NMT model summary:</b>
<br>
<img src="https://i.ibb.co/g6db932/2.jpg" alt="2" border="0"></a>
<img src="https://i.ibb.co/x1dB07f/3.jpg" alt="3" border="0"></a>
</p>

## **Dataset**
| Incorrect | Correct |
| :-------: | :-----: |
| I'm fond to reading and dressing up myself. | I'm fond of reading and dressing up myself|

Full dataset [here](https://drive.google.com/drive/folders/1uI0G6xtK0R-lzoPfXXSj3IVVy6vXu8K9).

## **Data Processing**
| Word | Index |
| :-------: | :-----: |
| I | 85|
| learn | 10 |
| a | 32 |
| lot | 25 |
| with | 76 |
| it | 23 |
| . | 4 |

**1. Raw Data**
```
'I learn a lot with it.'
```
**2. Tokenize Data**
```
['I', 'learn', 'a', 'lot', 'with', 'it', '.']
```
**3. Build Vocab Dictionary**
```
85, 10, 32, 25, 76, 23, 4
```
**4. Pad Data**

## **Data Padding**
```<Start>``` is the *beginning* of the sentence.

```<End>``` is the *end* of the sentence.

```<Pad>``` keeps the *sentence length* consistent.

| Word | Index |
| :-------: | :-----: |
| ```<Pad>``` | 0 |
| ```<Start>``` | 1 |
| ```<End>``` | 2 |

### Encoder sentence (input):
```[10, 17, 23, 4]``` → ```[10, 17, 23, 4, 2, 0, 0, 0]```
### Encoder sentence (input):
```[5, 18, 38, 40, 44, 4]``` → ```[1, 5, 18, 38, 40, 44, 4, 0]```

## **Embedding Layer**
```
Embedding(input_dim, output_dim, weights=
[embedding_matrix], trainable=[True | False])
```
* ```input_dim```: vocabulary size.
* ```output_dim```: output size, dim of word vector.
* ```weights```: pre-trained weights.
* ```trainable```: if *false*, freeze the layer.

## **LSTM Layer**
```
LSTM(units, return_sequences=[True | False],
return_state=[True | False])
```

* ```units```：hidden dimension (output size).
* ```return_sequences```：if *true*，return the output of all words; *otherwise*, the output of the last word is returned.
* ```return_state```：whether to return the last cell state.

## **Dense Layer**
```
Dense(units, activation=)
    units：num of decoder tokens
    activation：softmax
```

## **Dirty Data**
Example: 
>"To discuss ***about*** private problems..."

| False Positive | Correct |
| :-------: | :-----: |
| discuss about | discuss |
| explain about | explain |
| mention about | mention |
| desribe about | describe |

## **Effect of Cleaning Data**
* Clean every occurrence of false-positive data

    ```
    {‘discuss about’, ‘explain about’, ‘mention about’, ‘describe about’}
    ```
* Train a new model
* Analyze the result of the two models

# Goal
[(Back to top :arrow_up_small:)](#Seq2Seq-Neural-Network-for-Grammatical-Error-Correction)

* To use ```Seq2Seq``` Neural Network architecture in machine
translation to perform grammatical error correction.

* Word embedding: pre-trained word embedding
* To Analyze the effect of cleaning data

# Results
[(Back to top :arrow_up_small:)](#Seq2Seq-Neural-Network-for-Grammatical-Error-Correction)

## **Method 1**
<img src="https://i.ibb.co/52QZvYw/4.jpg" alt="4" border="0"></a>

## **Method 2**
<img src="https://i.ibb.co/kB79Rps/5.jpg" alt="5" border="0"></a>

## **Method 3**
<img src="https://i.ibb.co/ZfwQGh0/6.jpg" alt="6" border="0"></a>

## **Method 4**

Model 1:
<img src="https://i.ibb.co/8xh8qWK/7.jpg" alt="7" border="0"></a>

Model 2:
<img src="https://i.ibb.co/zF0PQ60/8.jpg" alt="8" border="0"></a>

## **Method 5**
<img src="https://i.ibb.co/qdmjRcR/9.jpg" alt="9" border="0"></a>

### **Remarks:**
When training starts, the validation loss gets lower and lower but after a certain number of epochs we see that the validation loss starts to increase while the training loss continues to increase. This result suggests that there may be a possibility of overfitting during training. This happens where a bias present in the model and it causes the weights to adjust themselves in a way to better predict the training set while not actually improving its chances of predicting sentences that are not included in the training set.

Results using only 10721 sentences and a small percentage of the validation set:
<img src="https://i.ibb.co/zN5RqC3/10.jpg" alt="10" border="0"></a>

Some of the prediction results:
<img src="https://i.ibb.co/18Rj5xj/11.jpg" alt="11" border="0"></a>

# Comparisons
[(Back to top :arrow_up_small:)](#Seq2Seq-Neural-Network-for-Grammatical-Error-Correction)

The comparison is done using the second method.

Training method:

<img src="https://i.ibb.co/xCvHmt5/12.jpg" alt="12" border="0"></a>

Clean data results:

<img src="https://i.ibb.co/yVnWbp4/13.jpg" alt="13" border="0"></a>

Dirty data results:

<img src="https://i.ibb.co/xDp4kq6/14.jpg" alt="14" border="0"></a>

Percentage of target sentences cleaned : ```0.00022037905196938736```

Number of target sentences cleaned: ```33```

Clean data results of ```20 epochs```

<img src="https://i.ibb.co/7nyCmQh/15.jpg" alt="15" border="0"></a>

# Questions
Submit your questions and bug reports [here](https://github.com/luowensheng/Natural-Language-Processing-Grammatical-Error-Correction-/issues).


<br>
<p align="center">  
  <sub>© luowensheng.
  </a>
