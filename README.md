# sql-exercises

# Dave Harms SQL statements

SELECT FirstName || " " || LastName, CustomerId, Country 
From Customer 
Where Country <> "USA"

SELECT *
From Customer 
Where Country = "Brazil"

SELECT FirstName || " " || LastName, InvoiceId, InvoiceDate, BillingCountry
From Customer JOIN Invoice 
ON Customer.CustomerId = Invoice.CustomerId
Where Country = "Brazil"

SELECT * 
FROM Employee
WHERE Title = "Sales Support Agent"

SELECT BillingCountry
FROM Invoice
GROUP BY BillingCountry

SELECT *
FROM Invoice JOIN Customer
ON Invoice.CustomerId = Customer.CustomerId
WHERE Customer.Country = 'Brazil'

SELECT FirstName || " " || LastName, Total, Customer.Country, SupportRepId 
FROM Customer JOIN Invoice
ON Invoice.CustomerId = Customer.CustomerId;

SELECT *
FROM Invoice
WHERE strftime('%Y', InvoiceDate) = '2009' OR strftime('%Y', InvoiceDate) = '2011';

SELECT count(InvoiceLine.InvoiceId)
FROM InvoiceLine JOIN Invoice
ON InvoiceLine.InvoiceId = Invoice.InvoiceId
Where Invoice.InvoiceId = 37;

SELECT Invoice.InvoiceId, count(Invoice.InvoiceId)
FROM InvoiceLine JOIN Invoice
ON InvoiceLine.InvoiceId = Invoice.InvoiceId
GROUP BY Invoice.InvoiceId;

SELECT Track.Name 
FROM Track JOIN InvoiceLine
ON Track.TrackId = InvoiceLine.InvoiceLineId;

SELECT Track.Name, Artist.Name
FROM InvoiceLine 
JOIN Track ON InvoiceLine.TrackId = Track.TrackId
JOIN Album ON Track.AlbumId = Album.AlbumId
JOIN Artist ON Album.ArtistId = Artist.ArtistId;

SELECT Invoice.BillingCountry, count(Invoice.InvoiceId)
FROM Invoice
GROUP BY Invoice.BillingCountry;

SELECT count(Track.TrackId) As "Number of Tracks"
FROM Track
JOIN PlaylistTrack ON PlaylistTrack.TrackId = Track.TrackId
JOIN Playlist ON Playlist.PlaylistId = PlaylistTrack.PlaylistId;  

SELECT Track.Name, Album.Title, MediaType.Name, Genre.Name
FROM Track
LEFT JOIN Album ON Album.AlbumId = Track.AlbumId
LEFT JOIN MediaType ON MediaType.MediaTypeId = Track.MediaTypeId
LEFT JOIN Genre ON Genre.GenreId = Track.GenreId;  

## 17
SELECT Invoice.InvoiceId, count(InvoiceLine.InvoiceLineId)
FROM Invoice
JOIN InvoiceLine ON InvoiceLine.InvoiceId = Invoice.InvoiceId
GROUP BY Invoice.InvoiceId

## 18
SELECT Employee.FirstName || " " || Employee.LastName AS "Full Name", Employee.EmployeeId, Employee.Title, printf("$%.2f", sum(Invoice.Total)) As "Total Sales" 
FROM Employee
JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId
JOIN Invoice ON Invoice.CustomerId = Customer.CustomerId
WHERE Employee.Title = "Sales Support Agent"
GROUP BY "Full Name";

## 19
SELECT Employee.FirstName || " " || Employee.LastName AS "Full Name", Employee.EmployeeId, Employee.Title, printf("$%.2f", sum(Invoice.Total)) As "Total Sales" 
FROM Employee
JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId
JOIN Invoice ON Invoice.CustomerId = Customer.CustomerId
WHERE Employee.Title = "Sales Support Agent" AND strftime('%Y', InvoiceDate) = '2009'
GROUP BY "Full Name";
*Jane Peacock*

## 20
SELECT Employee.FirstName || " " || Employee.LastName AS "Full Name", Employee.EmployeeId, Employee.Title, printf("$%.2f", sum(Invoice.Total)) As "Total Sales" 
FROM Employee
JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId
JOIN Invoice ON Invoice.CustomerId = Customer.CustomerId
WHERE Employee.Title = "Sales Support Agent" AND strftime('%Y', InvoiceDate) = '2010'
GROUP BY "Full Name";
*Marge Park*

## 21
*Jane Peacock*

## 22
SELECT Employee.FirstName || " " || Employee.LastName AS "Full Name", count(Customer.CustomerId) As "Total Customers"
FROM Employee
JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId
GROUP BY "Full Name";

## 23
SELECT Invoice.BillingCountry, printf("$%.2f", sum(Invoice.Total)) As "Total Sales"
FROM Invoice
GROUP BY Invoice.BillingCountry;

## 24
SELECT Name, max("Total Tracks") FROM (
SELECT Name, sum(Quantity) As "Total Tracks"
FROM Track
JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId
JOIN Invoice ON InvoiceLine.InvoiceId = Invoice.InvoiceId
WHERE strftime('%Y', InvoiceDate) = '2013'
GROUP BY Name)
*Eruption*

## 25
SELECT Name, sum(Quantity) As "Total Tracks"
FROM Track
JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId
JOIN Invoice ON InvoiceLine.InvoiceId = Invoice.InvoiceId
GROUP BY Name 
ORDER BY "Total Tracks" DESC
Limit 5
"The Trooper"   "5"
"Eruption"  "4"
"Hallowed Be Thy Name"  "4"
"Sure Know Something"   "4"
"The Number Of The Beast"   "4"

## 26
SELECT Artist.Name, sum(InvoiceLine.Quantity) As "Total Units Sold"
FROM Artist
JOIN Album ON Album.ArtistId = Artist.ArtistId
JOIN Track ON Track.AlbumId = Album.AlbumId
JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId
GROUP BY Artist.Name
ORDER By "Total Units Sold" DESC;
*Iron Maiden, U2, Metallica*

## 27
SELECT MediaType.Name, sum(InvoiceLine.Quantity) As "Total Units Sold"
FROM MediaType
JOIN Track ON Track.MediaTypeId = MediaType.MediaTypeId
JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId
GROUP BY MediaType.Name
ORDER By "Total Units Sold" DESC;
*mpeg*
