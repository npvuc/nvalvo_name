

---

# canAppendChild_method

Determines whether the Node.appendChild operation would make this document not compliant with the VAL_INCOMPLETE validity type.



---

# canInsertBefore_method

Determines whether the Node.insertBefore operation would make this document not compliant with the VAL_INCOMPLETE validity type.



---

# canRemoveChild_method

Determines whether the Node.removeChild operation would make this document not compliant with the VAL_INCOMPLETE validity type.



---

# canReplaceChild_method

Determines whether the Node.replaceChild operation would make this document not compliant with the VAL_INCOMPLETE validity type.



---

# defaultValue_attribute

The default value specified in an attribute or an element declaration or null if unspecified. If the schema is a W3C XML schema, this is the canonical lexical representation of the default value.



---

# enumeratedValues_attribute

A DOMStringList , as described in [ DOM Level 3 Core ], of distinct values for an attribute or an element declaration or null if unspecified. If the schema is a W3C XML schema, this is a list of strings which are lexical representations corresponding to the values in the [value] property of the enumeration component for the type of the attribute or element. It is recommended that the canonical lexical representations of the values be used.



---

# nodeValidity_method

Determines if the node is valid relative to the validation type specified in valType . This operation doesn't normalize before checking if it is valid. To do so, one would need to explicitly call a normalize method. The difference between this method and the DocumentEditVAL.validateDocument method is that the latter method only checks to determine whether the entire document is valid.



---

# validationState_enumeration

An integer indicating the validation state, or whether the operation can or cannot be done.

The validationState enumeration has the following constants of type unsigned short .



---

# validationType_enumeration

An integer indicating the validation type. Other specifications can define stricter validation types/constants by extending the NodeEditVAL interface.

The validationType enumeration has the following constants of type unsigned short .