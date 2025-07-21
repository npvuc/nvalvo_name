

---

# Box_Layout

The Box layout model divides a portion of the dialog box into a series of nested containers using the <box> element. Each container is oriented horizontally or vertically. Controls inside each container are listed in order according to the orientation of the container.

For example, the following dialog box can be expressed by using seven containers:

Dialog box with the following controls.

This dialog box can be described using XUI as follows:

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN" "xui.dtd">
<window orient="horizontal" focus="findtext" modal="false" title="Find">
<box orient="vertical">
<box orient="horizontal">
<label label="Fi&nd What:"/>
<textbox id="findtext">
<value></value>
</textbox>
</box>
<box orient="horizontal">
<box orient="vertical">
<checkbox label="Match &whole word only"></checkbox>
<checkbox label="Match &case"></checkbox>
</box>
<radiogroup label="Direction" resize="both" orient="horizontal">
<radio label="&Up"></radio>
<radio label="&Down"></radio>
</radiogroup>
</box>
</box>
<spacer resize="none" width="4"/>
<box orient="vertical" pack="start">
<button label="&Find Next" type="accept"></button>
<button label="Cancel" type="cancel"></button>
</box>
</window>
```

The <box> element has attributes for customizing the layout. For example, the attribute pack specifies how extra space should be distributed. The attribute orient specifies the baseline of the controls in a box. Refer to <box> Element for a detailed description of the <box> element.



---

# Grid_Layout

The Grid layout model lets you display a group of controls in rows and columns using the <grid> element.

For example, the following dialog box uses the Grid layout.

Dialog box with a Grid layout.

This dialog box has two columns and four rows. It is described using XUI as follows:

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN" "xui.dtd">
<window orient="vertical" modal="true" title="Register">
<grid columns="2">
<label label="&Name:"/>
<textbox width="180">
<value></value> </textbox>
<label label="&Organization:"/>
<textbox>
<value></value>
</textbox>
<label label="&Address:"/>
<textbox>
<value></value>
</textbox>
<label label="&Telephone:"/>
<textbox>
<value></value>
</textbox>
</grid>
<spacer height="8" resize="none"/>
<box orient="horizontal" pack="center">
<button label="&OK" type="accept"/>
<button label="Cancel" type="cancel"/>
</box>
</window>
```

Refer to <grid> Element for a detailed description of the <grid> element.



---

# Morph_Layout

The Morph layout uses the <morph> element to create a dialog box that dynamically adjusts the layout of its contents. This makes the Morph layout very useful for displaying a dialog box with an varying set of controls based on context or containing a large number of controls.

Consider a dialog box with a Morph layout that initially displays its contents in the same manner as a Grid layout:

A dialog box with a Morph layout with a single column of label and related textbox controls.

As the dialog box is resized, the layout may change to include additional columns. For example:

A dialog box with a Morph layout with two columns of label and related textbox controls.

When the dialog box is resized so small that all of the elements can no longer be displayed, the layout changes to a tabbed box. For example:

A dialog box with a Morph layout with tabs, each with a single column of label and related textbox controls.

This Morph dialog box is described in XML as follows:

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.1//EN" "xui.dtd">
<window title="Modify Attribute">
<box orient="horizontal">
<box orient="vertical">
<grid morph="true">
<label label="boardno:"/>
<combobox dropdown="true">
<listitem label="usafseal"/>
</combobox>
<label label="graphsty:"/> <textbox/>
<label label="llcordra:"/> <textbox/>
<label label="rucordra:"/> <textbox/>
<label label="reprowid:"/> <textbox/>
<label label="reprode:p"/> <textbox/>
<label label="hscale:"/> <textbox/>
<label label="vscale:"> <textbox/>
<label label="scalefit:"/> <textbox/>
<label label="hplace:"/>
<combobox dropdown="true">
<listitem label="center"/>
<listitem label="left"/>
<listitem label="none"/>
<listitem label="right"/>
</combobox>
<label label="vplace:"/>
<combobox dropdown="true">
<listitem label="bottom"/>
<listitem label="middle"/>
<listitem label="none"/>
<listitem label="top"/>
</combobox>
<label label="coordst:"/> <textbox/>
<label label="coordend:"/> <textbox/>
<label label="rotation:"/> <textbox/>
<label label="security:"/>
<combobox dropdown="true">
<listitem label="c"/>
<listitem label="s"/>
<listitem label="u"/>
</combobox>
</grid>
<description label="Element: graphic"/>
</box>
<box orient="vertical">
<button label="OK"/>
<button label="Cancel"/>
<button label="Help"/>
<button label="Validate"/>
<button label="Reset"/>
<button label="Reset All"/>
<button label="Delete"/>
<button label="Delete All"/>
</box>
</box>
</window>
```

The PTC Arbortext Editor Modify Attributes dialog box is an example of a Morph layout. While editing a document with PTC Arbortext Editor , choose Edit > Modify Attributes . The Modify Attributes dialog box displays all of the attributes for the current element. If you resize the dialog box, the layout changes to accommodate the controls.

Refer to <morph> Element for a detailed description of the <morph> element.