
# Tab 3 - Network Connections : network_connections_tab

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


