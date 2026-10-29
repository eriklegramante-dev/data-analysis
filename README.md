# 📊 Student Productivity & Wellbeing Data Pipeline

An end-to-end data engineering pipeline integrating digital behavior metrics (screen time), academic performance indicators, and real-time environmental data.

The project demonstrates practical data engineering competencies across multi-source ingestion, programmatic transformation, analytical data modeling, and interactive dashboard delivery.

---

## 🧠 Business Problem

The pipeline explores a central analytical question:

**Is there a quantifiable correlation between smartphone usage patterns, environmental factors, and academic performance?**

To evaluate this hypothesis, the pipeline ingests and reconciles three distinct domains:

- 📱 Digital footprint metrics (screen time, app categories)
- 🎓 Academic outcomes (grades, attendance, performance indices)
- 🌤️ Ambient meteorological conditions (temperature, humidity, precipitation)

These datasets are transformed, enriched, and loaded into an analytical data mart optimized for correlation analysis, aggregation, and visual exploration.

---

## 🏗️ Architecture & Data Modeling

The ingestion and transformation flow follows the **Medallion Architecture**, establishing progressive data quality guarantees across processing stages:

```text
[ CSV Data Sources ] ──┐
                       ├──> [ Bronze: Raw Layer ] ──> [ Silver: Cleaned Layer ] ──> [ Gold: Curated Layer ] ──> [ Streamlit Analytics ]
[ WeatherAPI (REST) ] ─┘        (Staging I/O)             (Pandas Transformation)         (PostgreSQL DW)
```

### Bronze — Ingestion & Raw Layer
Captures raw source data without destructive mutations:
- Batch ingestion from local CSV datasets
- Automated extraction via external REST API (WeatherAPI)

### Silver — Conformed & Cleaned Layer
Applies structural standardization, schema conformance, and data hygiene:
- Field normalization to standard `snake_case` conventions
- Primary key deduplication and foreign key alignment
- Deterministic data type casting and datetime parsing
- Null value imputation and edge-case handling
- Processing engine: **Pandas**

### Gold — Curated & Analytical Layer
Constructs query-optimized multidimensional models:
- Relational joins across academic records and behavioral sessions
- Temporal enrichment utilizing weather time-series observations
- Relational schema persistence and indexing via **PostgreSQL**

---

## 🛠️ Tech Stack

- **Core:** Python 3.11+
- **Data Processing & Manipulation:** Pandas, NumPy
- **Object-Relational Mapping & Database Driver:** SQLAlchemy, Psycopg2
- **Data Warehouse / RDBMS:** PostgreSQL
- **Containerization & Orchestration:** Docker, Docker Compose
- **Data Visualization & Analytics:** Streamlit

---

## 📂 Project Structure

```text
data-analysis/
├── app/
│   └── dashboard.py          # Interactive Streamlit reporting application
├── dataset/                  # Source CSV files and local staging assets
├── scripts/                  # Modular ETL extraction and transformation scripts
├── sql/                      # DDL definitions, views, and analytical queries
├── .env.example              # Template for API credentials and DB config
├── docker-compose.yml        # PostgreSQL container configuration
├── main.py                   # Orchestration entrypoint for the ETL pipeline
└── requirements.txt          # Pinned project dependencies
```

---

## ⚙️ Quickstart & Local Setup

### 1. Clone the repository

```bash
git clone [https://github.com/eriklegramante-dev/data-analysis.git](https://github.com/eriklegramante-dev/data-analysis.git)
cd data-analysis
```

### 2. Configure environment variables

```bash
cp .env.example .env
# Set your POSTGRES credentials and WEATHER_API_KEY inside .env
```

### 3. Initialize Python virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### 4. Provision local database infrastructure

```bash
docker compose up -d
```

### 5. Execute the pipeline

Run the end-to-end ingestion and transformation run:

```bash
python main.py
```

### 6. Launch the analytics dashboard

```bash
streamlit run app/dashboard.py
```

The dashboard will be available at `http://localhost:8501`.

---

## 📈 Analytical Deliverables

- Screen time thresholds vs. grade point distribution
- Categorical application usage trends across study cycles
- Multivariate correlation matrices between weather conditions, sedentary habits, and academic focus

---

## 🎯 Core Competencies Demonstrated

- **Data Pipeline Architecture:** Multi-tier Medallion architecture implementation
- **ETL/ELT Workflows:** Clean extraction, schema validation, and database ingestion
- **API Integration:** Resilient REST consumption and data enrichment
- **Infrastructure as Code:** Local database provisioning using Docker Compose
- **Relational Modeling:** PostgreSQL schema design, indexing, and SQLAlchemy integration
- **Business Intelligence:** Interactive analytical UI design via Streamlit

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

## 👨‍💻 Author

Engineered by [Erik Legramante](https://github.com/eriklegramante-dev) — Portfolio project focused on **Data Engineering and Python Systems**.