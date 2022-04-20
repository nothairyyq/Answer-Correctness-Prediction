# Answer-Correctness-Prediction

Riiid Labs' [Track knowledge states of 1M+ students in the wild](https://www.kaggle.com/competitions/riiid-test-answer-prediction ), used the company's EdNet dataset to create a knowledge tracking algorithm: modeling student knowledge over time to accurately predict how students will perform in future interactions.

## Model
- SAINT+ （based on Transformer）
- used train.csv and questions dataset (I didn't use lectures, because lectures didn't improve validation score)

### Input Features

1. content_id

2. answered_correctly

3. part

4. prior_question_elapsed_time

5. prior_question_had_explanation

6. lag_time1 - convert time to seconds. if lag_time1 >= 300 than 300.

7. lag_time2 - convert time to minutes. if lag_time2 >= 1440 than 300 (one day).

8. lag_time3 - convert time to days. if lag_time3 >= 365 than 365 (one year).

I found lag time split to different time format boosting score around 0.003.

### Encoder input

- question embedding

- part embedding

- position embedding

- prior question had explanation embedding

### Decoder Input

- position embedding

- reponse embedding

- prior elapsed time embedding

- lag_time1 categorical embedding

-  lag_time2 categorical embedding

- lag_time3 categorical embedding

> Note that I have tried categorical and continuous embedding in prior elapsed time and lag time. The performance of categorical embedding is better than continuous embedding.

Model Architecture: Embedding Layer+ Transformer + Feed Forward Layer(with residual connection)
