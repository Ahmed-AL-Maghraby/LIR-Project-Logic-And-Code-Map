



| Name | Access Modifiers | Objects | Inhert From | Number Of Function |
| ---- | ---------------- | ------- | ----------- | ------------------ |
| VirustotalScaner |      Plublic     | myform from Form1 |    none     |        0           |


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
| []() | Static - String | Public | wwwwwwwwwwwwwwww |
| []() | Static - String | Public | wwwwwwwwwwwwwwww |
| []() | Static - String | Public | wwwwwwwwwwwwwwww |
| []() | Static - String | Public | wwwwwwwwwwwwwwww |

	











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

