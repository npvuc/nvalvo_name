

---

# canOverride_attribute

If true, for the CMSSessionBurstDocument event, the event handler can override the values in the topLevelName and folderLogicalId properties.



---

# document_attribute

For the CMSSessionBurstDocument event, this is the document that will be burst. For the CMSSessionPostBurstDocument event, this is the document that was burst.



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

Parent folder for the CMS object.



---

# initCMSSessionBurstDocumentEvent_method

Initializes the value of an CMSSessionBurstDocumentEvent created through the CMSSessionBurstDocumentEvent interface. This method should only be called before the CMSSessionBurstDocumentEvent has been dispatched using the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times, the final invocation takes precedence.



---

# topLevelName_attribute

Name of the top-level object which will result from bursting the document. This may be null or empty which means the name will be auto-generated according to the bursting rules for this adapter. For the CMSSessionBurstDocument event, the event handler can override this value if canOverride is true.