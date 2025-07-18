# C# Quick Note

![](https://img.shields.io/badge/ASP.NET-C%23-brightgreen)

| Type                         | Function                    |
| :--------------------------: | :-------------------------- |
| [DataTable](#datatable)      | [新增資料(列)](#-datatable-add-new-row-新增資料列)、[新增資料(行)](#-datatable-add-new-column-新增資料行)、[欄位資料型態轉換](#-datatable-change-column-data-type-欄位-資料型態轉換-已存在資料免迴圈)、[排序](#-datatable-column-sorting-排序)、[篩選+排序](#-datatable-select--sorting-篩選--排序)、[唯一值](#-datatable-row-get-unique-唯一值)、[篩選+唯一值](#-datatable-where--select-篩選--唯一值)、[日期篩選](#-datatable-select-datetime-日期篩選)、[資料(列)轉List](#-datatable-row-itemarray-to-list-資料列-轉-list)、[資料(行)轉List](#-datatable-column-to-list-資料行-轉-list)、[移除重複資料行](#-datatable-remove-same-row-移除重複資料行)、[Sum加總/Average平均/運算式](#-datetable-欄位計算-sum加總average平均運算式)、[取前N筆資料](#-datatable-take-n-row-取前-n-筆資料)、[資料表合併-欄位衝突](#-datatable-merge-資料表合併-欄位衝突)、[資料表分組篩選 轉 Dictionary](#-datatable-分組篩選-轉-dictionary-datatable-groupby)、[排名](#-datatable-欄位排名-rank-排名-rank)、[欄位順序調整](#-datatable-欄位順序調整-column-setordinal) |
| [DataRow[]](#datarow)        | [轉DataTable](#-datarow-to-datatable-datarow-轉-datatable)、[轉List](#-datarow-to-list-datarow-轉-list)、[篩選](#-datarow-where-篩選-二次篩選)、[排序](#-datarow-column-orderby--orderbydescending-排序)、[排序+取唯一值](#-datarow-column-orderby--get-unique-排序-同時-取唯一值)、[Sum加總/Average平均](#-datarow-欄位計算-sum加總average平均)、[從 DataTable 中刪除 Select](#-delete-from-datatable-select-delete-from-datatable)、[操作所有資料 免迴圈](#-操作所有資料-免迴圈-edit-in-datarow-without-for-loop)|
| [Dictionary](#dictionary)    | [建立](#-dictionary-建立-新建)、[取值](#-dictionary-取值-取值)、[每個元素進行處理](#-dictionary-每個元素進行處理-免迴圈)、[排序](#-dictionary-排序-orderby-排序-orderby)|
| [String](#string)            | [字串分割](#-string-split-多字元-字串處理字串分割)、[字串比對](#-string-contains-字串比對-字串比對)、[字串多條件比對](#-string-startswith-字串模糊比對--多條件模糊比對-字串比對-多條件比對)、[字串補位元](#-string-padleft-字串補位元-字串補位元)、[佔位符](#-string-format--佔位符-佔位符)、[插值字串](#-string--插值字串-插值字串)、[字串插入](#-string-insert-字串插入-字串插入)、[字串重複](#-string-concat-字串重複-repeat效果-字串重複)|
| [Linq](#linq)                | [排序](#-特殊排序-特殊排序) |
| [DateTime](#datetime)        | [日期轉週別](#-date-to-weekly-日期-轉-週別)、[日期轉星期](#-date-to-week-日期-轉-星期)、[字串轉日期](#-datetimeparseexact-字串轉日期-特定格式轉換)、[月天數](#-datetimedaysinmonth-月天數)|
| [List](#list)                | [唯一值](#-list-get-unique-唯一值)、[轉String字串](#-list-轉-string-字串-免迴圈-list-轉-string)、[Where+IndexOf查找字串](#-list-where--indexof-查找字串-list-where--indexof)、[內容查詢](#-list-內容查詢-list-contains)、[建立數字陣列](#-list-建立數字陣列-enumerablerange)、[新增值於第N個位置](#-新增值於第n個位置-list-insert)、[List 計算](#-list-計算-sunaveragetaketakelastspip)、[List 內容移除 (兩個 List 比對)](#-list-內容移除-兩個-list-比對-list-remove)|
| [Function](#function)        | [判斷資料表是否存在資料](#-判斷資料表是否存在資料-check-if-datatable-is-empty)、[取得資料表單一欄位唯一值](#-取得資料表單一欄位唯一值-get-datatable-column-unique)、[資料表轉置矩陣](#-取資料表-轉置矩陣--datatable-轉置)、[時間區間重疊計算](#-時間區間重疊計算-時間重疊)、[Json 轉 DataTable](#-json-轉-datatable-json-to-datatable)|
| [Element](#element)          | [Button Click 動態連結事件](#-button-click-動態連結事件-button-dynamic-click)、[Input Type=number & runat:server 剖析器錯誤](#-input-typenumber--runatserver-剖析器錯誤-input-type-number-and-runat-server-error)|
| [Other](#other-1)              | [值類型與引用類型](#-值類型引用類型-value-typereference-type)、[二進位轉十進位]()、[十進位轉二進位]() |

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

### 📌 DataTable Where + Select #篩選 + 唯一值
```C#

List<string> ls_Index = dt_Index.AsEnumerable()
                                .Where(row => row.Field<string>("欄位A") == "AA" && row.Field<string>("欄位B") == "BB") // 篩選兩個欄位
                                .Select(row => row.Field<string>("欄位C")) // 選取 "欄位C"
                                .Distinct() // 取得唯一值
                                .ToList(); // 將結果轉換為 List

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

### 📌 DataTable Select DateTime #日期篩選
```C#

// 篩選 2022/05/02 ~ 2022/05/05 間的 資料
// 關鍵是 # 字號 將日期包起來
DataRow[] dr_Index = dt.Select("[開始日期] >= #" + "2022/05/02" + "# AND [結束日期] <= #" + "2022/05/05" + "# ")

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

### 📌 DataTable 分組篩選 轉 Dictionary #DataTable GroupBy
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
    .ToDictionary(x => x.C_A, x => x.C_B);      // 將 LINQ 查詢的結果轉換為 Dictionary。其中第一個參數 x => x.C_A 指定了鍵的選取條件，第二個參數 x => x.C_B 指定了值的選取條件。

```
🔥 Program comments provided by ChatGPT

### 📌 DataTable 欄位排名 Rank #排名 Rank
```C#

DataTable dt_index = new DataTable();

dt_index.Column.Add("Rank",typeof(int));

dt_index.Column.Add("Total",typeof(double));

...

// 進行排名
dt_index.AsEnumerable()
  .OrderByDescending(row => row.Field<double>("Total")) // 按 Total 欄位降序排序
  .Select((row, index) =>
  {
      row["Rank"] = index + 1; // 設置 Rank 欄位
      return row;
  }).ToList();

```
🔥 Program comments provided by ChatGPT

### 📌 DataTable 欄位順序調整 #Column SetOrdinal
```C#

private void MoveColumn(ref DataTable table, string sourceColumnName, string targetColumnName)
{
    // 獲取源列和目標列
    DataColumn sourceColumn = table.Columns[sourceColumnName];
    DataColumn targetColumn = table.Columns[targetColumnName];

    // 確保源列和目標列都存在
    if (sourceColumn != null && targetColumn != null)
    {
        // 確定目標列的索引
        int targetIndex = targetColumn.Ordinal;

        //直接使用 SetOrdinal 移動源列的位置
        sourceColumn.SetOrdinal(targetIndex); // 改變列的位置
    }
}

```
🔥 Program comments provided by ChatGPT

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

### 📌 Delete From DataTable Select #Delete From DataTable
```C#

DataRow[] dr_Index = dt_Index.Select("TYPE = 'A' ");

Array.ForEach(dr_Index, row => row.Delete()); // 免迴圈

dt_Index.AcceptChanges();

```
> Delete() 方法只是標記列為刪除狀態，真正刪除資料是在執行 AcceptChanges() 時完成。若沒有呼叫 AcceptChanges()，資料列將仍然存在，只是被標記為已刪除。

### 📌 操作所有資料 免迴圈 #Edit in DataRow[] without for loop
```C#

DataRow[] dr_Index = dt_Index.Select("TYPE = 'A' ");

Array.ForEach(dr_Index, row => row["Column_Status"] = "Checked"); // 免迴圈

```

## `<Dictionary>`

### 📌 Dictionary 建立 #新建
```C#

Dictionary<string, int> dir_Index = new Dictionary<string, int>(){{"Amy",10},{"Jack",12}};

dir_Index["Sean"] = 18;
dir_Index["Mandy"] = 7;

```

### 📌 Dictionary 取值 #取值
```C#

Dictionary<string, string> dic_Index = new Dictionary<string, string>(){};

dic_Index["A"] = "AAA";
dic_Index.Values;

// <方法一> for
for (int i = 0; i < dic_Index.Count; i++)
{
    string key = dic_Index.Keys.ElementAt(i);
    string value = dic_Index.Values.ElementAt(i);
}

// <方法二> foreach
foreach (var item in dic_Index)
{
    string key = item.Key;
    string value = item.Value;
}

// <方法三> 鍵取值
string value = dic_Index["A"];

```
🔥 Program comments provided by ChatGPT

### 📌 Dictionary 每個元素進行處理 #免迴圈
```C#

Dictionary<string, string> dir_Index = new Dictionary<string, string>(){};

dir_Index["A"] = "AAA";
dir_Index["B"] = "BBB";
dir_Index["C"] = "CCC";

// 字尾處理
dir_Index = dir_Index.ToDictionary(kv => kv.Key, kv => kv.Value.ToString().Substring(0, kv.Value.ToString().Length - 1));

```

### 📌 Dictionary 排序 OrderBy #排序 OrderBy
```C#

Dictionary<string, string> dir_Index = new Dictionary<string, string>(){};

dir_Index["1"] = "AAA";
dir_Index["3"] = "BBB";
dir_Index["4"] = "CCC";
dir_Index["2"] = "DDD";

// By Key 排序
dir_Index = dir_Index.OrderBy(k => k.Key).ToDictionary(k => k.Key, p => p.Value);
// By Value 排序
dir_Index = dir_Index.OrderBy(p => p.Value).ToDictionary(k => k.Key, p => p.Value);

```

## `<String>`

### 📌 String Split 多字元 #字串處理、字串分割
```C#

string index_STR = "白日依山盡，黃河入海流";

index_STR.Split('，');

// 移除空值
index_STR.Split(new[] { '，' }, StringSplitOptions.RemoveEmptyEntries);

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
> `轉義字符` : 如果字串本身包含大括號{}，則使用雙大括號進行轉義。
> string.Format("{{0}} + {{1}}","A","B")
> Result : "{A} + {B}"

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

### 📌 String Concat 字串重複 (Repeat效果) #字串重複
```C#

string index_STR = string.Concat(Enumerable.Repeat("ABC", 5));

```

## `<Linq>`

### 📌 特殊排序 #特殊排序
```C#

// 排序 忽略 某個值 達到讓某個值 在第一位的效果

string[] values = { "B", "C", "ALL", "A" };

values = values.OrderBy(x => x != "ALL").ThenBy(x => x).ToArray();

```

## `<DateTime>`

### 📌 Date To Weekly #日期 轉 週別
```C#

int index_Week = new CultureInfo("en-US").Calendar.GetWeekOfYear( DateTime.Now, new CultureInfo("en-US").DateTimeFormat.CalendarWeekRule, new CultureInfo("en-US").DateTimeFormat.FirstDayOfWeek )

```
Refer to : [Microsoft Build](https://docs.microsoft.com/zh-tw/dotnet/api/system.globalization.calendar.getweekofyear?view=net-6.0)

### 📌 Date To Week #日期 轉 星期
```C#

DateTime this_day = DateTime.Now;

DayOfWeek dw = this_day.DayOfWeek;

CultureInfo cultureInfo = CultureInfo.CurrentCulture; // 或者使用特定的文化，例如: new CultureInfo("en-US");

string shortDayName = cultureInfo.DateTimeFormat.GetShortestDayName(dw);

```

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

### 📌 List 內容查詢 #List Contains
```C#

List<string> MyList = new List<string> {"AAA", "BBB", "CCC", "DDD"};

string SearchValue = "AAA";

if (MyList.Contains(SearchValue))
{
    // 找到
}
else
{
    // 找不到
}

```

### 📌 List 建立數字陣列 #Enumerable.Range
```C#

List<string> ls_Index = Enumerable.Range(1, 25).ToList();

// Result : 1~25

```

### 📌 新增值於第N個位置 #List Insert
```C#

List<string> ls_Index = new List<string>() { "A","B","C" };

ls_Index.Insert(0, "D");

// Result : "D","A","B","C"

```

### 📌 List 計算 #Sun、Average、Take、TakeLast、Spip
```C#

List<int> mylist = new List<int> { 1, 2, 0, 4, 5, 6, 7, 0, 9, 10, 11, 12, 0, 14 };

// 加總
int this_sum = mylist.Sum();

// 平均
double this_average = mylist.Average();

// 排除值為 0 的元素
double this_average = mylist.Where(n => n != 0).Average();

// 取前 7 筆資料並計算平均值
double this_average = mylist.Take(7).Average();

// 取最後 7 筆資料並計算平均值
// .NET 6 及以上版本
double this_average = mylist.TakeLast(7).Average();

// 適用於所有 .NET 版本
double this_average = mylist.Skip(Math.Max(0, numbers.Count - 7)).Average();

```
🔥 Program comments provided by ChatGPT

### 📌 List 內容移除 (兩個 List 比對) #List Remove
```C#
using System.Collections.Generic; // HashSet

List<string> List_A = new List<string> {"BBB", "DDD"};
List<string> List_B = new List<string> {"AAA", "BBB", "CCC"};
List<string> List_C = new List<string> {"DDD", "EEE", "FFF"};

// 將 List_A 的元素添加到 HashSet 中
HashSet<string> setA = new HashSet<string>(List_A);

// 從 List_B 中移除與 List_A 重複的元素
List_B.RemoveAll(item => setA.Contains(item));

// 從 List_C 中移除與 List_A 重複的元素
List_C.RemoveAll(item => setA.Contains(item));
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

### 📌 時間區間重疊計算 #時間重疊
```C#

static TimeSpan GetOverlap(DateTime start1, DateTime end1, DateTime start2, DateTime end2)
{
    // 找到重疊的開始和結束時間
    DateTime overlapStart = start1 > start2 ? start1 : start2;
    DateTime overlapEnd = end1 < end2 ? end1 : end2;

    // 如果重疊的開始時間早於結束時間則存在重疊
    if (overlapStart < overlapEnd)
    {
        return overlapEnd - overlapStart; // 返回重疊的時間
    }

    return TimeSpan.Zero; // 不重疊
}

```
🔥 Program comments provided by ChatGPT

### 📌 Json 轉 DataTable #Json To DataTable
```C#

using Newtonsoft.Json;

// ...

static DataTable Json_To_DataTable(string this_json)
{
    DataTable dataTable = null;

    if (!string.IsNullOrEmpty(this_json))
    {
        // 使用 JObject 解析 JSON
        var xmlDoc = new XmlDocument();
        xmlDoc.LoadXml(this_json);

        // 取得 QueryResult 節點的值
        string queryResultJson = xmlDoc.InnerText;

        if (!string.IsNullOrEmpty(queryResultJson))
        {
            // 確保得到的 JSON 格式是有效的，然後解析
            dataTable = JsonConvert.DeserializeObject<DataTable>(queryResultJson);
        }
        else
        {
            // 錯誤處理：QueryResult 節點未找到或無效
            throw new Exception("QueryResult not found in the response.");
        }
    }
    else
    {

    }

    return dataTable;
}

```

## `<Element>`

### 📌 Button Click 動態連結事件 #Button Dynamic Click
```C#

private void Button_Setting(string f_type){
  if(f_type = "A"){
    Button_Element.Click += Button_Element_Click_A;
  }
  else
  {
    Button_Element.Click += Button_Element_Click_B;
  }
}

protected void Button_Element_Click_A(object sender, EventArgs e){
  // Click A Event
}

protected void Button_Element_Click_B(object sender, EventArgs e){
  // Click B Event
}

```


### 📌 Input Type=number & runat:server 剖析器錯誤 #Input Type number and runat server error
#### HTML
```HTML

<!-- 可能會出現錯誤 → 剖析器錯誤訊息: 'number' 不是輸入標記的有效型別。原因可能是 .Net Framework 版本差異 -->
<input id="this_textbox" type="number" placeholder="輸入數字" runat="server" />

<!-- 解法 : 由後段設定 Attributes 屬性 -->
<input id="this_textbox" placeholder="輸入數字" runat="server" />

```
#### C#
```C#
protected void Page_Load(object sender, EventArgs e){
  this_textbox.Attributes.Add("type", "number");
}
```
Refer to : [stackoverflow](https://stackoverflow.com/questions/9801120/html5-email-input-cannot-assign-id-and-runat-server-asp-net-4/27561096#27561096)

## `<Other>`
### 📌 值類型、引用類型 #value type、reference type
#### C#
```C#
private void Change_Array_Value(int[] index_array,int index_num){
    index_array[0] = 4;
    index_num = 100;
}

private void Main(){
    int[3] original_array = new int[] {1,2,3};
    int original_num = 10;

    Change_Array_Value(original_array,original_num);

    // Output
    // original_array[0] 會變為 4
    // original_num 則不變
}
```

### 📌 二進位轉十進位 #binary to decimal
```C#

string binStr = "1011"; // 二進位字串

int number = Convert.ToInt32(binStr, 2);

// 較長的二進位
string binStr = "111110"; // 二進位字串

long number = Convert.ToUInt64(binStr, 2);

```

### 📌 十進位轉二進位 #decimal to binary
```C#

int number = 42; // 要轉換的十進位數

string binStr = Convert.ToString(number, 2); // 第二個參數是「進位」（二進位：2）

```
