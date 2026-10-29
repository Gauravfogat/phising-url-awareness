# EWB Phishing URL Awareness Checker

## Overview

Phishing is a trick where fake links or messages try to make people share passwords, payment details, OTPs, or other sensitive information. This project is a beginner-friendly Python command-line tool that reads a URL as text and highlights selected visible warning signs.

The program is **text-only**. It never opens the URL, scans a website, contacts a reputation service, or sends the entered data anywhere.

## Features

- Detects an `@` symbol in the URL.
- Flags unusually long URLs over 100 characters.
- Flags IP-address hostnames.
- Flags hostnames with 5 or more segments.
- Flags punycode-style hostnames containing `xn--`.
- Flags the HTTP scheme.
- Handles malformed URL input without crashing.
- Allows repeated checks in one run and supports `q`, `quit`, or `exit`.
- Shows a clear **REVIEW CAREFULLY** summary when warning signs are found.

## Project Structure

```text
phishing-url-awareness/
├── phishing_checker.py
├── README.md
├── requirements.txt
├── tests/
│   └── test_samples.md
└── screenshots/
    ├── sample_run.png
    └── test_results.png
```

## Requirements

- Python 3.10 or later
- No extra Python packages are required.

## How to Run

### Windows

```bash
python phishing_checker.py
```

### macOS / Linux

```bash
python3 phishing_checker.py
```

Then enter a sample URL when prompted. Type `q` to quit.

## Example Output

```text
EWB Phishing URL Awareness Checker
Text checks only - this program does not open URLs.

Enter a sample URL (or type q to quit): http://192.0.2.10/account

Result:
- Uses an IP address instead of a familiar domain.
- Uses HTTP. HTTPS alone does not prove trust.

REVIEW CAREFULLY: 2 warning sign(s) found.
Never enter passwords from unexpected links.
```

## Testing

The five required workbook sample strings were tested:

| # | Input | Expected | Actual | Result |
|---|---|---|---|---|
| 1 | `https://www.example.com/login` | No warning signs | No listed warning signs found | PASS |
| 2 | `http://192.0.2.10/account` | IP address + HTTP | IP address + HTTP warnings | PASS |
| 3 | `http://example.com@sample.invalid/login` | @ symbol + HTTP | @ symbol + HTTP warnings | PASS |
| 4 | `https://a.b.c.d.e.example.invalid/path` | Many hostname segments | Many hostname segments warning | PASS |
| 5 | `https://xn--example.invalid/` | Punycode-style hostname | Punycode-style hostname warning | PASS |

A malformed-input check was also performed with `http://[bad`; the program returned a friendly message instead of crashing.

See `tests/test_samples.md` for detailed evidence.

## Screenshots

![Sample run](screenshots/sample_run.png)

![Test results](screenshots/test_results.png)

## Improvements

1. **Repeat-check loop** - The program can inspect several URLs without being restarted. The user can type `q`, `quit`, or `exit` to finish.
2. **Malformed-input handling** - URL parsing is protected with `try/except`, so malformed input such as `http://[bad` produces a clear message instead of a Python traceback.
3. **Review summary** - When warning signs are found, the program displays the number of warnings and asks the user to review the link carefully.

## Limitations

This is an educational awareness tool. It only reads URL text. It does not visit URLs, scan for malware, query reputation services, or prove that a URL is safe.

**No warning signs found does NOT mean a URL is safe.** The program checks only six selected clues.

## Ethical Use

Use sample strings for learning. Do not collect credentials, send phishing messages, or probe websites without written authorization. Never upload passwords, API keys, tokens, or confidential information to GitHub.

## Author

EWB Cybersecurity Internship Student
