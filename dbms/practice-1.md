# Problem Statement: Designing a Database for E-Commerce Customer Management

## Objective
Design a database to manage customer profiles, contact details, addresses, and user logins for an e-commerce platform.

** create command--**
   **CREATE DATABASE ecommerce;**
   use ecommerce;
   
**1.-- Create the Customer table..**
 
CREATE TABLE Customer (
    CustomerID INT PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(50),
    MiddleName VARCHAR(50),
    LastName VARCHAR(50),
    Roles VARCHAR(100)
);
  
**2.-- Create the Contact Information table..**

CREATE TABLE ContactInfo (
    ContactID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerID INT,
    ContactType VARCHAR(20),
    ContactValue VARCHAR(100),
    Purpose VARCHAR(50),
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID)
);


**3.-- Create the Address table...**

CREATE TABLE Address (
    AddressID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerID INT,
    StreetAddress VARCHAR(100),
    City VARCHAR(50),
    StateProvince VARCHAR(50),
    PostalCode VARCHAR(20),
    Country VARCHAR(50),
    Purpose VARCHAR(50),
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID)
);


**4.-- Create the User Login table..**

CREATE TABLE UserLogin (
    LoginID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerID INT,
    Username VARCHAR(50),
    Password VARCHAR(255),
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID)
);

**5.-- Create the Security Group table..**

CREATE TABLE SecurityGroup (
    SecurityGroupID INT PRIMARY KEY AUTO_INCREMENT,
    GroupName VARCHAR(50)
);

**6.-- Create the User Login Security Group table..**

CREATE TABLE UserLoginSecurityGroup (
    LoginID INT,
    SecurityGroupID INT,
    PRIMARY KEY (LoginID, SecurityGroupID),
    FOREIGN KEY (LoginID) REFERENCES UserLogin(LoginID),
    FOREIGN KEY (SecurityGroupID) REFERENCES SecurityGroup(SecurityGroupID)
);

**7.-- Create the Payment Information table**

CREATE TABLE PaymentInformation (
    PaymentID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerID INT,
    PaymentType VARCHAR(20),
    CardNumber VARCHAR(20),
    ExpirationDate DATE,
    BillingAddressID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID),
    FOREIGN KEY (BillingAddressID) REFERENCES Address(AddressID)
);
