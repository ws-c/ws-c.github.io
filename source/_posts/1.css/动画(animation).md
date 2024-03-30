---
title: css-动画
tags: [css]
categories: [css]
---
1.定义

~~~html
//第一种方法 只有起始帧和结束帧2个动作,中间自动补帧
@keyframes action{
	from{
		
	}//可不写
	to{
	
	}
}
//第二种方法	可以定义起始帧和结束帧持续时间中多个动作状态
@keyframes action{
	0%{	

	}
	50%{	

	}
	100%{
	
	}
}
~~~

 2.调用

![image-20220329191411724](https://s2.loli.net/2022/05/17/kxAthImrF1oOKCS.png)

infinite: 无线循环动画

alternate: 反向,来回执行动画   

forwards: 动画结束停留在最后一帧状态

linear: 动画匀速运行

**暂停动画**

~~~html
animation-play-state: paused; 
~~~

**逐帧动画 (CSS默认为补间动画)**

~~~html
animation: steps()
~~~

**多组动画使用逗号隔开**

~~~html
 animation: action,action2
~~~

动画效果脱标，不影响布局
