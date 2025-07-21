

---

# continuousValidityChecking_attribute

An attribute specifying whether the validity of the document is continuously enforced. When the attribute is set to true , the implementation may raise certain exceptions, depending on the situation (see the following). This attribute is false by default.



---

# getDefinedElements_method

Returns list of all element information item names of global declaration, belonging to the specified namespace.



---

# validateDocument_method

Validates the document against the schema, e.g., a DTD or an W3C XML schema or another. Any attempt to modify any part of the document while validating results in implementation-dependent behavior. In addition, the validation operation itself cannot modify the document, e.g., for default attributes. This method makes use of the error handler, as described in the [ DOM Level 3 Core ] DOMConfiguration interface, with all errors being SEVERITY_ERROR as defined in the DOMError interface.