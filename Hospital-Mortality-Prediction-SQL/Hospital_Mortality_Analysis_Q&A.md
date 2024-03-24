# <p align="center">Hospital Mortality Prediction Project</p>

# <p align="center"> ![pic](https://media.istockphoto.com/id/1194838627/vector/patient-in-hospital.jpg?s=612x612&w=0&k=20&c=LqhY8qXr1IgGA0PjGLwqEyVJL-MBTFBU5rf3Dcg4DWo=) </p>

#### **Tools Used**: Excel, MySQL, Tableau

[Dataset Used](https://www.kaggle.com/datasets/mitishaagarwal/patient)

[SQL Analysis (Code) https://github.com/jyoti-1233/SQL_Projects/blob/main/Hospital-Mortality-Prediction-SQL/Hospital_Mortality_SQL_Analysis.sql]


- **Business Problem:** Healthcare professionals are trying to identify the main causes of in-hospital mortality for admitted patients. By having a clear understanding of the causes early on, healthcare professionals will be in a better position to develop targeted interventions, and implement evidence-based protocols to address the factors that contribute to in-hospital patient deaths. 

- **My Appraoch To Solving The Problem:** To tackle the business problem of identifying the main causes of in-hospital mortality for admitted patients, My approach involved obtaining the dataset, importing it into Excel, cleaning the data, then importing it to MySQL and conducting insightful queries to extract valuable information. Using my SQL skills, I delved into the dataset, exploring various patient attributes such as age, ethnicity, gender, weight, BMI, heart rate, and comorbidities. After executing the queries with SQL, I uncovered insightful patterns, trends, and correlations within the data. To present my findings in a visually appealing manner, 



![Query1](https://i.ibb.co/SV4r1Rt/Screen-Shot-2023-06-29-at-4-52-19-PM.png)

Out of the 10,000 admitted patients in the hospital, a total of 634 patients died, which translates to 6.34%. This meant that understanding the factors contributing to in-hospital mortality was highly important in improving patient care and reducing preventable deaths.

2:

![Query2](https://i.ibb.co/XC5qXg8/Screen-Shot-2023-06-29-at-7-44-37-PM.png)

This output showed the amount of patients that died and survived in each age group, categorized by 10-year intervals. There were far more admitted patients between the ages of 50-89 compared to patients who were between 0-49. Observing the results more, we can see that patients between ages 0-9 had the highest death percentage and each 10-year age group in the 50-89 range had a slight increase in death percentage. Nearly 1 in every 6 patients between the ages of 70-89 died in the hospital. 

3:

![Query3](https://i.ibb.co/MnB3M5L/Screen-Shot-2023-06-29-at-7-56-52-PM.png)

This output further proves that the death probability of a patient in the hospital rises as they get older.

4:

![Q4](https://i.ibb.co/54ZBMBH/Screen-Shot-2023-06-29-at-8-08-53-PM.png)

![Q5](https://i.ibb.co/mJB1cxY/Screen-Shot-2023-06-29-at-8-09-28-PM.png)

These two outputs give more insight to the outcomes of patients in each ICU admit source & type. A vast majority of the patients were admitted to the "Accident & Emergency" ICU admit source and it also experienced the highest number of deaths. However, the ICU admit source with the highest probability of death was "Floor" with a percentage of 11.76. "Other ICU" was ignored because of its very small sample size. 

In the second output where death results are shown for each ICU type, there is a clear outlier: Med-Surg ICU

5:

![Q6](https://i.ibb.co/5cCNgyW/Screen-Shot-2023-06-29-at-8-32-29-PM.png)

Average weight, BMI, and max heart rate among the patients that died. 

The average weight of 67.57 kg (149 in lbs) suggests that, on average, the patients who passed away had a relatively moderate weight. The average BMI of 23.3 indicates that, on average, the patients who died had a BMI within the normal range. This suggests that weight alone may not be the sole determinant of mortality, as individuals with a normal BMI can also face significant health risks and complications leading to hospital death. The average maximum heart rate of 115.1 highlights a potential cardiovascular aspect in the patients' health profiles. Elevated heart rates can be indicative of underlying conditions , such as cardiac distress or organ failure, which might have contributed to the hospital mortality outcomes observed.

6: 

![Q7](https://i.ibb.co/GHb3dnT/Screen-Shot-2023-06-29-at-8-48-21-PM.png)

There were a total of 8 comorbidities in the dataset, and the 3 shown in the output results above (Diabetes, Immunosuppression, and Solid Tumor) had the highest probability of death with diabetes being the highest, by far. This highlights the importance of managing and monitoring this condition effectively during hospitalization.

7: 

![Q8](https://i.ibb.co/Tkc9RVr/Screen-Shot-2023-07-01-at-2-56-23-PM.png)

Generally speaking, and as shown by this output, prolonged stays in the ICU are associated with higher mortality rates . An increased length of stay in the ICU can be due to a number of reasons, such as cardiovascular system diseases, nervous system diseases, infections, underlying illnesses, and increased exposure to potential complications According to this output, a patient who stayed in the ICU for longer than a day had a higher chance of death compared to someone who spent less than a day in the ICU. 
