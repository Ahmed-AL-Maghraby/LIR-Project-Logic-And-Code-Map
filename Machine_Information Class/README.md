



| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| Machine_Information |      Plublic     | none |    none     |        6           |






## Methods


| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [Get_Processor_Identification]() | Static - String | Public | Retrieve information about the processor, including its name and clock speed |
| [Get_Primary_Adapter_Mac]() | Static - String | Public |  Retrieve the MAC (Media Access Control) address of the primary network adapter |
| [Get_System_Uptime]() | Static - String | Public | Retrieve the system uptime, which represents the duration for which the system has been running since the last boot |
| [Get_Installed_RAM]() | Static - String | Public | retrieve the installed RAM (Random Access Memory) of the computer |
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

The object of this function is to retrieve and return the MAC address of the primary network adapter that is currently active and not a loopback interface


```c#
public static string Get_Primary_Adapter_Mac()
        {
            NetworkInterface[] networkInterfaces = NetworkInterface.GetAllNetworkInterfaces();

            foreach (NetworkInterface interfaceItem in networkInterfaces)
            {
                if (interfaceItem.OperationalStatus == OperationalStatus.Up &&
                    interfaceItem.NetworkInterfaceType != NetworkInterfaceType.Loopback)
                {
                    PhysicalAddress macAddress = interfaceItem.GetPhysicalAddress();
                    byte[] bytes = macAddress.GetAddressBytes();
                    string mac = BitConverter.ToString(bytes).Replace("-", ":");
                    return mac;
                }
            }
            return string.Empty; 
        }
```


Here's how the function works:

1. It uses the `NetworkInterface.GetAllNetworkInterfaces()` method to retrieve an array of all available network interfaces on the machine.
2. It iterates over each `NetworkInterface` object in the `networkInterfaces` array using a `foreach` loop.
3. Inside the loop, it checks if the interface's `OperationalStatus` is set to "Up" (indicating the interface is active) and if the `NetworkInterfaceType` is not set to "Loopback" (indicating it's not a loopback interface).
4. If the above conditions are met, it retrieves the physical MAC address of the interface using the `GetPhysicalAddress()` method, which returns a `PhysicalAddress` object.
5. It converts the MAC address to a byte array using the `GetAddressBytes()` method of the `PhysicalAddress` object.
6. It converts the byte array to a string representation of the MAC address using the `BitConverter.ToString()` method, replacing the "-" separator with ":" using the `Replace()` method.
7. It returns the MAC address string.
8. If no active network interface is found or if the MAC address cannot be retrieved, it returns an empty string (`string.Empty`).

 
<br>

## Get_System_Uptime

The object of this function is to retrieve and return the system uptime as a `TimeSpan` value representing the duration since the last system boot.

```c#
public static string Get_System_Uptime()
        {
            TimeSpan uptime = TimeSpan.Zero;
            using (var uptimeCounter = new PerformanceCounter("System", "System Up Time"))
            {
                uptimeCounter.NextValue(); // Call NextValue once to initialize the counter value
                uptime = TimeSpan.FromSeconds(uptimeCounter.NextValue());
            }
            return uptime.ToString();
        }

```


Here's how the function works:

1. It initializes a `TimeSpan` variable named `uptime` to zero, representing a duration of zero.
2. It creates a new instance of the `PerformanceCounter` class, specifying the category name "System" and the counter name "System Up Time". This counter measures the system uptime.
3. It calls the `NextValue()` method on the `uptimeCounter` object once to initialize the counter value. This is necessary because the first call to `NextValue()` returns zero.
4. It calls the `NextValue()` method again to retrieve the actual system uptime value, which is in seconds.
5. It assigns the uptime value converted to a `TimeSpan` object to the `uptime` variable.
6. It returns the string representation of the `uptime` value by calling the `ToString()` method on the `TimeSpan` object.


<br>

## Get_Installed_RAM

The object of this function is to retrieve and return the installed RAM of the computer, rounded up to the nearest whole number in gigabytes (GB)

```c#
 public static string Get_Installed_RAM()
        {
            ManagementObjectSearcher searcher = new ManagementObjectSearcher("SELECT TotalPhysicalMemory FROM Win32_ComputerSystem");
            ManagementObjectCollection collection = searcher.Get();

            foreach (ManagementObject obj in collection)
            {
                ulong totalPhysicalMemoryBytes = (ulong)obj["TotalPhysicalMemory"];
                float totalPhysicalMemoryGB = (float)(totalPhysicalMemoryBytes / (1024.0 * 1024.0 * 1024.0)); // Convert bytes to GB
                return Math.Ceiling(totalPhysicalMemoryGB).ToString();
            }

            return string.Empty; // Return 0 if the installed RAM information is not available
        }
```


Here's how the function works:

1. It creates a new instance of the `ManagementObjectSearcher` class, specifying the query "SELECT TotalPhysicalMemory FROM Win32_ComputerSystem". This query retrieves the total physical memory of the computer system.
2. It calls the `Get()` method on the `searcher` object to retrieve a collection of `ManagementObject` instances that match the query.
3. It iterates over each `ManagementObject` in the `collection` using a `foreach` loop.
4. Inside the loop, it retrieves the `TotalPhysicalMemory` property of the `ManagementObject` as a `ulong` (unsigned long) value, representing the total physical memory in bytes.
5. It divides the `totalPhysicalMemoryBytes` value by the appropriate factor to convert it from bytes to gigabytes (GB). In this case, it divides by 1024.0 three times (1024.0 * 1024.0 * 1024.0).
6. It converts the result to a `float` to represent the total physical memory in GB with decimal precision.
7. It uses the `Math.Ceiling` method to round up the `totalPhysicalMemoryGB` value to the nearest whole number and converts it to a string.
8. It returns the rounded-up total physical memory value as a string.
9. If no `ManagementObject` is found in the collection or if the installed RAM information is not available, it returns an empty string (`string.Empty`).

 

<br>

## Get_Disk_Information









<br> 

## Get_Device_ID











<br>








