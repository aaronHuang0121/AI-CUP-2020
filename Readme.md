AI CUP 2020 - 醫病資料去識別化
===

Members
---
* 黃彥穎 Aaron Huang 
* 唐岳 Ray

Competition introduction
---

#### Medical information decision analysis and dialogue data construction system

* ##### Health Insurance Portability and Accountability Act
    According to the HIPAA in the clinical medical text records, the contents of the patient’s private information must be erased or changed.
* ##### Medical-patient dialogue 
    In the medical-patient dialogue materials, there are many private contents of the people seeking medical treatment.
* ##### Identify private contents
    The major goal of this competition is to identify and extract content involving private information from the conversation between doctors and patient.


Named Entity Recognition
---

* ##### Named Entity
    Entities with specific meaning in the text. Such as persons, locations, organizations, product
* ##### NER task
    Extract entities from unstructured input text.
    
![NER task](https://i.imgur.com/UKfMu07.png)


Data preprocessing
---
![data preprocessing pipeline](https://i.imgur.com/VD4nkVN.png)

1. At first, we input the training data and split all dialogues
1. After getting multiple dialogues, we need to split each dialogue into sentence to prevent from exceeding the limitation of the length.
1. And then we need to split sentence to words and mark training data provides named entities.


BERT (Bidirectional Encoder Representations form Transformers) 
---
* The architecture of BERT is Transformer’s Encoder.
* Encoder can convert the words we input into a vector, and then the Decoder can read the information of this vector and generate the output we want.
* BERT uses “character” instead of “word” as the unit when inputting Chinese sentences.
* The reason is that when processing the Embedding of the input sentence.
* We use One-Hot Encoding to convert the input sequence, and it is difficult to list Chinese words exhaustively.

![BERT](https://i.imgur.com/dcWSSVX.png)
> Source: https://www.youtube.com/watch?v=UYPa347-DdE&ab_channel=Hung-yiLee

### Training BERT
![Training BERT](https://i.imgur.com/Oz4pSWV.png)
* It divides Bert training into two major steps: Pre-training and Fine-Tuning. 
* In the pre-training phase, Google uses an extensive amount of text data to train the model in an unsupervised learning manner. 
* In the Fine-Tuning stage, it is for different tasks to train and fine-tune the model with labeled data.
>Source: https://arxiv.org/pdf/1810.04805.pdf

### Learning
![Learning](https://i.imgur.com/NOSzN9o.png)
Then, throw the question and the article into BERT together like two sentences and let the model learn two vectors.First, let the orange vector and the Embedding of each word in the article perform the inner product operation.After Softmax, it can get the probability distribution.The highest is the first word that predicts the answer.
>Source: https://www.youtube.com/watch?v=UYPa347-DdE&ab_channel=Hung-yiLee

### Validation
![Validation](https://i.imgur.com/SGYvmOR.png)
Then, let the blue vector and the Embedding of each word in the article perform the inner product operation.After Softmax, the highest is the last word that predicts the answer.The result from outputting the first word to the last word in the article is the conclusive answer.If the last word comes before the first, it means that this article has no answer.
>Source: https://www.youtube.com/watch?v=UYPa347-DdE&ab_channel=Hung-yiLee

Result
---
#### There are 531 groups, which are 811 people in total participating in this competition and our score is in the top 15.849 percent .
![Result](https://i.imgur.com/RiuJxLc.png)
#### In this competition Best score is 0.8305599, Lowest score is 0, Our score is 0.7033699
![](https://i.imgur.com/8sE3nd2.png)

Future work
---
* Add other Deep Learning layers(ex.CNN,CRF,RNN)
* Reorganize the preprocessing data into a problem and require all targets to retrain
* Re-sentence the preprocessing data


## References

1. https://github.com/huggingface/notebooks/blob/master/examples/token_classification.ipynb
1. 進擊的 BERT：NLP 界的巨人之力與遷移學習 - LeeMeng
1. Transformers API Doc
1. ELMO, BERT, GPT - Hung-yi Lee
1. Named Entity Recognition 命名實體識別


###### tags: `BERT` `Named Entity Recognition`
