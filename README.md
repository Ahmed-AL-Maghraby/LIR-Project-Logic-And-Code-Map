# Project Logic And Code Map
.<br>.<br>.<br>.<br>.<br>.<br>.<br>.<br>
# Form 1 - Tab Control : Guna2tabcontrol
it have 4 tabs
## Tab 1 - General I nformation
### Tab Control : Guna2tabcontrol2
#### Tab1 Machine Information : machine_information_tab
+ Panel : machin_information_panel
+ Table Layout : machine_information_table
  - Label : machine_name_result < Environment.MachineName
  - Label : host_name_result < Dns.GetHostName()
  - Label : system_date_result < DateTime.Now.ToString()
  - Label : time_zone_standerd_result.Text < TimeZoneInfo.Local.ToString()
  - Label : processor_identification_result < Machine_Information.Get_Processor_Identification()
  - Label : primary_network_adabter_mac_result < Machine_Information.Get_Primary_Adapter_Mac()
  - Label : uptime_result < Machine_Information.Get_System_Uptime()
  - Label : 
  - Label : 


