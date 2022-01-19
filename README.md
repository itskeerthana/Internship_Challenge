# Internship_Challenge
Question 1:
Question 1: Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

a.	Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 

	

b.	What metric would you report for this dataset?
	
c.	What is its value?
        The correct AOV values is $357.92


Question 2:
For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

a.	How many orders were shipped by Speedy Express in total?

Answer: 54	

Code Used: 
SELECT Shippers.ShipperName,COUNT(Orders.OrderID) AS TotalOrders FROM Orders
LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
GROUP BY ShipperName;

b.	What is the last name of the employee with the most orders?

ANSWER:   PEACOCK,40


Code Used:

SELECT  Employees.LastName , COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders
LEFT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY LastName
ORDER BY COUNT(Orders.OrderID) DESC;



c.	What product was ordered the most by customers in Germany?
 
Answer:  PRODUCT NAME: CAMEMBERT PIERROT
         Quantity - 40 
         Orders - 300
	 Total Ordered - 12000
         
Code Used:           CREATE VIEW Product_Ordered AS
		     SELECT Orders.OrderID, Customers.Country, OrderDetails.Quantity,  Products.ProductName
		     FROM Orders, OrderDetails
		     JOIN Customers ON Orders.CustomerID= Customers.CustomerID
	 	     JOIN Products ON OrderDetails.ProductID=Product.ProductID
		     WHERE Country=’Germany’;

	                     CREATE VIEW Product_Orders AS 
		     SELECT ProductName, Quantity, COUNT(*) as ‘Orders’
		     FROM Products_Ordered
		     GROUP BY ProductName;
			
		     SELECT ProductName, Quantity, Orders, (Quantity* Orders) AS TotalOrdered
		     FROM Product_Orders
		     ORDER BY TotalOrdered desc
		     LIMIT 1;
