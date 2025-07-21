

---

# addColumn_method

Add an empty column to the grid.



---

# addRow_method

Add an empty row to the grid.



---

# cell_method

Returns the cell at the specified coordinates. The upper left cell is (1,1).



---

# cells_attribute

A TableObjectStore containing all the cells in the grid. This is a static store; if cells are added to or removed from the grid (by adding or deleting rows or columns) it is not updated.



---

# column_method

Returns the column given its index. The first column is column 1.



---

# columnCount_attribute

The number of columns in the grid



---

# columns_attribute

A TableObjectStore containing all the columns in the grid. This is a static store; if columns are added or removed it is not updated.



---

# deleteColumn_method

Delete a column from the grid.



---

# deleteRow_method

Delete a row from the grid.



---

# firstGalleyCell_attribute

The first cell in the grid in galley order.



---

# gridAbove_attribute

The grid above this one in the table set, if any.



---

# gridBelow_attribute

The grid below this one in the table set, if any.



---

# hlineRuleList_method

Returns a table object store containing all the TableRule s in a specified horizontal line.



---

# index_attribute

The index of this table in the TableSet it is part of.



---

# insertColumns_method

Insert one or more columns into the grid.



---

# insertRows_method

Insert one or more rows into the grid.



---

# lastGalleyCell_attribute

The last cell in the grid in galley order.



---

# row_method

Returns a row given its index. The first row is row 1.



---

# rowCount_attribute

The number of rows in the grid



---

# rows_attribute

A TableObjectStore containing all the rows in the grid. This is a static store; if rows are added or removed it is not updated.



---

# rule_method

Returns the rule at a specified location in the grid. Rules are addressed using cell coordinates (with (1,1) being the upper left cell). For cell (m,n), (m,n) is actually the cell's upper left corner.



---

# rules_attribute

A TableObjectStore containing all the rules in the grid sorted in row major order.



---

# split_method

Splits the grid at the row indicated. That row will be the top row in a new grid inserted after this one.



---

# vlineRuleList_method

Returns a table object store containing all the TableRule s in a specified vertical line.