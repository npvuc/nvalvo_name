

---

# DOM_Limitations

The Arbortext implementation of the DOM may be used with SGML documents. Because the DOM portion of the AOM is XML- and HTML-based, features in Arbortext Editor that are available only for SGML, but not for XML, are not supported (such as IGNORE marked sections).

The DOM standard states that management of namespace-qualified elements and attributes will be performed without the insertion or modification of namespace-related XML attributes, at least until a document is actually written to disk. Instead, Arbortext Editor inserts xmlns and xmlns:prefix XML attributes as needed to establish and maintain namespace/prefix bindings.

Arbortext Editor does not return the document type's internal subset, if any. The internalSubset of the DocumentType interface will always return a null string.



---

# DOM_Programming_Considerations

The following programming considerations apply to all language bindings:

- • Document context

- • Performance issues



---

# Using_the_DOM_with_SGML_Documents

The DOM is designed to support XML documents. The DOM support for SGML documents is limited to parallel support for XML. If you'll be working with SGML documents, the DOM will ignore IGNORE marked sections and RCDATA sections. If an element in an SGML document contains three sub-elements, and one of the sub-elements is an IGNORE marked section or an RCDATA section, user-written DOM programs will see only two sub-elements.