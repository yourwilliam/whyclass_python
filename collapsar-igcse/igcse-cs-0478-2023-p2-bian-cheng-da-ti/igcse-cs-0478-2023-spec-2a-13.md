# IGCSE cs 0478 2023 spec 2a 13

## IGCSE cs 0478 2023 spec 2a 13

The one-dimensional (1D) array StudentName\[] contains the names of students in a class. The two-dimensional (2D) array StudentMark\[] contains the mark for each subject, for each student. The position of each student’s data in the two arrays is the same, for example, the student in position 10 in StudentName\[] and StudentMark\[] is the same.

The variable ClassSize contains the number of students in the class. The variable SubjectNo contains the number of subjects studied. All students study the same number of subjects.

The arrays and variables have already been set up and the data stored.

Students are awarded a grade based on their average mark.

| Average mark                                 | Grade awarded |
| -------------------------------------------- | ------------- |
| greater than or equal to 70                  | distinction   |
| greater than or equal to 55 and less than 70 | merit         |
| greater than or equal to 40 and less than 55 | pass          |
| less than 40                                 | fail          |

Write a program that meets the following requirements:

* calculates the combined total mark for each student for all their subjects
* calculates the average mark for each student for all their subjects, rounded to the nearest whole number
* outputs for each student:
  * name
  * combined total mark
  * average mark
  * grade awarded
* calculates, stores and outputs the number of distinctions, merits, passes and fails for the whole class.

You must use pseudocode or program code and add comments to explain how your code works.

You do not need to initialise the data in the array.

### Python版初始化代码，练习的时候使用如下的代码

```python

import string
import random

#################################################
# Declare
#################################################

class_size = 100
subject_no = 10
student_name = []
student_mark = []

#################################################
# Initialize Data (not include)
#################################################

for student_index in range(class_size):
    student_name.append(''.join(random.choice(string.ascii_letters) for student_name_index in range(6)))
    StudentPoints = [random.randint(10, 100) for i in range(subject_no)]
    student_mark.append(StudentPoints)

#################################################
# For you to write
#################################################

# declare variables
total_mark = [0] * class_size
average_mark = [0] * class_size
subject_counter = 0
student_counter = 0
distinction_no = 0
merit_no = 0
pass_no = 0
fail_no = 0

DESTINCTION = 75
MERIT = 55
PASS = 40
# Add others you used in your program

```

### 图解

![](http://ossp.pengjunjie.com/mweb/17133764493152.jpg)

### Python版答案

```Python
import string
import random

#################################################
# Declare
#################################################

class_size = 100
subject_no = 10
student_name = []
student_mark = []

#################################################
# Initialize Data (not include)
#################################################

for student_index in range(class_size):
    student_name.append(''.join(random.choice(string.ascii_letters) for student_name_index in range(6)))
    StudentPoints = [random.randint(10, 100) for i in range(subject_no)]
    student_mark.append(StudentPoints)

#################################################
# For you to write
#################################################

# declare variables
total_mark = [0] * class_size
average_mark = [0] * class_size
subject_counter = 0
student_counter = 0
distinction_no = 0
merit_no = 0
pass_no = 0
fail_no = 0

DESTINCTION = 75
MERIT = 55
PASS = 40
# Add others you used in your program

for student_counter in range(class_size):
    for subject_counter in range(subject_no):
        total_mark[student_counter] = total_mark[student_counter] + student_mark[student_counter][subject_counter]
    average_mark[student_counter] = round(total_mark[student_counter] / subject_no)
    print("Name: ", student_name[student_counter])
    print("Combined total mark: ", total_mark[student_counter])
    print("Average mark: ", average_mark[student_counter])
    if average_mark[student_counter] >= DESTINCTION:
        distinction_no = distinction_no + 1
        print("Grade awarded: distinction")
    elif MERIT < average_mark[student_counter] < DESTINCTION:
        merit_no += 1
        print("Grade awarded: merit")
    elif PASS < average_mark[student_counter] < MERIT:
        pass_no += 1
        print("Grade awarded: pass")
    else:
        fail_no += 1
        print("Grade awarded: fail")

print("Number of Distinctions: ", distinction_no)
print("Number of merit: ", merit_no)
print("Number of pass: ", pass_no)
print("Number of fail: ", fail_no)

```
