# ml-fake-social-profile (Heading)
- bullet
  - next set
** bold **
_italic_
__Best features__
`Highly negative`
*Test*


# ml-fake-social-profile
Detection of Fake Profiles in Social Media 'Twitter' from data received and collected by researcher with the condition not be re-distributed. The data comprise of validated accounts data labelled under various categories - 
genuine accounts; accounts spreading social spammed tweets/retweets - in favor of political candidate, spammed 
messages of paid app for mobile devices or products on sale in e-commerce site; traditional spammed messages - scam 
urls, job offers & fake followers.

# Problem Statement
Million of consumers are using different social platforms. They are sharing, collaborating or exchanging views & contents on various channels on general or focused topics relevant to academic, geo-political, technology, social affairs etc, with other consumers. Behind the digital wall, it’s completely hidden about the fact whether consumer is interacting with real person with right intention or fake users who in the platform with wrong intention or automated bots. For consumer digital security, It is deemed important to identify such actors and avoid such interactions. Fake users on the social media with malicious intensions either using automated bots, group of real bad actors working in-tandem or by using other technical advancement to generate traffic with intention to viral hashtags, spreading fake news, conducting digital crimes and many more actions which can potentially harm personally to individual or society as a whole. These activities may lead real/genuine consumers to take actions which may be vulnerable to them - in terms of monetary loss, social prestige or on the contrary, helps un-intentionally/unknowingly bad actors to circulate their spammed messages within real digital consumers herd and hence, Identification of such profiles are extremely important and integrate model with automated process for observing millions of profiles and their activities to avoid proliferation of such profiles at the source to strengthen the digital consumer security.

**Data Schema**
[data schema link](https://github.com/vishalnigam/ml-fake-social-profile/blob/main/data/Data_SCHEMA.txt)

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
  - `source_id`
  - `target_id`
- _Friends_
  - `source_id`
  - `target_id`

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

**Base Modelling (Dummy Classifier)**
Baseline modelling with DummyClassfier 
- Baseline Accuracy:        0.8650793650793651
- Baseline F1 Score:        0.8024991556906451
- Baseline Precision Score: 0.7483623078861175
- Baseline Recall Score:    0.8650793650793651

**Model Performance**
__Before__: With default parameters for `KNN`, `Logistic Regression`, `SVC` & `Decision Tree Classfier`
Model                   Train score	  Test score	  Train time	Accuracy	Precision	Recall	F1-score							
knn	                    0.989942	    0.988889	    14.348690	  0.988889	0.987500	0.929412	0.957576
logisticregression	    0.989412	    0.985714	    0.998861	  0.985714	0.963415	0.929412	0.946108
svc	                    0.994706	    0.988889	    0.069812	  0.988889	0.964286	0.952941	0.958580
decisiontreeclassifier	1.000000	    0.988889	    1.153847	  0.988889	0.953488	0.964706	0.959064

__After__: With best parameters after Grid Search Cross Validaion for `KNN`, `Logistic Regression`, `SVC` & `Decision Tree Classfier`
Model               Train Score    Test Score    Avg Fit Time    Accuracy    Precision   Recall    F1-Score						
knn                 0.991530        0.990476      0.099001       0.990476    0.964706    0.964706  0.964706
logisticregression	0.991530	      0.990476	    0.424832	     0.990476	   0.975904	   0.952941	 0.964286
svc	                0.990471	      0.992063	    0.876690	     0.992063	   0.976190	   0.964706	 0.970414
decisiontreeclasfer	0.998412	      0.982540	    0.037921	     0.982540	   0.951220	   0.917647	 0.934132

# Link to Jupyter notebook
[notebook link](https://github.com/vishalnigam/ml-fake-social-profile/blob/main/user-account.ipynb)


Data Cleaning and EDA
• The dataset is clean: imputation and removal of missing values, removal of duplicate values
• Outliers analysis to identify anomalies in the dataset.
• Perform feature engineering to extraction and transformation of variables from raw data.

Modeling:
• Identify an appropriate classification or regression ML model to utilize as baseline for your analysis.
• Valid interpretation of an evaluation metric.
• Clear identification of an evaluation metric.
• Clear rationale for use of the given evaluation metric.