

---

# attrChange_attribute

attrChange indicates the type of change which triggered the DOMAttrModified event. The values can be MODIFICATION , ADDITION , or REMOVAL .



---

# AttrChangeType_enumeration

An integer indicating in which way the Attr was changed.

The AttrChangeType enumeration has the following constants of type unsigned short .



---

# attrName_attribute

attrName indicates the name of the changed Attr node in a DOMAttrModified event.



---

# initMutationEvent_method

The initMutationEvent method is used to initialize the value of a MutationEvent created through the DocumentEvent interface. This method may only be called before the MutationEvent has been dispatched via the dispatchEvent method, though it may be called multiple times during that phase if necessary. If called multiple times, the final invocation takes precedence.



---

# newValue_attribute

newValue indicates the new value of the Attr node in DOMAttrModified events, and of the CharacterData node in DOMCharDataModified events.



---

# prevValue_attribute

prevValue indicates the previous value of the Attr node in DOMAttrModified events, and of the CharacterData node in DOMCharDataModified events.



---

# relatedNode_attribute

relatedNode is used to identify a secondary node related to a mutation event. For example, if a mutation event is dispatched to a node indicating that its parent has changed, the relatedNode is the changed parent. If an event is instead dispatched to a subtree indicating a node was changed within it, the relatedNode is the changed node. In the case of the DOMAttrModified event it indicates the Attr node which was modified, added, or removed.