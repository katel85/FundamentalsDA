# Fundamentals Data Analytics Project Dec 2021:

This repositiory contains two notebooks called CAO and Pyplot. They are jupyter notebooks that have been constructed to attain a better understaing of the fundamentals of data analytics.

The first notebook in this repositiry is the pyplot notebook. It is written using the python programming language. Python is an interpreted, object-oriented, high-level programming language with dynamic semantics.  Python supports modules and packages, which encourages program modularity and code reuse. The Python interpreter and the extensive standard library are available in source or binary form without charge for all major platforms, and can be freely distributed. One of these incorporated packes is Matplotlib


**CAO Final Notebook:**

- The beginning of the notebook we set the current date and time and set it as a now string to use during the importation of the CAO points.

**2021 Points Upload and Data Exploration:**

1) Data was initially copied into VScode into a folder named data. A sub folder was then created specifically for the 2021 data. It was manually worked on to remove pre-amble and other pre-columns and html code that were present in the folder. There may have been issues with reproducibility. All the course code, course name and points are in preformatted sections. There is no HTML tags on lines that we want to take the code from.
2) Using ctl+f in the VScode we can use the swatch function for regular expressions and use <.*>. or <[^>]*>
3) This will highlight all the html tags that have the open brackets. We hit the replace all and leave the replace box empty.
4) After this is completed we are left with college heading and other hyperlink lnes that we don't require in our dataset. 
5) Instead of trying to delete things in the folder we could use regular expression in python to **match** instead of **delete**. This is so we can produce a reproducible script.
6) Using the **import requests as rq** function we imported the 2021 CAO points directly from the CAO website as resp. The file path was created for the original data.
7) After trying to use regular experssions on the dataset we realised the dataset was encoded using UTF-8 and the Irish langauge symbol fada were posing a challenge to decode. After initally changing the code type to iso-8859-1 this didn't fix the issue due to a \x96 . To work around the encoding was changed to cp1252.
8) A regular expressions was compiled after several trial and error experiments and was given the name **re_course** to be used when itering through the dataset
9) The file path was then defined using the nowstr that was previously defined at the beginning of the notebook. 
9) The main body of code was then compiled by reading in the file path and using the for loop and if statements the code was first run through to decode the line using the cp1252 decoding function. Then use the regular expression pattern function for full match to use only lines that correspond to the re_compiler. The lines are then worked through using the if statement function to separate the course code,course title and round one points. Another if statent is used to separate out for round 2 points based on length of the round 1 points.Finally using regualar expression linesplit the headings are joined together in an array using a comma. The substrings are then rejoined with a commas in between using f.write function.
10) The print function is then used to determine the amount of lines afetr the code has run.
11) After using the code about we created a dataset called df2021 and saved it as a CSV file.

**2021 Points Upload and Data Exploration:**

1) The points on the CAO website for the year 2020 are in an excel format.
2) Using pandas we can read in the filepath easily. Pandas is an incredibly usefule module for dealing with spreadsheets. We can read in an excel file using pd.read_excel()
3) Initially when we directly use the website address to read in the excel file the format was incorrect. The first 10 row were then removed using skiprows function when reading in the file. This removed the preamble on the excel file. The 2020 cao points format is correct now for analysis.
4) To ensure the formatting is ok spot checks are conducted using the iloc function and looking at a random row and the last row to ensure we have all the courses.
5) The file path was saved and backed up in datafolder. In order to do the urllib request was used. The website was saved in the name url2020. This was then passed into the urlrq.urlretrieve function along with the file path for the original data.  
6) The file is then turned into a file path for pandas into csv and defined as path2020.
7) Path2020 is the saved as a new name df2020 using df2020.to_csv(path2020). 

**2019 Points Upload and Data Exploration:**

As I was working on this notebook everytime I ran the kernal it produced new files in the data folder because of the file paths created for 2021 and 2020 using the nowstring.
These had accumalated after a couple of weeks I decided to delete some. Unfortunately I deleted the 2019 edited version from the folder whie doing this. This was a big learnig curve to not ever delete data unless I'm 100% sure it's not required. Thankfully the steps below ensured it took minimal time to upload the 2019 points again:

1) Download original pdf file from the CAO website.
2) Open original pdf file in microsoft word.
3) Save Mircosoft Word's converted pdf in the docx format.
4) Resave word document for editing.
5) Delete headers and footers.
6) Delete preample in page 1.
7) Select all and copy to notepad++.
8) Delete blank lines and remove HEI headings and paste onto each course line respectively (using alt + scroll down).
9) Insert double quotes along the HEI title as this will make it easier to edit using regular expressions. 
10) Change backtick's to apostrophes.
11) Go to repleace all with \t (tab delimiter) and replace with comma(,) as it is a CSV file.
12) Many commas throughout the document so we couldn't load the dataframe as a csv file. Instead we went back to original format with the delimiter as the tab.
13) When reading data in the sep = '\t' was used as the delimiter for separating the columns.
14) Errors occured while loading this data because unknowningly there were some double tabs on the document. Fix was to replace \t\t with \t. DF was able to be read in after this.
15) I went back to the dataset and then replaced all ` back ticks ` with the correct ' forward tick mark.
16) The df2019 is then created using pandas to read in this edited text file and the sep = '\t' to separate the columns.

**Concat and Join Datasets**

- Begin with editing all three sets of CAO points and only using the code code and title.Once this is done we can concat all three edited datasets. The concatanated datasets were named 'allcourses'
- Once the concat was completed there was 3344 lines in total. The dataset was sorted using value codes. This revealed the duplication in the course code in the new dataset allcourses. To look at the duplicated row *allcourses[allcourses.duplicated()]* which revealed 1406 rows of duplicated code.
- A subset was created using just code and the when the duplicated code was run again this revealed 1692. However it was not taken into account that the duplicated code was also running on the index line. In order to ignore the index line *ignore_index=True* was used. This returned the dataset with 1652 lines.
- In order to check this dataset did not contain any duplicates we ran the code on the newly edited allcourses df and the return was empty indicating all the duplicates had been removed.
- As a checkpoint here I read this dataset to a csv file and viewed it. There was one completely empty row near the end of the dataset. I used numpy to fill the empty row with NAN and then used the dropna function to remove it. When I viewed the dataset after this it contained 1651 lines so the empty row had been removed.
- The code column of all three datasets was set as the index. 3 new datasets were then created using the index column and the R1 CAO points column from each dataset. Once this had been completed the 3 datasets were merged using the join function. 
- This dataset was further edited to remove the #,AQA, and NAN characters in the dataset. One anomaly I didn't correct was some NaN still remained even after code was run.
- I then changed the allcourses name to ac3 to make it eaier when writing code.
- All points columns were converted to numeric as dtypr float64. This was to ensure we could use descriptive code. To do this we needed the the dataset to be in numeric form.
- The above steps were repeated again but using the r2 points from all the 3 years.

**Data Analysis**
- Using the descibe function we analysed mean,min and max of points required for courses during the three years for Round 1 and Round 2.
- I then looked up soem information behing the courses which included GAMASAT and entrance exams. This points were artificially high and low due to other factor. Not just based on leaving cert points.
- Looking further into this we edited the dataset further to only include courses from 50-630 points. These would be the majority of courses that CAO points alone are required for. 
- 




