

| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| VirustotalScaner |      Plublic     | myform from Form1 |    none     |        5           |


## Help Classes

| Name | Access Modifiers | Number Of Classes |
| ---------------- | ----------- | ------------------ |
| [Api GetData Classes](https://github.com/Ahmed-AL-Maghraby/LIR-Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#api-getdata-classes) |      Plublic    |        4           |

## Global Varuable

| Name | Access Modifiers | Type | Description |
| -- | -- | -- | -- |
| scanresult | Private |static-string | Default value for scanresult = 0 |

## Methods


| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [RunScan](https://github.com/Ahmed-AL-Maghraby/LIR-Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#runscan) | Static - String | Public | Run Virustotal Scan And Show Message Box when finish  |
| [removeHash](https://github.com/Ahmed-AL-Maghraby/LIR-Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#removehash) | Static - String | Public | Remove Hash file |
| [GetIpScanResult](https://github.com/Ahmed-AL-Maghraby/LIR-Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#getipscanresult) | Static - String | Public | Get the scan result for a given IP address |
| [GetReultScan](https://github.com/Ahmed-AL-Maghraby/LIR-Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#getreultscan) | Static - String | Public | Get the scan result for a given file hash |
| [Scanner](https://github.com/Ahmed-AL-Maghraby/LIR-Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#scanner) | Static - String | Public | This method performs the actual API call to the VirusTotal service to scan a file based on its hash value |



<br>

## RunScan
This method is used to perform a full scan of running processes.
```c#


 public static void RunScan()
        {
            RuningProcessInfo RuningProcessInfo = new RuningProcessInfo();

            ProcessAction.remove_Process();
            Process[] processes = Process.GetProcesses();
            foreach (Process process in processes)
            {
                try
                {
                    myform.processTable1.Rows.Add(process.ProcessName.ToLower(), process.Id, RuningProcessInfo.Parent_process(process.Id), RuningProcessInfo.Process_StartTime(process.Id), RuningProcessInfo.Number_Instances(process.ProcessName), RuningProcessInfo.Process_image_path(process.ProcessName), RuningProcessInfo.P_user_acount(process.ProcessName), RuningProcessInfo.Process_Hash_MD5(RuningProcessInfo.Process_image_path(process.ProcessName)), GetReultScan(RuningProcessInfo.Process_Hash_MD5(RuningProcessInfo.Process_image_path(process.ProcessName)), myform.getapikey()).ToString());
                    foreach (DataGridViewRow row in myform.processTable1.Rows)
                    {


                        if (int.Parse(row.Cells[8].Value.ToString()) > 0)
                        {
                            row.DefaultCellStyle.BackColor = Color.Red;
                            row.DefaultCellStyle.ForeColor = Color.White;
                        }

                    }
                }
                catch (Exception e)
                {

                }
            }
            MessageBox.Show("Sacn Done Successfully");
        }
```

Here's how the function works:
   - It calls the `RuningProcessInfo` class to get information about running processes.
   - For each running process, it gathers relevant information (such as process name, ID, start time, etc.), and it also calculates the MD5 hash of the process image file using the `Process_Hash_MD5()` method.
   - The method then calls the `GetReultScan()` method to get the scan result for the MD5 hash.
   - It adds the collected information and the scan result to the `myform.processTable1` DataGridView control on the main form.
   - It also highlights processes with a positive scan result by changing the background color to red and the text color to white.
   - After processing all running processes, a message box displays "Scan Done Successfully."



<br>

## removeHash

```c#

public static void removeHash()
        {
            hashs = "";
        }

```





<br>

## GetIpScanResult
This method is used to get the scan result for a given IP address (not used in the provided code).
```c#
public static string GetIpScanResult(string ip)
        {
            Scanner(ip, myform.vir_api.Text);
            return scanresult;
        }
```

Here's how the function works:
   - It calls the `Scanner()` method with the IP address and the VirusTotal API key (`myform.vir_api.Text`).
   - The scan result is stored in the `scanresult` variable, and it is returned as a string.







<br>

## GetReultScan
This method is used to get the scan result for a given file hash.
```c#
public static int GetReultScan(string pro_hash, string apik)
        {
           
            
            int result = 0;
            if (pro_hash.Length > 10)
            {
                
                if(!hashs.Contains(pro_hash))
                {
                        
                    Scanner(pro_hash, apik);
                    result = int.Parse(scanresult);
                    hashs += pro_hash + result + " ";
                }
                else
                {
                    result = int.Parse(hashs.Substring(hashs.IndexOf(pro_hash) + 32, 2));
                }
                

            }
            return result;
        }

```

Here's how the function works:
   - It takes the file hash (MD5 hash in this case) and the VirusTotal API key as parameters.
   - The method checks if the file hash is not empty and then checks if it is not already present in the `hashs` variable.
   - If the hash is not present, it calls the `Scanner()` method with the hash and API key to get the scan result.
   - It then adds the hash and scan result to the `hashs` variable to avoid redundant scanning in the future.
   - The scan result is parsed into an integer and returned.








<br>

## Scanner
This method performs the actual API call to the VirusTotal service to scan a file based on its hash value
```c#
 public static void Scanner(string pro_hash, string apik)
        {
            string apiKey = apik;
            string hashValue = pro_hash;
            string url = $"https://www.virustotal.com/api/v3/files/{hashValue}";

            using (HttpClient client = new HttpClient())
            {
                client.DefaultRequestHeaders.Add("x-apikey", apiKey);

                HttpResponseMessage response = client.GetAsync(url).GetAwaiter().GetResult();
                if (response.IsSuccessStatusCode)
                {
                    string responseContent = response.Content.ReadAsStringAsync().GetAwaiter().GetResult();
                    var data = JsonConvert.DeserializeObject<ApiResponse>(responseContent);
                    if (data.data != null)
                    {
                        var attributes = data.data.attributes;
                        scanresult = attributes.last_analysis_stats.malicious.ToString();

                    }
                    else
                    {
                        scanresult = ("No information available for the hash.");
                    }
                }
                else
                {
                   scanresult = ("Some Error in api");
                }
            }
        }
```


Here's how the function works:
   - It uses `HttpClient` to send an HTTP GET request to the VirusTotal API endpoint with the given file hash.
   - The API key is added to the request headers for authentication.
   - If the response is successful (status code 200), it parses the response content and retrieves the scan result.
   - The scan result is stored in the `scanresult` variable.





<br>

## Api GetData Classes

```c#
public class ApiResponse
    {
        public Data data { get; set; }
    }

    public class Data
    {
        public Attributes attributes { get; set; }
    }

    public class Attributes
    {
        public LastAnalysisStats last_analysis_stats { get; set; }
    }

    public class LastAnalysisStats
    {
        public int malicious { get; set; }
    }
```
The code provided defines a set of nested classes that represent the structure of the JSON response returned by the VirusTotal API.

1. `ApiResponse` class:
   - This class has a property named `data` of type `Data`.
   - The `data` property represents the main data object in the API response.

2. `Data` class:
   - This class has a property named `attributes` of type `Attributes`.
   - The `attributes` property represents the attributes object in the API response, which contains detailed information about the file or hash being scanned.

3. `Attributes` class:
   - This class has a property named `last_analysis_stats` of type `LastAnalysisStats`.
   - The `last_analysis_stats` property represents the statistics related to the last analysis performed on the file or hash.

4. `LastAnalysisStats` class:
   - This class has a property named `malicious` of type `int`.
   - The `malicious` property represents the number of antivirus engines that have flagged the file or hash as malicious during the last analysis.

These classes provide a convenient way to deserialize the JSON response from the VirusTotal API into strongly-typed objects, allowing easy access to the relevant data within the response.

