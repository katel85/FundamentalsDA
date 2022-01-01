# FundamentalsDA

This repositiory contains two notebooks called CAO and Pyplot. They are jupyter notebooks that have been constructed to attain a better understaing of the fundamentals of data analytics.

The first notebook in this repositiry is the pyplot notebook. It is written using the python programming language. Python is an interpreted, object-oriented, high-level programming language with dynamic semantics.  Python supports modules and packages, which encourages program modularity and code reuse. The Python interpreter and the extensive standard library are available in source or binary form without charge for all major platforms, and can be freely distributed. One of these incorporated packes is Matplotlib


**CAO Final Notebook**

- The beginning of the notebook we set the current date and time and set it as a now string to use during the importation of the CAO points.

- 2021 Points Upload and Data Exploration:

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