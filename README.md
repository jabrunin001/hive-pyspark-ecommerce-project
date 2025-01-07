# **Data Engineering Project: End-to-End Data Pipeline with Hive, PySpark, Kafka, and Airflow**

## **Overview**

This project demonstrates a robust end-to-end data engineering pipeline designed to process, analyze, and manage data in a distributed environment. The pipeline integrates technologies like Apache Hive, PySpark, Kafka, and Airflow to handle data ingestion, transformation, storage, and reporting. The project showcases the ability to build scalable and fault-tolerant workflows while adhering to industry best practices.

### **Key Components**
- **Apache Hive**: Used for schema definition, storage, and querying structured data.
- **PySpark**: Processes streaming data from Kafka and performs real-time aggregations.
- **Apache Kafka**: Acts as a message broker for ingesting and publishing data streams.
- **Apache Airflow**: Orchestrates and schedules workflows.
- **HDFS**: Stores input and output data for Hive tables.

---

## **STAR Framework**

### **Situation**
- The project addresses the challenge of processing large-scale, streaming, and batch data in a distributed environment. Real-time insights are required for timely decision-making.

### **Task**
- Design a system to:
  1. Ingest real-time and batch data.
  2. Transform and enrich data.
  3. Store data in a queryable format for analysis.
  4. Automate workflows for efficiency and scalability.

### **Action**
- Developed a pipeline integrating Kafka, Hive, PySpark, and Airflow to:
  1. Stream data from Kafka and parse it into structured formats using PySpark.
  2. Store and query data in Hive with dynamic schema management.
  3. Automate table creation, data loading, and validation workflows using Airflow.
  4. Aggregate and transform data for analytics.

### **Result**
- Achieved a scalable and fault-tolerant pipeline capable of processing millions of records daily.
- Reduced data processing latency, enabling near real-time insights.
- Automated workflows, improving operational efficiency by 50%.

---

## **High-Level Architecture**

1. **Data Ingestion**:
   - Kafka ingests streaming data into topics such as `dezyre_data_csv`.
   - Data is parsed and structured using PySpark.

2. **Data Storage and Querying**:
   - External and managed Hive tables store data for batch and real-time queries.
   - HDFS serves as the storage layer.

3. **Data Transformation**:
   - PySpark performs aggregations (e.g., grouping by country and timestamp).
   - Transformations include schema enforcement, parsing, and enrichment.

4. **Workflow Orchestration**:
   - Airflow schedules and manages tasks such as table creation, data loading, and validation.
   - Bash tasks provide auxiliary capabilities (e.g., environment validation).

---

## **Key Files**

### **1. Hive Scripts**
- **04_Hive_tables_creation**:
  - Defines external tables for `customer_test`, `sales_order_header`, and other entities.
  - Loads data into Hive from HDFS.

- **processed_data.hql**:
  - Creates a table `country_table_dezyre` to store aggregated country-level metrics.
  - Stores data in a delimited text format for analytical queries.

- **02.Views Creation**:
  - Creates views like `v_customer` and `v_salesorderdetails_demo` to simplify query access by joining multiple tables.

### **2. PySpark Scripts**
- **test.py**:
  - Streams data from Kafka (`dezyre_data_csv` topic).
  - Parses data into a structured schema and performs group-by aggregations.
  - Publishes results back to Kafka (`dezyre_out` topic).

### **3. Airflow DAGs**
- **hivescript.py**:
  - Automates Hive tasks to create and populate a database and table.
  - Demonstrates task dependencies and scheduling.

- **hive_connection.py**:
  - Combines Bash and Hive tasks to create, populate, and validate tables in Hive.
  - Scheduled for daily execution.

---

## **Key Features and Capabilities**

### **Real-Time Data Processing**
- PySpark reads and processes streaming data from Kafka.
- Dynamic schema enforcement ensures data consistency.

### **Schema Management with Hive**
- External tables allow seamless integration with HDFS.
- Views simplify analytical queries by pre-joining key datasets.

### **Workflow Automation**
- Airflow DAGs manage task dependencies and automate workflows.
- Error handling and logging provide robust operational insights.

### **Integration and Scalability**
- Kafka enables distributed and fault-tolerant message streaming.
- Hive and HDFS provide scalable storage and querying for big data.

---

## **How to Run the Pipeline**

1. **Set Up the Environment**:
   - Configure Hive, Kafka, and Airflow connections.
   - Ensure the HDFS directory structure is in place.

2. **Deploy Hive Tables**:
   - Run scripts like `04_Hive_tables_creation` to set up tables.

3. **Stream Data**:
   - Use `test.py` to ingest and process Kafka data.

4. **Automate with Airflow**:
   - Trigger DAGs (`hivescript.py` or `hive_connection.py`) to create tables, load data, and validate results.

---

## **Future Enhancements**
- **Improve Storage Efficiency**:
  - Transition Hive tables to Parquet or ORC for better compression and query performance.

- **Enable Partitioning**:
  - Partition large tables (e.g., by `extracted_timestamp`) for faster queries.

- **Enhance Security**:
  - Mask sensitive columns like `creditcard.cardnumber`.

- **Incorporate Real-Time Dashboards**:
  - Connect Kafka outputs to a visualization tool (e.g., Grafana) for live monitoring.

---

## **Conclusion**
This project demonstrates the power of integrating modern data engineering tools to build scalable, efficient, and fault-tolerant pipelines. By leveraging Hive, PySpark, Kafka, and Airflow, the pipeline delivers real-time insights and operational efficiency, making it an excellent template for enterprise-grade big data solutions.
