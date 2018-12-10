# 			Typora常用快捷键

## 对文字的特殊标注

### 标题

```javascript
# 一阶标题  或者快捷键Ctrl+1
## 二阶标题 或者快捷键Ctrl+2
### 三阶标题    或者快捷键Ctrl+3
#### 四阶标题   或者快捷键Ctrl+4
##### 五阶标题  或者快捷键Ctrl+5
###### 六阶标题 或者快捷键Ctrl+6
```

### 下划线

```javascript
<u>下划线的内容</u> 或按快捷键Ctrl+U
```

<u>下划线的内容</u>

### 字体加粗

```
**加粗内容**    或按快捷键Ctrl+B
```

**加粗字体**

### 斜体

```
*倾斜内容*  或按快捷键Ctrl+I
```

*斜体内容*

### 删除线

```
~~删除线的内容~~  或按快捷键Alt+Shift+5
```

~~删除线内容~~

### 文字高亮

```
==我是最重要的==
```

==我是最重要的== 

### 角标

```
x^2^    H~2~O
```

x^2^ H~2~O 

### 文本居中

```
<center>这是要居中的文本内容</center>
PS：Typora目前并不会直接预览居中效果——相应的效果只有输出文本的时候才会显现。
```

<center>居中内容</center>

### list  有序

```
数字+英文小数点(.)+空格
```

1. 策划目标
2. 战前准备
3. 开始行动

### 无序

```
+ 、- 、* 创建无序列，任意数字开始+空格创建有序列表
```

+ 猪
+ 狗
+ 马

### Todolist

```
- [ ] 参加会议
- [x] 中超足球赛
```

- [1] 会议
- [2] 足球赛

### Table

```
快捷键Ctrl+T弹出对话框
```

| 国籍 | 省份 | 市区 |
| :--: | :--: | :--: |
| 中国 | 湖南 | 株洲 |

### 分割线

```
***+回车  
---+回车  
```

---

***

### 插入

#### 图片

```
![图片内容](http://t10.baidu.com/it/u=1069603383,3074552113&fm=170&s=771B15C75C12D8D61C3C69FB0300501F&w=640&h=426&img.JPEG) 也可使用快捷键Ctrl+K，
PS：也可将图片直接拖拽进来，自动生成链接
```

![https://www.baidu.com/img/bd_logo1.png](https://www.baidu.com/img/bd_logo1.png)

#### 链接

1. ##### 内行式；

   ```
   [百度一下，你就知道](https://www.baidu.com/)
   ```

   [百度一下，你就知道](https://www.baidu.com)

   ![1541950369758](C:\Users\LIZHIM~1\AppData\Local\Temp\1541950369758.png)

2. ##### 快速链接

   ```
   <http://blog.csdn.net/wwwfrank2>
   PS：按住Ctrl点击链接可直接打开。
   ```

   <https://blog.csdn.net/wwwfrank2>

3. ##### 参考式

   ```
   [百度一下，你就知道][]https://www.baidu.com/  # 第二个括号内可任意填写(不显)
   ```

   [][][百度一下，你就知道][]https://www.baidu.com

### 数学公式（简）

```
Typora支持加入用LaTeX写成的数学公式，并且在软件界面下用MathJax直接渲染。
```

#### 分为两种：

- 行内公式（inline math），可以在偏好设置中单独打开，由一个美元符号将公式围起来；name=将公式围起来；name=\prod \frac{1}{i^2}$ 
- 行外公式，直接按**Ctrl+Shift+M**；(双$+回车也可做到) 

$$
name= \prod \frac{1}{i^2}$
$$

### 代码

```
`PHP`是世界上最好的语言  
#此为单行代码，也可用快捷键Ctrl+Shift+
```

`PHP`是世界上最好的语言 

下为多行：

```markdown
​```markdown
```

```markdownprinf("hello world")
print("hello world");
```

``````
​```
``````

```
printf(hello world);
```

### 其余

#### 引用

```
>+ 空格 或按快捷键Ctrl+Shift+Q
```

> 
>
> 引用内容

### 注释

```
要添加注释的文字
这是我们的标号[^1]
[^1]:标号的含义
```

这是我们的符号[^1]

### 表情

```
:单词:
```

:smile::cry::2nd_place_medal:

### 目录

```
[TOC]
```

[TOC]

### Typora 快捷键整合

|    快捷键    |        作用        |    快捷键    |      作用      |
| :----------: | :----------------: | :----------: | :------------: |
|    Ctrl+1    |      一阶标题      |    Ctrl+B    |    字体加粗    |
|    Ctrl+2    |      二阶标题      |    Ctrl+I    |    字体倾斜    |
|    Ctrl+3    |      三阶标题      |    Ctrl+U    |     下划线     |
|    Ctrl+4    |      四阶标题      |  Ctrl+Home   | 返回Typora顶部 |
|    Ctrl+5    |      五阶标题      |   Ctrl+End   | 返回Typora底部 |
|    Ctrl+6    |      六阶标题      |    Ctrl+T    |    创建表格    |
|    Ctrl+L    |     选中某句话     |    Ctrl+K    |   创建超链接   |
|    Ctrl+D    |    选中某个单词    |    Ctrl+F    |      搜索      |
|    Ctrl+E    | 选中相同格式的文字 |    Ctrl+H    |   搜索并替换   |
| Alt+Shift+5  |       删除线       | Ctrl+Shift+I |    插入图片    |
| Ctrl+Shift+M |       公式块       | Ctrl+Shift+Q |      引用      |

```
注：一些实体符号需要在实体符号之前加”\”才能够显示
```

