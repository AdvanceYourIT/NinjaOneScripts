# NinjaOne Vulnerability Importer

Still looking for CSV Samples, just a header and 1 line of data, from the following Scan Sources: ConnectSecure, Crowdstrike Spotlight, Qualys, Rapid7 and Tenable.

This is to preconfigure colums so the uploads will be even faster.

Reach out to me on the NinjaOne Discord by doing @lobbie

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

## 🔑 Required NinjaOne API Scope

Make sure your API client has the following scope configured:

```
monitoring management offline_access
```
See the screenshot on how to properly set up your API Client App ID's in NinjaOne
![2025-04-22 12_19_54-New Client App _ NinjaOne — Mozilla Firefox](https://github.com/user-attachments/assets/53fe9330-156b-46f1-858a-5c01dc0ba8da)


This is required to authenticate, fetch scan groups, and upload CSV files.

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
```

---

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
```

---

## 🙏 Credits

Based on the original concept by [AIVenom](https://github.com/antivenom8/aivenom/blob/main/NinjaOne/NinjaOneVulnerabilityImport.ps1)

