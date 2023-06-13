



| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| User_Information |      Plublic     | none |    none     |        2           |






## Methods


| Name | Type | Access Modifiers | Description |
| ---- | ---- | ---------------- | ----------- |
| [Get_Registered_Owner](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/User_Information%20Class#get_registered_owner) | Static - String | Public |  Retrieve the registered owner of the operating system |
| [Get_Registered_Organization](https://github.com/Ahmed-AL-Maghraby/Project-Logic-And-Code-Map/tree/main/User_Information%20Class#get_registered_organization) | Static - String | Public |  Retrieve the registered organization of the operating system |


	


<br>

## Get_Registered_Owner

The object of this function is to retrieve and return the registered owner of the operating system, or "Unknown Registered Owner" if the information is not available

```c#
public static string Get_Registered_Owner()
        {
            const string keyPath = @"SOFTWARE\Microsoft\Windows NT\CurrentVersion";
            const string valueName = "RegisteredOwner";

            using (RegistryKey key = Registry.LocalMachine.OpenSubKey(keyPath))
            {
                if (key != null)
                {
                    string registeredOwner = key.GetValue(valueName)?.ToString();
                    if (!string.IsNullOrEmpty(registeredOwner))
                    {
                        return registeredOwner;
                    }
                }
            }

            return "Unknown Registered Owner";
        }
```

Here's how the function works:

1. It initializes a constant string variable `keyPath` with the registry path "SOFTWARE\Microsoft\Windows NT\CurrentVersion".
2. It initializes a constant string variable `valueName` with the name "RegisteredOwner".
3. It uses the `using` statement to open the registry key specified by `keyPath` under the `LocalMachine` hive.
4. If the key is successfully opened (not null), it retrieves the value of the registry entry specified by `valueName` using the `GetValue()` method of the `key` object.
5. The retrieved value is then converted to a string and assigned to the `registeredOwner` variable.
6. If the `registeredOwner` value is not null or empty, it is returned as the registered owner of the operating system.
7. If the `registeredOwner` value is null or empty, it means that the registered owner information is not available, and the function returns the string "Unknown Registered Owner".


<br>

## Get_Registered_Organization

The object of this function is to retrieve and return the registered organization of the operating system, or "Unknown Registered Organization" if the information is not available

```c#
 public static string Get_Registered_Organization()
        {
            const string keyPath = @"SOFTWARE\Microsoft\Windows NT\CurrentVersion";
            const string valueName = "RegisteredOrganization";

            using (RegistryKey key = Registry.LocalMachine.OpenSubKey(keyPath))
            {
                if (key != null)
                {
                    string registeredOrganization = key.GetValue(valueName)?.ToString();
                    if (!string.IsNullOrEmpty(registeredOrganization))
                    {
                        return registeredOrganization;
                    }
                }
            }

            return "Unknown Registered Organization";
        }
```


Here's how the function works:

1. It initializes a constant string variable `keyPath` with the registry path "SOFTWARE\Microsoft\Windows NT\CurrentVersion".
2. It initializes a constant string variable `valueName` with the name "RegisteredOrganization".
3. It uses the `using` statement to open the registry key specified by `keyPath` under the `LocalMachine` hive.
4. If the key is successfully opened (not null), it retrieves the value of the registry entry specified by `valueName` using the `GetValue()` method of the `key` object.
5. The retrieved value is then converted to a string and assigned to the `registeredOrganization` variable.
6. If the `registeredOrganization` value is not null or empty, it is returned as the registered organization of the operating system.
7. If the `registeredOrganization` value is null or empty, it means that the registered organization information is not available, and the function returns the string "Unknown Registered Organization".


<br>



