

---

# bubbles_attribute

Used to indicate whether or not an event is a bubbling event. If the event can bubble the value is true, else the value is false.



---

# cancelable_attribute

Used to indicate whether or not an event can have its default action prevented. If the default action can be prevented the value is true, else the value is false.



---

# currentTarget_attribute

Used to indicate the EventTarget whose EventListeners are currently being processed. This is particularly useful during capturing and bubbling.



---

# eventPhase_attribute

Used to indicate which phase of event flow is currently being evaluated.



---

# initEvent_method

The initEvent method is used to initialize the value of an Event created through the DocumentEvent interface. This method may only be called before the Event has been dispatched via the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times the final invocation takes precedence. If called from a subclass of Event interface only the values specified in the initEvent method are modified, all other attributes are left unchanged.



---

# PhaseType_enumeration

An integer indicating which phase of event flow is being processed.

The PhaseType enumeration has the following constants of type unsigned short .



---

# preventDefault_method

If an event is cancelable, the preventDefault method is used to signify that the event is to be canceled, meaning any default action normally taken by the implementation as a result of the event will not occur. If, during any stage of event flow, the preventDefault method is called the event is canceled. Any default action associated with the event will not occur. Calling this method for a non-cancelable event has no effect. Once preventDefault has been called it will remain in effect throughout the remainder of the event's propagation. This method may be used during any stage of event flow.



---

# stopPropagation_method

The stopPropagation method is used prevent further propagation of an event during event flow. If this method is called by any EventListener the event will cease propagating through the tree. The event will complete dispatch to all listeners on the current EventTarget before event flow stops. This method may be used during any stage of event flow.



---

# target_attribute

Used to indicate the EventTarget to which the event was originally dispatched.



---

# timeStamp_attribute

Used to specify the time (in milliseconds relative to the epoch) at which the event was created. Due to the fact that some systems may not provide this information the value of timeStamp may be not available for all events. When not available, a value of 0 will be returned. Examples of epoch time are the time of the system start or 0:0:0 UTC 1st January 1970.



---

# type_attribute

The name of the event (case-insensitive). The name must be an XML name.