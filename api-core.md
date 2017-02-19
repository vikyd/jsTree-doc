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




## $.jstree.reference (needle)
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
打开、折叠时的动画过渡时间。

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
boolean，决定是否在加载树时打开所有选中的节点。




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
判断一个节点是否已打开。

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

| 参数/返回/触发 |   描述   |
| --------------- | ------ |
| `obj`           | `mixed` |
| `callback`      | `function` 加载完毕的回调，将在实例的范围中执行，并接收两个参数：节点、boolean 状态 |
| `返回`          | `Boolean` |
| `触发事件`        | `load_node.jstree` |




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
| `触发事件`  | `load_all.jstree` |




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

| 参数/触发 | 描述 |
| ----- | ------ |
| `obj` | `mixed` 要添加到的节点 |
| `data` | `String` HTML 字符串 |
| `触发事件` | `model.jstree` `changed.jstree` |




## model.jstree （ Event ⚡ ）
当新数据插入到树模型（tree model）中时触发。

| 参数   | 描述 |
| :----- | :------ |
| `nodes` | `Array` 节点ID 数组 |
| `parent` | `String` 这些节点的父节点ID |




## _append_json_data (obj, data) - -  `private`
添加 JSON 内容到树，仅内部使用。

| 参数/触发 | 描述 |
| ----- | ------ |
| `obj` | `mixed` 要添加到的节点 |
| `data` | `String` JSON 对象字符串 |
| `force_processing` | `Boolean` 内部参数（无需设置） |
| `触发事件` | `model.jstree` `changed.jstree` |




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

| 触发 | 描述 |
| ----- | ------ |
| `触发事件` | `redraw.jstree` |




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
| `force_render` | `Boolean` 是否也重绘父节点未打开的子节点 |




## open_node (obj [, callback, animation])
打开一个节点，看到其子节点（原文：revaling its children）。
若此节点还未被加载，将先加载此节点，再打开。

| 参数/触发 | 描述 |
| ----- | ------ |
| `obj` | `mixed` 将要打开的节点 |
| `callback` | `Function` 节点打开完毕后的回调 |
| `animation` | `Number` 打开节点时的动画过渡时间（毫秒）（覆盖`core.animation`的设置），若为`false`则禁用动画效果 |
| `触发事件` | `open_node.jstree` `after_open.jstree` `before_open.jstree` |




## before_open.jstree （ Event ⚡ ）
当一个节点即将被打开时触发（if the node is supposed to be in the DOM, it will be, but it won't be visible yet）。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 将打开的节点 |




## open_node.jstree （ Event ⚡ ）
当一个节点打开完毕时触发（若有过渡动画，此时动画应该还没完毕）。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 打开完毕的节点 |




## after_open.jstree （ Event ⚡ ）
当一个节点打开完毕，且过渡动画也已完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 打开完毕的节点 |




## _open_to (obj) - -  `private`
打开节点的所有父节点（此时节点应已加载）

| 参数 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需显示的节点 |




## close_node (obj [, animation])
关闭一个节点，并隐藏其子节点

| 参数 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需关闭的节点 |
| `animation` | `Number` 关闭节点时的动画过渡时间（毫秒）（覆盖`core.animation`的设置），若为`false`则禁用动画效果 |
| `触发事件` | `close_node.jstree` `after_close.jstree` |




## close_node.jstree （ Event ⚡ ）
当一个节点关闭完毕时触发（若有过渡动画，此时动画应该还没完毕）。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 关闭完毕的节点 |




## after_close.jstree （ Event ⚡ ）
当一个节点关闭完毕，且过渡动画也已完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 关闭完毕的节点 |




## toggle_node (obj)
切换节点的状态，若已打开则关闭节点，若已关闭则打开节点。

| 参数 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需切换状态的节点 |




## open_all ([obj, animation, original_obj])
打开一个节点或整棵树的内所有节点，显示其子节点。
若节点还没加载，则先加载节点，完毕再打开节点。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需递归打开的节点，若忽略则打开整棵树的所有节点 |
| `animation` | `Number` 打开节点时动画的过渡时间（毫秒），默认禁用动画效果 |
| `reference` | `jQuery` 开始处理的节点（内部使用） |
| `触发事件` | `open_all.jstree` |




## open_all.jstree （ Event ⚡ ）
当`open_all`完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 已打开的节点 |




## close_all ([obj, animation])
关闭一个节点或整棵树的所有节点（后面这句没懂：revaling their children）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需递归关闭的节点，若忽略则关闭整棵树的所有节点 |
| `animation` | `Number` 打开节点时动画的过渡时间（毫秒），默认禁用动画效果 |
| `触发事件` | `close_all.jstree` |




## close_all.jstree （ Event ⚡ ）
当`close_all`完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 关闭完毕的节点 |




## is_disabled (obj)
检查一个节点是否被禁用了（即不可被选中）。

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed`  |
| `返回` | `Boolean` |




## enable_node (obj)
启用一个节点（这样节点才可被选中）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需启用的节点 |
| `触发事件` | `enable_node.jstree` |




## enable_node.jstree （ Event ⚡ ）
当一个节点被启用时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 需启用的节点 |




## disable_node (obj)
禁用一个节点（这样节点不可被选中）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需禁用的节点 |
| `触发事件` | `disable_node.jstree` |




## disable_node.jstree （ Event ⚡ ）
当一个节点被禁用时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 需禁用的节点 |




## is_hidden (obj)
检查一个节点是否被隐藏了。

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `返回` | `Boolean` |




## hide_node (obj)
隐藏一个节点（仍在树结构中，只是看不见了）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需隐藏的节点 |
| `skip_redraw` | `Boolean` 是否需要重绘，内部参数 |
| `触发事件` | `hide_node.jstree` |




## hide_node.jstree （ Event ⚡ ）
当一个节点被隐藏时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 被隐藏的节点 |




## show_node (obj)
显示一个节点。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需显示的节点 |
| `skip_redraw` | `Boolean` 是否需要重绘，内部参数 |
| `触发事件` | `show_node.jstree` |




## show_node.jstree （ Event ⚡ ）
当一个节点被显示时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 显示的节点 |




## hide_all ()
隐藏所有节点。

| 触发 | 描述 |
| :----- | :------ |
| `触发事件` | `hide_node.jstree` |




## hide_all.jstree （ Event ⚡ ）
当所有节点被隐藏时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Array` 所有被隐藏节点的 ID 集合 |




## show_all ()
显示所有节点。

| 触发 | 描述 |
| :----- | :------ |
| `触发事件` | `show_all.jstree` |




## show_all.jstree （ Event ⚡ ）
当所有节点被显示时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Array` 所有被显示节点的 ID 集合 |




## activate_node (obj, e) - -  `private`
当用户选中一个节点时被调用，仅内部使用。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `e` | `Object` 相关的事件 |
| `触发事件` | `activate_node.jstree` `changed.jstree` |




## activate_node.jstree （ Event ⚡ ）
当一个节点被用户点击或交互时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Object` |
| `event` | `Object` 触发调用的原始事件（也可能是一个空对象） |




## hover_node (obj) - -  `private`
当用户鼠标移过节点时，使节点的状态变为`鼠标经过`状态，仅内部使用。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |
| `触发事件` | `hover_node.jstree` |




## hover_node.jstree （ Event ⚡ ）
当用户鼠标经过节点时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Object` |




## dehover_node (obj) - -  `private`
当用户鼠标离开节点时，使移除节点的`鼠标经过`状态，仅内部使用。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |
| `触发事件` | `dehover_node.jstree` |




## dehover_node.jstree （ Event ⚡ ）
当用户鼠标离开节点时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Object` |




## select_node (obj [, supress_event, prevent_open])
选择一个节点。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需选中的节点数组 |
| `supress_event` | `Boolean` 若为`true`，将不触发`changed.jstree`事件 |
| `prevent_open` | `Boolean` 若为`true`，将不打开选中节点的父节点 |
| `触发事件` | `select_node.jstree` `changed.jstree` |




## select_node.jstree （ Event ⚡ ）
当节点被选中时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Object` |
| `selected` | `Array` 已选中的节点 |
| `event` | `Object` 触发本事件`select_node`的事件 |




## changed.jstree （ Event ⚡ ）
当已选中的节点发生变化（`选择`发生变化）时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Object` |
| `action` | `Object` 引起`选择`发生变化的`action` |
| `selected` | `Array` 当前的已选中的节点 |
| `event` | `Object` 触发本事件`changed_node`的事件 |




## deselect_node (obj [, supress_event])
不选中节点。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 若为一个数组，则是需被不选中的节点列表 |
| `supress_event` | `Boolean` 若为`true`，将不触发`changed.jstree`事件 |
| `触发事件` | `deselect_node.jstree` `changed.jstree` |




## deselect_node.jstree （ Event ⚡ ）
当节点被从`选中`变为`不选中`状态时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Object` |
| `selected` | `Array` 当前的已选中的节点 |
| `event` | `Object` 触发本事件`deselect_node`的事件 |




## select_all ([supress_event])
选中树的所有节点。

| 参数/触发 | 描述 |
| `supress_event` | `Boolean` 若为`true`，将不触发`changed.jstree`事件 |
| `触发事件` | `deselect_node.jstree` `changed.jstree` |




## select_all.jstree （ Event ⚡ ）
当树中所有节点都被选中时触发。

| 参数 | 描述 |
| :----- | :------ |
| `selected` | `Array` 当前的已选中的节点 |




## deselect_all ([supress_event])
不选中树中所有节点。

| 参数/触发 | 描述 |
| :----- | :------ |
| `supress_event` | `Boolean` 若为`true`，将不触发`changed.jstree`事件 |
| `触发事件` | `deselect_all.jstree` `changed.jstree` |




## deselect_all.jstree （ Event ⚡ ）
当树中所有节点状态变为不选中时触发。

| 参数 | 描述 |
| :----- | :------ |
| `nodes` | `Object` 之前的选中节点 |
| `selected` | `Array` 当前的已选中的节点 |




## is_selected (obj)
检查一个节点是否已被选中。

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |
| `返回` | `Boolean` |




## get_selected ([full])
获取所有已选中的节点。

| 参数/返回 | 描述 |
| :----- | :------ |
| `full` | `mixed` 若为`true`则返回节点对象全部数据，否则只返回节点 ID 列表 |
| `返回` | `Array` |




## get_top_selected ([full])
获取顶层的被选中节点。

| 参数/返回 | 描述 |
| :----- | :------ |
| `full` | `mixed` 若为`true`则返回节点对象全部数据，否则只返回节点 ID 列表 |
| `返回` | `Array` |




## get_bottom_selected ([full])
获取底层的被选中节点。

| 参数/返回 | 描述 |
| :----- | :------ |
| `full` | `mixed` 若为`true`则返回节点对象全部数据，否则只返回节点 ID 列表 |
| `返回` | `Array` |




## get_state () - -  `private`
获取树目前的状态（之后可使用`set_state(state)`来恢复状态），仅内部使用。

| 返回 | 描述 |
| :----- | :------ |
| `返回` | `Object` |




## set_state (state [, callback]) - -  `private`
设置树的状态，仅内部使用。

| 参数/触发 | 描述 |
| :----- | :------ |
| `state` | `Object` 要设置的状态。此对象是传引用，且 jstree 不会修改此对象 |
| `callback` | `Function` 可选，设置状态完毕后的回调函数 |
| `触发事件` | `set_state.jstree` |




## set_state.jstree （ Event ⚡ ）
当`set_state`完毕时触发。




## refresh ()
刷新树，所有的节点都将重新加载，并触发`load_node`。

| 参数/触发 | 描述 |
| :----- | :------ |
| `skip_loading` | `Boolean` 是否跳过加载动画 |
| `forget_state` | `Mixed` 若为`true`则将不可恢复原来的状态，若为一个函数（此函数将接收一个状态参数）则此函数的结果将作为状态 |
| `触发事件` | `refresh.jstree` |




## refresh.jstree （ Event ⚡ ）
当`refresh`完毕时触发。




## refresh_node (obj)
刷新一个节点（并重新加载其子节点，并触发`load_node`）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `Mixed` 节点 |
| `触发事件` | `refresh_node.jstree` |




## refresh_node.jstree （ Event ⚡ ）
当节点刷新完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` 已刷新的节点 |
| `nodes` | `Array` 已重新加载的节点 ID 列表 |




## set_id (obj, id)
设置节点 ID。

| 参数/返回/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `id` | `String` 新 ID |
| `返回` | `Boolean` |
| `触发事件` | `set_id.jstree` |




## set_id.jstree （ Event ⚡ ）
当节点的 ID 变化完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `node` | `Object` |
| `old` | `String` 旧 ID |




## get_text (obj)
获取节点名（text）

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点 |
| `返回` | `String` |




## set_text (obj, val) - -  `private`
设置节点的名称。仅内部使用。请使用`rename_node(obj, val)`

| 参数/返回/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 单个节点，或，多个节点组成的数组 |
| `val` | `String` 新名称 |
| `返回` | `Boolean` |
| `触发事件` | `set_text.jstree` |




## set_text.jstree （ Event ⚡ ）
当节点的名称变化完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `obj` | `Object` |
| `text` | `String` 新名称 |




## get_json ([obj, options])
获取一个节点（或整棵树）的 JSON 形式数据。

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |
| `options` | `Object` |
| `options.no_state` | `Boolean` 不包含状态 |
| `options.no_id` | `Boolean` 不包含 ID |
| `options.no_children` | `Boolean` 不包含子节点 |
| `options.no_data` | `Boolean` 不包含节点数据（node data） |
| `options.no_li_attr` | `Boolean` 不包含`LI`元素的属性`attributes` |
| `options.no_a_attr` | `Boolean` 不包含`A`元素的属性`attributes` |
| `options.flat` | `Boolean` 返回扁平 JSON 数据，而不是嵌套数据 |
| `返回` | `Object` |




## create_node ([par, node, pos, callback, is_loaded])
创建一个新节点（不要和`load_node`搞混）。

| 参数/返回/触发 | 描述 |
| :----- | :------ |
| `par` | `mixed` 父节点（若是创建根节点请用`#`或`null`） |
| `node` | `mixed` 新节点的数据（JSON 对象，或节点名字符串） |
| `pos` | `mixed` 插入节点的位置（index），支持`first`和`last`，默认是`last` |
| `callback` | `Function` 节点创建完毕后的毁回调函数 |
| `is_loaded` | `Boolean` 内部参数，用于检测父节点是否已成功加载 |
| `返回` | `String` 新建节点的 ID |
| `触发事件` | `model.jstree` `create_node.jstree` |




## create_node.jstree （ Event ⚡ ）
当节点创建完毕时触发。

| `node` | `Object` |
| `parent` | `String` 父节点 ID |
| `position` | `Number` 新节点在父节点中的位置 |




## rename_node (obj, val)
重命名节点。

| 参数/返回/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点，也可是一个数组，里面的节点将重命名为相同的名字 |
| `val` | `String` 新名称 |
| `返回` | `Boolean` |
| `触发事件` | `rename_node.jstree` |




## rename_node.jstree （ Event ⚡ ）
当节点重命名完毕时触发。

| `node` | `Object` |
| `text` | `String` 新名称 |
| `old` | `Number` 旧名称 |




## delete_node (obj)
删除节点。

| 参数/返回/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 节点，也可是一个数组，将同时删除多个 |
| `返回` | `Boolean` |
| `触发事件` | `delete_node.jstree` `changed.jstree` |




## delete_node.jstree （ Event ⚡ ）
当节点删除完毕时触发。

| `node` | `Object` |
| `parent` | `String` 父节点 ID |




## check (chk, obj, par, pos) - -  `private`
检查此树是否允许某种操作，仅内部使用。

| 参数/返回 | 描述 |
| :----- | :------ |
| `chk` | `String` 操作名，可以是`create_node` `rename_node` `delete_node` `copy_node` `move_node` |
| `obj` | `mixed` 节点 |
| `par` | `mixed` 父节点 |
| `pos` | `mixed` 插入的位置，或`rename_node`时的新名称 |
| `more` | `mixed` 各种附加信息，如 DND 插件触发 `move_node` 操作时，此值就是`鼠标经过的节点` |
| `返回` | `Boolean` |




## last_error ()
获取最后的错误信息。

| 返回 | 描述 |
| :----- | :------ |
| `返回` | `Object` |




## move_node (obj, par [, pos, callback, is_loaded])
移动节点到新的父节点。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需移动的节点（也可以是一个节点数组） |
| `par` | `mixed` 新的父节点 |
| `pos` | `mixed` 插入节点的位置（除了整数值，还支持`first` `last` `before` `after`）默认是整数`0` |
| `callback` | `Function` 节点移动完毕后的毁回调函数，接收 3 个参数：节点、新父节点、位置 |
| `is_loaded` | `Boolean` 内部参数，用于检测父节点是否已成功加载 |
| `skip_redraw` | `mixed` 内部参数，是否重画整棵树 |
| `instance` | `mixed` 内部参数，检测节点是否来自另一个树实例 |
| `触发事件` | `move_node.jstree` |




## move_node.jstree （ Event ⚡ ）
当节点移动完毕时触发。

| `node` | `Object` |
| `parent` | `String` 父节点 ID |
| `position` | `String` 节点在父节点中的位置 |
| `old_parent` | `String` 旧的父节点 |
| `ol_position` | `String` 旧的节点位置 |
| `is_multi` | `String` 节点、新的父节点是否属于不同的树实例 |
| `old_instance` | `String` 节点来自的树实例 |
| `new_instance` | `String` 新父节点来自的树实例 |




## copy_node (obj, par [, pos, callback, is_loaded])
复制节点到新的父节点。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需复制的节点（也可以是一个节点数组） |
| `par` | `mixed` 新的父节点 |
| `pos` | `mixed` 插入节点的位置（除了整数值，还支持`first` `last` `before` `after`）默认是整数`0` |
| `callback` | `Function` 节点复制完毕后的毁回调函数，接收 3 个参数：节点、新父节点、位置 |
| `is_loaded` | `Boolean` 内部参数，用于检测父节点是否已成功加载 |
| `skip_redraw` | `mixed` 内部参数，是否重画整棵树 |
| `instance` | `mixed` 内部参数，检测节点是否来自另一个树实例 |
| `触发事件` | `model.jstree` `copy_node.jstree` |




## copy_node.jstree （ Event ⚡ ）
当节点复制完毕时触发。

| `node` | `Object` 已复制的节点 |
| `original` | `Object` 原来的节点 |
| `parent` | `String` 父节点 ID |
| `position` | `String` 节点在父节点中的位置 |
| `old_parent` | `String` 旧的父节点 |
| `ol_position` | `String` 旧节点的位置 |
| `is_multi` | `String` 节点、新的父节点是否属于不同的树实例 |
| `old_instance` | `String` 节点来自的树实例 |
| `new_instance` | `String` 新父节点来自的树实例 |




## cut (obj)
剪切节点（之后需调用`paste(obj)`粘贴节点）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需剪切的节点（也可以是一个节点数组） |
| `触发事件` | `cut.jstree` |




## cut.jstree （ Event ⚡ ）
当节点添加到缓存区待移动时触发。

| `node` | `Array` |




## copy (obj)
复制节点（之后需调用`paste(obj)`粘贴节点）。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 需复制的节点（也可以是一个节点数组） |
| `触发事件` | `copy.jstree` |




## copy.jstree （ Event ⚡ ）
当节点添加到缓存区待复制时触发。

| 参数 | 描述 |
| `node` | `Array` |




## get_buffer ()
获取当前的缓存（缓存是一些待粘贴的节点）。

| 返回 | 描述 |
| :----- | :------ |
| `返回` | `Object` 一个对象，包含：状态`mode`（`copy_node`或`move_node`）、节点`node`（节点数组）、实例`instance`（树实例） |




## can_paste ()
检测缓存中是否有东西待粘贴。

| 返回 | 描述 |
| :----- | :------ |
| `返回` | `Boolean` |




## paste (obj [, pos])
复制或移动之前剪切或复制的节点到新父节点中。

| 参数/触发 | 描述 |
| :----- | :------ |
| `obj` | `mixed` 新父节点 |
| `pos` | `mixed` 插入的位置（除了整数，也支持`first` `last`），默认值`0` |
| `触发事件` | `paste.jstree` |




## paste.jstree （ Event ⚡ ）
当粘贴操作完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `parent` | `String` 接收粘贴节点的 ID |
| `node` | `Array` 缓存中的节点列表 |
| `mode` | `String` 执行的操作，`copu_node`或`move_node` |




## clear_buffer ()
清除缓存（因复制、剪切操作产生的）。

| 触发 | 描述 |
| :----- | :------ |
| `触发事件` | `clear_buffer.jstree` |




## clear_buffer.jstree （ Event ⚡ ）
当复制或剪切的缓存被清空完毕时触发。




## edit (obj [, default_text, callback])
使节点进入编辑模式（将出现一个`input`元素，用于重命名节点）。

| 参数 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |
| `default_text` | `String` 默认名称（若不填，或填一个空字符串，则默认为节点目前的名称） |
| `callback` | `Function` 离开编辑框时将执行的回调函数，执行环境是实例内，将接收 3 个参数：节点、状态（`true`则重命名成功，否则失败）、Boolean值（用户是否可取消编辑）。可通过`.text`获取节点名 |




## set_theme (theme_name [, theme_url])
设置主题。

| 参数/触发 | 描述 |
| :----- | :------ |
| `theme_name` | `String` 主题名 |
| `theme_url` | `mixed` 主题的 CSS 文件的 URL，若不填或`false`，则你需手动加载该文件，若`true`则将尝试自动从`core.theme.dir`目录中加载 |
| `触发事件` | `set_theme.jstree` |




## set_theme.jstree （ Event ⚡ ）
当设置主题完毕时触发。

| 参数 | 描述 |
| :----- | :------ |
| `theme` | `String` 主题名 |




## get_theme ()
获取当前的主题名。

| 返回 | 描述 |
| :----- | :------ |
| `返回` | `String` |




## set_theme_variant (variant_name)
设置主题的变体`variant`（如果变体存在的话）。

| 参数 | 描述 |
| :----- | :------ |
| `variant_name` | `String` `Boolean` 主题的变体（若`false`，则移除当前的变体） |




## show_stripes ()
在树容器背景中显示间隔条纹（前提是当前主题支持）




## show_stripes.jstree （ Event ⚡ ）
当间隔条纹显示完毕时触发。




## hide_stripes ()
在树容器背景中显示间隔条纹。




## hide_stripes.jstree （ Event ⚡ ）
当间隔条纹隐藏完毕时触发。




## toggle_stripes ()
消或隐树容器背景中的间隔条纹。




## show_dots ()
在树容器中显示连接线（前提是主题支持）




## show_dots.jstree （ Event ⚡ ）
当连接线显示时触发。




## hide_dots ()
在树容器中隐藏连接线。




## hide_dots.jstree （ Event ⚡ ）
当连接线隐藏时触发。




## toggle_dots ()
消或隐树容器背景中的连接线。




## show_icons ()
显示节点的图标。




## show_icons.jstree （ Event ⚡ ）
当节点图标显示时触发。




## hide_icons ()
因此节点的图标。




## hide_icons.jstree （ Event ⚡ ）
当节点图标隐藏时触发。




## toggle_icons ()
消或隐节点的图标。




## show_ellipsis ()
当节点名过长时，显示过长的部分为`...`。




## show_ellipsis.jstree （ Event ⚡ ）
当节点名过长，显示过长的部分为`...`时触发。（原文：triggered when ellisis is shown）




## hide_ellipsis ()
当节点名过长，不缩略显示。




## hide_ellipsis.jstree （ Event ⚡ ）
当节点名过长，不缩略显示时触发。




## set_icon (obj, icon)
设置节点的图标。

| 参数 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |
| `icon` | `String` 新的图标名，可以是一个图标的文件路径，或 CSS 的 class 名。若使用图标文件路径，则应使用当前目录作为前缀`./`，否则都认为是 CSS 类名 |




## get_icon (obj)
获取节点的图标。

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |
| `返回` | `String` |




## hide_icon (obj)
隐藏单个节点的图标。

| 参数/返回 | 描述 |
| :----- | :------ | 
| `obj` | `mixed` |




## show_icon (obj)
显示单个节点的图标。

| 参数/返回 | 描述 |
| :----- | :------ |
| `obj` | `mixed` |



