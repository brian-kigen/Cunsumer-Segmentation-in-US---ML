### DATA CODE BOOK

[Data Dictionary](https://sda.berkeley.edu/sdaweb/docs/scfcomb2019/DOC/hcbk0001.htm#AGE)

# Reading dataset


```python
#pip install seaborn
```


```python
#pip install matplotlib
```


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

```


```python
df = pd.read_csv("./scfp2022excel/SCFP2022.csv")
```


```python
df.head()
#print(df.shape)
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
      <th>YY1</th>
      <th>Y1</th>
      <th>WGT</th>
      <th>HHSEX</th>
      <th>AGE</th>
      <th>AGECL</th>
      <th>EDUC</th>
      <th>EDCL</th>
      <th>MARRIED</th>
      <th>KIDS</th>
      <th>...</th>
      <th>NWCAT</th>
      <th>INCCAT</th>
      <th>ASSETCAT</th>
      <th>NINCCAT</th>
      <th>NINC2CAT</th>
      <th>NWPCTLECAT</th>
      <th>INCPCTLECAT</th>
      <th>NINCPCTLECAT</th>
      <th>INCQRTCAT</th>
      <th>NINCQRTCAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>11</td>
      <td>3027.956120</td>
      <td>2</td>
      <td>70</td>
      <td>5</td>
      <td>9</td>
      <td>3</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>4</td>
      <td>2</td>
      <td>4</td>
      <td>2</td>
      <td>1</td>
      <td>8</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>12</td>
      <td>3054.900065</td>
      <td>2</td>
      <td>70</td>
      <td>5</td>
      <td>9</td>
      <td>3</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>4</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>1</td>
      <td>8</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>13</td>
      <td>3163.637766</td>
      <td>2</td>
      <td>70</td>
      <td>5</td>
      <td>9</td>
      <td>3</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>4</td>
      <td>2</td>
      <td>4</td>
      <td>2</td>
      <td>1</td>
      <td>8</td>
      <td>3</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>14</td>
      <td>3166.228463</td>
      <td>2</td>
      <td>70</td>
      <td>5</td>
      <td>9</td>
      <td>3</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>2</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>6</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>15</td>
      <td>3235.624715</td>
      <td>2</td>
      <td>70</td>
      <td>5</td>
      <td>9</td>
      <td>3</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>3</td>
      <td>2</td>
      <td>4</td>
      <td>2</td>
      <td>1</td>
      <td>8</td>
      <td>3</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 356 columns</p>
</div>



##### 

One of the first things you might notice here is that this dataset is HUGE — over 20,000 rows and 356 columns! SO MUCH DATA!!! We won't have time to explore all of the features in this dataset, but you can look in the data dictionary for this project for details and links to the official Code Book. For now, let's just say that this dataset tracks all sorts of behaviors relating to the ways households earn, save, and spend money in the United States.

For this project, we're going to focus on households that have "been turned down for credit or feared being denied credit in the past 5 years." These households are identified in the "TURNFEAR" columnumn.



## Exploration Data Analysis

#### 
Here we will subset to households which have been feared to been turned down or feared being turned down for credit ("TURNFEAR" == 1) and assign this subset to the variable name df_fear.


```python
mask = df["TURNFEAR"] ==1
mask.sum()
```




    3839




```python
mask = df["TURNFEAR"] ==1
df_fear = df[mask]
print("df_fear type:", type(df_fear))
print("df_fear shape:", df_fear.shape)
df_fear.head()
```

    df_fear type: <class 'pandas.core.frame.DataFrame'>
    df_fear shape: (3839, 356)
    




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
      <th>YY1</th>
      <th>Y1</th>
      <th>WGT</th>
      <th>HHSEX</th>
      <th>AGE</th>
      <th>AGECL</th>
      <th>EDUC</th>
      <th>EDCL</th>
      <th>MARRIED</th>
      <th>KIDS</th>
      <th>...</th>
      <th>NWCAT</th>
      <th>INCCAT</th>
      <th>ASSETCAT</th>
      <th>NINCCAT</th>
      <th>NINC2CAT</th>
      <th>NWPCTLECAT</th>
      <th>INCPCTLECAT</th>
      <th>NINCPCTLECAT</th>
      <th>INCQRTCAT</th>
      <th>NINCQRTCAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>5</td>
      <td>51</td>
      <td>7191.481109</td>
      <td>2</td>
      <td>19</td>
      <td>1</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>4</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>21</th>
      <td>5</td>
      <td>52</td>
      <td>7352.487205</td>
      <td>2</td>
      <td>19</td>
      <td>1</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>4</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>22</th>
      <td>5</td>
      <td>53</td>
      <td>7270.703541</td>
      <td>2</td>
      <td>19</td>
      <td>1</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>5</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>23</th>
      <td>5</td>
      <td>54</td>
      <td>7383.866597</td>
      <td>2</td>
      <td>19</td>
      <td>1</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>5</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>24</th>
      <td>5</td>
      <td>55</td>
      <td>7330.537669</td>
      <td>2</td>
      <td>19</td>
      <td>1</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>4</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 356 columns</p>
</div>



### AGE

##### Now that we have our subset, let's explore the characteristics of this group. One of the features is age group ("AGECL").


```python
age_groups = df_fear["AGECL"].unique()
print("Age Groups:", age_groups)
```

    Age Groups: [1 4 2 3 5 6]
    


```python
agecl_dict = {
    1: "Under 35",
    2: "35-44",
    3: "45-54",
    4: "55-64",
    5: "65-74",
    6: "75 or Older",
}

age_cl = df_fear["AGECL"].replace(agecl_dict)
print("age_cl type:", type(age_cl))
print("age_cl shape:", age_cl.shape)
age_cl.head(10)
```

    age_cl type: <class 'pandas.core.series.Series'>
    age_cl shape: (3839,)
    




    20     Under 35
    21     Under 35
    22     Under 35
    23     Under 35
    24     Under 35
    110       55-64
    111       55-64
    112       55-64
    113       55-64
    114       55-64
    Name: AGECL, dtype: object




```python
age_cl_value_counts = age_cl.value_counts()
# Bar plot of `age_cl_value_counts`
age_cl_value_counts.plot(kind = "bar", 
                         xlabel= "Age Groups", 
                         ylabel = "Frequencies (counts)", 
                         title = "Gredit Fearful : Age Groups")
```




    <Axes: title={'center': 'Gredit Fearful : Age Groups'}, xlabel='Age Groups', ylabel='Frequencies (counts)'>




    
![png](output_16_1.png)
    


####  
Our chart is telling us that many of the people who fear being denied credit are younger. But the first two age groups cover a wider range than the other four. So it might be useful to look inside those values to get a more granular understanding of the data.

To do that, we'll need to look at a different variable: "AGE". Whereas "AGECL" was a categorical variable, "AGE" is continuous, so we can use it to make a histogram of our own.


```python
# Plot histogram of "AGE"
df_fear["AGE"].hist(bins=10)
plt.xlabel("Age")
plt.ylabel("Frequencies (count)")
plt.title("Credit Fearful: Age Distribution")

# Show the plot
plt.show()

```


    
![png](output_18_0.png)
    


####
From our chart above, it looks like younger people are still more concerned about being able to secure a loan than older people, but the people who are most concerned seem to be between 30 and 40.

### INCOME

#### 
Lets explore the income level. Are people with lower incomes concerned about being denied credit, or is that something people with more money worry about? In order to answer that question, we'll need to again compare the entire dataset with our subgroup using the "INCCAT" feature, which captures income percentile groups. This time, though, we'll make a single, side-by-side bar chart

####
We will create a DataFrame df_inccat that shows the normalized frequency for income categories for both the credit fearful and non-credit fearful households in the dataset.


```python
inccat_dict = {
    1: "0-20",
    2: "21-39.9",
    3: "40-59.9",
    4: "60-79.9",
    5: "80-89.9",
    6: "90-100",
}

df_inccat = df["INCCAT"].replace(inccat_dict).groupby(df["TURNFEAR"]).value_counts(normalize =True).rename("FREQUENCY").to_frame().reset_index()
                            

print("df_inccat type:", type(df_inccat))
print("df_inccat shape:", df_inccat.shape)
df_inccat
```

    df_inccat type: <class 'pandas.core.frame.DataFrame'>
    df_inccat shape: (12, 3)
    




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
      <th>TURNFEAR</th>
      <th>INCCAT</th>
      <th>FREQUENCY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>90-100</td>
      <td>0.303982</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>60-79.9</td>
      <td>0.162312</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>40-59.9</td>
      <td>0.144492</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0-20</td>
      <td>0.140050</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>21-39.9</td>
      <td>0.139162</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>80-89.9</td>
      <td>0.110002</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>0-20</td>
      <td>0.340714</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>21-39.9</td>
      <td>0.266476</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>40-59.9</td>
      <td>0.205001</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>60-79.9</td>
      <td>0.112529</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>80-89.9</td>
      <td>0.041417</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>90-100</td>
      <td>0.033863</td>
    </tr>
  </tbody>
</table>
</div>



####
Using seaborn, we will create a side-by-side bar chart of df_inccat. Set hue to "TURNFEAR", and make sure that the income categories are in the correct order along the x-axis. We label the x-axis "Income Category", the y-axis "Frequency (%)", and use the title "Income Distribution: Credit Fearful vs. Non-fearful"


```python
# Create bar chart of `df_inccat`
sns.barplot(x="INCCAT",
            y= "FREQUENCY", 
            hue = "TURNFEAR",
            data = df_inccat,
            order=inccat_dict.values())
plt.xlabel("Income Category")
plt.ylabel("Frequency (%)")
plt.title("Income Distribution: Credit Fearful vs. Non-fearful");
```


    
![png](output_25_0.png)
    


####
Comparing the income categories across the fearful and non-fearful groups, we can see that credit fearful households are much more common in the lower income categories. In other words, the credit fearful have lower incomes.

So, based on all this, what do we know? Among the people who responded that they were indeed worried about being approved for credit after having been denied in the past five years, a plurality of the young and low-income had the highest number of respondents. That makes sense, right? Young people tend to make less money and rely more heavily on credit to get their lives off the ground, so having been denied credit makes them more anxious about the future.

### RACE

   ####
Now that we have an understanding of how age and income relate to our outcome of interest, let's try some other possibilities, starting with race. And if we look at the Code Book for "RACE", we can see that there are 4 categories.

If you observe from the code book -race, there's no 4 category here. If a value for 4 did exist, it would be reasonable to assign it to "Asian American / Pacific Islander" — a group that doesn't seem to be represented in the dataset. This is a strange omission, but you'll often find that large public datasets have these sorts of issues. The important thing is to always read the data dictionary carefully. In this case, remember that this dataset doesn't provide a complete picture of race in America — something that you'd have to explain to anyone interested in your analysis.

#### 
Lets create a horizontal bar chart showing the normalized value counts for "RACE". In your chart, you should replace the numerical values with the true group names. Be sure to label the x-axis "Frequency (%)", the y-axis "Race", and use the title "Credit Fearful: Racial Groups". Finally, set the xlim for this plot to (0,1).


```python
race_dict = {
    1: "White/Non-Hispanic",
    2: "Black/African-American",
    3: "Hispanic",
    5: "Other",
}
race = df_fear["RACE"].replace(race_dict)
race_value_counts = race.value_counts(normalize=True)
# Create bar chart of race_value_counts
race_value_counts.plot(kind= "barh")
plt.xlim((0, 1))
plt.xlabel("Frequency (%)")
plt.ylabel("Race")
plt.title("Credit Fearful: Racial Groups");
```


    
![png](output_30_0.png)
    


####
This suggests that White/Non-Hispanic people worry more about being denied credit, but thinking critically about what we're seeing, that might be because there are more White/Non-Hispanic in the population of the United States than there are other racial groups, and the sample for this survey was specifically drawn to be representative of the population as a whole.

Let's recreate the horizontal bar chart we just made, but this time we use the entire dataset df instead of the subset df_fear. The title of this plot should be "SCF Respondents: Racial Groups". 



```python
race = df["RACE"]
race_value_counts = race.value_counts(normalize=True)
# Create bar chart of race_value_counts
race_value_counts.plot(kind = "barh")
plt.xlim((0, 1))
plt.xlabel("Frequency (%)")
plt.ylabel("Race")
plt.title("SCF Respondents: Racial Groups");
```


    
![png](output_32_0.png)
    


####
How does this second bar chart change our perception of the first one? On the one hand, we can see that White Non-Hispanics account for around 60% of whole dataset, but only around 40% of credit fearful respondents. On the other hand, Black and Hispanic respondents represent 18% of the whole dataset but 35% of credit fearful respondents. In other words, Black and Hispanic households are actually more likely to be in the credit fearful group.

### ASSETS

####
Not all the data is demographic, though. If we were working for a bank, we would probably care less about how old the people are, and more about their ability to carry more debt. If we were going to build a model for that, we'd want to establish some relationships among the variables, and making some correlation matrices is a good place to start.

First, let's zoom out a little bit. We've been looking at only the people who answered "yes" when the survey asked about `"TURNFEAR"`, but what if we looked at everyone instead? To begin with, let's bring in a clear dataset and run a single correlatio

Lets calculate the correlation coefficient for "ASSET" and "HOUSES" in the whole dataset df.n.


```python
asset_house_corr = df["ASSET"].corr(df["HOUSES"])
print("SCF: Asset Houses Correlation:", asset_house_corr)
```

    SCF: Asset Houses Correlation: 0.561776546509548
    

#### 
That's a moderate positive correlation, which we would probably expect, right? For many Americans, the value of their primary residence makes up most of the value of their total assets. What about the people in our TURNFEAR subset, though? Let's run that correlation to see if there's a difference.

Lets now calculate the correlation coefficient for "ASSET" and "HOUSES" in the whole credit-fearful subset df_fear.


```python
asset_house_corr = df_fear["ASSET"].corr(df_fear["HOUSES"])
print("Credit Fearful: Asset Houses Correlation:", asset_house_corr)
```

    Credit Fearful: Asset Houses Correlation: 0.3649545427641164
    

####
Let's again make correlation matrices using the rest of the data for both df and df_fear and see if the differences persist. Here, we'll look at only 5 features: "ASSET", "HOUSES", "INCOME", "DEBT", and "EDUC".


```python
cols = ["ASSET", "HOUSES", "INCOME", "DEBT", "EDUC"]
corr = df[cols].corr()
corr.style.background_gradient(axis=None)
```




<style type="text/css">
#T_8534b_row0_col0, #T_8534b_row1_col1, #T_8534b_row2_col2, #T_8534b_row3_col3, #T_8534b_row4_col4 {
  background-color: #023858;
  color: #f1f1f1;
}
#T_8534b_row0_col1, #T_8534b_row1_col0 {
  background-color: #69a5cc;
  color: #f1f1f1;
}
#T_8534b_row0_col2, #T_8534b_row2_col0 {
  background-color: #2182b9;
  color: #f1f1f1;
}
#T_8534b_row0_col3, #T_8534b_row2_col3, #T_8534b_row3_col0, #T_8534b_row3_col2 {
  background-color: #d2d3e7;
  color: #000000;
}
#T_8534b_row0_col4, #T_8534b_row4_col0 {
  background-color: #faf2f8;
  color: #000000;
}
#T_8534b_row1_col2, #T_8534b_row2_col1 {
  background-color: #b7c5df;
  color: #000000;
}
#T_8534b_row1_col3, #T_8534b_row3_col1 {
  background-color: #e0dded;
  color: #000000;
}
#T_8534b_row1_col4, #T_8534b_row4_col1 {
  background-color: #efe9f3;
  color: #000000;
}
#T_8534b_row2_col4, #T_8534b_row4_col2 {
  background-color: #fef6fa;
  color: #000000;
}
#T_8534b_row3_col4, #T_8534b_row4_col3 {
  background-color: #fff7fb;
  color: #000000;
}
</style>
<table id="T_8534b">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th id="T_8534b_level0_col0" class="col_heading level0 col0" >ASSET</th>
      <th id="T_8534b_level0_col1" class="col_heading level0 col1" >HOUSES</th>
      <th id="T_8534b_level0_col2" class="col_heading level0 col2" >INCOME</th>
      <th id="T_8534b_level0_col3" class="col_heading level0 col3" >DEBT</th>
      <th id="T_8534b_level0_col4" class="col_heading level0 col4" >EDUC</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_8534b_level0_row0" class="row_heading level0 row0" >ASSET</th>
      <td id="T_8534b_row0_col0" class="data row0 col0" >1.000000</td>
      <td id="T_8534b_row0_col1" class="data row0 col1" >0.561777</td>
      <td id="T_8534b_row0_col2" class="data row0 col2" >0.706685</td>
      <td id="T_8534b_row0_col3" class="data row0 col3" >0.307143</td>
      <td id="T_8534b_row0_col4" class="data row0 col4" >0.120139</td>
    </tr>
    <tr>
      <th id="T_8534b_level0_row1" class="row_heading level0 row1" >HOUSES</th>
      <td id="T_8534b_row1_col0" class="data row1 col0" >0.561777</td>
      <td id="T_8534b_row1_col1" class="data row1 col1" >1.000000</td>
      <td id="T_8534b_row1_col2" class="data row1 col2" >0.384699</td>
      <td id="T_8534b_row1_col3" class="data row1 col3" >0.251876</td>
      <td id="T_8534b_row1_col4" class="data row1 col4" >0.186120</td>
    </tr>
    <tr>
      <th id="T_8534b_level0_row2" class="row_heading level0 row2" >INCOME</th>
      <td id="T_8534b_row2_col0" class="data row2 col0" >0.706685</td>
      <td id="T_8534b_row2_col1" class="data row2 col1" >0.384699</td>
      <td id="T_8534b_row2_col2" class="data row2 col2" >1.000000</td>
      <td id="T_8534b_row2_col3" class="data row2 col3" >0.306534</td>
      <td id="T_8534b_row2_col4" class="data row2 col4" >0.096549</td>
    </tr>
    <tr>
      <th id="T_8534b_level0_row3" class="row_heading level0 row3" >DEBT</th>
      <td id="T_8534b_row3_col0" class="data row3 col0" >0.307143</td>
      <td id="T_8534b_row3_col1" class="data row3 col1" >0.251876</td>
      <td id="T_8534b_row3_col2" class="data row3 col2" >0.306534</td>
      <td id="T_8534b_row3_col3" class="data row3 col3" >1.000000</td>
      <td id="T_8534b_row3_col4" class="data row3 col4" >0.086561</td>
    </tr>
    <tr>
      <th id="T_8534b_level0_row4" class="row_heading level0 row4" >EDUC</th>
      <td id="T_8534b_row4_col0" class="data row4 col0" >0.120139</td>
      <td id="T_8534b_row4_col1" class="data row4 col1" >0.186120</td>
      <td id="T_8534b_row4_col2" class="data row4 col2" >0.096549</td>
      <td id="T_8534b_row4_col3" class="data row4 col3" >0.086561</td>
      <td id="T_8534b_row4_col4" class="data row4 col4" >1.000000</td>
    </tr>
  </tbody>
</table>




####
Correlation matrix using `df_fear'.


```python
cols = ["ASSET", "HOUSES", "INCOME", "DEBT", "EDUC"]

corr = df_fear[cols].corr()
corr.style.background_gradient(axis=None)
```




<style type="text/css">
#T_9dba0_row0_col0, #T_9dba0_row1_col1, #T_9dba0_row2_col2, #T_9dba0_row3_col3, #T_9dba0_row4_col4 {
  background-color: #023858;
  color: #f1f1f1;
}
#T_9dba0_row0_col1, #T_9dba0_row1_col0 {
  background-color: #c4cbe3;
  color: #000000;
}
#T_9dba0_row0_col2, #T_9dba0_row2_col0 {
  background-color: #04588a;
  color: #f1f1f1;
}
#T_9dba0_row0_col3, #T_9dba0_row3_col0 {
  background-color: #97b7d7;
  color: #000000;
}
#T_9dba0_row0_col4, #T_9dba0_row2_col4, #T_9dba0_row4_col0, #T_9dba0_row4_col2 {
  background-color: #fff7fb;
  color: #000000;
}
#T_9dba0_row1_col2, #T_9dba0_row2_col1 {
  background-color: #d4d4e8;
  color: #000000;
}
#T_9dba0_row1_col3, #T_9dba0_row3_col1 {
  background-color: #308cbe;
  color: #f1f1f1;
}
#T_9dba0_row1_col4, #T_9dba0_row4_col1 {
  background-color: #f1ebf4;
  color: #000000;
}
#T_9dba0_row2_col3, #T_9dba0_row3_col2 {
  background-color: #a1bbda;
  color: #000000;
}
#T_9dba0_row3_col4, #T_9dba0_row4_col3 {
  background-color: #f2ecf5;
  color: #000000;
}
</style>
<table id="T_9dba0">
  <thead>
    <tr>
      <th class="blank level0" >&nbsp;</th>
      <th id="T_9dba0_level0_col0" class="col_heading level0 col0" >ASSET</th>
      <th id="T_9dba0_level0_col1" class="col_heading level0 col1" >HOUSES</th>
      <th id="T_9dba0_level0_col2" class="col_heading level0 col2" >INCOME</th>
      <th id="T_9dba0_level0_col3" class="col_heading level0 col3" >DEBT</th>
      <th id="T_9dba0_level0_col4" class="col_heading level0 col4" >EDUC</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="T_9dba0_level0_row0" class="row_heading level0 row0" >ASSET</th>
      <td id="T_9dba0_row0_col0" class="data row0 col0" >1.000000</td>
      <td id="T_9dba0_row0_col1" class="data row0 col1" >0.364955</td>
      <td id="T_9dba0_row0_col2" class="data row0 col2" >0.893282</td>
      <td id="T_9dba0_row0_col3" class="data row0 col3" >0.477171</td>
      <td id="T_9dba0_row0_col4" class="data row0 col4" >0.110659</td>
    </tr>
    <tr>
      <th id="T_9dba0_level0_row1" class="row_heading level0 row1" >HOUSES</th>
      <td id="T_9dba0_row1_col0" class="data row1 col0" >0.364955</td>
      <td id="T_9dba0_row1_col1" class="data row1 col1" >1.000000</td>
      <td id="T_9dba0_row1_col2" class="data row1 col2" >0.314501</td>
      <td id="T_9dba0_row1_col3" class="data row1 col3" >0.676984</td>
      <td id="T_9dba0_row1_col4" class="data row1 col4" >0.195174</td>
    </tr>
    <tr>
      <th id="T_9dba0_level0_row2" class="row_heading level0 row2" >INCOME</th>
      <td id="T_9dba0_row2_col0" class="data row2 col0" >0.893282</td>
      <td id="T_9dba0_row2_col1" class="data row2 col1" >0.314501</td>
      <td id="T_9dba0_row2_col2" class="data row2 col2" >1.000000</td>
      <td id="T_9dba0_row2_col3" class="data row2 col3" >0.456622</td>
      <td id="T_9dba0_row2_col4" class="data row2 col4" >0.108845</td>
    </tr>
    <tr>
      <th id="T_9dba0_level0_row3" class="row_heading level0 row3" >DEBT</th>
      <td id="T_9dba0_row3_col0" class="data row3 col0" >0.477171</td>
      <td id="T_9dba0_row3_col1" class="data row3 col1" >0.676984</td>
      <td id="T_9dba0_row3_col2" class="data row3 col2" >0.456622</td>
      <td id="T_9dba0_row3_col3" class="data row3 col3" >1.000000</td>
      <td id="T_9dba0_row3_col4" class="data row3 col4" >0.182570</td>
    </tr>
    <tr>
      <th id="T_9dba0_level0_row4" class="row_heading level0 row4" >EDUC</th>
      <td id="T_9dba0_row4_col0" class="data row4 col0" >0.110659</td>
      <td id="T_9dba0_row4_col1" class="data row4 col1" >0.195174</td>
      <td id="T_9dba0_row4_col2" class="data row4 col2" >0.108845</td>
      <td id="T_9dba0_row4_col3" class="data row4 col3" >0.182570</td>
      <td id="T_9dba0_row4_col4" class="data row4 col4" >1.000000</td>
    </tr>
  </tbody>
</table>




####
Whoa! There are some pretty important differences here! The relationship between "DEBT" and "HOUSES" is positive for both datasets, but while the coefficient for df is fairly weak at 0.25, the same number for df_fear is 0.67.

Remember, the closer a correlation coefficient is to 1.0, the more exactly they correspond. In this case, that means the value of the primary residence and the total debt held by the household is getting pretty close to being the same. This suggests that the main source of debt being carried by our "TURNFEAR" folks is their primary residence, which, again, is an intuitive finding.

"DEBT" and "ASSET" share a similarly striking difference, as do "EDUC" and "DEBT" which, while not as extreme a contrast as the other, is still big enough to catch the interest of our hypothetical banker.

Let's make some visualizations to show these relationships graphically.


```python

```
