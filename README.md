# Interview Attendance
Overall process:
* Exploratory Data Analysis (EDA) and some feature engineering in notebook `EDA and Feature Engineering.ipynb`
* First, try Logistic Regression in `LogisticRegression.ipynb` notebook
* Then, try a Boosted decision tree model (XGBoost) in `BoostedTrees.ipynb` notebook
* Experiment with h2o.ai's AutoML feature in `AutoML.ipynb` notebook
* Make predictions and build submission file in `Submission
Generation.ipynb`

## Final submission file
`submission.csv` located in root directory of project/archive


## Response to Task 2
***Prompt:*** 

***A client has scored a candidate with your model and it gave the candidate a 30% 
chance of attending the interview. However, the candidate did come to the interview. 
The client would like to know why there is this apparent discrepancy in your 
model. How would you explain this occurrence? Could you provide a better way 
for the client to evaluate your model's performance***

In general, I would explain to the client the general idea behind ROC analysis and confusion matrix
data.  

While it's somewhat counter-intuitive that a 30% probability of attendance (p\[Attend\]) resulted 
in an unexpected outcome, A binary classifier uses the p\[Attend\] as a raw output
and uses a threshold to determine whether that p\[Attend\] is really high enough to
warrant an expectation (layman term, not statistical expectation) of attendance.

Perhaps the threshold was somewhat low, i.e. p\[Attend\] > 20% to predict attendance.  Then,
we would expect attendance.

Going forward, it would be helpful to use p\[Attend\] **AND** the classifier threshold
together to makea prediction, rather than fiddle with one piece of raw output than 
can be subject to wrong interpretation. 


## Response to Task 3
***Prompt*** 

***Describe how you would create a simple application or RESTful API that returns back predictions given the required parameters. A few
sentences or bullet-points will suffice.***

Since I used h2o.ai's H2O3 open source library to affect predictions, I'd 
implement a basic web API using Python's Flask library to prototype something 
quickly.  I'd also leverage unittest or pytest to build a test suite that exercises 
the predictions and models that H2O3's model object generates.

To scale this, however, involves a higher level architecture.  One possibility is to 
serve the web API on an autoscaled fleet of EC2 instances in AWS, with a load balancer.

AWS also has a WEb API Gateway service that takes some of the heavy lifting
out of implementing a web API at scale.

If AWS is used, there is also the decision to use EC2 instances/servers, 
lambda functions, or another AWS construct to make predictions.  I tend to favor EC2
instances, as they tend to be more configurable, and aren't subject to cold start issues
when they are in a VPC. 