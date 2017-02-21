# 监听事件
jsTree 会在容器上触发各种事件，详细事件列表见`API 页面`。

想获取更多关于事件的信息，可打断点，查看其中的`data`参数。

大部分情况下，当调用节点时，都可获得整个节点对象。
还可通过节点 ID 和`get_node()`来获取节点数据。

```js
$('#jstree')
  // listen for event
  .on('changed.jstree', function (e, data) {
    var i, j, r = [];
    for(i = 0, j = data.selected.length; i < j; i++) {
      r.push(data.instance.get_node(data.selected[i]).text);
    }
    $('#event_result').html('Selected: ' + r.join(', '));
  })
  // create the instance
  .jstree();
```




