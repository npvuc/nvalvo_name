

---

# Configuring_the_.dcf_File

To associate an element with an ActiveX control, edit the attributes of the ActiveXControl element in your custom .dcf file for the document type containing the element.

The ActiveXControl element has the following attributes:

As an example, a .dcf file's ActiveXControl element could have the following attributes:

```
<ActiveXControl
element="date"
controlName="cal"
scriptFileName="date.js"
scriptName="date"
programId="MSCAL.Calendar"
eventName="DOMActivate"
inPlaceActivate="no">
</ActiveXControl>
```

This example specifies the following association:

- • Run the control when a DOMActivate event happens on a date element.

- • Create a new Microsoft ActiveX Calendar control with a Program ID of MSCAL.Calendar .

- • Name the control “ cal ” in the script engines list of named variables. (This provides the name used for script event binding and the methods which write to and from the XML data, described below.)

- • If the control attached to this DOM element is running, bring it to the desktop foreground. If the control attached to this DOM element has not been launched, then create and display it.

- • Run the Cal_OnInitialize( activenode ) function. This function name is a combination of the control name “ Cal ”, an underscore character, and “ OnInitialize ”. activenode is the element causing the ActiveX control to be loaded.

- • Once the user selects a date and closes the control, the function Cal_OnClose( activenode ) captures the current date from the Calendar and inserts the <date> element's PCDATA.

Refer to the examples at the end of this section for other sample ActiveXControl attribute settings.



---

# Establishing_Element-to-Control_Binding

Elements and ActiveX scripts are linked and bound to one another in the scripting environment with a naming convention that uses the control name specified in the ActiveXControl tag. Using the convention controlname _ function , three script functions use this binding:

controlname _OnInitialize (activenode )

Performs all required control initialization, beyond that which might have been provided by any initialization file streams.

For example, the Cal _OnInitialize( activenode ) function for a Calendar control might set the current date in the Calendar control according to any value in the current <date> element. Cal _OnInitialize( activenode ) would retrieve the PCDATA:

The current date

and pass it to the Calendar.Value property to display as follows:

controlname _OnClose (activenode )

Modifies the XML data to reflect the final state of the ActiveX control. The function is not required, but is a logical way to synchronize the control data with the XML data. It is also a logical way to update the XML data in scripts that do not employ control event handlers.

When the user closes or cancels the dialog box, controlname _OnClose( activenode ) is called if it exists in the active script. controlname _OnClose( activenode ) is not called if the control is embedded in the document using inPlaceActivate .

controlname _OnCancel (activenode )

Performs any actions needed when Arbortext Editor closes a dialog box because its owner element was deleted. This function is optional, but can be useful to undo previous script actions in cases where XML data may have changed with control events. controlname _OnCancel( activenode ) is not called if the control is embedded in the document using inPlaceActivate .



---

# Example:_Calendar_Control

This example illustrates how to associate an ActiveX control with an element. Specifically, this example gives a means of entering dates into a document using the Microsoft Calendar Control.

The following files support this example and are available at the following locations:

- • Arbortext-path \samples\activex\date.js

- • Arbortext-path \samples\activex\date.vbs



---

# Example:_Entering_Address_Information_with_an_HTML_Form

This example illustrates how to display an HTML form for entering address data using the Microsoft WebBrowser control.

The following files support this example and are available at the following locations:

- • Arbortext-path \samples\activex\address.js

- • Arbortext-path \samples\activex\address.vbs

- • Arbortext-path \samples\activex\address.htm

Use the following steps to implement this example: