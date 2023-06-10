# Project Logic And Code Map
.<br>.<br>.<br>.<br>.<br>.<br>.<br>.<br>
# Form 1 - Tab Control : Guna2tabcontrol
.<br>.<br>.<br>.<br>.<br>.<br>.<br>.<br>
## Tab 1 - General I nformation

.<br>.<br>.<br>

It have  Tab Control : Guna2tabcontrol2

.<br>.<br>.<br>

#### SubTab1 Machine Information : machine_information_tab
+ Panel : machin_information_panel
+ Table Layout : machine_information_table
  - Label : machine_name_result.Text = [Environment.MachineName]( )
  - Label : host_name_result.Text = [Dns.GetHostName()]( )
  - Label : system_date_result.Text = [DateTime.Now.ToString()]( )
  - Label : time_zone_standerd_result.Text = [TimeZoneInfo.Local.ToString()]( )
  - Label : processor_identification_result.Text = [Machine_Information.Get_Processor_Identification()]( )
  - Label : primary_network_adabter_mac_result.Text = [Machine_Information.Get_Primary_Adapter_Mac()]( )
  - Label : uptime_result.Text = [Machine_Information.Get_System_Uptime()]( )
  - Label : installed_ram_result.Text = [Machine_Information.Get_Installed_RAM()]( )
  - Label : device_id_result.Text = [Machine_Information.Get_Device_ID()]( )
  - Label : hard_disk_result.Text = [Machine_Information.Get_Disk_Information()]( )


#### Sub Tab2 Bios Information : bios_information_tab
+ Table Layout : bios_information_table
  - Label : bios_date_result.Text = [BIOS_Information.Get_Bios_Date()]( )
  - Label : bios_version_result.Text = [BIOS_Information.Get_Bios_Version()]( )
#### Sub Tab3 OS Information : os_information_tab
+ Table Layout : os_information_table
  - Label : operating_system_result.Text = [OS_Information.Get_Operating_System_And_Version()]( )
  - Label : operating_system_bitness_result.Text = [OS_Information.Get_Operating_System_Bitness()]( )
  - Label : product_name_result.Text = [OS_Information.Get_Product_Name()]( )
  - Label : product_id_result.Text = [OS_Information.Get_Product_ID()]( )
  - Label : os_build_result.Text = [OS_Information.Get_OS_Buil_dNumber()]( )
  - Label : system_directory_result.Text = [Environment.SystemDirectory]( )
  - Label : install_date_result.Text = [OS_Information.Get_OS_Install_Date()]( )

#### Sub Tab4 User Information : user_information_tab
+ Table Layout : user_information_table
  - Label : register_owener_result.Text = [User_Information.Get_Registered_Owner()]( )
  - Label : registered_organisations_result.Text = [User_Information.Get_Registered_Organization()]( )
  - Label : domain_result.Text = [Environment.UserDomainName]( )
  - Label : logged_in_user_result.Text = [Environment.UserName]( )

#### Sub Tab5 Reporting : reporting_tab
Description : " -- "
+ Button : machine_reporting_button
+ Button : bios_reporting_button
+ Button : os_reporting_button
+ Button : user_reporting_button
+ Button : all_general_reporting_button <br>
Click Event : [ExportReports.ConvertTableLayoutPanelToPdf()]( )


## Tab 2 - Running Process : running_processes_tab

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

Description : " -- "

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
























