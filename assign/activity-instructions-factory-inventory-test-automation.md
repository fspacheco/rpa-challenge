# Test Automation Assignment: Factory Inventory Management System

## Learning Objectives

By completing this assignment, you will:

* Practice writing automated UI tests with Robocorp/Playwright
* Learn to identify and document software defects
* Understand test case design and coverage
* Gain experience with real-world test automation scenarios

## Assignment Overview

Your task is to test a Factory Inventory Management System used to track parts and materials in a manufacturing facility. There are some bugs in the system. Your job is to create automated tests using Robocorp/Playwright to verify the system works correctly and **identify** the bugs.

This assignment is to be completed by teams of 2 students.

## System Description

The Factory Inventory Management System is a web-based application that allows factory managers to:
* Add new inventory items (parts, components, raw materials)
* View all items in the inventory
* Search for specific parts
* Update stock quantities
* Monitor low stock alerts
* Delete items from inventory

## Your Tasks

### Part 1\. Explore the System

* Open the [Factory Inventory Management System](https://fspacheco.github.io/rpa-challenge/factory-inventory-system-v1.html) in your browser
* Add several test items with different values
* Try the search functionality
* Update quantities
* Observe the statistics dashboard
* Find 5 bugs (check if the provided one is real!) and document them like:

| Bug ID | Title | Steps to Reproduce | Expected Result | Actual Result | Screenshot/Evidence |
|--------|-------|-------------------|-----------------|---------------|---------------------|
| BUG-00 | Negative quantities accepted | 1. Open the application<br>2. Click "Add New Inventory Item"<br>3. Enter "-50" in Quantity field<br>4. Fill other required fields<br>5. Click "Add Item" | System should reject negative quantities and show validation error | Item is added with negative quantity (-50) | [Screenshot image or link] |
| BUG-01 |  |  |  |  |  |
| BUG-02 |  |  |  |  |  |
| BUG-03 |  |  |  |  |  |
| BUG-04 |  |  |  |  |  |
| BUG-05 |  |  |  |  |  |

### Part 2\. Create Test Cases

Write automated tests using Robocorp/Playwright that verify, at least:

#### Basic Functionality Tests

1. Viewing all inventory items in the table
    - check if all added fields are correct in the table (that is, the name you entered is in the name column, quantity you entered is in the quantity column, and so on)
2. Adding a new inventory item with valid quantities
    - check if quantity and reorder threshold are validated (should accept only positive numbers)
3. Validating batch numbers (must be unique)
    - check that you cannot add duplicated batch numbers (you need to add at least two parts)
4. Updating the quantity of an existing item
    - check if the update button works correctly (you need to add two parts, then change the quantity of one, press update and check if the item was correctly updated)
5. Deleting an item from inventory
    - check if the delete button works correctly (add at least two parts, then delete one of them, check if the correct item was deleted)

#### Business Logic Tests

6. Low stock alert appears when quantity ≤ reorder threshold
7. Low stock alert does NOT appear when quantity > reorder threshold
8. Statistics dashboard shows correct total item count
9. Statistics dashboard shows correct low stock count

#### Search Functionality Tests

10. Search finds items with exact name match
    - check if the search works (it means you first need to add at least one item, and then try to search using the exact name)
11. Search finds items with partial name match
12. Search is case-insensitive (finds "pump" when searching "PUMP")

## Team Work Guidelines

This assignment should be completed in **teams of 2 students**. To avoid overloading one team member, I recommend dividing responsibilities as follows:
1. For Part 1, both students should collaborate on bug documentation - one person can execute exploratory testing while the other documents findings in real-time.
2. For Part 2, divide equally the 12 tests to be done and exchange ideas and tests.

Remember: both team members should understand all parts of the project, not just their assigned sections.

## Deliverables

Upload a report using Markdown format (file with extension .md) in the repository https://github.com/ICT-Robotics25/test-automation with

### 1. Bug Report Document

List of all bugs found, with detailed documentation for each bug in a table as shown in the [example](#part-1-explore-the-system). More info about tables in Markdown at [Github documentation](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-tables).

### 2. Code

Include your full code with syntax highlighting. Do not add the code as image. I want to be able to copy the code to test. In Markdown, place triple backticks ``` before and after the code block like in this example:

  ````
  ```python
  language='Python'
  print(f'This is {language} code with syntax highlighting')
  ```
  ````

  for obtaining:

  ```python
  language='Python'
  print(f'This is {language} code with syntax highlighting')
  ```
More info at [Github documentation](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks).

### 3. Test Report

Include:
  * Summary of tests executed
  * Coverage summary (that is, answer if you think that these 12 tests are enough. Are there any additional tests you consider necessary?)
  * Pass/fail results for Version 1 of the website: https://fspacheco.github.io/rpa-challenge/factory-inventory-system-v1.html
  * Pass/fail results for Version 2 of the website: https://fspacheco.github.io/rpa-challenge/factory-inventory-system-v2.html
  * Pass/fail results for Version 3 of the website: https://fspacheco.github.io/rpa-challenge/factory-inventory-system-v3.html  
  * Your comments about the process


## Additional information about Inventory Fields

Each inventory item has the following fields:

### Part Name

* The name or description of the component/material
* Examples: "Hydraulic Pump", "Steel Plate 10mm", "Bearing Type-A"
* Required field

### Quantity

* The current number of units available in stock
* Must be a **positive number** (0 or greater)
* Required field

### Batch Number
* A unique identifier for a production batch or shipment
* Used for quality control and traceability
* If a defect is found, the batch number helps identify which items are affected
* Examples: "BATCH-2024-001", "LOT-A-12345", "SHP-20240115"
* **Must be unique** - no two items can have the same batch number
* Required field

### Location
* The physical location in the warehouse/factory where the item is stored
* Helps workers quickly find items when needed
* Examples: "Warehouse A-Shelf 3", "Storage Room B", "Aisle 5-Bin 12"
* Required field

### Reorder Threshold
* The minimum quantity level that triggers a "low stock" warning
* When quantity falls to or below this number, the system alerts managers to reorder
* Example: If threshold is 50 and quantity drops to 50 or below, status shows "LOW STOCK"
* Must be a **positive number**
* Required field

### Status
* Automatically calculated by the system
* "LOW STOCK" (red) - Quantity is at or below the reorder threshold
* "OK" (green) - Quantity is above the reorder threshold
