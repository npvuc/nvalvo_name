

---

# detail_attribute

Specifies detail information about the ADocumentEvent , depending on the type of event.



---

# initADocumentEvent_method

Initializes the value of an ADocumentEvent created through the DocumentEvent interface. You should only call this method before the ADocumentEvent has been dispatched using the dispatchEvent method, though it can be called multiple times during that phase if necessary. If the initADocumentEvent is called multiple times, the final call takes precedence.



---

# relatedDocument_attribute

The relatedDocument attribute identifies a document related to the event. For DocumentCreate event, if the new document is cloned from another document, the relatedDocument is the source document that the new document is cloned from.



---

# relatedWindow_attribute

The relatedWindow attribute identifies a window related to the event. For the DocumentLoad event, relatedWindow is the window that the document loads to. For the DocumentUnload event, relatedWindow is the window that the document unloads from, as long as the window still exists. If the window is destroyed along with the document, then relatedWindow is null .



---

# targetEncoding_attribute

Specifies the encoding in which the document is saved in a DocumentSaving event.



---

# targetURI_attribute

Specifies the URI in which the document is saved in a DocumentSaving event.