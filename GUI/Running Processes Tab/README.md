


# Tab 2 - Running Process : running_processes_tab
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
     - Click Event : [VirustotalScaner.removeHash()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class) <br>
     &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;: [VirustotalScaner.RunScan()](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class)
     
  + Button : export_process_report
     - Click Event : [ExportReports.ExportRuningProcessReport()]( )

+ Data Grid View : processTable1
  - It contains 9 columns to show ( Name - PID -Parent PID - Start Time - Instance - Image Path - User Account - Hash - Virustotal Score )


