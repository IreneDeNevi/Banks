# ETL Pipeline: Top 10 Largest Banks Analysis

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Colab](https://img.shields.io/badge/Google-Colab-orange.svg)](https://colab.research.google.com/)
[![Status](https://img.shields.io/badge/Status-Complete-success.svg)]()

## 📊 Project Overview

An automated **ETL (Extract, Transform, Load)** data pipeline that retrieves, processes, and stores information about the world's top 10 largest banks by market capitalization. This project demonstrates core data engineering principles including web scraping, data transformation, and multi-format data persistence.

### 🎯 Key Features

- **Automated Data Extraction**: Web scraping from Wikipedia using BeautifulSoup
- **Multi-Currency Transformation**: Real-time conversion from USD to GBP, EUR, and INR
- **Dual Storage System**: Data persistence in both CSV and SQLite database formats
- **Comprehensive Logging**: Timestamped tracking of all ETL operations
- **SQL Analytics**: Built-in query execution for data analysis
- **Google Colab Ready**: Fully compatible with cloud-based execution

---

## 🚀 Quick Start

### Option 1: Google Colab (Recommended)

```bash
# 1. Upload banks_project_colab.ipynb to Google Colab
# 2. Run all cells
# 3. Download generated files
```

### Option 2: Local Execution

```bash
# Clone the repository
git clone https://github.com/yourusername/banks-etl-pipeline.git
cd banks-etl-pipeline

# Install dependencies
pip install -r requirements.txt

# Run the ETL pipeline
python banks_project.py
```

---

## 📁 Project Structure

```
banks-etl-pipeline/
│
├── banks_project_colab.ipynb    # Google Colab notebook version
├── requirements.txt              # Project dependencies
├── README.md                     # Project documentation
│
├── output/                       # Generated files (gitignored)
   ├── Largest_banks_data.csv   # Transformed data
   ├── Banks.db                  # SQLite database
   └── code_log.txt              # Execution logs

```

---

## 🛠️ Technologies Used

| Technology               | Purpose                           |
| ------------------------ | --------------------------------- |
| **Python 3.8+**    | Core programming language         |
| **Pandas**         | Data manipulation and analysis    |
| **NumPy**          | Numerical computations            |
| **BeautifulSoup4** | Web scraping and HTML parsing     |
| **Requests**       | HTTP requests for data retrieval  |
| **SQLite3**        | Lightweight database storage      |
| **Google Colab**   | Cloud-based execution environment |

---

## 📋 ETL Pipeline Workflow

### 1️⃣ **EXTRACT**

- Fetches data from Wikipedia (archived version for consistency)
- Parses HTML tables using BeautifulSoup
- Extracts bank names and market capitalization in USD

### 2️⃣ **TRANSFORM**

- Retrieves real-time exchange rates from CSV source
- Converts USD values to:
  - 🇬🇧 British Pound (GBP)
  - 🇪🇺 Euro (EUR)
  - 🇮🇳 Indian Rupee (INR)
- Rounds all values to 2 decimal places

### 3️⃣ **LOAD**

- Exports transformed data to CSV file
- Creates SQLite database table
- Maintains data integrity across formats

### 4️⃣ **ANALYZE**

- Executes SQL queries for insights
- Generates summary statistics
- Provides data validation

---

## 💻 Code Example

```python
# Import and initialize
from banks_project import extract, transform, load_to_csv, load_to_db

# Extract data
data = extract(URL, ['Name', 'MC_USD_Billion'])

# Transform with currency conversion
transformed_data = transform(data, EXCHANGE_RATE_CSV)

# Load to multiple destinations
load_to_csv(transformed_data, 'output.csv')
load_to_db(transformed_data, connection, 'banks_table')
```

---

## 📊 Sample Output

### Extracted & Transformed Data

| Name            | MC_USD_Billion | MC_GBP_Billion | MC_EUR_Billion | MC_INR_Billion |
| --------------- | -------------- | -------------- | -------------- | -------------- |
| JPMorgan Chase  | 432.92         | 346.34         | 402.62         | 35,910.71      |
| Bank of America | 231.52         | 185.22         | 215.31         | 19,204.58      |
| ICBC China      | 194.56         | 155.65         | 181.02         | 16,138.46      |
| Wells Fargo     | 155.87         | 124.72         | 144.96         | 12,936.67      |
| HSBC Holdings   | 148.90         | 119.15         | 138.48         | 12,354.71      |

### SQL Query Results

```sql
-- Average market cap in GBP
SELECT AVG(MC_GBP_Billion) AS Average_MC_GBP 
FROM Largest_banks;

-- Result: 187.45 Billion GBP
```

---

## 📖 Function Documentation

### Core Functions

#### `log_progress(message)`

Logs ETL pipeline progress with timestamps.

**Parameters:**

- `message` (str): Log entry description

**Output:** Appends to `code_log.txt`

---

#### `extract(url, table_attribs)`

Extracts bank data from Wikipedia.

**Parameters:**

- `url` (str): Source URL
- `table_attribs` (list): DataFrame column names

**Returns:** `pd.DataFrame` with extracted data

---

#### `transform(df, csv_path)`

Applies currency conversions to dataset.

**Parameters:**

- `df` (pd.DataFrame): Input data
- `csv_path` (str): Exchange rates CSV URL

**Returns:** `pd.DataFrame` with additional currency columns

---

#### `load_to_csv(df, output_path)`

Exports data to CSV format.

**Parameters:**

- `df` (pd.DataFrame): Data to export
- `output_path` (str): Destination file path

---

#### `load_to_db(df, sql_connection, table_name)`

Loads data into SQLite database.

**Parameters:**

- `df` (pd.DataFrame): Data to load
- `sql_connection`: SQLite connection object
- `table_name` (str): Target table name

---

#### `run_query(query, sql_connection)`

Executes SQL queries and displays results.

**Parameters:**

- `query` (str): SQL query string
- `sql_connection`: SQLite connection object

---

## 🔧 Configuration Parameters

| Parameter             | Value                        | Description           |
| --------------------- | ---------------------------- | --------------------- |
| `URL`               | Wikipedia Banks List         | Data source URL       |
| `EXCHANGE_RATE_CSV` | IBM Cloud Storage            | Exchange rates source |
| `OUTPUT_CSV_PATH`   | `./Largest_banks_data.csv` | CSV output location   |
| `DATABASE_NAME`     | `Banks.db`                 | SQLite database name  |
| `TABLE_NAME`        | `Largest_banks`            | Database table name   |
| `LOG_FILE`          | `code_log.txt`             | Log file location     |

---

## 📦 Installation

### Prerequisites

- Python 3.8 or higher
- pip package manager

### Dependencies

```bash
pip install -r requirements.txt
```

**requirements.txt:**

```
requests>=2.31.0
beautifulsoup4>=4.12.0
pandas>=2.0.0
numpy>=1.24.0
lxml>=4.9.0
```

---

## 🎓 Learning Outcomes

This project demonstrates proficiency in:

- ✅ **Web Scraping**: Extracting structured data from HTML
- ✅ **Data Transformation**: Processing and converting data formats
- ✅ **Data Persistence**: Multi-format storage (CSV, SQL)
- ✅ **Database Operations**: SQL query execution and management
- ✅ **Error Handling**: Robust exception management
- ✅ **Logging**: Comprehensive operation tracking
- ✅ **Code Organization**: Modular, reusable functions
- ✅ **Documentation**: Clear, professional code documentation

---

## 🔍 Use Cases

- **Financial Analysis**: Track banking sector market trends
- **Currency Markets**: Multi-currency comparative analysis
- **Data Engineering Portfolio**: Demonstrate ETL capabilities
- **Automated Reporting**: Quarterly financial reports
- **Educational Purpose**: Learn data pipeline construction

---

## 🐛 Troubleshooting

### Common Issues

**Problem:** `ModuleNotFoundError: No module named 'bs4'`

```bash
Solution: pip install beautifulsoup4
```

**Problem:** Network timeout during data extraction

```bash
Solution: Check internet connection; script will retry automatically
```

**Problem:** Database locked error

```bash
Solution: Close existing database connections before running script
```

**Problem:** Exchange rate CSV not loading

```bash
Solution: Verify CSV URL is accessible; check network permissions
```

---

## 📈 Performance Metrics

- **Execution Time**: ~15-30 seconds (depending on network speed)
- **Data Volume**: 10 records with 5 attributes each
- **Memory Usage**: <50 MB
- **Database Size**: ~4 KB
- **Log File Size**: ~1 KB

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Your Name**

- GitHub: [@IreneDeNevi](https://github.com/IreneDeNevi)
- LinkedIn: [Irene De Nevi](https://www.linkedin.com/in/irene-denevi/)

---

## 🙏 Acknowledgments

- **Data Source**: Wikipedia (List of Largest Banks)
- **Exchange Rates**: IBM Skills Network
- **Inspiration**: IBM Data Engineering Professional Certificate
- **Tools**: Python, Pandas, BeautifulSoup4

---

## 📚 Additional Resources

- [Python Documentation](https://docs.python.org/3/)
- [Pandas User Guide](https://pandas.pydata.org/docs/user_guide/index.html)
- [BeautifulSoup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [SQLite Tutorial](https://www.sqlitetutorial.net/)
- [ETL Best Practices](https://www.integrate.io/blog/etl-best-practices/)

---

## 🔄 Future Enhancements

- [ ] Add support for more currencies (JPY, CNY, CHF)
- [ ] Implement data visualization with charts
- [ ] Add automated email reporting
- [ ] Create REST API endpoints
- [ ] Add unit tests and CI/CD pipeline
- [ ] Implement data validation rules
- [ ] Add historical data tracking
- [ ] Create dashboard with real-time updates

---

## 📊 Project Statistics

![GitHub stars](https://img.shields.io/github/stars/yourusername/banks-etl-pipeline?style=social)
![GitHub forks](https://img.shields.io/github/forks/yourusername/banks-etl-pipeline?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/yourusername/banks-etl-pipeline?style=social)

---

**⭐ If you find this project useful, please consider giving it a star!**

---

*Last Updated: November 2025*
