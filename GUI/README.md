# GUI Map
.<br>.<br>.<br>.<br>.<br>.<br>.<br>.<br>
# Form 1

| Element | Name | Description | 
| -------------------- | -------------------- | -------------------- |
| Tab Control | Guna2tabcontrol2 |                    | --- |
| General I nformation | [general_information_tab]( https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/GUI#tab-1---general-information ) | Displays machine, user, capabilities, and network information |
| Running Process | [running_processes_tab]( https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/GUI#tab-2---running-process--running_processes_tab ) | Displays information about the running processes and their detection in the virustotal |
| Network Connections | [network_connections_tab]( https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/GUI#tab-3---network-connections--network_connections_tab ) | Displays information about connections being made and detected in VirusTotal and AbuseIPDB_Api |
|  | [](  ) |                    | --- |


## Tab 1 - General Information

Description : Displays machine, user, capabilities, and network information

| Element | Name | Description | 
| -------------------- | -------------------- | -------------------- |
| Tab Control | Guna2tabcontrol2 |                    | --- |
| Sub Tab1 | [machine_information_tab]( https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/GUI/README.md#subtab1-machine-information--machine_information_tab ) |   Displays information about machine as Host Name, System, Date, Time Zone, Processor Identification, Network Adapter, Up Time, Ram, Disk, Device ID information |
| Sub Tab2 | [bios_information_tab]( https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/GUI/README.md#sub-tab2-bios-information--bios_information_tab ) |   Displays bios information such as version and type |
| Sub Tab3 | [os_information_tab]( https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/GUI/README.md#sub-tab3-os-information--os_information_tab ) |    Displays information about OS as   Operating System, Product Name, Os Build, Install Date |
| Sub Tab4 | [user_information_tab]( https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/GUI/README.md#sub-tab4-user-information--user_information_tab ) |   Displays information User as Register Owener, Domain, Logged in user |
| Sub Tab5 | [reporting_tab]( https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/GUI/README.md#sub-tab5-reporting--reporting_tab ) |  Export Report |

<br>

#### SubTab1 Machine Information : machine_information_tab

Description : Displays information about machine as Host Name, System, Date, Time Zone, Processor Identification, Network Adapter, Up Time, Ram, Disk, Device ID information

+ Panel : machin_information_panel
+ Table Layout : machine_information_table
  - Label : machine_name_result.Text = [Environment.MachineName](https://learn.microsoft.com/en-us/dotnet/api/system.environment.machinename?view=net-7.0)
  - Label : host_name_result.Text = [Dns.GetHostName()](https://learn.microsoft.com/en-us/dotnet/api/system.net.dns.gethostname?view=net-7.0)
  - Label : system_date_result.Text = [DateTime.Now.ToString()](https://learn.microsoft.com/en-us/dotnet/api/system.datetime.tostring?view=net-7.0)
  - Label : time_zone_standerd_result.Text = [TimeZoneInfo.Local.ToString()](https://learn.microsoft.com/en-us/dotnet/api/system.timezoneinfo.tostring?view=net-8.0)
  - Label : processor_identification_result.Text = [Machine_Information.Get_Processor_Identification()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/Machine_Information%20Class#get_processor_identification)
  - Label : primary_network_adabter_mac_result.Text = [Machine_Information.Get_Primary_Adapter_Mac()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/Machine_Information%20Class#get_primary_adapter_mac)
  - Label : uptime_result.Text = [Machine_Information.Get_System_Uptime()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/Machine_Information%20Class#get_system_uptime)
  - Label : installed_ram_result.Text = [Machine_Information.Get_Installed_RAM()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/Machine_Information%20Class#get_installed_ram)
  - Label : device_id_result.Text = [Machine_Information.Get_Device_ID()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/Machine_Information%20Class#get_device_id)
  - Label : hard_disk_result.Text = [Machine_Information.Get_Disk_Information()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/Machine_Information%20Class#get_disk_information)


#### Sub Tab2 Bios Information : bios_information_tab

Description : Displays bios information such as version and type

+ Table Layout : bios_information_table
  - Label : bios_date_result.Text = [BIOS_Information.Get_Bios_Date()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/BIOS_Information%20Class#get_bios_date)
  - Label : bios_version_result.Text = [BIOS_Information.Get_Bios_Version()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/BIOS_Information%20Class#get_bios_version)
#### Sub Tab3 OS Information : os_information_tab

Description : Displays information about OS as Operating System, Product Name, Os Build, Install Date

+ Table Layout : os_information_table
  - Label : operating_system_result.Text = [OS_Information.Get_Operating_System_And_Version()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_operating_system_and_version)
  - Label : operating_system_bitness_result.Text = [OS_Information.Get_Operating_System_Bitness()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_operating_system_bitness)
  - Label : product_name_result.Text = [OS_Information.Get_Product_Name()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_product_name)
  - Label : product_id_result.Text = [OS_Information.Get_Product_ID()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_product_id)
  - Label : os_build_result.Text = [OS_Information.Get_OS_Buil_dNumber()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_os_buil_dnumber)
  - Label : system_directory_result.Text = [Environment.SystemDirectory](https://learn.microsoft.com/en-us/dotnet/api/system.environment.systemdirectory?view=net-7.0)
  - Label : install_date_result.Text = [OS_Information.Get_OS_Install_Date()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_os_install_date)

#### Sub Tab4 User Information : user_information_tab

Description : Displays information User as Register Owener, Domain, Logged in user

+ Table Layout : user_information_table
  - Label : register_owener_result.Text = [User_Information.Get_Registered_Owner()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/User_Information%20Class#get_registered_owner)
  - Label : registered_organisations_result.Text = [User_Information.Get_Registered_Organization()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/User_Information%20Class#get_registered_organization)
  - Label : domain_result.Text = [Environment.UserDomainName](https://learn.microsoft.com/en-us/dotnet/api/system.environment.userdomainname?view=net-7.0)
  - Label : logged_in_user_result.Text = [Environment.UserName](https://learn.microsoft.com/en-us/dotnet/api/system.environment.username?view=net-7.0)

#### Sub Tab5 Reporting : reporting_tab

Description : Export Report

Description : " -- "
+ Button : machine_reporting_button
+ Button : bios_reporting_button
+ Button : os_reporting_button
+ Button : user_reporting_button
+ Button : all_general_reporting_button <br>
Click Event : [ExportReports.ConvertTableLayoutPanelToPdf()]( )


## Tab 2 - Running Process : running_processes_tab
Description : Displays information about the running processes and their detection in the virustotal
+ Panel : panel2
  + TextBox : SearchBox1
    - Event : [ProcessAction.SearchByName()]( )
  + TextBox : SearchBox2
    - Event : [ProcessAction.SearchById()]( )

  + TextBox : SearchBox3
    - Event : [ProcessAction.SearchByParentId()]( )

  + TextBox : vir_api
    - Description : Store Virustotal Api
    
  + Button : refresh_process_button
     - Click Event : [ProcessAction.remove_Process()]( ) <br>
     &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;: [RuningProcessInfo.GetProcessesInfo()]( )

  + Button : run_anti_scan
     - Click Event : [VirustotalScaner.removeHash()]( ) <br>
     &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;: [VirustotalScaner.RunScan()]( )
     
  + Button : export_process_report
     - Click Event : [ExportReports.ExportRuningProcessReport()]( )

+ Data Grid View : processTable1
  - It contains 9 columns to show ( Name - PID -Parent PID - Start Time - Instance - Image Path - User Account - Hash - Virustotal Score )



## Tab 3 - Network Connections : network_connections_tab

Description :  Displays information about connections being made and detected in VirusTotal and AbuseIPDB_Api 

+ Panel : network_tab_up_panal
  + TextBox : SearchBox4
    - Event : [ConnectionsAction.SearchByIP()]( ) 
  + TextBox : SearchBox5
    - Event : [ConnectionsAction.SearchByPID()]( ) 
  + TextBox : SearchBox6
    - Event : [ConnectionsAction.SearchByProcessName()]( ) 
  + TextBox : AbuseIPDB_Api
    - Description : Store AbuseIPDB Api
  + Button : export_connection_report
    - Click Event : [ExportReports.ExportConnectionReport()]( )
  + Button : refresh_connection_result
    - Click Event : [ConnectionsAction.remove_connection()]( ) <br>
     &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;: [Network_Connections.GetNetworkConnections()]( )


+ Data Grid View : Networktable
  - It contains 12 columns to show ( Protocol - Local Address - Out Port - Foreign Adress - Connection Port - Connection State - PID - Process Name - Host Name - IP Country - AbuseIPDB Score - VirusTotal Score )



## Tab 4 - xxx : xxx_tab
























