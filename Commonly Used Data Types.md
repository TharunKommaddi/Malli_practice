### Common SQL Data Types and Examples

#### 1. **INT**
- **Description**: Represents an integer.
- **Example**: Used for storing a count of items, like the number of users.
  ```sql
  CREATE TABLE Users (
      UserID INT,
      Username VARCHAR(100)
  );
  ```

#### 2. **VARCHAR**
- **Description**: A variable-length string.
- **Example**: Used for storing names, email addresses, or any text with a variable length.
  ```sql
  CREATE TABLE Customers (
      CustomerID INT,
      Name VARCHAR(255)
  );
  ```

#### 3. **DATE**
- **Description**: Stores a date in YYYY-MM-DD format.
- **Example**: Used for storing a specific date, like a birthday.
  ```sql
  CREATE TABLE Employees (
      EmployeeID INT,
      BirthDate DATE
  );
  ```

#### 4. **DECIMAL**
- **Description**: Stores exact numeric data with fixed decimal points. Good for financial data where precision is crucial.
- **Example**: Used for storing prices or other monetary values.
  ```sql
  CREATE TABLE Products (
      ProductID INT,
      Price DECIMAL(10, 2)  -- Allows values up to 99999999.99
  );
  ```

#### 5. **BOOLEAN**
- **Description**: Stores TRUE or FALSE values.
- **Example**: Used for storing simple flags like whether a user is active.
  ```sql
  CREATE TABLE Logins (
      LoginID INT,
      IsActive BOOLEAN
  );
  ```

#### 6. **TEXT**
- **Description**: Stores long-form text data.
- **Example**: Ideal for storing large amounts of text, such as articles or descriptions.
  ```sql
  CREATE TABLE Articles (
      ArticleID INT,
      Content TEXT
  );
  ```

#### 7. **DATETIME**
- **Description**: Stores date and time together in YYYY-MM-DD HH:MM:SS format.
- **Example**: Used for recording precise events, like the exact time of a transaction.
  ```sql
  CREATE TABLE Transactions (
      TransactionID INT,
      TransactionTime DATETIME
  );
  ```
