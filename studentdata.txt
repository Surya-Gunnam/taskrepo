import requests
import csv
from io import StringIO

url = "https://raw.githubusercontent.com/Surya-Gunnam/taskrepo/master/studentinfo.csv"
response = requests.get(url)
csv_text = response.text
csv_reader = csv.reader(StringIO(csv_text), delimiter='\t')
for row in csv_reader:
    print(row)
