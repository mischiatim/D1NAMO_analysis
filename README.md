# D1NAMO_analysis
An analysis of the D1NAMO dataset of wearable data for healthy and Type 1 diabetic subjects 

# Outline of project goals and deliverables

I am intrigued by the potential of data collected via wearable sensors and smart devices to monitor a user’s health, managing existing medical conditions and possibly detect the onset of new ones. While several datasets from wearable devices are freely available for analysis, very few include medical-grade measurements and subjects with medical conditions in addition to healthy ones. I have chosen to focus on the ‘D1NAMO’ dataset released by researchers in Switzerland, which contains 1550hrs of data collected from a mix of healthy and Type 1 Diabetic (D1) subjects wearing a chest-worn bioharness. The data collected from this device include ECG traces at 250Hz, ‘Breathing’ traces from a pressure sensor at 18Hz and acceleration traces at 100Hz. This dataset contains medical-grade measurements of glucose for both cohorts, either manually collected before and after every meal for healthy subjects or monitored every 5 minutes for D1 subjects via a Continuous Glucose Monitoring (CGM) device. It also includes detailed information on the meals consumed by each subject (calories, balance and quality as assessed by a dietologist) and, specifically for the D1 cohort, the dosage of insulin medication. It is well known that physical activity, food consumption, physiological signals and glucose level in the blood are all related to each other, but not all their relationships have been investigated in equal depth or have been exploited in wearable technology. In this project I will investigate 4 types of relationships.

# 1) Relationship between physical activity and physiological signals
 
The relationship between physical activity and cardiovascular function is obviously a strong and well-studied one, and one that has been exploited in many recent consumer wearables, which can measure heart rate or ECG activity. Measurement of breathing signals in wearables, on the other hand, is less common. The D1NAMO dataset can be used to compare the information contained in breathing signals to the heart rate and ECG signals, and assess how all these signals depend on physical activity. 

Deliverables: 
-	Models for predicting the effect of physical movement (acceleration) on physiological signals (breathing rate, heart rate and more detailed ECG features) for healthy and D1 subjects
-	Comparison of the model parameters between the 2 cohorts: are physiological signals in D1 subjects (even if under medication) more sensitive to physical activity?

# 2) Relationship between food consumption (including meal size & quality) and physiological signals 

It is also known that there are physiological changes after consumption of a meal. For example, heart rate has been observed to start changing after a meal, with a peak around 30-60mins after end of the meal and the effect disappearing 2 hours afterwards. These changes depend on the meal size and quality. The D1NAMO dataset includes detailed labeled information of meal quantity and quality in addition to the continuously monitored physiological signals. It is thus an ideal dataset to investigate whether (and which) physiological signals also reflect meal consumption in addition to physical activity. If that is true, another interesting question is whether the relationship between food consumption and physiological signals (heart rate, ECG, breathing) is consistently different in D1 subjects compared to healthy ones even when under insulin medication. 
If the relationship between food consumption and physiological signals is strong enough, it could be possible to design a machine learning algorithm that detects when a meal has been consumed by the user, and perhaps estimates the size and quality of the meal consumed. This is going to be a hard task, as the food-dependent signals will be presumably hidden within the stronger fluctuations due to activity level and other factors. However, if achieved, this goal would open the door to novel wearable applications (e.g. a wearable could inform the user that a heavy meal has been consumed). 

Deliverables:
-	Models for predicting the effect of food consumption (in addition to acceleration) on physiological signals for healthy and D1 subjects, and comparison between the 2 cohorts
-	A model for estimating whether a meal has been consumed (and perhaps its size and quality) from trends in the physiological signals (heart rate, perhaps also breathing or ECG)  
# 3) Relationship between food consumption, activity level, insulin dosage and glucose level in the blood

This relationship is of course well studied in diabetes research as it informs the decisions that healthcare professionals and D1 patients make every day. For example, patients choose their insulin dosage at mealtime based on the predicted effect of their food consumption on their future glucose levels. While some patients wear Continuous Glucose Monitoring devices providing them frequent feedback on the outcome of their decisions, the majority of D1 patients do not have access to their glucose levels in-between manual measurements. I will attempt to learn a model that predicts the future evolution of glucose from the current glucose level, the meal being consumed, the chosen insulin dosage and the level of physical activity (acceleration) planned between manual measurements. Such a model could be used to compute an optimal control policy that suggests to the user the optimal insulin dosage to maximize the time in the ‘safe glucose zone’ between measurements.

Deliverables: 
-	A model for predicting future glucose levels (or at least the average time in the safe zone in the next window of time) based only on the previous glucose level, the meal being consumed, the insulin dosage taken and the level of physical activity (acceleration) planned in the near future.  
-	An algorithm based on the model above that suggests the optimal insulin dosage    

# 4) Relationship between glucose levels in the blood and physiological signals 
It is known that glucose levels – or at least the dangerous lows associated with hypoglycemic events – can be detected from features of the ECG signal (ST-segment changes, T-wave amplitude changes, length of QTc interval). In fact, the motivation behind the collection of the D1NAMO dataset was to enable the study of algorithms capable of predicting glucose levels from ECG or other physiological signals alone (for patients without CGM). I propose to investigate the use of ECG features (or some of the other physiological signals) as noisy measurements of the true glucose level, that could be combined in Bayesian fashion (a la Kalman filter) with the open-loop predictions of future glucose level yielded by the model described above.  This model could be used in wearables for improving prediction of future glucose levels for patients without continuous glucose monitoring.

Deliverables:
-	A Bayesian estimator of current glucose level based on physiological measurements and the open-loop prediction of future glucose levels derived in 3)
