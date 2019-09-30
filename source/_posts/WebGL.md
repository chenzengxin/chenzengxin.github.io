---
title: "WebGL"
author: "Chenzengxin"
date: 2019.09.30
---


### 1、WebGL基本原理
    WebGL 本质上是基于光栅化的 API，WebGL 只关注投影矩阵的坐标和投影矩阵的颜色，可以使用“着色器”来完成上述任务。顶点着色器可以提供投影矩阵的坐标，片段着色器可以提供投影矩阵的颜色。投影矩阵的坐标的范围始终是从 -1 到 1。WebGL基于图元（三角形、点、线）进行图像绘制

``` javascript
// Get A WebGL context
var canvas = document.getElementById("canvas");
var gl = canvas.getContext("experimental-webgl");//获取绘图上下文
```

### 2、viewport 视图窗口
    视图窗口定义了绘制区域的边界。通过绘图上下文可以设置绘制窗口

```javascript
function initViewport(gl,canvas){
    gl.viewport(0,0,canvas.width,canvas.height);
}
```

### 3、缓冲、缓冲数组和类型化数组
    图元以数组的形式存储数据（buffer）


``` javascript
// 构建用于绘制的正方形顶点数据
function createSquare(gl) { 
    var vertexBuffer; 
    vertexBuffer = gl.createBuffer(); 
    gl.bindBuffer(gl.ARRAY_BUFFER, vertexBuffer); 
    var verts = [ 
         .5,  .5, 0.0, 
        -.5,  .5, 0.0, 
         .5, -.5, 0.0, 
        -.5, -.5, 0.0 
    ]; 
    gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(verts), gl.STATIC_DRAW); 
    var square = {buffer:vertexBuffer, vertSize:3, nVerts:4,primtype:gl.TRIANGLE_STRIP}; 
    return square; 
}
```

### 4、矩阵
    在绘制之前，我们首先要创建一对矩阵。第一个矩阵用于描述正方形在3D坐标系统中的位置（模型-视图矩阵，ModelView matrix），第二个矩阵称为投影矩阵（Projection matrix），着色器使用它来执行从3D空间坐标到2D视口绘制空间坐标的转换。

```javascript
var projectionMatrix, modelViewMatrix; 
function initMatrices(canvas) 
{ 
    // 创建一个模型-视图矩阵，包含一个位于（0,0,-3.333）的相机
    modelViewMatrix = glMatrix.mat4.create(); 
    glMatrix.mat4.translate(modelViewMatrix, modelViewMatrix, [0, 0, -3.333]); 
    // 创建一个45度角视野的投影矩阵
    projectionMatrix = glMatrix.mat4.create(); 
    glMatrix.mat4.perspective(projectionMatrix, Math.PI / 4, canvas.width / canvas.height, 1, 10000); 
}
```



### 着色器
    着色器通常由两个部分组成：顶点着色器（vertex shader）和片段着色器（fragment shader，又称pixel shader，像素着色器），顶点着色器负责将物体的坐标转换为2D显示区域的坐标；片段着色器负责基于颜色、纹理、光照、材质等数值计算转换顶点像素的最终颜色，
    
``` javascript
//创建着色器
function createShader(gl, str, type) { 
    var shader; 
    if (type == "fragment") { 
        shader = gl.createShader(gl.FRAGMENT_SHADER); 
    } else if (type == "vertex") { 
        shader = gl.createShader(gl.VERTEX_SHADER); 
    } else { 
        return null; 
    } 
    gl.shaderSource(shader, str); 
    gl.compileShader(shader); 
    if (!gl.getShaderParameter(shader, gl.COMPILE_STATUS)) { 
        alert(gl.getShaderInfoLog(shader)); 
        return null; 
    } 
    return shader; 
}

var vertexShaderSource = 
    "attribute vec3 vertexPos;\n" + 
    "uniform mat4 modelViewMatrix;\n" +
    "uniform mat4 projectionMatrix;\n" + 
    "void main(void) {\n" + 
    "   //返回经过投影和变换的顶点值\n" + 
    "   gl_Position = projectionMatrix * modelViewMatrix * \n" + 
    "   vec4(vertexPos, 1.0);\n" + 
    "}\n"; 

var fragmentShaderSource = 
    "void main(void) {\n" + 
    "   //返回像素点的颜色：输出白色\n"+ 
    "   gl_FragColor = vec4(1.0, 1.0, 1.0, 1.0);\n" + 
    "}\n";

var shaderProgram, shaderVertexPositionAttribute,
    shaderProjectionMatrixUniform,
    shaderModelViewMatrixUniform;
function initShader(gl) { 
    // 加载并编译片段和顶点着色器
    var fragmentShader = createShader(gl, fragmentShaderSource, "fragment"); 
    var vertexShader = createShader(gl, vertexShaderSource, "vertex"); 
    // 将着色器链接到一个程序中
    shaderProgram = gl.createProgram(); 
    gl.attachShader(shaderProgram, vertexShader); 
    gl.attachShader(shaderProgram, fragmentShader); 
    gl.linkProgram(shaderProgram); 
    // 获取指向着色器参数的指针
    shaderVertexPositionAttribute = gl.getAttribLocation(shaderProgram, "vertexPos");
    gl.enableVertexAttribArray(shaderVertexPositionAttribute); 
    shaderProjectionMatrixUniform = 
    gl.getUniformLocation(shaderProgram, "projectionMatrix"); 
    shaderModelViewMatrixUniform = 
    gl.getUniformLocation(shaderProgram, "modelViewMatrix");

    if (!gl.getProgramParameter(shaderProgram, 
        gl.LINK_STATUS)) { 
        alert("Could not initialise shaders"); 
    }
}
```


### 绘制图元

``` javascript
function draw(gl, obj) { 
    // 清空背景（使用黑色填充）
    gl.clearColor(0.0, 0.0, 0.0, 1.0); 
    gl.clear(gl.COLOR_BUFFER_BIT); 
    // 设置待绘制的顶点缓冲
    gl.bindBuffer(gl.ARRAY_BUFFER, obj.buffer); 
    // 设置待用的着色器
    gl.useProgram(shaderProgram);
    // 建立着色器参数之间的关联：顶点和投影/模型矩阵
    gl.vertexAttribPointer(shaderVertexPositionAttribute, 
    obj.vertSize, gl.FLOAT, false, 0, 0); 
    gl.uniformMatrix4fv(shaderProjectionMatrixUniform, false, 
    projectionMatrix); 
    gl.uniformMatrix4fv(shaderModelViewMatrixUniform, false, 
    modelViewMatrix);
    // 绘制物体
    gl.drawArrays(obj.primtype, 0, obj.nVerts); 
}
 ```

### 展示效果

 ![](/img/webgl.png "title")