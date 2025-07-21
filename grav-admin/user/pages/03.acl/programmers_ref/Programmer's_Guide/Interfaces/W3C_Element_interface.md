

---

# getAttribute_method

Retrieves an attribute value by name.



---

# getAttributeNode_method

Retrieves an attribute node by name.

To retrieve an attribute node by qualified name and namespace URI, use the getAttributeNodeNS method.



---

# getAttributeNodeNS_method

Retrieves an Attr node by local name and namespace URI. HTML-only DOM implementations do not need to implement this method.



---

# getAttributeNS_method

Retrieves an attribute value by local name and namespace URI. HTML-only DOM implementations do not need to implement this method.



---

# getElementsByTagName_method

Returns a NodeList of all descendant Elements with a given tag name, in the order in which they are encountered in a preorder traversal of this Element tree.



---

# getElementsByTagNameNS_method

Returns a NodeList of all the descendant Elements with a given local name and namespace URI in the order in which they are encountered in a preorder traversal of this Element tree.

HTML-only DOM implementations do not need to implement this method.



---

# hasAttribute_method

Returns true when an attribute with a given name is specified on this element or has a default value, false otherwise.



---

# hasAttributeNS_method

Returns true when an attribute with a given local name and namespace URI is specified on this element or has a default value, false otherwise. HTML-only DOM implementations do not need to implement this method.



---

# removeAttribute_method

Removes an attribute by name. If the removed attribute is known to have a default value, an attribute immediately appears containing the default value as well as the corresponding namespace URI, local name, and prefix when applicable.

To remove an attribute by local name and namespace URI, use the removeAttributeNS method.



---

# removeAttributeNode_method

Removes the specified attribute node. If the removed Attr has a default value it is immediately replaced. The replacing attribute has the same namespace URI and local name, as well as the original prefix, when applicable.



---

# removeAttributeNS_method

Removes an attribute by local name and namespace URI. If the removed attribute has a default value it is immediately replaced. The replacing attribute has the same namespace URI and local name, as well as the original prefix.

HTML-only DOM implementations do not need to implement this method.



---

# schemaTypeInfo_attribute

The type information associated with this element.



---

# setAttribute_method

Adds a new attribute. If an attribute with that name is already present in the element, its value is changed to be that of the value parameter. This value is a simple string; it is not parsed as it is being set. So any markup (such as syntax to be recognized as an entity reference) is treated as literal text, and needs to be appropriately escaped by the implementation when it is written out. In order to assign an attribute value that contains entity references, the user must create an Attr node plus any Text and EntityReference nodes, build the appropriate subtree, and use setAttributeNode to assign it as the value of an attribute.

To set an attribute with a qualified name and namespace URI, use the setAttributeNS method.



---

# setAttributeNode_method

Adds a new attribute node. If an attribute with that name ( nodeName ) is already present in the element, it is replaced by the new one.

To add a new attribute node with a qualified name and namespace URI, use the setAttributeNodeNS method.



---

# setAttributeNodeNS_method

Adds a new attribute. If an attribute with that local name and that namespace URI is already present in the element, it is replaced by the new one.

HTML-only DOM implementations do not need to implement this method.



---

# setAttributeNS_method

Adds a new attribute. If an attribute with the same local name and namespace URI is already present on the element, its prefix is changed to be the prefix part of the qualifiedName , and its value is changed to be the value parameter. This value is a simple string; it is not parsed as it is being set. So any markup (such as syntax to be recognized as an entity reference) is treated as literal text, and needs to be appropriately escaped by the implementation when it is written out. In order to assign an attribute value that contains entity references, the user must create an Attr node plus any Text and EntityReference nodes, build the appropriate subtree, and use setAttributeNodeNS or setAttributeNode to assign it as the value of an attribute.

HTML-only DOM implementations do not need to implement this method.



---

# setIdAttribute_method

If the parameter isId is true , this method declares the specified attribute to be a user-determined ID attribute. This affects the value of Attr.isId and the behavior of Document.getElementById , but does not change any schema that may be in use, in particular this does not affect the Attr.schemaTypeInfo of the specified Attr node. Use the value false for the parameter isId to undeclare an attribute for being a user-determined ID attribute.

To specify an attribute by local name and namespace URI, use the setIdAttributeNS method.



---

# setIdAttributeNode_method

If the parameter isId is true , this method declares the specified attribute to be a user-determined ID attribute. This affects the value of Attr.isId and the behavior of Document.getElementById , but does not change any schema that may be in use, in particular this does not affect the Attr.schemaTypeInfo of the specified Attr node. Use the value false for the parameter isId to undeclare an attribute for being a user-determined ID attribute.



---

# setIdAttributeNS_method

If the parameter isId is true , this method declares the specified attribute to be a user-determined ID attribute. This affects the value of Attr.isId and the behavior of Document.getElementById , but does not change any schema that may be in use, in particular this does not affect the Attr.schemaTypeInfo of the specified Attr node. Use the value false for the parameter isId to undeclare an attribute for being a user-determined ID attribute.



---

# tagName_attribute

The name of the element. For example, in:

```
<elementExample id="demo">
...
</elementExample> ,
```

tagName has the value "elementExample" . Note that this is case-preserving in XML, as are all of the operations of the DOM. The HTML DOM returns the tagName of an HTML element in the canonical uppercase form, regardless of the case in the source HTML document.