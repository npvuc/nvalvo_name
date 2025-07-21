

---

# Inserting_an_Entity_Reference_Using_createEntityReference

To insert such characters as an entity references, use Document.createEntityReference rather than createTextNode . This example produces the same result as the previous example, but uses a character entity to insert the u-umlaut:

```
var doc = Application.activeDocument;
var paras = doc.getElementsByTagName("para");
var newText1 = doc.createTextNode("Austrians are known for their Gem");
var charEnt = doc.createEntityReference("uuml");
var newText2 = doc.createTextNode("tlichkeit");
paras.item(0).appendChild(newText1);
paras.item(0).appendChild(charEnt);
paras.item(0).appendChild(newText2);
```



---

# Inserting_Text_Containing_a_Non-Latin_Character

To insert a string containing characters such as letters from non-English alphabets, include the Unicode character in the text string. Do not include it as an entity reference.

For example, suppose you are authoring a travel guide and wish to append a paragraph that includes the German word Gemütlichkeit . If you include the ü as an entity reference, the entity will not be resolved. For example:

```
var newText1 = doc.createTextNode("Austrians are known for their Gem&uuml;tlichkeit");
```

The text node will literally contain “ Gem&uuml;tlichkeit ”. Instead, insert the character as in the following example:

```
var doc = Application.activeDocument;
var paras = doc.getElementsByTagName("para");
var newText = doc.createTextNode(" Austrians are known for their Gemütlichkeit");
paras.item(0).appendChild(newText);
```



---

# Inserting_Text_Using_createTextNode

This example appends the line “ Adding new text. ” to the end of the first paragraph in a document

```
var doc = Application.activeDocument;
var paras = doc.getElementsByTagName("para");
//create the new Text Node
var newText = doc.createTextNode(" Adding new text.");
//append it to first paragraph
paras.item(0).appendChild(newText);
```