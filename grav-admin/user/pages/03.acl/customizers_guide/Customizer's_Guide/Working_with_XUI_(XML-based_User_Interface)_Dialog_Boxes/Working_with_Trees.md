

---

# Dragging_and_Dropping_Tree_Control_Content

You can perform standard Windows drag and drop operations on XUI tree control items. XUI tree control drag and drop operations are accessible using ACL only. Drag and drop operations let you transfer data to and from the XUI tree control from and to other applications that also support drag and drop operations.

Two types of data can be transferred using a drag-and-drop operations:

- • Text data — A block of text.

- • File data — One or more file path names.

When a drag and drop operation begins in a XUI tree control, an ACL application is responsible for determining the type of data format that will be used, as well as providing the actual data. When a XUI tree control is the target of a drag and drop operation, the ACL application is responsible for examining the data available and determining how it is to be processed once it is dropped on the tree control. The meaning and the handling of the data in a drag and drop operation is completely up to the custom ACL application.

Drag and drop functionality is enabled by handling the following drag and drop events in your custom ACL application:

- • DRAGDROPBEGIN — Signals the beginning of a drag and drop operation in a XUI tree control. This event is raised when the left mouse button is clicked and held down over a selected item in the source tree control and the mouse is moved. A handler for this event must be provided to allow a XUI tree control to be a drag-and-drop source. (That is, to have drag and drop operations begin in the tree control.)

- • DRAGDROPENTER — Signals a drag and drop operation has entered the target tree control. This event is raised when the mouse is first moved into the tree control during a drag and drop operation. The handler function for this event determines what the drop effect would be if a drop were attempted at the current position.

- • DRAGDROPOVER — Signals a drag and drop operation is over the target tree control. This event is raised when the mouse is over the tree control during a drag and drop operation. This handler function determines what the drop effect would be if a drop were attempted at the current position.

- • DRAGDROPLEAVE — Signals a drag-and-drop operation has left the target tree control. This event is raised when the mouse cursor leaves the tree control. Handle this event when you want to provide custom behavior when the drag and drop operation leaves a tree control.

- • DRAGDROPDROP — Signals a drop has occurred in the target tree control. This event is raised when a drop operation is to occur. Handle this event to insert the dropped data.

- • DRAGDROPEND — Signals a drag and drop operation that started in the tree control has ended. This event is raised after the DRAGDROPDROP event only when the drag and drop operation started in this tree control. The event handler for this event should modify the tree control based on the resulting drop effect of the drag and drop operation. For example, if the drop effect result of the drag and drop operation is 2 , meaning the drop succeeded as a move operation, the drop target will have inserted the data. This handler should delete the source data to complete the move operation.

A sample application demonstrating how to use the XUI tree control drag-and-drop and multiple selection functionality is included in the following directory.

```
Arbortext-path
\samples\XUI\
```

The sample consists of the following files:

- • treectrldddlg.xml — A XUI file defining a dockable window containing a tree control. The tree control is populated with some sample items.

- • spaceimglist7.bmp — A bitmap graphic containing several images used for tree control items.

- • treectrlddtest.acl — An ACL file which loads the dockable window described in treectrldddlg.xml and handles drag-and-drop functionality for it.

Use the following steps to run this sample application:

This sample can demonstrate the transfer of both text and file data to and from the tree control by dragging and dropping the data. For drag-and-drop operations that originate in the tree control, the convention used in this sample is:

- • If a tree item has application-specific data associated with it, the application-specific data is a file path and the tree item should be dragged and dropped as file data.

- • If a tree item has no application-specific data associated with it, the tree item should be dragged and dropped as text data with the item label as the data.

Initially, the tree control contains a set of sample items that have no application-specific data.

For multiple selection, no dragging and dropping is allowed if a parent-child combination is selected. This sample application provides no rules for how this should be handled, so it is not allowed.

- • Demonstrating dragging and dropping text data within the tree control:

- • Demonstrating dragging and dropping text data to Arbortext Editor :

- • Demonstrating dragging and dropping text data from an external application:

- • Demonstrating dragging and dropping file data from an external application:

- • Demonstrating dragging and dropping file data to an external application:

- • Demonstrating dragging and dropping file data to Arbortext Editor :



---

# Selecting_Objects_in_Tree_Controls

A XUI tree control has two different selection types or modes: single selection and multiple selection. The tree control selection mode is set with the seltype attribute on the treecontrol element. Legal values are single (the default) and multiple . The selection mode cannot be changed at run time.

In single selection mode, the tree control allows only one tree node to be selected at a time.

Multiple selection allows more than one tree node in the tree control to be selected at a time. Multiple selection mode is accessible using ACL only. XUI has no default rules as to how parent and child nodes are handled when selected in multiple selection mode. Such handling is the responsibility of the custom ACL application working with the XUI controls.

Detect selection changes by using the dlgitem_add_callback function to add a callback to the tree control and the check for ITEM_CHANGED events in the callback function. Use the following functions to work with tree control selections:

- • dlgitem_get_select_array(window, dlgitem, array)

- • dlgitem_get_selected_appdata(window, dlgitem)

- • dlgitem_get_selected_listtag(window, dlgitem)

- • dlgitem_select_list_at(window, listtag, row)

- • dlgitem_get_selected_listtag_array(window, dlgitem, array)