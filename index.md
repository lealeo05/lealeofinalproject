---
# Do not edit the text between these lines!
layout: default
---

# COMP110 FINAL PROJECT (Leamsy Leon + Aminah )

## Introduction
For this final assignment for COMP110, we looked at student data to be able to improve the class in a way that is benefitical to it's steakholders (i.e. students, instructional team, academic institution or societal workforce). To begin answering this question we brainstormed some ideas on how to improve the class. 

The ideas are listed below:
1. This course should use pre-class readings because it will help students know what they are going to work on during class time, which benefits students who want to come to class more prepared.
2. This course should add recitations to help students have an organized time to work on assignments and get individual help, which benefits students who need extra support and structure.
3. This course should have different sections for different majors to focus more on each person’s strengths (for example, data science or computer science majors with experience could have a different section compared to majors taking the class as a prerequisite), which benefits students with different levels of experience.
4. This course should create an app to help students review the content in a more engaging way, which benefits students who learn better through interactive and mobile-friendly tools.
5. The course slides should be more descriptive to better support student learning and help with studying, which benefits all students, especially when reviewing material outside of class.

After brainstorming, we analyzed the data collected from our fellow classmates to see what questions can or cannot be answered. We concluded that "This course should add recitations to help students have an organized time to work on assignments and get individual help" cannot be fully analyzed because we do not currently have data that shows whether recitations improve student performance or understanding in this course. To answer this question in the future we can ask students if they feel they have done better in classes that include recitations and whether they think the extra one-on-one, structured help would improve their understanding. We could also collect data by offering optional recitation sessions and comparing performance or feedback from students who attend versus those who do not.

We then went through the other ideas and decided the best one to analyze was "This course should use pre-class readings because it will help students know what they are going to work on during class time. This idea is more valuable than the others brainstormed because it has already been used in the class, but the readings were optional and not assigned for every class. Making pre-class readings more consistent could help students better understand what is going to be covered before they come to class. This has the potential to improve overall student preparedness and engagement, making it a strong opportunity for improvement with a relatively simple change.

## Analysis
WRITE ANALYSIS HERE

The code we used to do this is written below with comments explaining the code:
import seaborn as sns # This imports the Seaborn library which is used to create statistical graphs. Sns is a short name for Seaborn.
import matplotlib.pyplot as plt # This imports the plotting tools from the Matplotlib library. This allows us to create the graphs we want.
from data_utils import (
    read_csv_rows,
    columnar,
    concat,
    select,
    convert_columns_to_int,
    count
) # This imports the functions we have in data_utils. This allows us to read our data files, manipulate them, and count values in columns.

sns.set_theme() # This sets the theme, to make the graphs look nicer.

izzi_rows = read_csv_rows("data/survey_izzi.csv") # This reads the data from survey_izzi.csv and stores it in a list of dictionaries called izzi_rows. Each dictionary represents a row of data, with the keys being the column names and the values being the data for that row.
alyssa_rows = read_csv_rows("data/survey_alyssa.csv") # This reads the data from survey_alyssa.csv and stores it in a list of dictionaries called alyssa_rows. Each dictionary represents a row of data, with the keys being the column names and the values being the data for that row.

izzi_table = columnar(izzi_rows) # This turns the data from izzi_rows into a column-oriented table, which is a dictionary. The keys of the dictionary are the column names, and the values are lists of the data in those columns.
alyssa_table = columnar(alyssa_rows) # This does the same for alyssa_rows.

combined = concat(izzi_table, alyssa_table) # This one combines the two tables into one table called combined. This allows us to work with all the data from both surveys at once.

selected = select(
    combined,
    ["own_examples", "pre_lecture_videos", "qz_effective"]
) # This selects only the columns we are interested in from the combined table.

clean = convert_columns_to_int(
    selected,
    ["own_examples", "pre_lecture_videos", "qz_effective"]
) # This converts the values in the selected columns from strings to integers. This allows us to do numerical analysis on the data.

own_freq = count(clean["own_examples"]) # This counts the frequency of each value in the "own_examples" column and stores it in a dictionary called own_freq. The keys of the dictionary are the unique values in the column, and the values are the counts of how many times each value appears.
pre_freq = count(clean["pre_lecture_videos"]) # This does the same for the "pre_lecture_videos" column.
qz_freq = count(clean["qz_effective"]) # This does the same for the "qz_effective" column.

plt.figure() # This create a new graph. This is necessary because we want to create multiple graphs, and if we don't create a new one, all the graphs will be drawn on top of each other.
sns.barplot(x=list(own_freq.keys()), y=list(own_freq.values())).set(title="Own Examples") # This creates a bar pot for the "own_examples" column. The x-axis has the unique values from the column, and the y-axis has the counts of how many times each value appears. The title of the graph is "Own Examples".

plt.figure()
sns.barplot(x=list(pre_freq.keys()), y=list(pre_freq.values())).set(title="Pre-Lecture Videos") # This also creates a bar plot but for the "pre_lecture_videos" column.

plt.figure()
sns.barplot(x=list(qz_freq.keys()), y=list(qz_freq.values())).set(title="Quizzes") # This also creates a bar plot but for the "qz_effective" column.

plt.show() # This displays all the graphs we have created. If we don't call this, the graphs will not be displayed.

Bar graphs made using this code:

<!-- This is a comment. Below, you'll see code for inserting an image. To make this image appear, update <custom-path>. To add an image, save it inside the imgs folder of this repository. -->
<img src="<custom-path>/static/imgs/logo.png" alt="Image of Comp110 rainbow logo. "  width="500"/>




## Conclusion
Using the data, it is inconclusive whether or not pre-lecture readings can help improve the class. In the analysis, we graphed the responses for "own_examples," "pre_lecture_videos," and "qz_effective." Both "qz_effective" and "pre_lecture_videos" showed a negatively skewed distribution, indicating that most of the responses were around 6–7. In contrast, "own_examples" had a more normal distribution, meaning most responses were around the middle (3–5).

Pre-lecture videos are similar to readings, and students generally think they help their understanding, which suggests that readings could also be helpful. These readings could also be used to study for quizzes since they provide material students can review, and students report that studying for quizzes is effective. Not many students currently create their own examples to study, but this could increase if they have readings to reflect on.

The reason this conclusion is inconclusive is because these ideas rely on assumptions, such as readings helping students create their own examples or improving studying. This change would also require students to spend more time on the course, which is already time-intensive due to coding assignments. One possible adjustment could be making assignments slightly shorter to balance the added workload.

To build more confidence in this idea, we could experimentally implement required pre-lecture readings for some class sections while keeping others the same, and then compare student performance, quiz scores, and feedback between the groups. We could also collect survey data asking students directly whether the readings improved their understanding, helped them study, or made them more likely to create their own examples. This additional data would help better determine if pre-lecture readings actually create value.

There are also trade-offs to consider. If the readings require a textbook, this could add a financial cost to a course that is currently free. It would also require more time from students and from the instructional team, who would need to assign or create the readings and adjust the course structure. Despite these trade-offs, the idea could still benefit student understanding and overall performance.