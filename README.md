CREDIT RISK MODEL WITH EXPLANATIONS AND FAIRNESS CHECKS

A model that predicts which credit card customers are likely to miss a payment, explains each decision in plain words, and checks that men, women and different age groups are treated consistently.

Headline result

If a lender approves the safest 70% of applicants using the LightGBM model, the default rate among approved customers falls from 22% (approve everyone) to 11.8%, and the model turns down 63% of the customers who would have defaulted. A simple logistic regression catches 57% at the same approval level.                                       

What this project does

Predicts default risk with two models: a simple logistic regression (the classic bank model) and LightGBM (stronger, harder to explain).

Checks the risk scores are honest. When the model says 30% risk, about 30% really default.

Explains decisions with SHAP, including plain-language reasons for individual applicants.

Checks fairness across gender and age groups.

Shows the business trade-off between approving more customers and accepting more defaults.

RESULTS

Logistic regression (AUC)	0.704	Gini0.409
LightGBM	AUC	0.777	Gini0.554

Risk scores are well calibrated  

What drives the model
The most important input is PAY_0, how late the customer's most recent payment was. Credit limit and the latest bill amount come next.                                                                                                                              Example of a plain-language reason for a high-risk applicant: predicted default risk 92%; main reasons: 3 months late on the latest payment, low credit limit, 7 months late six months ago.

Fairness check

Gender, age and marital status are not used as model inputs, in line with UK lending rules. They are kept aside only to check outcomes. The decision rule is "approve the safest 80% of applicants".

Women	81.4%	(Approval rate) 10.2 (Good customers wrongly rejected)
Men	77.9%(Approval rate)	13.0% (Good customers wrongly rejected)

The approval ratio between the lowest and highest group is 0.96 for gender and 0.95 for age, above the common 0.80 rule of thumb.
Model quality (AUC) is similar across groups, between 0.755 and 0.794.
Men who would have repaid are turned down slightly more often (13.0% vs 10.2%). The model never sees gender, so this comes from other inputs, such as payment history, that differ between groups.                                                                                                                     

Limitations

The data is from Taiwan in 2005, not the UK market, so this is a demonstration of the method, not a model ready for use.
Results come from a single train/test split.
The 51+ age group is small (471 people in the test set), so its numbers are less reliable.
Marital status is kept aside but has not been audited yet.
At an 80% approval level, about half of future defaulters are still approved. The business chart shows how this changes with a stricter policy.

Data
Default of Credit Card Clients, UCI Machine Learning Repository (CC BY 4.0). 30,000 customers, 22% defaulted.

How to run
on Kaggle
Open the dataset page and click New Notebook.
Upload credit_risk.ipynb from this repo, or paste in the code.
Run all cells.

On your own computer
bash
pip install -r requirements.txt
Download UCI_Credit_Card.csv from the dataset page above and put it in the same folder as credit_risk.ipynb.
Open credit_risk.ipynb and change the data path to UCI_Credit_Card.csv.
Run all cells.

Tools
Python, pandas, scikit-learn, LightGBM, SHAP, matplotlib.
