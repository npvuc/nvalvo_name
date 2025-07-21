

---

# aclId_attribute

An integer constant uniquely identifying the document. This is the value that would be returned by the ACL function current_doc if the document were current.



---

# ATISelectionType_enumeration

The selectionType attribute describes the type of selection in the Document and has one of the following values.

The ATISelectionType enumeration has the following constants of type short .



---

# canRenameNode_method

Tests whether an existing node of type ELEMENT_NODE or ATTRIBUTE_NODE can be renamed such that the resulting node is compliant with VAL_SCHEMA validity type.



---

# cloneDocument_method

Creates a completely independent copy of this document. The cloned document will have no Document.documentURI or ADocument.name attributes set for it. However, the ADocument.directory attribute will be identical to the source document so that relatively-referenced resources (such as graphic files) will be correctly resolved in the context of the cloned document.



---

# CloneFlags_enumeration

The following bit constants are used with the flags argument of the cloneDocument() method.

The CloneFlags enumeration has the following constants of type int .



---

# close_method

Closes the document, freeing all associated memory and system resources (for example, file handles). This method actually decrements the reference count for the document and does not free resources until the reference count becomes zero. The reference count is incremented when the document is associated with a View object.



---

# CMSObjects_attribute

Returns an collection of all the objects in this document. The objects in this collection may be in any order but each will be present exactly once. Note that if a document contains a given child object in two locations then the returned collection will contain two objects; one for each reference. Each object will reference the same repository object but, for example, will have different start and end values associated with them.



---

# directory_attribute

The directory associated with the document. For documents read from the file system, this is the directory part of the documentURI attribute, excluding the name, and expressed as a file system path not as a URI. If the document has no directory, for example, a new document created from a template and not yet saved, this is the null string. A document created by calling cloneNode on another Document node inherits this attribute.

This attribute is read-only. However, changing the documentURI attribute will also change the value of the directory attribute.



---

# editBegin_method

The editBegin and editEnd methods provide a mechanism to bracket a series of document changes which may optionally be rolled back. Before beginning a series of changes, call editBegin for this document. At the end of the changes, call editEnd to either commit the changes or to roll them back by specifying false as the commit parameter.

Multiple calls may be made to editBegin before an editEnd call, for example if one top-level script calls another as part of its implementation. In this case, the changes are not committed or rolled back until the outermost editEnd call is made. All changes since the first editBegin call will be rolled back if any nested call to editEnd or the outermost editEnd call specifies false as the commit parameter.

For example, in JavaScript:

```
doc.undoBoundary("Big Changes");
doc.editBegin();
var commit = true;
try {
doBigChanges();
} catch (e) {
commit = false;
}
doc.editEnd(commit);
```

This example assumes doBigChanges or a method it calls throws an exception if it detects an error condition after making some document changes which should then be discarded.



---

# editEnd_method

This method commits or rolls back the changes made to the document since the matching editBegin call. The commit or roll back does not actually happen until the outermost editEnd call is made. Refer to the description of editBegin for details.



---

# generateEntityName_method

Generates an entity name suitable for use with this document. If no logicalId is given (or if it doesn't map to an active session), a random number is used to create an entity name which is currently not in use by this document. Otherwise the associated CMS adapter session will be called to produce the entity name. The adapter guarantees that the returned entity name will be unique as per the given logicalId. Thus, if given the same logicalId twice, this may return the same entity name twice. However, if given different logicalId's, this will return different entity names.



---

# getElementsByAttribute_method

Returns a NodeList of all descendant Elements that match the given attribute name and attribute value, in the order in which they are encountered in a pre-order traversal of this Document tree.



---

# getElementsByAttributeNS_method

Returns a NodeList of all descendant Elements that match the given attribute namespace URI, local name, and attribute value, in the order in which they are encountered in a pre-order traversal of this Document tree.



---

# getOption_method

This method returns the value of the Arbortext set option, scoped to this document.



---

# insertionPoint_attribute

A collapsed DOM Range indicating the current location of the cursor.



---

# markupType_attribute

An integer constant indicating the type of markup used by the document. One of the following values: XML_MARKUP , SGML_MARKUP , HTML_MARKUP , or NO_MARKUP .



---

# MarkupType_enumeration

The MarkupType enumerated type defines the values for the markupType attribute and has the following constants:

The MarkupType enumeration has the following constants of type int .



---

# modified_attribute

A boolean indicating whether the document has been modified. This attribute is reset when the document in saved.



---

# modifyReferences_method

This method will replace references within the given ADocument . The references to be replaced are those listed as keys in the given PropertyMap , and will be replaced by the value of each associated PropertyMap key. If the given ADocument contains any inclusions (such as file entities or XIncludes), unlike IOHost::modifyReferences , this method will descend into those inclusions in order to update any references that might be found in their content if the reference is found as a key in the given PropertyMap .

What is considered an “inclusion”, as far as this method is concerned, is limited to file entities and XIncludes. Any elements or attributes of elements which are encountered that match a customref burst configuration file rule (as found in the burst configuration file associated with the doctype of the Document or CMSObject to which the scrutinized node belongs) is not considered an “inclusion” by this method since customref is a referencing mechanism and not intended for inline inclusions. Any matching customref references will be replaced by this method, but since customref is not considered an “inclusion ” mechanism, this method will not open the file or logical id the customref references in order to descend into its contents.

All keys in the PropertyMap that reference the file system will be made a canonicalized universal name before any lookups occur. Also, each reference that is to be looked up in the PropertyMap that is a filesystem reference will also be temporarily made into a canonicalized universal name before the lookup occurs. By making all filesystem references canonicalized universal names, the caller will be assured that multiple references that use different conventions but still reference the same filesystem location are actually recognized as the same reference. No such manipulation will be made to CMS logical ID references.

If the MODIFYREF_NO_CUSTOMREF flag is not included in the flags parameter, any elements or attributes of elements that are encountered that match a customref burst configuration file rule (as found in the burst configuration file associated with the doctype of the Document or CMSObject to which the scrutinized node belongs) will be recognized as a reference and as such will be modified as long as that reference is listed as a key in the given PropertyMap . If the mode of the customref rule is “dita-full”, then the reference will be replaced with the value of the relevant PropertyMap key, appended with any DITA fragment identifier (including the leading “#”) copied from the original reference. All customref rules whose mode is “dita-partial” are always ignored and never replaced by this method, even if the reference of the “dita-partial” customref is found as a key in the given PropertyMap .

Documents and CMSObjects have a notion of whether or not they contain unsaved modifications. The modified state of the Document or CMSObject to which the given DocumentFragment belongs will be preserved by this method.



---

# ModifyRefFlags_enumeration

The ModifyRefFlags enumerated type is used to construct the flags parameter to the modifyReferences method by ORing any of the following options.

The ModifyRefFlags enumeration has the following constants of type int .



---

# name_attribute

The name of the document or a null string if the document was created without a name. For documents read from the file system, the name is the base name of the documentURI , including the extension, if any.



---

# optionNames_attribute

A StringList containing the names of all document-scope Arbortext set options.



---

# properties_attribute

A PropertyMap object containing user-defined properties for the document. The properties are stored at the beginning of the XML file as processing instructions.



---

# redo_method

The redo method reverses the change made by the last undo. A series of consecutive undos may be reversed by the corresponding number of redos. Redo operations do not get added to the undo history.



---

# save_method

Saves this document.



---

# SaveFlags_enumeration

The SaveFlags enumerated type is used to construct the flags parameter to the save method, by ORing options from the following list:

The SaveFlags enumeration has the following constants of type int .



---

# selectionType_attribute

An integer constant indicating whether there is no selection ( NO_SELECTION ), a text selection ( TEXT_SELECTION ), or a table selection ( TABLE_SELECTION ).



---

# setOption_method

This method sets the value of the Arbortext set option, scoped to this document.



---

# tables_attribute

A TableObjectStore containing all of the TableSet s in the document. If there are no tables in the document, an empty store is returned.



---

# tableSelection_attribute

A TableTilePlex representing the current table selection. If there is no table selection, the value of tableSelection is an empty TableTilePlex .



---

# textSelection_attribute

A DOM Range indicating the current text selection. If there is no text selection, the value will be the same as insertionPoint .

If the text selection is set to a collapsed range, the selection is cleared. The insertion point is not changed.



---

# undo_method

This method reverses the previous change to the document. If called repeatedly, reverses earlier changes.



---

# undoBoundary_method

This method inserts a boundary in the undo history so that a subsequent undo will restore changes up to the current state. Normally, the editor inserts a boundary automatically before changes are made by a menu item, toolbar selection, or keyboard shortcut. When implementing a custom application dialog, it may be necessary to call the undoBoundary method before making document changes using the AOM, especially if the dialog is modeless and allows multiple changes to be made which should be undone individually.

The undoBoundary method enables undo history on this document. Normally, a document not associated with a window will not have undo history enabled.

The optional description parameter may be specified to set the label for the Undo menu. Application code can access this label by calling the eval method on the Acl interface. For example, in JavaScript:

```
var lbl = Acl.eval("main::undo_label");
```



---

# undoClear_method

Clears the document's undo history. No changes made before this call can be undone.