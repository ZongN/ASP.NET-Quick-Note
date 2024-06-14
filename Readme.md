# C# Quick Note

![](https://img.shields.io/badge/ASP.NET-C%23-brightgreen)

| Type        | Function       |
| :---------: | :------------- |
| [DataTable](#datatable)   | [新增資料(列)](#-datatable-add-new-row-新增資料列)、[新增資料(行)](#-datatable-add-new-column-新增資料行)、[欄位資料型態轉換](#-datatable-change-column-data-type-欄位-資料型態轉換-已存在資料免迴圈)、[排序](#-datatable-column-sorting-排序)、[篩選+排序](#-datatable-select--sorting-篩選--排序)、[日期篩選](#-datatable-select-datetime-日期篩選)、[唯一值](#-datatable-row-get-unique-唯一值)、[資料(列)轉List](#-datatable-row-itemarray-to-list-資料列-轉-list)、[資料(行)轉List](#-datatable-column-to-list-資料行-轉-list)、[移除重複資料行](#-datatable-remove-same-row-移除重複資料行)、[Sum加總/Average平均/運算式](#-datetable-欄位計算-sum加總average平均運算式)、[取前N筆資料](#-datatable-take-n-row-取前-n-筆資料)、[資料表合併-欄位衝突](#-datatable-merge-資料表合併-欄位衝突)、[資料表分組篩選轉 Dictionary](#-datatable-分組篩選轉-dictionary-datatable-groupby) |
| [DataRow[]](#datarow)   | [轉DataTable](#-datarow-to-datatable-datarow-轉-datatable)、[轉List](#-datarow-to-list-datarow-轉-list)、[篩選](#-datarow-where-篩選-二次篩選)、[排序](#-datarow-column-orderby--orderbydescending-排序)、[排序+取唯一值](#-datarow-column-orderby--get-unique-排序-同時-取唯一值)、[Sum加總/Average平均](#-datarow-欄位計算-sum加總average平均)|
|[Dictionary](#dictionary) |[取值](#-dictionary-取值-取值)、[每個元素進行處理](#-dictionary-每個元素進行處理-免迴圈)|
| [String](#string)     | [字串分割](#-string-split-多字元-字串處理字串分割)、[字串比對](#-string-contains-字串比對-字串比對)、[字串多條件比對](#-string-startswith-字串模糊比對--多條件模糊比對-字串比對-多條件比對)、[字串補位元](#-string-padleft-字串補位元-字串補位元)、[佔位符](#-string-format--佔位符-佔位符)、[插值字串](#-string--插值字串-插值字串)、[字串插入](#-string-insert-字串插入-字串插入)|
| [DateTime](#datetime)    | [日期轉週別](#-date-to-week-日期-轉-週別)、[字串轉日期](#-datetimeparseexact-字串轉日期-特定格式轉換)、[月天數](#-datetimedaysinmonth-月天數)|
| [List](#list)        | [唯一值](#-list-get-unique-唯一值)、[轉String字串](#-list-轉-string-字串-免迴圈-list-轉-string)、[Where+IndexOf查找字串](#-list-where--indexof-查找字串-list-where--indexof)|
|[Function](#Function)     | [判斷資料表是否存在資料](#-判斷資料表是否存在資料-check-if-datatable-is-empty)、[取得資料表單一欄位唯一值](#-取得資料表單一欄位唯一值-get-datatable-column-unique)、[資料表轉置矩陣](#-取資料表-轉置矩陣--datatable-轉置)|

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

// <方法三>

List<double> ls_Index = new List<double>() { 11.1, 12.2, 13.3 };

dt_Index.Rows.Add(ls_Index.ToArray());

```

> #### 🔥 Tips : 
> 用 `Datatable.Rows.Add` 新增 `DataRow` 遇到 _"例外狀況詳細資訊: System.ArgumentException: 這個資料列已經屬於其他資料表。"_ 的錯誤時，可改用 `Datatable.ImportRow(DataRow)` 方式新增

### 📌 DataTable Add New Column #新增資料(行)
```C#

DataTable dt_Index = new DataTable();

// <方法一> 資料表 不存在資料

dt_Index.Columns.Add("A",typeof(double));

dt_Index.Columns["A"].DefaultValue = 10.5;

DataRow dr_Index = dt_Index.NewRow()...

// <方法二> 資料表 已存在資料

DataColumn dc_Index = new DataColumn();

dc_Index.ColumnName = "B";

dc_Index.DefaultValue = "B_Default_Value";

dt_Index.Columns.Add(dc_Index);

```

### 📌 DataTable Change Column Data Type #欄位 資料型態轉換 (已存在資料)(免迴圈)
```C#

dt_Index.Columns.Add("Column_B", typeof(Int16), "CONVERT(Column_A,'System.Int16')");

DataView dv_index = new DataView(dt_Index);

dt_Index = dv_index.ToTable();

// 移除原欄位
dt_Re.Columns.Remove("Column_A");

```

> #### 🔥 Tips : 
> `Columns.Add` (新欄位) 後 無法直接 `Columns.Remove` (原欄位)。如果直接移除原欄位 (Column_A)，會報錯 : C# 無法移除這個資料行，因為它是運算式的一部分...
> 透過 `DataView` 轉換一次 可解決
> 原始欄位不能有非數值存在

### 📌 DataTable Column Sorting #排序
```C#

dt_Index.DefaultView.Sort = "Columns_A DESC";

dt_Index = dt_Index.DefaultView.ToTable();

```

### 📌 DataTable Select + Sorting #篩選 + 排序
```C#

DataRow[] dr_Index = dt_Index.Select("[TYPE] = 'A' ","[TYPE] DESC");

```
> 取得符合篩選條件 (按照排序順序，並符合指定狀態) 的所有 DataRow 物件之陣列。
> `Select(String, String, DataViewRowState)`

Refer to : [Microsoft Build](https://learn.microsoft.com/zh-tw/dotnet/api/system.data.datatable.select?view=net-7.0#system-data-datatable-select(system-string-system-string-system-data-dataviewrowstate))

### 📌 DataTable Select DateTime #日期篩選
```C#

// 篩選 2022/05/02 ~ 2022/05/05 間的 資料
// 關鍵是 # 字號 將日期包起來
DataRow[] dr_Index = dt.Select("[開始日期] >= #" + "2022/05/02" + "# AND [結束日期] <= #" + "2022/05/05" + "# ")

```

### 📌 DataTable Row Get Unique #唯一值
```C#

// <方法一> DataView
DataView dv_index = new DataView(dt_Index);

// <方法一 / 單一欄位>
dv_index.ToTable(true,"Columns_A");

// <方法一 / 多欄位>
dv_index.ToTable(true, new string[] { "Columns_A", "Columns_B", "Columns_C" });

// <方法二> Linq
List<string> ls_Index = dt_Index.AsEnumerable().Select(row => row.Field<string>("Columns_A")).Distinct().ToList();

// <取唯一值 + 排序>
List<string> ls_Index = dt_Index.AsEnumerable()
                                .Select(x => x.Field<string>("Columns_A"))
                                .Distinct()
                                .OrderBy(p => p)
                                .ToList();

// <取唯一值 + 排序(多條件排序)>
List<string> ls_Index = dt_Index.AsEnumerable()
                                .Select(x => x.Field<string>("Columns_A"))
                                .Distinct()
                                .OrderBy(p => p.Length) // 先按字串長度排序
                                .ThenBy(p => p) // 若長度相同，則按字母順序升冪排序
                                .ToList();

```

### 📌 DataTable Row ItemArray To List #資料列 轉 List
```C#

List<string> ls_Index = dt_Index.Rows[r].ItemArray.OfType<string>().ToList();

```

### 📌 DataTable Column To List #資料行 轉 List
```C#

List<string> ls_Index = dt_Index.Rows.OfType<DataRow>().Select(dr => dr.Field<string>("Column_A")).ToList();

// 同時 升冪 排序
List<string> ls_Index = dt_Index.Rows.OfType<DataRow>().Select(dr => dr.Field<string>("Column_A")).OrderBy(x => x).ToList();

// 同時 降冪 排序
List<string> ls_Index = dt_Index.Rows.OfType<DataRow>().Select(dr => dr.Field<string>("Column_A")).OrderByDescending(x => x).ToList();

```

### 📌 DataTable Remove Same Row #移除重複資料行
```C#

DataView dv_index = new DataView(dt_Index);

dt_Index = dv_index.ToTable(true);

```
> `.ToTable(Boolean)` / [Boolean distinct] 如果為 true，則返回 DataTable 包含具有與其所有列不同的值的行。默認值是 false。

Refer to : [Microsoft Build](https://learn.microsoft.com/zh-tw/dotnet/api/system.data.dataview.totable?view=net-7.0)

### 📌 DateTable 欄位計算 #Sum加總、Average平均、運算式
```C#

// <方法一>
// 欄位不需為數值
double db_QTY = dt_Index.AsEnumerable().Sum(x => Convert.ToDouble(x["QTY"].ToString()));

// <方法二>
// 欄位需為數值，才可使用 Compute 計算
dt_Index.Columns.Add("Columns_A",typeof(int)); 

double index_Sum = dt_Index.Compute("SUM(Columns_A)", string.Empty);

double index_Agv = dt_Index.Compute("AGV(Columns_A)", string.Empty);

// <方法三>
// 欄位運算式
dt_Index.Columns.Add("Columns_B", typeof(double));

dt_Index.Columns["Columns_B"].Expression = "CONVERT(Columns_A,'System.Int64') / 10";

```
> `DataColumn.Expression` 方法必須寫入空的欄位，無法直接複寫原欄位，否則會報錯 "無法設定Expression 屬性，因為在運算式中有循環參考..."

Refer to : [Microsoft Build](https://learn.microsoft.com/zh-tw/dotnet/api/system.data.datacolumn.expression?view=net-7.0)

### 📌 DataTable Take N Row #取前 N 筆資料
```C#

// 前 N 筆
int N = 10

dt_Index = dt_Index.Rows.Cast<DataRow>().Take(N).CopyToDataTable();

```

### 📌 DataTable Merge #資料表合併 欄位衝突
```C#

dt_A.merge(dt_B, true, MissingSchemaAction.Ignore);

```
Refer to : [Microsoft Build](https://learn.microsoft.com/zh-tw/dotnet/api/system.data.datatable.merge?view=net-8.0#system-data-datatable-merge)

### 📌 DataTable 分組篩選轉 Dictionary #DataTable GroupBy
```C#

Dictionary<string, List<string>> dic_Index = dt_Index
    .AsEnumerable()                             // 將 DataTable 轉換為可枚舉的集合。它將 DataTable 中的每一行轉換為 DataRow 物件，這樣就可以使用 LINQ 來查詢和操作這些資料了。
    .GroupBy(x => x.Field<string>("Column_A"))  // 將資料根據 "Column_A" 欄位的值進行分組。它將返回一個 IEnumerable<IGrouping<TKey, TSource>> 物件，其中每個分組都包含一個 Key 和相應的 DataRow 集合。
    .Select(group => new                        // 將每個分組進行選取操作，創建一個新的匿名類型物件(group)，其中包含 C_A（分組的鍵）和 C_B（相應分組中 Column_B 的列表）兩個屬性。
    {
        C_A = group.Key,
        C_B = group.Select(e => e.Field<string>("Column_B")).ToList()
    })
    .OrderBy(x => x.C_A)                        // 將結果集進行排序，根據 C_A（分組的鍵）的值進行升序排序。
    .ToDictionary(x => x.C_A, x => x.C_B);

```

## `<DataRow[]>`

### 📌 DataRow[] To DataTable #DataRow 轉 DataTable
```C#

DataRow[] dr_Index = dt_Index.Select("TYPE = 'A' ");

DataTable dt_Result = dr_Index.CopyToDataTable();

```

### 📌 DataRow[] To List #DataRow 轉 List
```C#

DataRow[] dr_Index = dt_Index.Select("TYPE = 'A' ");

List<string> ls_Index = dr_Index.OfType<DataRow>().Select(dr=>dr.Field<string>("ID")).ToList();

```

### 📌 DataRow[] Where #篩選 #二次篩選
```C#

DataRow[] dr_FindRow = dr_Index.Where(row => row["Column_A"].ToString() == "Apple").ToArray();

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

## `<Dictionary>`

### 📌 Dictionary 取值 #取值
```C#

Dictionary<string, string> dir_Index = new Dictionary<string, string>();

dir_Index["A"] = "AAA";

dir_Index.Values;

```

### 📌 Dictionary 每個元素進行處理 #免迴圈
```C#

Dictionary<string, string> dir_Index = new Dictionary<string, string>();

dir_Index["A"] = "AAA";
dir_Index["B"] = "BBB";
dir_Index["C"] = "CCC";

// 字尾處理
dir_Index = dir_Index.ToDictionary(kv => kv.Key, kv => kv.Value.ToString().Substring(0, kv.Value.ToString().Length - 1));

```

## `<String>`

### 📌 String Split 多字元 #字串處理、字串分割
```C#

string index_STR = "白日依山盡，黃河入海流";

index_STR.Split('，');

index_STR.Split(new string[] { "盡，黃" }, StringSplitOptions.None)[0];

// 移除空值
index_STR.Split(new string[] { "盡，黃" }, StringSplitOptions.RemoveEmptyEntries)[0];

```

### 📌 String Contains 字串比對 #字串比對
```C#

string index_STR = "白日依山盡，黃河入海流";

bool flag = index_STR.Contains('依山盡');

// 回傳布林值

```

### 📌 String StartsWith 字串模糊比對 / 多條件模糊比對 #字串比對 #多條件比對
```C#

string index_STR = "app";

string[] index_List = { "apple", "banner", "orange" };

bool isBelongToList = index_List.Any(d => index_STR.StartsWith(d));

// 回傳布林值

```

### 📌 String PadLeft 字串補位元 #字串補位元
```C#

string index_STR = "5";

index_STR.PadLeft(3, '0');

// Result : "003"

```

### 📌 String Format {} 佔位符 #佔位符
```C#

string name = "apple";

int price = 25;

string str_Result = string.Format("The price of {0} is {1} each.", name, price);

// Result : "The price of apple is 25 each."

// <指定格式>
double price = 25.5;

string str_Result = string.Format("The price of {0} is {1:C} each.", name, price);

// Result : "The price of apple is NT$25.50 each."

string str_Result = string.Format("The price of {0} is {1:0.00} each.", name, price);

// Result : "The price of apple is 25.50 each."

// <資料表>
string str_sql = "INSERT INTO A_TABLE ([A],[B],[C]) VALUES ('{0}','{1}','{2}')";

str_sql = string.Format(str_sql, dt_Row.Rows[0].ItemArray);

// Result : "INSERT INTO A_TABLE ([A],[B],[C]) VALUES ('XX','YY','ZZ')"

```

### 📌 String $ 插值字串 #插值字串
```C#
// 🔥 C# 6以上版本，支援 插值字串 $

var index = $"Welcome，{userName} ";

var date = new DateTime(2024, 4, 4);

var index = $"Today is {date:yyyy/MM/dd} ";

```
// Refer to : [Blogger](https://igouist.github.io/post/2020/08/csharp-string-interpolation/)

### 📌 String Insert 字串插入 #字串插入
```C#

string index_STR = "ABCEFG";

index_STR = index_STR.Insert(3,"D");

```
// Refer to : [Microsoft Build](https://learn.microsoft.com/zh-tw/dotnet/api/system.string.insert?view=net-8.0)

## `<DateTime>`

### 📌 Date To Week #日期 轉 週別
```C#

int index_Week = new CultureInfo("en-US").Calendar.GetWeekOfYear( DateTime.Now, new CultureInfo("en-US").DateTimeFormat.CalendarWeekRule, new CultureInfo("en-US").DateTimeFormat.FirstDayOfWeek )

```
Refer to : [Microsoft Build](https://docs.microsoft.com/zh-tw/dotnet/api/system.globalization.calendar.getweekofyear?view=net-6.0)

### 📌 DateTime.ParseExact #字串轉日期 #特定格式轉換
```C#

string str_index_Date = "2022-10-06";

// <方法一>
DateTime de_index_Date1 = DateTime.Parse(str_index_Date);

// <方法二>
DateTime de_index_Date2 = DateTime.ParseExact(str_index_Date, "yyyy-MM-dd", null);

// <特定格式轉換>
DateTime de_index_Date3 = DateTime.ParseExact("20240315145000", "yyyyMMddHHmmss", null);

```

### 📌 DateTime.DaysInMonth #月天數
```C#

int Day_in_Month = DateTime.DaysInMonth(DateTime.Now.Year, DateTime.Now.Month);

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

### 📌 List 轉 String 字串 (免迴圈) #List 轉 String
```C#

List<string> ls_Index = new List<string>() { "A", "B", "C" };

string str_Index = String.Join("+", ls_Index);

// Result : "A+B+C"

```

### 📌 List Where + IndexOf 查找字串 #List Where + IndexOf
```C#

List<string> ls_Index = new List<string>() { "A=1", "B=2", "C=3" };

string str_Re = ls_Index.Where(x => x.IndexOf("B") > -1).ToList()[0];

// Result : "B=2"

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

## `<Function>`

### 📌 判斷資料表是否存在資料 #Check If DataTable Is Empty
```C#

static bool Checkif_Data_Exist_In_DataTable(DataTable dt_Index)
{
    bool Check_Flag = false;

    if (dt_Index.Rows.Count > 0)
    {
        if (dt_Index.Rows[0][0].ToString() != "" && !String.IsNullOrEmpty(dt_Index.Rows[0][0].ToString()))
        {
            Check_Flag = true;
        }
    }
    return Check_Flag;
}

```

### 📌 取得資料表單一欄位唯一值 #Get DataTable Column Unique
```C#

static List<string> Get_DataTable_Column_Unique(DataTable dt_In, string Column_Name)
{
    DataView dv_index = new DataView(dt_In);

    // 單一欄位 取 唯一值
    dt_In = dv_index.ToTable(true, Column_Name);

    // 轉 LIST
    List<string> ls_Index = dt_In.Rows.OfType<DataRow>().Select(dr => dr.Field<string>(Column_Name)).ToList();

    return ls_Index;
}

```

### 📌 取資料表 轉置矩陣 # DataTable 轉置
```C#

static DataTable Transpose_DataTable(DataTable dt_input)
{
    DataTable dt = dt_input;
    DataTable NewDataTale = new DataTable();
    
    //原本DataTable列數
    int dtRowsCount = dt.Rows.Count;
    //原本DataTable欄數
    int dtColumnCount = dt.Columns.Count;
    //將原本DataTable的第一個欄位放入轉置後的第一欄
    NewDataTale.Columns.Add(dt.Columns[0].ToString(), typeof(string));
    //將原本DataTable的第一列轉置為轉置後的欄位
    for (int i = 0; i < dtRowsCount; i++)
    {
        NewDataTale.Columns.Add(dt.Rows[i][0].ToString(), typeof(string));
    }
    
    //將原本DataTable的欄位列依序轉置為轉置後的每一列
    //起始為1，因為原本第一列已經放置為欄位名稱，要從第二列開始跑起
    for (int s = 1; s < dtColumnCount; s++)
    {
        DataRow dr = NewDataTale.NewRow();
        dr[0] = dt.Columns[s].ToString();
        for (int i = 0; i < dtRowsCount; i++)
        {
            dr[i + 1] = dt.Rows[i][s].ToString();
        }
        NewDataTale.Rows.Add(dr);
    }
    
    return NewDataTale;
}

```
