#jS
#初识
	1.引入JS
		1.1.内嵌式：js写在script标签中
·			<script>
			    alert('沙漠骆驼')
			</script>

		2.外联式：js写在一个单独的.js文件中
			.需要通过script标签在网页中引入，一般会在一个大的项目中用
			<script src="my.js"></script>
	
		3.行内式：js写在标签的属性中
			 <input type="button" value="唐伯虎" onclick="alert('秋香')">
	2.输入框：prompt（'请输入你的年龄'）
	3.弹出框：alert（'计算结果是'）
	3.控制台输出，程序员看的：console.log（'程序员看的')
##变量
	1.变量命名规范
		..由字母(A-Za-z)、数字(0-9)、下划线()、美元符号($)组成，如：usrAge,num01,_name·严格区分大小写。varapp；和var App；是两个变量
		..不能以数字开头。18age 是错误的
		..不能是关键字、保留字。例如：var、for、while
		..变量名必须有意义。MMD BBD nl → age
		..遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。myFirstName 
#DOM
##常用方法:
	1.获取节点：
		通用：document.querySelector('')    //查找第一个，只需在引号里添加相应的选择属性，和css一致  .类名  #id名
			 document.querySelectorAll('')  //查找全部，以数组的形式存放所有的相应的元素对象
		document.getElementById(idName)          //通过id号来获取元素，返回一个元素对象
		document.getElementsByName(name)       //通过name属性获取id号，返回元素对象数组
		document.getElementsByClassName(className)   //通过class来获取元素，返回元素对象数组（ie8以上才有）
		document.getElementsByTagName(tagName)       //通过标签名获取元素，返回元素对象数组
	2.获取/设置元素的属性值：
		element.getAttribute(attributeName)     //括号传入属性名，返回对应属性的属性值
		element.setAttribute(attributeName,attributeValue)    //传入属性名及设置的值
	3.创建节点Node：
		document.createElement("h3")       //创建一个html元素，这里以创建h3元素为例
		document.createTextNode(String); //创建一个文本节点；
		document.createAttribute("class"); //创建一个属性节点，这里以创建class属性为例
	4.增添节点：
		element.appendChild(Node);   //往element内部最后面添加一个节点，参数是节点类型
		element.insertBefore(newNode,existingNode); //在element内部的中在existingNode前面插入newNode
		element.insertBefore(sp1, sp2.nextSibling);

	5.删除节点：
		element.removeChild(Node)    //删除当前节点下指定的子节点，删除成功返回该被删除的节点，否则返回null
	6.替换节点：
		replaceChild             //用于将一个节点替换另一个节点，语法：
	
	    parent.replaceChild(newChild, oldChild); 

##常用属性:
	1.获取当前元素的父节点 ：
			element.parentNode     //返回当前元素的父节点对象
	2.获取当前元素的子节点：
			element.chlidren        //返回当前元素所有子元素节点对象，只返回HTML节点
			element.chilidNodes   //返回当前元素多有子节点，包括文本，HTML，属性节点。（回车也会当做一个节点）
			element.firstChild      //返回当前元素的第一个子节点对象
			element.lastChild       //返回当前元素的最后一个子节点对象
	3.获取当前元素的同级元素：
			element.nextSibling          //返回当前元素的下一个同级元素 没有就返回null
			element.previousSibling   //返回当前元素上一个同级元素 没有就返回null
	4.获取当前元素的文本：
			element.innerHTML   //返回元素的所有文本，包括html代码
			element.innerText     //返回当前元素的自身及子代所有文本值，只是文本内容，不包括html代码
	5.获取当前节点的节点类型：
			node.nodeType   //返回节点的类型,数字形式（1-12）常见几个1：元素节点，2：属性节点，3：文本节点。
	6.设置样式：
			element.style.color=“#eea”;      //设置元素的样式时使用style，这里以设置文字颜色为例。
###自定义属性
	设置：
	1.html实现：
		1.<div data-index='2'></div>   //H5的写法 'data-'是自定义属性的前缀 便于区分自定义属性和内置属性
		2.<div id="dt" index='2'></div>   //H5以前版本的写法
	2.js实现：
		1.setAttribute('属性','值')
		2.元素对象名.dataset.属性名 = 值           //只能设置data-开头的
	获取：
		1.getAttribute('属性')

  		对象名.dataset.属性
  		 
  		2.对象名.dataset['属性']      //dataset是一个集合，里面存放了所有以“ data- ”开头的自定义属性

##三种动态创建元素区别
		document.write()
		element.innerHTML
		document.createElement()
	2.区别：
		1.document.write 是直接将内容写入页面的内容流，但是文档流执行完毕，则它会导致页面全部重绘
		2.innerHTML 是将内容写入某个 DOM 节点，不会导致页面全部重绘
		3.innerHTML 创建多个元素效率更高（不要拼接字符串，采取数组形式拼接），结构稍微复杂
		4.createElement() 创建多个元素效率稍低一点点，但是结构更清晰
	总结：不同浏览器下，innerHTML 效率要比 creatElement
