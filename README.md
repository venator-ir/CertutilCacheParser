# Certutil Cache Parser

Certutil Cache Reporter is a Windows forensic utility that analyzes **CryptnetUrlCache** artifacts created by `certutil.exe`. The tool enumerates cache entries across all user profiles, extracts download metadata, correlates downloaded content, calculates cryptographic hashes, performs optional YARA scanning, and exports the results to a CSV report for digital forensic investigations, incident response, and threat hunting.

---

## Features

* Enumerates CryptnetUrlCache artifacts for:

  * Standard user profiles
  * SYSTEM profile
* Supports:

  * Live Windows systems
  * Mounted forensic images
  * Offline Windows directories
* Parses Cryptnet metadata to extract:

  * Download URL
  * Download timestamp (UTC & Local)
  * HTTP Last-Modified header
  * HTTP ETag
  * Downloaded file size
* Correlates metadata with cached content files
* Calculates:

  * MD5
  * SHA-1
  * SHA-256
* Detects common file types
* Optional YARA scanning

  * Automatically downloads YARA if not supplied
  * Automatically downloads YARA Forge Core rules if not supplied
  * Supports custom YARA executables
  * Supports custom rule directories
  * Supports disabling YARA completely
* Generates a comprehensive CSV report
* Displays real-time progress and scan statistics

---

## Requirements

* Windows
* .NET 8 Runtime (or use the self-contained release)


---

## Usage

```text
CertutilCacheReporter.exe [options]
```

### Options

| Option             | Description                                           |
| ------------------ | ----------------------------------------------------- |
| `-d <WindowsRoot>` | Windows installation root (default: `C:\`)            |
| `-o <Output>`      | Output directory or CSV filename                      |
| `-e <YaraExe>`     | Path to `yara.exe` or `yara64.exe`                    |
| `-r <RulesDir>`    | Path to a directory containing `.yar` / `.yara` files |
| `--no-yara`        | Disable YARA download and scanning                    |
| `-h`, `--help`     | Show help                                             |

---

## Examples

### Scan the local system

```cmd
CertutilCacheReporter.exe
```

---

### Scan a mounted forensic image

```cmd
CertutilCacheReporter.exe -d D:\
```

---

### Save report to a custom directory

```cmd
CertutilCacheReporter.exe -o C:\Reports
```

---

### Specify the report filename

```cmd
CertutilCacheReporter.exe -o C:\Reports\Case001.csv
```

---

### Use a custom YARA executable

```cmd
CertutilCacheReporter.exe -e C:\Tools\yara64.exe
```

---

### Use custom YARA rules

```cmd
CertutilCacheReporter.exe -r C:\Rules
```

---

### Use custom YARA executable and rules

```cmd
CertutilCacheReporter.exe -e C:\Tools\yara64.exe -r C:\Rules
```

---

### Disable YARA scanning

```cmd
CertutilCacheReporter.exe --no-yara
```

---

## CSV Output

The generated report includes information such as:

* User/Profile
* Download Time (UTC)
* Download URL
* Downloaded Filename
* File Extension
* SHA-256
* MD5
* SHA-1
* YARA Match
* Matching YARA Rules
* Downloaded File Size
* Cache Key
* HTTP ETag
* HTTP Last-Modified
* File Type
* Content Exists
* Content Path
* Metadata Path
* Error Information

---

## Automatic Downloads

If no YARA executable is specified, the tool automatically downloads the latest supported Windows x64 YARA release.

If no rules directory is specified, the tool automatically downloads the latest YARA Forge Core rules.

Both are cached locally and reused on future executions.

---

## Workflow

1. Locate CryptnetUrlCache artifacts.
2. Parse metadata files.
3. Match metadata with cached content.
4. Calculate file hashes.
5. Detect file type.
6. Optionally scan files using YARA.
7. Export results to CSV.

---

## Credits

YARA rules:

* YARA Forge

---

## License

MIT License.
