# Stock Data Importer to SSMS

This project provides SQL scripts to create tables for storing stock index data and stored procedures to import CSV data into these tables.

## 1. Create Tables

### NIFTY_BANK Table

````sql
CREATE TABLE NIFTY_BANK (
    Date DATE,
    Opens DECIMAL(18,4),
    High DECIMAL(18,4),
    Low DECIMAL(18,4),
    Closes DECIMAL(18,4),
    AdjClose DECIMAL(18,4),
    Volume BIGINT
);
````

### NIFTY_50 Table

````sql
CREATE TABLE NIFTY_50 (
    Date DATE,
    Opens DECIMAL(18,4),
    High DECIMAL(18,4),
    Low DECIMAL(18,4),
    Closes DECIMAL(18,4),
    AdjClose DECIMAL(18,4),
    Volume BIGINT
);
````

## 2. Create Stored Procedures
ImportCSVData Procedure
````sql

CREATE PROCEDURE ImportCSVData
    @TableName NVARCHAR(128),
    @FilePath NVARCHAR(255)
AS
BEGIN
    DECLARE @SQL NVARCHAR(MAX);

    SET @SQL = '
    BULK INSERT ' + QUOTENAME(@TableName) + '
    FROM ' + QUOTENAME(@FilePath, '''') + '
    WITH (
        FIELDTERMINATOR = '','',
        ROWTERMINATOR = ''\n'',
        FIRSTROW = 2
    );';

    EXEC sp_executesql @SQL;
END;
````

## 3. Import CSV Files
To import CSV files into the respective tables, execute the following script. Adjust the file paths and table names as needed.

````sql

DECLARE @FilePath NVARCHAR(255);
DECLARE @TableName NVARCHAR(128);

-- Example for importing multiple files to their respective tables

-- Import NIFTY_BANK CSV file
SET @FilePath = 'D:\Pending Projects\Stock Data\Stock\Index\indices\NIFTY BANK.csv';
SET @TableName = 'NIFTY_BANK';
EXEC ImportCSVData @TableName, @FilePath;

-- Import NIFTY_50 CSV file
SET @FilePath = 'D:\Pending Projects\Stock Data\Stock\Index\indices\NIFTY 50.csv';
SET @TableName = 'NIFTY_50';
EXEC ImportCSVData @TableName, @FilePath;
````

# Just Run Step 3 for Daily Data
