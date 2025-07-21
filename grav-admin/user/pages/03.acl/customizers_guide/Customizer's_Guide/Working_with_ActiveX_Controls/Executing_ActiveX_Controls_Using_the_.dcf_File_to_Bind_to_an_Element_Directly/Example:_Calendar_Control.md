

---

# Implementation

Use the following steps to implement this example:



---

# Operation_Overview

In this scenario, assume your users want to choose dates from the Calendar control interface instead of having to type the PCDATA into a date element.

The users interact with the Calendar control in the following manner:

First, the user inserts or double-clicks a date element. Second, Arbortext Editor displays the ActiveX control. Third, the user uses the calendar interface to visually select a date and close the control. Fourth, the script retrieves the data from the calendar and inserts it into the DOM Text Node.



---

# Scripting_Overview

From an implementation perspective, the following actions occur.

- • When the user double-clicks the mouse or presses shift-Enter on a <date> element, a DOMActivate event is triggered.

- • The script file date.js (which we named date ) is executed.

- • The Calendar control is displayed.

- • The Calendar control is assigned the variable name cal . This lets the script have access to the control's methods and properties.

- • The script method cal_OnInitialize(ActiveNode) is called.

- • When the user closes the dialog box, the script method cal_OnClose(ActiveNode) is called.