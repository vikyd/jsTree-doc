# 插件？
jsTree 将一些功能从核心移出，成为插件，你需要时才启用此插件。
`plugins`配置项是一个数组，数组项是插件名，用于启用插件。

插件的选项配置见`插件 API`页面。

例如，下面示例表示启用了所有官方插件（你可按需启用）：
```js
"plugins" : [
	"checkbox",
	"contextmenu",
	"dnd",
	"massload",
	"search",
	"sort",
	"state",
	"types",
	"unique",
	"wholerow",
	"changed",
	"conditionalselect"
]
```

下面将逐一介绍每个插件。




# 变化插件（Changed plugin）
此插件作用是为选择变化时提供更多附加信息。
一旦在`plugins`配置项中启用本插件，`changed.jstree`事件数据中将多一个`changed`属性，
这个属性包含一些数据，如最近一次`changed.tree`事件中的`selected`、`deselected`的节点。

```js
$(function () {
  $("#plugins")
    .on("changed.jstree", function (e, data) {
      console.log(data.changed.selected); // newly selected
      console.log(data.changed.deselected); // newly deselected
    })
    .jstree({
      "plugins" : [ "changed" ]
    });
});
```

示例：https://www.jstree.com/plugins/




# 勾选框插件（Checkbox plugin）
此插件在每个节点前添加一个勾选框，使得多选节点更方便。

此插件支持三种状态：全部子节点选中、全部未选中、部分选中`undetermined`。部分选中状态会向上转播状态

你还可通过设置传播方式的选项进行微调。

需注意的是，即使一个节点处于禁用状态，勾选框也会受传播的影响。

半选中状态`undetermined`是插件自动计算出来的，但当你使用 AJAX 来按需加载节点，
且想将这些未加载节点的状态设置为半选中状态，那你可传入这个参数：`"undetermined" : true`。

插件的选项配置见`插件 API`页面。

```js
$(function () {
  $("#plugins1").jstree({
    "checkbox" : {
      "keep_selected_style" : false
    },
    "plugins" : [ "checkbox" ]
  });
});
```

示例：https://www.jstree.com/plugins/




# 条件选择插件（Conditionalselect plugin）
此插件覆盖了`activate_node`函数，并允许设置成不被回调函数调用。

```js
$(function () {
  $("#plugins10").jstree({
    "conditionalselect" : function (node, event) {
      return false;
    },
    "plugins" : [ "conditionalselect" ]
  });
});
```

示例：https://www.jstree.com/plugins/




# 右键菜单插件（Contextmenu plugin）
此插件用于在树中点击右键时弹出一个菜单。
此菜单可通过具体的配置进行自定义。

插件的选项配置见`插件 API`页面。


```js
$(function () {
  $("#plugins2").jstree({
     "core" : {
       // so that create works
       "check_callback" : true
     },
    "plugins" : [ "contextmenu" ]
  });
});
```

示例：https://www.jstree.com/plugins/




# Drag & drop plugin(dnd)
此插件允许拖动和释放节点来调整树结构。

插件的选项配置见`插件 API`页面。

```js
$(function () {
  $("#plugins3").jstree({
    "core" : {
      "check_callback" : true
    },
    "plugins" : [ "dnd" ]
  });
});
```

示例：https://www.jstree.com/plugins/




# 惯性加载插件（Massload plugin）
此插件允许一次请求获得多个节点的数据（与懒加载一起使用）。

插件的选项配置见`插件 API`页面。

```js
$(function () {
  $("#plugins10").jstree({
    "core" : {
      "data" : { .. AJAX config .. }
    },
    "massload" : {
      "url" : "/some/path",
      "data" : function (nodes) {
        return { "ids" : nodes.join(",") };
      }
    }
    "plugins" : [ "massload", "state" ]
  });
});
```

示例：https://www.jstree.com/plugins/




# 搜索插件（Search plugin）
此插件允许对树的节点进行搜索，并允许只显示搜索到的节点。

插件的选项配置见`插件 API`页面。

```js
$(function () {
  $("#plugins4").jstree({
    "plugins" : [ "search" ]
  });
  var to = false;
  $('#plugins4_q').keyup(function () {
    if(to) { clearTimeout(to); }
    to = setTimeout(function () {
      var v = $('#plugins4_q').val();
      $('#plugins4').jstree(true).search(v);
    }, 250);
  });
});
```

示例：https://www.jstree.com/plugins/




# 排序插件（Sort plugin）
此插件自动对兄弟节点进行排序，默认是按字母升序排序。

插件的选项配置见`插件 API`页面。

```js
$(function () {
  $("#plugins5").jstree({
    "plugins" : [ "sort" ]
  });
});
```

示例：https://www.jstree.com/plugins/




# 状态插件（State plugin）
此插件允许保存节点的打开、选中状态到用户浏览器中，这样下次重新打开页面时可恢复到上次关闭页面时的状态。

插件的选项配置见`插件 API`页面。

```js
$(function () {
  $("#plugins6").jstree({
    "state" : { "key" : "demo2" },
    "plugins" : [ "state" ]
  });
});
```

这个示例中，你可调整里面的节点，然后刷新页面看看节点的状态是否还有保留。
示例：https://www.jstree.com/plugins/




# 类型插件（Types plugin）
此插件用于为节点设置类型，即按类型形成不同的节点组，使得更容易对嵌套规则、图标等进行操作。

可用`set_type`或直接设置节点的`type`属性值来设置节点的类型。

插件的选项配置见`插件 API`页面。

```js
$(function () {
  $("#plugins7").jstree({
    "types" : {
      "default" : {
        "icon" : "glyphicon glyphicon-flash"
      },
      "demo" : {
        "icon" : "glyphicon glyphicon-ok"
      }
    },
    "plugins" : [ "types" ]
  });
});
```

示例：https://www.jstree.com/plugins/




# 唯一性插件（Unique plugin）
此插件强制限制兄弟节点间不能重名。
此插件没有配置项，其作用在于重命名、拖动节点时防止重名。

```js
$(function () {
  $("#plugins8").jstree({
    "core" : {
      "check_callback" : true
    },
    "plugins" : [ "unique", "dnd" ]
  });
});
```

示例：https://www.jstree.com/plugins/




# 整行插件（Wholerow plugin）
使每个节点显示为一整行，而不是仅仅节点的图标和节点名。
这会使得容易选中节点，但同时也可能会导致旧浏览器中拥有较多节点树较慢。

```js
$(function () {
  $("#plugins9").jstree({
    "plugins" : [ "wholerow" ]
  });
});
```

示例：https://www.jstree.com/plugins/




------