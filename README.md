# Sales Data Model Project in Power BI

## Project Overview
This project demonstrates the implementation of a dimensional data model (primarily star schema with snowflake elements) in Power BI using a sales dataset. The model transforms a flat CSV file into an optimized dimensional structure, improving data analysis capabilities and reporting performance.

## Data Source
The original dataset was provided as an Excel CSV file containing sales transactions with the following fields:
* ProductID, Date, CustomerID, CampaignID, Units, Product, Category, Segment
* ManufacturerID, Manufacturer, Unit Cost, Unit Price
* Customer details: ZipCode, Email, Name
* Geographic information: City, State, Region, District, Country

## Data Model Architecture

![image](https://github.com/user-attachments/assets/54a66e65-240d-4a05-923b-e332c2ddb0b4)


### Fact Table
The central fact table **Sales** contains the core transaction metrics and foreign keys:
* Measures: Units, Unit Cost, Unit Price
* Foreign Keys: ProductID, CustomerID, Date
* Additional Fields: Date, Manufacturer

### Dimension Tables
The model includes four dimension tables:

#### 1. Dim Products
Contains product-related attributes:
* ProductID (Primary Key)
* Product
* Category
* Segment

#### 2. Dim Customers
Stores customer information:
* CustomerID (Primary Key)
* Email
* First Name
* Last Name
* ZipCode (Foreign Key to Dim Geography)

#### 3. Dim Geography
Contains location hierarchies:
* ZipCode (Primary Key)
* City
* State
* Region
* District
* Country

*Note: This dimension introduces a snowflake element as it connects to the fact table through Dim Customers rather than directly.*

#### 4. Dim Date
A dedicated date dimension marked as the official date table:
* Date
* Day of Week
* Month
* Month Number
* Quarter
* Week Number
* Year

## Model Characteristics

### Star Schema Implementation
The model primarily follows a star schema design with these key characteristics:
* Centralized fact table (Sales)
* Denormalized dimension tables
* Single join path between fact and most dimensions
* Simplified query paths for better performance

### Snowflake Element
The geographic dimension (Dim Geography) introduces a snowflake element by:
* Connecting to the fact table through Dim Customers
* Using ZipCode as the linking field between Dim Customers and Dim Geography

## Development Process
The project followed a structured approach to data modeling:

1. **Conceptual Modeling**
   * Identified core business entities
   * Defined relationships between entities
   * Determined fact and dimension candidates

2. **Logical Modeling**
   * Designed the star schema structure
   * Defined primary and foreign keys
   * Established table relationships

3. **Physical Modeling**
   * Implemented the model in Power BI
   * Created appropriate data types
   * Established relationships with correct cardinality
   * Optimized for performance

## Learning Outcomes
This project provided valuable insights into:
* Star schema design principles and implementation
* Data normalization importance and techniques
* Dimensional modeling best practices
* Power BI data modeling capabilities
* The balance between performance and model complexity

## Tools Used
* Power BI Desktop
* Excel (source data)
