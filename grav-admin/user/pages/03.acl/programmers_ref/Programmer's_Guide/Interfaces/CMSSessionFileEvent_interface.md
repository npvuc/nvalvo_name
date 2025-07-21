

---

# errorCode_attribute

Used when the event handler wants to cancel the operation or throw an error exception. This can hold any defined CMSExceptionCode value. To cancel the operation, call preventDefault() and store a value of OPERATION_CANCELED_ERR into errorCode . To cause an error exception, call preventDefault() , store any other defined CMSExceptionCode value into errorCode , and optionally store a message into errorMessage .



---

# errorMessage_attribute

Used when the event handler wants to throw an error exception and additionally provide a human-readable error message. To do this, call preventDefault() , store the appropriate value into errorCode , and store a message into errorMessage .



---

# folderLogicalId_attribute

Parent folder for the CMS object.



---

# initCMSSessionFileEvent_method

Initializes the value of an CMSSessionFileEvent created through the CMSSessionFileEvent interface. This method should only be called before the CMSSessionFileEvent has been dispatched using the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times, the final invocation takes precedence.



---

# localPath_attribute

Full path to a resource (file or HTTP) accessible from the client.



---

# logicalId_attribute

LogicalId for the object being accessed.



---

# notation_attribute

An adapter-specific format specification.



---

# objectName_attribute

Name of a repository object.



---

# result_attribute

The logical ID of an object created in the repository.