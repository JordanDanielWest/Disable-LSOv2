# Disable-LSOv2

<#
.SYNOPSIS
    Disables Large Send Offload (LSO v2 for IPv4 and IPv6) to prevent upload speed degradation on Windows systems.

.NOTES
    Author          : ChatGPT (Generated for Jordan West)
    LinkedIn        : https://www.linkedin.com/in/jordan-west-it/
    GitHub          : https://github.com/JordanDanielWest
    Date Created    : 2025-05-23
    Last Modified   : 2025-05-23
    Version         : 1.0
    CVEs            : N/A
    Plugin IDs      : N/A
    STIG-ID         : CUSTOM-NET-0001

.TESTED ON
    Date(s) Tested  : 2025-05-23
    Tested By       : Jordan West
    Systems Tested  : Windows 10, Windows 11
    PowerShell Ver. : 5.1+

.USAGE
    Run this script as Administrator to disable LSO v2 (IPv4 and IPv6) on all Ethernet adapters.
    Example syntax:
    PS C:\> .\Disable-LSOv2.ps1

#>

# Disable LSO v2 on all Ethernet adapters
Get-NetAdapterAdvancedProperty -Name "*" -DisplayName "Large Send Offload v2 (IPv4)" -ErrorAction SilentlyContinue | `
    Set-NetAdapterAdvancedProperty -DisplayName "Large Send Offload v2 (IPv4)" -DisplayValue "Disabled"

Get-NetAdapterAdvancedProperty -Name "*" -DisplayName "Large Send Offload v2 (IPv6)" -ErrorAction SilentlyContinue | `
    Set-NetAdapterAdvancedProperty -DisplayName "Large Send Offload v2 (IPv6)" -DisplayValue "Disabled"

Write-Host "Large Send Offload v2 (IPv4 and IPv6) has been disabled on all Ethernet adapters."
