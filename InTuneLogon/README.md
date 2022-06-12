# Default Settings
- Create the scheduled task
- Runs at Logon
- Runs with Local SYSTEM account
- Runs a command specified (in this example it runs a .cmd file that requires administrative rights. The .cmd file is already present on the devices – a software vender has placed it here) 

# InTune Instructions:
1. Go to Microsoft 365 Device Management portal (https://devicemanagement.portal.azure.com)
2. Add the script with the following settings:
   - Run this script using the logged on credentials -> No
   - Enforce script signature check -> No
   - Run script in 64-bit PowerShell Host -> No
3. Assign the script to an Azure AD group containing the devices or users on which the script should run

# Running as the User instead of SYSTEM context:
1. Comment out or delete the following line:
   ```
   $STPrin = New-ScheduledTaskPrincipal -UserId "SYSTEM" -LogonType ServiceAccount
   ```
2. Remove `-Principal $STPrin` from the `Register-ScheduledTask` command under the **Create scheduled task** section

# Script Credit / Original Instructions:
https://larsstaal.com/2019/05/07/logon-scripts-in-intune/
