# 变化插件（Changed plugin）
此插件为`changed.jstree`事件添加了更多信息。
`changed`事件的数据属性更多新数据，并包含一系列选中的`selected`或取消选中`deselected`的节点。




## changed.jstree Event（`changed`插件）
当已选中的节点发生变化（`选择`发生变化）时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Object` |
| `action` | `Object` 引起`选择`发生变化的`action` |
| `selected` | `Array` 当前的已选中的节点 |
| `event` | `Object` 触发本事件`changed_node`的事件 |




# 勾选框插件（Checkbox plugin）
此插件在每个节点前添加勾选框`checkbox`，使得选中多个节点更方便。

勾选框支持 3 中状态：
- 节点下的所有节点均已选中
- 节点下的所有节点均未选中
- 节点下的部分节点被选中（状态将使得上游父节点均显示此状态）

译注：下面插件名用英文`checkbox`，说明文字用中文`勾选框`。




## $.jstree.defaults.checkbox（checkbox插件）
存储`checkbox`插件的所有默认配置。




## $.jstree.defaults.checkbox.visible（checkbox插件）
boolean，默认`true`，设置勾选框是否可见（之后可用`show_checkboxes()` `hide_checkboxes`修改是否可见）。




## $.jstree.defaults.checkbox.three_state（checkbox插件）
boolean，默认`true`，设置勾选框状态包含半选中状态，并传播状态。




## $.jstree.defaults.checkbox.whole_node（checkbox插件）
boolean，默认`true`，设置点击节点任意位置时是否都对勾选框生效。




## $.jstree.defaults.checkbox.keep_selected_style（checkbox插件）
boolean，默认`true`，设置是否保持节点的选中状态。




## $.jstree.defaults.checkbox.cascade（checkbox插件）
设置如何传播节点状态，默认为空字符串''。
- 字符串`up`：启用向上传播状态
- 字符串`down`：启用向下传播状态
- 字符串`undetermined`：启用半选中状态。
- 若`three_state`值为`true`，则本设置将自动设置为`'up+down+undetermined`。




## $.jstree.defaults.checkbox.tie_selection（checkbox插件）
boolean，默认`true`。
- `true`则勾选框与 3 种默认状态绑定。
- `false`则勾选框与`checkbox`插件内部自定义的状态数组绑定。




## _undetermined ()（checkbox插件） - -  `private`
设置勾选框为半选中状态`undetermined`，仅内部使用。




## show_checkboxes ()（checkbox插件）
显示勾选框的图标。




## hide_checkboxes ()（checkbox插件）
隐藏勾选框的图标。




## toggle_checkboxes ()（checkbox插件）
消或隐勾选框的图标。




## is_undetermined (obj)（checkbox插件）
判断节点是否处于半选中状态`undetermined`。

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |
| `返回` | `Boolean` |




## disable_checkbox (obj)（checkbox插件）
禁用节点的勾选框。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 单个节点，也可是节点数组 |
| `触发事件` | `disable_checkbox.jstree` |




## disable_checkbox.jstree Event （checkbox插件）
当节点的勾选框被禁用时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` |




## enable_checkbox (obj)（checkbox插件）
启用节点的勾选框。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 单个节点，也可是节点数组 |
| `触发事件` | `enable_checkbox.jstree` |




## enable_checkbox.jstree Event （checkbox插件）
当节点的勾选框被启用时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` |




## check_node (obj)（checkbox插件）
选中节点（除非`tie_selection`的值为`false`，否则`select_node`将被内部调起）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 单个节点，也可是节点数组 |
| `触发事件` | `check_node.jstree` |




## check_node.jstree Event （checkbox插件）
当节点被选中时触发（仅当`tie_selection`值为`false`时有效）。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` |
| `selected` | `Array` 当前的选中项 |
| `event` | `Object` 触发`check_node`的事件（若有的话） |




## uncheck_node (obj)（checkbox插件）
取消选中节点（除非`tie_selection`的值为`false`，否则`deselect_node`将被内部调起）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 单个节点，也可是节点数组 |
| `触发事件` | `uncheck_node.jstree` |




## uncheck_node.jstree Event （checkbox插件）
当节点被选中时触发（仅当`tie_selection`值为`false`时有效）。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` |
| `selected` | `Array` 当前的选中项 |
| `event` | `Object` 触发`uncheck_node`的事件（若有的话） |




## check_all ()（checkbox插件）
选中所有节点（除非`tie_selection`的值为`false`，否则`select_all`将被内部调起）。

| 触发 | 描述 |
| :----- | :------ |
| `触发事件` | `uncheck_node.jstree` |




## check_all.jstree Event （checkbox插件）
当选中所有节点时触发（仅当`tie_selection`值为`false`时有效）。

| 参数 | 描述 |
| :----- | :------ |
| `selected` | `Array` 当前的选中项 |




## uncheck_all ()（checkbox插件）
取消选中所有节点（除非`tie_selection`的值为`false`，否则`deselect_all`将被内部调起）。

| 触发 | 描述 |
| :----- | :------ |
| `触发事件` | `deselect_all.jstree` |




## uncheck_all.jstree Event （checkbox插件）
当取消选中所有节点时触发（仅当`tie_selection`值为`false`时有效）。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 之前的选中项 |
| `selected` | `Array` 当前的选中项 |




## is_checked (obj)（checkbox插件）
检查节点是否已选中（除非`tie_selection`的值为`true`，否则返回值将于`is_select`一致）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |
| `返回` | `Boolean` |




## get_checked ([full])（checkbox插件）
获取已选中的节点数组（除非`tie_selection`的值为`true`，否则返回值将于`get_selected`一致）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `full` | `mixed` 若为`true`，则返回的节点的详细数据，否则仅返回节点的 ID |
| `返回` | `Array` |




## get_top_checked ([full])（checkbox插件）
获取顶层的已选中节点数组
（将忽略已选中节点的子节点）
（除非`tie_selection`的值为`true`，否则返回值将于`get_top_selected`一致）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `full` | `mixed` 若为`true`，则返回的节点的详细数据，否则仅返回节点的 ID |
| `返回` | `Array` |




## get_bottom_checked ([full])（checkbox插件）
获取底层的已选中节点数组
（将忽略已选中节点的父节点）
（除非`tie_selection`的值为`true`，否则返回值将于`get_bottom_selected`一致）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `full` | `mixed` 若为`true`，则返回的节点的详细数据，否则仅返回节点的 ID |
| `返回` | `Array` |





# 条件选择插件（Conditionalselect plugin）
此插件允许定义一个回调函数，用来允许或不允许用户选中节点。




## $.jstree.defaults.checkbox.visible（checkBox插件）
译注：这个标题跳转到`checkbox插件`的同名设置项。




# 右键菜单插件（Contextmenu plugin）
在节点上点右键时弹出菜单.




## $.jstree.defaults.contextmenu（右键菜单插件）
存储右键插件的所有默认配置。




## $.jstree.defaults.contextmenu.select_node（右键菜单插件）
boolean，默认`true`，设置当右键弹出菜单时，是否也应选中该节点。




## $.jstree.defaults.contextmenu.show_at_node（右键菜单插件）
boolean，默认`true`，设置右键菜单是否显示在节点旁边，否则右键菜单将跟随鼠标位置。




## $.jstree.defaults.contextmenu.items（右键菜单插件）
（译注：这几乎算是此插件最重要的配置项，为了更通俗易明，这里部分翻译不完全与原文一致）

一个包含多个动作`actions`的对象，或一个函数，此函数接收 1 个参数：节点`node`，并返回动作对象。

每个动作`aciton`包含：
- 键名（动作名，唯一，如`rename`）
- 键值（一个对象）
  - label：显示的字符串
  - action：对应的动作调用函数，action 接收一个参数`data`对象，包含数据
    - item：点击的右键菜单项
    - reference：树中的节点 DOM
    - element：右键菜单的 DOM
    - position：右键菜单的位置`x/y`

其中上面`item`的属性包括：
- `separator_before`：boolean，是否在此菜单项前添加一个分隔符
- `separator_after`：boolean，是否在此菜单项后添加一个分隔符
- `_disabled`：boolean，是否禁用此菜单项
- `label`：string，菜单项的显示名称（也可以是返回字符串的函数）
- `title`：string，菜单项的`tooltip`
- `action`：function，点击此菜单单项时触发的动作
- `icon`：string，可以是一个图标的文件路径，或 CSS 的 class 名。若使用图标文件路径，则应使用当前目录作为前缀`./`，否则都认为是 CSS 类名 
- `shortcut`：此菜单项的快捷键码`keyCode`（前提是已看到此菜单项）（如重命名`rename`的快捷键是`F2`，即键值为`113`）
- `shortcut_label`：快捷键的显示名称（如重命名的`F2`）
- `submenu`：子菜单，结构与`$.jstree.defaults.contextmenu.items`一致。里面的每项都是一个子菜单，当鼠标经过本菜单项时将显示此处设置的子菜单。




## show_contextmenu (obj [, x, y])（右键菜单插件）
准备并显示节点的右键菜单。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `x` | `Number` 右键菜单的 x 坐标值（相对于 document） |
| `y` | `Number` 右键菜单的 y 坐标值 |
| `e` | `Object` 触发右键菜单的事件（若有的话） |
| `触发` | `show_contextmenu.jstree` |




## _show_contextmenu (obj, x, y, i)（右键菜单插件） - -  `private`
准备并显示节点的右键菜单。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `x` | `Number` 右键菜单的 x 坐标值（相对于 document） |
| `y` | `Number` 右键菜单的 y 坐标值 |
| `e` | `Object` 触发右键菜单的事件（若有的话） |
| `触发` | `show_contextmenu.jstree` |




## show_contextmenu.jstree Event （右键菜单插件）
当节点的右键菜单显示时触发。

| 参数 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `x` | `Number` 右键菜单的 x 坐标值（相对于 document） |
| `y` | `Number` 右键菜单的 y 坐标值 |




## context_parse.vakata Event （右键菜单插件）
当右键菜单解释完毕（HTML 建立完毕）时触发（在 document 中触发）。

| 参数 | 描述 |
| :----- | :------ |
| `reference` | `jQuery` 被点击的元素 |
| `element` | `jQuery` 右键菜单 |
| `position` | `Object` 右键菜单的 x、y 坐标值 |




## context_show.vakata Event （右键菜单插件）
当右键菜单显示完毕时触发（在 document 中触发）。

| 参数 | 描述 |
| :----- | :------ |
| `reference` | `jQuery` 被点击的元素 |
| `element` | `jQuery` 右键菜单 |
| `position` | `Object` 右键菜单的 x、y 坐标值 |




## context_hide.vakata Event （右键菜单插件）
当右键菜单消失完毕时触发（在 document 中触发）。

| 参数 | 描述 |
| :----- | :------ |
| `reference` | `jQuery` 被点击的元素 |
| `element` | `jQuery` 右键菜单 |
| `position` | `Object` 右键菜单的 x、y 坐标值 |




# 拖动和释放插件（Drag'n'drop plugin，即 DND 插件）
使节点可以在树中拖动并释放，从而实现节点的移动或复制。

本插件又名 DND 插件。




## $.jstree.defaults.dnd（右键菜单插件）
存储 DND 插件的所有默认配置。




## $.jstree.defaults.dnd.copy（右键菜单插件）
boolean，默认`true`，设置（按住`Ctrl`或`meta`键）拖动节点时是否复制节点。




## $.jstree.defaults.dnd.open_timeout（右键菜单插件）
number，默认`500`，单位毫秒，设置开始拖动后的有效时间。




## $.jstree.defaults.dnd.is_draggable（右键菜单插件）
function，若为`false`则全面禁用拖动，设置一个节点是否允许拖动。
此函数在树实例中执行，接收一个参数（将被拖动的节点数组 ）。




## $.jstree.defaults.dnd.check_while_dragging（右键菜单插件）
boolean，默认`true`，设置当用户拖动节点时是否不断检查（与之对应的时释放`drop`时的检查）。




## $.jstree.defaults.dnd.always_copy（右键菜单插件）
boolean，默认`false`，设置拖动释放时是否均采用复制操作（与之对应的是`移动`）。




## $.jstree.defaults.dnd.inside_pos（右键菜单插件）
integer，默认`0`，也支持`first` `last`，拖动节点释放在某个节点内的位置。




## $.jstree.defaults.dnd.drag_selection（右键菜单插件）
boolean，默认`true`，设置拖动时是拖动所有选中的节点，还是仅拖动鼠标所在的那个节点。




## $.jstree.defaults.dnd.touch（右键菜单插件）
控制 DND 插件在触屏设备环境中如何工作。

- 若为`true`，则与桌面浏览器一样，这样可能会对滚动有影响。
- 若为`false`，则 DND 插件在触屏设备环境中不生效。
- 若为`selected`，则在触屏设备环境中，仅已选中的节点可被拖动。




## $.jstree.defaults.dnd.large_drop_target（右键菜单插件）
控制是否可被释放到节点的任何位置，而不只能释放到节点锚点（锚点指节点的图标 + 名称的位置），默认只能释放到节点锚点。

此配置最好和`wholerow`插件一起使用。当此配置启用时，可能会造成在移动设备上难以取消拖动，
因为这时整棵树都是可被释放的区域。




## $.jstree.defaults.dnd.large_drag_target（右键菜单插件）
控制是否可从节点的任意位置开始拖动，而不只能在节点的图标和名称中开始拖动，此配置最好和`wholerow`插件一起使用。
需注意的是，此配置可能会导致在移动设备上滚动时产生一些问题，建议此时将`touch`配置项设置为`selected`。




## $.jstree.defaults.dnd.use_html5（右键菜单插件）
控制是否使用 HTML5 DND API，而不是传统的。
这将允许更好使用 HTML5 的其他 DND 事件控制。




## dnd_scroll.vakata Event （右键菜单插件）
当拖动引起元素滚动时触发（在 document 中触发）。

| 参数 | 描述 |
| :----- | :------ |
| `data` | `Mixed` 调用`$.vakata.dnd.start`时得到的数据 |
| `element` | `DOM` 被拖动的 DOM 元素 |
| `helper` | `jQuery` 在鼠标附近显示的辅助器 |
| `event` | `jQuery` 正在滚动的元素 |




## dnd_start.vakata Event （右键菜单插件）
当拖动开始时触发（在 document 中触发）。

| 参数 | 描述 |
| :----- | :------ |
| `data` | `Mixed` 调用`$.vakata.dnd.start`时得到的数据 |
| `element` | `DOM` 被拖动的 DOM 元素 |
| `helper` | `jQuery` 在鼠标附近显示的辅助器 |
| `event` | `jQuery` 引起开始拖动的事件（可能是`mousemove`） |




## dnd_move.vakata Event （右键菜单插件）
当拖动正在进行时触发（在 document 中触发）。

| 参数 | 描述 |
| :----- | :------ |
| `data` | `Mixed` 调用`$.vakata.dnd.start`时得到的数据 |
| `element` | `DOM` 被拖动的 DOM 元素 |
| `helper` | `jQuery` 在鼠标附近显示的辅助器 |
| `event` | `jQuery` 引起此行为的事件（很可能是`mousemove`） |




## dnd_stop.vakata Event （右键菜单插件）
当拖动结束时触发（在 document 中触发）。

| 参数 | 描述 |
| :----- | :------ |
| `data` | `Mixed` 调用`$.vakata.dnd.start`时得到的数据 |
| `element` | `DOM` 被拖动的 DOM 元素 |
| `helper` | `jQuery` 在鼠标附近显示的辅助器 |
| `event` | `jQuery` 引起拖动结束的事件 |




# 惯性加载插件（Massload plugin）
为 jsTree 添加所谓`惯性`加载功能，这样可在一次数据请求中获得多个节点的数据（仅在延迟加载时有用）。




## $.jstree.defaults.massload（惯性加载插件）
惯性加载的配置。

可以按照标准的 jQuery AJAX 的配置方式设置本选项。

除了 jQuery AJAX 方式配置，还可设置两个属性`data`和`url`。
可为这两个属性分别设置一个函数，这个函数将运行在树实例范围中，并接收 1 个参数（将被加载的节点 ID），
函数的返回值就是这两个属性的最终值。

还可直接将本选项设置为一个函数，此函数将接收 2 个参数，一个是将被加载的节点ID，另一个是一个回调函数，
作为结果返回。

AJAX 和 函数 这两种形式都依赖同样的返回值，即包含节点 ID 作为键名的一个对象，对应的键值则是对应节点的子节点数组。

```js
{
    "id1" : [
              { "text" : "Child of ID1", "id" : "c1" }, 
              { "text" : "Another child of ID1", "id" : "c2" }
            ],
    "id2" : [{ "text" : "Child of ID2", "id" : "c3" }]
}
```




# 搜索插件（Search plugin）
为 jsTree 添加搜索功能。




## $.jstree.defaults.search（搜索插件）
存储搜索插件的所有默认配置。




## $.jstree.defaults.search.ajax（搜索插件）
一个类似 jQuery AJAX 的配置，用于树从服务器中加载数据。

向服务器发送的请求中，将包含以下参数：
- `str`，搜索字符串
- `inside`，可选，限制在某个节点范围内的节点 ID 

服务器的响应结果：是一个 JSON 数组，每项都是一个节点的数据，以便于搜索匹配时直接打开该数组。

若本配置项值为`false`，则不从服务器查询数据。

若本配置项为一个函数，则此函数将被树实例范围内执行，并接收 3 个参数：
- 搜索字符串 
- 加载搜索结果完成时的回调函数
- 限制搜索范围在某节点的节点 ID




## $.jstree.defaults.search.fuzzy（搜索插件）
boolean，默认`false`，设置是否使用模糊搜索（如搜索`chnd3`时，能搜出`child node 3`）。




## $.jstree.defaults.search.case_sensitive（搜索插件）
boolean，默认`false`，设置搜索时是否区分大小写。




## $.jstree.defaults.search.show_only_matches（搜索插件）
boolean，默认`false`，设置在树中是否仅显示匹配的结果（没匹配上的隐藏），

需注意的是，在旧浏览器中或树节点较多时，此操作可能会很慢。

本选项可在搜索时动态设置。




## $.jstree.defaults.search.show_only_matches_children（搜索插件）
boolean，默认`false`，设置（当`show_only_matches`为`true`时）是否显示匹配节点的子节点。

本选项可在搜索时动态设置。




## $.jstree.defaults.search.close_opened_onclear（搜索插件）
boolean，默认`true`，设置当清空搜索条件或再次搜索时，是否关闭上次搜索打开的所有节点。




## $.jstree.defaults.search.search_leaves_only（搜索插件）
boolean，默认`false`，设置是否仅搜索叶子节点。




## $.jstree.defaults.search.search_callback（搜索插件）
若值为一个函数，则在树实例范围内被执行，并接收 2 个参数
- 搜索字符串
- 节点（可以是树的任意节点，所以请谨慎使用）

此函数须返回一个 boolean 值，默认是`false`，指明此节点是否匹配搜索结果。
（如果配置项`search_only_leaves`为`true`且节点不是叶子节点时，则不会显示出来）




## search (str [, skip_async])（搜索插件）
用于根据字符串在树中搜索节点。

| 参数/触发 | 描述 |
| :----- | :------ |
| `str` | `String` 搜索字符串 |
| `skip_async` | `Boolean` 若为`true`则不从服务器中加载数据（即使已配置了 AJAX） |
| `show_only_matches` | `Boolean` 若为`true`则仅显示匹配的节点（需注意此设置可能导致旧浏览器或树节点较多时很慢） |
| `inside` | `mixed` 节点，限制搜索范围在某个节点中 |
| `append` | `Boolean` 若为`true`则下次的搜索结果直接附加到上次的搜索结果中 |
| `触发事件` | `search.jstree` |




## search.jstree Event （搜索插件）
当搜索节点完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `jQuery` 已匹配的节点 |
| `str` | `String` 搜索字符串 |
| `res` | `Array` 已匹配节点的数据对象 |




## clear_search ()（搜索插件）
用于清空搜索结果（移除节点元素上的 CSS class，并显示所有被过滤器隐藏的节点）。

| 触发 | 描述 |
| :----- | :------ |
| `触发事件` | `clear_search.jstree` |




## clear_search.jstree Event （搜索插件）
当清空搜索结果完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `jQuery` 已匹配的节点 |
| `str` | `String` 搜索字符串 |
| `res` | `Array` 已匹配节点的数据对象 |




# 排序插件（Sort plugin）
根据排序函数在树中自动排序兄弟节点。




## $.jstree.defaults.sort（排序插件）
本设置函数用于排序节点。

此函数在树实例范围中执行，并接收两个节点作为参数，并应返回`1`或`-1`。




## sort (obj [, deep])（排序插件） - -  `private`
用于对节点的子节点进行排序。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `jQuery` 节点 |
| `deep` | `Boolean` 若为`true`则节点将递归排序 |
| `触发事件` | `search.jstree` |




# 状态插件（State plugin）
使用一些设置在用户电脑（浏览器的 localStorage、cookies等）中保存树的状态（选中的节点、已打开的节点）。




## $.jstree.defaults.state（状态插件）
存储状态插件的所有配置。




## $.jstree.defaults.state.key（状态插件）
字符串，默认`jstree`，作为树状态存储时的 key（若你的项目有棵树，请修改此配置）。




## $.jstree.defaults.state.events（状态插件）
字符串，为触发存储树状态的一些列事件，用空格隔开每个事件，
默认`changed.jstree open_node.jstree close_node.jstree`.




## $.jstree.defaults.state.ttl（状态插件）
树状态存储的有效期，单位毫秒，默认`false`，即永不过期。




## $.jstree.defaults.state.filter（状态插件）
function，在开始存储状态前执行的函数，接收 1 个参数（状态对象），用于清除一些不需要存储的状态。




## state_ready.jstree Event （状态插件）  
当状态插件完成状态存储时触发（可理解为当刚好没有状态需要存储时触发）。




## save_state ()（状态插件）
保存状态。




## restore_state ()（状态插件）
从用户电脑中恢复树的状态。




## clear_state ()（状态插件） 
清除用户电脑上存储的状态。




# 类型插件（Types plugin）   
用于为节点设置类型，即按类型形成不同的节点组，使得更容易对嵌套规则、图标等进行操作。




## $.jstree.defaults.types（类型插件）
一个对象，包含多个属性，这些属性就是所有的节点类型。

每个属性的 key 是节点类型名， value 则是一个对象，包括以下内容：
- `max_children`：节点可包含的最大子节点数，若不设置或设置为`-1`则无限制。
- `max_depth`：节点可包含的最大子节点深度。`1`表示节点可包含子节点，但不能包含子子节点。若不设置或设置为`-1`则无限制。
- `valid_children`：一个字符串数组，表示允许包含的节点类型。若不设置或设置为`-1`则无限制。
- `icon`：可以是一个图标的文件路径，或 CSS 的 class 名。若使用图标文件路径，则应使用当前目录作为前缀`./`，否则都认为是 CSS 类名。若忽略则使用主题的默认图标。
- `li_attr`：一个对象，里面的值用于添加的到 LI DOM 节点属性中（将与节点的自身数据合并）。
- `a_attr`：一个对象，里面的值用于添加的到 A DOM 节点属性中（将与节点的自身数据合并）。

有两个预定义的类型：
- `#`：代表树的根节点，如`max_children`会控制根节点的最大数量。
- `default`：代表默认节点，任何没有设置类型的节点都是此类型。




## get_rules (obj)（类型插件）
用于获取节点的类型设置。

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `返回` | `Object` |




## get_type (obj [, rules])（类型插件）
用于获取节点的类型（string）或设置（object）。

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `rules` | `Boolean` 若为`true`则返回设置（object），否则返回类型（string） |
| `返回` | `String` Object` |




## set_type (obj, type)（类型插件） 
用于修改节点的类型。

| 参数 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `type` | `String` 新类型 |




# 唯一性插件（Unique plugin）
强制兄弟节点间不允许包含相同的名字。




## $.jstree.defaults.unique（唯一性插件）
存储唯一性插件的所有配置。




## $.jstree.defaults.unique.case_sensitive（唯一性插件）
设置比较节点名时是否区分大小写，默认`false`。




## $.jstree.defaults.unique.duplicate（唯一性插件）
一个回调函数，将在树实例范围内执行，当新建节点名与已有节点名相同时触发，接收两个参数：冲突的名字、数量。
默认会将新建节点命名为`New node (2)`。




# 整行插件（Wholerow plugin）   
使每个节点显示为一整行，而不是仅仅节点的图标和节点名。
这会使得容易选中节点，但同时也可能会导致旧浏览器中拥有较多节点树较慢。




------