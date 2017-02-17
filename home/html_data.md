# Populating a tree using HTML

Basic markup

jsTree can turn a regular unordered list into a tree. The minimal required markup is a <ul> node with some nested <li> nodes with some text inside.

You should have a container wrapping the <ul> and create the instance on that container. Like so:
$('#html1').jstree();.

<div id="html1">
  <ul>
    <li>Root node 1</li>
    <li>Root node 2</li>
  </ul>
</div>
Root node 1
Root node 2
Nodes with children

To create a node with child nodes simpy nest an <ul>.

Internally jstree converts the text to a link, so if there already is a link in the markup jstree won't mind. Like Child node 2.
Clicking on the link however will not direct the user to a new page, to do that - intercept the changed.jstree event and act accordingly.

Keep reading for the section on handling events.

<div id="html1">
  <ul>
    <li>Root node 1
      <ul>
        <li>Child node 1</li>
        <li><a href="#">Child node 2</a></li>
      </ul>
    </li>
  </ul>
</div>
Root node 1
Setting initial state with classes

To make a node initially selected you can set the jstree-clicked class on the <a> element.

Similarly you can set the jstree-open class on any <li> element to make it initially extended, so that its children are visible.

It is a good idea to give your nodes unique IDs by adding the id attribute to any <li> element. This will be useful if you need to sync with a backend as you will get the ID back in any events jstree triggers.

…
<li class="jstree-open" id="node_1">Root
  <ul>
    <li>
      <a href="#" class="jstree-clicked">Child</a>
    </li>
  </ul>
</li>
…
Root
Child
Setting initial state with data attribute

You can also set the state on a node using a data-jstree attribute.

You can use any combination of the following: opened, selected, disabled, icon.

Specifying an address (anything containing a /) will display that image as the node icon. Using a string will apply that class to the <i> element that is used to represent the icon.
For example if you are using Twitter Bootstrap you can use "icon" : "glyphicon glyphicon-leaf" to display a leaf icon.

<li data-jstree='{"opened":true,"selected":true}'>Root
  <ul>
    <li data-jstree='{"disabled":true}'>Child</li>
    <li data-jstree='{"icon":"//jstree.com/tree.png"}'>
      Child</li>
    <li data-jstree='{"icon":"glyphicon glyphicon-leaf"}'>
      Child</li>
  </ul>
</li>
Root
Child
 Child
 Child
Loading with AJAX

You can also use AJAX to populate the tree with HTML your server returns. The format remains the same as the above, the only difference is that the HTML is not inside the container, but returned from the server.

To take advantage of this option you need to use the $.jstree.defaults.core.data config option.

Just use a standard jQuery-like AJAX config and jstree will automatically make an AJAX request populate the tree with the response.

Add a class of jstree-closed to any LI node you return and do not nest an UL node and jstree will make another AJAX call as soon as the user opens this node.

In addition to the standard jQuery ajax options here you can supply functions for data and url, the functions will be run in the current instance's scope and a param will be passed indicating which node is being loaded, the return value of those functions will be used as URL and data respectively.

$('#tree').jstree({
  'core' : {
    'data' : {
      'url' : 'ajax_nodes.html',
      'data' : function (node) {
        return { 'id' : node.id };
      }
    }
  }
});

// Example response:
<ul>
<li>Node 1</li>
<li class="jstree-closed">Node 2</li>
</ul>