# SVPWM原理、实现与数学表达
本文是笔者对自己《现代电力电子技术》课程的作业进行了修改、整合和补充得到的。虽然耗费了许多时间和精力，但是受限于个人知识水平和能力，文章中肯定会出现很多遗漏和错误。所以也诚心地邀请读者进行批评指正。

写作本文的动机主要是出于自己对LaTeX排版的兴趣，其次也为了对自己学过的东西做一些总结与记录，方便自己日后的查找和学习。

本文中的所有图片都是笔者自己绘制的，主要使用的工具是LaTeX的TikZ宏包和Python的matplotlib模块。TikZ绘图的源码已经上传，matplotlib绘制的部分图片因为效果并不是很好，因此并未上传此部分源码，未来将考虑用TikZ重新绘制。

## 下载方法
GitHub地址: https://github.com/Li-Huakang/SVPWM

完整下载: git clone https://github.com/Li-Huakang/SVPWM.git

PDF下载: https://github.com/Li-Huakang/SVPWM/raw/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE.pdf

## 预览
![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_01.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_02.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_03.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_04.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_05.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_06.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_07.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_08.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_09.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_10.png)

![image](https://github.com/Li-Huakang/SVPWM/blob/master/SVPWM%20%E5%8E%9F%E7%90%86%E3%80%81%E5%AE%9E%E7%8E%B0%E4%B8%8E%E6%95%B0%E5%AD%A6%E8%A1%A8%E8%BE%BE_%E9%A1%B5%E9%9D%A2_11.png)

