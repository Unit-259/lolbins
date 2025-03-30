# LOLBin PowerShell Module

A PowerShell module designed to interact with the [LOLBAS API](https://lolbas-project.github.io/api/lolbas.json) to learn about and explore Windows LOLBins (Living Off the Land Binaries). The module provides functions to refresh data, validate file paths, search and filter LOLBins by various criteria, and retrieve detection or usage details.

## Table of Contents
- [Overview](#overview)
- [Installation](#installation)
- [Usage](#usage)
  - [Update-LOLBinData](#update-lolbindata)
  - [Test-LOLBinPaths](#test-lolbinpaths)
  - [Get-LOLBinSummary](#get-lolbinsummary)
  - [Get-LOLBinByName](#get-lolbinbyname)
  - [Get-LOLBinUsage](#get-lolbinusage)
  - [Search-LOLBin](#search-lolbin)
  - [Find-LOLBinByMitreID](#find-lolbinbymitreid)
  - [Find-LOLBinByTag](#find-lolbinbytag)
  - [Get-LOLBinCategory](#get-lolbincategory)
  - [Get-LOLBinDetection](#get-lolbindetection)
- [Contributing](#contributing)
- [License](#license)

## Overview

This module leverages the LOLBAS API to:
- Refresh and load the latest LOLBAS data.
- Validate the existence of files listed as potential LOLBins on your system.
- Provide summary information, usage details, and detection rules for each LOLBin.
- Search or filter LOLBins by name, keywords, MITRE ATT&CK IDs, tags, or categories.

Each function is designed with consistent output and built-in parameter validation for improved usability.

## Installation

1. **Clone or Download** the module files to your local machine.
2. **Import the Module** in your PowerShell session:
    
    Import-Module <Path-to-Module>\LOLBinModule.psm1
    
3. (Optional) To ensure you’re working with the latest data, run:
    
    Update-LOLBinData

## Usage

### Update-LOLBinData

Refreshes the local `$lolbinData` variable by downloading the latest JSON from the LOLBAS API.

    # Refresh LOLBAS data from the official endpoint
    Update-LOLBinData

    # Optional: Specify a different URL if needed
    Update-LOLBinData -Url "https://lolbas-project.github.io/api/lolbas.json"

### Test-LOLBinPaths

Tests each LOLBin's file paths and returns only those LOLBins with valid paths on your system.

    # Get LOLBins with existing file paths
    Test-LOLBinPaths

### Get-LOLBinSummary

Displays a high-level summary of LOLBins, including key fields such as Name, Description, Author, Categories, Privileges, and Operating Systems.

    # Get summary for a specific LOLBin
    Get-LOLBinSummary -Name "AddinUtil.exe"

    # Get summary for all LOLBins
    Get-LOLBinSummary

### Get-LOLBinByName

Retrieves the full JSON object of a LOLBin by its name, including commands, detection rules, and resources.

    Get-LOLBinByName -Name "Certutil.exe"

### Get-LOLBinUsage

Returns detailed usage information (commands, use cases, categories, MITRE ID, etc.) for a specified LOLBin.

    Get-LOLBinUsage -Name "Bitsadmin.exe"

### Search-LOLBin

Searches LOLBins by a keyword across the Description and Command fields. Use the `-Extended` switch to include additional fields like Usecase, Category, or Tags.

    # Basic search by keyword
    Search-LOLBin -Keyword "proxy"

    # Extended search including additional fields
    Search-LOLBin -Keyword "proxy" -Extended

### Find-LOLBinByMitreID

Finds all LOLBins associated with a specific MITRE ATT&CK ID (e.g., T1218).

    Find-LOLBinByMitreID -MitreID "T1218"

### Find-LOLBinByTag

Returns LOLBins that include a given tag (e.g., `Download`, `Execute`, or `AWL Bypass`) in their command definitions.

    Find-LOLBinByTag -Tag "Download"

### Get-LOLBinCategory

Lists all distinct LOLBin categories if no parameter is provided; otherwise, returns LOLBins in a specific category.

    # List all unique categories
    Get-LOLBinCategory

    # Get all LOLBins in the "Execute" category
    Get-LOLBinCategory -Category "Execute"

### Get-LOLBinDetection

Displays detection-related information such as Sigma rules, Splunk queries, Elastic rules, and IOCs for a specified LOLBin.

    Get-LOLBinDetection -Name "AddinUtil.exe"

---

Enjoy exploring LOLBins with this module, and happy scripting!
