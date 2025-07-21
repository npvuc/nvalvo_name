

---

# Deleting_Sections_of_a_Document_Using_a_Range

This example illustrates several basic techniques:

- • Opening a document using the optional flags parameter ( Application.openDocument ).

- • Gathering elements by attribute name and value ( getElementsByAttribute ).

- • Prompting for user input ( Application.confirm ).

- • Using a range to mark content for deletion and delete it (the deleteTag function).

- • Handling a NodeList .

The result of the code in this example is that the user is prompted with the option to delete all the tags in a document that have a certain profiling attribute.

The deleteTag function in the example demonstrates the creation, marking, and use of a Range object. First the Range must be created ( Document.createRange ). The beginning and end points must then be set ( Range.setStartBefore and Range.setEndAfter ). The content in the Range is then deleted, and the range is detached.

The call to Range.detach() is critical, as this method frees all resources associated with this Range object. Any subsequent call on that object would result in an exception being thrown. This method should be called whenever a use of a Range object is complete.

```
//Delete the given node (tag and its children and/or contents)
function deleteTag(tag) {
var range = doc.createRange();
range.setStartBefore(tag);
range.setEndAfter(tag);
range.deleteContents();
range.detach();
}
//Open the document for writing, while suppressing any parse errors
//OPEN_DOCRDWR(0x0002) - open the document for reading and writing
//OPEN_NMSGS(0x0020) - suppress any parser error messages
var doc = Application.openDocument("sample.xml", (0x0002 | 0x0020));
//Select all tags with the profiling attribute "security" and the value "Employee"
var profiles = doc.getElementsByAttribute("security", "Employee", 1);
//Prompt the user to delete the selected tags
var response = Application.confirm("Found " + profiles.length +
" profiled items.\nOK to delete?", "Confirm Deletion");
//If the user clicked "OK", go ahead and delete them
if(response) {
while(0 < profiles.length) {
deleteTag(profiles.item(0));
}
}
```

Notice in this example that in the loop that calls deleteTag , it is item(0) that is deleted each time. This is because in the W3C DOM NodeList specification, NodeList s are live. That is, changes in the underlying document object are immediately reflected in the NodeList .

For example, if tags had been deleted using the following code, only every other node would have been deleted.

```
for(i = 0; i < profiles.length; i++) {
deleteTag(profiles.item(i));
}
```