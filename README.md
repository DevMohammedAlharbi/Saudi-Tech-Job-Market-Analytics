# JobDataPipeline_Project
JobDataPipeline is a collaborative data engineering project focused on collecting, transforming, and preparing technical job market data in Saudi Arabia for analytics. The project was developed as part of the Data Engineering Bootcamp – August 2026, offered by the Saudi Digital Academy (SDA) in collaboration with WeCloudData.

Job Data Pipeline - DE 2026 | Team C
End-to-end ELT pipeline to extract job postings from 5 heterogeneous sources, build a clean Data Warehouse on Snowflake with dbt, and enforce data quality.

Original Team Project: Lee115/DE-2026-TeamC-JobDataPipeline-Cohort-1 
My Role: Data Engineer - Extraction, Transformation & dbt Modeling Lead

Architecture Overview
5 Sources (API / Scraping / Static) -> Python Extractors - python cleaning and Transformation -> dbt (staging -> intermediate -> marts) -> Star Schema -> dbt tests + docs
What I Built (My Contribution)
This was a collaborative team project. My core contributions were:

1- Multi-Source Job Extraction Framework (Python)
Built 5 independent extractors, each with a different integration pattern to handle real-world constraints:

Jooble API: Direct API key authentication
JSearch / RapidAPI: Header-based auth with RapidAPI host/key management
FreeHire: Browser simulation & dynamic page handling
Tanqeeb (Arabic Source): Arabic content extraction
Tapneo: Static file ingestion
Implemented production-grade features for all extractors:

Robust error handling, retries, and Rate Limiting
Quota management for limited APIs
Unified JSON output schema

2. Data Cleaning & Normalization (Python - Pandas & BeautifulSoup)
HTML Cleaning: Removed HTML tags from job descriptions using BeautifulSoup
Skill Extraction: Parsed and extracted technical skills from unstructured text descriptions
Translation Layer: Translated Arabic job postings (Tanqeeb source) to English for unified analysis
Field Standardization: Unified formats for titles, locations, employment types before loading to Snowflake.

3. dbt Modeling - Full Star Schema on Snowflake
Designed and implemented a Fact Constellation schema with 3 layers:

Layers:

staging: Light cleaning, renaming, type casting from RAW
intermediate: Business logic, deduplication, skill normalization
marts: Final dimensional model
Dimensional Model:

[5 Dimensions]: dim_company, dim_location, dim_date, dim_job_attributes, dim_skill
2 Fact Tables: fct_job_postings, fct_job_skills
Used dbt_utils.generate_surrogate_key() for surrogate keys
Implemented Unknown Member Pattern to handle nulls / missing FKs without breaking joins
4. Data Quality & Testing Layer (dbt)
Built a comprehensive testing layer:

52 data quality tests across all layers: not_null, unique, relationships, accepted_values
Auto-documentation for every model and column via dbt docs
Solved real quality issues discovered during development:
Surrogate key collisions
Duplicate skill synonyms (e.g., "JS" vs "JavaScript")
Model build concurrency issues
Tech Stack
Python Pandas BeautifulSoup Snowflake dbt SQL Git RapidAPI Jooble API

Key Challenges Solved
Handling 5 different auth mechanisms in one unified pipeline
Arabic -> English translation for data consistency
Designing a scalable dimensional model that supports both job-level and skill-level analysis



Author: [Your Name] | [Your LinkedIn] | [Your Portfolio]
