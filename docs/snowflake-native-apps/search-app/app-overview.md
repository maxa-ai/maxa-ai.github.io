---
sidebar_position: 1
---

# Release Overview

The search feature allows users to search specific values within an entire database through a no-code interface, making the data discovery process both efficient and accessible. This tool accelerates data assessment and helps locate data pieces in cryptic databases, streamlining workflows for data teams.

# **Key Features**

## **Initiate a Search**

* **Search Value Input**: Begin by inputting the values you're looking for. The value input is flexible, allowing single value or multiple values that can be searched across the same or multiple columns.

  * *Example: Search Value Input*

     When 'AIR' is entered in the value field, the Setup App searches to locate all instances where 'AIR' appears, whether at the beginning, middle or end of a string.

    <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
        <img src="/search_app/image1.png" alt="Image 1" style={{ width: "45%" }} />
        <img src="/search_app/image2.png" alt="Image 2" style={{ width: "45%" }} />
    </div>

* **Define Search Parameters**: Enhance your search precision with optional parameters:

  * **Case Sensitive**: Match values with exact casing.

  * **Exact Match**: Locate values that exactly match your input.

  * **Row Search**: Search for your input values across multiple columns within the same row.

    * *Example: Row Search*

       When 'AIR' and '406' are entered as values and the row search option is selected, the Setup App searches for rows across the specified database and schema where both 'AIR' and '406' appear together in any columns of the same table.  
       <div style={{ display: "flex", justifyContent: "center", alignItems: "center" }}>
            <img src="/search_app/image3.png" alt="Image 3" style={{ width: "60%" }} />
       </div>
    
  * **Wildcard Search**: Insert a wildcard (%) before or after the value to search for something ending or starting with your input.

    * *Example: Wildcard Search*

       When ‘%PO’ is entered as value, the Setup App searches to locate all instances ending with PO.  
       <div style={{ display: "flex", justifyContent: "center", alignItems: "center" }}>
            <img src="/search_app/image4.png" alt="Image 4" style={{ width: "60%" }} />
       </div>

## **Database and Schema Selection**

* **Select Database and Schema**: Choose where your search will occur. Upon selection, enjoy a real-time preview of the relevant tables to ensure your search is targeted correctly.  
  * *Example: Select Database and Schema*

     Left side gives an overview of tables inside the selected database and schema.  
    <div style={{ display: "flex", justifyContent: "center", alignItems: "center" }}>
        <img src="/search_app/image5.png" alt="Image 5" style={{ width: "90%" }} />
    </div>

## **Advanced Search Criteria**

* **Optional Patterns**: Further refine your search by specifying table or column patterns. This flexibility allows for highly targeted searches based on known patterns or structures within your datasets.  
  * *Example: Optional Patterns*  
    When 'ASIA' and 'AFRICA' are entered in the value field along with the column pattern 'R%', the Setup App searches where either value appears in columns starting with 'R' across the specified database and schema.
    <div style={{ display: "flex", justifyContent: "center", alignItems: "center" }}>
        <img src="/search_app/image6.png" alt="Image 6" style={{ width: "90%" }} />
    </div>

### **Table and Column Searches**

* **Pattern-Based Search**: Use the search app to find table or column names without specifying a specific value, but rather a pattern. Enter '%' in the value field and use the advanced search section to specify the table or column pattern you’re targeting. This is particularly useful for identifying relevant structures in your database.

  * *Example: Pattern-Based Search*  
    
    When '%' is entered in the value field and 'P%' is specified as the column pattern, the Setup App searches for and identifies all columns that begin with 'P' across the specified database and schema
    <div style={{ display: "flex", justifyContent: "center", alignItems: "center" }}>
        <img src="/search_app/image7.png" alt="Image 7" style={{ width: "90%" }} />
    </div>

## **Real-Time Search Feedback**

* **Search Status and Results Summary**:  
  * Search will start with the “Queued” status. Press the “Refresh” button to update the status.  
  * At the “Queued” or “In Progress” stages, the “Cancel” button can be used to stop the search.  
  * Once a search concludes successfully, the status will update to "Success," with the number of search results displayed prominently. This immediate feedback lets you assess the efficiency of your search instantly.

## **Detailed Search Results**

* **Interactive Results Table**: Access a comprehensive table listing all column and table names where your values were found. Each entry allows for a quick preview of the table content, enabling you to verify results.  
* **Occurrences Filtering**: If needed, refine your examination by searching within the results based on the number of occurrences of values in specific columns.

## **Repeat and Refine Searches**

* **Search Parameters Summary**: Below the results table, view a detailed summary of the search parameters used. This ensures you can verify all criteria applied to your search.  
* **Repeat Search Functionality**: Click "Repeat Search" to open a new search tab pre-filled with the same criteria, facilitating similar searches without the hassle of re-entering parameters.
