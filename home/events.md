# Listening for events

jsTree triggers various events on the container. You can review the list of all events to know what to listen for.

To get more information about the event inspect its data argument.

In most cases where a node is involved you will get the whole node object passed in. If you get an ID string somewhere and want to inspect the node just use .get_node().


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