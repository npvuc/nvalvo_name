

---

# adoptNode_method

Attempts to adopt a node from another document to this document. If supported, it changes the ownerDocument of the source node, its children, as well as the attached attribute nodes if there are any. If the source node has a parent it is first removed from the child list of its parent. This effectively allows moving a subtree from one document to another (unlike importNode() which create a copy of the source node instead of moving it). When it fails, applications should use Document.importNode() instead. Note that if the adopted node is already part of this document (i.e. the source and target document are the same), this method still has the effect of removing the source node from the child list of its parent, if any. The following list describes the specifics for each type of node.



---

# createAttribute_method

Creates an Attr of the given name. Note that the Attr instance can then be set on an Element using the setAttributeNode method.

To create an attribute with a qualified name and namespace URI, use the createAttributeNS method.



---

# createAttributeNS_method

Creates an attribute of the given qualified name and namespace URI. HTML-only DOM implementations do not need to implement this method.



---

# createCDATASection_method

Creates a CDATASection node whose value is the specified string.



---

# createComment_method

Creates a Comment node given the specified string.



---

# createDocumentFragment_method

Creates an empty DocumentFragment object.



---

# createElement_method

Creates an element of the type specified. Note that the instance returned implements the Element interface, so attributes can be specified directly on the returned object.

In addition, if there are known attributes with default values, Attr nodes representing them are automatically created and attached to the element.

To create an element with a qualified name and namespace URI, use the createElementNS method.



---

# createElementNS_method

Creates an element of the given qualified name and namespace URI. HTML-only DOM implementations do not need to implement this method.



---

# createEntityReference_method

Creates an EntityReference object. In addition, if the referenced entity is known, the child list of the EntityReference node is made the same as that of the corresponding Entity node.



---

# createProcessingInstruction_method

Creates a ProcessingInstruction node given the specified name and data strings.



---

# createTextNode_method

Creates a Text node given the specified string.



---

# doctype_attribute

The Document Type Declaration (see DocumentType ) associated with this document. For HTML documents as well as XML documents without a document type declaration this returns null . The DOM Level 2 does not support editing the Document Type Declaration. docType cannot be altered in any way, including through the use of methods inherited from the Node interface, such as insertNode or removeNode .



---

# documentElement_attribute

This is a convenience attribute that allows direct access to the child node that is the root element of the document. For HTML documents, this is the element with the tagName "HTML".



---

# documentURI_attribute

The location of the document or null if undefined or if the Document was created using DOMImplementation.createDocument . No lexical checking is performed when setting this attribute; this could result in a null value returned when using Node.baseURI .

Beware that when the Document supports the feature "HTML" [ DOM Level 2 HTML ], the href attribute of the HTML BASE element takes precedence over this attribute when computing Node.baseURI .



---

# domConfig_attribute

The configuration used when Document.normalizeDocument is invoked.



---

# getElementById_method

Returns the Element whose ID is given by elementId . If no such element exists, returns null . Behavior is not defined if more than one element has this ID .



---

# getElementsByTagName_method

Returns a NodeList of all the Elements with a given tag name in the order in which they are encountered in a preorder traversal of the Document tree.



---

# getElementsByTagNameNS_method

Returns a NodeList of all the Elements with a given local name and namespace URI in the order in which they are encountered in a preorder traversal of the Document tree.



---

# implementation_attribute

The DOMImplementation object that handles this document. A DOM application may use objects from multiple implementations.



---

# importNode_method

Imports a node from another document to this document. The returned node has no parent; ( parentNode is null ). The source node is not altered or removed from the original document; this method creates a new copy of the source node.

For all nodes, importing a node creates a node object owned by the importing document, with attribute values identical to the source node's nodeName and nodeType , plus the attributes related to namespaces ( prefix , localName , and namespaceURI ). As in the cloneNode operation on a Node , the source node is not altered.

Additional information is copied as appropriate to the nodeType , attempting to mirror the behavior expected if a fragment of XML or HTML source was copied from one document to another, recognizing that the two documents may have different DTDs in the XML case. The following list describes the specifics for each type of node.



---

# inputEncoding_attribute

An attribute specifying the encoding used for this document at the time of the parsing. This is null when it is not known, such as when the Document was created in memory.



---

# normalizeDocument_method

This method acts as if the document was going through a save and load cycle, putting the document in a "normal" form. As a consequence, this method updates the replacement tree of EntityReference nodes and normalizes Text nodes, as defined in the method Node.normalize() .

Otherwise, the actual result depends on the features being set on the Document.domConfig object and governing what operations actually take place. Noticeably this method could also make the document namespace well-formed according to the algorithm described in , check the character normalization, remove the CDATASection nodes, etc. See DOMConfiguration for details.

```
// Keep in the document the information defined
// in the XML Information Set (Java example)
DOMConfiguration docConfig = myDocument.getDomConfig();
docConfig.setParameter("infoset", Boolean.TRUE);
myDocument.normalizeDocument();
```

Mutation events, when supported, are generated to reflect the changes occurring on the document.

If errors occur during the invocation of this method, such as an attempt to update a read-only node or a Node.nodeName contains an invalid character according to the XML version in use, errors or warnings ( DOMError.SEVERITY_ERROR or DOMError.SEVERITY_WARNING ) will be reported using the DOMErrorHandler object associated with the " error-handler" parameter. Note this method might also report fatal errors ( DOMError.SEVERITY_FATAL_ERROR ) if an implementation cannot recover from an error.



---

# renameNode_method

Rename an existing node of type ELEMENT_NODE or ATTRIBUTE_NODE .

When possible this simply changes the name of the given node, otherwise this creates a new node with the specified name and replaces the existing node with the new node as described below.

If simply changing the name of the given node is not possible, the following operations are performed: a new node is created, any registered event listener is registered on the new node, any user data attached to the old node is removed from that node, the old node is removed from its parent if it has one, the children are moved to the new node, if the renamed node is an Element its attributes are moved to the new node, the new node is inserted at the position the old node used to have in its parent's child nodes list if it has one, the user data that was attached to the old node is attached to the new node.

When the node being renamed is an Element only the specified attributes are moved, default attributes originated from the DTD are updated according to the new element name. In addition, the implementation may update default attributes from other schemas. Applications should use Document.normalizeDocument() to guarantee these attributes are up-to-date.

When the node being renamed is an Attr that is attached to an Element , the node is first removed from the Element attributes map. Then, once renamed, either by modifying the existing node or creating a new one as described above, it is put back.

In addition,

- • a user data event NODE_RENAMED is fired,

- • when the implementation supports the feature "MutationNameEvents", each mutation operation involved in this method fires the appropriate event, and in the end the event { http://www.w3.org/2001/xml-events , DOMElementNameChanged } or { http://www.w3.org/2001/xml-events , DOMAttributeNameChanged } is fired.



---

# strictErrorChecking_attribute

An attribute specifying whether error checking is enforced or not. When set to false , the implementation is free to not test every possible error case normally defined on DOM operations, and not raise any DOMException on DOM operations or report errors while using Document.normalizeDocument() . In case of error, the behavior is undefined. This attribute is true by default.



---

# xmlEncoding_attribute

An attribute specifying, as part of the XML declaration, the encoding of this document. This is null when unspecified or when it is not known, such as when the Document was created in memory.



---

# xmlStandalone_attribute

An attribute specifying, as part of the XML declaration, whether this document is standalone. This is false when unspecified.



---

# xmlVersion_attribute

An attribute specifying, as part of the XML declaration, the version number of this document. If there is no declaration and if this document supports the "XML" feature, the value is "1.0" . If this document does not support the "XML" feature, the value is always null . Changing this attribute will affect methods that check for invalid characters in XML names. Application should invoke Document.normalizeDocument() in order to check for invalid characters in the Node s that are already part of this Document .

DOM applications may use the DOMImplementation.hasFeature(feature, version) method with parameter values "XMLVersion" and "1.0" (respectively) to determine if an implementation supports [ XML 1.0 ]. DOM applications may use the same method with parameter values "XMLVersion" and "1.1" (respectively) to determine if an implementation supports [ XML 1.1 ]. In both cases, in order to support XML, an implementation must also support the "XML" feature defined in this specification. Document objects supporting a version of the "XMLVersion" feature must not raise a NOT_SUPPORTED_ERR exception for the same version number when using Document.xmlVersion .