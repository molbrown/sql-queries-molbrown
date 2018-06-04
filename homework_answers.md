For each of the questions below, add the following information to a Markdown file in your homework repo:

The original question text
Your final SQL query (which you must have run and validated on the included database)
The number of results returned (if more than one)
The specific result returned (if a single record is returned)

# Answers:

### **Find all time entries.**

**SQL query:**<br>
SELECT *<br>
FROM time_entries;<br>

**Number of Results:**<br>
500 rows returned<br><br>


### **Find the developer who joined most recently.**

**SQL query:**<br>
SELECT MAX(joined_on), name<br>
FROM developers;<br>

**Result:**<br>
MAX(joined_on) | name <br>
------------ | ------------- <br>
2015-07-10 | Dr. Danielle McLaughlin <br>
<br>

### **Find the number of projects for each client.**

**SQL query:**<br>
SELECT clients.name, COUNT(projects.id) AS project_count<br>
FROM clients<br>
LEFT JOIN projects<br>
ON clients.id = projects.client_id<br>
GROUP BY clients.id;<br>

**Number of Results:**<br>
12 rows returned<br><br>

### **Find all time entries, and show each one's client name next to it.**
**SQL query:**<br>
SELECT clients.name, time_entries.*<br>
FROM time_entries<br>
JOIN projects ON time_entries.project_id = projects.id<br>
JOIN clients ON projects.client_id = clients.id<br>

**Number of Results:**<br>
500 rows returned<br><br>

### **Find all developers in the "Ohio sheep" group.**

**SQL query:**<br>
SELECT developers.*<br>
FROM groups<br>
JOIN group_assignments ON groups.id = group_assignments.group_id<br>
JOIN developers ON group_assignments.developer_id = developers.id<br>
WHERE groups.name = 'Ohio sheep';<br>

**Number of Results:**<br>
3 rows returned<br><br>

### **Find the total number of hours worked for each client.**

**SQL query:**<br>
SELECT clients.name, SUM(time_entries.duration) AS total_hours<br>
FROM clients<br>
LEFT JOIN projects ON projects.client_id = clients.id <br>
LEFT JOIN  time_entries ON time_entries.project_id = projects.id<br>
GROUP BY clients.name;<br>

**Number of Results:**<br>
12 rows returned<br><br>

### **Find the client for whom Mrs. Lupe Schowalter (the developer) has worked the greatest number of hours.**

**SQL query:**<br>
SELECT SUM(time_entries.duration) AS total_hours, clients.name<br>
FROM developers <br>
JOIN time_entries ON developers.id = time_entries.developer_id <br>
JOIN  projects ON time_entries.project_id = projects.id<br>
JOIN clients ON projects.client_id = clients.id<br>
WHERE developers.name = "Mrs. Lupe Schowalter"<br>
GROUP BY clients.name<br>
ORDER BY total_hours DESC <br>
LIMIT 1;

**Result:**
total_hours | name
------------ | -------------
11 | Kuhic-Bartoletti
<br>

### **List all client names with their project names (multiple rows for one client is fine). Make sure that clients still show up even if they have no projects.**

**SQL query:**<br>
SELECT clients.name, projects.name<br>
FROM clients<br>
LEFT JOIN projects ON clients.id = projects.client_id;<br>

**Number of Results:**<br>
33 rows returned<br><br>

### **Find all developers who have written no comments.**

**SQL query:**<br>
SELECT developers.*<br>
FROM developers<br>
LEFT JOIN comments ON comments.developer_id = developers.id<br>
WHERE comments.id IS NULL;<br>

**Number of Results:**<br>
13 rows returned<br><br>

### **Find all developers with at least five comments.**

**SQL query:**<br>
SELECT COUNT(comments.id) as count_comment, developers.*<br>
FROM developers<br>
LEFT JOIN comments ON comments.developer_id = developers.id<br>
GROUP BY developers.id<br>
HAVING count_comment >= 5;<br>

**Result:**
count_comment | id | name 
------------ | ------------- | ------------- 
5 | 45 | Joelle Hermann
<br>

### **Find the developer who worked the fewest hours in January of 2015.**

**SQL query:**<br>
SELECT SUM(time_entries.duration) as work_hours, developers.*<br>
FROM developers<br>
LEFT JOIN time_entries ON developers.id = time_entries.developer_id<br>
WHERE time_entries.worked_on >= '2015-01-01 00:00:00' <br>
       and time_entries.worked_on < '2015-02-01 00:00:00'<br>
GROUP BY(developers.id)<br>
ORDER BY work_hours ASC<br>
LIMIT 1;<br>

**Result:**
work_hours | id | name 
------------ | ------------- | ------------- 
0 | 7 | Ms. Tremayne Kuhn
<br>



