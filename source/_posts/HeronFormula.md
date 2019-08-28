---
title: "海伦公式"
author: "Chenzengxin"
date: 2019.08.28
---


## 海伦公式
- 背景：相传这个公式最早是由古希腊数学家阿基米德得出的，而因为这个公式最早出现在海伦的著作《测地术》中，所以被称为海伦公式。中国秦九韶也得出了类似的公式，称三斜求积术。（百度百科）
- 表达式：S=√p(p-a)(p-b)(p-c)
- 描述
  - 假设在平面内，有一个三角形，边长分别为a、b、c，三角形的面积S可由以下公式求得：
    > p = (a+b+c)/2 <br/>
    > p 为半周长 <br/>
    > S = sqrt(p(p-a)(p-b)(p-c))
- 求点到线的最短距离
``` C sharp
double dis = 0;
double a, b, c;
a = DistancePt2Pt(pt0, pt1);// 线段的长度
b = DistancePt2Pt(pt0, pt);// Pt1到点的距离
c = DistancePt2Pt(pt1, pt);// Pt2到点的距离
#region 两点屏幕距离
public double DistancePt2Pt(Vector3 pt0, Vector3 pt1)
{
    return Math.Sqrt(Math.Pow((pt0.X - pt1.X), 2) + Math.Pow((pt0.Y - pt1.Y), 2));
}
#endregion
double p = (a + b + c) / 2;// 半周长
double s = Math.Sqrt(p * (p - a) * (p - b) * (p - c));// 海伦公式求面积
dis = 2 * s / a;// 返回点到线的距离（利用三角形面积公式求高）
```
