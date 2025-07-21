

---

# aclId_attribute

An integer constant uniquely identifying the window. This is the value that would be returned by the ACL function current_window if the window was active.



---

# activate_method

Gives the Window focus.



---

# activeView_attribute

A View object that represents the window's active view.



---

# backgroundColor_attribute

The background color of the window. For dialogs, you can both set and get the foreground and background colors of a window. For edit windows, you can only get the foreground and background colors of a window. You cannot set the foreground and background colors of an edit window.



---

# bringToFront_method

Places the Window on top of all other windows (at the top of the z-order).



---

# close_method

Closes this Window and releases all the native system resources it uses.



---

# createEvent_method

Creates an event of type WindowEvent .



---

# createMenuItem_method

Creates a menu item.



---

# dock_attribute

Indicates the docking state of the window. The value can only be changed before the window is displayed or when the window is hidden, but it can be read any time. If the value is DOCK_NONE, the window is floating.



---

# dockable_attribute

A boolean value indicating if the window can dock to a main window.



---

# DockEnabled_enumeration

The DockEnabled enumeration is an integer specifying the edges of the main window this window is allowed to dock to.

The DockEnabled enumeration has the following constants of type unsigned short .



---

# DockState_enumeration

The DockState enumeration is an integer showing the docking states of the window.

The DockState enumeration has the following constants of type unsigned short .



---

# dockTo_method

Docks the window to the specified location.



---

# embedded_attribute

A boolean value indicating if the window frame is embedded via ActiveX into a containing parent window.



---

# enableDocking_method

Specifies the edges of the main window this window is allowed to dock to.



---

# foregroundColor_attribute

The foreground color of the window. For dialogs, you can both set and get the foreground and background colors of a window. For edit windows, you can only get the foreground and background colors of a window. You cannot set the foreground and background colors of an edit window.



---

# getOption_method

Returns the value of the Arbortext set option, scoped to this window.



---

# getScriptContext_method

Returns the ScriptContext for the given language in this window. Returns null if there is no context for the language.



---

# height_attribute

The height of the window frame in pixels.



---

# hide_method

Causes the Window to no longer be displayed.



---

# loadComponentFile_method

Reads the XML file specified by filename and creates window components such as tool bars, menu bars, and so on according to the content of the XML File.



---

# longNativeHandle_attribute

The native window system handle associated with the window. On a Galaxy window system, this is a vwindow pointer.



---

# menuBar_attribute

The menu bar of the window.



---

# modal_attribute

A boolean value indicating if the window is modal. Modal windows grab all mouse and key events when open. The modal attribute can only be set before the window is displayed.



---

# moveTo_method

Moves the window to the specified location.



---

# nativeHandle_attribute

The native window system handle associated with the window. On a Galaxy window system, this is a vwindow pointer.

This is a 32-bit value. On a 64-bit system, call getLongNativeHandle().



---

# optionNames_attribute

A StringList containing the names of all window-scoped Arbortext set options.



---

# ownerNode_attribute

The document Node that this window is associated with. This attribute will be non-null only if the window is a dialog that was created as a result of a DCF file entry that associates a dialog with a document element.



---

# parent_attribute

The parent Window of this frame if it is a child window. If the window object is a top level window, this value is null . The parent attribute can only be set before the window is displayed.



---

# propertyMap_attribute

The PropertyMap associated with the window, or null if not set.



---

# screenX_attribute

The X coordinate of the window frame's left edge in pixels. If the window is docked to a main window, this value is relative to the upper left corner of the dock bar.



---

# screenY_attribute

The Y coordinate of the window frame's top edge in pixels. If the window is docked to a main window, this value is relative to the upper left corner of the dock bar.



---

# sendToBack_method

Places the Window behind all other windows (at the bottom of the z-order).



---

# setOption_method

Sets the value of the Arbortext set option, scoped to this window.



---

# setSize_method

Changes the size of the window so it has width width and height height .



---

# show_method

Makes the Window visible and brings it to the front of other windows.



---

# visible_attribute

A boolean value indicating if the window frame is visible.



---

# width_attribute

The width of the window frame in pixels.