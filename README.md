# **Azure End-to-End Data Engineering Project: Adventure Works Analytics**

This project demonstrates a complete **end-to-end data engineering solution** built on Microsoft Azure. It uses a **Medallion Architecture** to process sales, product, and customer data from the Adventure Works dataset, moving it from a raw API source to a final reporting dashboard.

---

### **Project Architecture**
The project follows a **Medallion (Bronze, Silver, Gold) Architecture** to ensure data quality and scalability:
*   **Bronze (Raw):** Stores the data exactly as it appears in the source GitHub API.
*   **Silver (Transformed):** Contains cleaned and formatted data in **Parquet format**.
*   **Gold (Serving):** A logical data warehouse layer used for final business reporting.

---

### **Technology Stack**
*   **Azure Data Factory (ADF):** Used as the **orchestration tool** to build dynamic data pipelines.
*   **Azure Data Lake Storage Gen2 (ADLS):** Serves as the centralized storage with **Hierarchical Namespace** enabled for folder management.
*   **Azure Databricks:** A powerful Spark-based platform for performing **Big Data transformations** using **PySpark**.
*   **Azure Synapse Analytics:** Provides a **Serverless SQL pool** to create a Lakehouse/Logical Data Warehouse.
*   **Power BI:** Connects to the Gold layer for **data visualization** and KPI tracking.
*   **Microsoft Entra ID:** Manages security through **App Registrations** and **Managed Identities**.

---

### **Data Source**
The project utilizes the **Adventure Works dataset**, which includes over **10 tables** such as Sales (2015–2017), Customers (56,000+ records), Products, and Territories. Data is pulled directly from a **GitHub API** rather than manual uploads to simulate a real-world scenario.

---

### **Implementation Steps**

#### **1. Data Ingestion (Source to Bronze)**
*   Set up **Azure Data Lake Storage Gen2** with containers for `bronze`, `silver`, and `gold`.
*   Built **Dynamic Pipelines** in ADF using **Parameters, For-Each loops, and Lookup activities**.
*   Ingested **10+ datasets** from the GitHub HTTP source into the Bronze layer in their original CSV format.

#### **2. Data Transformation (Bronze to Silver)**
*   Established a secure connection between Databricks and the Data Lake using a **Service Principal (App Registration)**.
*   Developed PySpark notebooks to clean and transform the data, including:
    *   **String Cleaning:** Concatenating names (e.g., `full name`) and splitting product SKUs.
    *   **Date Formatting:** Converting strings to timestamps and extracting months/years.
    *   **Mathematical Operations:** Calculating line item totals.
*   Saved the cleaned data into the **Silver layer** using the **Parquet file format** for better read performance.

#### **3. Data Serving (Silver to Gold)**
*   Created a **Serverless SQL Database** in Azure Synapse Analytics.
*   Built an abstraction layer using **OpenRowSet** and **SQL Views** to query Parquet files directly from the Data Lake.
*   Implemented **CETAS (Create External Table As Select)** to physically store the final refined data in the **Gold layer** folder.

#### **4. Reporting & Visualization**
*   Connected **Power BI Desktop** to the Azure Synapse **Serverless SQL endpoint**.
*   Imported the Gold layer tables to build a business dashboard.
*   Visualized key metrics such as **Sales Trends** over time and a total customer count of **56,000+**.

---

### **Key Concepts Covered**
*   **Dynamic Parameterization:** Reducing manual work by building scalable pipelines.
*   **Managed Identities:** Using built-in Azure security to access resources without managing passwords.
*   **Lakehouse Architecture:** Combining the flexibility of a Data Lake with the querying power of a Data Warehouse.