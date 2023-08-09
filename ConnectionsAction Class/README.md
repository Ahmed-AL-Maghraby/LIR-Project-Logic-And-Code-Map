



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
| [remove_connection]() | Static - Void | Public | wwwwwwwwwwwwwwww |
| [SearchByIP]() | Static - Void | Public | wwwwwwwwwwwwwwww |
| [SearchByPID]() | Static - Void | Public | wwwwwwwwwwwwwwww |
| [SearchByProcessName]() | Static - Void | Public | wwwwwwwwwwwwwwww |
| [Kill_Process]() | Static - Void | Public | wwwwwwwwwwwwwwww |
| [Copy_IP]() | Static - Void | Public | wwwwwwwwwwwwwwww |
| [SearchVirusTotal]() | Static - Void | Public | wwwwwwwwwwwwwwww |
| [BlockIpAddress]() | Static - Void | Public | wwwwwwwwwwwwwwww |
| [BlockPort]() | Static - Void | Public | wwwwwwwwwwwwwwww |
| []() | Static - Void | Public | wwwwwwwwwwwwwwww |






<br>

## remove_connection

The object of this function is to

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




<br>

## SearchByIP

The object of this function is to

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





<br>

## SearchByPID

The object of this function is to

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






<br>

## SearchByProcessName

The object of this function is to

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






<br>

## Kill_Process

The object of this function is to

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






<br>

## Copy_IP

The object of this function is to

```c#
public static void Copy_IP()
        {
            Clipboard.SetText(myform.Networktable.SelectedRows[0].Cells[3].Value.ToString());
        }
```

Here's how the function works:






<br>

## SearchVirusTotal

The object of this function is to

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





<br>

## BlockIpAddress

The object of this function is to

```c#
public static void BlockIpAddress()
        {
            string ipAddress = myform.Networktable.SelectedRows[0].Cells[3].Value.ToString();
            string arguments = $"/C netsh advfirewall firewall add rule name=\"Block IP - {ipAddress}\" dir=in action=block remoteip={ipAddress}";
            Process.Start("cmd.exe", arguments);
        }
        
```

Here's how the function works:






<br>

## BlockPort

The object of this function is to

```c#
public static void BlockPort()
        {
            int port = int.Parse(myform.Networktable.SelectedRows[0].Cells[3].Value.ToString());
            string arguments = $"/C netsh advfirewall firewall add rule name=\"Block Port - {port}\" dir=in action=block protocol=TCP localport={port}";
            Process.Start("cmd.exe", arguments);
        }
```

Here's how the function works:





























