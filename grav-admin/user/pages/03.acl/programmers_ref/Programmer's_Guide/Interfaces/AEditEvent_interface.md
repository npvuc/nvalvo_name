

---

# bufferName_attribute

Identifies the name of the paste buffer that is used by the AOMCut , AOMCopy , or AOMPaste event. The standard paste buffer is named default.



---

# detail_attribute

Identifies detail information about the Event , depending on the type of event.



---

# initAEditEvent_method

Initializes the value of an AEditEvent created through the DocumentEvent interface. This method should only be called before the AEditEvent has been dispatched using the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times, the final invocation takes precedence.



---

# relatedRange_attribute

Identifies the Range that the event affects.