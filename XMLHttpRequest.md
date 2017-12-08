# XMLHttpRequest

标签（空格分隔）： 未分类

---
创建XHR对象：
variable=new XMLHttpRequest();或
variable=new ActiveXObject("Microsoft.XMLHTTP");
向服务器发送请求：
xmlhttp.open("GET","test1.txt",true);
 - method：请求的类型；GET 或 POST 
 - url：文件在服务器上的位置 
 - async：true（异步）或 false（同步）
xmlhttp.send();
 - string：仅用于 POST 请求

与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。
然而，在以下情况中，请使用 POST 请求：
无法使用缓存文件（更新服务器上的文件或数据库）
向服务器发送大量数据（POST 没有数据量限制）
发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠
XHR存在readystate属性，当属性发生改变会触发readystatechange事件，该属性的可能状态值如下：
0-未初始化，1-载入请求，2-载入完成，3-请求交互，4-请求完成
status属性，若目标不存在则返回404，目标存在则返回200.

    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      }
    xmlhttp.open("GET","test1.txt",true);
    xmlhttp.send();



