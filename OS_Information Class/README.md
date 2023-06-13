

| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| OS_Information |      Plublic     | none |    none     |        6           |

## Methods

| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [Get_Operating_System_And_Version]() | Static - String | Public |  Retrieve the operating system name and version information. |
| [Get_Operating_System_Bitness]() | Static - String | Public |  Determine the bitness (32-bit or 64-bit) of the operating system. |
| [Get_Product_Name]() | Static - String | Public | wwwwwwwwwwwwwwww |
| [Get_OS_Buil_dNumber]() | Static - String | Public | wwwwwwwwwwwwwwww |
| [Get_Product_ID]() | Static - String | Public | wwwwwwwwwwwwwwww |
| [Get_OS_Install_Date]() | Static - String | Public | wwwwwwwwwwwwwwww |


<br>

## Get_Operating_System_And_Version

The object of this function is to retrieve and return the operating system name and version information, including the product name and build number from the Windows Registry if available, and falling back to using the Environment.OSVersion and Environment.Version properties if necessary.

```c#
public static string Get_Operating_System_And_Version()
        {
            const string keyPath = @"SOFTWARE\Microsoft\Windows NT\CurrentVersion";
            const string valueName = "ProductName";
            const string buildNumberValueName = "CurrentBuildNumber";

            using (RegistryKey key = Registry.LocalMachine.OpenSubKey(keyPath))
            {
                if (key != null)
                {
                    string productName = key.GetValue(valueName)?.ToString();
                    string buildNumber = key.GetValue(buildNumberValueName)?.ToString();

                    if (!string.IsNullOrEmpty(productName) && !string.IsNullOrEmpty(buildNumber))
                    {
                        return $"{productName} {buildNumber}";
                    }
                }
            }

            //IF Unknown Windows Server Version will run this code

            OperatingSystem os = Environment.OSVersion;

            string operatingSystem = string.Empty;

            if (os.Platform == PlatformID.Win32NT)
            {
                // Windows NT family
                if (os.Version.Major == 10)
                    operatingSystem = "Windows 10";
                else if (os.Version.Major == 6 && os.Version.Minor == 3)
                    operatingSystem = "Windows 8.1";
                else if (os.Version.Major == 6 && os.Version.Minor == 2)
                    operatingSystem = "Windows 8";
                else if (os.Version.Major == 6 && os.Version.Minor == 1)
                    operatingSystem = "Windows 7";
                else if (os.Version.Major == 6 && os.Version.Minor == 0)
                    operatingSystem = "Windows Vista";
                else if (os.Version.Major == 5 && os.Version.Minor == 2)
                    operatingSystem = "Windows Server 2003";
                else if (os.Version.Major == 5 && os.Version.Minor == 1)
                    operatingSystem = "Windows XP";
                else if (os.Version.Major == 5 && os.Version.Minor == 0)
                    operatingSystem = "Windows 2000";
                else
                    operatingSystem = "Unknown Windows";
            }
            else if (os.Platform == PlatformID.Unix)
            {
                // Unix-based
                operatingSystem = "Unix-based";
            }
            else if (os.Platform == PlatformID.MacOSX)
            {
                // macOS
                operatingSystem = "macOS";
            }
            else
            {
                operatingSystem = "Unknown";
            }

            Version frameworkVersion = Environment.Version;
            string version = frameworkVersion.ToString();

            return $"{operatingSystem} (Framework Version: {version})";
        }
```    


Here's how the function works:

1. It defines three constant strings: `keyPath`, `valueName`, and `buildNumberValueName`, which represent the registry key path and value names for retrieving the operating system information.
2. It uses the `Registry.LocalMachine` property to get a reference to the local machine's registry hive.
3. It calls the `OpenSubKey` method on the `Registry.LocalMachine` object with the `keyPath` to open the corresponding registry key.
4. It wraps the code block inside a `using` statement to ensure that the `RegistryKey` object is properly disposed of after use.
5. It checks if the `key` is not null, indicating that the key was successfully opened.
6. Inside the `if` statement, it retrieves the values associated with `valueName` and `buildNumberValueName` from the `key` using the `GetValue` method, and converts them to strings.
7. It checks if both `productName` and `buildNumber` are not null or empty.
8. If both values are available, it combines them using string interpolation to create a formatted string containing the product name and build number, and returns it.
9. If the registry key or values were not found, it proceeds to the next block of code.
10. It uses the `Environment.OSVersion` property to obtain information about the operating system.
11. It initializes a string variable `operatingSystem` as an empty string.
12. It checks the `PlatformID` property of the `os` object to determine the platform of the operating system.
13. If the platform is `Win32NT`, it checks the `Version` property of the `os` object to determine the major and minor version numbers.
14. Based on the version numbers, it assigns the appropriate operating system name to the `operatingSystem` variable.
15. If the platform is `Unix`, it assigns the string "Unix-based" to the `operatingSystem` variable.
16. If the platform is `MacOSX`, it assigns the string "macOS" to the `operatingSystem` variable.
17. If none of the above conditions match, it assigns the string "Unknown" to the `operatingSystem` variable.
18. It retrieves the framework version using the `Environment.Version` property and assigns it to the `frameworkVersion` variable.
19. It converts the `frameworkVersion` to a string and assigns it to the `version` variable.
20. It combines the `operatingSystem` and `version` strings using string interpolation to create a formatted string that includes the operating system name and framework version.
21. Finally, it returns the formatted string.


<br/>

## Get_Operating_System_Bitness

The object of this function is to determine and return the bitness of the operating system as a string.

```c#

public static string Get_Operating_System_Bitness()
        {
            return Environment.Is64BitOperatingSystem ? "64-bit" : "32-bit";
        }

```

Here's how the function works:

1. It uses the `Environment.Is64BitOperatingSystem` property, which returns `true` if the operating system is 64-bit and `false` if it is 32-bit.
2. It uses a ternary operator (`? :`) to return the string "64-bit" if `Environment.Is64BitOperatingSystem` is `true`, and "32-bit" if it is `false`.


## Get_Product_Name



## Get_OS_Buil_dNumber






























### Get_Product_ID




### Get_OS_Install_Date


