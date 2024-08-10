# E-Commerce Customer Management

## Objective
You are tasked with managing customer profiles for an e-commerce platform. Your tasks include creating, updating, and deleting records related to customer information, contact details, and user logins.

## Activity - 1: Managing Customer Profile for Mark Tailor

### Scenario
Mark Tailor is a new customer on your e-commerce platform. You need to create his profile and update it with various details.


### Tasks
1. **Create Customer Profile**
   
   INSERT INTO Customer (FirstName, MiddleName, LastName, Roles)
   VALUES ('Mark', '', 'Tailor', 'Customer');
   

3. **Update Customer Name**
    UPDATE Customer
    SET MiddleName = 'K'
    WHERE FirstName = 'Mark' AND LastName = 'Tailor';


4. **Add Contact Information**
         -- Add an email address
      INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor'), 'Email', 'mark.tailor@example.com', 'General');
      -- Add a billing phone number
      INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor'), 'Phone', '123-456-7890', 'Billing');
      -- Add a shipping phone number
      INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor'), 'Phone', '098-765-4321', 'Shipping');


**4. Add Address Information**
      -- Add a shipping address
      INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor'), '123 Shipping St', 'Shipping City', 'SC', '12345', 'USA', 'Shipping');
      -- Add a billing address
      INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor'), '123 Billing St', 'Billing City', 'BC', '67890', 'USA', 'Billing');
      -- Make billing and shipping addresses the same
      UPDATE Address
      SET StreetAddress = '123 Billing St', City = 'Billing City', StateProvince = 'BC', PostalCode = '67890', Country = 'USA'
      WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor') AND Purpose = 'Shipping';
      -- Change the purpose of the billing address to General correspondence
      UPDATE Address
      SET Purpose = 'General correspondence'
      WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor') AND Purpose = 'Billing';
   

  **5..Modify Contact Information**
      -- Delete the current email address and add a new one
      DELETE FROM ContactInfo
      WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor') AND ContactType = 'Email';
      INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor'), 'Email', 'new.mark.tailor@example.com', 'General');
      -- Delete the current billing address and add a new one
      DELETE FROM Address
      WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor') AND Purpose = 'Billing';
      INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor'), '456 New Billing St', 'New Billing City', 'NBC', '54321', 'USA', 'Billing');
      -- Delete the current shipping address and add a new one
      DELETE FROM Address
      WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor') AND Purpose = 'Shipping';
      INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'Mark' AND LastName = 'Tailor'), '456 New Shipping St', 'New Shipping City', 'NSC', '98765', 'USA', 'Shipping');


## Activity - 2: Advanced Customer Management for John Hays

### Scenario
John Hays is an existing customer who requires more advanced management, including credit card information and system access.

### Tasks
1. **Create Customer Profile**
   INSERT INTO Customer (FirstName, MiddleName, LastName, Roles)
   VALUES ('John', '', 'Hays', 'Customer');

2. **Update Customer Name**
    UPDATE Customer
    SET MiddleName = 'B'
    WHERE FirstName = 'John' AND LastName = 'Hays';


3. **Add Contact Information**
       -- Add an email address
       INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
       VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays'), 'Email', 'john.hays@example.com', 'General');
       -- Add a billing phone number
       INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
       VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays'), 'Phone', '234-567-8901', 'Billing');
       -- Add a shipping phone number
       INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
       VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays'), 'Phone', '987-654-3210', 'Shipping');
   

4. **Add Payment Information**
        -- Create a credit card record
    INSERT INTO PaymentInformation (CustomerID, PaymentType, CardNumber, ExpirationDate, BillingAddressID)
    VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays'), 'Credit Card', '4111111111111111', '2025-12-31', 
    (SELECT AddressID FROM Address WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays') AND Purpose = 'Billing'));

5. **Manage System Access**
       -- Add a user login
    INSERT INTO UserLogin (CustomerID, Username, Password)
    VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays'), 'john.hays', 'securepassword');
     -- Assign a security group
    INSERT INTO UserLoginSecurityGroup (LoginID, SecurityGroupID)
    VALUES (
        (SELECT LoginID FROM UserLogin WHERE Username = 'john.hays'),
        (SELECT SecurityGroupID FROM SecurityGroup WHERE GroupName = 'Customer Management')
    );


6. **Modify Contact Information**
      -- Delete the current email address and add a new one
      DELETE FROM ContactInfo
      WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays') AND ContactType = 'Email';
      INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays'), 'Email', 'new.john.hays@example.com', 'General');
      -- Delete the current billing address and add a new one
      DELETE FROM Address
      WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays') AND Purpose = 'Billing';
      INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays'), '101 New Billing St', 'New Billing City', 'NBC', '54321', 'USA',        'Billing');
      -- Delete the current shipping address and add a new one
      DELETE FROM Address
      WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays') AND Purpose = 'Shipping';
      INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
      VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'John' AND LastName = 'Hays'), '101 New Shipping St', 'New Shipping City', 'NS


## Activity - 3: Comprehensive Customer Management for David Zeneski

### Scenario
David Zeneski is a new customer who requires a comprehensive setup, including multiple user logins and access to different parts of the e-commerce system.

### Tasks
1. **Create Customer Profile**
   
    INSERT INTO Customer (FirstName, MiddleName, LastName, Roles)
    VALUES ('David', '', 'Zeneski', 'Customer');

3. **Update Customer Name**
       UPDATE Customer
    SET MiddleName = 'R'
    WHERE FirstName = 'David' AND LastName = 'Zeneski';

4. **Add Contact Information**
          -- Add an email address
       INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
       VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), 'Email', 'david.zeneski@example.com', 'General');
       -- Add a billing phone number
       INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
       VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), 'Phone', '345-678-9012', 'Billing');
       -- Add a shipping phone number
       INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
       VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), 'Phone', '876-543-2109', 'Shipping');
   
      -- Add a shipping address
       INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
       VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), '456 Shipping St', 'Shipping City', 'SC', '23456', 'USA', 
       'Shipping');
       -- Add a billing address
       INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
       VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), '456 Billing St', 'Billing City', 'BC', '34567', 'USA', 
       'Billing');
       -- Make billing and shipping addresses the same
       UPDATE Address
       SET StreetAddress = '456 Billing St', City = 'Billing City', StateProvince = 'BC', PostalCode = '34567', Country = 'USA'
       WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski') AND Purpose = 'Shipping';
       -- Change the purpose of the billing address to General correspondence
       UPDATE Address
       SET Purpose = 'General correspondence'
       WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski') AND Purpose = 'Billing';

6. **Add Payment Information**
       -- Create a credit card record
    INSERT INTO PaymentInformation (CustomerID, PaymentType, CardNumber, ExpirationDate, BillingAddressID)
    VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), 'Credit Card', '5111111111111111', '2026-11-30',
    (SELECT AddressID FROM Address WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski') AND Purpose =     
    'Billing'));

7. **Manage System Access**
      -- Add two user logins
   INSERT INTO UserLogin (CustomerID, Username, Password)
   VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), 'david.zeneski1', 'password1');
   INSERT INTO UserLogin (CustomerID, Username, Password)
   VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), 'david.zeneski2', 'password2');
   -- Assign security groups to each login
   -- For the order management application
   INSERT INTO UserLoginSecurityGroup (LoginID, SecurityGroupID)
   VALUES (
       (SELECT LoginID FROM UserLogin WHERE Username = 'david.zeneski1'),
       (SELECT SecurityGroupID FROM SecurityGroup WHERE GroupName = 'Order Management')
   );
   -- For the customer management application
   INSERT INTO UserLoginSecurityGroup (LoginID, SecurityGroupID)
   VALUES (
       (SELECT LoginID FROM UserLogin WHERE Username = 'david.zeneski2'),
       (SELECT SecurityGroupID FROM SecurityGroup WHERE GroupName = 'Customer Management')
   );

8. **Modify Contact Information**
       --- Delete the current email address and add a new one
   DELETE FROM ContactInfo
   WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski') AND ContactType = 'Email';
   INSERT INTO ContactInfo (CustomerID, ContactType, ContactValue, Purpose)
   VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), 'Email', 'new.david.zeneski@example.com', 'General');
   -- Delete the current billing address and add a new one
   DELETE FROM Address
   WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski') AND Purpose = 'Billing';
   INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
   VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), '789 New Billing St', 'New Billing City', 'NBC', '45678', 'USA', 'Billing');
   -- Delete the current shipping address and add a new one
   DELETE FROM Address
   WHERE CustomerID = (SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski') AND Purpose = 'Shipping';
   INSERT INTO Address (CustomerID, StreetAddress, City, StateProvince, PostalCode, Country, Purpose)
   VALUES ((SELECT CustomerID FROM Customer WHERE FirstName = 'David' AND LastName = 'Zeneski'), '789 New Shipping St', 'New Shipping City', 'NSC', '56789', 'USA', 'Shipping');
