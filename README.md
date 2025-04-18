# NinjaOne Vulnerability Importer

A Windows PowerShell-based GUI and CLI tool for filtering and uploading vulnerability scan data to NinjaOne via API.

![vulnerability-management](https://github.com/user-attachments/assets/fdceeba9-0e99-4237-8125-a0fb5447a03c)

![filter options](https://github.com/user-attachments/assets/84321b97-1617-42dd-b1e7-beda6eab1892)

## ✨ Features

- ✅ WPF-based modern user interface (dark-themed)
- ✅ CSV viewer with filtering (CVSS score, severity level, keyword)
- ✅ Column selection and hostname domain stripping
- ✅ Secure storage of API credentials using DPAPI
- ✅ NinjaOne API integration (token-based with auto-refresh)
- ✅ Upload filtered CSVs to a chosen scan group
- ✅ Import/export filter configurations
- ✅ Full CLI (headless) support for automation

---

## 🖥 Requirements

- **PowerShell 5.1 or later**
- **Windows only** (WPF and DPAPI required)
- NinjaOne API access (Client ID, Secret, Base URL)

---

## 🚀 GUI Usage

1. Run the script:
    ```powershell
    .\NinjaOneVulnerabilityImporter.ps1
    ```

2. Load a CSV file (exported from a vulnerability scanner)
3. Use the filters or column selection to clean your dataset
4. Connect to NinjaOne using your API credentials
5. Select a scan group and upload

---

## ⚙️ CLI (Headless) Mode

Run the script with `-UploadOnly` and required parameters:

```powershell
.\NinjaOneVulnerabilityImporter.ps1 `
    -CSV "C:\Scans\latest.csv" `
    -ClientID "your-client-id" `
    -ClientSecret "your-client-secret" `
    -BaseURL "eu.ninjarmm.com" `
    -ScanGroupID 1234 `
    -UploadOnly

## 🔒 Security

- API credentials are encrypted using [DPAPI](https://learn.microsoft.com/en-us/windows/win32/secauthn/data-protection) and stored per-user/machine in exported filter JSON files.
- Log files are written to:  
  `%APPDATA%\NinjaOneVulnerabilityImporter\log.txt`

---

## 📂 Filter Configuration

You can import/export settings (filters, columns, API settings) via the GUI.

Example exported JSON:
```json
{
  "filters": ["test", "unmanaged"],
  "autoExport": true,
  "ScanSource": "Qualys",
  "SelectedColumns": ["deviceName", "cvssScore", "vulnerabilitySeverityLevel"],
  "ClientID": "Encrypted",
  "ClientSecret": "Encrypted",
  "BaseURL": "eu.ninjarmm.com"
}

Credits to AIVenom with his original script: https://github.com/antivenom8/aivenom/blob/main/NinjaOne/NinjaOneVulnerabilityImport.ps1
