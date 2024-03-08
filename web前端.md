# HTML

## 1.常用标签

- 标题标签：h1~h6
  - 一级标题一般只用一次
  - 其余等级没有使用次数限制
  
- 段落标签：p（双标签）
  - 显示效果为独占一行
  
- 换行和水平线标签：br/hr

- 文本格式化标签：
  - 加粗：<strong>/<b>
  - 倾斜：<em>/<i>
  - 下划线：<ins>/<u>
  - 删除线：<del>/<s>
  
- 图像标签：<img src="图像位置">
  - 图片标签的属性：alt替换文本：图片无法显示是显示文字/title提示文本：鼠标悬停在图片上面现实的文字
  - width：设置图片的宽度
  - height：设置图片的高度
  
- 超链接标签：<a href="跳转的网址链接">显示的文字<a>
  - 属性target="_blank"作用是出现一个新窗口
  - href="#"作用是表示空链接
  
- 音频标签：<audio src=""></audio>
  - controls:显示音频控制面板
  - loop：循环播放
  - autoplay：自动播放，一般禁用
  - 属性名和属性值一样可以简写为一个单词
  
- 视频标签：<video src=""></video>
  - controls:显示音频控制面板
  - loop：循环播放
  - autoplay：自动播放，一般禁用
  - muted：静音播放 
  
- 列表标签

  - 无序列表：<ul> <li>每级标签内容</li> </ul>

    - ul标签里面只能由li标签
    - li把标签里面可以包含任意东西

  - 有序列表：<ol>

    ​    <li>第一有序列表</li>

    ​    <li>第二有序列表</li>

      </ol>

  - 定义列表： 

  - < dl>

    
    ​    <dt></dt>
    
    ​    <dd></dd>
    
      </dl>

- 表格标签：<table border=""><tr><td></td></tr></table>

- 合并单元格：

  - 跨行合并保留最上面的单元格，添加属性rowspan
  - 跨列合并保留最左单元格，添加属性colspan
  - 属性值为数字，代表合并的单元格数量

## 2.表单

### 2.1input标签

| type属性值 | 说明                     |
| ---------- | ------------------------ |
| text       | 文本框，用于输入单行文本 |
| password   | 密码框                   |
| radio      | 单选框                   |
| checkbox   | 多选框                   |
| file       | 上传文件                 |

- placeholder属性：默认提示信息
- name属性：和radio属性一起使用，当作一个标签使选项为一组使其只能选中一个 
- checked属性：和radio或checkbox属性一起使用，默认选中某个选项
- multiple属性：和file属性一起使用，表示可以上传多个文件

### 2.2下拉菜单

- 标签<select></select>
- 内嵌标签<option>选项内容</option>
- selected属性：默认选中某个选项

### 2.3文本域

- < textarea>   < /textarea>

### 2.4label标签

**作用增大点击范围**

- label标签只包裹内容，不包裹控件，设置label标签的for属性和表单空间的id属性值相同
- 例如：<input type="radio" id ="man">

<label for="man"> 男</label>



### 2.5按钮标签

- < button type="">按钮</button>

- | type属性值 | 说明                                           |
  | ---------- | ---------------------------------------------- |
  | submit     | 提交按钮点击后可以提交数据到后台               |
  | reset      | 重置按钮，点击后将标案控件恢复默认值           |
  | button     | 普通按钮，默认没有功能，一般配合JavaScript使用 |

- type属性值为reset时需要使用 **form标签表示表单区域**

### 2.6无语义布局标签

**用于布局网页，划分网页区域，摆放内容**

- div：独占一行，换行
- span：不换行

### 2.7实体字符

- 空格：&nbsp
- <:&lt
- 大于号：&gt

# CSS层叠样式表

## 1.基础选择器

- 1.1标签选择器

使用标签名作为选择器，选中同名标签设置相同的样式

无法差异化同名标签的效果

- 1.2类选择器

在<head>标签里写，<style>标签里定义选择器类名例如：

.red{

​		color:red

}

然后在所需改变样的的标签加class属性例如：

< p class="red">nihao</p>

nihao这几个字母就会变成红色

如果需要添加多个特性，class的属性值之间使用空格隔开

- 1.3id选择器

使用方法和类选择器差不多

定义格式为：

#red{

​		color:red

}

< div id="red">你好</div>

**同一个id选择器在一个页面只能使用一次**

- 通配符选择器

作用是查找所有的标签，设置相同的样式

所有标签统一样式

## 2.字体属性

格式：

.green

​    {

​      width: 100px;

​      height: 100px;

​      background-color: green;

​    }

< div class="green">原神启动< / div>

会出现一个长一百宽一百的绿色格子

- font-size:文字尺寸
- font-weight:控制字体粗细
- font-style:控制字体是否倾斜，两种属性值
  - normal：不倾斜
  - italic：倾斜
- 复合属性格式：

font: font-style  font-weight  font-size/line-height  font-family

各个属性之间使用空格隔开，并且顺序不能颠倒

有些属性可以省略，但是font-size和font-family不能省略

## 3.CSS文本属性

### 3.1对齐文本

- text-align:用于设置元素内文本内容的水平对齐方式
  - center：居中对齐
  - right：右对齐
  - 默认是左对齐

### 3.2装饰文本

- text-decoration:属性规定添加到文本的修饰，可以给文本添加下划线，删除线，上划线等
- 属性值
  - none：默认没有装饰线
  - underline：下划线，链接a自带下划线
  - overline：上划线，几乎不用
  - line-through：删除线，几乎不用

### 3.3文本缩进

- text-indent:属性用于指定文本第一行的缩进，通常是指段落首行缩进
- 语法格式：div{ text-indent:20px; }
- em单位：是一个相对单位，是当前像素font-size一个文字的大小，如果是2em就是当前两个文字大小缩进

### 3.4行间距

- text-height:设置行间的距离，可以控制行与行之间的距离
- line-height:设置行间距，两种写法
  - 数字+px
  - 数字（当前标签font-size 的倍数）

## 4.CSS引入方式

### 4.1内部样式表

内部样式(内嵌样式表) 时写道html页面内部，时将所有的css代码抽取出来，单独放到一个<style>标签中

理论上可以放在任何地方但是一般放在<head>标签里

### 4.2行内样式表

- 在元素标签内部的style属性设定CSS样式，适用于修改简单的样式
- 语法格式：< div style="color: red; font-size: 12px;">谢钦学css</div>
- 只能控制当前标签



### 4.3外部样式表（使用最多）

单独写入css文件中，再引入

**使用步骤两部**

1. 新建一个css文件，在这个文件里不用使用<style>文件，直接写样式即可
2. 使用<link>标签引入css文件：< link rel="stylesheet" href="文件路径">
