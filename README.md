# UD120-finalproject
The final project for the Udacity Machine Learning course.

I started with an exploratory data analysis to get a feeling for what the features were and the nature of the data. The data loaded as a dictionary of dictionaries. For each key (the name of an individual, with two exceptions) there was a dictionary with the following keys:
poi, 
salary, 
exercised_stock_options, 
expenses, 
bonus, 
restricted_stock, 
deferral_payments, 
total_payments, 
other, 
director_fees, 
deferred_income, 
long_term_incentive, 
restricted_stock, 
restricted_stock_deferred, 
total_stock_value, 
loan_advances, 
to_messages, 
from_messages, 
shared_receipt_with_poi, 
from_this_person_to_poi, 
from_poi_to_this_person, 
and email_address. 
The first, 'poi', is the target or label and is a boolean. With the exception of 'email_address' all the others are integer values and all have missing values indicated by 'NaN'. Each feature is either related to compensation or to the numbers of e-mail messages sent or received.


### Data prep
For my own benefit I wanted to get some experience prepping the data for use with sci-kit learn. I didn't use, or even take a look at, the provided data prep function. I chose to put the data into a pandas dataframe. This was quite a learning process as I slowly all the steps necessary to get the data into a form that ski-kit learn would accept. Some steps that I took were probably not entirely necessary, such as my initial dealings with the NaN values. I replaced all NaN values with either 0 or the median of the column. For things like the number of messages received it seemed reasonable to put in the median, whereas for something like expenses there was no reason to believe that every person had expenses so I replaced each NaN with 0.

### Data culling
There were two obvious outliers that didn't refer to individuals and that needed to be removed. One was the TOTAL and the other THE TRAVEL AGENCY IN THE PARK. There was a single negative value for one individual's 'total_stock_value', which didn't make sense so I changed that to a positive value. I took a look at the number of missing values for each of the features. Out of 144 rows (after removing the two outliers) there were 141 missing values for 'loan_advances', 128 missing values for 'director_fees', 106 missing values for 'deferral_payments'. In my own analysis I chose to drop these, the features involving 'poi's (see below) and 'email_address'.

### Leakage
I chose to completely ignore the three features involing 'poi's (i.e. messages to a poi, messages from a poi, on the same receipt as a poi). It seemed to me somewhat nonsensical to design a classifier to identify a 'poi' and use as input three features that already assumed we knew who the 'poi's were. I was influenced in my decision by the paper [Leakage in Data Mining: Formulation, Detection, and Avoidance](http://goo.gl/PyRkQy).

### Combining features
I chose to add 'restricted_stock' to 'restricted_stock_deferred' to create a new feature 'restricted_stock_combined' since there were very few values for 'restricted_stock_deferred' and these values seemed to be intimately related.

### Feature selection
I used SelectKBest to try to optimize my models and use the features that would give me the best performance. However, the features that were identified as best in my own scripts didn't necessary yield the best results when using the provided tester.py script, perhaps because of the handling of the NaN values.

### Cross Validation
Following the suggestion of Sebastian in the course videos I chose to implement a cross-validation regime. Since the number of 'poi's was relatively small I used stratified k-fold cross validation so that each of the folds would have roughly the same proportion of 'poi's. I found there were often quite large differences in the scores depending on what value I chose for the number of folds. Since the overall dataset was quite small it didn't make much sense to me to have too many folds, so for the most part I chose either 3 or 4 folds. Even this small difference led to dramatic differences in scoring as summarized in the tables below, with 4 folds leading to higher F1 scores in four out of the six models I chose to examine.

### Parameter Tuning
I started off using the GridCV function for parameter tuning, but in the end I did most of the tuning manually. I liked being able to see exactly what would happen when I changed one parameter by a certain amount. I found the models completely insensitive to certain parameters and incredibly sensitive to other parameters. I think part of this is due to the small size of the dataset. I also found the scoring of the models sensitive to the 'random state' parameter, which shouldn't really make much difference, but in practice sometimes made quite a big difference.

### ML Models
I experimented with a few different machine learning models using the sci-kit learn package. In each case I got the model running and then tried to tune the parameters to improve performance. Here is a quick summary of the performance I was able to achieve with each model. For some models it was difficult to get both the Precision and Recall over the suggested threshold of 0.30. For each model I also calculated the [Matthews Correlation Coefficient](https://en.wikipedia.org/wiki/Matthews_correlation_coefficient), which was suggested as a good score to look at even when the classes are of quite different sizes, as they are here.

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
