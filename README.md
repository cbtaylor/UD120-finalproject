# UD120-finalproject
The final project for the Udacity Machine Learning course.

I started with an exploratory data analysis to get a feeling for what the features were and the nature of the data.

### Data prep

### Cross Validation

### ML Models
I experimented with a few different machine learning models in using the sci-kit learn package. In each case I got the model running and then tried to tune the parameters to improve performance. Here is a quick summary of the performance I was able to achieve with each model.

| Naive Bayes   | 3-folds       | 4-folds       |
| ------------- | -------------:| -------------:|
| Precision     | 0.389         | 0.412         |
| Recall        | 0.389         | 0.389         |
| F1            | 0.389         | 0.400         |
| MCC           | 0.302         | 0.317         |

| SVM           | 3-folds       | 4-folds       |
| ------------- | -------------:| -------------:|
| Precision     | 0.250         | 0.240         |
| Recall        | 0.389         | 0.333         |
| F1            | 0.304         | 0.279        |
| MCC           | 0.186         | 0.159         |

| KNN           | 3-folds       | 4-folds       |
| ------------- | -------------:| -------------:|
| Precision     | 0.455         | 0.357         |
| Recall        | 0.278         | 0.278         |
| F1            | 0.345         | 0.313         |
| MCC           | 0.287         | 0.230         |

| DTree         | 3-folds       | 4-folds       |
| ------------- | -------------:| -------------:|
| Precision     | 0.138         | 0.385         |
| Recall        | 0.222         | 0.556         |
| F1            | 0.170         | 0.455         |
| MCC           | 0.020         | 0.368         |

| RndForrest    | 3-folds       | 4-folds       |
| ------------- | -------------:| -------------:|
| Precision     | 0.400         | 0.625         |
| Recall        | 0.111         | 0.278         |
| F1            | 0.174         | 0.385         |
| MCC           | 0.158         | 0.367         |

| AdaBoost      | 3-folds       | 4-folds       |
| ------------- | -------------:| -------------:|
| Precision     | 0.278         | 0.583         |
| Recall        | 0.278         | 0.389         |
| F1            | 0.278         | 0.467         |
| MCC           | 0.175         | 0.418         |
