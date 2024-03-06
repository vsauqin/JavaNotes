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

  - <dl>

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



