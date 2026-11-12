# Solar Operations Intelligence Accelerator
A Databricks Lakehouse prototype for a residential solar company. This provides insights regarding top performing territories and lead sources that generate the highest-quality customers

## Business Problem
Residential solar companies have data across many stages of the customer journey from lead generation, sales, installation operations, demos, and even customer responses. Because this data is 
fragmented across different systems, it is difficult for business leaders to udnerstand which acquisition channels and regions are generating the most valuable customers.

This project simulates a mid-sized residental solar company and explores the following business question:

**Which territories and lead sources generate the highest-quality customers, and where should the company focus its sales and markerting resources?**

For this MVP, customer quality is evaluated across the customer journey using these metrics:

+ **Qualification rate** - How effectively leads become real opportunities
+ **Contract conversion rate** - How effectively leads turn into signed customers
+ **Average contract value** - How much revenue a signed customer generates
+ **Installation completion rate** - How successfully customers reach the installation stage

### These metrics are presented so relevant stakeholders can evaluate tradeoffs on business priorities.

---
## Solution Overview
The Solar Operations Intelligence Accelerator uses a simplified **Medallion Architecture** to move data from raw source systems into business-ready analytics.

This project is being developed iteratively with a functional MVP and progressively improving the data architecrure and analytics.

## Architecture
### Source Data
The solutions begines with syntheically generated data instead of using proprietary data.

### Leads
This represents prospective solar customers and acquisition information.

Key attributes include:
+ Lead ID
+ Territory
+ Lead source
+ Homeowner type
+ Monthly electric bill
+ Appointment date

### Sales
This represents outcomes from the sales process.

Key attributes include:
+ Lead ID
+ Sales representative
+ Qualification status
+ Appointment outcome
+ Contract status
+ Contract value
+ Cancellation reason

### Installations
This represents outcomes after a customer contracts.

Key attributes include:
+ Lead ID
+ Installation status
+ Days to installation
+ Cancellation Reason

The datasets are connected using `lead_id`. This allows analysis of the complete customer journey from acquisition through installation.

## Data Pipeline
### 1. Source Data Gen
Python and Pandas were used to generate the synthetic datasets.
Our data-gen process is validated to ensure:

+ Unique lead IDs
+ Sales records match valid leads
+ Installation records can only exist for contracted customers

The dats is converted into Spark DataFrames and persisted as Delta tables.
### 2. Bronze Layer
The bronze layer preserves sources data with minimal transformation. We have ingestion metadata for traceability.

### 3. Silver Layer
🚧 Work In Progress
The silver layer will clean and standardize the Bronze data.

+ Null handling
+ Data validation
+ Create unified dataset

### 3. Gold Layer
🚧 Planned
The gold layer will contain our datasets of business ready insights that answer stakeholder questions.

+ Lead source performance
+ Territory performance
+ Customer quality comparisons

## Technology Stack
+ Databricks Free Edition
+ Apache Spark
+ Delta Lake
+ Python
+ Pandas
+ SQL
+ GitHub

AI-assisted dev tools are used selectively to accelerate implementation and iteration. Architecture decisions, business logic, and validation are designed and reviewed manually to ensure the implementation is understood and explained end-to-end.
## Key Design Decisions

### Why a Medallion Architecture?

The project uses Bronze, Silver, and Gold layers to separate concerns between:

Raw data ingestion

Data cleaning and validation

Business-ready analytics

This makes the pipeline easier to understand, maintain, and extend as additional data sources or business requirements are introduced.

### Why synthetic data?

The project does not use proprietary customer/company information. Synthetic data enables realistic relationships between acquisition, sales, and operational outcomes while remaining fully shareable. Unfortunately I don't have privileges to export real Salesforce data as an ingestion source. 

