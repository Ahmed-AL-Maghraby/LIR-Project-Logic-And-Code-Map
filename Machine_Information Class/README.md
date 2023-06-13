



| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| Machine_Information |      Plublic     | none |    none     |        6           |






## Methods


| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [Get_Processor_Identification]() | Static - String | Public | retrieve information about the processor, including its name and clock speed. |
| [Get_Primary_Adapter_Mac]() | Static - String | Public | wwwwwwwwwwwwwwww |
| [Get_System_Uptime]() | Static - String | Public | wwwwwwwwwwwwwwww |
| [Get_Installed_RAM]() | Static - String | Public | wwwwwwwwwwwwwwww |
| [Get_Disk_Information]() | Static - String | Public | wwwwwwwwwwwwwwww |
| [Get_Device_ID]() | Static - String | Public | wwwwwwwwwwwwwwww |
	

<br>

## Get_Processor_Identification

```c#
public static string Get_Processor_Identification()
        {

            using (ManagementObjectSearcher searcher = new ManagementObjectSearcher("SELECT Name, MaxClockSpeed FROM Win32_Processor"))
            {
                foreach (ManagementObject obj in searcher.Get())
                {
                    string processorName = obj["Name"] as string;
                    uint maxClockSpeed = (uint)obj["MaxClockSpeed"];

                    string processorInfo = string.Format("{0} @ {1} MHz ({2} GHz)", processorName, maxClockSpeed, maxClockSpeed / 1000);
                    return processorInfo;
                }
            }

            return string.Empty;
        }

```


The object of this function is to retrieve and return information about the processor, including its name and clock speed, by querying the WMI

Here's how the function works:

1. It uses the `ManagementObjectSearcher` class to query the Windows Management Instrumentation (WMI) and retrieve information about the processor.
2. It creates a new instance of `ManagementObjectSearcher` with the WMI query "SELECT Name, MaxClockSpeed FROM Win32_Processor".
3. It uses a `foreach` loop to iterate over the `ManagementObject` collection returned by the `Get()` method of the `ManagementObjectSearcher`.
4. Inside the loop, it retrieves the `Name` property of the processor object as a string and assigns it to the `processorName` variable.
5. It retrieves the `MaxClockSpeed` property of the processor object as a `uint` (unsigned integer) and assigns it to the `maxClockSpeed` variable.
6. It formats a string (`processorInfo`) that includes the processor name, maximum clock speed in MHz, and calculated clock speed in GHz (by dividing the `maxClockSpeed` by 1000).
7. It returns the `processorInfo` string.
8. If no processor information is found (e.g., if the `ManagementObjectSearcher` returns an empty collection), it returns an empty string (`string.Empty`).

<br>

## Get_Primary_Adapter_Mac





<br>

## Get_System_Uptime






<br>

## Get_Installed_RAM






<br>

## Get_Disk_Information









<br> 

## Get_Device_ID











<br>








