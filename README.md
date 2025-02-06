# GetMonitorSN-Win
Gets the Monitor Serial Numbers from WMI. A short yet complex script that pulls monitor serial numbers. It will report multiple. Can be looped into Management consoles or run with a foreach.

# Script Breakdown
Decode Function:

The Decode function takes a byte array as input and converts it to an ASCII string.
Parameter:
$Data: Byte array to be decoded.
function Decode {
    param ([byte[]]$Data)
    [System.Text.Encoding]::ASCII.GetString($Data)

Retrieve Monitor Information:

Uses Get-WmiObject to retrieve monitor information from the WmiMonitorID class in the root\wmi namespace.
$Monitors = Get-WmiObject WmiMonitorID -Namespace root\wmi
Decode and Output Serial Numbers:

Iterates through each monitor object, decodes the SerialNumberID property, and outputs the serial number.
foreach ($Monitor in $Monitors) {
    $SerialNumber = Decode $Monitor.SerialNumberID
    Write-Output "Monitor Serial Number: $SerialNumber"
}

# Example Output
When the script is executed, it will output the serial numbers of all connected monitors, for example:

Monitor Serial Number: ABC123456
Monitor Serial Number: XYZ987654

# Requirements
PowerShell
Administrative privileges to run the script
