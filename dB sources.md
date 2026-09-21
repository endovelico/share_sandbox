Absolutely — here's a reusable template you can copy and replace the **[KEYWORDS]**.

# [PROJECT NAME] — Data Source Analysis

## 1. Objective

The objective of this analysis is to identify and document all **[DATA SOURCES / SYSTEMS / APPLICATIONS]** that are relevant to the **[PROJECT NAME]** project.

The analysis aims to provide a comprehensive overview of the data landscape, including the origin of the data, how it is accessed, how it is processed, and where it is consumed.

## 2. Scope

The analysis covers the following areas:

* Identification of all **[INTERNAL / EXTERNAL]** data sources.
* Identification of the **[APPLICATIONS / DATABASES / APIs / FILES]** providing data.
* Identification of the relevant **[TABLES / DATASETS / FILES / ENDPOINTS]**.
* Documentation of data ownership and responsible teams.
* Analysis of data flows between source systems and **[TARGET SYSTEM / PROJECT / PLATFORM]**.
* Identification of data transformations and processing steps.
* Identification of dependencies, interfaces, and access requirements.
* Identification of potential data quality issues or gaps.

## 3. Data Source Identification

The following data sources have been identified as relevant to **[PROJECT NAME]**:

| Data Source | Source Type         | Owner   | Data Domain | Data Format | Frequency         | Usage     |
| ----------- | ------------------- | ------- | ----------- | ----------- | ----------------- | --------- |
| [SOURCE 1]  | [DATABASE/API/FILE] | [OWNER] | [DOMAIN]    | [FORMAT]    | [DAILY/REAL-TIME] | [PURPOSE] |
| [SOURCE 2]  | [DATABASE/API/FILE] | [OWNER] | [DOMAIN]    | [FORMAT]    | [DAILY/REAL-TIME] | [PURPOSE] |
| [SOURCE 3]  | [DATABASE/API/FILE] | [OWNER] | [DOMAIN]    | [FORMAT]    | [DAILY/REAL-TIME] | [PURPOSE] |

## 4. Source Description

### [SOURCE NAME]

**Description:**
[SHORT DESCRIPTION OF THE SOURCE AND ITS PURPOSE.]

**Source Type:** [DATABASE / API / FILE / APPLICATION / EXTERNAL SOURCE]

**Data Owner:** [TEAM / DEPARTMENT / PERSON]

**Data Domain:** [CUSTOMER / PRODUCT / TRANSACTION / FINANCIAL / OTHER]

**Data Format:** [CSV / JSON / XML / SQL TABLE / PARQUET / OTHER]

**Data Frequency:** [REAL-TIME / HOURLY / DAILY / WEEKLY / MONTHLY]

**Access Method:** [API / DATABASE CONNECTION / SFTP / CLOUD STORAGE / OTHER]

**Data Used By:** [APPLICATION / REPORT / PROCESS / MODEL]

**Relevant Data Elements:**

* [FIELD / ATTRIBUTE 1]
* [FIELD / ATTRIBUTE 2]
* [FIELD / ATTRIBUTE 3]

**Data Flow:**
Data is extracted from **[SOURCE]**, processed through **[PROCESS / TRANSFORMATION]**, and subsequently delivered to **[TARGET SYSTEM / DATA PLATFORM / APPLICATION]**.

**Dependencies:**
The availability of this data depends on **[SYSTEM / PROCESS / INTERFACE]**.

**Known Issues / Considerations:**
[DATA QUALITY ISSUES / MISSING DATA / ACCESS LIMITATIONS / OTHER OBSERVATIONS.]

## 5. Data Flow

The identified data sources contribute data to **[TARGET SYSTEM / PROJECT]** through different ingestion and processing mechanisms.

The general data flow can be described as:

**[SOURCE SYSTEM] → [INGESTION / INTERFACE] → [TRANSFORMATION / PROCESSING] → [TARGET SYSTEM] → [CONSUMER / REPORT / APPLICATION]**

Where applicable, additional transformations or enrichment steps are performed between the source and target systems.

## 6. Data Quality and Gaps

During the analysis, the following data quality considerations were identified:

* [ISSUE / GAP 1]
* [ISSUE / GAP 2]
* [ISSUE / GAP 3]

Further analysis may be required to determine whether **[MISSING DATA / DUPLICATES / INCONSISTENCIES / OUTDATED DATA]** have an impact on **[PROJECT / PROCESS / REPORTING]**.

## 7. Summary

The analysis identified **[NUMBER]** relevant data sources supporting **[PROJECT NAME]**.

These sources provide data related to **[MAIN DATA DOMAINS]** and are consumed by **[TARGET SYSTEMS / APPLICATIONS / PROCESSES]**.

Further investigation is recommended for **[OPEN ITEMS / UNCONFIRMED SOURCES / DATA QUALITY ISSUES]** to ensure that the data-source inventory is complete and that all dependencies are properly documented.

You can essentially use this as a **master template**: duplicate the *Source Description* section for every datasource you discover and fill in the brackets.
