---
title: jQuery插件开发
date: 2018-03-26 01:05:53
tags: jQuery
---

**插件分类**

- 封装对象方法 
- 封装全局函数
- 选择器插件

**插件要点**

1. 命名格式jquery.myplugin.js ，防止混淆。
2. 所有对象方法附加到$.fn对象，所有全局函数附加到jQuery对象。
3. 插件内部的this指向的是jQuery对象而不是DOM元素。
4. 可以用this.each来遍历所有元素。
5. 所有方法都应当以分号结尾甚至分号开头，防止压缩出错。
6. 插件需要返回一个jQuery对象，方便进行可链式操作。除非插件是为了返回获取量，例如字符串或数组等。
7. 在插件内部正确使用$。

**代码重构**

- 缓存this
- 缺省参数
- 事件类型
- 回调函数
- 拆分函数
- 注释和编码规范

**代码示例**
	
	//封装全局函数
	;(function($) {
		$.extend({
			pluginA: function() {
				console.log('pluginA');
			}		
		});
		$.pluginB = function() {
			console.log('pluginB');
		}
	})(jQuery);

	$.pluginA(); //'pluginA'
	$.pluginB(); //'pluginB'
	
	//封装对象方法
	;(function($) {
		$.fn.extend({
			pluginC: function(option) {
				var opts = $.extend({
					even_trigger_type: 'click',
					callback: function(e) {
						
					}
				}, option || {});
				return this.each(function() {
					var $this = $(this);
					/*
						私有函数
					*/					
					function init() {
						// 调用回调函数			
						calback();
					}					
					/*
						私有函数
					*/
					function bind() {
					}					
					//调用私有函数
					if(true) {
						init();
					}			
					
					
				})
			}
		});
	})(jQuery);

	$(selector).pluginC({
		even_trigger_type: 'mouserover',
		callback: function(e) {
			console.log(e);
		}
	}); 
	

	//选择器插件
	<p san='100' style="display: inline;">san100</p>

	;(function($) {
    	$.extend($.expr[':'], {
        	san: function(e) {
            	return $(e).attr('san');
        	},
        	inline: function(e) {
            	return $(e).css('display') === 'inline';
        	}
    	})
	})(jQuery);
	
	$('p:san').css('color', '#fff');
	$('p:inline').css('background', '#000');
		

**参考资料**

- [锋利的jquery第二版](https://book.douban.com/subject/10792216/)[书中的jQuery版本太低，案例中between选择器只能通过修改源码实现。]
- [jquery插件开发全指南](https://blog.csdn.net/ul646691993/article/details/52214101)[暴露参数和部分函数，方便他人协作开发。]
- [jQuery插件开发精品教程，让你的jQuery提升一个台阶](http://www.cnblogs.com/Wayou/p/jquery_plugin_tutorial.html)[插件压缩和发布到GitHub。]
- [How to write jQuery plugin?](http://i5ting.github.io/How-to-write-jQuery-plugin/build/jquery.plugin.html#10406)[使用前端自动化工具压缩和发布到jQuery plugin官网。]