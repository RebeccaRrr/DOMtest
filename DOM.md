# DOM

标签（空格分隔）： 未分类

---

hasChildNodes，hasAttributes方法
document.documentElement.hasChildNodes()
访问标签内容：innerHTML，textContent，nodeValue。其实textContent返回的是可追踪的DOM节点树，innerHTML返回的只是标签字符串
DOM方法：getElementsByTagName(),getElementById(),getAttribute(),getElementsByName()，getElementsByClassName()
兄弟节点：para.nextSibling,previousSibling
首尾节点：firstChild,lastChild
**修改样式**：my.style.border = "1px solid red";
CSS样式的JavaSript属性版本以小驼峰式命名法书写，而CSS版本带连接符号（backgroundColor 对 background-color）。确保你不会混淆，否则就不能工作。
**新建节点**：

 - createElement(),createTextNode()
例子：

    var myp = document.createElement('p');
    var myt = document.createTextNode('one more paragraph');
    myp.appendChild(myt);
    var str = document.createElement('strong');
    str.appendChild(document.createTextNode('bold'));
    myp.appendChild(str);
    document.body.appendChild(myp);

 - 克隆节点：cloneNode(false/true)。为false时浅拷贝只拷贝当前节点，为true时深拷贝，包括所有子节点。
 - appendChild：将新节点添加到指定节点的末端.
 - insertBefore()方法：可精确控制插入节点的位置。
   如以下代码中文本节点被插入body元素末端：
   document.body.appendChild(document.createTextNode('boo!'));
   或document.body.insertBefore(document.createTextNode('boo!')，document.body.firstChild);
**移除文本**removeChild()

    var myp = document.getElementsByTagName('p')[1];
    var removed = document.body.removeChild(myp);

replaceChild(removed,p)可用removed变量中的段落替换掉当前段落
若要将一个子树的内容全部删去，可将innerHTML设为空串。或者用纯DOM方法如下：
function removeAll(n){
while(n.firstChild){
   n.removeChild(n.firstChild);
}
}


----------


DOM事件
-----

1.内联HTML属性法

    <div onclick = "alert('boo')">click</div>

2.元素属性法

    var mypara = document.getElementById('closer');
      mypara.onclick = function(){
            alert('ouch!');
        }
        
        
3.DOM事件监听器
首参数是一个事件类型的参数，第二个参数是一个函数指针，第三个参数表示代码是否采用捕捉法来处理事件。
捕捉法：从document对象依次向下传递，最终到达链接
冒泡法：首先发生在链接上，然后逐层向上冒泡直至document对象

          var mypara = document.getElementById('closer');
          mypara.addEventListener('click',function(){
          alert('Boo!')},false);
          


----------
事件由具体标签向整个窗口传播的全过程

          var mypara = document.getElementById('closer');
          function paraHandler(){
        alert('clicked paragragh');
    }
    mypara.addEventListener('click',paraHandler,false);
    document.body.addEventListener('click',function(){ alert('click body')},false);
    document.addEventListener('click',function(){ alert('click doc')},false);
    window.addEventListener('click',function(){ alert('click window')},false);
          
removeEventListener可移除段落上的监听器，由匿名函数定义的监听器不能被移除。          mypara.removeEventListener('click',paraHandler,false);
阻断事件传播：调用stopPropagation()方法

    function paraHandler(){
            alert('clicked paragragh');
             e.stopPropagation();
        }