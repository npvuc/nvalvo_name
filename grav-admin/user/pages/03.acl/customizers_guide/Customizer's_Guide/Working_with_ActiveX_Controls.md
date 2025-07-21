

---

# Executing_ActiveX_Controls_Using_the_.dcf_File_to_Bind_to_an_Element_Directly

# Executing ActiveX Controls Using the .dcf File to Bind to an Element Directly

As an alternative to using an external XUI file to define the display of an ActiveX control, you can associate ActiveX controls with elements directly in the .dcf file, causing the controls to execute when triggered by specific DOM events. To use this alternate method to execute ActiveX controls from elements, you need to update your .dcf file to associate the element with the ActiveX control and related script. You also need to establish the proper element-to-control binding in the script.

Keep the following items in mind when using this method to associate ActiveX controls with elements:

- • Arbortext Editor tracks the element-control relationships by element name. Therefore, a document can contain only one instance of a given element and its associated ActiveX control. For example, a document may contain numerous instances of an element that is associated with an ActiveX control, but only one ActiveX control can be displayed at any given moment.

- • Each element must be associated with one script, creating a configuration trio of one element name to one script name to one control. A given control may be used multiple times, as long as each instance resides in its own configuration trio. A given script file can be used multiple times, as long as the script name (as specified in the ActiveXControl element), is unique in each trio.



---

# Executing_ActiveX_Controls_Using_XUI

# Executing ActiveX Controls Using XUI

You can implement ActiveX controls using the XUI <activex> control. (You can also implement ActiveX controls directly from the .dcf file. That implementation is detailed in Executing ActiveX Controls Using the .dcf File to Bind to an Element Directly .) The <activex> element is fully defined in the Working with XUI (XML-based User Interface) dialog boxes chapter of the Customizer's Guide , and can be described using XUI as in the following example:

```
<activex progid = "MSCAL.Calendar" id = "date">
</activex>
```

The progid attribute specifies which ActiveX control is to be added to the dialog box. It can either be a Program ID for the control, as shown in the previous example, or the value of the control's CLSID property as a string surrounded by curly brackets as in the following example:

```
<activex progid="{2398E32F-5C6E-11D1-8C65-0060081841DE}" id="TextToSpeach">
</activex>
```

The id parameter identifies the control.

Using the <param> child tag of the <activex> element allows you to provide parameters name-value pairs for the ActiveX control. For example:

```
<activex progid="MSCAL.Calendar" id="date">
<param name="ShowDateSelectors" value="false"/>
</activex>
```

By setting the parameter ShowDateSelectors to false , the date selector dropdowns (one for the month and another for the year) are removed from the Calendar ActiveX control.

An ActiveX control can be launched embedded in the document displayed in Arbortext Editor , as a standalone control, or as a control within a XUI dialog box. When launched as a standalone control, a XUI dialog box is automatically generated to contain the control.



---

# Integrating_Arbortext_Editor_with_Web_Pages

# Integrating Arbortext Editor with Web Pages

On the Microsoft Windows platform, you can set up links in web pages that will open an Arbortext Editor session.

You can use the arbortext-editor protocol (or scheme) in a URI (Uniform Resource Identifier) to invoke Arbortext Editor from a link. Sample web integration implementations are available in the Arbortext-path \samples\web-integration directory. Refer to the readme.txt file in that directory for a description of the samples.



---

# Running_Arbortext_Editor_in_an_ActiveX_Control

# Running Arbortext Editor in an ActiveX Control

Besides running other ActiveX controls inside of Arbortext Editor , you can run Arbortext Editor itself in an ActiveX control. The Arbortext Editor ActiveX control is located at Arbortext-path \bin\EditorControl.dll . This control is registered as a COM server whenever the associated version of Arbortext Editor is registered.

Arbortext Editor can run as an embedded ActiveX control inside of another window or dialog box. In this case, the Arbortext Editor menus are made available through a new Menu toolbar button. Also, some menu choices and toolbar buttons are not available in an embedded frame.

Sample Arbortext Editor ActiveX implementations are in the Arbortext-path \samples\activex_editor directory. The XUI directory has a sample XUI dialog box containing an embedded Arbortext Editor ActiveX control. The CSharp directory contains a sample C# implementation. These examples demonstrate how to use the return value of the open method (which is an ACL window id) with the Acl.getWindow AOM method to obtain a Window AOM object. This technique provides the caller with great control over the window and the document living in it.