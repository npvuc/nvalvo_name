

---

# cell_method

Returns a TableCell representing the cell at the given position in the row or a null pointer if that cell does not exist. The first cell is cell 1.



---

# cellCount_attribute

The number of cells in the row.



---

# cells_attribute

A TableObjectStore containing all the cells in the row.



---

# first_attribute

True if this row is the first row in the TableSet . A row that is first in the TableSet will also be first in its TableGrid . (However, a row that is first in its TableGrid will not necessarily also be first in the TableSet .)



---

# index_attribute

The row number of this row in its grid. The top row in the grid is row 1.



---

# last_attribute

True if this row is the last row in the TableSet . A row that is last in the TableSet will also be last in its TableGrid . (However, a row that is last in its TableGrid will not necessarily also be last in the TableSet .)



---

# leftCell_attribute

The left-most cell in the row.



---

# rightCell_attribute

The right-most cell in the row.



---

# rowAbove_attribute

A TableRow representing the row above this one. If this is the top row, it is a null pointer.



---

# rowBelow_attribute

A TableRow representing the row below this one. If this is the bottom row, it is a null pointer.



---

# ruleLeft_attribute

A TableRule for the rule at the left end of the row.



---

# ruleRight_attribute

A TableRule for the rule at the right end of the row.



---

# rulesAbove_attribute

A TableObjectStore containing a TableRule for each rule on the top edge of this row.



---

# rulesBelow_attribute

A TableObjectStore containing a TableRule for each rule on the bottom edge of this row.



---

# suppressed_attribute

True if the entire row is suppressed because all of its cells are spanned and none of them is a spanning cell.