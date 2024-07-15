# Problem Statement: Designing a Database for E-Commerce Customer Management

## Objective
Design a database to manage customer profiles, contact details, addresses, and user logins for an e-commerce platform.

## Requirements

1. **Customer Information**
    - Each customer has a unique identifier.
    - A customer can have a first name, middle name, and last name.
    - A customer can have multiple roles (e.g., Customer).

2. **Contact Information**
    - A customer can have multiple contact mechanisms, including email addresses and phone numbers.
    - Contact mechanisms should store information like email addresses and phone numbers with associated purposes (e.g., billing, shipping).

3. **Address Information**
    - A customer can have multiple addresses.
    - Addresses should include details such as street address, city, state/province, postal code, and country.
    - Addresses can have different purposes (e.g., billing, shipping, general correspondence).

4. **User Logins**
    - Each customer can have one or more user logins.
    - User logins should include a username and password.
    - Each user login can be associated with one or more security groups that determine access rights to different parts of the system.

5. **Payment Information**
    - A customer can have multiple payment methods, including credit cards.
    - Payment information should include details such as credit card number, expiration date, and billing address.


## Deliverables

 **ER Diagram**
    - Create an Entity-Relationship (ER) diagram to represent the tables and relationships.


## Instructions
- Ensure the database design supports all the requirements specified.
- Focus on data integrity and relationships between tables.
- Use appropriate data types for each column.
- Implement primary keys and foreign keys to maintain referential integrity.
