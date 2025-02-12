# CMD 指令

> **顯示防火牆目前是否已開啟**
>> ```cmd
>> netsh advfirewall show allprofile state
>> ```

> **顯示所有防火牆規則**
>> ```cmd
>> netsh advfirewall firewall show rule name=all  
>> ```

> **顯示 Administrators 群組內的成員**
>> ```cmd
>> net localgroup "Administrators"
>> ```

> **顯示系統資訊**
>> ```cmd
>> systeminfo
>> ```

> **顯示NTP校時資訊**
>> ```cmd
>> w32tm /query /peers
>> ```

> **顯示NetBIOS狀態**
>> ```cmd
>> nbtstat -n
>> ```

> **產生GPO清單(html及xml格式)**
>> ```cmd
>> gpresult /f /h ".\%COMPUTERNAME%\GPO_report.html"
>> gpresult /f /x ".\%COMPUTERNAME%\GPO_report.xml"
>> ```

<br>

# PowerShell 指令

> **顯示已安裝的軟體清單，以及其版本**
>> ```powershell
>> Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\*" | Select-Object DisplayName, DisplayVersion | Where-Object { $_.DisplayName -ne $null }  
>> ```

> **顯示所有"已啟用"的防火牆規則**
>> ```powershell
>> Get-NetFirewallRule | Select-Object Name, DisplayName, Description, DisplayGroup, Direction, Enabled, Profile | Where-Object { $_.Enabled -eq "True" }
>> ```

> **顯示SMBv1及SMBv2狀態**
>> ```powershell
>> Get-SmbServerConfiguration | Select EnableSMB*Protocol
>> ```

> **顯示已開啟的ShareFolder及權限設定**
>> ```powershell
>> Get-SmbShare | ForEach-Object { Get-SmbShareAccess -Name $_.Name }
>> ```

> **顯示WinEventLog的設定**
>> ```powershell
>> Get-EventLog -List
>> ```

> **計算Folder內所有檔案的hash值**
>> ```powershell
>> Get-ChildItem "Input_Folder_Path" -File | ForEach-Object { [PSCustomObject]@{ FileName = $_.Name; Hash = (Get-FileHash -Path $_.FullName -Algorithm SHA256).Hash } }
>> ```

> **計算單一檔案的hash值**
>> ```powershell
>> Get-FileHash -Path "Input_File_Path" -Algorithm SHA256).Hash
>> ```

> **將膽案或資料夾進行壓縮**
>> ```powershell
>> Compress-Archive -Path "Input_Path" -DestinationPath "Output_File_Path" -Force
>> ```
