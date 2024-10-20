create database labrary_books_inventory;
 use labrary_books_inventory;
 -- Create Books Table
CREATE TABLE Books (
                     BookID INT PRIMARY KEY AUTO_INCREMENT,
					 Title VARCHAR(255) NOT NULL,
                     Author VARCHAR(255),
                     Quantity INT
				   );
                   
 INSERT INTO Books (Title, Author, Quantity)
VALUES ('The Alchemist', 'Paulo Coelho', 5),('animal','ranjan shah',5);
                  
UPDATE Books
SET Quantity = Quantity - 1 WHERE bookid=1;

delete from books where bookid = 2;

select * from books;


-- Create Members Table
CREATE TABLE Members (
                       MemberID INT PRIMARY KEY AUTO_INCREMENT,
					   FirstName VARCHAR(100),
                       LastName VARCHAR(100),
                       Email VARCHAR(255) UNIQUE,
                       PhoneNumber VARCHAR(15),
                       MembershipDate DATE
                     );
			
INSERT INTO Members (FirstName, LastName, Email, PhoneNumber, MembershipDate)
VALUES ('John', 'cena', 'john.cena@gmail.com', '1234567890', '2024-10-20'),('jone','jones','jbones@gmail.com','2345678901','2024-10-20');

UPDATE Members
SET Email = 'jonh.cena2@gmail.com'
WHERE MemberID = 1;

delete from members where memberid = 2;

select * from members;

-- Create Transactions Table
CREATE TABLE Transactions (
                            TransactionID INT PRIMARY KEY AUTO_INCREMENT,
                            BookID INT,
						    MemberID INT,
                            TransactionType ENUM('Borrow', 'Return'),
                            TransactionDate DATE,
                            FOREIGN KEY (BookID) REFERENCES Books(BookID),
                            FOREIGN KEY (MemberID) REFERENCES Members(MemberID)
					);

INSERT INTO Transactions (BookID, MemberID, TransactionType, TransactionDate)
VALUES (1, 1, 'Borrow', '2024-10-20');

-- To retrieve all borrowed/returned books

SELECT Books.Title, Members.FirstName, Members.LastName, Transactions.TransactionDate
FROM Transactions
INNER JOIN Books ON Transactions.BookID = Books.BookID
INNER JOIN Members ON Transactions.MemberID = Members.MemberID
WHERE Transactions.TransactionType = 'Borrow';
