---
title: "CSS一键换肤"
date: 2023-03-07T16:29:24+08:00
draft: true
images:
---

	["red", "blue", "green"].forEach(v => {
	const btn = document.getElementById(`${v}-theme-btn`);
	    btn.addEventListener("click", () => document.body.style.setProperty("--bg-color", v));
	});
	
### 使用CSS变量的好处
* 减少样式代码的重复性
* 增加样式代码的扩展性
* 提高样式代码的灵活性
* 增多一种css与js的通讯方式
* 不用深层次遍历dom改变某个样式
