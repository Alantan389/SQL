# SQL



All of the questions in this
quiz pull from the open source Chinook Database. Please refer to the ER Diagram below and familiarize yourself with the table and
column names to write accurate queries and get the appropriate
answers.

![UAPENoOVEei4RQ5L9j9nDA_5042a1f0839511e8beb2b5b4ae9fa29a_ER-Diagram](https://user-images.githubusercontent.com/25523756/156111665-984e609b-190c-48ba-8748-77167d43bad6.png)


1. How many albums does the artist Led Zeppelin have? 

SELECT  COUNT(AlbumId) AS totalAlbumsCount FROM albums 
WHERE ArtistId=(SELECT ArtistId FROM artists WHERE name='Led Zeppelin')

<img width="157" alt="Screen Shot 2022-02-28 at 9 43 32 PM" src="https://user-images.githubusercontent.com/25523756/156112997-da706860-df7f-4fcb-b376-61941133bfeb.png">





2. Create a list of album titles and the unit prices for the artist "Audioslave".

How many records are returned?

Only 25 records will be shown in the output so please look at the bottom of the output to see how many records were retrieved.


SELECT artists.Name, tracks.UnitPrice FROM 
((albums INNER JOIN artists ON albums.ArtistId=artists.ArtistId)
INNER JOIN tracks ON tracks.AlbumId=albums.AlbumId)
WHERE artists.Name='Audioslave'

<img width="410" alt="Screen Shot 2022-02-28 at 9 48 32 PM" src="https://user-images.githubusercontent.com/25523756/156112979-bb508d6d-2032-4e18-961e-2bffb9ef915a.png">






3. Find the first and last name of any customer who
does not have an invoice. Are there any customers returned from the query?  

select customers.FirstName,customers.LastName,
invoices.InvoiceId
from customers left join invoices
on customers.CustomerId=invoices.CustomerId
where invoices.InvoiceId is null;

<img width="311" alt="Screen Shot 2022-02-28 at 9 49 31 PM" src="https://user-images.githubusercontent.com/25523756/156112934-a10e748b-9a30-4d8d-bf07-8db6d64ebefc.png">






4. Find the total price for each album.
What is the total price for the album "Big Ones" ?


SELECT SUM(tracks.UnitPrice) AS Total_Price,albums.Title FROM tracks
LEFT JOIN albums on albums.AlbumId=tracks.AlbumId 
WHERE albums.Title="Big Ones"

<img width="222" alt="Screen Shot 2022-02-28 at 9 51 16 PM" src="https://user-images.githubusercontent.com/25523756/156112894-ad838909-505f-4456-99c2-05f2019a7fc4.png">






5. How many records are created when you apply a Cartesian join to the invoice and invoice items table?

Only 25 records will be shown in the output so please look at the bottom of the output to see how many records were retrieved.

SELECT  count(*)total_records FROM invoices CROSS JOIN invoice_items ;

<img width="141" alt="Screen Shot 2022-02-28 at 9 52 02 PM" src="https://user-images.githubusercontent.com/25523756/156112853-1111486b-f5a6-49a8-afa4-0a04afcdd447.png">


```


------------------------------------------------------------------------------------------


```
![ChinookDatabaseSchema](https://user-images.githubusercontent.com/25523756/156966524-f4d49ec8-91f1-49ba-8cd5-92c3d16db836.png)

1. Using a subquery, find the names of all the tracks for the album "Californication".
   What is the title of the 8th track ?
   
   SELECT t.Name, t.AlbumId From Tracks t WHERE t.AlbumId=(SELECT a.AlbumId
   FROM Albums a WHERE a.Title='Californication');
  <img width="379" alt="Screen Shot 2022-03-06 at 8 13 51 PM" src="https://user-images.githubusercontent.com/25523756/156967647-7fba048d-b2f3-47c9-802a-ccfd2fbb3cdf.png">

```
   
```   
   
2.  Find the total number of invoices for each customer along with the customer's full name, city and email.
    After running the query described above, what is the email address of the 5th person, Franti??ek Wichterlov??? Enter the answer below (feel free to copy and paste).
  
  select c.CustomerId, c.FirstName, c.LastName, c.City, c.Email, COUNT(i.InvoiceId)
from Customers c inner join Invoices i
on c.CustomerId = i.CustomerId
Group by c.CustomerId ;  
<img width="782" alt="Screen Shot 2022-03-06 at 8 14 15 PM" src="https://user-images.githubusercontent.com/25523756/156967672-291bc111-5569-4c30-906a-445fb4fb97fe.png">
```
   
```  



3. Retrieve the track name, album, artistID, and trackID for all the albums.
What is the song title of trackID 12 from the "For Those About to Rock We Salute You" album? Enter the answer below.

SELECT T.Name, T.TrackId, R.ArtistId,A.Title FROM Tracks T 
INNER JOIN Albums A ON A.AlbumId=T.AlbumId 
INNER JOIN Artists R ON R.ArtistId=A.ArtistId;

<img width="768" alt="Screen Shot 2022-03-06 at 8 20 39 PM" src="https://user-images.githubusercontent.com/25523756/156967694-68b2abd6-cf63-47d8-99bf-9e7ae23ac7ee.png">

```
   
```  



    
    

4. Retrieve a list with the managers last name, and the last name of the employees who report to him or her.
After running the query described above, who are the reports for the manager named Mitchell (select all that apply)?

SELECT M.LastName Manager_Last_Name , E.LastName Employee_Last_Name
FROM Employees E 
LEFT JOIN Employees M    
ON E.ReportsTo=M.EmployeeID;

<img width="323" alt="Screen Shot 2022-03-06 at 8 20 48 PM" src="https://user-images.githubusercontent.com/25523756/156967735-a27aef4c-a081-443a-9a7c-d6b2b2243af7.png">

```
   
```  





5. Find the name and ID of the artists who do not have albums.
After running the query described above, two of the records returned have the same last name. Enter that name below.

SELECT Al.AlbumID, Al.Title, Ar.ArtistId, Ar.Name  
FROM Artists Ar LEFT JOIN Albums Al 
ON Ar.ArtistId = Al.ArtistId
WHERE Al.Title is NULL

<img width="457" alt="Screen Shot 2022-03-06 at 8 21 07 PM" src="https://user-images.githubusercontent.com/25523756/156967748-741812ce-7142-4845-b804-b770dcb3bbb9.png">


```
   
```  



6. Use a UNION to create a list of all the employee's and customer's first names and last names ordered by the last name in descending order.

After running the query described above, determine what is the last name of the 6th record? Enter it below. Remember to order things in descending order to be sure to get the correct answer

select e.FirstName, e.LastName
from Employees e
UNION
select c.FirstName, c.LastName
from Customers c
order by c.LastName DESC

<img width="376" alt="Screen Shot 2022-03-06 at 8 21 19 PM" src="https://user-images.githubusercontent.com/25523756/156967768-ff435fe7-8868-4f48-b2d4-934fc54480b5.png">


```
   
```  





7. See if there are any customers who have a different city listed in their billing city versus their customer city.

<img width="163" alt="Screen Shot 2022-03-06 at 8 21 29 PM" src="https://user-images.githubusercontent.com/25523756/156967779-ea49a3e0-338d-4045-9c33-23775447fd03.png">




```
------------------------------------------------------------------------------------------
```

![ChinookDatabaseSchema](https://user-images.githubusercontent.com/25523756/158047849-d210fe90-5037-4f1d-ba43-1cf9d5da29fb.png)


```
```

1. Pull a list of customer ids with the customer???s full name, and address, along with combining their city and country together. Be sure to make a space in between these two and make it UPPER CASE. (e.g. LOS ANGELES USA)


SELECT C.CustomerId,C.FirstName,C.LastName,C.Address,
C.Country,C.City FROM Customers C;

<img width="619" alt="Screen Shot 2022-03-12 at 10 33 48 PM" src="https://user-images.githubusercontent.com/25523756/158048312-08584121-f156-443c-9f83-b4038f1437d3.png">





2. Create a new employee user id by combining the first 4 letters of the employee???s first name with the first 2 letters of the employee???s last name. Make the new field lower case and pull each individual step to show your work.

SELECT C.FirstName, SUBSTR(C.FirstName,1,4) AS First4,
C.LastName,SUBSTR(C.LastName, 1,2) AS Last2,
LOWER(SUBSTR(C.FirstName,1,4)|| SUBSTR(C.LastName,1,2))
AS New_Employee_User FROM Customers c;

<img width="510" alt="Screen Shot 2022-03-12 at 10 34 08 PM" src="https://user-images.githubusercontent.com/25523756/158048323-181c7c41-9e54-4297-b2e7-396b4d0f4275.png">





3.Show a list of employees who have worked for the company for 15 or more years using the current date function. Sort by lastname ascending.

SELECT E.LastName,E.FirstName,Date('now')-E.HireDate
AS Years_Hired FROM Employees E WHERE
Years_Hired >= 15
ORDER BY E.LastName ASC

<img width="290" alt="Screen Shot 2022-03-12 at 10 34 19 PM" src="https://user-images.githubusercontent.com/25523756/158048326-56002214-aa31-484a-8b24-cebbaaa16da0.png">





4.Profiling the Customers table, answer the following question.

SELECT C.PostalCode,C.Address,C.Company,C.Fax,
C.Phone,C.FirstName FROM Customers C
WHERE PostalCode is Null

<img width="597" alt="Screen Shot 2022-03-12 at 10 35 22 PM" src="https://user-images.githubusercontent.com/25523756/158048333-4f12970d-3ce0-4cf4-b5c2-76c7d8f01b12.png">






5. Find the cities with the most customers and rank in descending order.

SELECT C.City,COUNT(C.CustomerId)
FROM Customers C
GROUP BY C.City
ORDER BY COUNT(C.CustomerId)
DESC

<img width="345" alt="Screen Shot 2022-03-12 at 10 35 35 PM" src="https://user-images.githubusercontent.com/25523756/158048340-521a17c1-9532-4c87-ba76-b089de7644f4.png">





6. Create a new customer invoice id by combining a customer???s invoice id with their first and last name while ordering your query in the following order: firstname, lastname, and invoiceID.

SELECT C.FirstName || C.LastName || I.InvoiceId 
AS NEW_Invoice_ID
FROM Customers C INNER JOIN Invoices I 
ON C.CustomerID=I.CustomerId
WHERE NEW_Invoice_ID LIKE  "AstridGruber%"


<img width="162" alt="Screen Shot 2022-03-12 at 10 35 47 PM" src="https://user-images.githubusercontent.com/25523756/158048343-3fe016c9-1e8a-4054-b2b2-d3f26a134794.png">













