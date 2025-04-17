操，兄弟，欢迎来到 HTML 学习的第二天！昨天你已经他妈的牛逼了一把，搞定了基本的网页骨架，写出了带标题、段落、图片和链接的页面，爽得不行吧？今天我们继续冲，不整那些高深莫测的玩意儿，保持简单粗暴，带你再学几个 HTML 的核心技能，顺便加点 CSS 基础，让你的网页从“能看”进化到“有点骚气”。这篇教程是为零基础的小白量身打造，，干货塞满，脏话照旧，傻逼废话一概没有。还会把可能踩的坑掰开揉碎讲清楚，省得你抓狂。

**今天的目标**：学会列表、表格、简单表单，搞懂怎么用 CSS 给网页加点颜色和样式，写一个更像样的网页。昨天的坑（乱码、图片不显示、链接点不动）我们会再提醒，今天的新坑也会一一列出，确保你不翻车。准备好了？操，干！

---

## 复习第一天：你已经是个小牛逼了

昨天你已经掌握了 HTML 的入门精髓，简单回顾一下，给你点信心：

- **HTML 是啥**：网页的骨架，负责内容结构，简单得像吃薯片，一嚼就懂。
- **文件结构**：`<!DOCTYPE html>`、`<html>`、`<head>`、`<body>`，这是网页的固定套路。
- **核心标签**：
  - `<h1>`-`<h6>`：标题，从大到小，写网页的头条。
  - `<p>`：段落，写大段文字，自动换行。
  - `<a>`：链接，点一下跳转到别的网页。
  - `<img>`：图片，展示骚气的猫狗图。
  - `<br>`：换行，强制断行。
  - `<!-- -->`：注释，写备注不显示。
- **实战成果**：你写了个带标题、段落、链接、图片的网页，打开浏览器看效果，爽得一批。
- **踩过的坑**：
  - 乱码：忘了 `<meta charset="UTF-8">`。
  - 图片不显示：路径错（大小写、文件不在文件夹）。
  - 链接点不动：`href` 写错（漏 `https://`）。

今天我们在这基础上加料，学新标签（列表、表格、表单）和基础 CSS，网页直接起飞。别慌，内容不多，慢慢嚼，保你爽。

---

## 准备工作：别他妈磨叽，赶紧开干

跟第一天一样，你需要的最低配置很简单：

1. **文本编辑器**：

   - **VS Code**（下载：`code.visualstudio.com`）是首选，免费，功能牛逼，代码高亮、自动补全、插件丰富。
   - 装 **Live Server** 插件，写代码实时看效果，爽到爆炸。
   - **替代选项**：Windows 自带记事本、Mac 的 TextEdit 也能用，但体验烂，建议直接上 VS Code。
   - **坑提醒**：
     - 下载 VS Code 时选对系统版本（Windows 64 位、Mac M1 芯片等）。
     - Live Server 装好后，确认 VS Code 底部有“Go Live”按钮，没反应可能是端口（默认 5500）被占，换个端口（右键 Live Server 设置）。
     - 保存文件（Ctrl + S）后 Live Server 才刷新，忘了保存就等着抓狂吧。

2. **浏览器**：

   - **Chrome** 最佳，F12 开发者工具能查错、看样式，牛逼得不行。
   - Edge、Firefox 也行，但 Chrome 的调试体验最爽。
   - **坑提醒**：
     - 老版本浏览器（比如 IE）可能不支持新 HTML/CSS 特性，用最新版 Chrome 避坑。
     - 网页没更新？可能是浏览器缓存，按 **Ctrl + F5** 强制刷新。
     - 拖文件到浏览器没效果？确认文件后缀是 `.html`，别保存成 `.txt`。

3. **文件夹**：

   - 建个新文件夹，比如 `my_webpage_day2`，放 HTML 文件、图片。
   - **坑提醒**：
     - 文件夹别放太深（比如 `C:\Users\XXX\XXX\XXX`），路径长可能导致图片加载失败。
     - 文件夹名和文件名别用中文、空格、特殊字符（比如 `#`、`%`），否则可能出问题。
     - 比如 `我的网页` 改成 `my_webpage`，`dog pic.jpg` 改成 `dog_pic.jpg`。

4. **图片**：

   - 准备 1-2 张图片（jpg/png，1MB 以内），比如 `dog.jpg`、`cat.jpg`，放文件夹里，后面练 `<img>` 标签。
   - **坑提醒**：
     - 图片文件名大小写敏感（`Dog.jpg` 和 `dog.jpg` 不一样）。
     - 图片太大（比如 10MB）加载慢，压缩到 1MB 以下（用在线工具如 `tinypng.com`）。
     - 图片格式用 jpg/png，gif 也行，其他格式（比如 webp）可能不兼容。

5. **心态**：

   - 学新东西难免踩坑，别他妈一出错就放弃，跟着教程一步步来，准能搞定。
   - 遇到问题，Google 或 Baidu 搜，99% 有人踩过同样的坑。

---

## 新技能 1：列表标签，内容整理得倍儿清晰

网页上经常要列东西，比如爱好、导航条、购物清单。HTML 有两种列表标签，简单实用，学了就能装逼。

### 1. 无序列表：`<ul>` + `<li>`

- **用处**：列出一堆没顺序的东西，比如你的爱好、待办事项。

- **格式**：

  ```html
  <ul>
      <li>第一项</li>
      <li>第二项</li>
      <li>第三项</li>
  </ul>
  ```

- **效果**：每项前面有小圆点（或方块），自动换行，干净整齐。

- **示例**：

  ```html
  <h2>我的爱好，操，爽爆！</h2>
  <ul>
      <li>刷 B 站，动漫游戏视频看不停</li>
      <li>打 LOL，排位上分贼刺激</li>
      <li>吃鸡，落地成盒也开心</li>
  </ul>
  ```

- **效果**：

  ## 我的爱好，操，爽爆！

  - 刷 B 站，动漫游戏视频看不停
  - 打 LOL，排位上分贼刺激
  - 吃鸡，落地成盒也开心

- **坑提醒**：

  - `<li>` 必须放在 `<ul>` 里，别单独写 `<li>`，否则浏览器可能渲染乱。

  - 忘了闭合 `<li>`（比如 `<li>xxx`），排版可能错位。

  - 想改小圆点样式（比如换成方块或箭头），得用 CSS，后面会讲。

  - 列表嵌套（比如 `<ul>` 里再放 `<ul>`）要小心，别搞乱层级，比如：

    ```html
    <!-- 错 -->
    <ul>
        <li>爱好<ul>xxx</li></ul>
    </ul>
    <!-- 对 -->
    <ul>
        <li>爱好
            <ul>
                <li>xxx</li>
            </ul>
        </li>
    </ul>
    ```

### 2. 有序列表：`<ol>` + `<li>`

- **用处**：列出有顺序的东西，比如步骤、排名、计划。

- **格式**：

  ```html
  <ol>
      <li>第一步</li>
      <li>第二步</li>
      <li>第三步</li>
  </ol>
  ```

- **效果**：每项前面有数字（1, 2, 3），自动换行，整齐划一。

- **示例**：

  ```html
  <h2>学 HTML 的骚气步骤</h2>
  <ol>
      <li>学会基本标签，操，简单到爆</li>
      <li>加点 CSS，网页变漂亮</li>
      <li>搞 JavaScript，网页能动起来</li>
  </ol>
  ```

- **效果**：

  ## 学 HTML 的骚气步骤

  1. 学会基本标签，操，简单到爆
  2. 加点 CSS，网页变漂亮
  3. 搞 JavaScript，网页能动起来

- **坑提醒**：

  - `<ol>` 里只能放 `<li>`，别塞其他标签（比如 `<p>`），否则可能报错或渲染乱。

  - 想改数字样式（比如用字母 a, b, c 或罗马数字 I, II, III），加 `type` 属性：

    ```html
    <ol type="a">
        <li>第一项</li>
        <li>第二项</li>
    </ol>
    ```

    效果：a. 第一项 b. 第二项

  - 或者用 CSS 更灵活，后面会讲。

  - 忘了闭合 `<ol>` 或 `<li>`，浏览器可能自动补全，但代码不规范，容易出问题。

  - 嵌套有序列表时，保持层级清晰，别交叉嵌套。

---

## 新技能 2：表格标签，数据整齐又专业

表格用来展示结构化数据，比如成绩单、时间表、产品对比。HTML 的表格标签简单，但得写对，不然容易乱。

### 表格结构：`<table>`、`<tr>`、`<th>`、`<td>`

- **标签说明**：

  - `<table>`：整个表格的容器。
  - `<tr>`：表格的一行（table row）。
  - `<th>`：表头单元格（table header），默认加粗居中。
  - `<td>`：普通单元格（table data）。

- **示例**：

  ```html
  <table>
      <tr>
          <th>名字</th>
          <th>成绩</th>
      </tr>
      <tr>
          <td>小明</td>
          <td>90</td>
      </tr>
      <tr>
          <td>小红</td>
          <td>85</td>
      </tr>
  </table>
  ```

- **效果**：

  | 名字 | 成绩 |
  | --- | --- |
  | 小明 | 90 |
  | 小红 | 85 |

- **坑提醒**：

  - 忘了闭合 `<tr>`、`<th>`、`<td>`，表格可能显示不全或错位。
  - 每行 `<tr>` 的 `<th>` 或 `<td>` 数量要一致，不然表格会歪（比如第一行 2 个 `<th>`，第二行 3 个 `<td>`，就乱了）。
  - 默认没边框，丑得像狗屎，后面加 CSS 或临时用 `border` 属性。

### 加边框（临时用 HTML 属性）

- HTML5 不推荐用 `border` 属性，但小白阶段可以用，简单粗暴：

  ```html
  <table border="1">
      <tr>
          <th>名字</th>
          <th>成绩</th>
      </tr>
      <tr>
          <td>小明</td>
          <td>90</td>
      </tr>
  </table>
  ```

- **效果**：表格有 1 像素的边框，看着清楚多了。

- **坑提醒**：

  - `border` 值是像素（比如 `border="2"`），别写单位（`border="2px"` 无效）。
  - 想让表格更骚气（改颜色、调整间距），得用 CSS。
  - `border` 只加在 `<table>` 上，单元格可能没边框，CSS 能解决。

### 表格进阶：合并单元格

- 用 `colspan`（跨列）、`rowspan`（跨行）合并单元格。

- **示例**：

  ```html
  <table border="1">
      <tr>
          <th colspan="2">标题跨两列</th>
      </tr>
      <tr>
          <td>单元格1</td>
          <td>单元格2</td>
      </tr>
  </table>
  ```

- **效果**：

  | 标题跨两列 |  |
  | --- | --- |
  | 单元格1 | 单元格2 |

- **坑提醒**：

  - 合并后，后面 `<tr>` 的 `<td>` 数量要减去合并的格子（比如 `colspan="2"`，下一行少 1 个 `<td>`）。
  - 别乱合并，容易算错格子数，表格会歪。

---

## 新技能 3：简单表单，收集用户输入像大佬

表单让用户输入信息，比如登录框、搜索框、留言板。HTML 表单标签很多，今天只学最简单的，够你装逼。

### 表单结构：`<form>`、`<input>`、`<button>`

- **标签说明**：

  - `<form>`：表单容器，包住所有输入控件。
  - `<input>`：输入框（单身狗标签），类型由 `type` 属性决定。
  - `<button>`：按钮，通常用来提交表单。

- **示例**：

  ```html
  <form>
      <p>用户名: <input type="text" placeholder="输入你的名字"></p>
      <p>密码: <input type="password" placeholder="输入密码"></p>
      <button>提交，操！</button>
  </form>
  ```

- **效果**：

  用户名: \[输入框，提示“输入你的名字”\]\
  密码: \[密码框，提示“输入密码”\]\
  \[提交，操！\]

- **说明**：

  - `<input type="text">`：普通文本输入框。
  - `<input type="password">`：密码输入框，输入显示为 `****`。
  - `placeholder`：输入框的提示文字，灰色，输入后消失。
  - `<button>`：默认是提交按钮，点一下提交表单数据。

- **坑提醒**：

  - 现在点“提交”没反应，因为没加 `action` 属性（指定提交地址）。后面学 JavaScript 或后端再搞。
  - `<input>` 不要闭合（`<input></input>` 错，`<input>` 就行）。
  - `placeholder` 不显示？确认浏览器是最新版，旧浏览器可能不支持。
  - 表单默认样式丑（输入框小、按钮灰），用 CSS 美化。

### 表单扩展：加个选择框

- 用 `<select>` 和 `<option>` 做下拉菜单。

- **示例**：

  ```html
  <form>
      <p>选择你的爱好: 
          <select>
              <option>B 站</option>
              <option>LOL</option>
              <option>吃鸡</option>
          </select>
      </p>
  </form>
  ```

- **效果**：下拉框，选项是 B 站、LOL、吃鸡。

- **坑提醒**：

  - `<option>` 必须放在 `<select>` 里，别单独写。
  - 忘了闭合 `<select>`，下拉框可能显示不全。
  - 想默认选中某项，加 `selected`：`<option selected>B 站</option>`。

---

## 新技能 4：基础 CSS，网页从土鳖变骚气

HTML 是骨架，CSS（Cascading Style Sheets，层叠样式表）是装修，能改颜色、字体、间距、布局。CSS 很强大，今天只学最简单的**内联样式**（写在标签的 `style` 属性里），小白也能上手。

### 内联 CSS：用 `style` 属性

- **格式**：`<标签 style="属性: 值; 属性: 值">`

- **示例**：

  ```html
  <h1 style="color: red;">红色的标题，骚气冲天！</h1>
  <p style="font-size: 20px; color: blue;">蓝色大字，爽得一批！</p>
  <img src="dog.jpg" alt="狗" style="width: 200px;">
  ```

- **效果**：

  - 标题变红色。
  - 段落文字变蓝，字体大小 20 像素。
  - 图片宽度缩到 200 像素。

- **常用 CSS 属性**：

  - `color`：文字颜色（`red`, `blue`, `#FF0000`, `rgb(255, 0, 0)`）。
  - `font-size`：字体大小（`20px`, `1.5em`, `16pt`）。
  - `width`、`height`：宽度、高度（`200px`, `50%`）。
  - `background-color`：背景色（`yellow`, `#00FF00`）。
  - `border`：边框（`1px solid black`）。
  - `text-align`：文字对齐（`left`, `center`, `right`）。

- **坑提醒**：

  - CSS 属性名区分大小写，`color` 正确，`Color` 无效。
  - 属性间用 `;` 分隔，忘了分号可能导致后面样式失效。
  - 值写错（比如 `color: redd`），样式不生效，用 Chrome F12 检查。
  - 内联 CSS 不利于维护，后面学外部 CSS 文件。

### 给表格加样式

- **示例**：

  ```html
  <table style="border: 1px solid black;">
      <tr>
          <th style="background-color: yellow; border: 1px solid black;">名字</th>
          <th style="background-color: yellow; border: 1px solid black;">成绩</th>
      </tr>
      <tr>
          <td style="border: 1px solid black;">小明</td>
          <td style="border: 1px solid black;">90</td>
      </tr>
  </table>
  ```

- **效果**：表格有黑边，表头黄色，清晰又骚气。

- **坑提醒**：

  - 每格都加 `border`，不然边框不完整（只加 `<table>` 的 `border` 不够）。
  - 颜色值可以用名字（`red`）、十六进制（`#FF0000`）、RGB（`rgb(255, 0, 0)`）。
  - 想调整单元格间距，用 CSS `padding` 或 `margin`，后面学。

### 给表单加样式

- **示例**：

  ```html
  <form>
      <p>用户名: <input type="text" style="width: 200px; border: 2px solid blue;"></p>
      <button style="background-color: red; color: white;">提交，操！</button>
  </form>
  ```

- **效果**：输入框宽 200px，蓝边框；按钮红底白字。

- **坑提醒**：

  - 输入框默认窄，加 `width` 让它好看。
  - 按钮样式不生效？检查 `background-color` 和 `color` 是否拼错。

---

## 实战：写一个牛逼到爆的网页

整合今天学的，写个包含列表、表格、表单、CSS 样式的网页。假设你有张图片 `dog.jpg`。

### 代码

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>第二天网页，操，骚气升级！</title>
</head>
<body style="background-color: #f0f0f0;">
    <!-- 主标题 -->
    <h1 style="color: blue; text-align: center;">欢迎体验我的第二天网页，爽爆了！</h1>
    
    <!-- 关于我 -->
    <h2 style="color: green;">关于我</h2>
    <p style="font-size: 18px;">老子是 HTML 小白，第二天继续冲，感觉他妈的爽到飞起！</p>
    <p style="font-size: 18px;">这个网页有列表、表格、表单，还加了点样式，牛逼得不行！</p>
    
    <!-- 爱好列表 -->
    <h2 style="color: green;">我的爱好</h2>
    <ul>
        <li>刷 B 站，动漫游戏视频看不停</li>
        <li>打 LOL，操，排位上分贼爽</li>
        <li>吃鸡，落地成盒也开心</li>
    </ul>
    
    <!-- 学习计划表格 -->
    <h2 style="color: green;">我的学习计划</h2>
    <table style="border: 1px solid black;">
        <tr>
            <th style="background-color: yellow; border: 1px solid black;">阶段</th>
            <th style="background-color: yellow; border: 1px solid black;">内容</th>
        </tr>
        <tr>
            <td style="border: 1px solid black;">第一周</td>
            <td style="border: 1px solid black;">搞定 HTML 基础</td>
        </tr>
        <tr>
            <td style="border: 1px solid black;">第二周</td>
            <td style="border: 1px solid black;">学 CSS 装扮网页</td>
        </tr>
        <tr>
            <td style="border: 1px solid black;">第三周</td>
            <td style="border: 1px solid black;">搞 JavaScript 让网页动起来</td>
        </tr>
    </table>
    
    <!-- 留言表单 -->
    <h2 style="color: green;">给我留言</h2>
    <form>
        <p>名字: <input type="text" placeholder="你的名字" style="width: 200px; border: 2px solid blue;"></p>
        <p>密码: <input type="password" placeholder="输入密码" style="width: 200px; border: 2px solid blue;"></p>
        <p>爱好: 
            <select>
                <option>B 站</option>
                <option>LOL</option>
                <option>吃鸡</option>
            </select>
        </p>
        <button style="background-color: red; color: white;">提交，操！</button>
    </form>
    
    <!-- 图片 -->
    <h2 style="color: green;">一张骚气的图片</h2>
    <img src="dog.jpg" alt="一只帅狗" style="width: 300px;">
    <p style="font-size: 18px; color: purple;">这只狗帅得一批，哈哈！</p>
</body>
</html>
```

### 怎么运行

1. 在 VS Code 建新文件，复制代码，保存为 `day2.html`。
2. 确保 `dog.jpg` 在同一文件夹（没图片就找张别的，改名）。
3. 用浏览器打开，或用 Live Server 实时预览。

### 效果

网页长这样：

- **浏览器标题**：第二天网页，操，骚气升级！

- **内容（带样式）**：

  # 欢迎体验我的第二天网页，爽爆了！（蓝色，居中）

  ## 关于我（绿色）

  老子是 HTML 小白，第二天继续冲，感觉他妈的爽到飞起！（18px）\
  这个网页有列表、表格、表单，还加了点样式，牛逼得不行！（18px）

  ## 我的爱好（绿色）

  - 刷 B 站，动漫游戏视频看不停
  - 打 LOL，操，排位上分贼爽
  - 吃鸡，落地成盒也开心

  ## 我的学习计划（绿色）

  | 阶段 | 内容 |
  | --- | --- |
  | 第一周 | 搞定 HTML 基础 |
  | 第二周 | 学 CSS 装扮网页 |
  | 第三周 | 搞 JavaScript 让网页动起来 |
  | （黄色表头，黑边框） |  |

  ## 给我留言（绿色）

  名字: \[输入框，200px 宽，蓝边框\]\
  密码: \[密码框，200px 宽，蓝边框\]\
  爱好: \[下拉框：B 站、LOL、吃鸡\]\
  \[提交，操！\]（红底白字）

  ## 一张骚气的图片（绿色）

  \[图片：一只帅狗\]（300px 宽）\
  这只狗帅得一批，哈哈！（18px，紫色）

- **整体效果**：背景浅灰，标题蓝色居中，副标题绿色，表格黄色表头，表单输入框蓝边框，按钮红底白字，图片缩放合适，文字大小颜色骚气。

**坑提醒**：

- **图片没显示**？检查 `dog.jpg` 是否在文件夹，文件名大小写一致，路径别用绝对路径（`C:\XXX`）。
- **表格没边框**？确认每格都加了 `border: 1px solid black`。
- **表单点提交没反应**？正常，后面学 JavaScript 加功能。
- **CSS 没效果**？检查 `style` 语法（属性间用 `;` 分开，值别拼错）。
- **背景色没变**？确认 `<body>` 的 `background-color` 写对（`#f0f0f0` 是浅灰）。
- **Live Server 不刷新**？确认保存文件，端口没被占（换 5501 试试）。

---

## 常见问题及解决：别他妈抓狂，坑都给你列好了

昨天的问题（乱码、图片不显示、链接点不动）可能还会遇到，今天加几个新坑，帮你快速解决：

1. **列表显示不正常？**

   - **原因**：`<li>` 没放 `<ul>` 或 `<ol>` 里，或者嵌套乱了。

   - **解决**：

     - 确认 `<ul><li>xxx</li></ul>` 或 `<ol><li>xxx</li></ol>` 结构完整。

     - 嵌套列表别交叉，比如：

       ```html
       <!-- 错 -->
       <ul><li><ul>xxx</li></ul></ul>
       <!-- 对 -->
       <ul><li><ul><li>xxx</li></ul></li></ul>
       ```

     - 用 Chrome F12 检查 HTML 结构，看层级是否正确\`\`\`html

     | 阶段 | 内容 |
     | --- | --- |
     | 第一周 | 搞定 HTML 基础 |
     | 第二周 | 学 CSS 装扮网页 |
     | 第三周 | 搞 JavaScript 让网页动起来 |

     \`\`\` - \*\*效果\*\*：表格有黑边，表头黄色，清晰又骚气。 - \*\*坑提醒\*\*： - 每格都加 \`border\`，不然边框不完整（只加 \`\` 的 \`border\` 不够）。 - 颜色值可以用名字（\`red\`）、十六进制（\`#FF0000\`）、RGB（\`rgb(255, 0, 0)\`）。 - 想调整单元格间距，用 CSS \`padding\` 或 \`margin\`，后面学。

   - **表单输入框太丑或没反应？**

     - **原因**：默认样式丑，或没加 `action` 属性。
     - **解决**：
       - 用 CSS 改输入框大小（比如 `<input style="width: 200px;">`）。
       - 提交没反应正常，后面学 JavaScript 或后端。
       - `placeholder` 文字不显示？确认浏览器是最新版，旧浏览器可能不支持。
       - 输入框太小？加 `width` 和 `padding`（比如 `style="width: 200px; padding: 5px;"`）。

   - **CSS 没效果？**

     - **原因**：语法错、属性不支持、值写错。
     - **解决**：
       - 检查 `style` 属性，比如 `color: red;`（别写 `color: Red` 或 `color=red`）。
       - 颜色值用 `red`, `#FF0000`, `rgb(255, 0, 0)`，别用奇怪的值（比如 `redd`）。
       - 用 Chrome F12 开发者工具，看“Styles”面板，找错误。
       - 多个属性忘了 `;`，后面样式可能失效（比如 `style="color: red font-size: 20px"` 错，改成 `style="color: red; font-size: 20px;"`）。

   - **网页背景色没变？**

     - **原因**：`background-color` 写错或作用范围不对。
     - **解决**：
       - 确认写的是 `background-color: #f0f0f0;`（别漏 `color` 或写成 `background`）。
       - 整页背景要写在 `<body>` 的 `style` 里（比如 `<body style="background-color: #f0f0f0;">`）。
       - 检查值是否正确，`#f0f0f0` 是浅灰，`#000000` 是黑，`#FFFFFF` 是白。

   - **VS Code 或 Live Server 抽风？**

     - **原因**：插件没装好、端口占用、文件没保存。
     - **解决**：
       - 确认 Live Server 插件已安装并启用（VS Code 底部有“Go Live”按钮）。
       - 端口被占（比如 5500），在 VS Code 设置里改端口（比如 5501）。
       - 每次改代码后保存（Ctrl + S），Live Server 才会刷新。
       - VS Code 卡顿？重启软件，或者关掉无关扩展。

   - **代码没效果，浏览器报错？**

     - **原因**：语法错误、浏览器不兼容、标签嵌套错。
     - **解决**：
       - 打开 Chrome F12 开发者工具，看“Console”标签有没有错误提示。
       - 比如提示“Unexpected token”，检查标签是否写错（比如 `<h1>xxx<h1>`）。
       - 用最新版 Chrome，避开老浏览器兼容问题。
       - 检查嵌套，比如 `<form><p><input></p></form>` 合法，`<form><p><input></form></p>` 会乱。

   - 练习：动动手，练出顶级骚气

     光看不练假把式，下面是几个练习，巩固今天学的，练完你的网页能拿去装逼：

     1. **改样式**：

        - 把 `<h1>` 改成紫色（`color: purple`），字体大小 30px，居中（`text-align: center`）。
        - 表格边框改成蓝色（`border: 1px solid blue`），表头背景改成绿色（`background-color: green`）。
        - 按钮改成绿底白字（`background-color: green; color: white`）。
        - **坑提醒**：
          - CSS 属性值别写错（`color: purple` 不是 `color: Purple`）。
          - 检查分号（`style="color: purple; font-size: 30px;"`）。
          - 保存后刷新，确认效果。

     2. **加列表**：

        - 加一个有序列表，写你未来 3 天的学习计划（比如“明天学 CSS”）。

        - **示例**：

          ```html
          <h2 style="color: green;">未来三天计划</h2>
          <ol>
              <li>明天学 CSS，搞样式</li>
              <li>后天学 JavaScript，网页动起来</li>
              <li>大后天做个小项目，装逼</li>
          </ol>
          ```

        - **坑提醒**：

          - `<li>` 放 `<ol>` 里，别漏闭合（`<li>xxx</li>`）。
          - 列表样式想改（比如用字母），加 `type="a"` 或用 CSS。

     3. **改表格**：

        - 在表格加一行，写你自己的数据（比如“第四周，建个个人网站”）。

        - **示例**：

          ```html
          <tr>
              <td style="border: 1px solid black;">第四周</td>
              <td style="border: 1px solid black;">建个个人网站</td>
          </tr>
          ```

        - **坑提醒**：

          - 新行 `<td>` 数量要跟表头一致（2 个 `<th>` 就对应 2 个 `<td>`）。
          - 边框别忘了加（`border: 1px solid black`）。

     4. **加表单项**：

        - 在表单加个文本输入框（比如“邮箱”）和一个下拉框（比如“性别”）。

        - **示例**：

          ```html
          <p>邮箱: <input type="text" placeholder="你的邮箱" style="width: 200px; border: 2px solid blue;"></p>
          <p>性别: 
              <select>
                  <option>男</option>
                  <option>女</option>
                  <option>其他</option>
              </select>
          </p>
          ```

        - **坑提醒**：

          - 检查 `type` 是否正确（`text` 不是 `txt`）。
          - `<option>` 放 `<select>` 里，别漏闭合。

     5. **加图片和样式**：

        - 加一张新图片（比如 `cat.jpg`），设置宽度 250px，描述文字改成绿色，字体大小 20px。

        - **示例**：

          ```html
          <h2 style="color: green;">另一张骚气图片</h2>
          <img src="cat.jpg" alt="一只萌猫" style="width: 250px;">
          <p style="color: green; font-size: 20px;">这猫可爱得一批，哈哈！</p>
          ```

        - **坑提醒**：

          - 图片路径确认正确（`cat.jpg` 在文件夹里，大小写一致）。
          - 图片太大？压缩到 1MB 以下。
          - 路径别用绝对路径（`C:\XXX\cat.jpg` 错，用 `cat.jpg`）。

     **练习目标**：改完网页应该有：

     - 紫色居中大标题（30px），蓝色边框绿色表头的表格，绿底白字按钮。
     - 1 个有序列表（3 项，未来计划）。
     - 表格多 1 行（第四周）。
     - 表单多 1 个邮箱输入框和 1 个性别下拉框。
     - 新图片（250px 宽），绿色 20px 描述文字。
     - 整体背景浅灰，标题副标题骚气，表单按钮醒目。

     保存，刷新浏览器，看看效果。是不是他妈的帅炸了？

     ---

     ## 进阶小技巧：第二天再牛逼点，装逼更彻底

     虽然是第二天，但你这么猛，给你点进阶技巧，让网页更专业：

     1. **列表嵌套，内容更有层次**：

        - 在 `<ul>` 或 `<ol>` 里再加列表，组织复杂内容。

        - **示例**：

          ```html
          <ul>
              <li>爱好
                  <ul>
                      <li>B 站，看动漫</li>
                      <li>LOL，上分</li>
                  </ul>
              </li>
              <li>学习计划
                  <ul>
                      <li>HTML</li>
                      <li>CSS</li>
                  </ul>
              </li>
          </ul>
          ```

        - **效果**：

          - 爱好
            - B 站，看动漫
            - LOL，上分
          - 学习计划
            - HTML
            - CSS

        - **坑提醒**：

          - 嵌套别乱，保持层级清晰（`<ul><li><ul><li>`）。
          - 用 Chrome F12 检查列表结构，确认没交叉。

     2. **表格合并单元格，布局更灵活**：

        - 用 `colspan`（跨列）、`rowspan`（跨行）。

        - **示例**：

          ```html
          <table border="1">
              <tr>
                  <th colspan="2">标题跨两列</th>
              </tr>
              <tr>
                  <td>单元格1</td>
                  <td>单元格2</td>
              </tr>
          </table>
          ```

        - **效果**：

     | 标题跨两列 |  |
     | --- | --- |
     | 单元格1 | 单元格2 |

   - **坑提醒**：

     - 合并后，后面 `<tr>` 的 `<td>` 数量要调整（`colspan="2"` 少 1 个 `<td>`）。
     - 别乱合并，容易算错格子，表格会歪。
     - 用 CSS 加 `padding`（比如 `style="padding: 10px;"`）让格子内容不贴边。

2. **CSS 文字对齐和间距**：

   - 用 `text-align` 控制文字对齐，`margin` 和 `padding` 调间距。

   - **示例**：

     ```html
     <h2 style="text-align: center;">居中标题</h2>
     <p style="margin: 20px; padding: 10px; border: 1px solid black;">有边框和间距的段落</p>
     ```

   - **效果**：标题居中，段落有 20px 外边距、10px 内边距、黑边框。

   - **坑提醒**：

     - `text-align` 只对块级元素（`<h2>`、`<p>`）有效，`<img>` 无效。
     - `margin` 是外边距，`padding` 是内边距，别搞混。
     - 值可以是 `10px`, `1em`, `10%`，但别写错单位。

3. **调试技巧，快速找错**：

   - 用 Chrome F12 开发者工具：
     - “Elements”面板：看 HTML 结构，检查标签嵌套。
     - “Styles”面板：看 CSS 样式，找失效的属性。
     - “Console”面板：看错误提示（比如 “Unexpected token”）。
   - **示例**：写错 `<h1>xxx<h1>`，Console 会报错，点错误跳转到代码行。
   - **坑提醒**：
     - 改代码后保存（Ctrl + S），刷新浏览器（Ctrl + F5）。
     - 调试时关掉无关标签页，浏览器跑得快。

4. **代码格式化，保持整洁**：

   - VS Code 右键 &gt; “格式化文档”，自动缩进代码，清晰易读。
   - 装 **Prettier** 插件（扩展栏搜索 `Prettier`，安装），每次保存自动格式化。
   - **坑提醒**：
     - 格式化前保存文件，不然可能丢代码。
     - Prettier 可能跟其他插件冲突，关掉无关扩展。

5. **图片居中**：

   - 用 CSS `display: block; margin: auto;` 让图片居中。

   - **示例**：

     ```html
     <img src="dog.jpg" alt="狗" style="display: block; margin: auto; width: 300px;">
     ```

   - **坑提醒**：

     - 必须加 `display: block`，否则 `margin: auto` 无效。
     - 确认图片宽度（`width`）合理，别撑爆页面。

---

## 总结：第二天你他妈无敌了

今天你学了：

- **列表**：`<ul>`（无序，带圆点）、`<ol>`（有序，带数字），清晰列内容，嵌套也能搞。
- **表格**：`<table>`、`<tr>`、`<th>`、`<td>`，展示数据整齐，合并单元格更灵活。
- **表单**：`<form>`、`<input>`（文本、密码、下拉框）、`<button>`，收集用户输入，装逼利器。
- **基础 CSS**：内联 `style`，改颜色（`color`, `background-color`）、字体（`font-size`）、边框（`border`）、对齐（`text-align`）、间距（`margin`, `padding`），网页从土鳖变骚气。
- **实战**：写了带列表、表格、表单、样式的网页，背景浅灰，标题蓝色，表格黄色，表单蓝边框，按钮红底白字，图片缩放完美。
- **坑及解决**：
  - 列表：嵌套乱、漏闭合。
  - 表格：格子数量不对、没边框。
  - 表单：样式丑、提交无反应。
  - CSS：语法错、值无效。
  - 调试：用 Chrome F12 找错，保存刷新确认。

你已经能搞出功能齐全、有点样子的网页，比昨天骚气十倍。HTML 还有更多花样（语义标签、外部 CSS、响应式布局），但第二天稳住这些，你已经吊打 95% 的小白。

**下一步建议**：

- **多练**：把列表、表格、表单代码多写几遍，熟到飞起。
- **试 CSS**：玩更多属性（`border-radius` 圆角、`box-shadow` 阴影），调出骚气效果。
- **学外部 CSS**：明天学怎么把 CSS 写到单独文件，代码更整洁，维护更爽。
- **找资源**：去 Unsplash（`unsplash.com`）下免费高清图片，练 `<img>` 标签。
- **做项目**：试着做个个人主页，整合 HTML 和 CSS，装逼到朋友圈。

**鼓励一下**：操，兄弟，第二天你干得太他妈无敌了！网页已经有点大佬范儿了，继续冲，明天更骚更牛逼！