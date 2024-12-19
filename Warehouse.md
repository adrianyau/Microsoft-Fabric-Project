1. In the Workspace, click on 'New Item' and select 'Warehouse'.
<img width="975" alt="Screenshot 2024-12-19 at 9 18 40 AM" src="https://github.com/user-attachments/assets/d681d0c0-30d9-48c9-8ce2-d86ed2b739a3" />

2. Add a new schema:
```sql

CREATE schema mavenmarket;
```

<img width="1440" alt="Screenshot 2024-12-19 at 1 34 11 PM" src="https://github.com/user-attachments/assets/a7ca4ec6-2303-4ee6-93ac-1eaab2d2b532" />

3. After running the Pipeline Activity, the tables should be uploaded under the 'mavenmarket' schema.
<img width="1429" alt="Screenshot 2024-12-19 at 2 19 15 PM" src="https://github.com/user-attachments/assets/fe037d96-46c4-4471-8842-19d2a25d4c05" />

4. Select 'New SQL query' to make queries for each table.

```sql
   SELECT TOP 10
    CAST(date AS date) AS date, 
    CAST(DATEADD(day, -DATEDIFF(day, -1, date) % 7, date) AS date) AS start_of_week,
    CAST(DATENAME(weekday, date) AS varchar(30)) AS name_of_day,
    CAST(DATEADD(month, DATEDIFF(month, 0, date), 0) AS date) AS start_of_month, 
    CAST(DATENAME(month, date) AS varchar(30)) AS name_of_month, 
    CONCAT('Q',DATEPART(quarter, date)) AS quarter_of_year, 
    YEAR(date) AS year
   FROM mavenmarket.calendar
```
|date      |start_of_week|name_of_day|start_of_month|name_of_month|quarter_of_year|year|
|----------|-------------|-----------|--------------|-------------|---------------|----|
|1997-01-01|1996-12-29   |Wednesday  |1997-01-01    |January      |Q1             |1997|
|1997-01-02|1996-12-29   |Thursday   |1997-01-01    |January      |Q1             |1997|
|1997-01-03|1996-12-29   |Friday     |1997-01-01    |January      |Q1             |1997|
|1997-01-04|1996-12-29   |Saturday   |1997-01-01    |January      |Q1             |1997|
|1997-01-05|1997-01-05   |Sunday     |1997-01-01    |January      |Q1             |1997|
|1997-01-06|1997-01-05   |Monday     |1997-01-01    |January      |Q1             |1997|
|1997-01-07|1997-01-05   |Tuesday    |1997-01-01    |January      |Q1             |1997|
|1997-01-08|1997-01-05   |Wednesday  |1997-01-01    |January      |Q1             |1997|
|1997-01-09|1997-01-05   |Thursday   |1997-01-01    |January      |Q1             |1997|
|1997-01-10|1997-01-05   |Friday     |1997-01-01    |January      |Q1             |1997|


