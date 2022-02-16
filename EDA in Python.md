Predicting now if the Falcon 9 first stage will land successfully. SpaceX advertises Falcon 9 rocket launches on its website with a cost of 62 million dollars; other providers cost upward of 165 million dollars each, much of the savings is due to the fact that SpaceX can reuse the first stage.

Falcon 9 first stage will land successfully

Most unsuccessful landings are planned. Space X performs a controlled landing in the oceans.

Objectives:
Perform exploratory Data Analysis and Feature Engineering using Pandas and Matplotlib


```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
df=pd.read_csv("https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/datasets/dataset_part_2.csv")

# If you were unable to complete the previous lab correctly you can uncomment and load this csv

df = pd.read_csv('https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DS0701EN-SkillsNetwork/api/dataset_part_2.csv')

df.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FlightNumber</th>
      <th>Date</th>
      <th>BoosterVersion</th>
      <th>PayloadMass</th>
      <th>Orbit</th>
      <th>LaunchSite</th>
      <th>Outcome</th>
      <th>Flights</th>
      <th>GridFins</th>
      <th>Reused</th>
      <th>Legs</th>
      <th>LandingPad</th>
      <th>Block</th>
      <th>ReusedCount</th>
      <th>Serial</th>
      <th>Longitude</th>
      <th>Latitude</th>
      <th>Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2010-06-04</td>
      <td>Falcon 9</td>
      <td>6104.959412</td>
      <td>LEO</td>
      <td>CCAFS SLC 40</td>
      <td>None None</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0</td>
      <td>B0003</td>
      <td>-80.577366</td>
      <td>28.561857</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2012-05-22</td>
      <td>Falcon 9</td>
      <td>525.000000</td>
      <td>LEO</td>
      <td>CCAFS SLC 40</td>
      <td>None None</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0</td>
      <td>B0005</td>
      <td>-80.577366</td>
      <td>28.561857</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2013-03-01</td>
      <td>Falcon 9</td>
      <td>677.000000</td>
      <td>ISS</td>
      <td>CCAFS SLC 40</td>
      <td>None None</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0</td>
      <td>B0007</td>
      <td>-80.577366</td>
      <td>28.561857</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2013-09-29</td>
      <td>Falcon 9</td>
      <td>500.000000</td>
      <td>PO</td>
      <td>VAFB SLC 4E</td>
      <td>False Ocean</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0</td>
      <td>B1003</td>
      <td>-120.610829</td>
      <td>34.632093</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2013-12-03</td>
      <td>Falcon 9</td>
      <td>3170.000000</td>
      <td>GTO</td>
      <td>CCAFS SLC 40</td>
      <td>None None</td>
      <td>1</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>0</td>
      <td>B1004</td>
      <td>-80.577366</td>
      <td>28.561857</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
##We can plot out the FlightNumber vs. PayloadMassand overlay the outcome of the launch.
##We see that as the flight number increases, the first stage is more likely to land successfully. 
##The payload mass is also important; it seems the more massive the payload, the less likely the first stage will return.

sns.catplot(y="PayloadMass", x="FlightNumber", hue="Class", data=df, aspect = 5)
plt.xlabel("Flight Number",fontsize=20)
plt.ylabel("Pay load Mass (kg)",fontsize=20)
plt.show()
```


    
![png](output_3_0.png)
    



```python
##There can be watched that different launch sites have different success rates. CCAFS LC-40, has a success rate of 60 %, 
##while KSC LC-39A and VAFB SLC 4E has a success rate of 77%.

```

TASK 1: Visualize the relationship between Flight Number and Launch Site
Use the function catplot to plot FlightNumber vs LaunchSite, set the parameter x parameter to FlightNumber,set the y to Launch Site and set the parameter hue to 'class'TASK 


```python
# Plot a scatter point chart with x axis to be Flight Number and y axis to be the launch site, and hue to be the class value
sns.catplot(y="LaunchSite", x="FlightNumber", hue="Class", data=df, aspect = 5)
plt.xlabel("Flight Number",fontsize=20)
plt.ylabel("Launch Site",fontsize=20)
plt.show()
```


    
![png](output_6_0.png)
    


TASK 2: Visualize the relationship between Payload and Launch Site
We also want to observe if there is any relationship between launch sites and their payload mass.


```python
# Plot a scatter point chart with x axis to be Pay Load Mass (kg) and y axis to be the launch site, and hue to be the class value
sns.catplot(y="PayloadMass", x="LaunchSite", hue="Class", data=df, aspect = 5)
plt.xlabel("Launch Site",fontsize=20)
plt.ylabel("Pay load Mass (kg)",fontsize=20)
plt.show()
```


    
![png](output_8_0.png)
    


TASK 3: Visualize the relationship between success rate of each orbit type
Next, we want to visually check if there are any relationship between success rate and orbit type.

Let's create a bar chart for the sucess rate of each orbit


```python
# HINT use groupby method on Orbit column and get the mean of Class column
temp = df.groupby(["Orbit"]).mean().reset_index()
temp2 = temp[["Orbit", "Class"]]
temp2["Class"] = temp2["Class"]*100
sns.barplot(x = "Orbit", y = "Class", data = temp2)
```

    <ipython-input-8-7e88f588b437>:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      temp2["Class"] = temp2["Class"]*100
    




    <AxesSubplot:xlabel='Orbit', ylabel='Class'>




    
![png](output_10_2.png)
    


TASK 4: Visualize the relationship between FlightNumber and Orbit type
For each orbit, we want to see if there is any relationship between FlightNumber and Orbit type.


```python
# Plot a scatter point chart with x axis to be FlightNumber and y axis to be the Orbit, and hue to be the class value
sns.catplot(y="Orbit", x="FlightNumber", hue="Class", data=df, aspect = 5)
plt.xlabel("FlightNumber",fontsize=20)
plt.ylabel("Orbit",fontsize=20)
plt.show()
```


    
![png](output_12_0.png)
    



```python
##Clearly, in the LEO orbit the Success appears related to the number of flights; on the other hand, 
##there seems to be no relationship between flight number when in GTO orbit
```

TASK 5: Visualize the relationship between Payload and Orbit type
Similarly, we can plot the Payload vs. Orbit scatter point charts to reveal the relationship between Payload and Orbit typeTASK 5: Visualize the relationship between Payload and Orbit type



```python
# Plot a scatter point chart with x axis to be Payload and y axis to be the Orbit, and hue to be the class value
sns.catplot(y="Orbit", x="PayloadMass", hue="Class", data=df, aspect = 5)
plt.xlabel("PayloadMass",fontsize=20)
plt.ylabel("Orbit",fontsize=20)
plt.show()
```


    
![png](output_15_0.png)
    



```python
## Obviously, Heavy payloads have a negative influence on GTO orbits and positive on GTO and Polar LEO (ISS) orbits.
```

TASK 6: Visualize the launch success yearly trend
You can plot a line chart with x axis to be Year and y axis to be average success rate, to get the average launch success trend.


```python
# A function to Extract years from the date 
year=[]
def Extract_year(date):
    for i in df["Date"]:
        year.append(i.split("-")[0])
    return year
    
# Plot a line chart with x axis to be the extracted year and y axis to be the success rate
year = []
df["year"] = Extract_year(year)
df["Success Rate"] = df["Class"] * 100
sns.lineplot(data = df, x = "year", y = "Success Rate")
```




    <AxesSubplot:xlabel='year', ylabel='Success Rate'>




    
![png](output_18_1.png)
    



```python
##There can be observed it is an ongoing trend in success rate since 2013 until 2020
```


```python

```
