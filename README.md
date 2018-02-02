# Microsoft Sync Framwork
Synchronizing SQL Server and SQL Express, This repository will help you quickly ramp up on basic database synchronization concepts.

Prerequisite for this repository are as follow 

You need to create a sample SQL Server database that you will use later in a synchronization. Use following script to create database and table that are required for this project 

For more detail you can visit : https://msdn.microsoft.com/en-us/library/ff928700(v=SQL.110).aspx

-Server Database: SyncDB
-Client Database: SyncExpressDB

`USE [master]
GO

IF EXISTS(SELECT name FROM sys.databases WHERE name = 'SyncDB')
DROP DATABASE SyncDB

CREATE DATABASE [SyncDB] 
GO

USE [SyncDB]
GO

CREATE TABLE [dbo].[Products](
[ID] [int] NOT NULL,
[Name] [nvarchar](50) NOT NULL,
[ListPrice] [money] NOT NULL
      
      CONSTRAINT [PK_Products] PRIMARY KEY CLUSTERED ([ID] ASC)
)

GO

CREATE TABLE [dbo].[Orders](
[OrderID] [int] NOT NULL,
[ProductID] [int] NOT NULL,
[Quantity] [int] NOT NULL,
[OriginState] [nvarchar](2) NOT NULL,
    CONSTRAINT [PK_Orders] PRIMARY KEY CLUSTERED ([OrderID] ASC,[ProductID] ASC)
)
GO

ALTER TABLE [dbo].[Orders]  WITH CHECK ADD  CONSTRAINT [FK_Orders_Products] FOREIGN KEY([ProductID])
REFERENCES [dbo].[Products] ([ID])
GO

ALTER TABLE [dbo].[Orders] CHECK CONSTRAINT [FK_Orders_Products]
GO

INSERT INTO Products VALUES (1, 'PC', 400)
INSERT INTO Products VALUES (2, 'Laptop', 600)
INSERT INTO Products VALUES (3, 'NetBook', 300)
INSERT INTO Orders VALUES (1, 1, 2, 'NC')
INSERT INTO Orders VALUES (2, 2, 1, 'NC')
INSERT INTO Orders VALUES (3, 1, 5, 'WA')
INSERT INTO Orders VALUES (3, 3, 10, 'WA')
INSERT INTO Orders VALUES (4, 2, 4, 'WA')`
