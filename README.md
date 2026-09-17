# ECE-2112-PA4
Made by: Charles Steven Ang <br>
<br>
This Repository contains the code for ECE2112_PA4 and the `xlsx` file used to create the data frame. <br>
This experiment focuses on Data Wrangling and Data Visualization.<br>
<br>

A. VISAYAS COMMUNICATION DATAFRAME
Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track
is Communication. Retain only these columns, in the stated order:<br>
`Name, Gender, Math, Electronics, Average`

```python
import pandas as pd
import matplotlib.pyplot as plt
```
The library `pandas` and `matplotlib.pyplot` are imported at the very start of the code.

```python
INITIAL = pd.read_excel('board2.xlsx')
INITIAL['Average'] = INITIAL[['Math',	'Electronics',	'GEAS',	'Communication']].mean(axis=1)
```
The first line sets the xlsx file is set as the data frame `INITIAL`. The second line creates another row which contains the average scores of each subject per row. It does that by using the `.mean` function that uses an axis of 1 which just means it gets the average value of the variables inside the row.

```python
Viscommtemp = INITIAL[(INITIAL['Hometown'] == 'Visayas') & (INITIAL['Track'] == 'Communication')]
Viscomm = Viscommtemp[['Name', 'Gender', 'Math', 'Electronics', 'Average']]
```
This part basically filters out the students whose hometown is `Visayas` and whose track is `Communication` after filtering it displays the set columns which are: `'Name' 'Gender' 'Math' 'Electronics' 'Average'`.

```python
display(Viscomm)
print("Total Row Number:", len(Viscomm))
```
The Manual asks to display the finished data frame and how long it is.

B. VISAYAS FEMALE DATAFRAME
Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and
whose Gender is Female. Retain only:

```python
VisfemaleTemp = INITIAL[(INITIAL['Gender'] == 'Female') & (INITIAL['Hometown'] == 'Visayas')]
Visfemale = VisfemaleTemp[['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
```
`VisfemaleTemp` is used to filter out the Hometown and Gender of the students. After Filtering the `Visfemale` data frame is created, which shows the specified columns asked for by the manual.

```python
display(Visfemale)
display(Visfemale.loc[Visfemale['Average']>=60])
```
The first line displays the finished data frame. The second line displays the students whose average is equal and greater than 60.

C. CATEGORY-AVERAGE VISUALIZATION
Examine how the recorded Average differs across the three categorical features Track, Gender, and
Hometown. <br>
<br>
a. For each feature, compute the mean of Average for every category using Pandas. <br>
b. Display the three summary tables.<br>
c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.<br>
d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature.<br>

```python
avgTrack = INITIAL.groupby('Track')['Average'].mean().reset_index()
avgGender = INITIAL.groupby('Gender')['Average'].mean().reset_index()
avgHometown = INITIAL.groupby('Hometown')['Average'].mean().reset_index()
```
This part creates individual data frames from the main data frame `INITIAL` and gets the total average for each track.

```python
display(avgTrack)
display(avgGender)
display(avgHometown)
```
This part displays the new data frames containing the average for each track.

```python
graph, axes = plt.subplots(nrows=1, ncols=3, figsize=(16,4))

axes[0].bar(avgTrack['Track'], avgTrack['Average'])
axes[0].set(title='Mean Average by Track', xlabel='Track', ylabel='Mean Average')

axes[1].bar(avgGender['Gender'], avgGender['Average'])
axes[1].set(title='Mean Average by Gender', xlabel='Gender', ylabel='Mean Average')

axes[2].bar(avgHometown['Hometown'], avgHometown['Average'])
axes[2].set(title='Mean Average by Region', xlabel='Region', ylabel='Mean Average')

graph.text(0.125, -0.10, 'Summary of Results:', size=11)
graph.text(0.125, -0.28, 
    'For Track, Communication recorded the highest sample mean of 67.975.\n'
    'For Gender, Male recorded the highest sample mean of 67.183333.\n'
    'For Hometown, Luzon recorded the highest sample mean of 68.083333.', 
    size=11)

plt.show()
```








REPOSITORY VERSION HISTORY <br>
September 13, 2026 - Created Repository <br>
September 17, 2026 - Uploaded ipynb file. Finished README FILE <br>
