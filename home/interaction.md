# Invoking methods on an instance

Please keep in mind that by default all modifications to the tree are prevented (create, rename, move, delete). To enable them set core.check_callback to true
To invoke a method on an instance you must obtain a reference of the instance and invoke the method. The example shows how to obtain a reference and invoke a method.

Check the API for a list of available methods.


// 3 ways of doing the same thing
$('#jstree').jstree(true)
  .select_node('mn1');
$('#jstree')
  .jstree('select_node', 'mn2');
$.jstree.reference('#jstree')
  .select_node('mn3');
				