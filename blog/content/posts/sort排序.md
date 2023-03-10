---
title: "Sort排序"
date: 2023-03-07T16:39:32+08:00
draft: true
---

### Sort
***为了按照某个方式进行排序，必须给sort方法传递一个比较函数，该函数决定了它的两个参数在排好序的数组中的先后顺序。假设第一个参数应该在前，比较函数应该返回一个小于0的数值，假如第一个参数应该在后，函数应该返回一个大于0的数值，如果两个数值相等，那么他们的顺序无关紧要，此时函数应该返回0。***

这是js权威指南中对数组sort方法的描述，红包书中的描述与此类似，并给出了函数的例子：

		function compare(value1, value2) {
	    if (value 1 < value2) {
	        return -1;
	    } else if (value1 > value2) {
	        return 1;
	    } else {
	        return 0;
	    }
	}
只要将compare函数作为参数传递给sort方法即可，如下所示：

	var values = [0,1,5,10,15];

	values.sort(compare); // 0,1,5,10,15
	
	这里的解释是：如果第一个参数应该位于第二个参数之前，则返回一个负数，如果第一个参数应该位于第二个参数之后则返回一个正数。

所以其实这个函数的规则定义是一个从结果来推导条件的过程，函数的逻辑已经定义好了：无论你要比较什么，我的规则比较后的结果就是：如果第一个参数应该位于第二个参数之前，则返回一个负数，如果第一个参数应该位于第二个参数之后则返回一个正数，这里的a,b的理解就是待排序数组中的任意两个元素，没有什么顺序的规定，也不是什么一定相邻的两个元素，就是任意两个元素。我们使用sort来进行排序的时候实际是根据它比较结果的规则来去写我们的比较条件的，也就是if表达式，告诉它什么时候返回-1，什么时候返回1，也就是告诉它深呢时候把a排前面，什么时候把a排后面。这个规则要写完整，不能只写一半只告诉它什么情况下把a排在前面，其他情况不写，它就不知怎么排了。

简单记忆： a - b 是生序 b - a 是降序，其实是一中“偷懒”的记忆方式，可以用来快速的进行排序，但是也要记得sort函数最原始的规则：如果第一个参数应该位于第二个参数之前，则返回一个负数，如果第一个参数应该位于第二个参数之后则返回一个正数。

如果忘记了sort方法，可以回去复习LeeCod第1122题：[https://leetcode-cn.com/problems/relative-sort-array/solution/sortfang-fa-zui-jing-jian-fang-shi-by-storm-24/
](https://leetcode-cn.com/problems/relative-sort-array/solution/sortfang-fa-zui-jing-jian-fang-shi-by-storm-24/
)
