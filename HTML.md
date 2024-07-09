# HTML Quick Note 前端

![](https://img.shields.io/badge/-HTML-brightgreen) ![](https://img.shields.io/badge/-JavaScript-orange) ![](https://img.shields.io/badge/-CSS-FF00FF)

| Function                     |
| :--------------------------: |
|[分頁效果](#-分頁效果)         |  

### 📌 分頁效果
#### CSS
```CSS
#tab-demo > ul { display: block;  margin: 0 -1%;  list-style: none;  text-align: left;}
.tab-title {  list-style: none;}
#tab-demo > ul > li {  font-size: medium;  display: inline-block;  vertical-align: top;  margin: 0 -1px -1px 0;  border: 1px solid #BCBCBC;  line-height: 35px;  background: #F7F7F7;  padding: 0 10px;  list-style: none;  box-sizing: border-box;}
#tab-demo > ul > li a {  color: #000;  text-decoration: none;}
#tab-demo > ul > li.active {  border-bottom: 1px solid #fff;  background: #fff;}
#tab-demo > .tab-inner {  clear: both;  border: 1px #BCBCBC solid;}
.tab-inner {  padding: 15px;  background-color: white;  overflow: auto;}
```
#### JavaScript
```JavaScript
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
```
#### HTML
```HTML
<div id="tab-demo" style=" width:99%; margin:auto;">
  <!-- 分頁標籤 -->
  <ul class="tab-title">
    <li onclick="Selector_Click('tab_One')"><a href="#" onclick="Selector_Click('tab_One')" style="font-size:small;">One</a></li>
    <li onclick="Selector_Click('tab_Two')"><a href="#" onclick="Selector_Click('tab_Two')" style="font-size:small;">One</a></li>
    <li onclick="Selector_Click('tab_Three')"><a href="#" onclick="Selector_Click('tab_Three')" style="font-size:small;">One</a></li>
  </ul>

  <!-- 分頁內容 -->
  <div id="tab_One" class="tab-inner" style=" margin:auto;"></div>
  <div id="tab_Two" class="tab-inner" style=" margin:auto; display:none;"></div>
  <div id="tab_Three" class="tab-inner" style=" margin:auto; display:none;"></div>
</div>
```

