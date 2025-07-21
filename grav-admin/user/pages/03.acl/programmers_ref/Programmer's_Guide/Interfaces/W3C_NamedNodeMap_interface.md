

---

# getNamedItem_method

Retrieves a node specified by name.



---

# getNamedItemNS_method

Retrieves a node specified by local name and namespace URI. HTML-only DOM implementations do not need to implement this method.



---

# item_method

Returns the index th item in the map. If index is greater than or equal to the number of nodes in this map, this returns null .



---

# length_attribute

The number of nodes in this map. The range of valid child node indices is 0 to length-1 inclusive.



---

# removeNamedItem_method

Removes a node specified by name. When this map contains the attributes attached to an element, if the removed attribute is known to have a default value, an attribute immediately appears containing the default value as well as the corresponding namespace URI, local name, and prefix when applicable.



---

# removeNamedItemNS_method

Removes a node specified by local name and namespace URI. A removed attribute may be known to have a default value when this map contains the attributes attached to an element, as returned by the attributes attribute of the Node interface. If so, an attribute immediately appears containing the default value as well as the corresponding namespace URI, local name, and prefix when applicable.

HTML-only DOM implementations do not need to implement this method.



---

# setNamedItem_method

Adds a node using its nodeName attribute. If a node with that name is already present in this map, it is replaced by the new one.

As the nodeName attribute is used to derive the name which the node must be stored under, multiple nodes of certain types (those that have a "special" string value) cannot be stored as the names would clash. This is seen as preferable to allowing nodes to be aliased.



---

# setNamedItemNS_method

Adds a node using its namespaceURI and localName . If a node with that namespace URI and that local name is already present in this map, it is replaced by the new one.

HTML-only DOM implementations do not need to implement this method.