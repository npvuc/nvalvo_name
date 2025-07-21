

---

# Copying_and_Pasting_between_Documents

Content can also be moved between documents using Document.importNode . The code in this example results in a copy and paste without the need to clone the region from the first document. This is because Document.importNode does not alter or remove content from the original document; it creates a new copy of the source node — in effect, cloning it. This example also demonstrates the use of ADocument.openDocument , the use of optional flags and path parameters on ADocument.save , and ADocument.close .

```
var doc1 = Application.openDocument("sample1.xml");
var doc2 = Application.openDocument("sample2.xml");
//Get the first chapter from sample1.xml and sample2.xml
var sample1Chapter = doc1.getElementsByTagName("chapter").item(0);
var sample2Chapter = doc2.getElementsByTagName("chapter").item(0);
var book = doc2.getElementsByTagName("book").item(0);
//Import the chapter from sample1.xml into sample2.xml
var newChapter = doc2.importNode(sample1Chapter,true);
//insert the chapter
book.insertBefore(newChapter,sample2Chapter);
//SAVE_NAC_ENTREF(0x0400) - write non-ascii characters as
// character entity references
doc2.save(0x0400, "newSample2.xml");
doc1.close();
doc2.close();
```

To execute a cut and paste between documents, select and delete the contents in the original document after inserting it in the target document.



---

# Copying_and_Pasting_within_a_Document

A copy and paste within a document can be done by cloning the contents of chapter one before inserting them before chapter three. In this example, the result will be two copies of chapter one in the document; one before and one after chapter two.

```
var doc = Application.openDocument("sample1.xml");
var chapters=doc.getElementsByTagName("chapter");
var chapter1 = chapters.item(0);
var chapter3 = chapters.item(2);
var book = doc.getElementsByTagName("book").item(0);
var range = doc.createRange();
range.setStartBefore(chapter1);
range.setEndAfter(chapter1);
var clone = range.cloneContents();
book.insertBefore(clone,chapter3);
range.detach();
```



---

# Cutting_and_Pasting_within_a_Document

This example swaps the position of the first two chapters in a document. When chapter one is inserted before chapter three, it is the same as a cut and paste; it is not a copy of the node, but the node itself that is being moved.

```
var doc = Application.openDocument("sample1.xml");
//Get the nodes contining chapters one and three from the document
//Chapter three will be the node to insert before
var chapters=doc.getElementsByTagName("chapter");
var chapter1 = chapters.item(0);
var chapter3 = chapters.item(2);
var book = doc.getElementsByTagName("book").item(0);
//chapter1 is the new node, and chapter3 is the reference
book.insertBefore(chapter1,chapter3);
```



---

# Inserting_Markup_at_the_Caret

The ARange extension includes the method insertParsedString . This method makes it easy to insert strings containing markup (tags and entity references) into a range, including the one that represents the document caret position. The following two examples are equivalent and insert the string “an emphasized word” with the second word “ emphasized ” enclosed in <emphasis> tags. The first example is implemented using standard DOM methods:

```
var doc = Application.activeDocument;
var caret = doc.insertionPoint;
var node = caret.endContainer;
var parent = node.parentNode;
// does not consider caret offset into text node
parent.insertBefore(doc.createTextNode("an "), node);
var emph = doc.createElement("emphasis");
emph.appendChild(doc.createTextNode("emphasized"));
parent.insertBefore(emph, node);
parent.insertBefore(doc.createTextNode(" word"), node);
```

The following example uses the ARange.insertParsedString method:

```
var doc = Application.activeDocument;
doc.insertionPoint.insertParsedString("an <emphasis>emphasized</> word");
```



---

# Inserting_Text_at_the_Caret

This example shows how to insert text in the document where the caret is located using the Range returned by the ADocument.insertionPoint attribute. If the caret is within a text node, the text is inserted into that node. Otherwise, a new text node is inserted before the insertionPoint node.

```
var doc = Application.activeDocument;
var caret = doc.insertionPoint;
var node = caret.endContainer;
if (node.nodeType == node.TEXT_NODE)
node.insertData(caret.endOffset, " new text ");
else
caret.insertNode(doc.createTextNode(" new text "));
```