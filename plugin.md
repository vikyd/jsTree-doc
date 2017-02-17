# Plugins?

jsTree has some functionality moved out of the core so you can only use it when you need it. To enable a plugin use the plugins config option and add that plugin's name to the array.

For example enabling all the plugins can be done this way: (enable only plugins you need)

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

Here is a quick overview for each one.





# Changed plugin
This plugin adds additional information about selection changes. Once included in the plugins config option, each changed.jstree event data will contain a new property named changed, which will give information about selected and deselected nodes since the last changed.jstree event

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




# Checkbox plugin
This plugin renders checkbox icons in front of each node, making multiple selection much easier.
 
It also supports tri-state behavior, meaning that if a node has a few of its children checked it will be rendered as undetermined, and state will be propagated up. You can also fine tune the cascading options with the cascade config option.

Keep in mind when cascading checkbox will check even disabled nodes.

Undetermined state is automatically calculated, but if you are using AJAX and loading on demand and want to render a node as underemined pass "undetermined" : true in its state.

You can find all the checkbox plugin config options in the API.

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




# Conditionalselect plugin
This plugin overrides the activate_node function (the one that gets called when a user tries to select a node) and enables preventing the function invokation by using a callback.

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




# Contextmenu plugin
This plugin makes it possible to right click nodes and shows a list of configurable actions in a menu.

You can find all the contextmenu plugin config options in the API.

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




# Drag & drop plugin(dnd)
This plugin makes it possible to drag and drop tree nodes and rearrange the tree.

You can find all the dnd plugin config options in the API.

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




# Massload plugin
This plugin makes it possible to load nodes in a single request (used with lazy loading).

You can find all the massload plugin config options in the API.

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




# Search plugin
This plugin adds the possibility to search for items in the tree and even to show only matching nodes.

You can find all the search plugin config options in the API.

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



# Sort plugin
This plugin automatically arranges all sibling nodes according to a comparison config option function, which defaults to alphabetical order.

```js
$(function () {
  $("#plugins5").jstree({
    "plugins" : [ "sort" ]
  });
});
```




# State plugin
This plugin saves all opened and selected nodes in the user's browser, so when returning to the same tree the previous state will be restored.

You can find all the state plugin config options in the API. Make a selection and refresh this page to see the change persisted.

```js
$(function () {
  $("#plugins6").jstree({
    "state" : { "key" : "demo2" },
    "plugins" : [ "state" ]
  });
});
```




# Types plugin
This plugin makes it possible to add predefined types for groups of nodes, which means to easily control nesting rules and icon for each group.

To set a node's type you can use set_type or supply a type property with the node's data.

You can find all the types plugin config options & functions in the API.

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



# Unique plugin
Enforces that no nodes with the same name can coexist as siblings. This plugin has no options, it just prevents renaming and moving nodes to a parent, which already contains a node with the same name.

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



# Wholerow plugin
Makes each node appear block level which makes selection easier. May cause slow down for large trees in old browsers.

```js
$(function () {
  $("#plugins9").jstree({
    "plugins" : [ "wholerow" ]
  });
});
```