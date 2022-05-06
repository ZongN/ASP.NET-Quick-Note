# ASP.NET C# Quick Note

![](https://img.shields.io/badge/ASP.NET-C%23-brightgreen)

### 1. DataTable Add New Row : 
```C#

DataTable dt_Index = new DataTable();
dt_Index.Columns.Add("A",typeof(double));
dt_Index.Columns.Add("B",typeof(double));
dt_Index.Columns.Add("C",typeof(double));

DataRow dr_Index = dt_Index.NewRow();
dr_Index["A"] = 10;
dr_Index["B"] = 11.5;
dr_Index["C"] = 0.9;

dt_Index.Rows.Add(dr_Index);
```

### 2.DataTable Column Sorting
```C#

dt_Index.DefaultView.Sort = "Columns_A DESC";

dt_Index = dt_Index.DefaultView.ToTable();

```

### 3.DataTable Row Get Unique
```C#

DataView dv_index = new DataView(dt_Index);
dt_Index = dv_index.ToTable(true,"Columns_A");

```
> Before :
| Columns_A  | Columns_B |
| ---------- | --------- |
| 2022-05-05 | Jack  |
| 2022-05-05 | Mandy |
| 2022-05-01 | Amy |
| 2022-05-01 | Sean |
| 2022-05-03 | Mandy |
> After :
| Columns_A  |
| ---------- |
| 2022-05-05 |
| 2022-05-01 |
| 2022-05-03 |
