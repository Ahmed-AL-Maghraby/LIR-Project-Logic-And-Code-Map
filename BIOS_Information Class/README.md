


| Name | Access Modifiers | Objects | Inherit From | Number Of Function |
| ---- | ----------- | ------- | ----------- | ------------------ |
| BIOS_Information | Public | none | none | 2 |

## Methods

| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [Get_Bios_Date](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/BIOS_Information%20Class#get_bios_date) | Static - String | Public |  Retrieve the BIOS release date of the current system |
| [Get_Bios_Version](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/BIOS_Information%20Class#get_bios_version) | Static - String | Public |  Retrieve the BIOS version of the current system using the Windows Registry. |

<br>

## Get_Bios_Date

The object of this function is to retrieve and return the BIOS release date of the current system as a formatted string

```c#
public static string Get_Bios_Date()
        {

            ManagementObjectSearcher searcher = new ManagementObjectSearcher("SELECT * FROM Win32_BIOS");
            ManagementObjectCollection biosCollection = searcher.Get();

            foreach (ManagementObject biosObject in biosCollection)
            {
                DateTime biosDate = ManagementDateTimeConverter.ToDateTime(biosObject["ReleaseDate"].ToString());
                return biosDate.ToString("yyyy-MM-dd");
            }


            return string.Empty;
        }
```

Here's a breakdown of how the function works:

1. It creates a `ManagementObjectSearcher` object named `searcher` that queries the "Win32_BIOS" class to retrieve BIOS information.
2. It calls the `Get()` method on the `searcher` object to execute the query and obtain a collection of `ManagementObject` objects representing the BIOS instances found on the system.
3. It iterates over each `ManagementObject` in the `biosCollection`.
4. Inside the loop, it retrieves the "ReleaseDate" property value from the current `biosObject`. This value is a string representation of the BIOS release date.
5. It uses the `ManagementDateTimeConverter.ToDateTime` method to convert the string representation of the release date to a `DateTime` object named `biosDate`.
6. It returns the `biosDate` formatted as a string in the "yyyy-MM-dd" format.
7. If there are no BIOS instances found or an error occurs during the retrieval process, it returns an empty string.

<br>

## Get_Bios_Version

The object of this function is to retrieve and return the BIOS version of the current system using the Windows Registry

```c#

 public static string Get_Bios_Version()
        {
            using (RegistryKey baseKey = Registry.LocalMachine.OpenSubKey(@"HARDWARE\DESCRIPTION\System\BIOS"))
            {
                if (baseKey != null)
                {
                    object value = baseKey.GetValue("BIOSVersion");
                    if (value != null)
                    {
                        return value.ToString();
                    }
                }
            }

            return string.Empty;
        }

```

Here's how the function works:

1. It uses the `Registry.LocalMachine` property to get a reference to the local machine's registry hive.
2. It calls the `OpenSubKey` method on the `Registry.LocalMachine` object to open the key path `"HARDWARE\DESCRIPTION\System\BIOS"`.
3. It wraps the code block inside a `using` statement to ensure that the `RegistryKey` object is properly disposed of after use.
4. It checks if the `baseKey` is not null, indicating that the key was successfully opened.
5. Inside the `if` statement, it calls the `GetValue` method on the `baseKey` object to retrieve the value associated with the key name "BIOSVersion".
6. It checks if the `value` is not null, indicating that the key and value were found.
7. Inside the nested `if` statement, it converts the `value` to a string using the `ToString` method and returns it.
8. If the key or value was not found, or an error occurred during the retrieval process, it returns an empty string.



<br>

