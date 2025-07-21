

---

# altKey_attribute

Used to indicate whether the 'alt' key was depressed during the firing of the event. On some platforms this key may map to an alternative key name.



---

# button_attribute

During mouse events caused by the depression or release of a mouse button, button is used to indicate which mouse button changed state. The values for button range from zero to indicate the left button of the mouse, one to indicate the middle button if present, and two to indicate the right button. For mice configured for left handed use in which the button actions are reversed the values are instead read from right to left.



---

# clientX_attribute

The horizontal coordinate at which the event occurred relative to the DOM implementation's client area.



---

# clientY_attribute

The vertical coordinate at which the event occurred relative to the DOM implementation's client area.



---

# ctrlKey_attribute

Used to indicate whether the 'ctrl' key was depressed during the firing of the event.



---

# initMouseEvent_method

The initMouseEvent method is used to initialize the value of a MouseEvent created through the DocumentEvent interface. This method may only be called before the MouseEvent has been dispatched via the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times, the final invocation takes precedence.



---

# metaKey_attribute

Used to indicate whether the 'meta' key was depressed during the firing of the event. On some platforms this key may map to an alternative key name.



---

# relatedTarget_attribute

Used to identify a secondary EventTarget related to a UI event. Currently this attribute is used with the mouseover event to indicate the EventTarget which the pointing device exited and with the mouseout event to indicate the EventTarget which the pointing device entered.



---

# screenX_attribute

The horizontal coordinate at which the event occurred relative to the origin of the screen coordinate system.



---

# screenY_attribute

The vertical coordinate at which the event occurred relative to the origin of the screen coordinate system.



---

# shiftKey_attribute

Used to indicate whether the 'shift' key was depressed during the firing of the event.