

| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| ---- |      Plublic     | 2 |    none     |        11           |

## Objects
```C#
VirustotalScaner VirustotalScaner = new VirustotalScaner();
```
```C#
public static Form1 myform = Application.OpenForms.OfType<Form1>().FirstOrDefault();
```




## Methods


| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [GetProcessesInfo]() | Void | Public | Retrieve information about running processes |
| [Process_StartTime]() | String | Public | Take a process ID as input and retrieves the start time of the corresponding process |
| [Process_image_path]() | Static - String | Public | Take a process name as input and retrieves the executable path of the corresponding process |
| [Number_Instances]() | Int | Public | Takes a process name as input and returns the number of instances of processes with that name |
| [GetParentProcessId]() | Int | Private | Take a process ID as input and retrieves the parent process ID using WMI |
| [Parent_process]() | String | Public | Take a process ID as input and retrieves the parent process ID |
| [GetProcessUserAccount]() | String | Private | Retrieve the user account associated with a given process |
| [GetProcessOwner]() | Static - String | Private | Retrieves the owner of a given process using WMI |
| [P_user_acount]() | String | Public | Take a process name as input and returns the user account associated with that process |
| [Process_Hash_MD5]() | Static - String | Public | Take a file path as input and calculates the MD5 hash of the file |
| [VirusTotalScanner]() | Static - String | Public | This method is a placeholder for VirusTotal scanning functionality |




<br>

## GetProcessesInfo

The object of this function is to Retrieve information about running processes.

```c#
public  void GetProcessesInfo()
        {
            Process[] processes = Process.GetProcesses();
            foreach (Process process in processes)
            {
                try
                {
                    myform.processTable1.Rows.Add(process.ProcessName.ToLower(), process.Id, Parent_process(process.Id), Process_StartTime(process.Id), "Number_Instances(process.ProcessName)", Process_image_path(process.ProcessName), P_user_acount(process.ProcessName), Process_Hash_MD5(Process_image_path(process.ProcessName))," ");
                    
                }
                catch (Exception ex)
                {

                }
            }
  
        }
```

Here's how the function works:
   - It uses the `Process.GetProcesses()` method to get an array of all running processes.
   - For each process, it adds relevant information to the `myform.processTable1` DataGridView control on the main form.
   - The added information includes process name, ID, parent process ID, start time, number of instances, executable path, user account, and an empty placeholder for the VirusTotal scan result.

<br>

## Process_StartTime

The object of this function is to Take a process ID as input and retrieves the start time of the corresponding process

```c#
        public string Process_StartTime(int pro_id)
        {
            string p_time = "";

            try
            {
                Process process = Process.GetProcessById(pro_id);
                DateTime S_Time = process.StartTime;
                p_time = S_Time.ToString();
            }
            catch (Exception e) { }

            return p_time;
        }
```

Here's how the function works:
   - It converts the process ID to a `Process` object and gets the start time from the `StartTime` property.
   - The start time is returned as a formatted string.


<br>

## Process_image_path

The object of this function is to Take a process name as input and retrieves the executable path of the corresponding process.

```c#
public static string Process_image_path(string p_name)
        {

            Process[] processesq = Process.GetProcessesByName(p_name);
            string executablePath = "";
            foreach (Process processa in processesq)
            {
                try
                {
                    executablePath = processa.MainModule.FileName;

                }
                catch (Exception ex) { }
            }
            return executablePath;
        }
```

Here's how the function works:
   - It uses `Process.GetProcessesByName()` to get an array of processes with the given name.
   - For each process, it attempts to get the executable path from the `MainModule.FileName` property.
   - The executable path of the last process in the array is returned.



<br>

## Number_Instances

The object of this function is to Takes a process name as input and returns the number of instances of processes with that name.

```c#
public int Number_Instances(string pr_name)
        {
            Process[] processes = Process.GetProcessesByName(pr_name);
            try
            {
                return processes.Length;
            }
            catch (Exception ex)
            {
                return processes.Length;
            }
        }
```

Here's how the function works:
 - It uses `Process.GetProcessesByName()` to get an array of processes with the given name and returns the array length.



<br>

## GetParentProcessId

The object of this function is to Take a process ID as input and retrieves the parent process ID using WMI

```c#
        private int GetParentProcessId(int processId)
        {
            string query = $"SELECT ParentProcessId FROM Win32_Process WHERE ProcessId = {processId}";
            using (ManagementObjectSearcher searcher = new ManagementObjectSearcher(query))
            {
                using (ManagementObjectCollection processList = searcher.Get())
                {
                    foreach (ManagementObject obj in processList)
                    {
                        return Convert.ToInt32(obj["ParentProcessId"]);
                    }
                }
            }

            throw new Exception("Parent process not found.");
        }
```

Here's how the function works:
   - It executes a WMI query to retrieve the parent process ID from the `Win32_Process` class.
   - The parent process ID is returned as an integer.



<br>

## Parent_process

The object of this function is to Take a process ID as input and retrieves the parent process ID.

```c#
public string Parent_process(int processId)
        {
            string parent = "";
            int parentProcessId = GetParentProcessId(processId);

            try
            {
                parent = parentProcessId.ToString();
            }
            catch (Exception e) { }
            return parent;
        }
```

Here's how the function works:
  - It calls the `GetParentProcessId()` method to get the parent process ID.
  - The parent process ID is returned as a string.


<br>

## GetProcessUserAccount

The object of this function is to Retrieve the user account associated with a given process.

```c#
        private string GetProcessUserAccount(string processName)
        {
            try
            {
                Process process = Process.GetProcessesByName(processName)[0];
                string processOwner = GetProcessOwner(process);
                return processOwner;
            }
            catch (IndexOutOfRangeException)
            {
                throw new Exception("Process not found.");
            }
            catch (Exception ex)
            {
                throw new Exception("Error occurred while retrieving process user account.", ex);
            }
        }
```

Here's how the function works:
   - They use WMI queries to retrieve process information and the associated user account.
   - `GetProcessUserAccount()` calls `GetProcessOwner()` to extract the user account from the query result.



<br>

## GetProcessOwner

The object of this function is to provided retrieves the owner of a given process using WMI (Windows Management Instrumentation) queries.

```c#
        private static string GetProcessOwner(Process process)
        {
            string query = "SELECT * FROM Win32_Process WHERE ProcessId = " + process.Id;
            ManagementObjectSearcher searcher = new ManagementObjectSearcher(query);
            ManagementObjectCollection processList = searcher.Get();

            foreach (ManagementObject obj in processList)
            {
                string[] argList = new string[] { string.Empty, string.Empty };
                int returnVal = Convert.ToInt32(obj.InvokeMethod("GetOwner", argList));

                if (returnVal == 0)
                {
                    // argList[0] contains the domain, argList[1] contains the username
                    return $"{argList[0]}\\{argList[1]}";
                }
            }

            return "Unknown";
        }
```

Here's how the function works:

- The method takes a `Process` object as input, representing the process for which you want to retrieve the owner.

- It constructs a WMI query using the process ID to find the corresponding process in the `Win32_Process` class.

- It uses a `ManagementObjectSearcher` to execute the query and retrieve a collection of `ManagementObject` instances that match the query conditions.

- The method then iterates through the collection of `ManagementObject` instances.

- For each `ManagementObject`, it prepares an argument list (an array of strings) with two empty strings.

- It invokes the method `GetOwner` on the `ManagementObject` instance, passing the argument list.

- The return value of the `GetOwner` method is an integer. If the return value is 0, it means the method call was successful, and the owner information is available.

- If the return value is 0, the method extracts the domain and username from the argument list and combines them to create the owner's full name in the format "domain\username".

- If the return value is not 0, the method returns "Unknown" to indicate that the owner information could not be retrieved.

- Finally, the method returns the owner information or "Unknown" depending on the result of the WMI query.

   



<br>

## P_user_acount

The object of this function is to Take a process name as input and returns the user account associated with that process.
```c#
public string P_user_acount(string processName)
        {
            string processUserAccount = "";

            try
            {
                 processUserAccount = GetProcessUserAccount(processName);
                
            }
            catch (Exception ex)
            {

            }
            return (processUserAccount);
        }
```

Here's how the function works:
   - It calls the `GetProcessUserAccount()` method to get the user account.
   - The user account is returned as a string.



<br>

## Process_Hash_MD5

The object of this function is to Take a file path as input and calculates the MD5 hash of the file.

```c#
public static string Process_Hash_MD5(string file_path)
        {
            if(file_path == string.Empty)
            {
                return "";
            }
            string output;

            using (var md5 = MD5.Create())
            {
                using (var stream = File.OpenRead(file_path))
                {
                    byte[] checksum = md5.ComputeHash(stream);
                    output = BitConverter.ToString(checksum).Replace("-", String.Empty).ToLower();
                    return (output);

                }
            }
        }
```

Here's how the function works: 

   - It uses the `MD5` class to compute the hash of the file contents.
   - The hash value is returned as a lowercase string.



<br>

## VirusTotalScanner

This method is a placeholder for VirusTotal scanning functionality.

```c#
        public static string VirusTotalScanner(string fileHash)
        {
                return "";
        }
```

Here's how the function works:
   - It currently returns an empty string.







<p>


Overall, the `RuningProcessInfo` class provides methods to gather and display information about running processes, including process names, IDs, start times, executable paths, parent processes, user accounts, and MD5 hashes of process image files. Additionally, it includes a placeholder for VirusTotal scanning, which could be further developed to perform actual scanning operations.

</p>
