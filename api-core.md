# jsTree 核心功能（core functionality）

## $.jstree
包含所有 jstree 相关的函数和变量，包括用于创建、访问、维护实例的类和方法。



## $.jstree.version
jstree 的版本号



## $.jstree.defaults
包含用于创建新实例的默认配置



## $.jstree.defaults.plugins
默认是`[]`。

配置实例中使用的插件。是一个字符串数组，每个字符串是一个插件名。



## $.jstree.plugins
存放所有已加载的插件（内部用）



## $.jstree.create (el [, options])
创建一个 jstree 实例

| 参数/返回 |   描述   |
| --------   | -----  |
| `el`       | `DOMElement` `jQuery` `String`，要创建实例的元素，可以是jQuery对象或一个选择器 |
| `options`  | `Object` 此实例的配置（扩展自`$.jstree.defaults`）  |
| `返回`      | `jsTree` 新的实例    |



## $.jstree.destroy ()
从 DOM 中删除 jstree 的所有痕迹，并销毁所有的实例。



## $.jstree.core (id) - -  `private`
jstree 类的构造函数，仅用于内部。

| 参数 |   描述   |
| --------   | -----  |
| `id`       | `Number` 此实例的索引号（index） |


$.jstree.reference (needle)
获取一个已存在实例的引用。

| 参数/返回 |   描述   |
| --------   | -----  |
| `needle`   | `DOMElement` `jQuery` `String` |
| `返回`      | `jsTree` `null` 实例，若找不到实例则返回 `null` |

**Examples**
```js
// provided a container with an ID of "tree", and a nested node with an ID of "branch"
// all of there will return the same instance
$.jstree.reference('tree');
$.jstree.reference('#tree');
$.jstree.reference($('#tree'));
$.jstree.reference(document.getElementByID('tree'));
$.jstree.reference('branch');
$.jstree.reference('#branch');
$.jstree.reference($('#branch'));
$.jstree.reference(document.getElementByID('branch'));
```



## $().jstree([arg])
创建实例、获取实例、在实例中调用命令。

- 若当前节点（node）没有关联的实例，则会新建一个实例。新建实例时，将`arg`用于扩展`$.jstree.defaults`。
此时将没有返回值（不会中断链式操作）。

- 若已存在实例，且`arg`是一个字符串，则此实例将执行`arg`中填的命令及命令参数。
若此命令有返回值，则返回此值（此命令函数可能会影响链式操作）。

- 若已存在实例，且`arg`不是一个字符串，则返回此实例（类似`$.jstree.reference`）。

- 其他情况，则无返回值，且不会中断链式操作。

| 参数/返回 |   描述   |
| --------   | -----  |
| `arg`   | `String` `Object`|
| `返回`   | `Mixed` |

**Examples**
```js
$('#tree1').jstree(); // creates an instance
$('#tree2').jstree({ plugins : [] }); // create an instance with some options
$('#tree1').jstree('open_node', '#branch_1'); // call a method on an existing instance, passing additional arguments
$('#tree2').jstree(); // get an existing instance (or create an instance)
$('#tree2').jstree(true); // get an existing instance (will not create new instance)
$('#branch_1').jstree().select_node('#branch_1'); // get an instance (using a nested element and call a method)
```



## $(':jstree')
用于在实例中查找元素。

| 参数/返回 |   描述   |
| -------- | ------ |
| `返回`   | `jQuery` |

**Examples**
```js
$('div:jstree').each(function () {
    $(this).jstree('destroy');
});
```



## $.jstree.defaults.core
存储核心功能的所有默认配置。



## $.jstree.defaults.core.data
数据配置。

若值为`false`，则 jstree 容器元素内的 HTML 将用于构建树（这些元素应是一些包含子项的无序列表）。

你也可以在这里传入一个 HTML 字符串 或 JSON 数字。

还可以传入一个 jQuery 的 AJAX 配置，jstree 会自动判断响应的类型（JSON 或 HTML）来构建树。

除了标准的 jQuery AJAX 选项，这里还可传入函数给`data`和`url`。
这些函数将接收一个参数（加载的节点），返回的值作为最终的配置。

最后，还可传入一个函数。此函数将接收 2 个参数：1 个是加载的节点，1 个是回调函数。
函数最后应执行回调函数。

**Examples**
```js
// AJAX
$('#tree').jstree({
    'core' : {
        'data' : {
            'url' : '/get/children/',
            'data' : function (node) {
                return { 'id' : node.id };
            }
        }
    });

// direct data
$('#tree').jstree({
    'core' : {
        'data' : [
            'Simple root node',
            {
                'id' : 'node_2',
                'text' : 'Root node with options',
                'state' : { 'opened' : true, 'selected' : true },
                'children' : [ { 'text' : 'Child 1' }, 'Child 2']
            }
        ]
    }
});

// function
$('#tree').jstree({
    'core' : {
        'data' : function (obj, callback) {
            callback.call(this, ['Root 1', 'Root 2']);
        }
    });
```




## $.jstree.defaults.core.strings
配置在树整个过程中出现的文字。

- 可以是一个对象，对象中的 key、value 对应你要替换的内容。

- 可以是一个函数，此函数将接收一个参数（将用到的字符串），并应返回一个替代的字符串。

**Examples**
```js
// function
$('#tree').jstree({
    'core' : {
        'data' : function (obj, callback) {
            callback.call(this, ['Root 1', 'Root 2']);
        }
    });
```



## $.jstree.defaults.core.check_callback
当用户想修改树的结构时，此参数用于决定是否允许修改 或 如何修改。

- `false`，所有操作（创建 create、重命名 rename、删除 delete、移动 move、复制 copy）都将被阻止。
- `true`，所有操作都被允许。
- 函数，更详细的逻辑控制。

**Examples**
```js
$('#tree').jstree({
    'core' : {
        'check_callback' : function (operation, node, node_parent, node_position, more) {
            // operation can be 'create_node', 'rename_node', 'delete_node', 'move_node' or 'copy_node'
            // in case of 'rename_node' node_position is filled with the new node name
            return operation === 'rename_node' ? true : false;
        }
    }
});
```



## $.jstree.defaults.core.error
出错时（树操作被阻止、AJAX 失败等）的回调函数。
此回调函数将接收一个参数。



## $.jstree.defaults.core.animation
展开、折叠时的动画过渡时间。

- 默认：200
- `false`：禁用动画过渡
- 数字：单位 毫秒




## $.jstree.defaults.core.multiple
是否允许节点多选。




## $.jstree.defaults.core.themes
一个对象，用于配置主题。




## $.jstree.defaults.core.themes.name
主题的名字（若为`false`，则使用默认主题）




## $.jstree.defaults.core.themes.url
主题对应的 CSS 文件的 URL。

- 字符串：URL
- `false`：不加载额外的 CSS 文件（因为你可在页面手动包含主题的 CSS 文件）
- `true`：jstree 将尝试自动加载主题 CSS 文件



## $.jstree.defaults.core.themes.dir
所有主题的目录。

只有当`url`的值为`true`时才生效。




## $.jstree.defaults.core.themes.dots
boolean，是否显示树连接线。




## $.jstree.defaults.core.themes.icons
boolean，是否显示节点的图标。




## $.jstree.defaults.core.themes.ellipsis
boolean，节点名过长时是否显示省略号。

仅当容器是固定宽度时（fixed width）才生效。



## $.jstree.defaults.core.themes.stripes
背景是否显示间纹。



## $.jstree.defaults.core.themes.variant
字符串（或`false`），指定主题的形态变化（前提是主题支持形态变化，如大小）。




## $.jstree.defaults.core.themes.responsive
boolean（默认`false`），是否使用主题的响应式状态（遇到小屏设备时）。



## $.jstree.defaults.core.expand_selected_onload
boolean，决定是否在加载树时展开所有选中的节点。



## $.jstree.defaults.core.worker
默认`true`。

当为`true`时，将尽可能使用 web worker（译注：理解为多线程） 来解释接收到的 JSON 数据，
这样的好处是有较大的请求时，不容易使 UI 变卡顿。

注意的是，使用 web worker 时，将慢约 30%。



## $.jstree.defaults.core.force_text
boolean（默认`false`），强制将节点的 text 值解释为纯文本。



## $.jstree.defaults.core.dblclick_toggle
boolean（默认`true`），双击节点名时是否选择（toggled）节点。




## plugin (deco [, opts]) - -  `private`
用于为实例设置插件，仅内部使用。

| 参数/返回 |   描述   |
| -------- | ------ |
| `deco`   | `String` 插件名 |
| `opts`   | `Object` 插件的配置 |
| `返回`   | `jsTree` |




## init (el, optons) - -  `private`
初始化实例，仅内部使用。

| 参数/触发 |   描述   |
| -------- | ------ |
| `el`     | `DOMElement` `jQuery` `String` 将要成为树元素 |
| `options` | `Object` 实例的配置 |
| `触发器（Triggers）` | `init.jstree` `loading.jstree` `loaded.jstree` `ready.jstree` `changed.jstree` |





## init.jstree （ Event ⚡ ）
当所有事件都已绑定后触发。





## loading.jstree （ Event ⚡ ）
在加载文本（loading text）已显示，且在加载（loading）开始之前，触发。





## destroy ()
销毁一个实例。

| 参数 |   描述   |
| -------- | ------ |
| `keep_html` | `Boolean` 若为`true`，树容器将被清空，否则将保持原状 |





## 创建节点原型（Create prototype node）



## teardown () - -  `private`
销毁实例的其中一步，仅内部使用。



## bind () - -  `private`
绑定所有事件，仅内部使用。




## loaded.jstree （ Event ⚡ ）
当根节点（root）第一次加载时触发。



## ready.jstree （ Event ⚡ ）
当所有节点都加载完毕时触发。



## unbind () - -  `private`
销毁实例的其中一步，仅内部使用。



## trigger (ev [, data]) - -  `private`
触发一个事件，仅内部使用。

| 参数 |   描述   |
| -------- | ------ |
| `ev` | `String` 要触发的事件名称 |
| `data` | `Object` 传递给事件的附加数据 |



## get_container ()
返回扩展自 jQuery 的实例容器。

| 返回 |   描述   |
| -------- | ------ |
| `返回` | `jQuery` |




## get_container_ul () - -  `private`
返回扩展自 jQuery 的主 UL 元素节点（树实例容器中），仅内部使用。

| 返回 |   描述   |
| -------- | ------ |
| `返回` | `jQuery` |


## get_string (key) - -  `private`
获取树中用到的字符串（本地化），仅内部使用。

| 参数/返回 |   描述   |
| -------- | ------ |
| `key` | `String` |
| `返回` | `String` |




## _firstChild (dom) - -  `private`
获取 DOM 节点中的第一个子元素，仅内部使用。

| 参数/返回 |   描述   |
| -------- | ------ |
| `dom` | `DOMElement` |
| `返回` | `DOMElement` |




## _nextSibling (dom) - -  `private`
获取 DOM 节点的下一个兄弟节点，仅内部使用。

| 参数/返回 |   描述   |
| -------- | ------ |
| `dom` | `DOMElement` |
| `返回` | `DOMElement` |




## _previousSibling (dom) - -  `private`
获取 DOM 节点的上一个兄弟节点，仅内部使用。

| 参数/返回 |   描述   |
| -------- | ------ |
| `dom` | `DOMElement` |
| `返回` | `DOMElement` |




## get_node (obj [, as_dom])
根据输入（子 DOM 元素、ID字符串、选择器等）获取节点的 JSON 形式数据（或 扩展自 jQuery 的 DOM 节点）。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `as_dom` | `Boolean` |
| `返回`   | `Object` `jQuery` |




## get_path (obj [, glue, ids])
获取节点的路径。可能是
- 一堆节点名称
- 一堆节点ID
- 一堆节点名和 ID（或数组）

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` 节点 |
| `glue`   | `String` 若是字符串，则填间隔字符串（如`/`），若是一个假值（[译注](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)），则返回数组 |
| `ids`    | `Boolean` 若为`true`则用节点ID 构建路径，否则用节点名称 |
| `返回`   | `mixed` |




## get_next_dom (obj [, strict])
获取`obj`节点的下一个可见节点，若`strict`为`true`，则只可能返回兄弟节点。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `strict` | `Boolean` |
| `返回`   | `jQuery` |



## get_prev_dom (obj [, strict])
获取`obj`节点的前一个可见节点，若`strict`为`true`，则只可能返回兄弟节点。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `strict` | `Boolean` |
| `返回`   | `jQuery` |




## get_parent (obj)
获取节点的父节点。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `返回`   | `String` |




## get_children_dom (obj)
获取节点的所有子节点（jQuery 集合）（节点必须是已渲染的）。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `返回`   | `jQuery` |



## is_parent (obj)
判断一个节点是否包含子节点。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `返回`   | `Boolean` |




## is_loaded (obj)
判断一个节点是否已加载（其子节点已可用）。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `返回`   | `Boolean` |




## is_loading (obj)
判断一个节点是否正在加载（正在拉取子节点）。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `返回`   | `Boolean` |




## is_open (obj)
判断一个节点是否已展开。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `返回`   | `Boolean` |




## is_closed (obj)
判断一个节点是否关闭状态。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `返回`   | `Boolean` |




## is_leaf (obj)
判断一个节点是不是没包含子节点。

| 参数/返回 |   描述   |
| -------- | ------ |
| `obj`    | `mixed` |
| `返回`   | `Boolean` |




## load_node (obj [, callback])
加载一个节点（即使用 `core.data` 的设置来拉取子节点），支持传入多个节点（数组形式）。

| 参数/返回/触发器 |   描述   |
| --------------- | ------ |
| `obj`           | `mixed` |
| `callback`      | `function` 加载完毕的回调，将在实例的范围中执行，并接收两个参数：节点、boolean 状态 |
| `返回`          | `Boolean` |
| `触发器`        | `load_node.jstree` |




## load_node.jstree （ Event ⚡ ）
一个节点加载完毕后触发。

| 参数 |   描述   |
| ----- | ------ |
| `node`   | `Object` 已加载的节点 |
| `status` | `Boolean` 是否加载成功 |




## _load_nodes (nodes [, callback]) - -  `private`
加载多个节点（数组）（只有出现在结构中，也会加载不可用的节点），仅内部使用。

| 参数 |   描述   |
| ----- | ------ |
| `node`   | `array` |
| `callback` | `function` 加载完毕的回调，将在实例的范围中执行，并接收 1 个参数：传入的那些节点（数组） |




## load_all ([obj, callback])
加载所有仍未加载的节点。

| 参数 |   描述   |
| ----- | ------ |
| `node`   | `mixed` 加载节点下的所有节点，而非整棵树的所有节点 |
| `status` | `function` 加载成功的回调 |
| `触发器`  | `load_all.jstree` |



## load_all.jstree （ Event ⚡ ）
`load_all`执行完毕后触发。

| 参数 |   描述   |
| ----- | ------ |
| `node`   | `Object` 已递归加载的节点 |




## _load_node (obj [, callback]) - -  `private`
真正处理一个节点的加载过程，仅内部使用。

| 参数/返回 | 描述 |
| ----- | ------ |
| `obj` | `mixed` |
| `callback` | `function` 加载完毕后执行此回调函数，此函数允许在实例范围内，并将接收 1 个状态参数（boolean） |
| `返回` | `Boolean` |




## _node_changed (obj [, callback]) - -  `private`
添加一个节点到将要重绘的节点列表中，仅内部使用。

| 参数 |   描述   |
| ----- | ------ |
| `obj` | `mixed` |




## _append_html_data (obj, data) - -  `private`
添加 HTML 内容到树，仅内部使用。

| 参数/触发器 | 描述 |
| ----- | ------ |
| `obj` | `mixed` 要添加到的节点 |
| `data` | `String` HTML 字符串 |
| `触发器` | `model.jstree` `changed.jstree` |





## model.jstree （ Event ⚡ ）
当新数据插入到树模型（tree model）中时触发。

| 参数   | 描述 |
| :----- | :------ |
| `nodes` | `Array` 节点ID 数组 |
| `parent` | `String` 这些节点的父节点ID |





## _append_json_data (obj, data) - -  `private`
添加 JSON 内容到树，仅内部使用。

| 参数/触发器 | 描述 |
| ----- | ------ |
| `obj` | `mixed` 要添加到的节点 |
| `data` | `String` JSON 对象字符串 |
| `force_processing` | `Boolean` 内部参数（无需设置） |
| `触发器` | `model.jstree` `changed.jstree` |





## _parse_model_from_html (d [, p, ps]) - -  `private`
从jQuery对象中解释节点，并添加到树的内存模型中，仅内部使用。

| 参数/返回 | 描述 |
| ----- | ------ |
| `d` | `jQuery`jQuery对象 |
| `p` | `String` 父节点ID |
| `ps` | `Array` 所有的父节点列表 |
| `返回` | `String` 将被添加到模型中的节点ID |





## _parse_model_from_flat_json (d [, p, ps]) - -  `private`
从 JSON 对象中解释节点（用于处理扁平数据，即无嵌套的子节点，但这些子节点拥有 ID 和 父节点ID），
并添加到树的内存模型中，仅内部使用。

| 参数/返回 | 描述 |
| ----- | ------ |
| `d` | `Object` JSON 对象 |
| `p` | `String` 父节点ID |
| `ps` | `Array` 所有的父节点列表 |
| `返回` | `String` 将被添加到模型中的节点ID |





## _parse_model_from_json (d [, p, ps]) - -  `private`
从 JSON 对象中解释节点，并添加到树的内存模型中，仅内部使用。

| 参数/返回 | 描述 |
| ----- | ------ |
| `d` | `Object` JSON 对象 |
| `p` | `String` 父节点ID |
| `ps` | `Array` 所有的父节点列表 |
| `返回` | `String` 将被添加到模型中的节点ID |





## _redraw () - -  `private`
重绘所有需要重绘的节点，仅内部使用。

| 触发器 | 描述 |
| ----- | ------ |
| `触发器` | `redraw.jstree` |





## redraw.jstree （ Event ⚡ ）
当节点们重绘完毕后触发。

| 参数 | 描述 |
| ----- | ------ |
| `nodes` | `array` 已重绘的节点 |





## redraw ([full])
重绘所有需要重绘的节点，或者 重绘整个树的所有节点。

| 参数 | 描述 |
| ----- | ------ |
| `full` | `Boolean` 若`true`则重绘整个树的所有节点 |





## draw_children (node) - -  `private`
重绘单个节点的子节点，仅内部使用。

| 参数 | 描述 |
| ----- | ------ |
| `node` | `mixed` 节点（将重绘其子节点） |





## redraw_node (node, deep, is_callback, force_render) - -  `private`
重绘单个节点，仅内部使用。

| 参数 | 描述 |
| ----- | ------ |
| `node` | `mixed` 将要重绘的节点 |
| `deep` | `Boolean` 是否也重绘子节点 |
| `is_callback` | `Boolean` 是否递归调用 |
| `force_render` | `Boolean` 是否也重绘父节点未展开的子节点 |





## open_node (obj [, callback, animation])
展开一个节点，看到其子节点（原文：revaling its children）。
若此节点还未被加载，将先加载此节点，再展开。

| 参数/触发器 | 描述 |
| ----- | ------ |
| `obj` | `mixed` 将要展开的节点 |
| `callback` | `Function` 节点展开完毕后的回调 |
| `animation` | `Number` 展开节点时的动画过渡时间（毫秒）（覆盖`core.animation`的设置），若为`false`则禁用动画效果 |
| `触发器` | `open_node.jstree` `after_open.jstree` `before_open.jstree` |





## before_open.jstree （ Event ⚡ ）
当一个节点即将被展开时触发（if the node is supposed to be in the DOM, it will be, but it won't be visible yet）。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 将展开的节点 |





## open_node.jstree （ Event ⚡ ）






## after_open.jstree （ Event ⚡ ）






## _open_to (obj) - -  `private`






## close_node (obj [, animation])






## close_node.jstree （ Event ⚡ ）






## after_close.jstree （ Event ⚡ ）






## toggle_node (obj)






## open_all ([obj, animation, original_obj])






## open_all.jstree （ Event ⚡ ）






## close_all ([obj, animation])






## close_all.jstree （ Event ⚡ ）






## is_disabled (obj)






## enable_node (obj)






## enable_node.jstree （ Event ⚡ ）






## disable_node (obj)






## disable_node.jstree （ Event ⚡ ）






## is_hidden (obj)






## hide_node (obj)






## hide_node.jstree （ Event ⚡ ）






## show_node (obj)






## show_node.jstree （ Event ⚡ ）






## hide_all ()






## hide_all.jstree （ Event ⚡ ）






## show_all ()






## show_all.jstree （ Event ⚡ ）






## activate_node (obj, e) - -  `private`






## activate_node.jstree （ Event ⚡ ）






## hover_node (obj) - -  `private`






## hover_node.jstree （ Event ⚡ ）






## dehover_node (obj) - -  `private`






## dehover_node.jstree （ Event ⚡ ）






## select_node (obj [, supress_event, prevent_open])






## select_node.jstree （ Event ⚡ ）






## changed.jstree （ Event ⚡ ）






## deselect_node (obj [, supress_event])






## deselect_node.jstree （ Event ⚡ ）






## select_all ([supress_event])






## select_all.jstree （ Event ⚡ ）






## deselect_all ([supress_event])






## deselect_all.jstree （ Event ⚡ ）






## is_selected (obj)






## get_selected ([full])






## get_top_selected ([full])






## get_bottom_selected ([full])






## get_state () - -  `private`






## set_state (state [, callback]) - -  `private`






## set_state.jstree （ Event ⚡ ）






## refresh ()






## refresh.jstree （ Event ⚡ ）






## refresh_node (obj)






## refresh_node.jstree （ Event ⚡ ）






## set_id (obj, id)






## set_id.jstree （ Event ⚡ ）






## get_text (obj)






## set_text (obj, val) - -  `private`






## set_text.jstree （ Event ⚡ ）






## get_json ([obj, options])






## create_node ([par, node, pos, callback, is_loaded])






## create_node.jstree （ Event ⚡ ）






## rename_node (obj, val)






## rename_node.jstree （ Event ⚡ ）






## delete_node (obj)






## delete_node.jstree （ Event ⚡ ）






## check (chk, obj, par, pos) - -  `private`






## last_error ()






## move_node (obj, par [, pos, callback, is_loaded])






## move_node.jstree （ Event ⚡ ）






## copy_node (obj, par [, pos, callback, is_loaded])






## copy_node.jstree （ Event ⚡ ）






## cut (obj)






## cut.jstree （ Event ⚡ ）






## copy (obj)






## copy.jstree （ Event ⚡ ）






## get_buffer ()






## can_paste ()






## paste (obj [, pos])






## paste.jstree （ Event ⚡ ）






## clear_buffer ()






## clear_buffer.jstree （ Event ⚡ ）






## edit (obj [, default_text, callback])






## set_theme (theme_name [, theme_url])






## set_theme.jstree （ Event ⚡ ）






## get_theme ()






## set_theme_variant (variant_name)






## get_theme ()






## show_stripes ()






## show_stripes.jstree （ Event ⚡ ）






## hide_stripes ()






## hide_stripes.jstree （ Event ⚡ ）






## toggle_stripes ()






## show_dots ()






## show_dots.jstree （ Event ⚡ ）






## hide_dots ()






## hide_dots.jstree （ Event ⚡ ）






## toggle_dots ()






## show_icons ()






## show_icons.jstree （ Event ⚡ ）






## hide_icons ()






## hide_icons.jstree （ Event ⚡ ）






## toggle_icons ()






## show_icons ()






## show_ellipsis.jstree （ Event ⚡ ）






## hide_ellipsis ()






## hide_ellipsis.jstree （ Event ⚡ ）






## toggle_icons ()






## set_icon (obj, icon)






## get_icon (obj)






## hide_icon (obj)






## show_icon (obj)