

---

# Traversing_and_Printing_a_Document_Structure

In this example, as the document is traversed, the tag name and up to the first 60 characters of each node are printed to illustrate the hierarchical structure of the current document.

In addition to demonstrating how to walk a DOM tree, this example also shows how to access the names of nodes ( Node.nodeName ), how to determine a node's type ( Node.nodeType = text, element, comment, or processing instruction), and how to extract text content from a document ( Node.data ).

```
function printTree(n, elem) {
if (elem == null) {
if (n == 0)
print("document has no element nodes");
return;
}
var str = "";
for (var i = 0; i < n; i++)
str += " ";
// show this node
print(str + elem.tagName + getAttrs(elem));
str += " ";
// followed by its children
for (var child = elem.firstChild; child != null;
child = child.nextSibling) {
if (child.nodeType == child.ELEMENT_NODE)
printTree(n + 1, child);
else if (child.nodeType == child.TEXT_NODE) {
// for text nodes, show the first 60 characters
// note, concatentation with a null string is used to convert
// the Java String returned into a JavaScript string.
var text = child.data + "";
if (text.length > 60)
print(str + '"' + text.substr(0, 60) + "...\"");
else
print(str + '"' + text + '"');
}
else if (child.nodeType == child.COMMENT_NODE) {
var text = "#comment: " + child.data;
if (text.length > 60)
text = text.substr(0, 60) + "...";
print(str + text);
}
else if (child.nodeType == child.PROCESSING_INSTRUCTION_NODE)
print(str + "#pi: " + child.target + ' ' + child.data);
else // all others
print(str + child.nodeName);
}
}
// start at the root
printTree(0, Application.activeDocument.documentElement);
```



---

# Using_getElementsByAttribute

The previous example could be improved by using the AElement.getElementsByAttribute method. (The AOM AElement interface extends the W3C DOM Element interface.) Doing so will return only those tags from the document that have the role attribute set to bold . The value on all of the tags can then be changed from bold to italic without having to test every <emphasis> tag in the document.

The getElementsByAttribute method takes three arguments: name , value , and selector . If selector is set to 1 (one), the search will return all nodes that match both name and value . If selector is set to 0 (zero), all nodes matching name , regardless of their value, are returned.

```
var doc = Application.activeDocument;
var tags = doc.getElementsByAttribute("role", "bold", 1);
for (i=0; i < tags.length; i++) {
tags.item(i).setAttribute("role", "italic");
}
```



---

# Using_getElementsByTagName

In this example, the tree is traversed by calling getElementsByTagName . All of the Document , ADocument , Element , and AElement interface getElementsBy Xxx methods populate a NodeList with nodes in the order encountered in a preorder traversal of the tree. All occurrences of the <emphasis> tag have their role attribute value changed from bold to italic , changing all bold text to italic. This is done by iterating over the NodeList returned by getElementsByTagName , and using Node.getAttribute to check the value of each node's role attribute, and then using Node.setAttribute to change that value to italic .

```
var doc = Application.activeDocument;
//get all emphasis tags in the document
var tags = doc.getElementsByTagName("emphasis");
for(i=0; i < tags.length; i++) {
if(tags.item(i).getAttribute("role") == "bold") {
tags.item(i).setAttribute("role", "italic")
}
}
```