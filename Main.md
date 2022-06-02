# ASP.NET C# Quick Note

![](https://img.shields.io/badge/ASP.NET-C%23-brightgreen)

### 📌 DataTable Add New Row #新增資料(列)
```C#

DataTable dt_Index = new DataTable();
dt_Index.Columns.Add("A",typeof(double));
dt_Index.Columns.Add("B",typeof(double));
dt_Index.Columns.Add("C",typeof(double));

// <方法一>

DataRow dr_Index = dt_Index.NewRow();
dr_Index["A"] = 10;
dr_Index["B"] = 11.5;
dr_Index["C"] = 0.9;

dt_Index.Rows.Add(dr_Index);

// <方法二>

double index_A = "0.5";
double index_B = "0.51";
double index_C = "0.43";

dt_Index.Rows.Add(index_A,index_B,index_C);

```

### 📌 DataTable Column Sorting #排序
```C#

dt_Index.DefaultView.Sort = "Columns_A DESC";

dt_Index = dt_Index.DefaultView.ToTable();

```

### 📌 DataTable Row Get Unique #唯一值
```C#

DataView dv_index = new DataView(dt_Index);

dt_Index = dv_index.ToTable(true,"Columns_A");

```

### 📌 List Get Unique #唯一值
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

### 📌 ?: operator #運算子
```C#

string index_str = "MODE_UPDATE_001";

index_str.IndexOf("UPDATE") > -1 ? "UPDATE" : "INSERT";

return "UPDATE"

```
(is this condition true ? yes : no)

Refer to : [Microsoft Build](https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/operators/conditional-operator)

### 📌 Date To Week #日期 轉 週別
```C#

int index_Week = new CultureInfo("en-US").Calendar.GetWeekOfYear( DateTime.Now, new CultureInfo("en-US").DateTimeFormat.CalendarWeekRule, new CultureInfo("en-US").DateTimeFormat.FirstDayOfWeek )

```
Refer to : [Microsoft Build](https://docs.microsoft.com/zh-tw/dotnet/api/system.globalization.calendar.getweekofyear?view=net-6.0)

### 📌 DataTable Select DateTime #日期篩選
```C#
// 篩選 2022/05/02 ~ 2022/05/05 間的 資料
// 關鍵是 # 字號 將日期包起來
DataRow[] dr_Index = dt.Select("[開始日期] >= #" + "2022/05/02" + "# AND [結束日期] <= #" + "2022/05/05" + "# ")

```
