#动画
	1.过渡效果：实现两个状态间的转变
	2.动画效果：实现多个状态间的变化过程，动画过程可控（重复播放，最终画面，是否暂停）
	3.定义动画：
		1.@keyframes 动画名字 {
		  		from{}
				to{}
		  }  
		    实现两状态之间的转换
		2.@keyframes 动画名字 {
				0%{}
				10%{}
				15% {}
				100%{}
		 }      
			实现多个动画间的转换
	4.使用动画：
			animation：动画名字 动画花费时长；
			animation：动画1 ，动画2；  动画之间以逗号隔开。
	5.控制动画属性的连写：
			animation：动画名字 动画时长 速度曲线 延迟时间 重复次数 动画方向 执行完毕时的状态；
		注意：
			1. 动画名称动画时长必修赋值
			2. 取值不分先后顺序
			3. 如果有两个时间值，第一个是动画时长 ， 第二个是延迟时间
		重复次数：step（次数）
		无限循环：infinite
		动画方向：alternate（反向）
		执行完毕时的状态：backwards（默认值。最开始的状态   forwards（终止时的状态）
	6.拆分写法                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       相关属性;
			animation-name                      动画名称
			animation-duration                  动画时长
			animation-delay       				延迟时间
			forwards：							最后一帧状态
			animation-fil1-mode 			动画执行完毕时状态 backwards：第一帧状态
			animation-timing-function 			速度曲线 steps(数字)：逐帧动画
			animation-iteration-count 			重复次数 infinite为无限循环
			animation-direction 				动画执行方向 alternate为反向
			animation-play-state 			暂停动画 paused为暂停，通常配合：hover使用
#flex布局
	1.作用：基于flex精确控制块级盒子的布局方式，避免浮动布局中脱离标准流的现象
	2.设置方式：父元素（亲爹，不能是爷爷啥的）添加 display：flex，子元素可以自动的挤压或者拉伸
	3.组成：
		1.整体父元素大盒子（弹性容器）
		2.内部子元素小盒子（弹性盒子）
		3.x轴（主轴）
		4.y轴（侧轴或者交叉轴）
##flex布局——主轴对齐方式
	1.属性：justify-content
	2.取值：
		flex-start                         默认值，起点开始依次排列
		flex-end                              终点开始依次排列
		//后面四个常用
		center                                 沿主轴居中排列
		space-around                弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子两侧
		space-between               弹性盒子沿主轴均匀排列，空白间距均分在相邻盒子之间
		space-evenly                弹性盒子沿主轴均匀排列，弹性盒子与容器之间间距相等
##flex布局——侧轴对齐方式
	1.属性： 
			aligin-items（添加到弹性容器（父元素）里，控制所有的子盒子）
			aligin-self（添加到弹性盒子（子元素）里，单独控制一个盒子）
	2.取值：
			flex-start 						默认值，起点开始依次排列
			flex-end 							终点开始依次排列
			//后两个较为常用
			center 								沿侧轴居中排列
			stretch 					默认值，弹性盒子沿着主轴线被拉伸至铺满容器
##felx布局——修改主轴方向
	1.属性：flex-direction
	2.取值：
			row                       行 ，默认值，水平
			column            主要：    列，垂直
			row-reverse               行，从左到右
			column-reverse            列，从下到上
##felx布局——弹性盒子换行
	1.介绍
		因为用了felx布局，所有的盒子变成弹性盒子，当子盒子可以被父盒子容纳，所设定的盒子宽度照常。
		当子盒子不能被父盒子在一行之中容纳时，所设定的盒子宽高失效，
		会根据父盒子的宽度对子盒子进行弹性收缩，直到父盒子可以完全在一行中容纳子盒子。
	2.属性：flex-wrap
	3.取值：
			nowrap          默认，不换行
			wrap               换行（顺着换行，第一行在上方，第二行在下方）
			wrap-reverse		换行（逆着换行，第一行在下方，第二行在上方）
##felx布局——调整行对齐的方式
	1.介绍：调整上一行与下一行之间的行间距
	2.属性：align-content
	3.取值：与justify-content取值大致相同 

#以上是给父元素设计的，以下是给子元素设计的
##felx布局——order
	order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。也就是该属性决定子元素在容器中的排序位置。
##felx布局——flex-grow
	flex-grow属性定义项目的放大比例，默认为0。
	设置flex-grow会将父容器的剩余空间占满。
##felx布局——flex-shrink
	和flex-grow属性相反，flex-shrink属性是控制元素缩小比例。默认为1，即如果空间不足，该项目将缩小。
##felx布局——flex-basis
	flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
##felx布局——flex
	flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
##felx布局——align-self
	align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

	..该属性可能取6个值，除了auto，其他都与align-items属性完全一致。
#移动端适配
##rem
	1.相对单位，1rem=HTML标签的也就是根标签的字号；
			eg:
				html{
					font-size:32px;
				}
		    ...1 rem = 32px;

	2.为适应不同的移动端窗口也就是不同的屏幕大小。
		.需要使用媒体查询
	3.@media（wodth：375px）{
			HTML {
			font-size：40px；
			}
	 } 
###了解了解less也就是css预处理编译器                                                                                                                                     
#BootStrap-栅格系统
	.栅格化是指将整个网页的宽度分成若干等份
	.BootStrap3默认将网页分成12等份
			           超小屏幕 		小屏幕		 中等屏幕 		大屏幕

			响应断点 	<768px 		>=768px 	  >=992px 		>=1200px

			别名 		xs 			 sm 			md 			  lg

			容器宽度 	100% 		750px 			970px 		1170px

			类前缀 		col-xs-* 	col-sm-* 	  col-md-* 		col-lg-*

			列数         12 			 12 			12			  12

			列间隙  		30px		 30px 			30px 		30px
	eg：
		<div class="col-lg-3 col-md-6 col-sm-12">2</div>  //一行四个，两个 ， 一个 
        <div class="col-lg-3 col-md-6 col-sm-12">3</div> 
        <div class="col-lg-3 col-md-6 col-sm-12">4</div>
        <div class="col-lg-3 col-md-6 col-sm-12">5</div>
	注意点：
		1. container   版心   会有一个左右15px的padding

		2. row        会有一个左右-15px的padding
			
			当用container时，如果不想要那个默认的15pxpadding，可以再写一个盒子定类名为row抵消掉。也可以自己再次定义padding为0  ，覆盖了。
