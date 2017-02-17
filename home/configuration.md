# Configuring instances

Creating an instance as described in the overview does not modify any of the defaults:

$('#jstree').jstree();
You can change the defaults for all future instances:

$.jstree.defaults.core.themes.variant = "large";
$('#jstree').jstree();
But most of the time you will want to change the defaults only for the instance that is being created. This is achieved by passing in a config object when creating the instance:

$('#jstree').jstree({
  "plugins" : [ "wholerow", "checkbox" ]
});
As seen in the previous example - there is one special key in the config object named plugins. It is an array of strings, which contain the names of the plugins you want active on that instance.

All options that do not depend on a plugin are contained in a key of the config object named core, the options for each plugin are contained within a key with the same name as the plugin:

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
You can have a look at all the options and their default values. This list is what you can configure on each instance.
For example, by default the tree allows multiple selection as stated in $.jstree.defaults.core.multiple, to overwrite that make sure your config object contains "core" : { "multiple" : false }. If you have multiple overrides for the same key (like "core" here), group them:

$("#jstree").jstree({
  "core" : {
    "multiple" : false,
    "animation" : 0
  }
});