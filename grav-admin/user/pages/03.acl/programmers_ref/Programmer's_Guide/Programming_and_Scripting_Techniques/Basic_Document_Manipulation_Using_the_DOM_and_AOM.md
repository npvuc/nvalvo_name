

---

# Inserting_Text

Text can be added at any appropriate place in a document by creating and inserting a new Text node. Document.createTextNode takes a text string as an argument, and returns a new node ( Text object) that can be inserted by calling methods such as Node.appendChild or Node.insertBefore on the desired node.



---

# Opening,_Closing,_and_Saving_documents

DOM Level 2 does not provide methods to open, save, and close documents. However, the AOM includes methods on the Application and ADocument interfaces that implement these capabilities.

The Application interface openDocument method returns a Document object that has information about a document or document type and can be used to dynamically update the content, structure, and style of the document

The openDocument method takes several optional parameters, including the flags parameter, which controls the state in which the document is opened. This parameter is constructed by adding the hex values of the LoadFlag enumeration constants. (The symbolic constant names can be used instead with some language bindings.) Refer to Application interface for a complete listing and full descriptions of the LoadFlag enumeration constants. The following table highlights a selection of these constants.

In the following code, the flags parameter is used to open a document for read and write while suppressing any parser errors:

```
var doc = Application.openDocument("mydocument.xml", (0x0002 + 0x0020))
```

Once a document is opened, it can be manipulated and then saved and closed using methods of the ADocument interface (which extends the W3C DOM Document interface).

ADocument.save writes the document to disk. The save method's flags parameter determines the state of the saved document.

ADocument.close frees all resources associated with the Document object.

Refer to the examples in the remainder of this chapter for several sample uses of the Application.openDocument , ADocument.save , and ADocument.close methods.



---

# Selecting,_Copying,_Moving_Content

The following examples demonstrate how to copy, cut, and paste content within and between documents.



---

# Traversing_a_Document_Using_the_DOM_and_AOM

A Document object is the tree representation of the document's structure. Like any tree, the document can be traversed several ways.



---

# Using_Range_to_Select_and_Delete_Content

The W3C DOM Range API consists of a single interface, Range . This interface exposes the ability to select contiguous portions of a structured document, delineated by specified beginning and end points. The Range interface contains methods that allow copying, inserting, or deleting of content, as well as methods for marking the start and end points of the content range.