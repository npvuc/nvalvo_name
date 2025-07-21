

---

# Dialog_Item_Attributes

All dialog items have the following attributes:

- • ACTIVE — An integer: non-zero if the dialog item is active, zero if the dialog item is not active. An active dialog item responds to user actions (mouse clicks and key strokes).

- • APPDATA — A string: application-specific data that is passed to dialog item and outline list expansion callbacks.

- • BACKGROUND — An integer: the red-green-blue value denoting the item's background color. The value is either a named color or an RGB specification preceded by # .

- • CALLBACKS — A string: a comma-delimited list of callback for the item, in the order that the callbacks are used.

- • DLGITEM_PTR — An integer: Returns the window pointer of the MFC dialog item.

- • EDITABLE — An integer: non-zero if the dialog item accepts user modifications, zero if the dialog item does not accept user modifications.

- • FOREGROUND — An integer: the red-green-blue value denoting the item's foreground color. The value is either a named color or an RGB specification preceded by # .

- • GEOMETRY — A string. If dlgitem is the XUI ID of an existing control, the value of geometry is a string representing the screen geometry of the control. The string has the format width x height + X + Y , where width is the width of the control, height is the height of the control, X is the horizontal screen coordinate, and Y is the vertical screen coordinate. For example, 520x320+100+200 . If dlgitem is not the XUI ID of an existing control, dlgitem_get returns an empty string.

- • IMAGE — A string: the name of an image to display within the dialog item.

- • sourcecontrol — A string. If dlgitem is the XUI ID of a menu bar, a context menu, or a dropdown menu, the value of sourcecontrol is the XUI ID of the control currently associated with the menu. For a menu bar, dlgitem_get returns the ID of the menu bar. For context and dropdown menus, dlgitem_get returns the ID of the control for which the menu is posted (such as a tree, table, or button control). If this menu was posted using the menu_popup ACL function, no control is associated with the menu and dlgitem_get returns an empty string.

- • TITLE — A string: the title of the dialog item. Not all dialog items display their title.

- • VALUE — A string: the value of the dialog item.

- • VISIBLE — An integer: non-zero if the dialog item is visible, zero if the dialog item is not visible. A visible dialog item is shown when its dialog is open.

- • WITHDRAW — Makes the dialog item invisible when the window is open. This is useful on the toolbar, because it automatically resets the display of the toolbar, shifting the other toolbar buttons to fill the space left by a withdrawn button (if the window is already open, you will see a momentary flash as this re-display takes place).



---

# Dialog_Item_Specific_Attributes

Certain dialog items may have type-specific attributes in addition to the default attributes for dialog items:

- • COLLAPSE — A callback function that is called to when an listtag is collapsed in an outlist item.

- • ENABLE — A callback function that is called to enable or disable menu items before a menu is opened.

- • EXPAND — A callback function that is called when a listtag is expanded in an outlist item.

- • EXTRAIMGCB — A callback function that is called when the extra image of an outlist item is clicked with the left mouse button.

- • KEYBOARD — A callback function that is called when a keyboard key is pressed for an outlist item.

- • LIST_COUNT — An integer for items which contain lists. Contains the number of items in the list. Setting the value extends or truncates the list as appropriate.

- • ON — An integer (zero or non-zero) representing the check status of a checkbox menu item or checkbox toolbar button.

## Related topic

dlgitem_get