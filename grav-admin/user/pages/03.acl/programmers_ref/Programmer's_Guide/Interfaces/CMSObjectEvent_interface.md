

---

# end_attribute

Specifies an event-dependent DOM end Node associated with the event.



---

# errorCode_attribute

Used when the event handler wants to cancel the operation or throw an error exception. This can hold any defined CMSExceptionCode value. To cancel the operation, call preventDefault() and store a value of OPERATION_CANCELED_ERR into errorCode . To cause an error exception, call preventDefault() , store any other defined CMSExceptionCode value into errorCode , and optionally store a message into errorMessage .



---

# errorMessage_attribute

Used when the event handler wants to throw an error exception and additionally provide a human-readable error message. To do this, call preventDefault() , store the appropriate value into errorCode , and store a message into errorMessage .



---

# flags_attribute

Provides an event-dependent bitmask of information.



---

# initCMSObjectEvent_method

Initializes the value of an CMSObjectEvent created through the CMSObjectEvent interface. This method should only be called before the CMSObjectEvent has been dispatched using the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times, the final invocation takes precedence.



---

# result_attribute

Represents the event-dependent result of an event.



---

# start_attribute

Specifies an event-dependent DOM start Node associated with the event.