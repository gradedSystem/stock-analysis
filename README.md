# Real-time Stock Price Analysis and Alerting

## Project Overview
This project provides a real-time stock price analysis and alerting system using the Alpha Vantage API. It fetches stock data, processes it with Python, stores it in a local PostgreSQL database, and sends email notifications when the stock price crosses user-defined thresholds.

## Features
- Real-time stock price retrieval using Alpha Vantage API
- Data processing and analysis with Python (Pandas)
- Storage of stock data in a PostgreSQL database
- Workflow orchestration with Apache Airflow
- Email alerts sent via Python’s `smtplib` or SendGrid

## Technologies Used
- **Programming Language**: Python
- **Data Ingestion**: `requests` (API calls)
- **Data Processing**: `Pandas` (data manipulation)
- **Data Storage**: PostgreSQL (local setup)
- **Workflow Orchestration**: Apache Airflow
- **Alerting**: Email notifications (via `smtplib` or SendGrid)

## Setup

### 1. Obtain an API Key
Create an account on [Alpha Vantage](https://www.alphavantage.co/) and obtain an API key to access real-time stock data.

### 2. Set Up the Virtual Environment
Follow the steps below to set up the virtual environment:

```bash
# Create a virtual environment
python -m venv venv

# For Windows users
./venv/Scripts/activate

# For Linux/Mac users
source venv/bin/activate
```
### 3. Setup Airflow
In order to setup Airflow it is necessary to downgrade the Python version to a stable release as it is said here: [Releases Apache Airflow](https://github.com/apache/airflow/?tab=readme-ov-file#requirements), so I downgraded mine to `3.12.8` and the version of apache is 2.10.5 it should be done manually
> Note: best way to downgrade your python version is to use [pyenv](https://github.com/pyenv/pyenv) 
> `pyenv install 3.12` and then
> `pyenv global 3.12` 
```bash
pip install 'apache-airflow==2.10.5' --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.10.5/constraints-3.12.txt"

# Running from MacOS
airflow db init
airflow users create --username admin --password admin --role Admin --email example.com@gmail.com --firstname John --lastname Doe

# These both should be runned at the same time
airflow webserver -p 8080 &  # Start the Airflow webserver
airflow scheduler &  # Start the Airflow scheduler

# Make Sure to install java
brew install java
```