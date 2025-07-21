

---

# detail_attribute

Specifies detail information about the ApplicationEvent , depending on the type of event.



---

# initApplicationEvent_method

Initializes the value of an ApplicationEvent created through the Application interface. This method should only be called before the ApplicationEvent has been dispatched using the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times, the final invocation takes precedence.