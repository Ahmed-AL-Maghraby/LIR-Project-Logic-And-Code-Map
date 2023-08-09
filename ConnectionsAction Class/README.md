



| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| ConnectionsAction |      Plublic     | 1 |    none     |        9           |


## Objects
```C#
public static Form1 myform = Application.OpenForms.OfType<Form1>().FirstOrDefault();
```



## Methods


| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [remove_connection]() | Static - Void | Public |  Remove all rows from the myform.Networktable DataGridView |
| [SearchByIP]() | Static - Void | Public | Search and filter rows in the myform.Networktable DataGridView control based on an IP address |
| [SearchByPID]() | Static - Void | Public | Search and filter rows based on a Process ID (PID) keyword |
| [SearchByProcessName]() | Static - Void | Public | Search and filter rows based on a process name keyword |
| [Kill_Process]() | Static - Void | Public | Terminate a selected process based on the selected row in the DataGridView |
| [Copy_IP]() | Static - Void | Public | Copy the IP address from the selected row in the DataGridView to the clipboard |
| [SearchVirusTotal]() | Static - Void | Public | open the default web browser with a VirusTotal scan URL |
| [BlockIpAddress]() | Static - Void | Public | Block an IP address using the Windows firewall |
| [BlockPort]() | Static - Void | Public | Block a network port using the Windows firewall |
| []() | Static - Void | Public | wwwwwwwwwwwwwwww |






<br>

## remove_connection

The object of this function is to remove all rows from the `myform.Networktable` DataGridView control on the main form.

```c#
public static void remove_connection()
        {
            while (myform.Networktable.Rows.Count > 0)
            {
                myform.Networktable.Rows.RemoveAt(0);
            }
        }
```

Here's how the function works:
   - It iterates through the rows of the DataGridView and removes them one by one until there are no more rows left.




<br>

## SearchByIP

The object of this function is to search and filter rows in the `myform.Networktable` DataGridView control based on an IP address keyword.


```c#
 public static void SearchByIP(string name)
        {
            string keyword = name;
            for (int i = 0; i < myform.Networktable.Rows.Count; i++)
            {
                if (myform.Networktable.Rows[i].Cells[3].Value.ToString().Contains(keyword))
                {
                    myform.Networktable.Rows[i].Visible = true;
                }
                else
                {
                    myform.Networktable.Rows[i].Visible = false;
                }
                if (keyword == string.Empty)
                {
                    myform.Networktable.Rows[i].Visible = true;
                }
            }
        }
```

Here's how the function works:
   - It takes a keyword as input and compares it with the IP addresses present in the DataGridView.
   - It iterates through each row and checks if the IP address in column index 3 contains the keyword.
   - If the keyword is found in the IP address, the row is set to be visible; otherwise, it's hidden.
   - If the keyword is empty, all rows are set to be visible.





<br>

## SearchByPID

The object of this function is to search and filter rows based on a Process ID (PID) keyword.

```c#
public static void SearchByPID(string name)
        {
            string keyword = name;
            for (int i = 0; i < myform.Networktable.Rows.Count; i++)
            {
                if (myform.Networktable.Rows[i].Cells[6].Value.ToString().Contains(keyword))
                {
                    myform.Networktable.Rows[i].Visible = true;
                }
                else
                {
                    myform.Networktable.Rows[i].Visible = false;
                }
                if (keyword == string.Empty)
                {
                    myform.Networktable.Rows[i].Visible = true;
                }
            }
        }
```

Here's how the function works:

   - It takes a keyword as input and compares it with the PIDs present in the DataGridView.
   - It iterates through each row and checks if the PID in column index 6 contains the keyword.
   - If the keyword is found in the PID, the row is set to be visible; otherwise, it's hidden.
   - If the keyword is empty, all rows are set to be visible.






<br>

## SearchByProcessName

The object of this function is to search and filter rows based on a process name keyword.

```c#
public static void SearchByProcessName(string name)
        {
            string keyword = name;
            for (int i = 0; i < myform.Networktable.Rows.Count; i++)
            {
                if (myform.Networktable.Rows[i].Cells[7].Value.ToString().Contains(keyword))
                {
                    myform.Networktable.Rows[i].Visible = true;
                }
                else
                {
                    myform.Networktable.Rows[i].Visible = false;
                }
                if (keyword == string.Empty)
                {
                    myform.Networktable.Rows[i].Visible = true;
                }
            }
        }
```

Here's how the function works:

- It takes a keyword as input and compares it with the process names present in the DataGridView.
- It iterates through each row and checks if the process name in column index 7 contains the keyword.
- If the keyword is found in the process name, the row is set to be visible; otherwise, it's hidden.
- If the keyword is empty, all rows are set to be visible.






<br>

## Kill_Process

The object of this function is to Terminate a selected process based on the selected row in the DataGridView.

```c#
public static void Kill_Process()
        {
            Process process = Process.GetProcessById(int.Parse(myform.Networktable.SelectedRows[0].Cells[6].Value.ToString()));
            try
            {
                process.Kill();
                myform.Networktable.SelectedRows[0].Visible = false;
            }
            catch (Exception ex)
            {
            }
        }
```

Here's how the function works:
   - It retrieves the PID from the selected row, converts it to an integer, and gets the corresponding `Process` object.
   - It attempts to kill the process using the `Kill()` method.
   - If the process is successfully killed, the selected row is hidden.






<br>

## Copy_IP

The object of this function is to Copy the IP address from the selected row in the DataGridView to the clipboard.

```c#
public static void Copy_IP()
        {
            Clipboard.SetText(myform.Networktable.SelectedRows[0].Cells[3].Value.ToString());
        }
```

Here's how the function works:
   - It retrieves the IP address from the selected row and sets it as the clipboard's text content.






<br>

## SearchVirusTotal

The object of this function is to open the default web browser with a VirusTotal scan URL

```c#
public static void SearchVirusTotal()
        {
            string ip = myform.Networktable.SelectedRows[0].Cells[3].Value.ToString();
            string url = $"https://www.virustotal.com/gui/file/{ip}";
            try
            {
                Process.Start("cmd", $"/C start {url}");
            }
            catch (Exception ex)
            {
            }
        }
```

Here's how the function works:
   - It constructs the URL using the IP address from the selected row and opens it in the browser.





<br>

## BlockIpAddress

The object of this function is to block an IP address using the Windows firewall.


```c#
public static void BlockIpAddress()
        {
            string ipAddress = myform.Networktable.SelectedRows[0].Cells[3].Value.ToString();
            string arguments = $"/C netsh advfirewall firewall add rule name=\"Block IP - {ipAddress}\" dir=in action=block remoteip={ipAddress}";
            Process.Start("cmd.exe", arguments);
        }
        
```

Here's how the function works:
   - It retrieves the IP address from the selected row and constructs the necessary command arguments.
   - It uses `Process.Start()` to execute the command using the Windows Command Prompt (`cmd.exe`).






<br>

## BlockPort

The object of this function is to block a network port using the Windows firewall.


```c#
public static void BlockPort()
        {
            int port = int.Parse(myform.Networktable.SelectedRows[0].Cells[3].Value.ToString());
            string arguments = $"/C netsh advfirewall firewall add rule name=\"Block Port - {port}\" dir=in action=block protocol=TCP localport={port}";
            Process.Start("cmd.exe", arguments);
        }
```

Here's how the function works:
   - It retrieves the port number from the selected row and constructs the necessary command arguments.
   - It uses `Process.Start()` to execute the command using the Windows Command Prompt (`cmd.exe`).





























