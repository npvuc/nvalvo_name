

---

# Dockable_Dialog_Boxes_and_the_AOM

The methods to create and display a dockable dialog box are the same as those for a standard dialog box. For example:

```
var dialog = Application.createDialogFromFile('c:\temp\myxuifile');
dialog.dock = 0; // override the dock attribute in the XML file
dialog.show();
```



---

# Example

Refer to the dockable dialog box example contained in the file:

```
Arbortext-path
\samples\XUI\dockableDialog.xml
```



---

# Geometry

When a dockable dialog box is docked in an edit window, users still can resize the dialog box by dragging the splitter separating the docked dialog box and the edit window.

Arbortext Editor remembers three sizes for each dockable dialog type:

- • the size when the dialog box is docked horizontally

- • the size when the dialog box is docked vertically

- • the size when the dialog box is floating

Therefore, when a dockable dialog box is displayed or docked, Arbortext Editor will set the dialog box size to the size of the previous dialog box of the same type.