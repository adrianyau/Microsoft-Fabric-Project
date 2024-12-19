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

##### Calendar
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


##### Customers
```sql
SELECT TOP 10
    CAST(customer_id AS NUMERIC) AS customer_id,
    customer_acct_num,
    CONCAT(first_name,' ', last_name) AS full_name,
    customer_address,
    customer_city,
    customer_state_province,
    customer_postal_code,
    customer_country,
    CAST(birthdate AS DATE) AS birthdate,
    YEAR(birthdate) AS birth_year,
    marital_status,
    yearly_income,
    gender,
    total_children,
    CASE
        WHEN total_children > 0 THEN 'Y'
        ELSE 'N'
        END has_children,
    num_children_at_home,
    education,
    CAST(acct_open_date AS DATE) AS acct_open_date,
    member_card,
    occupation,
    homeowner
FROM mavenmarket.customers
```
|customer_id|customer_acct_num|full_name|customer_address|customer_city|customer_state_province|customer_postal_code|customer_country|birthdate |birth_year|marital_status|yearly_income|gender|total_children|has_children|num_children_at_home|education          |acct_open_date|member_card|occupation    |homeowner|
|-----------|-----------------|---------|----------------|-------------|-----------------------|--------------------|----------------|----------|----------|--------------|-------------|------|--------------|------------|--------------------|-------------------|--------------|-----------|--------------|---------|
|35         |87771052718      |Ed Young |Rt. 470 Box A   |Merida       |Yucatan                |69940               |Mexico          |1920-04-17|1920      |M             |$30K - $50K  |M     |5             |Y           |1                   |Partial College    |1992-09-21    |Bronze     |Skilled Manual|Y        |
|1447       |13038234700      |Anthony Ghysels|8964 Dumbarton Street|La Cruz      |Sinaloa                |70672               |Mexico          |1952-11-23|1952      |M             |$70K - $90K  |M     |1             |Y           |1                   |Bachelors Degree   |1990-07-10    |Bronze     |Professional  |Y        |
|2094       |17556732296      |Nancy Moreno|9233 Pepperidge Way|Acapulco     |Guerrero               |70849               |Mexico          |1945-07-17|1945      |M             |$90K - $110K |F     |2             |Y           |1                   |Partial High School|1994-03-26    |Bronze     |Management    |Y        |
|2433       |20083099603      |Moyie Cortese|7544 Olivera Rd.|La Cruz      |Sinaloa                |25454               |Mexico          |1928-08-12|1928      |M             |$30K - $50K  |M     |1             |Y           |1                   |High School Degree |1994-02-14    |Bronze     |Skilled Manual|Y        |
|2974       |23905108000      |Lorraine Ardell|5404 Panoramic Ave|Acapulco     |Guerrero               |93738               |Mexico          |1947-06-12|1947      |M             |$30K - $50K  |M     |1             |Y           |1                   |High School Degree |1992-01-04    |Bronze     |Skilled Manual|N        |
|3032       |24360541701      |Betty Tobias|5439 McElroy Court|Acapulco     |Guerrero               |39825               |Mexico          |1970-05-20|1970      |M             |$30K - $50K  |F     |2             |Y           |1                   |High School Degree |1994-08-27    |Bronze     |Skilled Manual|Y        |
|4531       |35667871236      |Anatole Sisk|1463 Lincoln Dr |Acapulco     |Guerrero               |47599               |Mexico          |1976-09-09|1976      |M             |$90K - $110K |M     |1             |Y           |1                   |Bachelors Degree   |1994-04-06    |Bronze     |Management    |Y        |
|5481       |42885159300      |Linda Brown|3229 Mark Twain Dr.|Merida       |Yucatan                |16241               |Mexico          |1958-06-17|1958      |M             |$30K - $50K  |F     |4             |Y           |1                   |High School Degree |1993-04-22    |Bronze     |Skilled Manual|Y        |
|6603       |52399458885      |Colleen Bowen|4350 Laguna St  |Merida       |Yucatan                |58352               |Mexico          |1919-05-02|1919      |M             |$30K - $50K  |F     |5             |Y           |1                   |High School Degree |1992-03-06    |Bronze     |Manual        |N        |
|7745       |62001209259      |Douglas Jegier|5979 Leisure Lane|Acapulco     |Guerrero               |73201               |Mexico          |1911-01-08|1911      |M             |$30K - $50K  |M     |2             |Y           |1                   |High School Degree |1990-04-26    |Bronze     |Manual        |Y        |


##### Products
```sql
SELECT TOP 10
    CAST(product_id AS NUMERIC) AS product_id,
    product_brand,
    product_name,
    product_sku,
    CAST(product_retail_price AS FLOAT) AS product_retail_price,
    ROUND(CAST(product_retail_price AS FLOAT) * 0.9, 2) AS discount_price,
    CAST(product_cost AS FLOAT) AS product_cost,
    CAST(product_weight AS FLOAT) AS product_weight,
    COALESCE(recyclable, 0) AS recyclable,
    COALESCE(low_fat, 0) AS low_fat
FROM mavenmarket.products
```
|product_id|product_brand|product_name|product_sku|product_retail_price|discount_price|product_cost|product_weight|recyclable|low_fat|
|----------|-------------|------------|-----------|--------------------|--------------|------------|--------------|----------|-------|
|45        |Club         |Club Sour Cream|14866315722|0.53                |0.48          |0.25        |13.6          |0         |0      |
|94        |Golden       |Golden Apple Cinnamon Waffles|16446555256|0.62                |0.56          |0.25        |7.9           |1         |0      |
|144       |Denny        |Denny Glass Cleaner|67840190529|0.51                |0.46          |0.25        |20.3          |1         |0      |
|147       |Denny        |Denny D-Size Batteries|52095012068|0.64                |0.58          |0.25        |13            |1         |0      |
|384       |Moms         |Moms Sliced Turkey|49593787789|0.54                |0.49          |0.25        |14.7          |1         |1      |
|596       |Landslide    |Landslide Hot Chocolate|69221592545|0.64                |0.58          |0.25        |10.4          |0         |1      |
|651       |Bravo        |Bravo Chicken Ramen Soup|66987923979|0.8                 |0.72          |0.25        |15            |0         |1      |
|709       |Imagine      |Imagine Frozen Sausage Pizza|47281391024|0.57                |0.51          |0.25        |16.9          |1         |1      |
|769       |Cormorant    |Cormorant D-Size Batteries|96734759211|0.59                |0.53          |0.25        |21            |0         |0      |
|784       |Cormorant    |Cormorant Large Sponge|69949565529|0.52                |0.47          |0.25        |8.17          |1         |0      |


##### Regions
```sql
SELECT TOP 10
    CAST(region_id AS NUMERIC) AS region_id,
    sales_district,
    sales_region
FROM mavenmarket.regions
```
|region_id |sales_district|sales_region|
|----------|--------------|------------|
|1         |San Francisco |Central West|
|2         |Mexico City   |Mexico Central|
|3         |Los Angeles   |South West  |
|4         |Guadalajara   |Mexico West |
|5         |Vancouver     |Canada West |
|6         |Victoria      |Canada West |
|7         |San Diego     |South West  |
|8         |San Diego     |South West  |
|9         |San Diego     |South West  |
|10        |San Diego     |South West  |


##### Returns

```sql
SELECT TOP 10
    CAST(return_date AS date) AS return_date,
    CAST(product_id AS NUMERIC) AS product_id,
    CAST(store_id AS NUMERIC) AS store_id,
    CAST(quantity AS NUMERIC) AS quantity
FROM mavenmarket.returns
```
|return_date|product_id|store_id |quantity|
|-----------|----------|---------|--------|
|1998-03-12 |180       |9        |2       |
|1998-04-08 |1506      |9        |2       |
|1998-04-09 |117       |9        |2       |
|1998-05-13 |246       |9        |2       |
|1998-05-14 |187       |9        |2       |
|1998-07-30 |313       |9        |2       |
|1998-07-30 |1488      |9        |2       |
|1998-09-13 |936       |9        |2       |
|1998-11-02 |135       |9        |2       |
|1998-11-03 |1316      |9        |2       |


##### Stores
```sql
SELECT TOP 10
    CAST(store_id AS NUMERIC) AS store_id,
    CAST(region_id AS NUMERIC) AS region_id,
    store_type,
    store_name,
    store_street_address,
    store_city,
    store_state,
    store_country,
    CONCAT(store_city,', ', store_state,', ', store_country) AS full_address,
    store_phone,
    LEFT(store_phone, 3) AS area_code,
    CAST(first_opened_date AS date) AS first_opened_date,
    CAST(last_remodel_date AS date) AS last_remodel_date,
    CAST(total_sqft AS numeric) AS total_sqft,
    CAST(grocery_sqft AS numeric) AS grocery_sqft
FROM mavenmarket.stores




SELECT CAST(store_id AS NUMERIC) AS store_id, CAST(region_id AS NUMERIC) AS region_id
FROM mavenmarket.stores


SELECT CONCAT(store_city,', ', store_state,', ', store_country) AS full_address
FROM mavenmarket.stores


SELECT store_phone, LEFT(store_phone, 3) AS area_code
FROM mavenmarket.stores
```
|store_id  |region_id |store_type|store_name|store_street_address     |store_city   |store_state|store_country|full_address                |store_phone |area_code|first_opened_date|last_remodel_date|total_sqft|grocery_sqft|
|----------|----------|----------|----------|-------------------------|-------------|-----------|-------------|----------------------------|------------|---------|-----------------|-----------------|----------|------------|
|1         |28        |Supermarket|Store 1   |2853 Bailey Rd           |Acapulco     |Guerrero   |Mexico       |Acapulco, Guerrero, Mexico  |262-555-5124|262      |1982-01-09       |1990-12-05       |23593     |17475       |
|2         |78        |Small Grocery|Store 2   |5203 Catanzaro Way       |Bellingham   |WA         |USA          |Bellingham, WA, USA         |605-555-8203|605      |1970-04-02       |1973-06-04       |28206     |22271       |
|3         |76        |Supermarket|Store 3   |1501 Ramsey Circle       |Bremerton    |WA         |USA          |Bremerton, WA, USA          |509-555-1596|509      |1959-06-14       |1967-11-19       |39696     |24390       |
|4         |27        |Gourmet Supermarket|Store 4   |433 St George Dr         |Camacho      |Zacatecas  |Mexico       |Camacho, Zacatecas, Mexico  |304-555-1474|304      |1994-09-27       |1995-12-01       |23759     |16844       |
|5         |4         |Small Grocery|Store 5   |1250 Coggins Drive       |Guadalajara  |Jalisco    |Mexico       |Guadalajara, Jalisco, Mexico|801-555-4324|801      |1978-09-18       |1991-06-29       |24597     |15012       |
|6         |47        |Gourmet Supermarket|Store 6   |5495 Mitchell Canyon Road|Beverly Hills|CA         |USA          |Beverly Hills, CA, USA      |958-555-5002|958      |1981-01-03       |1991-03-13       |23688     |15337       |
|7         |3         |Supermarket|Store 7   |1077 Wharf Drive         |Los Angeles  |CA         |USA          |Los Angeles, CA, USA        |477-555-7967|477      |1971-05-21       |1981-10-20       |23598     |14210       |
|8         |26        |Deluxe Supermarket|Store 8   |3173 Buena Vista Ave     |Merida       |Yucatan    |Mexico       |Merida, Yucatan, Mexico     |797-555-3417|797      |1958-09-23       |1967-11-18       |30797     |20141       |
|9         |2         |Mid-Size Grocery|Store 9   |1872 El Pintado Road     |Mexico City  |DF         |Mexico       |Mexico City, DF, Mexico     |439-555-3524|439      |1955-03-18       |1959-06-07       |36509     |22450       |
|10        |24        |Supermarket|Store 10  |7894 Rotherham Dr        |Orizaba      |Veracruz   |Mexico       |Orizaba, Veracruz, Mexico   |212-555-4774|212      |1979-04-13       |1982-01-30       |34791     |26354       |




