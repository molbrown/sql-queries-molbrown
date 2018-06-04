For each of the questions below, add the following information to a Markdown file in your homework repo:

The original question text
Your final SQL query (which you must have run and validated on the included database)
The number of results returned (if more than one)
The specific result returned (if a single record is returned)

# Answers:

## **Find all time entries.**

*SQL query:*

SELECT *

FROM time_entries;

*Number of Results:*

500 rows returned

## **Find the developer who joined most recently.**

*SQL query:*

SELECT MAX(joined_on), name

FROM developers;

*Result:*

MAX(joined_on) | name
------------ | -------------
2015-07-10 | Dr. Danielle McLaughlin