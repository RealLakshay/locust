# Monolith Performance Testing with Locust

This repository contains a **monolithic FastAPI application** along with a **Locust-based load testing suite** to evaluate system performance under varying concurrency levels. The setup is intended for experimentation, benchmarking, and performance analysis in a controlled local environment.

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/reallakshay/locust.git
cd locust
```

---

### 2. Set Up the Virtual Environment

To keep dependencies isolated and avoid conflicts, create and activate a virtual environment.

**On Windows (PowerShell):**

```powershell
python -m venv .venv
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
.\.venv\Scripts\activate
```

**On macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

### 3. Install Dependencies

Install all required Python packages, including **FastAPI**, **Uvicorn**, and **Locust**:

```bash
pip install -r requirements.txt
```

---

## 🛠 Running the Application

### Start the FastAPI Server

Run the FastAPI application using Uvicorn:

```bash
python -m uvicorn main:app --reload
```

The API will be available at:

```
http://127.0.0.1:8000
```

---

### Initialize the Database

Before running performance tests, ensure the SQLite database is populated:

```bash
python insert_events.py
```

This script inserts sample data required by the checkout workflow.

---

## 📈 Load Testing with Locust

### Launch Locust

Open a **new terminal window** (with the virtual environment activated) and run:

```bash
python -m locust -f locust/checkout_locustfile.py
```

---

### Configure the Test

Open your browser and navigate to:

```
http://localhost:8089
```

Recommended initial settings:

- **Number of users:** 10–100  
- **Spawn rate:** 1–5 users/second  
- **Host:** http://127.0.0.1:8000

---

### Analyze Results

While the test is running, observe:

- Average and percentile response times
- Request failure rates
- Throughput (requests per second)
- CPU usage during peak load

Pay special attention to how the `checkout_logic` function behaves under high concurrency, as it is intentionally CPU-intensive for benchmarking purposes.

---

## 📁 Project Structure

```
.
├── main.py                # FastAPI application entry point
├── checkout/              # Core checkout business logic
├── locust/
│   └── checkout_locustfile.py  # Locust performance test definition
├── database.py            # SQLite database utilities
├── insert_events.py       # Database initialization script
├── requirements.txt       # Python dependencies
└── README.md
```

---

## 🧪 Use Cases

- Benchmarking monolithic FastAPI services
- Studying CPU-bound request behavior
- Comparing performance before and after optimizations
- Demonstrating load testing concepts using Locust

---

## 📌 Next Steps

You can extend this repository by adding:

- Automated benchmark scripts
- Result summary tables for lab reports
- CI-based load testing workflows
- Troubleshooting documentation for common SQLite and concurrency issues

---

## 📄 License

This project is intended for educational and experimental purposes. Add a license file if you plan to reuse or distribute it publicly.

---

Happy load testing 🚀

