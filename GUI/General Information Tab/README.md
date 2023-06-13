

# Tab 1 - General Information

Description : Displays machine, user, capabilities, and network information

| Element | Name | Description | 
| -------------------- | -------------------- | -------------------- |
| Tab Control | Guna2tabcontrol2 |                    | --- |
| Machine Information Tab | [machine_information_tab](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/GUI/General%20Information%20Tab#machine-information-tab--machine_information_tab) |   Displays information about machine as Host Name, System, Date, Time Zone, Processor Identification, Network Adapter, Up Time, Ram, Disk, Device ID information |
| Bios Information Tab | [bios_information_tab](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/GUI/General%20Information%20Tab#bios-information-tab--bios_information_tab) |   Displays bios information such as version and type |
| OS Information Tab | [os_information_tab](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/GUI/General%20Information%20Tab#os-information-tab--os_information_tab) |    Displays information about OS as   Operating System, Product Name, Os Build, Install Date |
| User Information Tab | [user_information_tab](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/GUI/General%20Information%20Tab#user-information-tab--user_information_tab) |   Displays information User as Register Owener, Domain, Logged in user |
| Reporting Tab | [reporting_tab](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/GUI/General%20Information%20Tab#reporting-tab--reporting_tab) |  Export Report |

<br>

## Machine Information Tab : machine_information_tab

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


## Bios Information Tab : bios_information_tab

Description : Displays bios information such as version and type

+ Table Layout : bios_information_table
  - Label : bios_date_result.Text = [BIOS_Information.Get_Bios_Date()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/BIOS_Information%20Class#get_bios_date)
  - Label : bios_version_result.Text = [BIOS_Information.Get_Bios_Version()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/BIOS_Information%20Class#get_bios_version)
## OS Information Tab : os_information_tab

Description : Displays information about OS as Operating System, Product Name, Os Build, Install Date

+ Table Layout : os_information_table
  - Label : operating_system_result.Text = [OS_Information.Get_Operating_System_And_Version()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_operating_system_and_version)
  - Label : operating_system_bitness_result.Text = [OS_Information.Get_Operating_System_Bitness()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_operating_system_bitness)
  - Label : product_name_result.Text = [OS_Information.Get_Product_Name()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_product_name)
  - Label : product_id_result.Text = [OS_Information.Get_Product_ID()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_product_id)
  - Label : os_build_result.Text = [OS_Information.Get_OS_Buil_dNumber()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_os_buil_dnumber)
  - Label : system_directory_result.Text = [Environment.SystemDirectory](https://learn.microsoft.com/en-us/dotnet/api/system.environment.systemdirectory?view=net-7.0)
  - Label : install_date_result.Text = [OS_Information.Get_OS_Install_Date()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/OS_Information%20Class#get_os_install_date)

## User Information Tab : user_information_tab

Description : Displays information User as Register Owener, Domain, Logged in user

+ Table Layout : user_information_table
  - Label : register_owener_result.Text = [User_Information.Get_Registered_Owner()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/User_Information%20Class#get_registered_owner)
  - Label : registered_organisations_result.Text = [User_Information.Get_Registered_Organization()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/User_Information%20Class#get_registered_organization)
  - Label : domain_result.Text = [Environment.UserDomainName](https://learn.microsoft.com/en-us/dotnet/api/system.environment.userdomainname?view=net-7.0)
  - Label : logged_in_user_result.Text = [Environment.UserName](https://learn.microsoft.com/en-us/dotnet/api/system.environment.username?view=net-7.0)

## Reporting Tab : reporting_tab

Description : Export Report

Description : " -- "
+ Button : machine_reporting_button
+ Button : bios_reporting_button
+ Button : os_reporting_button
+ Button : user_reporting_button
+ Button : all_general_reporting_button <br>
Click Event : [ExportReports.ConvertTableLayoutPanelToPdf()]( )
