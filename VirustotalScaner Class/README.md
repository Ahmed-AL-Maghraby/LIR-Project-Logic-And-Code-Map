



| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| VirustotalScaner |      Plublic     | myform from Form1 |    none     |        5           |


## Help Classes

| Name | Access Modifiers | Number Of Classes |
| ---------------- | ----------- | ------------------ |
| [Api GetData Classes](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#api-getdata-classes) |      Plublic    |        4           |

## Global Varuable

| Name | Access Modifiers | Type | Description |
| -- | -- | -- | -- |
| scanresult | Private |static-string | wwwww |

## Methods


| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [RunScan](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#runscan) | Static - String | Public | Run Virustotal Scan And Show Message Box when finish  |
| [removeHash](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#removehash) | Static - String | Public | wwwwwwwwwwwwwwww |
| [GetIpScanResult](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#getipscanresult) | Static - String | Public | wwwwwwwwwwwwwwww |
| [GetReultScan](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#getreultscan) | Static - String | Public | wwwwwwwwwwwwwwww |
| [Scanner](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/blob/main/VirustotalScaner%20Class/README.md#scanner) | Static - String | Public | wwwwwwwwwwwwwwww |



<br>

## RunScan

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
                        if (row.Cells[8].Value.ToString().Contains("Detections") && !(row.Cells[8].Value.ToString().Contains("Detections by : 0")))
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

```c#
public static string GetIpScanResult(string ip)
        {
            Scanner(ip, myform.vir_api.Text);
            return scanresult;
        }
```








<br>

## GetReultScan

```c#

public static string GetReultScan(string pro_hash, string apik)
        {
           
            
            string result = "";
            if (pro_hash.Length > 10)
            {
                
                if(!hashs.Contains(pro_hash))
                {
                        
                    Scanner(pro_hash, apik);
                    result = scanresult;
                    hashs += pro_hash + result + " ";
                }
                else
                {
                    result = hashs.Substring(hashs.IndexOf(pro_hash) + 32 ,18);
                }
                

            }
            return result;
        }


```








<br>

## Scanner

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
                        scanresult = ($"Detections by : {attributes.last_analysis_stats.malicious}");

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

