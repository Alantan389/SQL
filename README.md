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











