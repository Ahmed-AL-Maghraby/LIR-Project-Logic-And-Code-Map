

| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| OS_Information |      Plublic     | none |    none     |        6           |

## Methods

| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [Get_Operating_System_And_Version]() | Static - String | Public |  Retrieve the operating system name and version information |
| [Get_Operating_System_Bitness]() | Static - String | Public |  Determine the bitness (32-bit or 64-bit) of the operating system |
| [Get_Product_Name]() | Static - String | Public | Retrieve the product name of the operating system or software |
| [Get_OS_Buil_dNumber]() | Static - String | Public | Retrieve the build number of the operating system |
| [Get_Product_ID]() | Static - String | Public | Retrieve the product ID of the operating system |
| [Get_OS_Install_Date]() | Static - String | Public | Retrieve the installation date of the operating system |


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

<br>

## Get_Product_Name

The object of this function is to retrieve and return the product name of the operating system or software by accessing the Windows Registry. If the product name cannot be retrieved, it returns a default value of "Unknown Product"
 
```c#

public static string Get_Product_Name()
        {
            const string keyPath = @"SOFTWARE\Microsoft\Windows NT\CurrentVersion";
            const string valueName = "ProductName";

            using (RegistryKey key = Registry.LocalMachine.OpenSubKey(keyPath))
            {
                if (key != null)
                {
                    string productName = key.GetValue(valueName)?.ToString();
                    if (!string.IsNullOrEmpty(productName))
                    {
                        return productName;
                    }
                }
            }

            return "Unknown Product";
        }
```

Here's how the function works:

1. It defines two constant strings: `keyPath` and `valueName`. `keyPath` represents the registry key path where the product name is stored, and `valueName` represents the value name of the product name.
2. It uses the `Registry.LocalMachine` property to get a reference to the local machine's registry hive.
3. It calls the `OpenSubKey` method on the `Registry.LocalMachine` object with the `keyPath` to open the corresponding registry key.
4. It wraps the code block inside a `using` statement to ensure that the `RegistryKey` object is properly disposed of after use.
5. It checks if the `key` is not null, indicating that the key was successfully opened.
6. Inside the `if` statement, it retrieves the value associated with `valueName` from the `key` using the `GetValue` method and converts it to a string.
7. It checks if the `productName` is not null or empty.
8. If the `productName` is available, it returns the `productName`.
9. If the registry key or value was not found or if the `productName` is null or empty, it returns the string "Unknown Product".

<br>

## Get_OS_Buil_dNumber

The object of this function is to retrieve and return the build number of the operating system by accessing the Windows Registry. If the build number cannot be retrieved, it returns a default value of "Unknown Build Number"
 
```c#

public static string Get_OS_Buil_dNumber()
        {
            const string keyPath = @"SOFTWARE\Microsoft\Windows NT\CurrentVersion";
            const string valueName = "CurrentBuildNumber";

            using (RegistryKey key = Registry.LocalMachine.OpenSubKey(keyPath))
            {
                if (key != null)
                {
                    string buildNumber = key.GetValue(valueName)?.ToString();
                    if (!string.IsNullOrEmpty(buildNumber))
                    {
                        return buildNumber;
                    }
                }
            }

            return "Unknown Build Number";
        }

```


Here's how the function works:

1. It defines two constant strings: `keyPath` and `valueName`. `keyPath` represents the registry key path where the build number is stored, and `valueName` represents the value name of the build number.
2. It uses the `Registry.LocalMachine` property to get a reference to the local machine's registry hive.
3. It calls the `OpenSubKey` method on the `Registry.LocalMachine` object with the `keyPath` to open the corresponding registry key.
4. It wraps the code block inside a `using` statement to ensure that the `RegistryKey` object is properly disposed of after use.
5. It checks if the `key` is not null, indicating that the key was successfully opened.
6. Inside the `if` statement, it retrieves the value associated with `valueName` from the `key` using the `GetValue` method and converts it to a string.
7. It checks if the `buildNumber` is not null or empty.
8. If the `buildNumber` is available, it returns the `buildNumber`.
9. If the registry key or value was not found or if the `buildNumber` is null or empty, it returns the string "Unknown Build Number".


<br>

### Get_Product_ID

The object of this function is to retrieve and return the product ID of the operating system by accessing the Windows Registry. If the product ID cannot be retrieved, it returns a default value of "Unknown Product ID"

```c#

public static string Get_Product_ID()
        {
            const string keyPath = @"SOFTWARE\Microsoft\Windows NT\CurrentVersion";
            const string valueName = "ProductId";

            using (RegistryKey key = Registry.LocalMachine.OpenSubKey(keyPath))
            {
                if (key != null)
                {
                    string productID = key.GetValue(valueName)?.ToString();
                    if (!string.IsNullOrEmpty(productID))
                    {
                        return productID;
                    }
                }
            }

            return "Unknown Product ID";
        }

```

Here's how the function works:

1. It defines two constant strings: `keyPath` and `valueName`. `keyPath` represents the registry key path where the product ID is stored, and `valueName` represents the value name of the product ID.
2. It uses the `Registry.LocalMachine` property to get a reference to the local machine's registry hive.
3. It calls the `OpenSubKey` method on the `Registry.LocalMachine` object with the `keyPath` to open the corresponding registry key.
4. It wraps the code block inside a `using` statement to ensure that the `RegistryKey` object is properly disposed of after use.
5. It checks if the `key` is not null, indicating that the key was successfully opened.
6. Inside the `if` statement, it retrieves the value associated with `valueName` from the `key` using the `GetValue` method and converts it to a string.
7. It checks if the `productID` is not null or empty.
8. If the `productID` is available, it returns the `productID`.
9. If the registry key or value was not found or if the `productID` is null or empty, it returns the string "Unknown Product ID".


<br>

### Get_OS_Install_Date

The object of this function is to retrieve and return the installation date of the operating system by accessing the Windows Registry. If the installation date cannot be retrieved, it returns a default value of the minimum `DateTime` value formatted as "yyyy-MM-dd"

```c#

public static string Get_OS_Install_Date()
        {
            const string keyPath = @"SOFTWARE\Microsoft\Windows NT\CurrentVersion";
            const string valueName = "InstallDate";

            using (RegistryKey key = Registry.LocalMachine.OpenSubKey(keyPath))
            {
                if (key != null)
                {
                    string installDateValue = key.GetValue(valueName)?.ToString();
                    if (!string.IsNullOrEmpty(installDateValue) && long.TryParse(installDateValue, out long installDateTicks))
                    {
                        return DateTime.FromFileTimeUtc(installDateTicks).ToString("yyyy-MM-dd");
                    }
                }
            }

            return DateTime.MinValue.ToString("yyyy-MM-dd");
        }
        

```


Here's how the function works:

1. It defines two constant strings: `keyPath` and `valueName`. `keyPath` represents the registry key path where the installation date is stored, and `valueName` represents the value name of the installation date.
2. It uses the `Registry.LocalMachine` property to get a reference to the local machine's registry hive.
3. It calls the `OpenSubKey` method on the `Registry.LocalMachine` object with the `keyPath` to open the corresponding registry key.
4. It wraps the code block inside a `using` statement to ensure that the `RegistryKey` object is properly disposed of after use.
5. It checks if the `key` is not null, indicating that the key was successfully opened.
6. Inside the `if` statement, it retrieves the value associated with `valueName` from the `key` using the `GetValue` method and converts it to a string.
7. It checks if the `installDateValue` is not null or empty, and if it can be parsed as a `long` value using `long.TryParse` method.
8. If the `installDateValue` is available and successfully parsed, it converts the parsed `installDateTicks` to a `DateTime` object using `DateTime.FromFileTimeUtc` method, and formats it to a string in the format "yyyy-MM-dd".
9. If the registry key or value was not found, or if the `installDateValue` is null or empty, or if the `installDateValue` could not be parsed as a `long`, it returns the minimum `DateTime` value (DateTime.MinValue) formatted as "yyyy-MM-dd".



<br>





