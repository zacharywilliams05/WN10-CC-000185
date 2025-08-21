# WN10-CC-000185
STIG Implementation WN10-CC-000185

<# 
.SYNOPSIS 
Script checks for, and creates if not existing, the NoAutoRun key in HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer

.NOTES 
Author : Zachary Williams  
LinkedIn : [linkedin.com/in/zacharywilliams05/](https://linkedin.com/in/zacharywilliams05/)  
GitHub : [github.com/zacharywilliams05](https://github.com/zacharywilliams05)  
Date Created : 2025-08-21  
Last Modified : 2024-08-21  
Version : 1.0  
CVEs : N/A  
Plugin IDs : N/A  
STIG-ID : WN10-CC-000185

.TESTED ON 
Date(s) Tested :  
Tested By :  
Systems Tested :  
PowerShell Ver. :  

.USAGE 
PS C:> .\remediation_template(STIG-ID-WN10-CC-000185).ps1 
#>

```powershell
# You may need to modify your Execution policy with
# Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
# Define the registry path and value
$registryPath = "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer"
$valueName = "NoAutoRun"
$valueData = 1

# Check if the registry key exists
if (-not (Test-Path $registryPath)) {
    # Create the registry key if it does not exist
    New-Item -Path $registryPath -Force
    Write-Host "Created registry key: $registryPath"
}

# Check if the value exists
$value = Get-ItemProperty -Path $registryPath -Name $valueName -ErrorAction SilentlyContinue

if (-not $value) {
    # Set the registry value if it does not exist
    New-ItemProperty -Path $registryPath -Name $valueName -Value $valueData -PropertyType DWord -Force
    Write-Host "Created registry value: $valueName with data: $valueData"
} else {
    Write-Host "Registry value: $valueName already exists."
}
```
