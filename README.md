# Sales Data Model Project in Power BI - Part 1

## Overview
This part of the project demonstrates the implementation of a dimensional data model (primarily star schema with snowflake elements) in Power BI using a sales dataset. The model transforms a flat CSV file into an optimized dimensional structure, improving data analysis capabilities and reporting performance.

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

# Sales and Budget Data Model Enhancement - Part 2

## Overview: 
This phase of the project extends the existing sales data model by incorporating budget data, demonstrating advanced data modeling techniques to handle many-to-many relationships and complex dimensional hierarchies.

## New Data Structure

### New Fact Table
**FactBudget** was introduced with the following fields:
* Value (measure)
* Date (foreign key)
* Scenario
* Original Category and Segment fields (later replaced with CatSeg Key)

## Data Modeling Challenges and Solutions

### Handling Many-to-Many Relationships
* Identified a potential many-to-many relationship between FactBudget and product dimension tables through Category
* Implemented a bridge table solution to resolve the many-to-many relationship
* Created a new dimension table (Dim CatSeg) to establish proper relationships

### Creation of Bridge Dimension
**Dim CatSeg** was created through the following steps:
* Extracted Category and Segment combinations from Dim Category
* Removed duplicates to ensure distinct Category-Segment pairs
* Created a surrogate key (CatSeg Key) using the index column technique
* Established as the central dimension for category-related attributes

### Data Transformation Process
1. **Merge Operations**
   * Merged Dim CatSeg with FactBudget to incorporate CatSeg Key
   * Performed similar merge operation with Dim Product
   * Based merge operations on Category and Segment columns

2. **Data Cleanup**
   * Removed redundant Category and Segment columns from FactBudget
   * Cleaned up Dim Product by removing duplicate category information
   * Maintained data integrity while reducing model complexity

## Model Optimization

### Relationship Management
* Established proper relationships between:
   * FactBudget and Dim Date through Date column
   * FactBudget and Dim CatSeg through CatSeg Key
   * Dim Product and Dim CatSeg through CatSeg Key
     
## Data Model Architecture
Final Data Model
![image](https://github.com/user-attachments/assets/7d8e4451-9fc1-4686-94c8-4de4c2ab08f7)
Sales table and related dimension tables
![image](https://github.com/user-attachments/assets/0bb796ec-61b9-4fb6-9718-d37422a3082c)
FactBudget and related dimension tables 
![image](https://github.com/user-attachments/assets/5a0eb62f-3f1b-4b74-8d38-7d1fdfe4fc07)

### Performance Considerations
* Implemented surrogate keys for efficient joins
* Removed redundant columns to reduce model size
* Optimized relationship cardinality for better query performance

## Technical Skills Demonstrated

### Advanced Data Modeling
* Resolution of many-to-many relationships
* Creation and implementation of bridge tables
* Surrogate key generation and management

### Data Transformation
* Complex merge operations
* Duplicate removal and data deduplication
* Column management and cleanup

### Dimensional Modeling
* Bridge dimension design and implementation
* Proper key management
* Relationship optimization

### Power BI Features Utilized
* Merge queries functionality
* Index column creation
* Relationship management
* Data model optimization techniques

## Business Intelligence Best Practices
* Maintained dimensional modeling standards
* Implemented proper key management
* Ensured data integrity across the model
* Created efficient paths for data analysis

## Results
The enhanced data model now supports:
* Integrated analysis of sales and budget data
* Proper handling of category-segment hierarchies
* Efficient querying across multiple fact tables
* Streamlined reporting capabilities

This phase of the project demonstrates advanced data modeling techniques and showcases the ability to handle complex business requirements while maintaining model efficiency and analytical capabilities.

## Tools Used
* Power BI Desktop
* Excel (source data)
