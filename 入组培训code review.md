---
title: 入组培训code review
tags: 
  - c/c++
categories: c/c++
---

* 今天入组培训又被超哥吊打了，code review给我挑了很多毛病，对此我是服气的，感谢超哥和佳哥。下面具体说说：
	* 文件的组织：
		* src: .c makefile
		* bin: .so .inf makefile
		* conf: .conf
		* 值得一提的是，bin中的makefile是假的makefile，他的作用就是
	* 不要重复造轮子，读配置文件可以用MESA load prof这个公共库。写日志可以用MESA handle logger这个库(下划线打不出来)。
	* 用CJSON,比较专业。
	* 另外，自己写读配置文件的时候，要写的优雅一点，每需要一个配置就去扫描整个配置文件一遍，这样虽然效率低，但是很整齐。
	* 不要随便拆成两个文件，完全不相关的函数才拆成两个文件。
	* 超过20行的字符串处理就要考虑glic中自带的库。具体见[c语言基础,长期更新](https://leocui.github.io/2016/10/20/c%E8%AF%AD%E8%A8%80%E5%9F%BA%E7%A1%80%EF%BC%8C%E9%95%BF%E6%9C%9F%E6%9B%B4%E6%96%B0/>)
	* 输出错误信息时要输出具体的系统的错误(errno, strerror(errno))
	* malloc和free最好成对出现，即在同一个函数中
	* 每个.c都对应一个头文件，不是所有的声明都要放到头文件中。放到头文件中是要给别人用的，也就是说如果某个函数只有本文件用，那么就不用放到头文件中。
	* cpp代码要给c用的时候，用extern 'C'，具体见[c语言基础,长期更新](https://leocui.github.io/2016/10/20/c%E8%AF%AD%E8%A8%80%E5%9F%BA%E7%A1%80%EF%BC%8C%E9%95%BF%E6%9C%9F%E6%9B%B4%E6%96%B0/>)
	* 多用assert，表示你很确定这个情况不会发生，出现就死。
	* free后要把指针置为NULL,养成习惯。
	* 同一个全局变量不用在两个文件中重复声明，加一个extern就行了。具体见[c语言基础,长期更新](https://leocui.github.io/2016/10/20/c%E8%AF%AD%E8%A8%80%E5%9F%BA%E7%A1%80%EF%BC%8C%E9%95%BF%E6%9C%9F%E6%9B%B4%E6%96%B0/>)
	* 