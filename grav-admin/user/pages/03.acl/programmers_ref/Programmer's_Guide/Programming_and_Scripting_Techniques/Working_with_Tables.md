

---

# Example:_Identifying_a_Document_Type's_Table_Model_Support

This example uses the function tableModelInfo to print all the available information on the current document type's supported table model(s) to the Arbortext Editor message window.

To run this sample code:

```
//-----------------------------------------------------------------
// Function: tableModelInfo
// Description: Print all information about the current table models
// Parameters: NONE
//-----------------------------------------------------------------
function tableModelInfo()
{
var docType = Application.activeDocument.doctype;
var tblModels = docType.tableModels;
Application.alert("Table model information for the " +
docType + "doctype");
Application.alert("Number of table models = " + tblModels.length);
for (var i = 0; i < tblModels.length; i++) {
Application.print(" [" + i + "] = '" + tblModels.item(i) + "'");
Application.print(" Supports multiple grids = " +
docType.tableModelSupport(tblModels.item(i), "multiplegrids"));
Application.print(" Supports headers = " +
docType.tableModelSupport(tblModels.item(i), "HeaderRows"));
Application.print(" Supports footers = " +
docType.tableModelSupport(tblModels.item(i), "FooterRows"));
var wrappers = docType.tableModelWrappers(tblModels.item(i));
Application.print(" Number of wrapper tags = " + wrappers.length);
for (var j = 0; j < wrappers.length; j++) {
Application.print(" [" + j + "] = '" + wrappers.item(j) + "'");
}
var tags = docType.tableModelTags(tblModels.item(i));
Application.print(" Number of table model tags = " + tags.length);
for (j = 0; j < tags.length; j++) {
Application.print(" [" + j + "] = '" + tags.item(j) + "'");
}
}
}//end of tableModelInfo
```



---

# Example:_Inserting_a_Column_Based_on_the_Current_Selection

This example uses the function tbl_insert_column to insert a column to the left of the current selection. If the selection is invalid, that is, it is discontiguous or not a rectangle, a message is displayed in a dialog box and tbl_insert_column returns zero.

To run this sample code:

```
//-----------------------------------------------------------------
// Function: tbl_insert_column
//
// Description:
// Inserts one or more columns into a document
//
// Parameter:
// insertLeft: if true (nonzero), adds columns to the left of
// the target
//
// Returns:
// 0 if the insert failed, 1 if it succeeded
//
//-----------------------------------------------------------------
function tbl_insert_column(insertLeft)
{
if(insertLeft == undefined){insertLeft = 0;}
var doc = Application.activeDocument;
//Check to see that there's either a table selection, or that the
//cursor is in a table cell.
//To see of a cursor is in a cell:
//get the range that is the cell containing the cursor
//get the cell node
//get the cell containing the caret
if((doc.selectionType != doc.TABLE_SELECTION) &&
((cell = doc.insertionPoint.endContainer.enclosingCell) == null)){
Application.alert("No table object is selected");
return 0;
}
//get the table selection from the active document
var tilePlex = doc.tableSelection;
//if the selection is empty, i.e., just a cursor in a cell,
//add that cell to the tableTilePlex to create a 1x1 rectangle
if(tilePlex.empty){
tilePlex.addObject(cell);
}
//ensure table selection will accept inserted columns
if(!tilePlex.modifiable){
Application.alert("table cannot be modified");
return 0;
}
//ensure table selection is contiguous and does not cross
//grid boundaries
var validRectangle = tilePlex.pasteRectangle;
if(validRectangle == null){
Application.alert("The table selection is discontiguous or crosses grid boundaries");
return 0;
}
//At this point, the selection is valid and can be modified, add the
//columns to the grid.
//A new column is added for each one that the user has selected.
var newGrid = validRectangle.lowerLeft.grid;
for(i = 0; i < validRectangle.width; i++){
try{
if(insertLeft){
newGrid.addColumn(validRectangle.lowerLeft.column);
}
else{
newGrid.addColumn(validRectangle.upperRight.column.columnRight);
}
}
catch(e){Application.alert("Column insertion failed because " + e.code);}
}
//success
return 1;
}//end of tbl_insert_column
```

To implement the previous example using JScript, change the line:

```
if((doc.selectionType != doc.TABLE_SELECTION) &&
```

to be:

```
if((doc.selectionType != 2) &&
```



---

# Example:_Inserting_and_Modifying_a_Table

This example uses the function addTable to perform the following actions:

- • Insert a six-row five-column table into the first paragraph of a Arbortext XML Docbook template.

- • Span cells 1-2 and 3-5 of the first row and add text to the spanned cells.

- • Convert the first row to a header row.

- • Turn off rules for the entire table.

The function appendText is a utility function for adding text to a cell.

To run this sample code:

```
//-----------------------------------------------------------------
// Function: appendText
//
// Description: A utility function called by addTable.
// Adds text to a cell
//
// Parameters: cell: the target for the added text
// text: the text to be added
//
//-----------------------------------------------------------------
function appendText(cell, text)
{
var cellRange = cell.contents;
cellRange.collapse( false );
var textNode = cell.document.createTextNode(text);
cellRange.insertNode(textNode);
}
//-----------------------------------------------------------------
// Function: addTable
//
// Description: Add a table to the first para in a document
//
// Parameters: NONE
//
//-----------------------------------------------------------------
function addTable(){
var doc = Application.activeDocument;
var para = doc.getElementsByTagName("para").item(0);
try{
var set = para.insertTable("OASIS Exchange", "table", 5, 6, null);
}
catch(e){Application.alert("Exception " + e.code() +
" caught in insertTable");
return 0;}
var grid = set.grids.item(0);
var firstRow = grid.row(1);
// Span cells 1-2 and 3-5
firstRow.cell(1).span(firstRow.cell(2));
firstRow.cell(3).span(firstRow.cell(5));
appendText(firstRow.cell(1), "Cells 1 and 2");
appendText(firstRow.cell(3), "Cells 3-5");
// Change first row to a header row
firstRow.setAttribute("header_level",1);
//turn off the table rules
var rules = grid.rules;
for (i = 0; i < rules.length; i++) {
rules.item(i).setAttribute("style", "blank");
}
}//end of addTable
```