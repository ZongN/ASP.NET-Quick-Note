# HTML Quick Note 前端

![](https://img.shields.io/badge/-HTML-brightgreen) ![](https://img.shields.io/badge/-JavaScript-orange) ![](https://img.shields.io/badge/-CSS-FF00FF)

| Function                     |
| :--------------------------: |
|[分頁效果](#-分頁效果)、[自動刷新](#-自動刷新) 、[摺疊效果-上下](#-摺疊效果-上下)、[摺疊效果-左右](#)、[iframe loading 監聽事件](#-iframe-loading-監聽事件)、[限制只能輸入數字](#-限制只能輸入數字)、[jQuery拖動視窗效果](#-jquery拖動視窗效果)、[後端註冊JavaScript Function事件](#-後端註冊-javascript-function事件)、[jQuery引用不同版本](#-jquery引用不同版本)、[jQuery 客製 tooltip](#-jquery-客製-tooltip)、[Javascript 觸發 AsyncPostBackTrigger 事件](#-javascript-觸發-asyncpostbacktrigger-事件)、[水平導航列 Navbar-純css](#-水平導航列-navbar-純css)、[CSS閃爍效果](#-css閃爍效果)、[Javascript Ajax Web Service(SOAP)](#-javascript-ajax-web-service-soap)、[兩物件連接線效果](#-兩物件連接線效果-利用-javascript-添加-連接線-物件)、[Table固定標頭-純css](#-table固定標頭)、[後端關閉網頁](#-後端關閉網頁)|

### 📌 分頁效果
#### CSS
```CSS

// 頁籤在上
#tab-demo > ul { display: block;  margin: 0 -1%;  list-style: none;  text-align: left;}
.tab-title {  list-style: none;}
#tab-demo > ul > li {  font-size: medium;  display: inline-block;  vertical-align: top;  margin: 0 -1px -1px 0;  border: 1px solid #BCBCBC;  line-height: 35px;  background: #F7F7F7;  padding: 0 10px;  list-style: none;  box-sizing: border-box;}
#tab-demo > ul > li a {  color: #000;  text-decoration: none;}
#tab-demo > ul > li.active {  border-bottom: 1px solid #fff;  background: #fff;}
#tab-demo > .tab-inner {  clear: both;  border: 1px #BCBCBC solid;}
.tab-inner {  padding: 15px;  background-color: white;  overflow: auto;}

// 頁籤在左
#tab-demo{display: flex;}
#tab-demo > ul{display: block;width: 150px;list-style: none;text-align: left;margin-right: -1px;padding: 0;z-index: 99;max-height: 50vh;}
.tab-title{list-style: none;}
#tab-demo > ul > li{display: block;margin: 0;border: 1px solid #BCBCBC;line-height: 35px;background: #F7F7F7;padding: 0 10px;box-sizing: border-box;}
#tab-demo > ul > li a{color: #000;text-decoration: none;}
#tab-demo > ul > li.active{border-right: 1px solid #fff;background: #fff;}
#tab-demo > .tab-inner{border: 1px #BCBCBC solid;flex: 1;}
.tab-inner{padding: 15px;background-color: white;overflow: auto;display: flex;height: 93vh;z-index: 0;}
```
#### JavaScript
```JavaScript
<script type="text/javascript" src="XXX/jquery.min.js"></script>
<script type="text/javascript" src="XXX/jquery-ui.js"></script>
<script type="text/javascript">
// 網頁預載 Function
$(function () {
        // 模擬 Excel 各個 Sheet 分頁 ，切換的效果
        var $li = $('ul.tab-title li');
        $($li.eq(0).addClass('active').find('a').attr('href')).siblings('.tab-inner').hide(); // li.eq(0) → 預設 第 0 頁 

    $li.click(function () {
        $($(this).find('a').attr('href')).show().siblings('.tab-inner').hide();
        $(this).addClass('active').siblings('.active').removeClass('active');
    });
});
// Onclick 切換效果
function Selector_Click(ul_id) {
    //////////////// 這段 處理 各分頁 激活效果 ////////////////
    var list = document.getElementsByClassName('tab-inner');

    for (var i = 0; i < list.length; i++) {

        var index_id = document.getElementsByClassName('tab-inner')[i].id;

        document.getElementById(index_id).style.display = "none";

        if (index_id.indexOf(ul_id) >= 0) {
            document.getElementById(index_id).style.display = null;
        }
    }
}
</script>
```
#### HTML
```HTML
<div id="tab-demo" style=" width:99%; margin:auto;">
  <!-- 分頁標籤 -->
  <ul class="tab-title">
    <li onclick="Selector_Click('tab_One')"><a href="#" onclick="Selector_Click('tab_One')" style="font-size:small;">One</a></li>
    <li onclick="Selector_Click('tab_Two')"><a href="#" onclick="Selector_Click('tab_Two')" style="font-size:small;">Two</a></li>
    <li onclick="Selector_Click('tab_Three')"><a href="#" onclick="Selector_Click('tab_Three')" style="font-size:small;">Three</a></li>
  </ul>

  <!-- 分頁內容 -->
  <div id="tab_One" class="tab-inner" style=" margin:auto;"></div>
  <div id="tab_Two" class="tab-inner" style=" margin:auto; display:none;"></div>
  <div id="tab_Three" class="tab-inner" style=" margin:auto; display:none;"></div>
</div>
```

### 📌 自動刷新
#### JavaScript
```JavaScript
<script>
        // 每 5 秒刷新一次頁面
        setInterval(function(){location.reload();} , 5000);
</script>
```

### 📌 摺疊效果-上下
#### JavaScript
```JavaScript
<script>
        // 收合效果 (jQuery效果)
        function Fold_Unfold(element_id) {
                var this_element = "#" + element_id;
                $(this_element).slideToggle('3500'); // 3500 = 3500 ms 完成摺疊
        }
</script>
```

### 📌 iframe loading 監聽事件
#### JavaScript
```JavaScript
<script>
        function main(){
                // 先加入 iframe 的 loading 監聽事件
                iframe_add_loading_event('this_iframe');
                // 重新導向 src 觸發 loading
                document.getElementById('this_iframe').src = "https://github.com/ZongN/ASP.NET-Quick-Note/blob/main/C%23.md";
        }

        function iframe_add_loading_event(iframe_id) {
                // Loading 中的行為
                // ...
                // Loading 中的行為
                var iframe = document.getElementById(iframe_id);
                iframe.addEventListener('load', function () {
                        // 結束的行為
                        // ...
                        // 結束的行為
                });
        }
</script>
```

### 📌 限制只能輸入數字
#### JavaScript
```JavaScript
<script>
        function isNumberKey(evt) {
                var charCode = (evt.which) ? evt.which : event.keyCode;
                if (charCode < 48 || charCode > 57)
                    return false;
                else
                    return true;
            }
</script>
```
#### HTML
```HTML
<div>
        <input type="text" id="this_text" onkeypress="return isNumberKey(event)" />
</div>
```

### 📌 jQuery拖動視窗效果
#### JavaScript
```JavaScript
<script>
        $(function () {
                ("#draggable").draggable({ containment: "parent" }); // 表示拖拽元素只能在其父元素內移動，不能超出父元素的範圍
        });
</script>
```

### 📌 後端註冊 JavaScript Function事件
#### C#
```C#
// 註冊 JS Function
// 警示訊息彈窗
ScriptManager.RegisterStartupScript(this, this.GetType(), "alertScript", "alert('這是一個警示訊息！');", true);

// 修改元素樣式的腳本
string script = "document.getElementById('myElement').style.color = 'red';";
ScriptManager.RegisterStartupScript(this, this.GetType(), "styleScript", script, true);

// 彈出彈窗
string script = "alert('您點選了按鈕！');";
ScriptManager.RegisterStartupScript(this, this.GetType(), "buttonClickScript", script, true);
```

### 📌 jQuery引用不同版本
#### JavaScript
```JavaScript
<script type="text/javascript" src="script/1.9.1/jquery.min.js"></script>
<script type="text/javascript">var jQ191 = $.noConflict(true);</script>

<script type="text/javascript" src="script/3.6.0/jquery.min.js"></script>
<script type="text/javascript">var jQ360 = $.noConflict(true);</script>

<script>
        // 網頁預載 Function
        jQ191(function ($) {
                // Example : Js DataTable
                $("#MyTable").DataTable({
                    "autoWidth": false,
                    "scrollCollapse": true,
                    "scrollY": "32vh",
                    "scrollX": true,
                    "paging": false,
                    "searching": false,
                    "info": false
                });
        });

        jQ360(function ($) {
                // XXX
        });
</script>
```
Refer to : [博客园](https://www.cnblogs.com/djd66/p/9243290.html)

### 📌 jQuery 客製 tooltip
#### CSS
```CSS
.custom-tooltip {
	display: none;
	position: absolute;
	background-color: black;
	color: #fff;
	padding: 5px;
	border-radius: 5px;
	font-size: 14px;
	z-index: 1000;
}
```
#### JavaScript
```JavaScript
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
	$(document).ready(function(){
		// 選擇所有包含 title 屬性的元素
		$('[title]').hover(
			// 滑鼠進入事件
			function(event){
				// 取得 title 屬性的值
				var tooltipContent = $(this).attr('title');
				
				// 清空 title 屬性，避免瀏覽器預設的工具提示
				$(this).attr('data-title', tooltipContent).removeAttr('title');
				
				// 顯示自定義工具提示
				$('#tooltip').html(tooltipContent).css({
					display: 'block',
					top: event.pageY + 10 + 'px',
					left: event.pageX + 10 + 'px'
				});

				this.style.cursor = 'help';
			}, 
			// 滑鼠離開事件
			function(){
				// 隱藏工具提示，並恢復 title 屬性
				var originalTitle = $(this).attr('data-title');
				$(this).attr('title', originalTitle);
				$('#tooltip').css('display', 'none');

				this.style.cursor = 'default';
			}
		);

		// 更新工具提示的位置
		$('[title]').mousemove(function(event){
			$('#tooltip').css({
				top: event.pageY + 10 + 'px',
				left: event.pageX + 10 + 'px'
			});
		});
    });
</script>
```
#### HTML
```HTML
<div title="Test Tooltip">Custom-Tooltip 測試區</div>

<div class="custom-tooltip" id="tooltip"></div>
```

### 📌 Javascript 觸發 AsyncPostBackTrigger 事件
#### JavaScript
```JavaScript
<script type="text/javascript">
        function MyJsFunction(){
		__doPostBack('<%=UpdatePanel_1.ClientID%>'); // 主動觸發
	}
</script>
<script runat="server">
    protected void HiddenField_ValueChanged(object sender, EventArgs e)
    {
        TextBox_B.Text = HiddenField_A.Value;
	// 這裡也可以呼叫後端 .cs 中的 public function
    }
</script>
```

#### HTML
```HTML
<asp:UpdatePanel ID="UpdatePanel_1" runat="server" UpdateMode="Conditional">
	<ContentTemplate>
		<asp:TextBox ID="TextBox_B" runat="server"></asp:TextBox>
        	<asp:HiddenField ID="HiddenField_A" runat="server" OnValueChanged="HiddenField_ValueChanged" />
	</ContentTemplate>
    	<Triggers>
		<asp:AsyncPostBackTrigger ControlID="HiddenField_A" />
    	</Triggers>
</asp:UpdatePanel>
```

### 📌 水平導航列 Navbar-純css
#### CSS
```CSS
.NavBar
{

}

/* 父節點 */
.NavBar > ul {
    padding: 0;
    list-style-type: none;            
    white-space: nowrap;
    background-color:lime;
}

.NavBar > ul > li {
    display: inline-block;
    margin: .5%;
}

.NavBar label:hover {
    cursor:pointer;
    color:white;
}

/* 展開子節點 */
.NavBar li:hover > ul {
    display: block;
}

/* 子節點 */
.NavBar > ul ul {
    background:silver;
    display: none;
    position:fixed;
    list-style-type: none;
    padding:.5%;
}

.NavBar > ul ul > li {
    margin-bottom: 5px; /* li 間距*/
}
```
#### HTML
```HTML
<div class="NavBar">
    <ul>
	<li><label>A-Item</label></li>
	<li><label>B-Item</label>
	    <ul>
		<li><label>B001-Item</label></li>
		<li><label>B002-Item</label></li>
		<li><label>B003-Item</label>
		    <ul>
			<li><label>B011-Item</label></li>
			<li><label>B012-Item</label></li>
			<li><label>B013-Item</label></li>
			<li><label>B014-Item</label></li>
		    </ul>
		</li>
	    </ul>
	</li>
	<li><label>C-Item</label></li>
	<li><label>D-Item</label>
	    <ul>
		<li><label>D001-Item</label></li>
		<li><label>D002-Item</label></li>
		<li><label>D003-Item</label></li>
		<li><label>D004-Item</label></li>
		<li><label>D005-Item</label></li>
	    </ul>
	</li>
	<li><label>E-Item</label></li>
    </ul>
</div>
```

### 📌 CSS閃爍效果
#### CSS
```CSS
/* 定義一個閃爍效果的關鍵幀動畫 */
@-webkit-keyframes fade {
	from {
		opacity: 1.0; /* 動畫開始時的透明度為1.0（完全不透明） */
	}
	50% {
		opacity: 0.4; /* 動畫中途時的透明度為0.4（半透明） */
	}
	to {
		opacity: 1.0; /* 動畫結束時的透明度回到1.0（完全不透明） */
	}
}

/* 定義一個閃爍效果的CSS類 */
.blink {
	-webkit-animation: fade 600ms infinite; /* 應用fade動畫，持續600毫秒並無限循環 */
}
```
#### HTML
```HTML
<div class="blink">
    Blink Test
</div>
```

### 📌 Javascript Ajax Web Service (SOAP)
#### JavaScript
```JavaScript
<script type="text/javascript">
        function SendWebService(parameter_1, parameter_2, parameter_3)
        {
		var soapMessage = `<?xml version="1.0" encoding="utf-8"?>
					<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
	     					<soap:Body>
							<MyFunction xmlns="http://tempuri.org/">
		                                            <parameter_1>${parameter_1}</parameter_1>
		                                            <parameter_2>${parameter_2}</parameter_2>
		                                            <parameter_3>${parameter_3}</parameter_3>
		                                        </MyFunction>
						</soap:Body>
					</soap:Envelope>`;
                $.ajax({
                    type: "POST",
                    url: "http://XXXXXXXXXXXXXXXXXXXXXXXXXXXX.asmx",
                    data: soapMessage,
                    contentType: "text/xml; charset=utf-8",
                    dataType: "xml",
                    success: function (response) {
                        console.log("成功:", response);

                        // 回傳內容
                        var result_content = extractResponseValue(response);

                        // 將 JSON 字符串解析為 JavaScript 對象
                        var jsonArray = JSON.parse(result_content);

                        // 解析回傳值 轉成 Timeline 格式
                        if (jsonArray.length > 0)
                        {
                            refresh_content = "";

                            // 逐筆提取欄位內容
                            jsonArray.forEach(function (item) {
				console.log("Result1:", item.result_1);
				console.log("Result2:", item.result_2);
				console.log("Result3:", item.result_3);
                            });
                        }
                    },
                    error: function (xhr, status, error) {
                        console.error("錯誤:", error);
                    }
                });         
        }
        function extractResponseValue(response) {
            // 設置 NS，根據 WSDL 或實際返回的 XML 結構進行設置
            var namespaces = { soap: "http://schemas.xmlsoap.org/soap/envelope/", ns: "http://tempuri.org/" };
            // 使用查詢選擇器從 XML 響應中獲取值
            var returnValue = response.getElementsByTagName("Update_RemarkResult")[0].textContent;
            console.log("回傳值:", returnValue);
	    return returnValue;
        }
</script>
```

### 📌 兩物件連接線效果 (利用 Javascript 添加 "連接線" 物件)
#### JavaScript
```JavaScript
<script>
function draw_connect_line(parent_id, element1_id, element2_id) {

        // 取得父原素的座標點
        const parentRect = document.getElementById(parent_id).getBoundingClientRect();
        const obj1 = document.getElementById(element1_id);
        const obj2 = document.getElementById(element2_id);

        // 點1 中心座標 (相對於父元素)
        let x1 = (obj1.getBoundingClientRect().left + obj1.getBoundingClientRect().right) / 2 - parentRect.left;
        let y1 = (obj1.getBoundingClientRect().top + obj1.getBoundingClientRect().bottom) / 2 - parentRect.top;

        // 點2 中心座標 (相對於父元素)
        let x2 = (obj2.getBoundingClientRect().left + obj2.getBoundingClientRect().right) / 2 - parentRect.left;
        let y2 = (obj2.getBoundingClientRect().top + obj2.getBoundingClientRect().bottom) / 2 - parentRect.top;

        // 計算兩點距離 (歐幾里得距離算法)
        let length = Math.sqrt((x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1));

        // 計算連接線旋轉弧度值
        let rad = Math.atan2((y2 - y1), (x2 - x1));
        let deg = rad * (180 / Math.PI); // 轉換為角度

        // 連接線未旋轉前，起點座標計算
        let top = (y1 + y2) / 2;
        let left = (x1 + x2) / 2 - length / 2;

        // 創建連接線 dom 節點，並設置樣式
        let line = document.createElement('div');
        let style =`
            position: absolute;
            background-color: blue;
            height: 1px;
            top: ${top}px;
            left:${left}px;
            width:${length}px;
            transform: rotate(${deg}deg);
        `;
        line.setAttribute('style', style);

        // 加入 父元素 中
        document.getElementById(parent_id).appendChild(line);
    }

draw_connect_line('div_parent', 'div_element_1', 'div_element_2');
</script>
```
#### HTML
```HTML
<div id='div_parent'>
        <div id='div_element_1'></div>
	<div id='div_element_2'></div>
</div>
```

### 📌 Table固定標頭
#### CSS
```CSS
.table_fixed { margin:auto; width: 99%; border-spacing: 0px; border-collapse: collapse; word-break: break-all; }
.table_fixed caption { font-weight: bold; font-size: 14px; line-height: 30px; }
.table_fixed th, .table_fixed td { height: 35px; text-align: center; border: 0.5px solid gray; }
.table_fixed th { border-radius: 5px; }
.table_fixed thead { color: #194176; font-weight: lighter; background-color: #F7F7F7; }
.table_fixed tbody { display: block;  width: calc(100% + 4px); /* 這裡的4px是卷軸的寬度 */ height: 32vh; overflow-y: auto; -webkit-overflow-scrolling: touch; }
.table_fixed tfoot { background-color: #71ea71; }
.table_fixed thead tr, .table_fixed tbody tr, .table_fixed tfoot tr { box-sizing: border-box; table-layout: fixed; display: table; width: 100%; }
.table_fixed tbody tr:nth-of-type(odd) { background: #F0F0F0; /* 帶狀列效果 */ }
.table_fixed tbody tr:nth-of-type(even) {background: white; /* 帶狀列效果 */ }
.table_fixed tbody tr td { border-bottom: none; }
/* 捲軸設定 */
/* 整個捲軸 */
::-webkit-scrollbar { width: 4px; height: 4px; }
/* 捲軸的軌道 */
::-webkit-scrollbar-track { background: #E9EBEE; }
/*捲軸尚未滑到的軌道*/
::-webkit-scrollbar-track-piece { background: #E9EBEE; }
/* 滑動的區塊 */
::-webkit-scrollbar-thumb { background: #90949C; }
/* 滑鼠移到滑動的區塊上 */
::-webkit-scrollbar-thumb:hover { background: #616771; }
```
#### HTML
```HTML
<table class='table_fixed'>
	<thead>
		<tr>
			<th>column_a</th>
			<th>column_b</th>
			<th>column_c</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>A</td>
			<td>B</td>
			<td>C</td>
		</tr>
		<tr>
			<td>D</td>
			<td>E</td>
			<td>F</td>
		</tr>
		<tr>
			<td>G</td>
			<td>H</td>
			<td>I</td>
		</tr>
		<tr>
			<td>J</td>
			<td>K</td>
			<td>L</td>
		</tr>
	</tbody>
</table>
```

### 📌 後端關閉網頁
#### CS
```CS
	Response.Write("<script>window.opener=null;window.open('','_parent','');window.close();</script>");
```
