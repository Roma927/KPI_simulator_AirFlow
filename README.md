# Kpi_simulator_AirFlow

## About
KPI Simulator is a Django-based application that dynamically generates Airflow DAGs to simulate and monitor KPIs (Key Performance Indicators). The system allows users to create simulator instances with customizable parameters, which automatically generate corresponding Airflow DAGs to periodically calculate and track KPI values.

## Features
- Dynamic DAG generation based on simulator configurations
- Customizable KPI calculation endpoints
- Flexible scheduling options (hourly, daily, weekly)
- REST API for KPI calculations
- Admin interface for simulator management

## Tech Stack
- Django 4.2.0
- Django REST Framework 3.14.0
- Apache Airflow 2.7.1
- PostgreSQL
- Python 3.9+

## Installation

### Prerequisites
- Python 3.9 or higher
- PostgreSQL
- pip (Python package manager)

### Setup Using Virtual Environment (venv)

1. Clone the repository:
```bash
git clone https://github.com/yourusername/kpi-simulator.git
cd kpi-simulator
```

2. Create and activate virtual environment:
```bash
# Windows
python -m venv venv
.\venv\Scripts\activate

# Linux/MacOS
python3 -m venv venv
source venv/bin/activate
```

3. Install required packages:
```bash
pip install -r requirements.txt
```

4. Configure Django:
```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

5. Configure Airflow:
```bash
export AIRFLOW_HOME=./airflow  # Linux/MacOS
set AIRFLOW_HOME=./airflow    # Windows

airflow db init
airflow users create \
    --username admin \
    --password admin \
    --firstname admin \
    --lastname admin \
    --role Admin \
    --email admin@admin.com
```

## Running the Application

1. Start Django server:
```bash
python manage.py runserver
```

2. Start Airflow webserver (in new terminal):
```bash
airflow webserver -p 8080
```

3. Start Airflow scheduler (in new terminal):
```bash
airflow scheduler
```

Access the applications:
- Django Admin: http://localhost:8000/admin
- Airflow UI: http://localhost:8080

## Usage

1. Log in to Django admin interface
2. Create a new Simulator instance with:
   - Start date
   - Interval (hourly/daily/weekly)
   - KPI ID
3. Airflow will automatically generate a DAG based on your configuration
4. Monitor DAG execution in Airflow UI

## API Endpoints

### Calculate KPI
- URL: `/api/calculate/`
- Method: POST
- Request Body:
  ```json
  {
    "value": 100,
    "kpi_id": 1
  }
  ```
- Response:
  ```json
  {
    "result": 150
  }
  ```

## Project Structure
```
kpi_simulator/
│
├── kpi_simulator/          # Project settings
├── simulator/             # Main application
├── dags/                 # Airflow DAGs
├── manage.py
├── requirements.txt
└── README.md
```
