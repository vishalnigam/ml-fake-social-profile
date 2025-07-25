# ml-fake-social-profile
Million of consumers are using different social platforms. They are sharing, collaborating or exchanging views & contents on various channels on general or focused topics relevant to academic, geo-political, technology, social affairs etc, with other consumers. Behind the digital wall, it’s completely hidden about the fact whether consumer is interacting with real person with right intention or fake users who in the platform with wrong intention or automated bots. For consumer digital security, It is deemed important to identify such actors and avoid such interactions. Fake users on the social media with malicious intensions either using automated bots, group of real bad actors working in-tandem or by using other technical advancement to generate traffic with intention to viral hashtags, spreading fake news, conducting digital crimes and many more actions which can potentially harm personally to individual or society as a whole. These activities may lead real/genuine consumers to take actions which may be vulnerable to them - in terms of monetary loss, social prestige or on the contrary, helps un-intentionally/unknowingly bad actors to circulate their spammed messages within real digital consumers herd and hence, Identification of such profiles are extremely important and integrate model with automated process for observing millions of profiles and their activities to avoid proliferation of such profiles at the source to strengthen the digital consumer security.

# Data
Detection of Fake Profiles in Social Media 'Twitter' from data received and collected by researcher with the condition not be re-distributed. The data comprise of validated accounts data labelled under various categories - 
genuine accounts; accounts spreading social spammed tweets/retweets - in favor of political candidate, spammed 
messages of paid app for mobile devices or products on sale in e-commerce site; traditional spammed messages - scam 
urls, job offers & fake followers.

**Data Schema**
[schema link](https://github.com/vishalnigam/ml-fake-social-profile/blob/main/data/DATA_SCHEMA.txt)

**Features**
Most of the features in users account table are relevent to asthetic of the tweets and decide personalization for look and feel which mostly can not be converted into numerical values appropriate for regression or classification modelling.Following are the features choosen for analysis and modeling purpose
- _User Account_
  - `statuses_count`   - Total number of tweets the user has posted 
  - `followers_count`  - Number of followers the user has
  - `friends_count`    - Number of accounts the user is following
  - `favourites_count` - Number of tweets the user has liked
  - `listed_count`     - Number of public lists the user appears in
  - `url`              - User-defined link in their Twitter bio, typically pointing to personel website, blog etc
  - `geo_enabled`      - User has allowed geolocation (location tagging) in their tweets
- _Followers_
  - `source_id`        - Twitter account id
  - `target_id`        - Followers twitter account id 
- _Friends_
  - `source_id`        - Twitter account id 
  - `target_id`        - Friends twitter account id 

**Data Observation**:
- Based on the correlation between various feature with account type (Real|Fake) 
  - geo_enabled       : `Strong positive`       : Real accounts highly likely to have geolocation enabled than fake users
  - url               : `Moderate positive`     : Real accounts usually provide URLs more often than Fake accounts
  - statuses_count    : `Moderate positive`     : Real accounts tweets more frequently. Fake ones are more passive.
  - favourites_count  : `Weak positive`         : Real accounts favorite more often than Fake accounts
  - listed_count      : `Weak positive`         : Fake accounts are less recognized and thus appear less in public lists.
  - followers_count   : `Very weak positive`    : Fake accounts barely have any relationship.
  - friends_count     : `Very weak negative`    : Not a strong signal.
- __URL__ which is `optional` field for twitter accounts 
  - URLs are missing in large proportionate for fake accounts in comparision to Real Accounts
- __Geo Status__ is `optional` field for twitter accounts                       
  - Being privacy, enabling geo status is not mandatory however, real acounts has large number of geo enabled than fake accounts
- _Statuses Count_, _Followers Count_, _Friends Count_, _Favourites Count_ data is highly skewed reaching to millions
between 75% to 100% quartile
- Inter Quartile Range observation for Statuses Count', 'Followers Count', 'Friends Count', 'Favourites Count' are
  - __Statuses Count__
    - Fake Account : Median status count is `very low`. Entire IQR near the bottom. Large number of outliers in above 100 and even >2500 statuses so, most fake accounts are very inactive but few extemely active, possible bots.
    - Real Account : Median is `much higher`, real accounts tweet more on average, IQR spread wider and showing variability Outliers exists but are distributed more naturally 
  - __Follower Count__ 
    - Fake Account : Median status count `very low` and IQR near bottom but large number of outliers
    - Real Account : `Natural distribution` of follower counts
  - Similar pattern for friends count and favourite counts for real and fake accounts
- Relation among the features generated using pairplot
  - Fake users relations among various features are concentrated and have similar pattern rather than distributed which give sense of abnormality or seems generated based on certain logic
  - Distribution plot for various feature reflect the similar observations

# Modeling
**Modeling Objectives**
- Compare the performance of the classifiers :
  - K Nearest Neighbor
  - Logistic Regression
  - Decision Trees
  - Support Vector Machines
- Based on parameters :
  - Time to fit
  - Predication efficacy

**Base Modeling (Dummy Classifier)**
Baseline modelling with DummyClassfier 
- Baseline Accuracy:        0.8650793650793651
- Baseline F1 Score:        0.8024991556906451
- Baseline Precision Score: 0.7483623078861175
- Baseline Recall Score:    0.8650793650793651

**Model Performance**


**Model Evaluation**
- Decision Tree Classifier took min average time (0.0339101) among all the modeling technique used to fit the model
- Decisoin Tree Classifier score well on training (0.9873990) and perform well in comparision to other models for test  score (0.978820) as well with no signs of over-fitting
- Closest to DTC result is KNN model which achieves near same result with maximum accuracy (0.975794) 
- Space vector classification took maximum time (78.630172) to fit 
- Overall, Decision Tree Classifier achieve highest rating and being best with highers accuracy (0.978820) and best f1-score (0.972332)

**Recommmandation and next steps**
- To increase model prediction, ensamble or stacked multiple models would be recommanded. Currently, account dataset   

# Link to Jupyter notebook
[notebook link](https://github.com/vishalnigam/ml-fake-social-profile/blob/main/user-account.ipynb)