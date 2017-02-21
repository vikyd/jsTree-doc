# 用 HTML 来填充树
## 基本使用
jsTree 可自动转换一个标准的无序列表为一棵树。
最低要求是包含 1 个`ul`并内嵌几个包含名称的`li`。

```html
<div id="html1">
  <ul>
    <li>Root node 1</li>
    <li>Root node 2</li>
  </ul>
</div>
```

你应以一个容器包围`ul`，并在此容器上创建实例，如：
```js
$('#html1').jstree();
```




## 子节点
若需创建子节点，只需继续内嵌`ul`。

```html
<div id="html1">
  <ul>
    <li>Root node 1
      <ul>
        <li>Child node 1</li>
        <li><a href="#">Child node 2</a></li>
      </ul>
    </li>
  </ul>
</div>
```

在 jstree 内部，默认会将文本转换成一个链接`<a>`。
若本身已存在一个`<a>`（如上述的`Child node 2`），并不受影响，
因为 jstree 设置为不自动跳转到对应的链接，而是触发一个名为`changed.jstree`的事件，
你可监听此事件来做想做的事。

关于事件，请见`API 页面`。




## 用 CSS class 设置初始状态
若想一个节点默认被选中，只需为`<a>`添加一个`jstree-clicked`类即可。

类似的，还可在`li`中添加`jstree-open`类，使得节点展开，可见其子节点。

建议为每个`<li>`设置唯一的`id`属性，在 jstree 的某些事件中，通过这些 id，可以很方便进行相关的操作。

```html
…
<li class="jstree-open" id="node_1">
  <ul>
    <li>
      <a href="#" class="jstree-clicked">Child</a>
    </li>
  </ul>
</li>
…
```




## 用`data`属性设置初始状态
可通过`data-jstree`属性来设置一个节点的状态。

属性中支持的组合包括：`opened` `selected` `disabled` `icon`。

```html
<li data-jstree='{"opened":true,"selected":true}'>
  <ul>
    <li data-jstree='{"disabled":true}'>Child</li>
    <li data-jstree='{"icon":"//jstree.com/tree.png"}'>
      Child</li>
    <li data-jstree='{"icon":"glyphicon glyphicon-leaf"}'>
      Child</li>
  </ul>
</li>
```

指定一个图片文件地址（任何包含`/`的字符串），可以在节点上显示图标。
也可通过填入 CSS class 名来设置图标。
例如，下面将设置一个 Twitter Bootstrap 的叶子图标：
```json
"icon" : "glyphicon glyphicon-leaf"
```




## 通过 AJAX 加载数据
可通过 AJAX 的响应的 HTML 数据来填充树。
响应的 HTML 格式与前面所述的一致，不同的仅是数据来源于后台服务器而已。

可通过配置` $.jstree.defaults.core.data`来更好使用此功能。

只需使用类似 jQuery AJAX 的配置，jstree 即可自动发送 AJAX 请求来获取填充树的数据。

请在响应数据的每个`LI`中添加`jstree-closed`类，且不要在其中再嵌套`UL`，
因为 jstree 会自动发起另外的 AJAX 请求来请求嵌套的节点数据。

除了标准的 jQuery AJAX 配置项，jstree 还提供了`data`和`url`。
这两个选项的值可以是一个函数，函数将在实例范围内执行，并接收 1 个参数（正在加载的节点），
函数的返回值作为这两个配置项各自最终的值。


```html
$('#tree').jstree({
  'core' : {
    'data' : {
      'url' : 'ajax_nodes.html',
      'data' : function (node) {
        return { 'id' : node.id };
      }
    }
  }
});

// Example response:
<ul>
<li>Node 1</li>
<li class="jstree-closed">Node 2</li>
</ul>
```




------