## Model Retraining
if model performance doesnt change, then why should we retrain? still we may find advantages with updated data. When the toll plaza problem was running, we tried to do a model on completely new set of data in december to accomodate rainy season, yet it performed inferior to original, we ned to only add a few of the previous model. But there was definetly a improvement ion performance when we took low confident samples, previous samples and mainly hourly samples, the night performance increased. we dont know when it will work, when it will not work, its only decided on thetestset and pseudo running on real data. Did literatuire on this subject improved? what is the current level going through references in interest of apoplication in one of the projects. lets see how it is

1. [KDnuggets](https://www.kdnuggets.com/2019/12/ultimate-guide-model-retraining.html)
- the very first argument is when the distribution of data changes. Yes when distribution of data changes by definition as we are extrapolating our evaluation metrics on test data doesnt hold true. So Idealy I should check my test set distribution as long as test set distribution is similar to the production data model performance must remain the same?
- For lingo freaks who say model drift and concept drift , concept drift is a better name for the changing data influencing model performance model drift is the popular lingo, so they are both one and the same. although there can be obvious other case of model assumption itself getting violated and causing degradation of model performance that is just a case of bad assumption either because it it tricky or human error, ignoring the discussion for that case. But as a practitioner we should always verify if model assumption is causing the issue. 
eg: lets say we have given image based classification for toll plaza , no matter how many retrains we do by monitoring underperformance , resampling and retraining , we cant get the accuracy that can be achieved from video and sequence based assumption(and may be that can be beaten by a profile view detector and classifying based on from\nt and profile view)

### How to monitor this concept drift?
- if model performance can be evaluated/ if ground thriths can be obtained then that is some indicator opf either a bad training split or changing environment 
- In time series we can take historic values and see how the model trained on prehistoric values deteriote with time due to change in environment, this is like understand model drift in offline itself. any kind of estimate at this level if its possible for the problem should be included in productionising 
- Examining Feature distribution of live and predicted. Here the reference talks about the changing in training, but I feelit should be testing as we are validating the stats based on test. But Ideally test will be very similar to vaL and mostly training(I cant come up with an example where test is dissimilar to training even in timeseries that seems like can it work? so assuming all three train, test and val to be the same distribution)
- A point to note here is when we are monitoring we need not have any ground thruth for live data, we are just inferring that as distribution is changing performance can go bad
- There can be many ways to monitor the distribution change , may be using another descriminator or a fewshot learning model. But these simple statistics can be starting point and can be applicable very widely/generically
 -- Range of possible values
 -- histogram of values
 -- whether feature accepts NULLm, if so how many NULLS?
 _ He internally refers to another [this paper](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/45742.pdf) which says as many features are dependent on the correlation betwwen the features we need to monitor them as well
  -- Track correlation between features
  -- make a model with one or two subset of features
  -- remove one or two features from the testset
  The last two points were not evident to me, may be need to reference the paper to get a feeol on whta exactly they are doing 
  
  Next reference is [Machine learning high interest credit card paper](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/43146.pdf) which says that if target distribution changes then almost always the prediction performance will decrease(I Think for many datasets for classification will have atleast one class which is less frequent, so if wwe see a distribution over time we will have less samples of that class , wehere as in training we ideally want it to be equal sampled. so I think this assumption should not hold good but as a alert if we need to configure this or not can simply decided on case to case basis
  he also agrees it being no means a comprehensive test n\but his reason is that if a naive model which avaerages the y labels is deployed, even if intra label distribution change the result could be same
  
  Two questions we need to be able to answer
  - How often do we retrain? some problems will give direct answer as data wont be available to retrain until next iteration
  if thats not the case, like KPI prediction, we need to monitor some score and decide on divergence
  - What data goes into retrain? this is also hard, even if env changes its not better to use new small dataset as training data matters
  - will online leartning work? mostly batching should do good as we add good sample of data , but for KPIs it can run and lets see
  
  2. [nano nets retraining](https://nanonets.com/blog/machine-learning-production-retraining/) very similar to above
  - He gives example of their developed chatbot being used by construction workers on site which adds unexpected noise and trained data is clean samples. same as toll plaza case where we only have ddata from summer
  - How to do retraining
   How much new data should we include for retraining, if distribution changes very frequiently then its better to use all new data, small chunk of old maybe and if distribution doesnt change much good chunk of old data
  - setting a batch training job with kubernetes or jetkins, applying online learning where it makes sense and performance and using batch retraining for most cases.
  - estimate offline how much model needs to be retrained by using a sample of data from another time or all new left out split
  - Examining distributiuon of preicted samples and seeing if they are abnormal in case of intra class distributions or deviation from training data/test data
  - see correlation between features and other model explainability assumptions over time and see if there is any change in it 
  - Can we freeze and train only the last layers, as complete model training is heavy
  - directly deploying after training decision. usually risky but is the way for online learning 
 3.[blog post towards data science](https://towardsdatascience.com/concept-drift-and-model-decay-in-machine-learning-a98a809ea8d4) finally a grammer nazi. concept drift is change in model or modellling assumption so old data neeed to relabelled as well mostly. data drift being newer data tagging and trained on differet things
concept drift can happen when our interpretation of data has changed, for example in 1960 politically correct can be something else altogether to current gen for a sentiment analysis kind of model. drift can be detected through some global scores like F1 score as well. This post is only on concept drift and relabelling complete data is often a difficult task

4. [AWS retraining on new data] if data distribution monotored deviated significantly from training data trigger a retrain(how siignificant and how to measure deviation is the work)
 easier solution to answer those complications is to retrain periodically like montly.

5.[ML mastery](https://machinelearningmastery.com/gentle-introduction-concept-drift-machine-learning/)[2](https://machinelearningmastery.com/machine-learning-qa-concept-drift-better-results-and-learning-faster/) 
  
6.https://www.sas.com/content/dam/SAS/support/en/sas-global-forum-proceedings/2019/3496-2019.pdf and https://www.sas.com/content/dam/SAS/support/en/sas-global-forum-proceedings/2019/3496-2019.pdf(dummy how to use the forecast) 
 - Model retraining depends on many factors like calender fluctuations, business cycles, data drift, model peformance, expected benefits
 - Things tto monitor
 	- Data Drift : change in distribution of data
        - model stability : chnage in distribution of model predictions
        - Model accuracy: if predictionsae availabhle atleast at a later point of time we can see if any change in model accuracy
       - change ibn a variable contribution to model performance
       
- Reasons for model retraining
 - Business strategy : change in the requirements may be change in the acceptablpe level of accuracy or throughput
 - External conditions: availability of new data source or somethiong else 
 - Business performance: change in type of business performance, new evaluations, may n\be new models
 - model monitoring: data drift, model stability or accuracy

 - #### Process for monitoring and retraining of model
  - A timer event to start each cycle based on predefined schedule
  - one timer event to directly start model retraining 
  - one timer event to directly start model monitoring
  - timer event to check availability of new data, if new data is available new monitoring job will be triggered ( may be for data drift ?)
  - Regardless of the source we always want to monitor and log(is it a step, why the authorsd gave it in steps. its more like a philosophy or strategy
  - A KPI measure can trigger a retraining , for example if misclassification accuracy is more than 20%
  - A business strategy might trigge new model training or retrainig of old model
  - new retrained model tested may be by comparing it with champion model(why dont they simply call it the current model) 
  - They give an example of flight data , but on decision treaa nd logistic regression models(as they uise a simulater scenario of fiest model being built on\\in 1987) 
     - so the caution is if we see any data drift, and if we trigger a retrain it can also be that this change is a short term trend and we risk unintended fitting on shorty term trend
	- he also got a surprising result that single model trained on october data perfors better than model 12 models trained on each individual data
	- they went for a strategy of 4 month train and 3 month monitor and claims that as there is a month data in overlap of training data it resulted in smooth change of model performance
	
7. https://www.cs.bham.ac.uk/~minkull/publications/OliveiraEtAlICTAI2017.pdf
 - even this paper says concept drift is data drift(I am starting to feel like having a good lingo is better: lingo nazi)
 - They propose a new method called PMO for concept drift detection(CDT)
 - previous method is Intersection ofconfidence intervals; so this is targets monitoring, so they say detection of change in features as a proxy to detrect change in time series performance which contradicts the idea that this is targets monitoring where this is infact features monitoring
 - he discusses a swarm of models and all agreeing that a concept drift occurs. good reading (which can be time taking) is need to to know how the weights are given to each sample in data and how a swarm is constructed. But this sems to be reduing false postive rate, to start with single model forecasting results to detct concept drift should be decent enough
 - They do friedman's test and nemenyi test for p -values, can these two tests be implemented and use3d for significant tests in DL models
 -  
8.https://apps.dtic.mil/dtic/tr/fulltext/u2/1012527.pdf
 -they habe some method CorEx for determining distribution changes over hisgh dimensional data
 - normalised mean shoudl be same for same distribution(although papaer wont tell this tehy tell some metjod they developed? on ionformation theoru)
 - very big, seems useful though
 -
9 https://blog.valohai.com/cicd-for-machine-learning
 - he had a example of classyfying reddit subreddits
 - he uses P@1 on test set as a measure for model drift
10. https://www.atlantis-press.com/journals/ijcis/25888775/view 
 - drift detetion added to adaptive ensemble learning model
 - in previous work they point out drop in accuracy, Kolmogorov-Smirnov value and KL divergence to detect drift
 - mple datasets on which we can test the retraining scenarious
11. https://hackernoon.com/how-to-keep-your-machine-learning-models-up-to-date-vd5z3yzw
 - more a blog post of hey you need to retrain. see netflix and spotig\fy and develop systems from begioning

12. they have drift score and fugacity score. how to come upo with those especially how fugacity score and how is it different from drift score

13. https://blog.datatron.com/ 
 - K-S test to chek distribution similarity post and pre deployment
 - Population stability index - how a varian\bles distribution changed over time, (can we suse on predictions?)
 - Z-score comparision and having threshold(usually >3)

14 https://www.datarobot.com/blog/all-data-drift-is-not-created-equal-dot-dot-dot/
 - All drifts are not equal, if we monitor changen in every possible variable then number of alerts will be significantloy higher than using feature importance to figure out changes in important features. hence do feature importance
15 . docs.seldon.io shows they have three monitoring alerts based on
   - outlier detection
  - adversarial detection
 - drift detection
   How do they do adversarial detection

16. explaining coincept drift Xiolu wang
 - in reasearch gate need to get access
 - measures difference in distribution of training and predcitions
 - Also for classification in neural nets different filters might correspomd to different classes, carefullook at this should be done to detect any model drift

17. cloud google : MLOPS
 - https://cloud.google.com/solutions/machine-learning/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning
 - a high level overview on ci cd system. a talk in gcloud 2019 meeting added to reference
 
18. https://nms.kcl.ac.uk/guillermo.suarez-tangil/papers/2016aisec.pdf
- Discusses venn abber method for retraining. a weighted confusion matrix based model

19. neptune.ai/blog/concept-drift-best-practices
- F1 score
 - decrease in average classification probability score
 - instance selection to choose new samples which correspond to the distributions
 - ensembels : ensembles generally drift lessd
 - Drop features where AUc ROc svcore is not upt mark
 - checkout creme python library to implement online learning 
 
20 Dont pay for validation: using Margin density
 - not so promising, in research gate check again if usefu;

21 Survey on concept drift: JOAO GAMA
 - https://dl.acm.org/doi/10.1145/2523813
- some examples are interesting other than that same poiunts reiterated

22. https://www.datanami.com/2020/06/16/staying-on-top-of-ml-model-and-data-drift/
- just says its important to have better strategy too than periodic retraininng
- markets their tool domino

23. https://dzone.com/articles/concept-drift-monitoring-model-quality-in-streamin
- a webinar , video on best practices of mmonitoring 

24. azure ml data monitoring
https://docs.microsoft.com/en-us/azure/machine-learning/how-to-monitor-datasets
- drift can be because of change in measurements, in our case change in the frequency value from 1 hour to 15 min intervals
 - data quality issue, some variable having always one value(some glitch)
 - natural drift in the value, like mean value]
 - change in relation between features -- decrease in calculated correlations, model accuracy.
 - azure gives features to detect and alert drift on new data, analyse old data for drift, profile new data over time(custom alerts azure application insights
- some counts like min,max distinct values, distinct value counts etc
- wasserstein distance metric to see difference in distributions

25 https://arxiv.org/pdf/2004.00438.pdf
 - error intersection approach to determine concept drift
 - classification uses classification eror. for regression they suggest two models and slect the best one using error over intersection method , ehere have 2 moidels in pipeline, whichbone is favourable is choosen based on EIA

26. https://storage.googleapis.com/pub-tools-public-publication-data/pdf/45742.pdf
- alerts based on distribution of each feature
- test correlation of eac feature
- have a cost of each feature
- test how 1% increase in accuracy impacts actual value like click rates
- examing some clusters of data(his terminology is data slices)

27https://storage.googleapis.com/pub-tools-public-publication-data/pdf/43146.pdf
