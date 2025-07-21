

---

# Defining_the_Dialog_Box

# Defining the Dialog Box

You can use Arbortext Architect to interactively define and modify XUI dialog boxes. With Arbortext Architect open, choose Edit > XUI . Open your XUI XML document. (A sample file is at Arbortext-path \doctypes\xui\demo.xml .)

With Arbortext Architect displaying the XUI XML document, choose Tools > View Dialog . The XUI dialog box will be displayed.

Changing values and settings in the XML document will be reflected immediately in the dialog box. Likewise, modifying controls in the dialog box will cause immediate updates to the XML document.

You should save your custom XUI files in the Arbortext-path \custom\dialogs directory.



---

# Describing_Dialog_Box_Controls

# Describing Dialog Box Controls

Dialog boxes and their controls are defined using the XUI elements described in XUI Element Reference . Refer to that section for detailed descriptions of each element and its attributes.

For example, the following XUI markup defines this dialog box:

Dialog box with label , textbox , and two button controls.

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN" "xui.dtd">
<window title="Find">
<label label="&Find what:"/>
<textbox multiline="false">
<value></value>
</textbox>
<button label="Find &Next" type="accept"></button>
<button label="Cancel" type="cancel"></button>
</window>
```

The content of the value element will become the text the user enters into the text box in the dialog box. A button with the type cancel is activated when the Esc key is pressed. A button with the type accept is the default button and is activated when the ENTER key is pressed.



---

# Displaying_the_Dialog_Box_using_the_AOM

# Displaying the Dialog Box using the AOM

The AOM Application.createDialogFromFile() method creates XUI dynamic dialog boxes.

To display a XUI dialog box (in this example, the dialog box is defined in the XML file C:\Project\find.xml ), you can run the following JavaScript statements:

```
var dialog = Application.createDialogFromFile("c:\Project\find.xml");
dialog.show();
```

Another method, Application.createDialogFromDocument() , creates a XUI dynamic dialog box from an existing DOM Document .

As when defining the XUI dialog box, value and setting changes in the XML document will be reflected immediately in the dialog box. Likewise, modifying controls in the dialog box will cause immediate updates to the XML document.

To suspend immediate updates, set the value of View.suspendupdates to TRUE .



---

# Embedding_XUI_Dialog_Box_Controls_in_a_Document

# Embedding XUI Dialog Box Controls in a Document

You can embed XUI dialog box controls in the content of a document displayed in Arbortext Editor . Users can use these controls to interact with other data sources, take advantage of ActiveX controls, select values from restricted lists, and so on.

Use the following steps to embed XUI dialog box controls in a document. (Examples follow.)

By default, the XUI controls are displayed embedded in the document. You can display the XUI markup inline instead of the rendered controls using the ACL set command set dialogdisplay=off . set dialogdisplay=on will again display the embedded controls.

When using embedded XUI dialog box controls, be aware that only one occurrence of a specific element's dialog box can be displayed at one time. If the same element appears in multiple open windows, only one occurrence of the element will be displayed as an embedded XUI control.

This example shows how to embed a combo box in a document. The user can select an item from the combo box and have it inserted at the current cursor location.



---

# Identifying_the_Parent_Window_of_a_Dialog_Box

# Identifying the Parent Window of a Dialog Box

The methods Application.createDialogFromFile() and Application.createDialogFromDocument() each take a parameter, parent , for specifying the parent window of the dialog box. If the parent is not specified, the default parent is the current active window.

The parent parameter is useful when a user creates a dockable dialog box in a document type startup file or a document startup file. At the time these startup files are executed, the active document is the document to be brought up, and the edit window for the document is not yet displayed.

Users can get the new edit window from the active document and assign the correct parent to the new dockable dialog box as follows:

```
var parent = Application.activeDocument.defaultView.window;
var window = Application.createDialogFromFile('my.xml',null,parent);
window.dock = window.DOCK_LEFT;
window.show();
```



---

# Manipulating_XUI_Dialog_Boxes_using_the_AOM

# Manipulating XUI Dialog Boxes using the AOM

AOM Window and View interfaces work on both XUI dynamic dialog boxes and PTC Arbortext Editor Edit windows. A XUI Window object can be obtained when the dialog box is created. For example, the following JavaScript statement returns an AOM Window object.

```
var window = Application.createDialogFromFile("C:\find.xml");
```

An Edit Window object can be obtained by converting an ACL window ID to its corresponding AOM Window object. For example:

```
var window = Acl.getWindow(5);
```

Whether or not the window with focus is a XUI dialog box or an Edit window, you can use the following JavaScript statement to get its Window object.

```
var window = Application.activeWindow;
```

Once you have the Window object, you can call the methods of the Window interface to manipulate the window. For example, the following JavaScript code moves the active window to a specific location:

```
Application.activeWindow.moveTo(200, 200);
```

You can find a complete list of methods for the Window interface in the Window interface chapter of the Programmer's Reference .



---

# Returning_Values_from_Dialog_Boxes

# Returning Values from Dialog Boxes

Because the XUI document is updated when any values or states change in the control it defines, the value of the control can be obtained by evaluating the content of the XUI document. Based on the XUI DTD, each control type (textbox, checkbox, and so on) potentially stores its value in a different manner in the document.

For example, a <textbox> element stores its value as the content of its child <value> element. A <combobox> element stores it's value in its value attribute. Refer to XUI Element Reference (or the XUI DTD) for details on each control.

The following examples return the current values of different dialog box controls.

The value of a <textbox> element is stored as the content of the child <value> element. The following example displays the value in a message window when the OK button is selected.

```
<?xml version="1.0" encoding="utf-8"?>
<!--ArborText, Inc., 1988-2003, v.4002-->
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN"
"xui.dtd">
<window orient="horizontal" align="center" modal="false" title="Value Test">
<label label="User ID"/>
<textbox id="userid">
<value></value>
</textbox>
<button label="OK" type="accept">
<script type="application/x-javascript" ev:event="domactivate">
var document = Application.event.target.ownerDocument;
var textnode = document.getElementById("userid").firstChild.firstChild;
if (textnode) {
Application.alert(textnode.nodeValue);
}
else {
Application.alert("[ EMPTY]");
}
var dialog = Application.event.view.window;
dialog.close();
</script>
</button>
</window>
```

The value of a <combobox> is stored in its value attribute. The following example displays the value in a message window when the OK button is selected.

```
<?xml version="1.0" encoding="utf-8"?>
<!--ArborText, Inc., 1988-2003, v.4002-->
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN"
"xui.dtd">
<window orient="horizontal" align="center" modal="false" title="Value Test">
<label label="Choose a color"/>
<combobox id="color" value="Red" type="dropdownlist">
<listitem label="Red"/>
<listitem label="Orange"/>
<listitem label="Yellow"/>
<listitem label="Green"/>
<listitem label="Blue"/>
</combobox>
<button label="OK" type="accept">
<script type="application/x-javascript" ev:event="domactivate">
var document = Application.event.target.ownerDocument;
var value = document.getElementById("color").getAttribute("value");
Application.alert(value);
var dialog = Application.event.view.window;
dialog.close();
</script>
</button>
</window>
```

You can select 1 or more values in a multiple-selection <listbox> control. The following example displays each selected value in a message window when the OK button is selected.

```
<?xml version="1.0" encoding="utf-8"?>
<!--ArborText, Inc., 1988-2003, v.4002-->
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN"
"xui.dtd">
<window orient="horizontal" modal="false" title="Value Test">
<label label="Choose Colors"/>
<listbox id="color" width="100" height="100" value="Red" type="multiple">
<listitem label="Red" selected="true"/>
<listitem label="Orange"/>
<listitem label="Yellow" selected="true"/>
<listitem label="Green"/>
<listitem label="Blue"/>
</listbox>
<button label="OK" type="accept">
<script type="application/x-javascript" ev:event="domactivate">
var document = Application.event.target.ownerDocument;
var listbox = document.getElementById("color");
var nodelist = listbox.getElementsByAttribute("selected", "true", 1);
for (var i = 0; i < nodelist.length; i++) {
Application.alert(nodelist.item(i).getAttribute("label"));
}
var dialog = Application.event.view.window;
dialog.close();
</script>
</button>
</window>
```

For more information on working with events, refer to the Events chapter in the Programmer's Reference .



---

# Specifying_Dialog_Box_Layout

# Specifying Dialog Box Layout

XUI supports three layout models: Box, Grid, and Morph.

Layout models are specified by using their corresponding elements.



---

# Specifying_Event_Listeners

# Specifying Event Listeners

Since a XUI dialog box is synchronized with its XUI XML document, you can register DOM events in the document to monitor activities in the dialog box. For example, when a check box is selected, the checked attribute of the element will change to true . If you register a DOMAttrModified event on the checkbox element, you will be informed whenever the check status is changed in the dialog box.

XUI extends the DOMActivate event to be dispatched when the status of a control is changed. For example, a DOMActivate event will be dispatched to the affected element whenever a button is clicked, a check box is selected, an item in a list box is selected, the content of a text box is changed, and so on. Therefore, you can register a DOMActivate event listener on a button element to execute the necessary routines when a button is pushed.

XUI makes use of W3C XML Events. You can register event listeners in the XUI document as follows:

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN" "xui.dtd">
<window>
<button label="OK">
<script type="application/x-javascript" ev:event="DOMActivate">
Application.alert("The OK button is selected");
</script>
</button>
</window>
```

This document declares the XML Events namespace in the window element. The script element contains the script that will be executed when the event specified by the ev:event attribute is dispatched. Therefore, the script element registers a DOMActivate event listener on the button element, and the body of the event listener is the content of the script element. When the OK button is pushed, the JavaScript engine will display a message box with the message “ The OK button is selected ”.

The type attribute of the script element specifies the type of the script. XUI supports JavaScript (Rhino), JScript (Microsoft), and VBScript. Refer to <script> Element for a list of valid script types.

In addition to DOM Events, you can register AOM WindowEvent events on the window element. The WindowEvent module has the following event types:

The following examples show the three ways to register an event listener:

In this example, the usage attribute <script> is set to indirect . Doing so disassociates the <script> element from its parent <window> element. If usage is set to direct (the default), the observer of the handler is the handler's parent element.

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN" "xui.dtd">
<window>
<button id="ok" label="OK"/>
<script id="select" usage="indirect" type="application/x-javascript">
Application.alert("The OK button is selected");
</script>
<ev:listener event="DOMActivate" observer="ok" handler="#select"/>
</window>
```

As in the previous example, the usage attribute of <script> is set to indirect , disassociating the <script> element from its parent <window> element.

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN" "xui.dtd">
<window>
<button label="OK" ev:event="DOMActivate" ev:handler="#select"/>
<script id="select" usage="indirect" type="application/x-javascript">
Application.alert("The OK button is selected");
</script>
</window>
```

The observer is the parent element of the handler. This example illustrates the simplest way to register an event listener.

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN" "xui.dtd">
<window>
<button label="OK">
<script type="application/x-javascript" ev:event="DOMActivate">
Application.alert("The OK button is selected");
</script>
</button>
</window>
```



---

# Working_with_Dockable_Dialog_Boxes

# Working with Dockable Dialog Boxes

Dockable dialog boxes can be displayed standalone or be dragged into a Arbortext Editor edit window and docked on one edge of the edit window. If you drag a docked dialog box away from the edge of the edit window, the dialog box undocks. A dockable dialog box can contain all controls that are allowed in a standard dialog box except for toolbars and menubars. ( <menubar> and <toolbar> elements in the file are ignored.)

The markup for a dockable dialog box is the same as that for a standard dialog box. Dockable dialog boxes are specified using the attributes enabledocking and dock of the <window> element.

- • enabledocking — Specifies the edges of the edit window the dialog box can dock to.

- • dock — Specifies the docking state of the dockable dialog box.

The following example shows a valid pairing of attributes:

```
<window enabledocking="leftright" dock="left" >
...
</window>
```

Whether a dialog box is dockable or not is determined at the dialog box creation time. After a dialog box is created, the dialog box cannot change between dockable and undockable even if enabledocking is modified or the AOM enableDocking method is called.

The modal attribute in the <window> element takes precedence over the enabledocking attribute. If modal has a value of true , the XUI file will be displayed as a standard modal dialog box regardless of the value of enabledocking .



---

# Working_with_Images

# Working with Images

Images can be used in many areas of XUI dialog boxes, such as in check boxes, on menus, and on buttons. (However, images are not available on submenu items.) Images are first defined using image or imagelist elements. The images are then referenced using the image attribute of the element displaying the image.

The following example uses the image element to define the image c:\temp\logo1.jpg and display it on a button.

```
<window>
<imagegroup>
<image id="imageLogo" path="c:\temp\logo1.jpg"/>
</imagegroup>
...
<button image="imageLogo"></button>
...
</window>
```

When deploying XUI controls, absolute paths to images may be restrictive. For XUI controls referencing images by name only, Arbortext Editor will first search the paths defined with the set dialogspath command option (and Advanced Preference). If the image is not found, Arbortext Editor will search the paths defined with set graphicspath . Images with relative paths will also be searched for in directories relative to the paths defined by set dialogspath and set graphicspath .

Another approach to working with images is to use the imagelist element to specify that a single graphic file contains multiple images of identical widths and heights.

For example, if path specifies a graphic file with a width of 48 and height of 16, and imagewidth is set to a value of 16, imagelist will contain 3 image elements, each defining an image 16 pixels wide by 16 pixels high.

The following example uses the imagelist element to define three images in tool_icons.jpg and displays them in a list box.

```
<window>
<imagegroup>
<imagelist path="tool_icons.bmp" imagewidth="16">
<image id="imageIconCopy"/>
<image id="imageIconCut"/>
<image id="imageIconPaste"/>
</imagelist>
</imagegroup>
...
<listbox>
<listitem image="imageIconCopy">
<listitem image="imageIconCut">
<listitem image="imageIconpaste">
</listbox>
...
</window>
```

If a menu item has the same command as a toolbar button, then the button's image is displayed next to the item on the menu. For example, if a toolbar button element has command set to FileNew and image set to image.jpg , and a menuitem element also has command set to FileNew , the image image.jpg will be displayed next to the menu item.



---

# Working_with_Menus

# Working with Menus

You can create menus using the <menubar> and <menuitem> elements. Menus can be create on menubars, as shortcut menus, and as dropdown menus.

A <menuitem> can execute the ACL command specified in its command parameter, or the actions defined in its child <script> element using menuselected and menupost event listeners. The menuselected listener can contain the command for the menu item. The menupost listener can disable the menu item when certain conditions are met. Listeners can also be registered for the same events on items within a shortcut or dropdown menu. The posting of a menu for either a menubar or a control will cause the event ITEM_POSTMENU to be dispatched. The selection of an item will cause the existing ITEM_CHANGED event to be dispatched.



---

# Working_with_Tables

# Working with Tables

The <tablecontrol> element displays content in rows and columns. The child element <header> defines the columns in the table. The child element <row> defines the table's rows. The <tablecontrol> sortedcolumn attribute specifies the column to use when sorting rows. (When rows are resorted in a dialog box, the order of the rows in the XUI XML document is not reordered.) The <tablecontrol> gridlines attribute specifies that rules are displayed between rows and columns.

If the <tablecontrol> showimages attribute is set to true , images specified in the <row> elements will appear in the table to the left of each row.

The following XUI markup defines this table:

```
<window width="125" height="200" focus="tablecontrol">
<tablecontrol id="tablecontrol" columns="2" value="Newton" gridlines="true">
<header>
<column label="Name"/>
<column label="Country"/>
</header>
<row>
<cell>Newton</cell>
<cell>England</cell>
</row>
<row>
<cell>Plato</cell>
<cell>Greece</cell>
</row>
</tablecontrol>
</window>
```



---

# Working_with_Toolbars

# Working with Toolbars

XUI provides limited toolbar support. You can create toolbars on dialog boxes using the <toolbargroup> and <toolbar> elements. A toolbar is made up of a collection of toolbar buttons defined with the <button> and <checkbox> elements. Other controls, such as <colordropdown> , <comboxbox> , <listdropdown> and <textbox> elements can be copied from those delivered with Arbortext Editor , but they cannot be customized. Refer to the following file for examples of the toolbars used by Arbortext Editor .

```
Arbortext-path
\lib\dialogs\editwindow.xml
```

Toolbar buttons invoke ACL functions using their command attributes. AOM calls and events are not supported.

You can display a XUI toolbar with the ACL function window_load_component_file() or with the AOM loadComponentFile method of the Window class.

Use the following ACL functions to control toolbars. ( toolbar_id is the value of the id attribute of the <toolbar> element in the XUI file.)

- • Hiding and showing toolbars

- • Hiding and showing a toolbar while also removing and adding the toolbar name to the View > Toolbars menu.

- • Removing toolbars

- • Temporarily removing or replacing a control in a toolbar. control_id is the id attribute of the element representing the control in the toolbar.



---

# Working_with_Trees

# Working with Trees

The <treecontrol> element creates a hierarchical outline view of data displayed as branches off of nodes. Each node in a <treecontrol> structure is created with a <treenode> element. A <treecontrol> element can have child <treecontrol> elements.

The <treecontrol> branchimage , extraimage , leafimage , openbranchimage , and selectedimage parameters let you specify images to appear to the left of node labels. The same parameters on <treenode> elements override those set on the <treecontrol> element.

The following XUI markup defines this tree control:

```
<window width="125" height="200" focus="treecontrol">
<treecontrol id="treecontrol" height="100">
<treenode label="Books" selected="true">
<treenode label="Fiction">
<treenode label="Fantasy"></treenode>
<treenode label="Mystery"></treenode>
<treenode label="Science"></treenode>
</treenode>
<treenode label="History" expanded="true">
<treenode label="Egypt"></treenode>
<treenode label="France"></treenode>
<treenode label="Thailand"></treenode>
</treenode>
</treenode>
</treecontrol>
</window>
```



---

# XUI_Dialog_Boxes_and_ACL

# XUI Dialog Boxes and ACL

All XUI dialog boxes support dlgitem_set() , dlgitem_get() , and all variations of dlgitem_set_ xxx () and dlgitem_get_ xxx () ACL functions. The id attribute of the element in the XUI document is the dialog box control name. If a control has no id specified, the control has no dialog box control name and cannot be used with dlgitem_set() .

For example, if the XUI document contains the following checkbox element:

```
<checkbox id="full" label="Full Menus"/>
```

you can use dlgitem_set(win, 'full', 'VALUE', 1) to mark the check box as checked.

When using any of the dlgitem_set_ xxx () functions, the value displayed in the dialog box control will be updated on-screen. However, the underlying XUI document will not change. That is, the value in the XUI document will not be updated by the dlgitem_set_ xxx () function.



---

# XUI_Display_Recommendations

# XUI Display Recommendations

When implementing XUI dialog boxes, you should add as many XUI controls to a dialog box as possible in a single pass to improve the display refresh of XUI dialog boxes.

For example, the following Java code adds ten controls to the dialog box one by one:

```
Element box = _xui.getElementById("AddControlsBox");
for(int i = 0; i < 10; ++i) {
Element textbox = _xui.createElement("textbox");
box.appendChild(textbox);
}
```

The dialog box display refresh would be improved by adding all ten controls to the dialog box at once as in the follow example:

```
DocumentFragment frag = _xui.createDocumentFragment();
for(int i = 0; i < 10; ++i) {
Element textbox = _xui.createElement("textbox");
frag.appendChild(textbox);
}
Element box = _xui.getElementById("AddControlsBox");
box.appendChild(frag);
```

For optimum display speed when clearing all listitems from a combobox or listbox , delete the items in order beginning with the firstChild .



---

# XUI_Element_Reference

# XUI Element Reference

PTC Arbortext Editor supports the following XUI elements for creating dialog box controls. The document type for XUI XML documents is Arbortext-path \doctypes\xui\xui.dtd .