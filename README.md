# Denver Businesses and PPP Loans

## Selected topic
Denver Businesses and PPP Loans

## Reason why we selected the topic 
Businesses were hit hard during the COVID-19 pandemic. Many industries suffered significant sales and job losses since the pandemic began. According to the [Colorado Business Economic Outlook report](https://www.colorado.edu/today/2020/08/13/colorado-lose-128500-jobs-2020-report-forecasts), Colorado alone reported a job loss of 4.6% or 128,500 jobs by mid 2020. We chose to explore Yelp data on businesses that used Paycheck Protection Program (PPP) loans. Our whole team lives in Denver, CO so we chose to focus solely on businesses in the Denver metro area.

## Description of our source of data
We explored Denver business data from the Yelp Fusion API and loan data from the Paycheck Protection Program (PPP) managed by the Small Business Administration (SBA).
Sources:
*  [Yelp Fusion API](https://www.yelp.com/developers/documentation/v3/get_started)
*  [PPP Data](https://www.sba.gov/funding-programs/loans/covid-19-relief-options/paycheck-protection-program/ppp-data) 

## Technologies
The following technologies, languages, and tools were used throughout the project:
* Python
* Pandas
* Anaconda/Jupyter Notebook
* SciKit Learn
* Tableau

## Questions we hope to answer with the data
* Can Yelp data and PPP loan data reasonably predict whether a business is in good standing and satisfies the terms of its loan?

* What were the most important features contributing to our machine learning model? 

* Why was the professional services industry granted the largest amount of PPP loans in our dataset? What are the implications of this?

## Data Exploration & Analysis Phase
We explored multiple data sources as part of our data exploration phase and ultimately settled on using the Yelp Fusion API and the Small Business Administration’s (SBA) Paycheck Protection Program (PPP) loan data. Our initial intent was to only use Denver restaurant data because it seemed like the hospitality industry was one of the hardest hit.  The [Colorado Business Economic Outlook report](https://www.colorado.edu/today/2020/08/13/colorado-lose-128500-jobs-2020-report-forecasts) reported that the leisure & hospitality sector in Denver lost 22.3% of jobs in 2020. Unfortunately, the restaurant dataset was too small after combining with the PPP loan data set. We then expanded it to include the [top industries of Denver businesses that received PPP loans](https://data.coloradoan.com/paycheck-protection-program-loans/summary/colorado/denver-county/08031/) to increase the amount of data to analyze. The Yelp categories used to pull business data were: 
* fashion
* financial services
* health
* professional services
* real estate
* restaurants
* salons 
* transportation. 

The Yelp Fusion API has a limit of calling 1000 entries. To increase the amount of data, a zip code parameter was used. The zip code parameter is not strict and pulls a substantial number of duplicates which had to be removed. To ensure that a wide variety of businesses were pulled, category parameters were set for each call as the default is restaurants.

## Machine Learning Model
### Data Preprocessing
After extracting the data from the Yelp Fusion API and the SBA, the data was transformed to the cleanest version it could be. 

The Yelp data was extracted and saved into multiple spreadsheets, depending on the category parameter pulled. A column was added to each spreadsheet signifying the specific category and the spreadsheets were merged into one business dataframe. Duplicates, unneeded columns and null values were removed.

The PPP data initially had nationwide information; this was narrowed down to the City of Denver. The PPP data had many misspellings in the business name. The business names also included extra characters like LLC, Inc, Corp, commas and periods, etc. The business names were cleaned using "replace" expressions to ensure the business names would match up when the Yelp data and PPP data was combined. Again, duplicates, unneeded columns and null values were removed. 

The two datasets were merged on the business name and our dataset shrunk from 13,029 to 1,357. The merged data was then encoded to prepare for machine learning models. 

### Feature Engineering and Preliminary Feature Selection
The features were analyzed using the random forest classifier and we determined as a group whether to keep them as part of the dataframe. The target (our Y) was the "loan status", whether it was Paid in Full or granted an Exemption 4. We eliminated features like Loan Forgiveness Amount because that column was too closely related to the target. We also eliminated demographic data because the majority of the rows were null values in those columns. From here, a number of machine learning models were run to determine the best model including the following: 
* Logistic Regression
* Random Over Sampler
* SMOTE
* Cluster Centroids
* SMOTEENN
* Decision Tree Classifier
* Support Vector Machine
* Random Forest Classifier
* Easy Ensemble
* Balanced Random Forest  

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
The best model was determined to be the random forest classifier due to its high accuracy at 90.4%. Additionally, out of all the models that were run, it had the highest precision at 33%. We looked at the precision of the exempted loans because we wanted to limit the false positives. The main limitation of random forest is that a large number of trees can make the algorithm too slow and ineffective for real-time predictions. The benefits of random forest are its robustness against overfitting, its usefulness in ranking the importance of input variables in a natural way, and its ability to accomodate outliers and nonlinear data.

Below is the Confusion Matrix, Accuracy Score and Classification report from our model. 

![image of confusion matrix](https://github.com/ereekaj/Final_Project/blob/main/Images/Confustion_matrix.png)

## Further Analysis
While exploring the data and beginning to create our visualizations, we were suprised to find that Professional Services accounted for a large amount of the loans granted in Denver. Our analysis showed the following:

* Professional services account for 39.92% of the PPP loans

* Nationwide: 10% of all PPP loans were for professional services firms

* Denver area: 17% of all PPP loans were for professional services firms

* Employment agencies accounted for 35.45% of professional services loans

* Law firms accounted for 34.87% professional services loans

* Average PPP loan of entire dataset: $139,597

* Average PPP loan of professional  services: $234,831

* Average PPP loan  of employment agencies: $1,340,443

* Average PPP loan of law firms: $198,223

The graphs below show these stats in action.  The graph on the left shows that  the professional services industry did receive the highest amount of loans despite not receiving the most loans (graph on the right).
![plots by industry](https://github.com/ereekaj/Final_Project/blob/main/Images/PlotsByIndustry.png)

### Results 
**Question:** Can Yelp data and PPP loan data reasonably predict whether a business is in good standing and satisfies the terms of its loan? 

The machine learning model was able to predict loan status with an accuracy of 90.4%; however, the feature importance showed that the yelp data features did not really add much to the machine learning model. Only 2 yelp categories showed up in the top 10 features. That caused us to explore some other aspects of the data. 

**Question:** What were the most important features contributing to our machine learning model? 

As mentioned above, the feature importance showed that the yelp data features did not really add much to the machine learning model. Only 2 yelp categories showed up in the top 10 features. That caused us to explore some other aspects of the data. 

**Question:** Why was the professional services industry granted the largest amount of PPP loans in our dataset? What are the implications of this?

It was surprising to find that professional services accounted for the highest amount of loan dollars, but further research showed that this was not unique to Denver. Our research showed that business and professional services firms across the country borrowed more PPP loans than all but four segments of the U.S. economy. According to this [article](https://realeconomy.rsmus.com/ppp-loan-data-business-professional-services), "Industry executives took advantage of federal assistance in an effort to maintain their capabilities and client relationships by retaining their people."

Through our data exploration, machine learning and further analysis, we were able to find the answers to our questions and see the impact of COVID-19 on the Denver metro area and its businesses.  

### Lessons Learned

As the team performed the data analysis, a few lessons were learned.

1. Machine learning is not the end all be all. It did not tell us the full data story.  For example, our ML model did not show category as being an important feature, but our visualization showed a much different picture. 

2. There is always more to be explored. In this case, we realized we could have asked more questions about potentially fraudulent loans and discovered ways to identify them in our model.

3. Data visualizations and conclusions, while impactful, are merely the results of extensive data exploration, cleaning, and curiosity.

### Future Analysis

Future analysis could focus on determining whether industries recovered due to receiving PPP loans and whether fraud can be detected from the data. 

## Dashboard
### Final Presentation

Our final presentation is available on Google Slides at this [link](https://docs.google.com/presentation/d/1dWn_G4nov9FRoMqOXes7-a8apl2l8IZGHHXaMj0cDug/edit?usp=sharing).

### Description of the tools used to create the final dashboard

We used Tableau to [visualize our data](https://public.tableau.com/app/profile/dylan1351/viz/PPPLoanAnalysis/Story1).

### Description of interactive element

We have various interactive elements on our Tableau dashboard including a map of businesses and various plots showing size of loan, types of businesses and other features.  Users are able to change views and hover over data points to get additional information from the map and plots. Click on the [tableau link](https://public.tableau.com/app/profile/dylan1351/viz/PPPLoanAnalysis/Story1) to see the dashboard in action or refer to the screenshots below.

Loan Amount by Business 

![Loan Amount by Business](https://github.com/ereekaj/Final_Project/blob/main/Images/LoanAmtbyBixetc.png)

Map of loans by location and size

![Loans by location map](https://github.com/ereekaj/Final_Project/blob/main/Images/Map.png)

Loan Amounts and Counts by Industry
![plots by industry](https://github.com/ereekaj/Final_Project/blob/main/Images/loanamtbyindustryvjobs.png)
