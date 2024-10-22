# REAL ESTATE DATA ANALYTICS PIPELINE

### **Overview:**
This project aims to **automate the process** of extracting and transforming **real estate data** to support **market analysis** on Tableau. By leveraging cloud-based services, the pipeline handles storage and transformation of large data. The ultimate goal is to streamline data processing to provide insights on **real estate trends** using a data pipeline.

### **Process Description:**

1. **Data Extraction:**
   - The **first step** involves **extracting real estate data** from the **Redfin API**. The data extracted includes details like property prices, locations, property types, and other key features relevant to the real estate market.
   - The pipeline is designed to extract data with automated jobs ensuring that the process is repeatable without manual intervention.

2. **Data Ingestion and Storage**:
   - Once extracted, the raw data is **ingested** into **Amazon S3** (Simple Storage Service), a cloud-based object storage service. This storage acts as a **landing zone** for raw data files.
   - **S3** is configured to store the incoming data in structured folders and files, which ensures efficient retrieval and processing.
  
<img width="1130" alt="image" src="https://github.com/user-attachments/assets/3d767f40-ce5d-45fe-a140-c58b6745457f">

3. **Data Transformation and Processing**:
   - The next step involves transforming the ingested raw data. This is where the data is cleaned, processed, and prepared for analysis. **Amazon EMR (Elastic MapReduce)** is used to perform distributed data processing, which is particularly useful for handling large datasets.
   - The transformation process includes:
     - **Data cleansing**: Removing duplicates, handling missing values, and normalizing data.
     - **Feature engineering**: Creating new features from the data for enhanced analysis (e.g., property price trends over time).
   - Transformed data is saved back to **Amazon S3** in a dedicated storage bucket (intermediate storage) for later access.
  
![image](https://github.com/user-attachments/assets/e5d6361b-2145-4baa-bed7-8e802524e221)

4. **Data Loading into Snowflake**:
   - Once the data has been processed, it is loaded into **Snowflake**, a cloud-based data warehousing platform. **Snowflake** was chosen for its ability to:
     - **Scale compute and storage separately**.
     - Handle **structured and semi-structured data** formats (e.g., JSON, CSV).
     - Offer **high-performance querying** and **data sharing** capabilities.
   - The connection between **S3 and Snowflake** is managed using **Snowflake’s external stage** feature. This allows **data to be imported directly** from **S3** into Snowflake using the **COPY INTO** command.

<img width="1285" alt="image" src="https://github.com/user-attachments/assets/d005a297-a1d0-4ca1-948b-26706369ce75">

5. **Data Analytics and Visualization**:
   - With the processed data now in Snowflake, **SQL-based querying** is used to **analyze the data** for market trends, pricing insights, and various other analytical purposes.
   - The results of these queries are then exported for **visualization** using **Power BI**, a powerful business intelligence tool. In Power BI, interactive dashboards are created to visualize key metrics such as:
     - **Average property prices** over time.
     - **Price distribution** across different regions.
     - **Market trends** based on features such as property type, square footage, and location.
   - Power BI's integration with **Snowflake** allows for **real-time data analysis**, ensuring the visualizations are always up-to-date with the latest data.


### Click here to view the interactive Tableau Dashboard - [Link](https://public.tableau.com/app/profile/harshitha.chandrashekar/viz/RealEstateMarketOverview/Dashboard1)
<img width="1201" alt="image" src="https://github.com/user-attachments/assets/1aea599d-4d04-4a68-ac1d-bf22707a5342">

### Data Interpretation
- Home inventory increased from 2012 to 2018, peaking at over 15 million homes. It then declined sharply in 2020 and 2021, likely due to market factors. Inventory slightly recovered in 2022 and 2023 but dropped again in 2024.
- Florida leads with 9.88 million homes (10.09%), followed by California and Texas. These three states dominate the housing market. Pennsylvania, Ohio, and North Carolina rank in the middle with 3.4 to 3.5 million homes.
- Median sale prices rose steadily until 2022, peaking at over 1 billion USD. However, in 2024, prices dropped to around 900 million USD, indicating a cooling market.
- Home sales peaked in 2021 but declined sharply in 2022 and beyond. Single-family homes dominate sales, with townhouses and multi-family properties representing smaller portions.

## Tools and Technologies Used

1. **Data Extraction**: **Redfin API** for gathering real estate data

2. **Data Storage and Ingestion**:
   - **Amazon S3**: Used for both raw data storage (landing zone) and processed data storage (intermediate storage).

3. **Data Transformation and Processing**: **Amazon EMR**, **AWS Lambda**
     - For distributed data processing and transformation and to trigger data transformations and automate workflows.

4. **Data Warehouse**: **Snowflake**
     - Used as the central data warehouse to store and analyze transformed data.
     - External stages allow for easy import of data from S3.
     - Provides **high-performance querying** and supports **semi-structured** and **structured** data formats.

5. **Data Visualization and Reporting**: **Tableau**
     - Used for creating interactive dashboards to visualize real estate trends and market insights.
     - Integrated with Snowflake for data analysis and visualization.

6. **Orchestration**: **Apache Airflow**
     - To schedule and manage end-to-end workflows. Airflow ensures that tasks like data extraction, processing, and loading into Snowflake happen automatically and in sequence.

  
### **Project Outcomes:**
- The pipeline successfully handles large data, ensuring reliable data ingestion, transformation, and analysis.
- By automating the entire pipeline, the team can generate **real-time insights** into the real estate market, helping analysts make **data-driven decisions**.
- The use of **Snowflake** for data warehousing enables **fast querying** and **scalability**, ensuring that as data volume grows, the performance remains unaffected.
- The **visualization dashboards** in **Tableau** provide stakeholders with a clear view of the market, helping them understand **price trends**, identify **high-value properties**, and analyze market dynamics.
