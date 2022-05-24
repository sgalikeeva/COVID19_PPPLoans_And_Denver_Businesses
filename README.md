# Denver Businesses and PPP Loan Repayment Risk

## Selected topic
Denver Businesses and PPP Loan Repayment Risk

## Reason why we selected the topic 
Businesses were hit hard during the COVID-19 pandemic.  Many industries suffered significant sales and job losses since the pandemic began. We chose to explore how businesses used Paycheck Protection Program (PPP) loans and whether loan repayment can be predicted using Machine Learning. Our whole team lives in Denver, CO so we chose to focus solely on businesses in the Denver metro area. 

## Description of our source of data
We have chosen to explore Denver business data from the Yelp Fusion API and loan data from the Paycheck Protection Program (PPP) managed by the Small Business Administration (SBA).
Sources:
*  [Yelp Fusion API](https://www.yelp.com/developers/documentation/v3/get_started)
*  [PPP Data](https://www.sba.gov/funding-programs/loans/covid-19-relief-options/paycheck-protection-program/ppp-data) 

## Questions we hope to answer with the data
* Can business data and PPP loan data reasonably predict whether a loan will be paid in full or not?

* Do factors like the type of businesses, location, gender of lendee, size of loan or other factors affect loan repayment?

* Were certain types of businesses able to pay loans back in full while others weren't? 

## Data Exploration & Analysis Phase
We explored multiple data sources as part of our data exploration phase and ultimately settled on using the Yelp Fusion API and the Small Business Administration’s (SBA) Paycheck Protection Program (PPP) loan data. Our initial intent was to only use Denver restaurant data from Yelp, but we expanded it to include the [top industries of Denver businesses that received PPP loans](https://data.coloradoan.com/paycheck-protection-program-loans/summary/colorado/denver-county/08031/) to increase the amount of data to analyze. The Yelp categories used to pull business data from Yelp were: fashion, financial services, health, professional services, real estate, restaurant, salon and transportation. 

The Yelp Fusion API has a limit of calling 1000 entries. To increase the amount of data, a zip code parameter was used. The zip code parameter is not strict and pulls a substantial number of duplicates which had to be removed. To ensure that a wide variety of businesses were pulled, category parameters were set for each call as the default is restaurants.

## Machine Learning Model
### Data Preprocessing
After extracting the data from the Yelp Fusion API and the SBA, the data was transformed to the cleanest version it could be. 

The Yelp data was extracted and saved into multiple spreadsheets, depending on the category parameter pulled. A column was added to each spreadsheet signifying the specific category and the spreadsheets were merged into one business dataframe. Duplicates, unneeded columns and null values were removed.

The PPP data initially had nationwide information; this was narrowed down to the Denver area using zip code information. The PPP data had many misspellings in the business name. The business names also included extra characters like LLC, Inc, Corp, commas and periods, etc. The business names were cleaned using regex expressions to ensure the business names would match up when the Yelp data and PPP data was combined. Again, duplicates, unneeded columns and null values were removed. 

The two datasets were merged on the business name and our dataset shrunk from 13,029 to 1,357. The merged data was then encoded to prepare for machine learning models. 

### Feature Engineering and Preliminary Feature Selection
The features needed to be analyzed and determined whether to keep them as part of the dataframe or not. The target (our Y) was the loan status, whether it was Paid in Full or granted an Exemption 4. A random forest classifier was used to determine the importance of features in the dataset. From this ranking, it was determined that a few columns were extraneous and were removed. From here, a number machine learning models were run to determine the best model. 

The random forest classifier ranked the top 5 features as:
1. InitialApprovalAmount
2. Longitude
3. Latitude
4. Yelp Review Count
5. Jobs Reported

### Training and Testing Sets
The data was split into training and testing set using train_test_split and a random_state of 1. 

### Model Choice
The best model was determined to be random forest classifier due to its high accuracy at 90.4% and out of all the models that were run it had the highest precision at 33%. The main limitation of random forest is that a large number of trees can make the algorithm too slow and ineffective for real-time predictions. The benefits of random forest are it is robust against overfitting, can be used to rank the importance of input variables in a natural way and are robust to outliers and nonlinear data.

Below is the Confusion Matrix, Accuracy Score and Classification report from our model. 


## Dashboard
- Final Presentation

Our final presentation is available on Google Slides at this [link](https://docs.google.com/presentation/d/1dWn_G4nov9FRoMqOXes7-a8apl2l8IZGHHXaMj0cDug/edit?usp=sharing).

- Description of the tools used to create the final dashboard

We used Tableau to [visualize our data](https://public.tableau.com/app/profile/dylan1351/viz/PPPLoanAnalysis/Story1).

- Description of interactive element

We have various interactive elements on our Tableau dashboard including a map of businesses and various plots showing size of loan, types of businesses and other features.  Users are able to change views and hover over data points to get additional information from the map and plots. 


✓ Technologies, languages, tools, and algorithms used throughout the project
✓ Description of data preprocessing
✓ Description of feature engineering and the feature selection, including the team's decision-making process

✓ Explanation of model choice, including limitations and benefits
✓ Explanation of changes in model choice (if changes occurred between the Segment 2 and Segment 3 deliverables)
✓ Description of how model was trained (or retrained, if they are using an existing model)
✓ Description and explanation of model’s confusion matrix, including final accuracy score
Additionally, the model obviously addresses the question or problem the team is solving.
