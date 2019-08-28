---
title: "C# Reflection"
author: "Chenzengxin"
date: 2019.08.27
---


## 定义
- 审查元数据并收集关於它的类型信息的能力,元数据(编辑后的基本数据单元)就是一大堆表，编译器会创建一个类定义表，一个字段定义表，一个方法定义表等,System.Reflection命名空间包含的几个类，允许你反射(解析)这些元数据的代码
---

## Assembly 结构

- Assembly由以下几部分组成：
##### Assembly Manifest
+ 包含assembly的数据结构的细节。下面列出了Manifest中的主要信息：
  - Assembly名字
  - 版本号
  - Assembly运行的机器的操作系统和处理器
  - Assembly中包含的文件列表
  - 所有assembly依赖的信息
- Strong Name信息
##### Type Metadata
+ 包含assembly中允许的类型数据。（前面提到过，class, interface，member, property等）
---

## 获取Assembly：

- Assembly.Load
- Assembly.LoadFile
- Assembly.LoadFrom
- Type对象的Assembly方法

## 使用反射获取类型

- 获取类型有两种方式：
  - 利用实例对象去获取它的类型（通过调用System.Object上声明的方法GetType来获取实例对象的类型对象）
  - 通过Type.GetType以及Assembly.GetType方法

	##### Type:
	- 表示类型声明：类类型、接口类型、数组类型、值类型、枚举类型、类型参数、泛型类型定义，以及开放或封闭构造的泛型类型。
	
    - **官方示例**
	``` C sharp
	using System;
	using System.Reflection;
	class Example
	{
		static void Main()
		{
			Type t = typeof(String);
			MethodInfo substr = t.GetMethod("Substring", 
				new Type[] { typeof(int), typeof(int) });
			Object result = 
				substr.Invoke("Hello, World!", new Object[] { 7, 5 });
			Console.WriteLine("{0} returned \"{1}\".", substr, result);
		}
	}
	/* This code example produces the following output:
	System.String Substring(Int32, Int32) returned "World".
	*/
	```

## 动态创建对象
##### Assembly.CreateInstance:
``` C sharp
    object[] param = new object[] { true,(byte)1,(short)2,'A',3,4L, _float, 6.0,"i'm a string" };
    var instance1 = assembly.CreateInstance("MyLib.ClassA", false, BindingFlags.Default, null, param, null, null);
    var instance2 = assembly.CreateInstance("MyLib.ClassA", false, BindingFlags.Default, null, null, null, null);
```
##### Activator.CreateInstance:
``` C sharp
    var instance3 = Activator.CreateInstance(types[0], param);
    var instance4 = Activator.CreateInstance(types[0], null);
```

## 动态调用对象方法
	Type对象的 InvokeMember方法 
	MethodInfo对象的Invoke方法
``` C sharp
    var result = types[0].InvokeMember("ToString", BindingFlags.InvokeMethod, null, instance1, null);
    Debug.Log(result);
    Debug.Log(instance2.GetType().GetMethod("FuncA").Invoke(instance2,null));
    Debug.Log(instance2.GetType().GetMethod("FuncB").Invoke(instance2, new object[] {"i'm args" }));
```


## CLASS 
``` C sharp
namespace MyLib
{
    public class ClassA
    {
        private bool _bool;

        private byte _byte;

        private short _short;

        private char _char;

        private int _int;

        private long _long;

        private float _float;

        private double _double;

        private string _string;


        public ClassA() {
            
        }
        
        public ClassA(bool _bool, byte _byte, short _short, char _char, int _int, long _long, float _float, double _double, string _string)
        {
            this._bool = _bool;
            this._byte = _byte;
            this._short = _short;
            this._char = _char;
            this._int = _int;
            this._long = _long;
            this._float = _float;
            this._double = _double;
            this._string = _string;
        }

        public string FuncA() {
            return "FuncA";
        }

        public string FuncB(string args) {
            return "FuncB，args = " + args;
        }

        public override string ToString() {
            return String.Format("my prop is {0},{1},{2},{3},{4},{5},{6},{7},{8}", this._bool, this._byte, this._short, this._char, this._int, this._long, this._float, this._double, this._string);
        }
    }
}
```