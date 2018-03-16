

```python
import pandas as pd
import numpy as np
import collections
```


```python
# File path for first csv
schools_data= "schools_complete.csv"
# Read our first csv into Pandas as a dataframe 
schools_data_df = pd.read_csv(schools_data)
# Rename "name" column to schools
schools_data_df = schools_data_df.rename(index=str, columns={"name": "school"})
# File path for second csv
student_data = "students_complete.csv"
# Read our second csv into Pandas 
student_data_df = pd.read_csv(student_data)
```


```python
# Get a list of columns for reference, in first csv
schools_data_df.columns
```




    Index(['School ID', 'school', 'type', 'size', 'budget'], dtype='object')




```python
# Get a list of columns for reference, in 2nd csv
student_data_df.columns
```




    Index(['Student ID', 'name', 'gender', 'grade', 'school', 'reading_score',
           'math_score'],
          dtype='object')




```python
# Merge Dataframes and view first 5 rows of new df 
merge_table_df = pd.merge(schools_data_df, student_data_df, how="left", on="school")
merge_table_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop unnecessary columns from df
merge_table_df = merge_table_df.drop("Student ID", axis=1)
merge_table_df = merge_table_df.drop("School ID", axis=1)
merge_table_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Find total number of records
total_records = len(merge_table_df)

# Find total number of schools
number_of_schools = (merge_table_df["school"]).nunique()

# Find total count of number of students 
number_students = (merge_table_df["size"]).value_counts()
number_students = number_students.sum()

# Find the total budget 
reduced_df = merge_table_df.groupby("school").agg(np.mean)
total_budget = reduced_df["budget"].sum()

# Find the average math score
average_math_score = merge_table_df.math_score.mean()

# Find the average reading score
average_reading_score = merge_table_df.reading_score.mean()

# Find the percent passing math
percent_passing_math = merge_table_df[merge_table_df["math_score"]>= 70]
percent_passing_math = len(percent_passing_math)
percent_passing_math = (percent_passing_math/total_records) * 100

# Find the percent passing reading
percent_passing_reading = merge_table_df[merge_table_df["reading_score"]>= 70]
percent_passing_reading = len(percent_passing_reading)
percent_passing_reading = (percent_passing_reading/total_records) * 100

# Find the overall passing rate
overall_passing_rate = (percent_passing_math + percent_passing_reading)/2
```


```python
# Create new dataframe from calculations
from collections import OrderedDict
district_summary_dict = {"Total Schools": [number_of_schools],
                        "Total Students": [number_students],
                        "Total Budget": [total_budget],
                        "Average Math Score": [average_math_score],
                        "Average Reading Score": [average_reading_score],
                        "Percent Passing Math":[percent_passing_math],
                        "Percent Passing Reading":[percent_passing_reading],
                        "Overall Passing Rate":[overall_passing_rate]}
district_summary_dict = OrderedDict(sorted(district_summary_dict.items()))
new_district_summary = OrderedDict([("Total Schools", [number_of_schools]),
                        ("Total Students", [number_students]),
                        ("Total Budget", [total_budget]),
                        ("Average Math Score", [average_math_score]),
                        ("Average Reading Score", [average_reading_score]),
                        ("Percent Passing Math", [percent_passing_math]),
                        ("Percent Passing Reading", [percent_passing_reading]),
                        ("Overall Passing Rate", [overall_passing_rate])])

district_summary_df = pd.DataFrame(new_district_summary)
district_summary_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Percent Passing Math</th>
      <th>Percent Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39170</td>
      <td>24649428.0</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>74.980853</td>
      <td>85.805463</td>
      <td>80.393158</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Begin the schools summary by finding the average reading and math scores per school
new_merge_df = merge_table_df.groupby("school").mean()
new_merge_df
# Reset index
new_merge_df = new_merge_df.reset_index(level=None, drop=False, inplace=False)

# Add column with school type via merge
school_type_df = merge_table_df.loc[:,"school":"type"]
school_type_df = pd.DataFrame(school_type_df.groupby("school").min())
# Reset index so that we can use "school" as a merge column
school_type_df = school_type_df.reset_index(level=None, drop=False, inplace=False)
school_summary_table_df = pd.merge(school_type_df, new_merge_df, how="left", on="school")

# Create a new column called "Per Student Budget" and add to existing dataframe 
school_summary_table_df["Per Student Budget"] = school_summary_table_df["budget"]/school_summary_table_df["size"]

# Calculate and add a new column called percent passing reading
new_merge_df = merge_table_df[merge_table_df["reading_score"] >= 70]
group_of_passing_reading = new_merge_df.groupby("school").count()["name"]
school_percent_passing_reading = group_of_passing_reading / merge_table_df.groupby("school").count()["name"]*100
school_percent_passing_reading = school_percent_passing_reading.to_frame()
school_percent_passing_reading = school_percent_passing_reading.reset_index(level=None, drop=False, inplace=False)
school_summary_merge = pd.merge(school_summary_table_df, school_percent_passing_reading, how="left", on="school")

# Create a new column called "Percent Passing Math" and add to existing dataframe 
new_merge_df = merge_table_df[merge_table_df["math_score"] >= 70]
group_of_passing_math = new_merge_df.groupby("school").count()["name"]
school_percent_passing_math = group_of_passing_math / merge_table_df.groupby("school").count()["name"]*100
school_percent_passing_math = school_percent_passing_math.to_frame()
school_percent_passing_math = school_percent_passing_math.reset_index(level=None, drop=False, inplace=False)
school_summary_merge = pd.merge(school_summary_merge, school_percent_passing_math, how="left", on="school")

# Create a new column called "Overall Passing Rate" and add to existing dataframe 
school_summary_merge["Overall Passing Rate"] = (school_summary_merge['name_y']+school_summary_merge['name_x'])/2
# Rename columns
school_summary_merge = school_summary_merge.rename(columns={"name_x":"Percent Passing Reading","name_y":"Percent Passing Math"})
school_summary_merge
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Per Student Budget</th>
      <th>Percent Passing Reading</th>
      <th>Percent Passing Math</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976.0</td>
      <td>3124928.0</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>628.0</td>
      <td>81.933280</td>
      <td>66.680064</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858.0</td>
      <td>1081356.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>582.0</td>
      <td>97.039828</td>
      <td>94.133477</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949.0</td>
      <td>1884411.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>639.0</td>
      <td>80.739234</td>
      <td>65.988471</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739.0</td>
      <td>1763916.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>644.0</td>
      <td>79.299014</td>
      <td>68.309602</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468.0</td>
      <td>917500.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>625.0</td>
      <td>97.138965</td>
      <td>93.392371</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635.0</td>
      <td>3022020.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>652.0</td>
      <td>80.862999</td>
      <td>66.752967</td>
      <td>73.807983</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427.0</td>
      <td>248087.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>581.0</td>
      <td>96.252927</td>
      <td>92.505855</td>
      <td>94.379391</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917.0</td>
      <td>1910635.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>655.0</td>
      <td>81.316421</td>
      <td>65.683922</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761.0</td>
      <td>3094650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>650.0</td>
      <td>81.222432</td>
      <td>66.057551</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962.0</td>
      <td>585858.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>609.0</td>
      <td>95.945946</td>
      <td>94.594595</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999.0</td>
      <td>2547363.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>637.0</td>
      <td>80.220055</td>
      <td>66.366592</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761.0</td>
      <td>1056600.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>600.0</td>
      <td>95.854628</td>
      <td>93.867121</td>
      <td>94.860875</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635.0</td>
      <td>1043130.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>638.0</td>
      <td>97.308869</td>
      <td>93.272171</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283.0</td>
      <td>1319574.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>578.0</td>
      <td>96.539641</td>
      <td>93.867718</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800.0</td>
      <td>1049400.0</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>583.0</td>
      <td>96.611111</td>
      <td>93.333333</td>
      <td>94.972222</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a table that highlights the top 5 performing schools based on overall passing rate
top_schools = school_summary_merge.sort_values(by=['Overall Passing Rate'], ascending=False)
top_schools.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Per Student Budget</th>
      <th>Percent Passing Reading</th>
      <th>Percent Passing Math</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858.0</td>
      <td>1081356.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>582.0</td>
      <td>97.039828</td>
      <td>94.133477</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635.0</td>
      <td>1043130.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>638.0</td>
      <td>97.308869</td>
      <td>93.272171</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962.0</td>
      <td>585858.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>609.0</td>
      <td>95.945946</td>
      <td>94.594595</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468.0</td>
      <td>917500.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>625.0</td>
      <td>97.138965</td>
      <td>93.392371</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283.0</td>
      <td>1319574.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>578.0</td>
      <td>96.539641</td>
      <td>93.867718</td>
      <td>95.203679</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Bottom performing schools
bottom_schools = school_summary_merge.sort_values(by=['Overall Passing Rate'], ascending=True)
bottom_schools.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Per Student Budget</th>
      <th>Percent Passing Reading</th>
      <th>Percent Passing Math</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999.0</td>
      <td>2547363.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>637.0</td>
      <td>80.220055</td>
      <td>66.366592</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949.0</td>
      <td>1884411.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>639.0</td>
      <td>80.739234</td>
      <td>65.988471</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917.0</td>
      <td>1910635.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>655.0</td>
      <td>81.316421</td>
      <td>65.683922</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761.0</td>
      <td>3094650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>650.0</td>
      <td>81.222432</td>
      <td>66.057551</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739.0</td>
      <td>1763916.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>644.0</td>
      <td>79.299014</td>
      <td>68.309602</td>
      <td>73.804308</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Math scores for each grade, grouped by school
student_data_df_9th = student_data_df[student_data_df["grade"] == '9th']
mathbygrade_9th = student_data_df_9th.groupby("school").math_score.mean()
mathbygrade_9th = mathbygrade_9th.reset_index(level=None, drop=False, name=None, inplace=False)

student_data_df_10th = student_data_df[student_data_df["grade"] == '10th']
mathbygrade_10th = student_data_df_10th.groupby("school").math_score.mean()
mathbygrade_10th = mathbygrade_10th.reset_index(level=None, drop=False, name=None, inplace=False)

student_data_df_11th = student_data_df[(student_data_df["grade"] == '11th')]
mathbygrade_df_11th = student_data_df_11th.groupby("school").math_score.mean()
mathbygrade_df_11th = mathbygrade_df_11th.reset_index(level=None, drop=False, name=None, inplace=False)

student_data_df_12th = student_data_df[(student_data_df["grade"] == '12th')]
mathbygrade_df_12th = student_data_df_12th.groupby("school").math_score.mean()
mathbygrade_df_12th = mathbygrade_df_12th.reset_index(level=None, drop=False, name=None, inplace=False)

# Merge all new data into one dataframe
merge_mathbygrade_df = pd.merge(mathbygrade_df_11th, mathbygrade_df_12th, how="outer", on= "school", suffixes=('_11th', '_12th'))
merge_mathbygrade_df = pd.merge(mathbygrade_10th, merge_mathbygrade_df, how= "outer", on= "school")
merge_mathbygrade_df = pd.merge(mathbygrade_9th, merge_mathbygrade_df, how= "outer", on= "school")
merge_mathbygrade_df
# Change column labels
merge_mathbygrade_df = merge_mathbygrade_df.rename(columns={"math_score_x":"math_score_9th","math_score_y":"math_score_10th"})
merge_mathbygrade_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>math_score_9th</th>
      <th>math_score_10th</th>
      <th>math_score_11th</th>
      <th>math_score_12th</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Reading scores by grade, grouped by school
student_data_df_9th = student_data_df[student_data_df["grade"] == '9th']
readingbygrade_9th = student_data_df_9th.groupby("school").reading_score.mean()
readingbygrade_9th = readingbygrade_9th.reset_index(level=None, drop=False, name=None, inplace=False)

student_data_df_10th = student_data_df[student_data_df["grade"] == '10th']
readingbygrade_10th = student_data_df_10th.groupby("school").reading_score.mean()
readingbygrade_10th = readingbygrade_10th.reset_index(level=None, drop=False, name=None, inplace=False)

student_data_df_11th = student_data_df[(student_data_df["grade"] == '11th')]
readingbygrade_11th = student_data_df_11th.groupby("school").reading_score.mean()
readingbygrade_11th = readingbygrade_11th.reset_index(level=None, drop=False, name=None, inplace=False)

student_data_df_12th = student_data_df[(student_data_df["grade"] == '12th')]
readingbygrade_12th = student_data_df_12th.groupby("school").reading_score.mean()
readingbygrade_12th = readingbygrade_12th.reset_index(level=None, drop=False, name=None, inplace=False)

# Merge all new data into one dataframe
merge_readingbygrade_df = pd.merge(readingbygrade_11th, readingbygrade_12th, how="outer", on= "school", suffixes=('_11th', '_12th'))
merge_readingbygrade_df = pd.merge(readingbygrade_10th, merge_readingbygrade_df, how= "outer", on= "school")
merge_readingbygrade_df = pd.merge(readingbygrade_9th, merge_readingbygrade_df, how= "outer", on= "school")
merge_readingbygrade_df
# Change column labels
merge_readingbygrade_df = merge_readingbygrade_df.rename(columns={"reading_score_x":"reading_score_9th","reading_score_y":"reading_score_10th"})
merge_readingbygrade_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school</th>
      <th>reading_score_9th</th>
      <th>reading_score_10th</th>
      <th>reading_score_11th</th>
      <th>reading_score_12th</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>81.303155</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.676136</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>81.198598</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>80.632653</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.369193</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>80.866860</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>83.677165</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>81.290284</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>81.260714</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>83.807273</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>80.993127</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>84.122642</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>83.728850</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>83.939778</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>83.833333</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Scores by school spending per student budget
bins = [575, 600, 620, 640, 660]
spending_names = ["$575-599", "$600-619", "$620-639", "$640-659"]
school_summary_merge["Spending per student"] = pd.cut(school_summary_merge["Per Student Budget"], bins, labels=spending_names)
school_summary_reduced = school_summary_merge.drop("size", axis = 1)
school_summary_reduced = school_summary_reduced.drop("budget", axis = 1)
school_summary_reduced = school_summary_reduced.drop("Per Student Budget", axis = 1)
school_spending_group = school_summary_reduced.groupby("Spending per student")
school_spending_group.mean()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Percent Passing Reading</th>
      <th>Percent Passing Math</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Spending per student</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>$575-599</th>
      <td>83.892196</td>
      <td>83.436210</td>
      <td>96.459627</td>
      <td>93.541501</td>
      <td>95.000564</td>
    </tr>
    <tr>
      <th>$600-619</th>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>95.945946</td>
      <td>94.594595</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>$620-639</th>
      <td>82.120471</td>
      <td>79.474551</td>
      <td>87.468080</td>
      <td>77.139934</td>
      <td>82.304007</td>
    </tr>
    <tr>
      <th>$640-659</th>
      <td>80.957446</td>
      <td>77.023555</td>
      <td>80.675217</td>
      <td>66.701010</td>
      <td>73.688113</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Scores by school size
bins = [0, 1750, 3250, 5000]
group_names = ["Small", "Medium", "Large"]
school_summary_reduced["School Size Category"] = pd.cut(school_summary_merge["size"], bins, labels=group_names)
school_size_categories = school_summary_reduced.groupby("School Size Category")
school_size_categories.mean()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Percent Passing Reading</th>
      <th>Percent Passing Math</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Size Category</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small</th>
      <td>83.881343</td>
      <td>83.603261</td>
      <td>96.661677</td>
      <td>93.441248</td>
      <td>95.051462</td>
    </tr>
    <tr>
      <th>Medium</th>
      <td>82.676142</td>
      <td>80.545935</td>
      <td>89.628554</td>
      <td>82.169092</td>
      <td>85.898823</td>
    </tr>
    <tr>
      <th>Large</th>
      <td>80.919864</td>
      <td>77.063340</td>
      <td>81.059691</td>
      <td>66.464293</td>
      <td>73.761992</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Scores by School type
school_type_categories = school_summary_reduced.groupby("type")
school_type_categories.mean() 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Percent Passing Reading</th>
      <th>Percent Passing Math</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.896421</td>
      <td>83.473852</td>
      <td>96.586489</td>
      <td>93.620830</td>
      <td>95.103660</td>
    </tr>
    <tr>
      <th>District</th>
      <td>80.966636</td>
      <td>76.956733</td>
      <td>80.799062</td>
      <td>66.548453</td>
      <td>73.673757</td>
    </tr>
  </tbody>
</table>
</div>


