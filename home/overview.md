# Getting Started - everything at a glance

Download jsTree or use CDNJS
If you choose to download - all the files you need are in the dist/ folder of the download
Include a jsTree theme
Themes can be autloaded too, but it is best for performance to include the CSS file.
If hosting the files yourself:
<link rel="stylesheet" href="dist/themes/default/style.min.css" />
If using CDNJS:
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/jstree/3.2.1/themes/default/style.min.css" />
Setup a container
This is the element where you want the tree to appear, a <div> is enough. This example has a nested <ul> as there is no other data source configured (such as JSON).
  <div id="jstree_demo_div"></div>
Include jQuery
jsTree requires 1.9.0 or greater in your webpage. You can use a CDN version or include a local copy.
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/1.12.1/jquery.min.js"></script>
Include jsTree
If hosting the files yourself: for production include the minified version: dist/jstree.min.js, there is a development version too: dist/jstree.js
<script src="dist/jstree.min.js"></script>
If using CDNJS:
<script src="https://cdnjs.cloudflare.com/ajax/libs/jstree/3.2.1/jstree.min.js"></script>
Create an instance
Once the DOM is ready you can start creating jstree instances.
$(function () { $('#jstree_demo_div').jstree(); });
Listen for events
jsTree uses events to notify you when something changes while users (or you) interact with the tree. So binding to jstree events is as easy binding to a click. There is a list of events and what information they provide in the API documentation.
$('#jstree_demo_div').on("changed.jstree", function (e, data) {
  console.log(data.selected);
});
Interact with your instances
Once an instance is ready you can invoke methods on it. There is a list of available methods in the API documentation. The three examples below do exactly the same thing
$('button').on('click', function () {
  $('#jstree').jstree(true).select_node('child_node_1');
  $('#jstree').jstree('select_node', 'child_node_1');
  $.jstree.reference('#jstree').select_node('child_node_1');
});
show the complete code


<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>jsTree test</title>
  <!-- 2 load the theme CSS file -->
  <link rel="stylesheet" href="dist/themes/default/style.min.css" />
</head>
<body>
  <!-- 3 setup a container element -->
  <div id="jstree">
    <!-- in this example the tree is populated from inline HTML -->
    <ul>
      <li>Root node 1
        <ul>
          <li id="child_node_1">Child node 1</li>
          <li>Child node 2</li>
        </ul>
      </li>
      <li>Root node 2</li>
    </ul>
  </div>
  <button>demo button</button>

  <!-- 4 include the jQuery library -->
  <script src="dist/libs/jquery.js"></script>
  <!-- 5 include the minified jstree source -->
  <script src="dist/jstree.min.js"></script>
  <script>
  $(function () {
    // 6 create an instance when the DOM is ready
    $('#jstree').jstree();
    // 7 bind to events triggered on the tree
    $('#jstree').on("changed.jstree", function (e, data) {
      console.log(data.selected);
    });
    // 8 interact with the tree - either way is OK
    $('button').on('click', function () {
      $('#jstree').jstree(true).select_node('child_node_1');
      $('#jstree').jstree('select_node', 'child_node_1');
      $.jstree.reference('#jstree').select_node('child_node_1');
    });
  });
  </script>
</body>
</html>
 