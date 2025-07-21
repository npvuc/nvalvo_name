

---

# Error_Handling

Functions that return toid or tmid values will return h::tblNullToid or h::tblNullTmid to indicate failure.

Functions that return [ 0 | 1 ] will return 0 to indicate error.

List functions return 0 to indicate that no data was returned in an array.



---

# Galley_Ordering

Some routines navigate around a table or grid using “galley” order. Galley order is row-major order with one difference: cells that are spanned and which are not the master cell are omitted entirely. The basic progression (start with upper-left cell, continue from left to right in each row, process rows from top to bottom, ending with the lower-right cell) is the same, we just skip cells whose content is uninteresting because they're neither unspanned nor the master cell of a multicell.



---

# List_Functions

Functions whose names end with “list” take as one parameter an array variable. On return they place some number of data elements in the array and return the number of array elements as their result. The list will be numerically indexed. If the function is unable to return any information, it will return zero, indicating that there is nothing in the array.



---

# Row-Major_Ordering

Functions that return a list of cells or rules usually do so in row-major order. Row major order means starting with the upper-left cell in a grid (or in a region within a grid) and proceeding horizontally from left to right. At the end of the row, we move to the left most cell of the row below, and again continue from left to right. The last cell processed is the lower-right cell of the grid or region.



---

# Table_Directions

Functions that take or return directions may use these predefined values:

- • h::tblDirUndef

- • h::tblDirLeft

- • h::tblDirRight

- • h::tblDirAbove

- • h::tblDirBelow



---

# Table_Object_and_Table_Model_IDs

Functions that take or return table object identifier ( toid ) or table model identifier ( tmid ) parameters or values may use these predefined constants to test for null or invalid values:

- • h::tblNullToid

- • h::tblNullTmid



---

# Table_Object_Types

Functions that take or return objectType parameters or results may use these predefined values:

- • h::tblTypeUndef

- • h::tblTypeSet

- • h::tblTypeGrid

- • h::tblTypeRow

- • h::tblTypeColumn

- • h::tblTypeCell

- • h::tblTypeRule

- • h::tblTypeStore

- • h::tblTypeSelector



---

# Table_Orientation

Functions that take or return orientations may use these predefined values:

- • h::tblVertical

- • h::tblHorizontal