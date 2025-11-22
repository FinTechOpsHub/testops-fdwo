# Financial Data Workflow Orchestrator (FDWO) – Architecture Overview

## 🧩 Concept
The Financial Data Workflow Orchestrator (FDWO) is a generic, configurable framework that provides a centralised environment where a user can design, configure, and execute end-to-end data upload workflows into a SQL database across multiple data types, files, and upload methods.

It replaces manual, fragmented upload practices with a structured workflow engine that supports orchestration, validation, and execution across environments.

---

## 🏗 Context & Assumptions

FDWO assumes an existing application or system capable of accepting uploads via:

- `.csv` / `.xlsx` front-end file upload  
- direct SQL inserts / scripts  
- (optional) API endpoints, subject to system capability  

### Data Types
Each data type corresponds to a specific database table or view with its own schema.

Each data type has:
- a unique column set  
- defined data types (Excel type: general, date, number, text)  
- constraints (max length, nullability, uniqueness)  
- validations (column-level and cross-column)  
- mapping rules to DB columns via:  
  - 1–1 mappings  
  - transformation logic  
  - lookups / code translations  
  - key generation / mapping logic  

### Volume & Performance
- Multiple rows can be uploaded per file  
- Practical volume limits apply depending on system performance  
- Processing time varies by data type and schema complexity  

### Dependencies
Data types may be independent or interdependent.

Validation may occur:
- within a file (row/column level)
- across different data types (relational dependencies)

### Execution Modes
FDWO supports:
- manual uploads via front-end  
- scheduled uploads (SQL Agent / job scheduler)  
- direct SQL insertion (bypasses FE validations; requires caution)  
- potential future extension: API-based uploads  

---

## 🧠 What FDWO Does

FDWO enables users to design and run workflows without manually juggling uploads, scripts, or brittle sequences.

From one central interface, users can:

### Workflow Design
- choose which data types to include  
- define values or files for each data type  
- specify:
  - target environment / target DB  
  - upload method  
  - dependency order  
  - parameters, flags, options  

### Workflow Execution
- run the entire workflow with a single orchestrated action  
- FDWO handles sequencing, validation, orchestration, and execution  

### Workflow Value
- time reduction  
- streamlined processes  
- centralised logic (reduces tribal knowledge)  
- scalable and configurable architecture  
- improved UX for testers/BAs  
- consistent behaviour across environments  
- full auditability / traceability  
- more intuitive and repeatable testing  

---

## 🧰 Tech Stack (Current / Near-Term)

### Front-End
- Excel UI (main control surface)  
- user-friendly layout, dropdowns, validations, navigation  

### Orchestration Layer
VBA for:
- reading user selections  
- generating config/input files  
- triggering workflows via `.bat` or COM calls  

### Core Logic
C# or Python to:
- apply business logic  
- process files  
- interact with DB  
- handle logging  
- manage workflow sequencing  

### Database Layer
- SQL scripts / stored procedures  
- validation logic  
- scheduled jobs  
- reference/static tables  

### Execution Bridge
- `.bat` or shell scripts called from Excel/VBA  
- optional direct COM integration  

---


