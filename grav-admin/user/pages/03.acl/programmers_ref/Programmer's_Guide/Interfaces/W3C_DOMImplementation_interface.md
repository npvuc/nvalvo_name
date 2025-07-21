

---

# createDocument_method

Creates an XML Document object of the specified type with its document element. HTML-only DOM implementations do not need to implement this method.



---

# createDocumentType_method

Creates an empty DocumentType node. Entity declarations and notations are not made available. Entity reference expansions and default attribute additions do not occur. It is expected that a future version of the DOM will provide a way for populating a DocumentType .

HTML-only DOM implementations do not need to implement this method.



---

# getFeature_method

This method returns a specialized object which implements the specialized APIs of the specified feature and version, as specified in . The specialized object may also be obtained by using binding-specific casting methods but is not necessarily expected to, as discussed in . This method also allow the implementation to provide specialized objects which do not support the DOMImplementation interface.



---

# hasFeature_method

Test if the DOM implementation implements a specific feature.