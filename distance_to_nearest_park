import math
import os
import numpy as np
import pprint as pp
import pandas as pd
os.chdir("C:\Datasets")

crime=pd.read_csv("crime_train.csv")
parks=pd.read_csv("Recreation___Park_Department_Park_Info_Dataset.csv")

def dist(loc1, loc2):
    R=6372.8 # Earth radius (KM)
    lat1=math.radians(loc1[0])
    lat2=math.radians(loc2[0])
    
    dLon=math.radians(loc1[1]-loc2[1])
    dLat=math.radians(loc1[0]-loc2[0])
    
    a=(math.sin(dLat/2))**2 + (math.cos(lat1))*(math.cos(lat2))*(math.sin(dLon/2))**2
    c=2*math.asin(math.sqrt(a))
    return R*c
  
def find_nearest(location,locations):
    global dist
    nearest=float('inf')
    
    for loc in locations:
        d=dist(loc,location)
        if d<nearest:
            nearest=d
    return nearest

crime["location"]=zip(crime.X, crime.Y)
parkLocations=[]

c=1
for index,park in parks.iterrows():
    if str(park['Location 1']) != 'nan':
        loc=park['Location 1']
    else:
        loc=str(park['ParkName'])+"+"+str(park['Zipcode'])
    print "index eqls " + str(index)
    query_params={'key':key}   
    response=req.get(url+"+"+loc, params=query_params)
    data=response.json()
    park_lat= data['results'][0]['geometry']['location']['lat']
    park_lng= data['results'][0]['geometry']['location']['lng']
    park_location=tuple([park_lat,park_lng])
    parkLocations.append(park_location)
    
    print "park lat/lng indx " +str(c)+" location = " +str(park_location)
    c+=1
print "end api loop"
for i,j in crime.iterrows():
    crime_loc=j['location']
    dist_to_park=find_nearest(crime_loc,parkLocations)
    crime.set_value(i,'DistToPark',dist_to_park)
    print "dist to_closest_park =" + str(dist_to_park) +" park -" +str(c)
    c+=1
print "end dist loop"
crime.to_csv("crime_train.csv")
