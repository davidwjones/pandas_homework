
1)	Bigger is not better!
    a.	The performance difference between the smaller schools (under 1,000 students) and the larger schools (over 4,000 students) is significant.
    b.	When you also look at the total student experience (passing both the math and the reading tests) it is a significant data point that HALF of the students are not excelling in the larger schools.

2)	Money is not the answer!
    a.	The performance difference between the schools with the largest per student spend vs the smallest per student spend is also significant.
    b.	This is actually an interesting view of the data.  It mirrors the student class size as far as the student success.  However, if you review across the summary you will note that the spend per student does not really corelate to the school’s number of students.  Intuitively, you would think that an economy of scale for larger schools would be in play, but that does not prove out across the district. 

3)	If the district is looking for the most strategic use of future tax funding, it would appear that the district should focus on 2 items.  First, they should be trying to have smaller, cheaper schools.  The second thing they should focus on is a year over year focus on improvement.  

 While the type of school appears to be significant (Charter School vs District), the student makeup of the Charter School is  typically the smarter students who want a different school experience. Therefore, it does not make sense to drive for Charter Schools as an alternative growth plan. 

 As I mentioned earlier, there needs to be a focus on year over year improvement.  If you look at the graphs across the various school’s grades, you will notice that there is no significant change at the school level from grade to grade in either math or reading.
 
 The average change over the 4 years of High School is between .4% and 1.9% for reading and .4% and 2.6% for math.  What this means is that no matter what school you attend, you are not significantly improving between your Freshman year and your Senior year.  We MUST drive change there to make a difference.        


```python
#Dependencies
import os
import pandas as pd
```


```python
#read the csv files and load the DataFrames
schools="schools_complete.csv"
students="students_complete.csv"
school_data=pd.read_csv(schools,encoding="iso-8859-1")
student_data=pd.read_csv(students,encoding="iso-8859-1")
school_df=pd.DataFrame(school_data)
student_df=pd.DataFrame(student_data)

school_df=school_df.rename(columns={"name":"school"})
school_df

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
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
    </tr>
  </tbody>
</table>
</div>




```python
#set Boolean variables to asses passing

student_df["reading pass"]=student_df["reading_score"]>70
student_df["math pass"]=student_df["math_score"]>70
student_df["Passed Math & Reading"]=((student_df["reading pass"])&(student_df["math pass"]))

student_df.head()
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
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>reading pass</th>
      <th>math pass</th>
      <th>Passed Math &amp; Reading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
#start calculating the various required summary information from the two dataframes
total_schools=len(school_df["school"])
total_students=len(student_df["name"])
total_budget=school_df["budget"].sum()
avg_math_score=student_df["math_score"].mean()
avg_read_score=student_df["reading_score"].mean()
math_pass=sum(student_df["math pass"])
math_pass_percent= (math_pass/total_students) * 100
read_pass=sum(student_df["reading pass"])
read_pass_percent=(read_pass/total_students) * 100
#This is not required, but I'm also reviewing the passing of both math and reading
total_pass=sum((student_df["reading pass"]) & (student_df["math pass"]))
total_pass_percent=(total_pass/total_students) * 100
overall_passing_rate = ((read_pass_percent + math_pass_percent)/2)

```


```python
#take all of the summarized data and put it in a summary table, fomatted for the District
district_summary = pd.DataFrame({  "Total Schools": [total_schools],
                                   "Total Students": [total_students],
                                   "Total Budget": [total_budget],
                                   "Avg. Math Score": [avg_math_score],
                                   "Percent Passing Math": [math_pass_percent],
                                   "Avg Reading Score": [avg_read_score],
                                   "Percent Passing Reading":[read_pass_percent],
                                   "Overall Passing Rate":[overall_passing_rate] })
district_summary = district_summary[["Total Schools",
                                    "Total Students",
                                    "Total Budget",
                                    "Avg. Math Score",
                                    "Percent Passing Math",
                                    "Avg Reading Score",
                                    "Percent Passing Reading",
                                    "Overall Passing Rate"]]
district_summary=district_summary.round(2)
district_summary["Total Students"]=district_summary["Total Students"].map("{0:,d}".format)
district_summary["Percent Passing Math"]=district_summary["Percent Passing Math"].map("{0:,.2f}%".format)
district_summary["Percent Passing Reading"]=district_summary["Percent Passing Reading"].map("{0:,.2f}%".format)
district_summary["Overall Passing Rate"]=district_summary["Overall Passing Rate"].map("{0:,.2f}%".format)
district_summary["Total Budget"]=district_summary["Total Budget"].map("${0:,.0f}".format)
district_summary
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
      <th>Avg. Math Score</th>
      <th>Percent Passing Math</th>
      <th>Avg Reading Score</th>
      <th>Percent Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428</td>
      <td>78.99</td>
      <td>72.39%</td>
      <td>81.88</td>
      <td>82.97%</td>
      <td>77.68%</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Now creating a Summary Table for all of the Schools
school_summary=school_df
school_summary=school_summary.rename(columns={"type":"School Type",
                                             "size":"Total Students",
                                             "budget":"Total School Budget"})
school_summary["Per Student Budget"]=school_summary["Total School Budget"]/school_summary["Total Students"]
school_summary.drop("School ID",axis=1,inplace=True)

first_gp=student_df.groupby(["school"])
```


```python
#calculate the various variables required for the summary table
school_math=first_gp['math_score'].mean()
school_reading=first_gp['reading_score'].mean()
math_num=first_gp['math pass'].sum()
reading_num=first_gp['reading pass'].sum()
both_num=first_gp['Passed Math & Reading'].sum()
school_math_df=pd.DataFrame(school_math)
school_math_df["math pass num"]= math_num
school_math_df["Passed Both"]=both_num
school_math_df.reset_index(inplace=True)
school_reading_df=pd.DataFrame(school_reading)
school_reading_df["read pass num"]=reading_num
school_reading_df.reset_index(inplace=True)
math_and_read=pd.merge(school_math_df,school_reading_df,)
school_summary=pd.merge(school_summary,math_and_read,on="school")
school_summary["% Passing Math"]=school_summary["math pass num"]/school_summary["Total Students"]*100
school_summary["% Passing Reading"]=school_summary["read pass num"]/school_summary["Total Students"]*100
school_summary["Overall Passing Rate"]=((school_summary['% Passing Math']+school_summary['% Passing Reading'])/2)
school_summary["% Passed Both"]=school_summary['Passed Both']/school_summary["Total Students"]*100
```


```python
#Additional Formatting for the table
final_school_summary=school_summary
final_school_summary=final_school_summary.rename(columns={"school":"School",
                                                         "math_score":"Avg. Math Score",
                                                         "reading_score":"Avg. Reading Score"})
final_school_summary.drop("math pass num",axis=1,inplace=True)
final_school_summary.drop("read pass num",axis=1,inplace=True)
final_school_summary=final_school_summary.round(2)
final_school_summary["Total Students"]=final_school_summary["Total Students"].map("{0:,d}".format)
final_school_summary["% Passing Math"]=final_school_summary["% Passing Math"].map("{0:,.2f}%".format)
final_school_summary["% Passing Reading"]=final_school_summary["% Passing Reading"].map("{0:,.2f}%".format)
final_school_summary["Overall Passing Rate"]=final_school_summary["Overall Passing Rate"].map("{0:,.2f}%".format)
final_school_summary["Total School Budget"]=final_school_summary["Total School Budget"].map("${0:,.0f}".format)
final_school_summary["Per Student Budget"]=final_school_summary["Per Student Budget"].map("${0:,.0f}".format)
final_school_summary["% Passed Both"]=final_school_summary["% Passed Both"].map("{0:,.2f}%".format)
#Summary for all schools
final_school_summary=final_school_summary.sort_values("School")
final_school_summary.reset_index(inplace=True)
final_school_summary
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
      <th>index</th>
      <th>School</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Avg. Math Score</th>
      <th>Passed Both</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>% Passed Both</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4,976</td>
      <td>$3,124,928</td>
      <td>$628</td>
      <td>77.05</td>
      <td>2545.0</td>
      <td>81.03</td>
      <td>64.63%</td>
      <td>79.30%</td>
      <td>71.97%</td>
      <td>51.15%</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1,858</td>
      <td>$1,081,356</td>
      <td>$582</td>
      <td>83.06</td>
      <td>1561.0</td>
      <td>83.98</td>
      <td>89.56%</td>
      <td>93.86%</td>
      <td>91.71%</td>
      <td>84.02%</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2,949</td>
      <td>$1,884,411</td>
      <td>$639</td>
      <td>76.71</td>
      <td>1472.0</td>
      <td>81.16</td>
      <td>63.75%</td>
      <td>78.43%</td>
      <td>71.09%</td>
      <td>49.92%</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2,739</td>
      <td>$1,763,916</td>
      <td>$644</td>
      <td>77.10</td>
      <td>1405.0</td>
      <td>80.75</td>
      <td>65.75%</td>
      <td>77.51%</td>
      <td>71.63%</td>
      <td>51.30%</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1,468</td>
      <td>$917,500</td>
      <td>$625</td>
      <td>83.35</td>
      <td>1228.0</td>
      <td>83.82</td>
      <td>89.71%</td>
      <td>93.39%</td>
      <td>91.55%</td>
      <td>83.65%</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4,635</td>
      <td>$3,022,020</td>
      <td>$652</td>
      <td>77.29</td>
      <td>2325.0</td>
      <td>80.93</td>
      <td>64.75%</td>
      <td>78.19%</td>
      <td>71.47%</td>
      <td>50.16%</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087</td>
      <td>$581</td>
      <td>83.80</td>
      <td>359.0</td>
      <td>83.81</td>
      <td>90.63%</td>
      <td>92.74%</td>
      <td>91.69%</td>
      <td>84.07%</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2,917</td>
      <td>$1,910,635</td>
      <td>$655</td>
      <td>76.63</td>
      <td>1456.0</td>
      <td>81.18</td>
      <td>63.32%</td>
      <td>78.81%</td>
      <td>71.07%</td>
      <td>49.91%</td>
    </tr>
    <tr>
      <th>8</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4,761</td>
      <td>$3,094,650</td>
      <td>$650</td>
      <td>77.07</td>
      <td>2371.0</td>
      <td>80.97</td>
      <td>63.85%</td>
      <td>78.28%</td>
      <td>71.07%</td>
      <td>49.80%</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858</td>
      <td>$609</td>
      <td>83.84</td>
      <td>816.0</td>
      <td>84.04</td>
      <td>91.68%</td>
      <td>92.20%</td>
      <td>91.94%</td>
      <td>84.82%</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3,999</td>
      <td>$2,547,363</td>
      <td>$637</td>
      <td>76.84</td>
      <td>1977.0</td>
      <td>80.74</td>
      <td>64.07%</td>
      <td>77.74%</td>
      <td>70.91%</td>
      <td>49.44%</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1,761</td>
      <td>$1,056,600</td>
      <td>$600</td>
      <td>83.36</td>
      <td>1465.0</td>
      <td>83.73</td>
      <td>89.89%</td>
      <td>92.62%</td>
      <td>91.25%</td>
      <td>83.19%</td>
    </tr>
    <tr>
      <th>12</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1,635</td>
      <td>$1,043,130</td>
      <td>$638</td>
      <td>83.42</td>
      <td>1378.0</td>
      <td>83.85</td>
      <td>90.21%</td>
      <td>92.91%</td>
      <td>91.56%</td>
      <td>84.28%</td>
    </tr>
    <tr>
      <th>13</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2,283</td>
      <td>$1,319,574</td>
      <td>$578</td>
      <td>83.27</td>
      <td>1938.0</td>
      <td>83.99</td>
      <td>90.93%</td>
      <td>93.25%</td>
      <td>92.09%</td>
      <td>84.89%</td>
    </tr>
    <tr>
      <th>14</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1,800</td>
      <td>$1,049,400</td>
      <td>$583</td>
      <td>83.68</td>
      <td>1520.0</td>
      <td>83.96</td>
      <td>90.28%</td>
      <td>93.44%</td>
      <td>91.86%</td>
      <td>84.44%</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Formatted for the top 5 performing schools
final_school_summary=final_school_summary.sort_values("Overall Passing Rate",ascending=False)
final_school_summary.head(5)
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
      <th>index</th>
      <th>School</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Avg. Math Score</th>
      <th>Passed Both</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>% Passed Both</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>13</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2,283</td>
      <td>$1,319,574</td>
      <td>$578</td>
      <td>83.27</td>
      <td>1938.0</td>
      <td>83.99</td>
      <td>90.93%</td>
      <td>93.25%</td>
      <td>92.09%</td>
      <td>84.89%</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858</td>
      <td>$609</td>
      <td>83.84</td>
      <td>816.0</td>
      <td>84.04</td>
      <td>91.68%</td>
      <td>92.20%</td>
      <td>91.94%</td>
      <td>84.82%</td>
    </tr>
    <tr>
      <th>14</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1,800</td>
      <td>$1,049,400</td>
      <td>$583</td>
      <td>83.68</td>
      <td>1520.0</td>
      <td>83.96</td>
      <td>90.28%</td>
      <td>93.44%</td>
      <td>91.86%</td>
      <td>84.44%</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1,858</td>
      <td>$1,081,356</td>
      <td>$582</td>
      <td>83.06</td>
      <td>1561.0</td>
      <td>83.98</td>
      <td>89.56%</td>
      <td>93.86%</td>
      <td>91.71%</td>
      <td>84.02%</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087</td>
      <td>$581</td>
      <td>83.80</td>
      <td>359.0</td>
      <td>83.81</td>
      <td>90.63%</td>
      <td>92.74%</td>
      <td>91.69%</td>
      <td>84.07%</td>
    </tr>
  </tbody>
</table>
</div>




```python
#formatted for the 5 worst performing schools
final_school_summary=final_school_summary.sort_values("Overall Passing Rate",ascending=True)
final_school_summary.head(5)
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
      <th>index</th>
      <th>School</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Avg. Math Score</th>
      <th>Passed Both</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>% Passed Both</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3,999</td>
      <td>$2,547,363</td>
      <td>$637</td>
      <td>76.84</td>
      <td>1977.0</td>
      <td>80.74</td>
      <td>64.07%</td>
      <td>77.74%</td>
      <td>70.91%</td>
      <td>49.44%</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2,917</td>
      <td>$1,910,635</td>
      <td>$655</td>
      <td>76.63</td>
      <td>1456.0</td>
      <td>81.18</td>
      <td>63.32%</td>
      <td>78.81%</td>
      <td>71.07%</td>
      <td>49.91%</td>
    </tr>
    <tr>
      <th>8</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4,761</td>
      <td>$3,094,650</td>
      <td>$650</td>
      <td>77.07</td>
      <td>2371.0</td>
      <td>80.97</td>
      <td>63.85%</td>
      <td>78.28%</td>
      <td>71.07%</td>
      <td>49.80%</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2,949</td>
      <td>$1,884,411</td>
      <td>$639</td>
      <td>76.71</td>
      <td>1472.0</td>
      <td>81.16</td>
      <td>63.75%</td>
      <td>78.43%</td>
      <td>71.09%</td>
      <td>49.92%</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4,635</td>
      <td>$3,022,020</td>
      <td>$652</td>
      <td>77.29</td>
      <td>2325.0</td>
      <td>80.93</td>
      <td>64.75%</td>
      <td>78.19%</td>
      <td>71.47%</td>
      <td>50.16%</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Table to look at the Math Scores across all schools and by Class
by_grade=student_df
by_grade['grade']=by_grade['grade'].astype('category', categories=['9th','10th','11th','12th'])
math_scores_grade= round(by_grade.pivot_table(index="school",columns="grade",values="math_score"),2)
math_scores_grade

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
      <th>grade</th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.08</td>
      <td>77.00</td>
      <td>77.52</td>
      <td>76.49</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.09</td>
      <td>83.15</td>
      <td>82.77</td>
      <td>83.28</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.40</td>
      <td>76.54</td>
      <td>76.88</td>
      <td>77.15</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.36</td>
      <td>77.67</td>
      <td>76.92</td>
      <td>76.18</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.04</td>
      <td>84.23</td>
      <td>83.84</td>
      <td>83.36</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.44</td>
      <td>77.34</td>
      <td>77.14</td>
      <td>77.19</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.79</td>
      <td>83.43</td>
      <td>85.00</td>
      <td>82.86</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.03</td>
      <td>75.91</td>
      <td>76.45</td>
      <td>77.23</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.19</td>
      <td>76.69</td>
      <td>77.49</td>
      <td>76.86</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.63</td>
      <td>83.37</td>
      <td>84.33</td>
      <td>84.12</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.86</td>
      <td>76.61</td>
      <td>76.40</td>
      <td>77.69</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.42</td>
      <td>82.92</td>
      <td>83.38</td>
      <td>83.78</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.59</td>
      <td>83.09</td>
      <td>83.50</td>
      <td>83.50</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.09</td>
      <td>83.72</td>
      <td>83.20</td>
      <td>83.04</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.26</td>
      <td>84.01</td>
      <td>83.84</td>
      <td>83.64</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Table to look at Reading scores across all schools by grade
reading_scores_grade= round(by_grade.pivot_table(index="school",columns="grade",values="reading_score"),2)
reading_scores_grade
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
      <th>grade</th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.30</td>
      <td>80.91</td>
      <td>80.95</td>
      <td>80.91</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.68</td>
      <td>84.25</td>
      <td>83.79</td>
      <td>84.29</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.20</td>
      <td>81.41</td>
      <td>80.64</td>
      <td>81.38</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.63</td>
      <td>81.26</td>
      <td>80.40</td>
      <td>80.66</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.37</td>
      <td>83.71</td>
      <td>84.29</td>
      <td>84.01</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.87</td>
      <td>80.66</td>
      <td>81.40</td>
      <td>80.86</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.68</td>
      <td>83.32</td>
      <td>83.82</td>
      <td>84.70</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.29</td>
      <td>81.51</td>
      <td>81.42</td>
      <td>80.31</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.26</td>
      <td>80.77</td>
      <td>80.62</td>
      <td>81.23</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.81</td>
      <td>83.61</td>
      <td>84.34</td>
      <td>84.59</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.99</td>
      <td>80.63</td>
      <td>80.86</td>
      <td>80.38</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.12</td>
      <td>83.44</td>
      <td>84.37</td>
      <td>82.78</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.73</td>
      <td>84.25</td>
      <td>83.59</td>
      <td>83.83</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.94</td>
      <td>84.02</td>
      <td>83.76</td>
      <td>84.32</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.83</td>
      <td>83.81</td>
      <td>84.16</td>
      <td>84.07</td>
    </tr>
  </tbody>
</table>
</div>




```python
#binning on spending to look at schools grouped by the average spend per student
spending_bin=[0,599,625,640,1000]
spending_labels=[" < $600 ", "$600 - $625", "$626 - $640"," > $640 "]
binned_spend=school_summary
binned_spend["Spending Ranges per Student"]=pd.cut(binned_spend["Per Student Budget"],spending_bin,labels=spending_labels)
spend_grouped_schools=pd.pivot_table(binned_spend, index=["Spending Ranges per Student"])
per_student_spend=round(spend_grouped_schools[['math_score','reading_score','% Passing Math','% Passing Reading','Overall Passing Rate','% Passed Both']],2)
per_student_spend=per_student_spend.rename(columns={"math_score":"Avg. Math Score","reading_score":"Avg. Reading Score"})

per_student_spend
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
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>% Passed Both</th>
    </tr>
    <tr>
      <th>Spending Ranges per Student</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt; $600</th>
      <td>83.46</td>
      <td>83.93</td>
      <td>90.35</td>
      <td>93.33</td>
      <td>91.84</td>
      <td>84.36</td>
    </tr>
    <tr>
      <th>$600 - $625</th>
      <td>83.52</td>
      <td>83.86</td>
      <td>90.43</td>
      <td>92.74</td>
      <td>91.58</td>
      <td>83.89</td>
    </tr>
    <tr>
      <th>$626 - $640</th>
      <td>78.51</td>
      <td>81.70</td>
      <td>70.67</td>
      <td>82.10</td>
      <td>76.38</td>
      <td>58.69</td>
    </tr>
    <tr>
      <th>&gt; $640</th>
      <td>77.02</td>
      <td>80.96</td>
      <td>64.42</td>
      <td>78.20</td>
      <td>71.31</td>
      <td>50.29</td>
    </tr>
  </tbody>
</table>
</div>




```python
#binning on school size to look at schools grouped by the average size of schools
size_bin=[0,1000,2000,4000,8000]
size_labels=[" < 1,000 ", "1,000 - 2,000", "2,000 - 4,000"," > 4,000"]
binned_size=school_summary
binned_size["Number of Students"]=pd.cut(binned_size["Total Students"],size_bin,labels=size_labels)
size_grouped_schools=pd.pivot_table(binned_size, index=["Number of Students"])
per_student_size=round(size_grouped_schools[['math_score','reading_score','% Passing Math','% Passing Reading','Overall Passing Rate','% Passed Both']],2)
per_student_size=per_student_size.rename(columns={"math_score":"Avg. Math Score","reading_score":"Avg. Reading Score"})

per_student_size
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
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>% Passed Both</th>
    </tr>
    <tr>
      <th>Number of Students</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt; 1,000</th>
      <td>83.82</td>
      <td>83.93</td>
      <td>91.16</td>
      <td>92.47</td>
      <td>91.82</td>
      <td>84.45</td>
    </tr>
    <tr>
      <th>1,000 - 2,000</th>
      <td>83.37</td>
      <td>83.86</td>
      <td>89.93</td>
      <td>93.24</td>
      <td>91.59</td>
      <td>83.92</td>
    </tr>
    <tr>
      <th>2,000 - 4,000</th>
      <td>78.11</td>
      <td>81.56</td>
      <td>69.56</td>
      <td>81.15</td>
      <td>75.36</td>
      <td>57.09</td>
    </tr>
    <tr>
      <th>&gt; 4,000</th>
      <td>77.14</td>
      <td>80.98</td>
      <td>64.41</td>
      <td>78.59</td>
      <td>71.50</td>
      <td>50.37</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Table to look at the two school types and their scores
type_of_school=pd.pivot_table(school_summary,index=["School Type"])
type_of_school=round(type_of_school[['math_score','reading_score','% Passing Math','% Passing Reading','Overall Passing Rate','% Passed Both']],2)
type_of_school=type_of_school.rename(columns={"math_score":"Avg. Math Score","reading_score":"Avg. Reading Score"})
type_of_school
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
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>% Passed Both</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
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
      <td>83.47</td>
      <td>83.90</td>
      <td>90.36</td>
      <td>93.05</td>
      <td>91.71</td>
      <td>84.17</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.96</td>
      <td>80.97</td>
      <td>64.30</td>
      <td>78.32</td>
      <td>71.31</td>
      <td>50.24</td>
    </tr>
  </tbody>
</table>
</div>


