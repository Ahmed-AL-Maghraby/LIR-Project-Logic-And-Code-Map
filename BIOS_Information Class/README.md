


| Name | Access Modifiers | Objects | Inherit From | Number Of Function |
| ---- | ----------- | ------- | ----------- | ------------------ |
| BIOS_Information | Public | none | none | 2 |

## Methods

| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| Get_Bios_Date | Static - String | Public |  Retrieve the BIOS release date of the current system |
| Get_Bios_Version | Static - String | Public |  Retrieve the BIOS version of the current system using the Windows Registry. |




It creates a ManagementObjectSearcher object named searcher that queries the "Win32_BIOS" class to retrieve BIOS information.
It calls the Get() method on the searcher object to execute the query and obtain a collection of ManagementObject objects representing the BIOS instances found on the system.
It iterates over each ManagementObject in the biosCollection.
Inside the loop, it retrieves the "ReleaseDate" property value from the current biosObject. This value is a string representation of the BIOS release date.
It uses the ManagementDateTimeConverter.ToDateTime method to convert the string representation of the release date to a DateTime object named biosDate.
It returns the biosDate formatted as a string in the "yyyy-MM-dd" format.
If there are no BIOS instances found or an error occurs during the retrieval process, it returns an empty string.




It uses the Registry.LocalMachine property to get a reference to the local machine's registry hive.
It calls the OpenSubKey method on the Registry.LocalMachine object to open the key path "HARDWARE\DESCRIPTION\System\BIOS".
It wraps the code block inside a using statement to ensure that the RegistryKey object is properly disposed of after use.
It checks if the baseKey is not null, indicating that the key was successfully opened.
Inside the if statement, it calls the GetValue method on the baseKey object to retrieve the value associated with the key name "BIOSVersion".
It checks if the value is not null, indicating that the key and value were found.
Inside the nested if statement, it converts the value to a string using the ToString method and returns it.
If the key or value was not found, or an error occurred during the retrieval process, it returns an empty string.
