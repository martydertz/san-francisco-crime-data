import math
import os
import numpy as np
import pandas as pd

os.chdir('C:\Datasets')
crime=pd.read_csv("crime_train2.csv")
crime['Dates']=pd.to_datetime(crime['Dates'])
crime['Hour']=crime.Dates.apply(lambda x: x.hour)
crime['Month']=crime.Dates.apply(lambda x: x.month)
i=0

# create dictionary of prior probabilities for each category using freqency of 
# each category divided by the number of crimes in frame
prior={}
for item in crime['Category'].value_counts().iteritems():
    count= float(item[1])
    prior[item[0]]=count

# create counts dictionary to store frequencies for each column value for each
# categorical variable
counts={}
# start with 3 keys for each category key
for item in crime['Category'].unique():
    counts[item]={}
    for i in range(1,4):
        counts[item][i]={}
# add each unique value for each column        
for key in counts:
    for dist in crime['PdDistrict'].unique():
        counts[key][1][dist]=0
    for hour in crime['Hour'].unique():
        counts[key][2][hour]=0
    for month in crime['Month'].unique():
        counts[key][3][month]=0
# count frequencies 
for index, row in crime.iterrows():
    cat=row['Category']
    hour = row['Hour']
    dist= row['PdDistrict']
    month=row['Month']    
    counts[cat][1][dist]+=1
    counts[cat][2][hour]+=1
    counts[cat][3][month]+=1
conditional={}
for cat,cols in counts.items():
    conditional.setdefault(cat, {})
    for col, vals in cols.items():
        conditional[cat].setdefault(col, {})
        for attr,cnt in vals.items():
            conditional[cat][col].setdefault(attr,{})
            conditional[cat][col][attr]= float(cnt)/prior[cat]

# Define funtion that takes prior, conditionals probabilitites and
# a feature vecture and returns the most likely category using bayes
def classify(condProbs, priorProbs, featureVector):
    results =[]
    for cat,prior in priorProbs.items():
        prob=prior
        col=1
        for feature in featureVector:
            if not feature in condProbs[cat][col].items():
                prob=0
            else:
                prob=prob*condProbs[cat][col][feature]
        results.append((prob,cat))
    return(max(results)[1])
