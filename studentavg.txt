import requests
import csv
from io import StringIO
from collections import defaultdict

url = "https://raw.githubusercontent.com/Surya-Gunnam/taskrepo/master/studentinfo.csv"
response = requests.get(url)
csv_text = response.text
csv_reader = csv.reader(StringIO(csv_text), delimiter='\t')

# Initialize the dictionary to store student grades
Students_Info = defaultdict(list)

# Skip the header row
headers = next(csv_reader)

# Parse the CSV file
for row in csv_reader:
    if len(row) != 3:
        continue
    Name, Subject, Grade = row
    Students_Info[Name].append(float(Grade))

# Calculate and print the average for each student
for Name, Grades in Students_Info.items():
    if Grades: 
        average_grade = sum(Grades) / len(Grades)
        print(f"{Name}'s average grade is {average_grade:.2f}")
