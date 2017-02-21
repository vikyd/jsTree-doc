# 调用实例的方法
> 注意：默认情况下，禁止对树进行任何修改（`create` `rename` `move` `delete`），若需启用修改，请把`core.check_callback`设为`true`。 

若需调用实例提供方法，则应先获得实例的引用。

下面例子演示了如何获得实例的引用，并调用其中的方法。

详细的 API 见`API 页面`。

```js
// 3 ways of doing the same thing
$('#jstree').jstree(true)
  .select_node('mn1');
$('#jstree')
  .jstree('select_node', 'mn2');
$.jstree.reference('#jstree')
  .select_node('mn3');
```



