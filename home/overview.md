# 新手入门 - 都在这里

## [下载 jsTree](https://github.com/vakata/jstree/zipball/3.3.3) 或 使用 CDNJS
若选择下载，则所有所需的文件都在`dist/`目录下。




## 包含 jsTree 主题
支持自动加载主题，但为了性能考虑，建议包含主题的 CSS 文件。

若自己管理 CSS 文件：
```html
<link rel="stylesheet" href="dist/themes/default/style.min.css" />
```

若从 CDNJS加载文件：
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/jstree/3.2.1/themes/default/style.min.css" />
```




## 创建一个容器
容器是一个放置树的地方，一个`<div>`就足够。
此例子仅包含一个嵌套的`<ul>`，没有任何其他数据源。
```html
<div id="jstree_demo_div"></div>
```

> 译注：这个例子貌似真没有`<ul>`，只有增加了下面这段 Js 才会默认生成一个空的`<ul>`：
> ```js
> $('#jstree_demo_div').jstree();
> ```




## 引入 jQuery
jsTree 要求 1.9.0 或以上版本的 jQuery，你可以使用一个 CDN 版本或引用本地的 js 文件。
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/1.12.1/jquery.min.js"></script>
```




## 引入 jsTree
若你自己管理 jsTree 的文件，对于线上生产项目请使用`dist/jstree.min.js`，对于开发项目请使用`dist/jstree.js`。
```html
<script src="dist/jstree.min.js"></script>
```

若使用 CDNJS：
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jstree/3.2.1/jstree.min.js"></script>
```




## 创建一个实例
当 DOM 就绪后，就可开始创建 jstree 实例。
```js
$(function () { $('#jstree_demo_div').jstree(); });
```




## 监听事件
当用户对树进行操作时，jsTree 通过事件告诉你发生了什么变化。
在 jsTree 中绑定事件就像绑定一个普通的 click 事件那么简单。
jsTree 提供的事件见`API 页面`。

```js
$('#jstree_demo_div').on("changed.jstree", function (e, data) {
  console.log(data.selected);
});
```




## 在实例上操作
一旦树创建完毕，你可对树进行一些操作。
jsTree 提供的操作方法见`API 页面`。

下面 3 个例子的作用是一样的：
```js
$('button').on('click', function () {
  $('#jstree').jstree(true).select_node('child_node_1');
  $('#jstree').jstree('select_node', 'child_node_1');
  $.jstree.reference('#jstree').select_node('child_node_1');
});
```




## 所有代码
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>jsTree test</title>
  <!-- 2 load the theme CSS file -->
  <link rel="stylesheet" href="dist/themes/default/style.min.css" />
</head>
<body>
  <!-- 3 setup a container element -->
  <div id="jstree">
    <!-- in this example the tree is populated from inline HTML -->
    <ul>
      <li>Root node 1
        <ul>
          <li id="child_node_1">Child node 1</li>
          <li>Child node 2</li>
        </ul>
      </li>
      <li>Root node 2</li>
    </ul>
  </div>
  <button>demo button</button>

  <!-- 4 include the jQuery library -->
  <script src="dist/libs/jquery.js"></script>
  <!-- 5 include the minified jstree source -->
  <script src="dist/jstree.min.js"></script>
  <script>
  $(function () {
    // 6 create an instance when the DOM is ready
    $('#jstree').jstree();
    // 7 bind to events triggered on the tree
    $('#jstree').on("changed.jstree", function (e, data) {
      console.log(data.selected);
    });
    // 8 interact with the tree - either way is OK
    $('button').on('click', function () {
      $('#jstree').jstree(true).select_node('child_node_1');
      $('#jstree').jstree('select_node', 'child_node_1');
      $.jstree.reference('#jstree').select_node('child_node_1');
    });
  });
  </script>
</body>
</html>
```




------