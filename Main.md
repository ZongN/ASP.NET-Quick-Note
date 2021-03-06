# ASP.NET C# Quick Note

![](https://img.shields.io/badge/ASP.NET-C%23-brightgreen)

### đ DataTable Add New Row #æ°åĸčŗæ(å)
```C#

DataTable dt_Index = new DataTable();
dt_Index.Columns.Add("A",typeof(double));
dt_Index.Columns.Add("B",typeof(double));
dt_Index.Columns.Add("C",typeof(double));

// <æšæŗä¸>

DataRow dr_Index = dt_Index.NewRow();
dr_Index["A"] = 10;
dr_Index["B"] = 11.5;
dr_Index["C"] = 0.9;

dt_Index.Rows.Add(dr_Index);

// <æšæŗäē>

double index_A = "0.5";
double index_B = "0.51";
double index_C = "0.43";

dt_Index.Rows.Add(index_A,index_B,index_C);

```

### đ DataTable Column Sorting #æåē
```C#

dt_Index.DefaultView.Sort = "Columns_A DESC";

dt_Index = dt_Index.DefaultView.ToTable();

```

### đ DataTable Row Get Unique #å¯ä¸åŧ
```C#

DataView dv_index = new DataView(dt_Index);

dt_Index = dv_index.ToTable(true,"Columns_A");

```

### đ List Get Unique #å¯ä¸åŧ
```C#

using System.Linq;

IEnumerable<string> distinct_Index = ls_Index.Distinct(); // Get unique

ls_Index = new List<string>();

foreach (var i in distinct_Index)
{
  ls_Index.Add(i);
}

return ls_Index;

```

### đ ?: operator #éįŽå­
```C#

string index_str = "MODE_UPDATE_001";

index_str.IndexOf("UPDATE") > -1 ? "UPDATE" : "INSERT";

return "UPDATE"

```
(is this condition true ? yes : no)

Refer to : [Microsoft Build](https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/operators/conditional-operator)

### đ Date To Week #æĨæ čŊ éąåĨ
```C#

int index_Week = new CultureInfo("en-US").Calendar.GetWeekOfYear( DateTime.Now, new CultureInfo("en-US").DateTimeFormat.CalendarWeekRule, new CultureInfo("en-US").DateTimeFormat.FirstDayOfWeek )

```
Refer to : [Microsoft Build](https://docs.microsoft.com/zh-tw/dotnet/api/system.globalization.calendar.getweekofyear?view=net-6.0)

### đ DataTable Select DateTime #æĨæį¯Šé¸
```C#
// į¯Šé¸ 2022/05/02 ~ 2022/05/05 éį čŗæ
// ééĩæ¯ # å­č å°æĨæåčĩˇäž
DataRow[] dr_Index = dt.Select("[éå§æĨæ] >= #" + "2022/05/02" + "# AND [įĩææĨæ] <= #" + "2022/05/05" + "# ")

```

### đ DataRow[] æŦäŊč¨įŽ #Sumå į¸ŊãAverageåšŗå
```C#

double index_Sum = dr_Index.Sum(x => double.Parse(x["Columns_A"].ToString()));

double index_Avg = dr_Index.Average(x => double.Parse(x["Columns_A"].ToString()));

```
