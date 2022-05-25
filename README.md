# Denver Businesses and PPP Loan Repayment Risk

## Selected topic
Denver Businesses and PPP Loan Repayment Risk

## Reason why we selected the topic 
Businesses were hit hard during the COVID-19 pandemic. Many industries suffered significant sales and job losses since the pandemic began. According to the [Colorado Business Economic Outlook report](https://www.colorado.edu/today/2020/08/13/colorado-lose-128500-jobs-2020-report-forecasts), Colorado alone reported a job loss of 4.6% or 128,500 jobs by mid 2020. We chose to explore yelp data on business that used Paycheck Protection Program (PPP) loans. Our whole team lives in Denver, CO so we chose to focus solely on businesses in the Denver metro area.

## Description of our source of data
We chose to explore Denver business data from the Yelp Fusion API and loan data from the Paycheck Protection Program (PPP) managed by the Small Business Administration (SBA).
Sources:
*  [Yelp Fusion API](https://www.yelp.com/developers/documentation/v3/get_started)
*  [PPP Data](https://www.sba.gov/funding-programs/loans/covid-19-relief-options/paycheck-protection-program/ppp-data) 

## Technologies
The following technologies, languages, and tools were used throughout the project:
* Python
* Pandas
* NumPy
* Anaconda/Jupyter Notebook
* SkiKit Learn
* Tableau

## Questions we hope to answer with the data
* Can business data and PPP loan data reasonably predict whether a loan will be paid in full or not?

* What were the most important features contributing to our machine learning model? 

* Why was the professional services industry granted the largest amount of PPP loans in our dataset?

* [OTHER QUESTIONS?]

## Data Exploration & Analysis Phase
We explored multiple data sources as part of our data exploration phase and ultimately settled on using the Yelp Fusion API and the Small Business Administration’s (SBA) Paycheck Protection Program (PPP) loan data. Our initial intent was to only use Denver restaurant data because it seemed like the hospitality industry was one of the hardest hit.  The [Colorado Business Economic Outlook report](https://www.colorado.edu/today/2020/08/13/colorado-lose-128500-jobs-2020-report-forecasts) reported that the leisure & hospitality sector in Denver lost 22.3% of jobs in 2020. Unfortunately, the restaurant dataset was too small after combining with the PPP loan data set. We then expanded it to include the [top industries of Denver businesses that received PPP loans](https://data.coloradoan.com/paycheck-protection-program-loans/summary/colorado/denver-county/08031/) to increase the amount of data to analyze. The Yelp categories used to pull business data from Yelp were: fashion, financial services, health, professional services, real estate, restaurant, salon and transportation. 

The Yelp Fusion API has a limit of calling 1000 entries. To increase the amount of data, a zip code parameter was used. The zip code parameter is not strict and pulls a substantial number of duplicates which had to be removed. To ensure that a wide variety of businesses were pulled, category parameters were set for each call as the default is restaurants.

## Machine Learning Model
### Data Preprocessing
After extracting the data from the Yelp Fusion API and the SBA, the data was transformed to the cleanest version it could be. 

The Yelp data was extracted and saved into multiple spreadsheets, depending on the category parameter pulled. A column was added to each spreadsheet signifying the specific category and the spreadsheets were merged into one business dataframe. Duplicates, unneeded columns and null values were removed.

The PPP data initially had nationwide information; this was narrowed down to the Denver area using zip code information. The PPP data had many misspellings in the business name. The business names also included extra characters like LLC, Inc, Corp, commas and periods, etc. The business names were cleaned using regex expressions to ensure the business names would match up when the Yelp data and PPP data was combined. Again, duplicates, unneeded columns and null values were removed. 

The two datasets were merged on the business name and our dataset shrunk from 13,029 to 1,357. The merged data was then encoded to prepare for machine learning models. 

### Feature Engineering and Preliminary Feature Selection
The features were analyzed using the random forest classifier and we determined as a group whether to keep them as part of the dataframe or not. The target (our Y) was the loan status, whether it was Paid in Full or granted an Exemption 4. We eliminated features like Loan Forgiveness Amount because that column was too closely related to the target. We also eliminated demographic data but the majority of the rows were null values in those columns. From here, a number machine learning models were run to determine the best model. 

The random forest classifier ranked the top 10 features as:
1. InitialApprovalAmount
2. Longitude
3. Latitude
4. Yelp Review Count
5. Jobs Reported
6. BorrowerZip
7. Yelp Rating
8. Term
9. Year Loan Approved 2020
10. Year Loan Approved 2021

### Training and Testing Sets
The data was split into training and testing set using train_test_split and a random_state of 1. 

### Model Choice and Confusion matrix
The best model was determined to be random forest classifier due to its high accuracy at 90.4% and out of all the models that were run it had the highest precision at 33%. The main limitation of random forest is that a large number of trees can make the algorithm too slow and ineffective for real-time predictions. The benefits of random forest are it is robust against overfitting, can be used to rank the importance of input variables in a natural way and are robust to outliers and nonlinear data.

Below is the Confusion Matrix, Accuracy Score and Classification report from our model. 

![image of confusion matrix](https://github.com/ereekaj/Final_Project/blob/main/Images/Confustion_matrix.png)

### Results 
**Question:** Can business data and PPP loan data reasonably predict whether a loan will be paid in full or not? 

The machine learning model was able to predict loan status with an accuracy of 90.4%; however, the feature importance showed that the yelp data features did not really add much to the machine learning model. Only 2 yelp categories showed up in the top 10 features. That caused us to explore some other aspects of the data. 

**Question:** What were the most important features contributing to our machine learning model? 

As mentioned above, the feature importance showed that the yelp data features did not really add much to the machine learning model. Only 2 yelp categories showed up in the top 10 features. That caused us to explore some other aspects of the data. 

**Question:** Why was the professional services industry granted the largest amount of PPP loans in our dataset?

[ADD ANSWER]

### Lessons Learned

### Future Analysis

## Dashboard
### Final Presentation

Our final presentation is available on Google Slides at this [link](https://docs.google.com/presentation/d/1dWn_G4nov9FRoMqOXes7-a8apl2l8IZGHHXaMj0cDug/edit?usp=sharing).

### Description of the tools used to create the final dashboard

We used Tableau to [visualize our data](https://public.tableau.com/app/profile/dylan1351/viz/PPPLoanAnalysis/Story1).

### Description of interactive element

We have various interactive elements on our Tableau dashboard including a map of businesses and various plots showing size of loan, types of businesses and other features.  Users are able to change views and hover over data points to get additional information from the map and plots. Click on the [tableau link](https://public.tableau.com/app/profile/dylan1351/viz/PPPLoanAnalysis/Story1) to see the dashboard in action or refer to the screenshots below.

Loan Amount by Business 

![Loan Amount by Business](https://github.com/ereekaj/Final_Project/blob/main/Images/LoanAmtByBusiness.png)

Map of loans by location and size
![Loans by location map](https://github.com/ereekaj/Final_Project/blob/main/Images/LoansByLocationMap.png)

Plots by industry
![plots by industry](https://github.com/ereekaj/Final_Project/blob/main/Images/PlotsByIndustry.png)
