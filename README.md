-- Create Products Table
CREATE TABLE Products (
    ProductID INT PRIMARY KEY AUTO_INCREMENT,
    ProductName VARCHAR(100),
    StockQuantity INT,
    Price DECIMAL(10,2)
);

-- Procedure to Add a Product
DELIMITER $$
CREATE PROCEDURE AddProduct (
    IN p_name VARCHAR(100),
    IN p_quantity INT,
    IN p_price DECIMAL(10,2)
)
BEGIN
    INSERT INTO Products(ProductName, StockQuantity, Price)
    VALUES (p_name, p_quantity, p_price);
END $$
DELIMITER ;

-- Procedure to Update Stock
DELIMITER $$
CREATE PROCEDURE UpdateStock (
    IN p_id INT,
    IN p_quantity INT
)
BEGIN
    UPDATE Products
    SET StockQuantity = StockQuantity + p_quantity
    WHERE ProductID = p_id;
END $$
DELIMITER ;

-- Procedure to Get Product Details
DELIMITER $$
CREATE PROCEDURE GetProductDetails (
    IN p_id INT
)
BEGIN
    SELECT ProductID, ProductName, StockQuantity, Price
    FROM Products
    WHERE ProductID = p_id;
END $$
DELIMITER ;
CALL AddProduct('Laptop', 10, 50000.00);
CALL AddProduct('Mouse', 50, 500.00);
CALL UpdateStock(1, 5);        -- Add 5 laptops
CALL GetProductDetails(1);     -- Show laptop details
