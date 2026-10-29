# Test Results

Python version used: Python 3.11+
Operating system: Python execution environment
Date: 2026-10-29

| # | Input | Expected result | Actual result | Pass/Fail |
|---|---|---|---|---|
| 1 | `https://www.example.com/login` | No warning signs | No listed warning signs found. This does NOT prove safety. | **PASS** |\n| 2 | `http://192.0.2.10/account` | IP address + HTTP | Uses an IP address instead of a familiar domain. | Uses HTTP. HTTPS alone does not prove trust. | **PASS** |\n| 3 | `http://example.com@sample.invalid/login` | @ symbol + HTTP | Contains an @ symbol; inspect carefully. | Uses HTTP. HTTPS alone does not prove trust. | **PASS** |\n| 4 | `https://a.b.c.d.e.example.invalid/path` | Many hostname segments | Contains many hostname segments/subdomains. | **PASS** |\n| 5 | `https://xn--example.invalid/` | Punycode-style hostname | Contains a punycode-style hostname. | **PASS** |\n
## Additional malformed-input check

Input: `http://[bad`

Actual result:

```text
This text is not a valid URL format.
```

Result: **PASS** - malformed input is handled without a traceback.

## Notes

The project checks URL text only and does not open or contact any URL. The five required workbook samples produced the expected warning categories. The malformed-input improvement also prevents a parsing error from stopping the program.
