

---

# Menus_on_Menubars

Menu bar menus can contain any combination of the following types of menu items:

- • Button menu item — Appears as a standard menu selection with an optional graphic to the left of its label. This is the only type of menu item that can have child <menuitem> elements.

- • Menu separator — A line separating adjacent items.

- • Toggle menu item — When activated, the item will display a check mark to the left of its label.

- • Radio menu item — The menu item is displayed as a radio button.

The following example creates a menu named Custom that contains the following menu items:

- • A Find menu item that uses ACL to open the Find/Replace dialog box

- • An Options menu with the following menu items:

- • A My ACL Function menu item that displays a response dialog box. This item is a template for inserting your own function.

```
<window width="150" height="40">
<menubar>
<menuitem label="Custom">
<menuitem label="Find" command="FindReplace"></menuitem>
<menuitem label="Options">
<menuitem label="Cut" shortcut="Ctrl+X" command="EditCut">
<script type="application/x-javascript" ev:event="menupost">
if (Application.activeDocument.textSelection.collapsed == true) {
Application.event.target.enabled=false;
}
else {
Application.event.target.enabled=true;
}</script>
</menuitem>
<menuitem label="Full Menus" type="toggle">
<script type="application/x-javascript" ev:event="menupost">
if (Application.getOption("fullmenus") == "on") {
Application.event.target.checked=true;
}
else {
Application.event.target.checked=false;
}
</script>
<script type="application/x-javascript" ev:event="menuselected">
if (Application.event.target.checked == true) {
Application.setOption("fullmenus", "off");
}
else {
Application.setOption("fullmenus", "on");
}
</script>
</menuitem>
</menuitem>
<menuitem label="-" type="separator">
</menuitem>
<menuitem label="My ACL function"
command="response('Put your ACL function call here')">
</menuitem>
</menuitem>
</menubar>
</window>
```



---

# Shortcut_and_Dropdown_Menus

You can create shortcut and dropdown menus in the following situations:

- • Shortcut menu assigned to a tree control and customized in context for its nodes.

- • Shortcut menu assigned to a table control and customized in context for its cells and rows.

- • Dropdown menus for button controls.

- • Dropdown menus for toolbar buttons controls.

When implemented, shortcut menus are displayed by placing the mouse cursor over the control and right-clicking. Shortcut menus are also displayed by pressing the Application key when the control has focus. Dropdown menus are displayed by left-clicking on a control and by activating a control when it has focus.

The Acl event notification API supports menus within XUI dialog boxes. Menus can be specified in menu configuration files as well, but the event management for these menus does not use the Acl event enhancements. Instead, event management is specified within the configuration files.

An example application of XUI menus with menu bars, controls, and tool bars is provided in the following directory:

```
Arbortext-path
\samples\XUI\xuimenusample
```