

---

# entities_attribute

A NamedNodeMap containing the general entities, both external and internal, declared in the DTD. Parameter entities are not contained. Duplicates are discarded. For example in:

```
<!DOCTYPE ex SYSTEM "ex.dtd" [
<!ENTITY foo "foo">
<!ENTITY bar "bar">
<!ENTITY bar "bar2">
<!ENTITY % baz "baz">
]>
<ex/>
```

the interface provides access to foo and the first declaration of bar but not the second declaration of bar or baz . Every node in this map also implements the Entity interface.

The DOM Level 2 does not support editing entities, therefore entities cannot be altered in any way.



---

# internalSubset_attribute

The internal subset as a string.



---

# name_attribute

The name of DTD; i.e., the name immediately following the DOCTYPE keyword.



---

# notations_attribute

A NamedNodeMap containing the notations declared in the DTD. Duplicates are discarded. Every node in this map also implements the Notation interface.

The DOM Level 2 does not support editing notations, therefore notations cannot be altered in any way.



---

# publicId_attribute

The public identifier of the external subset.



---

# systemId_attribute

The system identifier of the external subset.