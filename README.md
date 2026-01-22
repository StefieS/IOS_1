# IOS - Project 1

XTF (eXchange Transaction Filter) - Shell script for analyzing cryptocurrency exchange transaction logs.

## 📋 What It Does

A POSIX-compliant shell script that processes and analyzes cryptocurrency exchange logs:
- Filter transactions by user, date, and currency
- Display account balances and transaction history
- Calculate profits with configurable rates
- Support both plain text and gzipped log files

## 🔨 How to Use

### Basic Syntax

```bash
./xtf [-h|--help] [FILTER] [COMMAND] USER LOG [LOG2 [...]]
```

### Commands

- `list` - List all records for the given user (default)
- `list-currency` - List sorted currencies used by the user
- `status` - Display current account status (balance per currency)
- `profit` - Display account status with fictional profit applied

### Filters

- `-a DATETIME` - Records after this date (exclusive)
- `-b DATETIME` - Records before this date (exclusive)
- `-c CURRENCY` - Records with specific currency only

**Date format:** `YYYY-MM-DD HH:MM:SS`  
**Currency format:** Three letters (e.g., BTC, USD, EUR)

### Examples

```bash
# List all transactions for user john
./xtf list john transaction.log

# Show status for user alice with EUR only
./xtf -c EUR status alice exchange.log

# List currencies used after specific date
./xtf -a "2024-01-01 00:00:00" list-currency bob data.log

# Calculate profit for multiple log files
./xtf profit john log1.log log2.log.gz

# Use custom profit rate (via environment variable)
export XTF_PROFIT=15
./xtf profit john transaction.log
```

## 📄 Log File Format

Logs must follow this semicolon-separated format:
```
USERNAME;DATETIME;CURRENCY;VALUE
```

Example:
```
john;2024-03-15 10:30:00;BTC;0.5
alice;2024-03-15 11:00:00;EUR;-100.0
bob;2024-03-15 12:00:00;USD;250.75
```

**Field Requirements:**
- USERNAME: Any printable characters (no semicolons)
- DATETIME: `YYYY-MM-DD HH:MM:SS` format
- CURRENCY: Exactly 3 letters
- VALUE: Decimal number (max 4 decimal places), can be negative

## 💰 Profit Calculation

Default profit rate: 20% (1.2x multiplier)

Custom rate via environment variable:
```bash
export XTF_PROFIT=15  # 15% profit
./xtf profit john transaction.log
```

**Note:** Profit only applies to positive balances.

## 📁 Files

```
IOS_1/
├── xtf                      # Main analysis script
├── test_xtf.sh              # Test script
├── cryptoexchange-3.log     # Sample log file
├── cryptoexchange-5.log     # Sample log file
└── big_file.log             # Larger sample log
```

## 🧪 Testing

Run the test script:
```bash
./test_xtf.sh
```

## 🔧 Features

- **POSIX Compliant** - Works with standard shell utilities
- **Gzip Support** - Automatically handles `.gz` compressed logs
- **Multiple Logs** - Process multiple log files at once
- **Input Validation** - Checks date, currency, and value formats
- **Error Handling** - Clear error messages for invalid input

## 🎓 Course Info

**Course**: IOS (Operating Systems)  
**School**: FIT VUT Brno  
**Project**: Project 1 - Shell Scripting  
**Author**: Mikuláš Lešiga (xlesigm00)

## ⚙️ Requirements

- POSIX-compliant shell (sh, bash, dash)
- Standard Unix utilities (awk, sed, grep, sort, etc.)
- gzip (for compressed log support)

## ✍️ Author

StefieS (Mikuláš Lešiga)

---

**Note**: Academic project - follow your school's academic integrity policy.
