

---

# addObject_method

Adds a table object to the tileplex.



---

# addRectangle_method

Adds a rectangle to the tileplex. It will be consolidated with an existing rectangle if possible.



---

# clear_method

Clears the tileplex by removing all rectangles and rules that the tileplex contains.



---

# clonePlex_method

Makes a copy of the specified tileplex. The tileplex and all of the rectangles it contains are duplicated, but the underlying table objects are not duplicated.



---

# deleteFromDocument_method

Deletes the contents of this tileplex from the document if possible.



---

# empty_attribute

True if the tileplex is empty.



---

# getObjects_method

Returns a table object store containing the contents of the tileplex interpreted according to the parameters. A given tileplex can often be interpreted in many ways. For example, as a set of grids, a set of rows, a set of columns, or a set of cells. The parameters to getObjects control which interpretation is desired. If it is not possible to interpret the tileplex this way, no table object store is returned. If several want xxx parameters are true, the largest possible unit (sets, grids, rows or columns, or cells) will be returned. If wantRules is true , rules will be returned if the tileplex contains any, regardless of what else is returned. If wantRules is false and the tileplex contains rules, nothing will be returned.



---

# isSelected_method

Returns true if the tileplex selects the specified table object (that is, if one of the rectangles in the tileplex contains the entire rectangle defined by the table object).



---

# pasteRectangle_attribute

If the tileplex consists of a single rectangle and no rules, this rectangle is returned. Otherwise, a null pointer is returned. A tileplex that contains only a single rectangle is suitable for pasting somewhere using the TableRectangle.copyRectangle method.



---

# pasteType_method

Content that would be replaced if the tileplex were pasted to the specified location.



---

# rectangle_method

Returns the rectangle from the tileplex corresponding to the index given. The rectangles are indexed in no particular order.



---

# valid_attribute

True if the tileplex is valid. It is valid if all the rectangles in the tileplex are valid.