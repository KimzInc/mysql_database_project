# mysql_database_project
creating a database inventory and two tables, products and suppliers 

Using MySQL database workbench, create a new database called Inventory – your own name.
Create two tables within the database – Products and Suppliers and then enter the following data.

Products:
Make Product ID the primary key and set up each field with the appropriate data type and size.
ProductID, ProductName, Category, SupplierID, UnitsInStock, UnitPrice
(111, 'Ebony Carving', 'Art', 30, 120, 120.00),
(122, 'Talking Drum', 'Instrument', 30, 9, 55.00),
(123, 'Carved Polar Bear', 'Art', 20, 15, 250.00),
(136, 'Lacquer Dinner Set', 'Household', 10, 13, 85.00),
(137, 'Turquoise Earrings', 'Jewelry', 20, 5, 15.00),
(148, 'Opal Earrings', 'Jewelry', 10, 7, 110.00),
(189, 'Smoked Salmon', 'Food', 20, 15, 25.95),
(324, 'Hippo Carving', 'Art', 30, 15, 180.00),
(357, 'Maple Sugar Treats', 'Food', 20, 15, 80.50),
(552, 'Aztec Mask', 'Art', 40, 8, 55.00),
(554, 'Mahogany Salad Bowl', 'Household', 40, 8, 22.95),
(773, 'Hand Pipes', 'Instrument', 40, 18, 95.00),
(797, 'Jade Ring', 'Jewelry', 10, 8, 40.00),
(811, 'Soapstone Seal', 'Art', 20, 4, 300.00),
(986, 'Coral Pendant', 'Jewelry', 10, 9, 220.00)

Suppliers:
Make Supplier ID the primary key and set up each field with the appropriate data type and size.
SupplierID, SupplierName, Region
(10, 'Far East Imports', 'Asia'),
(20, 'America Arts', 'North America'),
(30, 'Kenya Crafts', 'Africa'),
(40, 'Rainforest Cooperative', 'Central America')


Create a form from the Products table and name it Products.  Include all the fields from the Products table in the form.

Create a report from the Suppliers table and name it Suppliers and Regions.  Include the Supplier Name and the Region in the report.  Do not include the Supplier ID.  Use Landscape Orientation for the report.
Create the following queries
    • Display the Product Name and Category for all the records in the Products table.  Save the query and name it Names and Categories.
    • Display the Product Name and Category for all records in the Products table with a Unit Price greater than $100.00.  Save the query and name it Large Price.
    • Display the Product Name, Category, Units In Stock, and Unit Price for all records in the Product table where the Product Name includes the word “Carving”.  Use a wildcard, not an OR condition.  Save the query and name it Carving Products.
    • Display the Product Name and Category for all records in the Products table with a Supplier ID of 20 and the Units In Stock less than 15.  Save the query and name it Low Stock.
    • Display the Product Name and Category for all records in the Products table with a Category of Art or a Supplier ID of 20.  Sort the records in descending order by Product Name.  Save the query and name it Art and North America.
    • Join the Products table and the Suppliers table.  Display the Product Name, Category and Supplier ID from the Products table and the Supplier Name and Region from the Supplier table.  Sort the records in ascending order by Region, and within Region, by Product Name.  Save the query and name it Products and Suppliers.
    • Display the Product Name, Category, Units In Stock, Unit Price, and Extended Price for all records in the Products table.  Calculate the extended price (Units In Stock * Unit Price).  Save the query and name it Extended Price.

CREATE DATABASE Inventory_Singh

-- Suppliers Table
CREATE TABLE Inventory_Singh.Suppliers (
    SupplierID INT PRIMARY KEY,
    SupplierName VARCHAR(100) NOT NULL,
    Region VARCHAR(50) NOT NULL
);

-- Products table
CREATE TABLE Inventory_Singh.Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100) NOT NULL,
    Category VARCHAR(50) NOT NULL,
    SupplierID INT NOT NULL,
    UnitsInStock INT NOT NULL,
    UnitPrice DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID)
);

-- insert values to Suppliers table
INSERT INTO Inventory_Singh.Suppliers (SupplierID, SupplierName, Region) 
VALUES (10, 'Far East Imports', 'Asia'),
(20, 'America Arts', 'North America'),
(30, 'Kenya Crafts', 'Africa'),
(40, 'Rainforest Cooperative', 'Central America');

-- insert values to Productst table
INSERT INTO Inventory_Singh.Products (ProductID, ProductName, Category, SupplierID, UnitsInStock, UnitPrice)
VALUES (111, 'Ebony Carving', 'Art', 30, 120, 120.00),
(122, 'Talking Drum', 'Instrument', 30, 9, 55.00),
(123, 'Carved Polar Bear', 'Art', 20, 15, 250.00),
(136, 'Lacquer Dinner Set', 'Household', 10, 13, 85.00),
(137, 'Turquoise Earrings', 'Jewelry', 20, 5, 15.00),
(148, 'Opal Earrings', 'Jewelry', 10, 7, 110.00),
(189, 'Smoked Salmon', 'Food', 20, 15, 25.95),
(324, 'Hippo Carving', 'Art', 30, 15, 180.00),
(357, 'Maple Sugar Treats', 'Food', 20, 15, 80.50),
(552, 'Aztec Mask', 'Art', 40, 8, 55.00),
(554, 'Mahogany Salad Bowl', 'Household', 40, 8, 22.95),
(773, 'Hand Pipes', 'Instrument', 40, 18, 95.00),
(797, 'Jade Ring', 'Jewelry', 10, 8, 40.00),
(811, 'Soapstone Seal', 'Art', 20, 4, 300.00),
(986, 'Coral Pendant', 'Jewelry', 10, 9, 220.00);


-- Queries
-- form 
SELECT * FROM Inventory_Singh.Products;



-- report 
SELECT SupplierName, Region FROM Inventory_Singh.Suppliers;

-- Names and Categories

SELECT ProductName, Category 
FROM Inventory_Singh.Products;

-- Large Price
SELECT ProductName, Category 
FROM Inventory_Singh.Products
WHERE UnitPrice > 100.00;

-- Carving Products
SELECT ProductName, Category, UnitsInStock, UnitPrice
FROM Inventory_Singh.Products
WHERE ProductName LIKE '%Carving%';

-- Low Stock
SELECT ProductName, Category
FROM Inventory_Singh.Products
WHERE SupplierID = 20 AND UnitsInStock < 15;


-- Art and North America
SELECT ProductName, Category
FROM Inventory_Singh.Products
WHERE Category = 'Art' OR SupplierID = 20
ORDER BY ProductName DESC;

-- Products and Suppliers

SELECT 
    p.ProductName, 
    p.Category, 
    p.SupplierID, 
    s.SupplierName, 
    s.Region
FROM 
    Inventory_Singh.Products p
JOIN 
    Inventory_Singh.Suppliers s
ON 
    p.SupplierID = s.SupplierID
ORDER BY 
    s.Region ASC, 
    p.ProductName ASC;

-- Extended Price
SELECT 
    ProductName,
    Category,
    UnitsInStock,
    UnitPrice,
    (UnitsInStock * UnitPrice) AS ExtendedPrice
FROM 
    Inventory_Singh.Products;






    
