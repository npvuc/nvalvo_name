

---

# allowedAttributes_attribute

A NameList , as described in [ DOM Level 3 Core ], of all possible attribute information items or wildcards that can appear as attributes of this element, or null if this element has no context or schema. Duplicate pairs of {namespaceURI, name} are eliminated.



---

# allowedChildren_attribute

A NameList , as described in [ DOM Level 3 Core ], of all possible element information items or wildcards that can appear as children of this element, or null if this element has no context or schema. Duplicate pairs of {namespaceURI, name} are eliminated.



---

# allowedFirstChildren_attribute

A NameList , as described in [ DOM Level 3 Core ], of all possible element information items or wildcards that can appear as a first child of this element, or null if this element has no context or schema. Duplicate pairs of {namespaceURI, name} are eliminated.



---

# allowedNextSiblings_attribute

A NameList , as described in [ DOM Level 3 Core ], of all element information items or wildcards that can be inserted as a next sibling of this element, or null if this element has no context or schema. Duplicate pairs of {namespaceURI, name} are eliminated.



---

# allowedParents_attribute

A NameList , as described in [ DOM Level 3 Core ], of all possible element information items that can appear as a parent this element, or null if this element has no context or schema.



---

# allowedPreviousSiblings_attribute

A NameList , as described in [ DOM Level 3 Core ], of all element information items or wildcards that can be inserted as a previous sibling of this element, or null if this element has no context or schema.



---

# canRemoveAttribute_method

Verifies if an attribute by the given name can be removed.



---

# canRemoveAttributeNode_method

Determines if an attribute node can be removed.



---

# canRemoveAttributeNS_method

Verifies if an attribute by the given local name and namespace can be removed.



---

# canSetAttribute_method

Determines if the value for specified attribute can be set.



---

# canSetAttributeNode_method

Determines if an attribute node can be added.



---

# canSetAttributeNS_method

Determines if the attribute with given namespace and qualified name can be created if not already present in the attribute list of the element. If the attribute with the same qualified name and namespaceURI is already present in the element's attribute list, it tests whether the value of the attribute and its prefix can be set to the new value.



---

# canSetTextContent_method

Determines if the text content of this node and its descendants can be set to the string passed in.



---

# contentType_attribute

The content type of an element as defined above.



---

# ContentTypeVAL_enumeration

An integer indicating the content type of an element.

The ContentTypeVAL enumeration has the following constants of type unsigned short .



---

# isElementDefined_method

Determines if name is defined in the schema. This only applies to global declarations. This method is for non-namespace aware schemas.



---

# isElementDefinedNS_method

Determines if name in this namespace is defined in the current context. Thus not only does this apply to global declarations. but depending on the content, this may also apply to local definitions. This method is for namespace aware schemas.



---

# requiredAttributes_attribute

A NameList , as described in [ DOM Level 3 Core ], of required attribute information items that must appear on this element, or null if this element has no context or schema.