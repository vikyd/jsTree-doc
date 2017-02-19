# Changed plugin
This plugin adds more information to the changed.jstree event. The new data is contained in the changed event data property, and contains a lists of selected and deselected nodes.




## changed.jstree Event  changed plugin




# Checkbox plugin
This plugin renders checkbox icons in front of each node, making multiple selection much easier.

It also supports tri-state behavior, meaning that if a node has a few of its children checked it will be rendered as undetermined, and state will be propagated up.





## $.jstree.defaults.checkbox checkbox plugin





## $.jstree.defaults.checkbox.visible checkbox plugin





## $.jstree.defaults.checkbox.three_state checkbox plugin





## $.jstree.defaults.checkbox.whole_node checkbox plugin





## $.jstree.defaults.checkbox.keep_selected_style checkbox plugin





## $.jstree.defaults.checkbox.cascade checkbox plugin





## $.jstree.defaults.checkbox.tie_selection checkbox plugin





## _undetermined () checkbox pluginprivate





## show_checkboxes () checkbox plugin





## hide_checkboxes () checkbox plugin





## toggle_checkboxes () checkbox plugin





## is_undetermined (obj)





## disable_checkbox (obj) checkbox plugin





## disable_checkbox.jstree Event  checkbox plugin





## disable_checkbox (obj) checkbox plugin





## enable_checkbox.jstree Event  checkbox plugin





## check_node (obj) checkbox plugin





## check_node.jstree Event  checkbox plugin





## uncheck_node (obj) checkbox plugin





## uncheck_node.jstree Event  checkbox plugin





## check_all () checkbox plugin





## check_all.jstree Event  checkbox plugin





## uncheck_all () checkbox plugin





## uncheck_all.jstree Event  checkbox plugin





## is_checked (obj) checkbox plugin





## get_checked ([full]) checkbox plugin





## get_top_checked ([full]) checkbox plugin





## get_bottom_checked ([full]) checkbox plugin




# Conditionalselect plugin
This plugin allows defining a callback to allow or deny node selection by user input (activate node method).






## $.jstree.defaults.checkbox.visible checkbox plugin




# Contextmenu plugin
Shows a context menu when a node is right-clicked.






## $.jstree.defaults.contextmenu contextmenu plugin





## $.jstree.defaults.contextmenu.select_node contextmenu plugin





## $.jstree.defaults.contextmenu.show_at_node contextmenu plugin





## $.jstree.defaults.contextmenu.items contextmenu plugin





## show_contextmenu (obj [, x, y]) contextmenu plugin





## _show_contextmenu (obj, x, y, i) contextmenu pluginprivate





## show_contextmenu.jstree Event  contextmenu plugin





## context_parse.vakata Event  contextmenu plugin





## context_show.vakata Event  contextmenu plugin





## context_hide.vakata Event  contextmenu plugin




# Drag'n'drop plugin
Enables dragging and dropping of nodes in the tree, resulting in a move or copy operations.






## $.jstree.defaults.dnd dnd plugin





## $.jstree.defaults.dnd.copy dnd plugin





## $.jstree.defaults.dnd.open_timeout dnd plugin





## $.jstree.defaults.dnd.is_draggable dnd plugin





## $.jstree.defaults.dnd.check_while_dragging dnd plugin





## $.jstree.defaults.dnd.always_copy dnd plugin





## $.jstree.defaults.dnd.inside_pos dnd plugin





## $.jstree.defaults.dnd.drag_selection dnd plugin





## $.jstree.defaults.dnd.touch dnd plugin





## $.jstree.defaults.dnd.large_drop_target dnd plugin





## $.jstree.defaults.dnd.large_drag_target dnd plugin





## $.jstree.defaults.dnd.use_html5 dnd plugin





## dnd_scroll.vakata Event  dnd plugin





## dnd_start.vakata Event  dnd plugin





## dnd_move.vakata Event  dnd plugin





## dnd_stop.vakata Event  dnd plugin




# Massload plugin
Adds massload functionality to jsTree, so that multiple nodes can be loaded in a single request (only useful with lazy loading).






## $.jstree.defaults.massload massload plugin




# Search plugin
Adds search functionality to jsTree.






## $.jstree.defaults.search search plugin





## $.jstree.defaults.search.ajax search plugin





## $.jstree.defaults.search.fuzzy search plugin





## $.jstree.defaults.search.case_sensitive search plugin





## $.jstree.defaults.search.show_only_matches search plugin





## $.jstree.defaults.search.show_only_matches_children search plugin





## $.jstree.defaults.search.close_opened_onclear search plugin





## $.jstree.defaults.search.search_leaves_only search plugin





## $.jstree.defaults.search.search_callback search plugin





## search (str [, skip_async]) search plugin





## search.jstree Event  search plugin





## clear_search () search plugin





## clear_search.jstree Event  search plugin




# Sort plugin
Automatically sorts all siblings in the tree according to a sorting function.






## $.jstree.defaults.sort sort plugin





## sort (obj [, deep]) sort pluginprivate









# State plugin
Saves the state of the tree (selected nodes, opened nodes) on the user's computer using available options (localStorage, cookies, etc)






## $.jstree.defaults.state state plugin





## $.jstree.defaults.state.key state plugin





## $.jstree.defaults.state.events state plugin





## $.jstree.defaults.state.ttl state plugin





## $.jstree.defaults.state.filter state plugin





## state_ready.jstree Event  state plugin  





## save_state () state plugin





## restore_state () state plugin





## clear_state () state plugin 




# Types plugin   
Makes it possible to add predefined types for groups of nodes, which make it possible to easily control nesting rules and icon for each group.







## $.jstree.defaults.types types plugin 





## get_rules (obj) types plugin





## get_type (obj [, rules]) types plugin 





## set_type (obj, type) types plugin  




# Unique plugin
Enforces that no nodes with the same name can coexist as siblings.






## $.jstree.defaults.unique unique plugin







## $.jstree.defaults.unique.case_sensitive unique plugin







## $.jstree.defaults.unique.duplicate unique plugin





 
 
 
 
# Wholerow plugin   
Makes each node appear block level. Making selection easier. May cause slow down for large trees in old browsers.

 