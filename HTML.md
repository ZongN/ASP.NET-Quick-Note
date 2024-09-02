# HTML Quick Note 前端

![](https://img.shields.io/badge/-HTML-brightgreen) ![](https://img.shields.io/badge/-JavaScript-orange) ![](https://img.shields.io/badge/-CSS-FF00FF)

| Function                     |
| :--------------------------: |
|[分頁效果](#-分頁效果)、[自動刷新](#-自動刷新) 、[摺疊效果-上下](#-摺疊效果-上下)、[摺疊效果-左右](#)、[iframe loading 監聽事件](#-iframe-loading-監聽事件)、[限制只能輸入數字](#-限制只能輸入數字)、[jQuery拖動視窗效果](#-jquery拖動視窗效果)、[後端觸發前端的Document Ready事件(jQuery)](#-後端觸發前端的-document-ready-事件jquery)、[jQuery引用不同版本](#-jquery引用不同版本)、[jQuery 客製 tooltip](#-jquery-客製-tooltip)|

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

### 📌 後端註冊+觸發前端的 Document Ready 事件(jQuery)
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
