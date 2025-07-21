

---

# aclId_attribute

An integer constant uniquely identifying the view . This is the value that is returned by the ACL function current_window if the view is active.



---

# backgroundColor_attribute

The background color of the View .



---

# foregroundColor_attribute

The foreground color of the View .



---

# getOption_method

This method returns the value of the Arbortext set option, scoped to this view .



---

# optionNames_attribute

A StringList containing the names of all view-scope Arbortext set options.



---

# setOption_method

Sets the value of the Arbortext set option, scoped to this view .



---

# suspendUpdate_attribute

A boolean value showing whether the view should be updated when the document is modified. Typically used when an application programmer needs to modify a large portion of the document and does not want the view to be updated until all changes have been made.

If the value is set to true , the view is not updated when the document is modified. If the value is set to false , normal updates are restored, and all changes to the document will be immediately reflected in the corresponding view. If the view is an edit view, this value only affects the modifications happened within the same script this value is set, and all edit views of the same document are affected. When the script finishes executing, the views will be updated. If the view is a dialog view, the value only affects the view it is set to, and the value affects the view until it is set to a different value .



---

# window_attribute

The Window in which this view resides.