

---

# initActivexEvent_method

Initializes the value of an ActivexEvent created through the Window createEvent method. This method should only be called before the ActivexEvent has been dispatched with the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times, the final invocation takes precedence.