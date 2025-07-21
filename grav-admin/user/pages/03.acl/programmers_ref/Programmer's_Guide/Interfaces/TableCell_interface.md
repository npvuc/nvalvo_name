

---

# cellAbove_attribute

The cell above this cell.



---

# cellBelow_attribute

The cell below this cell.



---

# cellLeft_attribute

The cell to the left of this cell.



---

# cellRight_attribute

The cell to the right of this cell.



---

# column_attribute

The column that the cell is part of.



---

# contents_attribute

The contents of the cell. The Range returned contains the cell's contents. If the cell has no contents, a collapsed Range is returned. The contents of the cell can be changed by changing the contents of the Range .



---

# deleteFontPI_method

Deletes the font PI from the table cell if it has one. Otherwise does nothing.



---

# findFontPI_method

Returns an Element node for the font PI in the cell, creating it if asked to.



---

# inSameColumn_method

Returns true if this cell is in the same column in the same grid as the indicated cell.



---

# inSameRow_method

Returns true if this cell is in the same row in the same grid as the indicated cell.



---

# instantiate_method

Marks the cell as being non-sparse. Some table models allow sparse markup, where some cells of a table are not explicitly described in markup. Arbortext Editor and Arbortext Editor add generated cell markup to the document when reading a sparse table so that there is markup underlying every table cell. When a document containing a table is saved, this generated markup is deleted, unless the cell has acquired content, attributes, or some other reason for existence. This function allows the user to require that the markup corresponding to a cell NOT be discarded, even if it is generated markup.



---

# isAdjacent_method

Returns true if the indicated cell is a neighbor.



---

# multicell_attribute

The TableMulticell that this cell is part of. Will be null if not part of a multicell.



---

# nextGalleyCell_method

Returns the next cell in galley order, wrapping around from the last to the first if requested.



---

# onBottomMulticellEdge_attribute

True if the cell is on the bottom edge of a multicell.



---

# onLeftMulticellEdge_attribute

True if the cell is on the left edge of a multicell.



---

# onRightMulticellEdge_attribute

True if the cell is on the right edge of a multicell.



---

# onTopMulticellEdge_attribute

True if the cell in on the top edge of a multicell.



---

# previousGalleyCell_method

Returns the previous cell in galley order, wrapping around from the first to the last if requested.



---

# rectangle_method

Returns a TableRectangle with this cell on one corner and the cell given as the parameter on the other corner. Either cell may be the upper left cell. Both must be in the same grid.



---

# row_attribute

The row that the cell is part of.



---

# ruleAbove_attribute

The TableRule on the top edge of the cell.



---

# ruleBelow_attribute

The TableRule on the bottom edge of the cell.



---

# ruleLeft_attribute

The TableRule on the left edge of the cell.



---

# ruleRight_attribute

The TableRule on the right edge of the cell.



---

# span_method

Creates a span of a rectangle of cells. This cell is on one corner and the cell given as a parameter is on the other corner.



---

# spanned_attribute

True if this cell is in a multicell and is not the spanning cell in the multicell



---

# spanning_attribute

True if this cell is the spanning cell in a multicell



---

# unspan_method

Unspans the cell, which must be in a multicell.