# ASP.NET C# Quick Note

![](https://img.shields.io/badge/ASP.NET-C%23-brightgreen)

| TYPE        | Function       |
| :---------: | :------------- |
| DataTable   | #新增資料(列) #排序 #篩選+排序 #日期篩選 #唯一值 #Sum加總/Average平均 |
| DataRow[]   | #DataRow轉DataTable #排序 #排序+取唯一值 #Sum加總/Average平均       |
| String      | #字串分割                                                         |
| DateTime    | #日期轉週別 #字串轉日期                                            |
| List        | #唯一值                                                           |

## `<DataTable>`

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
### 📌 DataTable Select + Sorting #篩選 + 排序
```C#

DataRow[] dr_Index = dt_Index.Select("[TYPE] = 'A' ","[TYPE] DESC");

```
>取得符合篩選條件 (按照排序順序，並符合指定狀態) 的所有 DataRow 物件之陣列。

>Select(String, String, DataViewRowState)

Refer to : [Microsoft Build](https://learn.microsoft.com/zh-tw/dotnet/api/system.data.datatable.select?view=net-7.0#system-data-datatable-select(system-string-system-string-system-data-dataviewrowstate))

### 📌 DataTable Select DateTime #日期篩選
```C#
// 篩選 2022/05/02 ~ 2022/05/05 間的 資料
// 關鍵是 # 字號 將日期包起來
DataRow[] dr_Index = dt.Select("[開始日期] >= #" + "2022/05/02" + "# AND [結束日期] <= #" + "2022/05/05" + "# ")

```

### 📌 DataTable Row Get Unique #唯一值
```C#

DataView dv_index = new DataView(dt_Index);

dt_Index = dv_index.ToTable(true,"Columns_A");

```

### 📌 DateTable 欄位計算 #Sum加總、Average平均
```C#
// 欄位需為數值
// 才可使用 Compute 計算

dt_Index.Columns.Add("Columns_A",typeof(int)); 

double index_Sum = dt_Index.Compute("SUM(Columns_A)", string.Empty);

double index_Agv = dt_Index.Compute("AGV(Columns_A)", string.Empty);

```
Refer to : [痞客幫](https://einboch.pixnet.net/blog/post/279208343)

## `<DataRow[]>`

### 📌 DataRow[] To DataTable #DataRow 轉 DataTable
```C#

DataRow[] dr_Index = dt_Index.Select("TYPE = 'A' ");

DataTable dt_Result = dr_Index.CopyToDataTable();

```

### 📌 DataRow[] Column OrderBy / OrderByDescending #排序
```C#

var dr_OrderBy_Check_Time = dr_index.OrderBy(x=> DateTime.Parse(x["Check_Time"].ToString()));

foreach(DataRow row in dr_OrderBy_Check_Time)
{
    row["Check_Time"].ToString();
}

```

### 📌 DataRow[] Column OrderBy + Get Unique #排序 同時 取唯一值
```C#

// 先排序 → 取某欄位("Name") → 取唯一值

var index_Dis = dr_Index.OrderBy(x => x["Name"].ToString()).Select(x => x["Name"].ToString()).Distinct();

foreach(var value in index_Dis)
{
    value;
}

```
Refer to : [MSDN](https://social.msdn.microsoft.com/Forums/vstudio/en-US/ba3c5126-bd6c-4ee2-a1be-7ca1ae2df342/how-to-select-distinct-data-from-a-datarow-in-c?forum=netfxbcl)

### 📌 DataRow[] 欄位計算 #Sum加總、Average平均
```C#

double index_Sum = dr_Index.Sum(x => double.Parse(x["Columns_A"].ToString()));

double index_Avg = dr_Index.Average(x => double.Parse(x["Columns_A"].ToString()));

```
## `<String>`

### 📌 String Split 多字元 #字串處理、字串分割
```C#

string index_STR = "白日依山盡，黃河入海流";

index_STR.Split(new string[] { "盡，黃" }, StringSplitOptions.None)[0];

```

## `<DateTime>`

### 📌 Date To Week #日期 轉 週別
```C#

int index_Week = new CultureInfo("en-US").Calendar.GetWeekOfYear( DateTime.Now, new CultureInfo("en-US").DateTimeFormat.CalendarWeekRule, new CultureInfo("en-US").DateTimeFormat.FirstDayOfWeek )

```
Refer to : [Microsoft Build](https://docs.microsoft.com/zh-tw/dotnet/api/system.globalization.calendar.getweekofyear?view=net-6.0)

### 📌 DateTime.ParseExact #字串轉日期
```C#

string str_index_Date = "2022-10-06";

DateTime de_index_Date = DateTime.ParseExact(str_index_Date, "yyyy-MM-dd", null);

```

## `<List>`

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

## `<Other>`

### 📌 ?: operator #運算子
```C#

string index_str = "MODE_UPDATE_001";

index_str.IndexOf("UPDATE") > -1 ? "UPDATE" : "INSERT";

return "UPDATE"

```
(is this condition true ? yes : no)

Refer to : [Microsoft Build](https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/operators/conditional-operator)
