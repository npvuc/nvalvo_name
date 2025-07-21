

---

# appendData_method

Append the string to the end of the character data of the node. Upon success, data provides access to the concatenation of data and the DOMString specified.



---

# data_attribute

The character data of the node that implements this interface. The DOM implementation may not put arbitrary limits on the amount of data that may be stored in a CharacterData node. However, implementation limits may mean that the entirety of a node's data may not fit into a single DOMString . In such cases, the user may call substringData to retrieve the data in appropriately sized pieces.



---

# deleteData_method

Remove a range of 16-bit units from the node. Upon success, data and length reflect the change.



---

# insertData_method

Insert a string at the specified 16-bit unit offset.



---

# length_attribute

The number of 16-bit units that are available through data and the substringData method below. This may have the value zero, i.e., CharacterData nodes may be empty.



---

# replaceData_method

Replace the characters starting at the specified 16-bit unit offset with the specified string.



---

# substringData_method

Extracts a range of data from the node.