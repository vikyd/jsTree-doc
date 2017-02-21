# 配置实例
如前面所述，创建这样一个实例不会改变任何设置。
```js
$('#jstree').jstree();
```


你可一次性进行全局设置，在之后创建的实例中都生效：
```js
$.jstree.defaults.core.themes.variant = "large";
$('#jstree').jstree();
```


但大部分情况下，你想要的可能不是全局设置，而是针对不同的实例进行不同的设置。
下面是传入一个配置对象的例子：
```js
$('#jstree').jstree({
  "plugins" : [ "wholerow", "checkbox" ]
});
```

上述例子中，配置对象中有一个属性是`plugins`，是一个字符串数组，表示需要启用的插件的名字。


所有不与插件相关的配置都放在名为`core`的属性中，不同插件的配置放在以各插件为名的属性中：
```js
$('#jstree').jstree({
  "core" : {
    "themes" : {
      "variant" : "large"
    }
  },
  "checkbox" : {
    "keep_selected_style" : false
  },
  "plugins" : [ "wholerow", "checkbox" ]
});
```


可用的配置及其默认选项见`API 页面`，可用于配置任何实例。

譬如，jstree 默认允许对节点进行多选，对应的默认配置是`$.jstree.defaults.core.multiple`。
但你可在配置对象中传入`"core" : { "multiple" : false }`进行修改：
```js
$("#jstree").jstree({
  "core" : {
    "multiple" : false,
    "animation" : 0
  }
});
```



------