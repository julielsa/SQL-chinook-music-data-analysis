# SQL-Chinook Music Analysis
The Chinook database represents a digital media store, including tables for artists, albums, media tracks, invoices, and customers.

### Dataset 
[Click here to download dataset](https://cdn.fs.teachablecdn.com/dRmwOLQsS22FVFbXfh3x)

### Methodology
1. Data Understanding: Reviewed the structure of the Chinook database, which includes tables for artists, albums, media tracks, invoices, and customers.
2. Objective Definition: To evaluate employee performance, analyze customer and market trends, and catalog insights.
3. Query Formulation:

   Crafted specific SQL queries to extract relevant data for analysis:
    -  Customers (full names, customer ID, and country) not in the US.
    -  Customers specifically from Brazil and then invoices for customers from Brazil.
    -  Employees who are Sales Agents.
    -  Unique list of billing countries from the Invoice table.
    -  Invoices associated with each sales agent.
    -  Show the Invoice Total, Customer name, Country, and Sales Agent name for all invoices and customers.
    -  Identify purchased track names with each invoice line ID.
    -  Identify the purchased track name AND artist name with each invoice line ID.
5. Data Extraction and Analysis:
     - Executed the SQL queries to retrieve and analyze the data.
     - Interpreted the results to draw meaningful insights.


### Database Diagram
The Chinook database has 11 tables in it. This visualization highlights where the tables are related. 
![chinook diagram](https://github.com/julielsa/SQL-chinook-music-data-analysis/blob/main/chinook%20diagram.png)

### Area of Skills

These SQL skills collectively enable complex data retrieval and manipulation, allowing for comprehensive data analysis and insights generation.

#### Summary of SQL Skills Used
- Basic Querying: SELECT, WHERE
- Filtering Data: WHERE, BETWEEN
- Joining Tables: INNER JOIN, LEFT JOIN
- Removing Duplicates: DISTINCT
- Aggregation: COUNT, SUM
- Aliasing: AS
- Complex Joins: Combining multiple tables using various join operations
- Column Selection and Formatting: Selecting specific columns and renaming them for clarity

### Results & Recommendation
#### Results
--Show Customers (their full names, customer ID, and country) who are not in the US. 
```
SELECT customerid
,FirstName
,LastName
,Country
FROM chinook.customers
WHERE Country <> 'USA';
```

--Show only the Customers from Brazil.
```
SELECT customerid
,FirstName
,LastName
,Country
FROM chinook.customers
WHERE Country = 'Brazil';
```
--Find the Invoices of customers who are from Brazil.
```
SELECT 
customers.FirstName
,customers.LastName
,invoices.invoiceID
,invoices.InvoiceDate
,invoices.BillingCountry
FROM chinook.invoices
LEFT JOIN chinook.customers
ON invoices.customerid = customers.customerid
WHERE invoices.BillingCountry = 'Brazil';
```

--Show the Employees who are Sales Agents.
```
SELECT Title
,FirstName
,LastName
FROM chinook.employees
WHERE Title= 'Sales Support Agent'
;
```

--Unique list of billing countries from the Invoice table.
```
SELECT distinct
BillingCountry
FROM chinook.invoices;
```

--Provide a query that shows the invoices associated with each sales agent.
```
SELECT inv.invoiceid
,emp.FirstName
,emp.Lastname
FROM chinook.employees as emp
JOIN chinook.Customers as cust ON cust.SupportRepId = emp.EmployeeId
JOIN chinook.Invoices as Inv ON Inv.CustomerId = cust.CustomerId; 
```

--Show the Invoice Total, Customer name, Country, and Sales Agent name for all invoices and customers.
```
SELECT emp.LastName, emp.Firstname, cust.FirstName, cust.LastName, cust.Country, inv.total
FROM chinook.employees emp 
JOIN chinook.Customers cust ON cust.SupportRepId = emp.EmployeeId
JOIN chinook.Invoices Inv ON Inv.CustomerId = cust.CustomerId; 
```

--Write a query that includes the purchased track name with each invoice line ID.
```
SELECT t.Name, i.InvoiceLineId
FROM chinook.Invoice_items i
JOIN chinook.Tracks t 
ON i.TrackId = t.TrackId;
```

--Write a query that includes the purchased track name AND artist name with each invoice line ID.
```
SELECT ar.name as Artist, t.Name as Track, i.InvoiceLineId
FROM chinook.Invoice_items i
LEFT JOIN chinook.tracks t 
ON i.TrackID=t.TrackID
INNER JOIN chinook.albums a
ON a.AlbumID=t.AlbumID
LEFT JOIN chinook.artists ar
ON ar.ArtistID=a.ArtistID;
```

#### Recommendations
1. Market Expansion and Customer Trends:
     - Focus marketing efforts on countries with growing customer bases outside the US.
     - Develop targeted marketing campaigns for Brazilian customers based on their purchasing patterns and preferences.

2. Data Utilization for Strategic Decisions:
     - Leverage insights from the unique list of billing countries to identify potential new markets for expansion.
     - Use detailed invoice data to streamline billing processes and improve customer service.

By following this methodology and implementing the recommendations, the Chinook digital media store can enhance employee performance, better understand customer and market trends, and make informed strategic decisions to drive growth.

