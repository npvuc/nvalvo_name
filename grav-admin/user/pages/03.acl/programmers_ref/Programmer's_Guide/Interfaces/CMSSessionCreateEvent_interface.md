

---

# end_attribute

DOM end Node associated with the event.



---

# errorCode_attribute

Used when the event handler wants to cancel the operation or throw an error exception. This can hold any defined CMSExceptionCode value. To cancel the operation, call preventDefault() and store a value of OPERATION_CANCELED_ERR into errorCode . To cause an error exception, call preventDefault() , store any other defined CMSExceptionCode value into errorCode , and optionally store a message into errorMessage .



---

# errorMessage_attribute

Used when the event handler wants to throw an error exception and additionally provide a human-readable error message. To do this, call preventDefault() , store the appropriate value into errorCode , and store a message into errorMessage .



---

# flags_attribute

Creation options. Same as the flags parameter of the CMSSession.createNewObject .



---

# folderLogicalId_attribute

Parent folder for the new object.



---

# initCMSSessionCreateEvent_method

Initializes the value of an CMSSessionCreateEvent created through the CMSSessionCreateEvent interface. This method should only be called before the CMSSessionCreateEvent has been dispatched using the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times, the final invocation takes precedence.



---

# name_attribute

Name of the object being created.



---

# objType_attribute

Adapter-specific object type string.



---

# result_attribute

The CMS object created.



---

# start_attribute

DOM start Node associated with the event.



---

# version_attribute

The object's version number. The value is represented using CMS-specific syntax.