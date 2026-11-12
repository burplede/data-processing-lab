# data-processing-lab

## Lab Overview
In this lab we process data from Cities.csv which has a list of cities in Europe with their country, latitude, longitude and temperature. We answer questions like the average temperature of all cities, cities in Germany, max temperature in Italy etc.

The code was written in different ways for each commit:
- Commit 1: normal code with loops
- Commit 2: procedural style using filter_items and aggregate functions with lambda
- Commit 3: OOP style using classes (DataLoader and Table)

## Project Structure
```
data-processing-lab/
├── README.md              # this file
├── Cities.csv             # the dataset
└── data_processing.py     # the code
```

## Design Overview

**DataLoader class**
- used to load the csv file
- attribute: base_path - the folder where the csv file is. If you dont give one it uses the folder that data_processing.py is in
- load_csv(filename) - opens the csv file and returns the data as a list of dictionaries (each row is one dictionary)

**Table class**
- stores the data as a table
- attributes:
  - table_name - name of the table e.g. 'cities'
  - table - list of dictionaries (the rows)
- methods:
  - __init__(table_name, table) - sets the table name and the data
  - filter(condition) - returns a new Table with only the rows where condition is True. condition is a function like a lambda
  - aggregate(function, aggregation_key) - gets all the values from the column aggregation_key and puts them into function (for example sum, max, average). Values that are numbers get converted to float first because they are strings in the csv
  - __str__ - for printing the table

Since filter returns a Table you can call aggregate right after it, for example:
```python
my_table1.filter(lambda x: x['country'] == 'Italy').aggregate(lambda x: max(x), 'temperature')
```

## How to test and run
You need Python 3. Run this in the project folder:
```
python3 data_processing.py
```
It runs the test code at the bottom of the file and prints the answers (average temp of all cities, cities in Germany, cities in Spain above 12°C, number of unique countries, average temp in Germany and max temp in Italy).
