

---

# attribute_default_value_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
oid
,
attrArr
[,flag]
)
```

attribute_default_value is called whenever default attribute values for an element are needed. The callback allows default attribute values to be provided when the default value is not specified in the DTD or schema or when a default value should be inherited from other elements. This callback is only used for Column View display, not during DITA document publishing.

This function returns either a count of the number of items added to attrArr , 0 if no items were added to attrArr , or -1 if there was an error.

Arguments:

- • doc — The identifier of the document containing the element for which you want to provide default values.

- • oid — The object identifier (OID) of the element for which you want to provide default values.

- • attrArr — An input/output associative array with the array key being the attribute names and the array values being the default values for the corresponding attribute.

- • flag — An optional set of option bit flags which default to zero. Allowed values are:



---

# clone_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
clone
)
```

clone is called when the specified document is cloned by the doc_clone function to create a new document. This action can not be cancelled by this callback.

Arguments

- • doc is the identifier of the source document.

- • clone is the identifier of the newly cloned document.

A document may be cloned during some publishing processes. This callback allows an action to be taken on the cloned document before further processing is performed.



---

# completeness_check_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
logname
)
```

completeness_check is called when a completeness check is being performed on the specified document.

Arguments

- • doc is the identifier of the source document.

- • logname is the name of the event log being used for reporting the completeness checking. It is an empty string if the results are not being logged.

This callback can add reports to the event log. The callback should return the number of errors reported to the event log.



---

# conref_content_Callback_Type

Function prototype:

```
function
funcname
(
window
,
oid
,
reference
)
```

conref_content is called to resolve a content reference by a conref or a resolved conkeyref attribute during generated text processing.

Arguments

- • window is the identifier of the window containing the document whose conref or conkeyref content is being resolved.

- • oid is the object identifier (OID) of the element with the conref or conkeyref attribute value to be resolved.

- • reference is the name of the attribute that is being resolved. Allowed values are conref and conkeyref . The default is conref .

The function must return the content to be inserted as an XML markup string, for example, returning the result from calling oid_content on an element in the referenced document. If it returns a null string, the default processing is done. Note that an empty string is also valid content to return. To return an empty string as content, return the value *ATI_EMPTY_STRING* .



---

# context_changed_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
oid
,
pos
)
```

context_changed is called when the caret has moved within the specified document to cause a change in context. This action can not be cancelled by this callback.

Arguments

- • doc is the document containing the active cursor.

- • oid is the OID containing the active cursor.

- • pos is the number of characters into the OID where the cursor is located.

The location within the document specified by oid and pos must be a valid insertion position. If the cursor is currently inside generated text, this callback will be called with a position that is valid for element insertion. You can call the in_context_list function to find out which elements are valid at a particular position.



---

# context_error_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
opcode
,
errcode
,
object
)
```

context_error is called when a context error is detected after certain edit operations, such as inserting tags or text.

context_error must return one of the following values:

- • -2 — Handled the error, the operation will return failure status.

- • -1 — Handled the error, the operation will return success status.

- • 0 — Did not handle the error so normal error processing should be done. That is, the context error message will be displayed.

context_error will not be called if:

- • an attempt to do a pending delete caused a context error

- • an auto-inserted tag caused a context error

If pending delete succeeded, but an error occurred, context_error will be called after the delete. If context_error returns 0 , the delete will be undone, otherwise it will not be undone.

Arguments:

- • doc is the identifier of the document in which the insertion was attempted and can be used to derive the cursor position and/or the selected region.

- • opcode specifies the operation being attempted and currently is one of the following values:

- • errcode defines the type of error and is one of the following values:

- • object is opcode specific:



---

# copy_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
buffername
,
op
)
```

copy is called before a copy operation is done in the Edit pane.

It is not called if the copy will request an external selection (that is, Arbortext Editor does not own the selection). This caveat does not apply to Windows platforms, because they do not support external selections.

A drag and drop action uses a special paste buffer named _APT_DRAGDROP_PASTEBUF . You can check _APT_DRAGDROP_PASTEBUF to tell if the copy operation is due to a drag and drop action.

Arguments

- • doc is the identifier of the document in which the copy was attempted and can be used to derive the cursor position and/or the selected region.

- • buffername is the name of the paste buffer that is the target of the copy. The standard paste buffer is named " default ".

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# create_Callback_Type

Function prototype:

```
function
funcname
(
doc
)
```

create is called whenever a new document is created by an edit or new command, by a call to doc_open , or when a file (external) entity is loaded.

Argument

doc is the identifier of the document created.



---

# cut_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
buffername
,
op
)
```

cut is called before a cut operation is done in the Edit window.

A drag and drop action uses a special paste buffer named _APT_DRAGDROP_PASTEBUF . You can check _APT_DRAGDROP_PASTEBUF to tell if the cut operation is due to a drag and drop action.

Arguments

- • doc is the identifier of the document in which the cut was attempted and can be used to derive the cursor position and/or the selected region.

- • buffername is the name of the paste buffer that is the target of the cut. The standard paste buffer is named " default ".

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

## Related Topics

- • delete_mark command



---

# delete_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
op
)
```

delete is called before a delete operation occurs in the Edit window.

Arguments

- • doc is the identifier of the document in which the delete was attempted and can be used to derive the cursor position or the selected region.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# delete_region_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
buffername
,
startoid
,
startpos
,
endoid
,
endpos
,
flags
,
op
)
```

delete_region is called before an attempt to delete a contiguous region of a document in an edit window. This callback can be used in place of the delete , pending_delete , and cut callbacks.

Arguments:

- • doc — The identifier of the document in which the delete was attempted.

- • buffername — The name of the paste buffer that is the target if the delete is a cut operation. The standard paste buffer is named default . If the delete is not a cut, then buffername will be an empty string.

- • startoid — The object identifier representing the position of the beginning of the region to be deleted.

- • startpos — The position from startoid (in characters) of the start of the region to be deleted.

- • endoid — The object identifier representing the position of the end of the region to be deleted.

- • endpos — The position from endoid (in characters) of the end of the region to be deleted.

- • flags — The following flags can be set:

- • op — The function callback operation. It is generally called twice in succession



---

# delete_tag_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
tagname
,
oid
,
op
)
```

delete_tag is called before a Delete Markup operation is done in the Edit window.

Arguments

- • doc is the identifier of the document in which the Delete Markup was attempted and can be used to derive the cursor position and/or the selected region.

- • tagname is the name of the tag that will be deleted (generally, to the left of the caret position).

- • oid is the object identifier of the element to be deleted.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# destroy_Callback_Type

Function prototype:

```
function
funcname
(
doc
)
```

destroy is called whenever a document is unloaded from memory.

Argument

doc is the identifier of the document being destroyed.



---

# enter_key_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
flags
,
op
)
```

enter_key is called whenever the ENTER key is pressed. The default binding can be changed using this callback.

Arguments

- • doc is the current document associated with this function.

- • flags is a bit mask providing information about the following operation: 0x0001 — the SHIFT key is pressed.

- • op is the standard doc_add_callback operation number (1 on the first call, 2 on the second).

This callback can be used to implement application-specific behavior for the ENTER key for a document or a document type, or for all documents if the callback is registered with 0 as the first parameter to doc_add_callback .



---

# entity_notation_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
entity
,
pubid
,
sysid
,
type
,
notation
)
```

entity_notation is invoked whenever an NDATA-type entity reference is inserted into the document. It is also called for each NDATA-type entity encountered when the document is initially opened. It is not called for NDATA-type entities assigned as attribute values.

Normally, Arbortext Editor treats NDATA entities as "graphic" entities. NDATA entities are treated specially only when they are assigned to a designated attribute of an element marked as a graphic tag. Arbortext Editor ignores graphic entities inserted into the document body (for example, using insert("&ndataent;") ) because they have no effect on the document structure. This callback type allows the application writer to provide any special processing for such entities.

Arguments

- • doc is the identifier of the current document.

- • entity is the name of the entity inserted.

- • pubid is the public identifier or a null string if no PUBLIC ID was specified in the entity declaration.

- • sysid is the system identifier or a null string if no SYSTEM ID was specified in the entity declaration.

- • type is the declared type of the entity and is always "NDATA".

- • notation is the specified data notation.

The return value, if any, of the callback function is ignored.



---

# entity_path_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
entname
,
pubid
,
sysid
,
type
,
notation
)
```

entity_path is called to resolve an external entity and allows an application to override the default way of looking up an external entity path name. It must return the path name of a file to be opened by the standard I/O library functions open or fopen or the null string, if it is not able to associate a system path name with the entity. If a null string, the default processing is done.

If the path name returned is a file (that is, it does not contain any directory components), Arbortext Editor searches the document directory for the name if appropriate, and if a graphic entity, searches the path list specified by the environment variable APTCATPATH to locate the file.

Arguments

- • doc is the identifier of the document associated with the entity path.

- • entname is the name of the entity to be resolved.

- • pubid is the public identifier or a null string if no PUBLIC ID was specified on the entity declaration.

- • sysid is the system identifier or NULL if no SYSTEM ID was specified on the entity declaration.

- • type is the declared type of the entity and is one of the strings "SUBDOC", "NDATA", "CDATA", "SDATA" or the null string if no type was declared (that is, an SGML text entity).

- • notation is the specified data notation if entname is a graphic entity, or the null string otherwise.

Example

Here is an example function that implements the default entity path name processing:

```
function entpathhook(doc, entity, public, system, type)
{
# if a PUBLIC id given, lookup that first and return
# associated path if found
if (public)
{
local path = public_id_path(public)
if (path) { return path;}
}
# otherwise, return SYSTEM if given, else ENTITY name
return system ? system : entity;
}
```

The body of this example function could be replaced by a call to the built-in function entity_path .

## Related Topics

- • entity_path function



---

# exclude_graphic_notation_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
notationname
)
```

exclude_graphic_notation is called before a notation is added to the notation dropdown of the graphic entity dialog box. If exclude_graphic_notation returns 0 , the notation will be added to the notation dropdown. Otherwise, the notation will not be added to the notation dropdown.



---

# exclude_tag_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
tagname
)
```

exclude_tag is called before a tag is added to the insert markup panel. exclude_tag is also called when a menu is posted that contains tag-type menu items. In this case, if exclude_tag returns 0 , the tag menu item is enabled. Otherwise, the menu item is grayed out (made insensitive).

exclude_tag is only called for tags that are in context (that is, it may be inserted at the current cursor position.



---

# generate_id_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
oid
,
attrname
)
```

generate_id is called to provide a generated ID to replace an ID that would otherwise be generated by Arbortext Editor . It returns the generated ID string or null, if no ID is being generated.

Arguments

- • doc is the identifier of the document for which the ID is being generated. When an ID is being generated in a context that does not involve an open or existing document, the value of doc will be zero.

- • oid is the object identifier of the element for which the ID is being generated. When an ID is being generated in a context that does not involve a particular element, the value of oid will be oid_null( ) .

- • attrname is the name of the attribute for which the ID is being generated or a null string when the ID is not being generated for use as an attribute value.



---

# include_path_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
attrs[]
)
```

include_path is called when an XML inclusion section of a document is initially expanded.

Arguments:

- • doc — The identifier of the document containing the XML inclusion reference.

- • attrs[] — An associative array containing the attributes of the XML inclusion tag. Any values changed by the callback will be used instead of the original values if the callback returns -1 .

Also refer to the entity_path callback type .

Following is an example of implementing the include_path callback type.

```
function my_include_path_callback(doc, attrs[])
{
local original_href = attrs['href'];
local new_href = original_href;
# possibly alter new_href here.
if (original_href != new_href)
{
attrs['href'] = new_href;
return -1; # force use of this new href
}
return 0; # continue as normal
}
doc_add_callback(doc, 'include_path', 'my_include_path_callback')
```



---

# insert_content_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
startoid
,
startpos
,
endoid
,
endpos
)
```

insert_content is called by the insert_string command, and the insert command and function after a string that contains markup is successfully inserted. insert_content is also called by the read command after a successful insertion.

insert_content is not called for normal typing, inserting of symbols, or inserting text with the insert command or function.

If a pending delete occurs as a result of the insertion, then the pending_delete_after callback type is called instead of insert_content .

Arguments

- • doc — identifier of the current document.

- • startoid — the object identifier representing the position of the beginning of the inserted content.

- • startpos — the position from startoid in characters of the start of the inserted content.

- • endoid — the object identifier representing the position of the end of the inserted content.

- • endpos — the position from endoid in characters of the end of the inserted content.



---

# insert_entity_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
entity
,
op
)
```

insert_entity is called by the insert_entity command before the entity reference is inserted. If the callback function inserts the reference itself, for example, using the insert function, it should return -1 .

Arguments

- • doc is the identifier of the current document.

- • entity is the name of the entity reference to insert. The name is prefixed with the entity reference open character '&'.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# insert_include_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
uri
,
parse
,
op
)
```

insert_include is called before an XML inclusion reference is inserted by the insert_include command. If the callback function inserts the reference itself, it should return -1 .

Arguments:

- • doc — The document in which the XML inclusion reference is being inserted.

- • uri — The resolved path to the resource (file) to be inserted.

- • parse — The value of the parse attribute of the XML inclusion.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

Example

```
function my_insert_include_callback(doc, uri, parse, op)
{
}
doc_add_callback(doc, 'insert_include', 'my_insert_include_callback')
```

## Related Topics

- • insert_entity callback type



---

# insert_include_path_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
attrs[]
)
```

insert_include_path is called before an XML inclusion reference is inserted by the insert_include command. The callback can optionally modify the path value that will be stored on the href attribute value of the inserted XML inclusion tag.

Arguments:

- • doc — The document in which the XML inclusion reference is being inserted.

- • attrs[] — An associative array containing the attributes of the XML inclusion tag. If any values changed by the callback, -1 is returned.

Example

```
function my_insert_include_path_callback(doc, attrs[])
{
local original_href = attrs['href'];
local new_href = original_href;
# possibly alter new_href here.
if (original_href != new_href)
{
attrs['href'] = new_href;
return -1; # force use of this new href
}
return 0; # continue as normal
}
doc_add_callback(doc, 'insert_include_path', 'my_insert_include_path_callback')
```



---

# insert_tag_after_Callback_Type

Function prototype:

```
function funcname (
doc
,
tagname
,
oid
,
op
)
```

insert_tag_after is called after the element tagname , specified by oid , is inserted into the document.

Arguments:

- • doc is the identifier of the document associated with this function.

- • tagname is the name of the element specified.

- • oid is the object identifier of the start tag that was inserted into the document.

- • op is the function callback operation. op is called twice in succession ( op = 1 and op = 2 ) as is the convention with these callback types, but because the tag insertion has already occurred, it cannot cancel the operation.



---

# insert_tag_auto_Callback_Type

Function prototype:

```
function funcname (
doc
,
oids[]
,
op
)
```

The insert_tag_auto callback is called after tags are automatically inserted when context checking adds required tags, or if auto insertions are specified by the InsertAroundToFix , InsertAutoNested , and InsertAutoHeading categories in the DCF file for the document type.

This function is called after the document is valid and all the changes are applied by the insert_tag , insert_string , newline , read , paste , and split commands and by the insert and insert_tag functions. This function is called before the insert_tag_after callback is called by the insert_tag command and function.

Arguments

- • doc is the identifier of the document associated with this function.

- • oids is an array of object identifiers of the start tags that were automatically inserted, in the order they were inserted into the document.

- • op is the function callback operation. op is called twice in succession ( op = 1 and op = 2 ) as is the convention with these callback types, but because the tag insertion has already occurred, it cannot cancel the operation.



---

# insert_tag_Callback_Type

Function prototype:

```
function funcname (
doc
,
tagname
,
op
)
```

insert_tag is called before the markup specified by tagname is inserted into a document, by either the insert_tag command, the insert_graphic command, or a markup menu item. If the function inserts the markup itself, for example, using the insert_tag function, it should return -1 .

Arguments

- • doc is the identifier of the document associated with this function.

- • tagname is the markup specified.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# keybase_list_changed_Callback_Type

Function prototype:

```
function funcname (
doc
,
path
)
```

The keybase_list_changed callback is called any time a DITA document’s ditakeybaselist option is updated.

Arguments

- • doc is the ACL ID of the document for which the ditakeybaselist option is updated.

- • path is the updated list of paths.



---

# link_Callback_Type

Function prototype:

```
function funcname (
doc
,
oid
,
pos
,
op
)
```

link is called by the link command before the link action is taken, except for URI links. See the callback type linkuri for additional information.

Arguments

- • doc is the identifier of the current document.

- • oid is the object identifier representing the current mouse (if link mouse ) or caret (if link caret ) position.

- • pos is the position from oid in characters of the mouse or cursor as returned by oid_mouse_pos(oid) or oid_caret_pos(oid) .

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

The callback function must return -1 if it performs the link action; otherwise it should return 0 to let Arbortext Editor complete its normal processing.



---

# linkto_Callback_Type

Function prototype:

```
function funcname (
doc
,
target
,
type
,
data
,
op
)
```

linkto is called by the link command before the link action is taken. It is only called when either the -idref or -uri argument is specified for the link command. This is the only callback for the link command if one of these two arguments is specified.

Arguments

- • doc is the identifier of the current document.

- • target is the target of the link, either an IDREF or a URI.

- • type is the type of the target . When type is 0 , the target is an IDREF. When type is 1 , the target is a URI.

- • data is the string specified by the -data argument the link command.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

The callback function must return -1 if it performs the link action; otherwise it should return 0 to let Arbortext Editor complete its normal processing.



---

# linkuri_Callback_Type

Function prototype:

```
function funcname (
doc
,
oid
,
uri
,
op
)
```

When linking to a URI, the link command calls linkuri before any link action is taken. This is unlike all other link actions, which call link hooks instead.

Arbortext Editor determines if a link is to a URI when the LinkUriAttr tag is configured in the .dcf file or in a link:href e-i-c characteristic ( Link URI/ID in a style panel).

Arguments

- • doc — Identifier of the current document.

- • oid — Object identifier representing the current mouse (if link mouse ) or caret (if link caret ) position.

- • uri — target URI.

- • op — Function callback operation. It is called twice in succession:

The callback function must return -1 if it performs the link action; otherwise it should return 0 to let Arbortext Editor complete its normal processing.



---

# modify_tag_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
oid
,
win
,
op
)
```

modify_tag is called before a Modify Attributes dialog box is opened to modify the attributes of an element. This allows an application to automatically set certain attributes before the dialog box is displayed or to prevent the dialog box from being displayed (by destroying it). modify_tag applies only to elements, and cannot be used to set attributes of processing instructions.

modify_tag is called before the dialog box fields are initialized, so that any changes made to attribute values by the callback will be reflected in the dialog box. If modify_tag returns -1 , the Modify Attributes dialog box is not displayed. for example, if modify_tag does not want the tag to be modified or sets the attributes itself.

Arguments

- • doc is the identifier of the document associated with this function.

- • oid is the object identifier of the tag being modified.

- • win is the window identifier of the Modify Attributes dialog box.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# paste_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
buffername
,
after
,
op
)
```

The paste hook is called before a paste operation is done in the Edit window.

A drag and drop action uses a special paste buffer named _APT_DRAGDROP_PASTEBUF . You can check _APT_DRAGDROP_PASTEBUF to tell if the paste operation is due to a drag and drop action.

Arguments

- • doc is the identifier of the document associated with this function.

- • buffername is the name of the paste buffer being pasted.

- • after determines whether the table object(s) in the paste buffer will be pasted before or after the cell, row, or column containing the text caret. If after is zero, the table object(s) in the paste buffer will be pasted before the cell, row, or column containing the text caret. If after is not zero, then the table object(s) in the paste buffer will be pasted after the cell, row, or column containing the text caret. If the hook will be performing the paste itself, it can use this parameter to determine whether the -after flag should be supplied to the paste command.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

## Related Topics

- • paste command



---

# pending_delete_after_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
startoid
,
startpos
,
endoid
,
endpos
)
```

pending_delete_after is called after any successful insertion that followed a pending delete.

Arguments

- • doc — the identifier of the current document.

- • startoid — the object identifier representing the position of the beginning of the inserted content.

- • startpos — the position from startoid in characters of the start of the inserted content.

- • endoid — the object identifier representing the position of the end of the inserted content.

- • endpos — the position from endoid in characters of the end of the inserted content.



---

# pending_delete_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
op
)
```

pending_delete is called before a pending delete operation occurs in the Edit pane.

Arguments:

- • doc — The identifier of the document in which the delete was attempted. It can be used to derive the cursor position or the selected region.

- • op — The function callback operation. It is generally called twice in succession



---

# print_panel_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
prtcmd
,
op
)
```

print_panel is called when the user dismisses the Print Editor View dialog box.

Arguments

- • doc is the identifier of the document associated with this function.

- • prtcmd is a string giving the actual print command used to execute the print request.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

Notes

prtcmd is the null string if the panel was dismissed without the user pressing the OK button.

## Related Topics

- • print command



---

# protect_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
opCode
,
errorCode
)
```

protect is called when an operation is about to fail because of protection. The callback function may tell Arbortext Editor to perform the operation regardless. Currently, this callback is only called when delete operations fail due to a read-only protection error.

Arguments:

- • doc — The identifier of the document in which the operation is being attempted.

- • opCode — A code describing the operation. Currently this value is always 1 for a delete.

- • errorCode — The protection error code. Currently it may be one of the following values:

Return arguments are:

- • 0 — Proceed and let the operation fail due to the protection error.

- • -1 — Ignore the protection error and let the operation continue.



---

# quick_attribute_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
oid
,
win
,
op
)
```

quick_attribute is called before a Quick Attribute dialog box is opened to modify the attributes of an element. This allows an application to automatically set certain attributes before the dialog box is displayed or to prevent the dialog box from being displayed (by destroying it). quick_attribute applies only to elements, and cannot be used to set attributes of processing instructions.

quick_attribute is called before the dialog box fields are initialized, so that any changes made to attribute values by the callback will be reflected in the dialog box. If quick_attribute returns -1 , the Quick Attribute dialog box is not displayed. for example, if quick_attribute does not want the tag to be modified or sets the attributes itself.

Arguments

- • doc is the identifier of the document associated with this function.

- • oid is the object identifier of the tag being modified.

- • win is the window identifier of the Quick Attribute dialog box.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# reference_modify_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
oid
,
prevvalarr
)
```

reference_modify is called whenever a reference attribute has been added or modified. It is not called when a reference attribute is deleted. When reference_modify is called, any additions or changes to an attribute have already been made in the document. The callback is called once per element, even if more than one reference attribute for an element is being added or changed. If one or more modifications are being made as part of a single operation that modifies several elements, the callback is called once for each element. Note that if changes to reference attribute values are made from a reference_modify callback, the callback is not called again for these changes.

Arguments

- • doc is the identifier of the document containing the reference or references for which the value is being added or changed.

- • oid is the object identifier of the element containing the reference or references for which the value is being added or changed.

- • prevvalarr is an associative array with an entry for each reference attribute that is changed. The array is indexed by the reference attribute name. The values are the original values of the reference attributes before the change. These values can be used by the callback to restore a particular element and attribute to its previous value.

The return value of the callback function is ignored and should be zero.



---

# reference_path_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
oid
,
attrname
,
refvalue
)
```

reference_path is used to resolve references other than graphic references. It returns the possibly modified reference value or null, if there was an error. The returned reference value is usually an absolute or relative path name or a Logical ID . If refvalue is to be used unchanged, its value should be returned.

Arguments

- • doc is the identifier of the document containing the reference for which the value is being resolved. If doc is set to zero, the current document is used.

- • oid is the object identifier of the element containing the reference for which the value is being resolved.

- • attrname is the name of the attribute for which the value is being resolved.

- • refvalue is the value of the attribute for which the value is being resolved.



---

# save_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
op
)
```

save is called before a document is saved.

Arguments

- • doc is the identifier of the document associated with this function.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

## Related Topics

- • exit command

- • save command

- • save_as command



---

# saveas_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
filename
,
ro
,
savetype
,
encoding
,
op
)
```

saveas is called when a save_as command is performed before the document is saved. The Save As dialog box issues a save_as command when the user selects OK after choosing a new path name for the document.

Arguments

- • doc is the identifier of the current document.

- • filename is the path name entered from the command line or selected by the user from the Save As dialog box.

- • ro is 1 if the -readonly option was specified on the save_as command or if Read Only was checked on the Save As dialog box.

- • savetype is an integer that indicates any change in file type.

- • encoding is a string. It is a null string if the operating system's encoding is used to save the file. Otherwise, it is a encoding name. Refer to the table below for a list of available encoding names.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

If saveas needs to perform some action after the document is saved, it must execute the save_as command and then return -1 to indicate that the command completed.

Example

```
function saveashook(doc, path, ro, savetype, encoding, op) {
if (op == 1) {
return 0; # proceed
}
if (ro) {
save_as -readonly $path
} else {
save_as $path
}
if (status != 0) {
# command failed
}
# do extra code here ...
return -1; # we did the save
}
```



---

# tbl_cell_clear_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
target
,
content
,
span
,
attrs
,
op
)
```

tbl_cell_clear is called before the tbl_cell_clear ACL function is executed. It may be called by the user from ACL or internally by the table editor user interface.

Arguments

- • doc is the identifier of the document containing the target .

- • target is the table object ID (toid) of the cell to be cleared.

- • content is a boolean: one ( 1 ) if the cell's content is going to be discarded, zero ( 0 ) if the cell's content is not being cleared.

- • span is a boolean: one ( 1 ) if the cell is going to be unspanned, zero ( 0 ) if the cell's spanned state is not being changed.

- • attrs is a boolean: one ( 1 ) if the cell's attributes are going to be set to their default values, zero ( 0 ) if the cell's attributes are not being changed.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# tbl_cell_span_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
ulid
,
lrid
,
op
)
```

tbl_cell_span is called whenever the tbl_cell_span function is called.

Arguments

- • doc is the identifier of the document containing ulid and lrid .

- • ulid is the table object ID (toid) of the upper-left corner cell of the region to be spanned.

- • lrid is the table object ID (toid) of the lower-right corner cell of the region to be spanned.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# tbl_cell_unspan_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
cellid
,
op
)
```

tbl_cell_unspan is called whenever the tbl_cell_unspan function is called.

Arguments

- • doc is the identifier of the document containing cellid .

- • cellid is the table object ID (toid) of the master cell that contains the spanned region's content and attributes.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# tbl_grid_focus_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
gridid
,
window
,
action
)
```

tbl_grid_focus is called whenever a table grid becomes active or inactive in the Edit window.

Arguments

- • doc is the identifier of the document containing gridid .

- • gridid is the table object ID (toid) of the table grid.

- • window is the identifier of the window.

- • action is a boolean: one ( 1 ) if the grid is becoming active, zero ( 0 ) if the grid is becoming inactive.



---

# tbl_insert_after_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
setid
)
```

tbl_insert_after is called after a table is inserted into the document.

Arguments

- • doc is the identifier of the document containing setid .

- • setid is the table object ID (toid) of the TSet containing the table.



---

# tbl_insert_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
oid
,
pos
,
rows
,
cols
,
tmid
,
tag
,
op
)
```

tbl_insert is called before a table is inserted into the document.

Arguments

- • doc is the identifier of the document containing oid .

- • oid and pos indicate where the table is being inserted.

- • rows and cols indicate the number of rows and columns (respectively) within the table that is being inserted.

- • tmid is the table model ID of the table model that will manage the table being inserted.

- • tag is name of the wrapper tag for the table being inserted.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# tbl_model_prompt_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
tmIDs[]
)
```

The tbl_model_prompt callback is called when users try to insert a table in their document, and the cursor is in a location in which it is valid to insert more than one table model.

Arguments:

- • doc is the identifier of the document in which the table will be inserted.

- • tmIDs[] is the array of valid table model IDs.

Return arguments:

- • -1 — Cancels the table insertion.

- • 0 — Displays the prompt if set prompttablemodel is on , or automatically inserts the primary table model if set prompttablemodel is off .

- • Non-zero integer — A one-based index value into the tmIDs array that indicates the table model to be inserted.



---

# tbl_obj_add_after_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
toid
)
```

tbl_obj_add_after is called after a grid, column, or row is inserted into an existing table.

Arguments

- • doc is the identifier of the document containing toid .

- • toid is the table object ID (toid) of the newly inserted grid, row, or column.



---

# tbl_obj_add_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
before
,
after
,
op
)
```

tbl_obj_add is called before a Grid, Column, or Row is inserted into an existing table.

Arguments

- • doc is the identifier of the document containing before and after .

- • before is the table object ID (toid) of the grid, column, or row after which the new grid, column, or row will be inserted.

- • after is the table object ID (toid) of the grid, column, or row before which the new grid, column, or row will be inserted.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

Either the before or after arguments, but not both, may be h::tblNullToid if the new object will be inserted as the first or last grid, row, or column.



---

# tbl_obj_attr_modifiable_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
target
,
attr
)
```

tbl_obj_attr_modifiable is called by the table editor user interface to ask permission to modify a table object attribute.

Arguments

- • doc is the identifier of the document containing target .

- • target is the table object ID (toid) of the table object whose attribute is to be modified.

- • attr is the name of the attribute to be modified. This callback only supports two attributes: TARGET_HEIGHT (rows) and COLWIDTH (columns).

Returns

tbl_obj_attr_modifiable may return:

- • 0 : modification is permitted

- • -1 : modification is forbidden

A return of –1 restricts modification by the row and column rulers, and also by the Table Properties dialog box. However, this callback does not let you restrict changes to the TARGET_HEIGHT and COLWIDTH attributes in other ways, such as using a direct ACL function call. It also does not let you restrict changes to other attributes.

This callback does not let you forbid changes to these attributes in other ways, for example, by a direct ACL function call.



---

# tbl_obj_attr_set_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
target
,
attr
,
old
,
new
,
op
)
```

tbl_obj_attr_set is called before a table object attribute is modified.

Arguments

- • doc is the identifier of the document containing target .

- • target is the table object ID (toid) of the table object whose attribute is to be modified.

- • attr is the name of the attribute to be modified.

- • old is the current attribute value.

- • new is the intended attribute value.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# tbl_obj_delete_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
target
,
op
)
```

tbl_obj_delete is called before a table, grid, column, or row is deleted.

Arguments

- • doc is the identifier of the document containing target .

- • target is the table object ID (toid) of the grid, column or row being deleted.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# tbl_recognize_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
setid
)
```

tbl_recognize is called whenever the table editor notices that a document contains a table. This may occur as a document is opened, during the copying of data to or from a paste buffer, or when manipulation of a document's tags using ACL causes the a collection of tags to match a table template pattern.

Arguments

- • doc is the identifier of the document containing setid .

- • setid is the table object ID (toid) of the TSet containing the table.



---

# tbl_rectangle_copy_after_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
source_ul
,
source_lr
,
target_ul
,
target_lr
)
```

tbl_rectangle_copy_after is called after a successful rectangle-to-rectangle copy.

Arguments

- • doc is the identifier of the document containing target_ul and target_lr .

- • source_ul is the table object ID (toid) of the upper-left corner cell in the region from which the copy is taking place.

- • source_lr is the table object ID (toid) of the lower-right corner cell in the region from which the copy is taking place.

- • target_ul is the table object ID (toid) of the upper-left corner cell in the region where the table objects are being inserted.

- • target_lr is the table object ID (toid) of the lower-right corner cell in the region where the table objects are being inserted.



---

# tbl_rectangle_copy_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
source_ul
,
source_lr
,
target_ul
,
target_lr
,
op
)
```

tbl_rectangle_copy is called before a rectangle of cells is copied from one table to another. Usually the copy takes place between a table in a paste buffer and a table in a document in an Edit window.

Arguments

- • doc is the identifier of the document containing target_ul and target_lr .

- • source_ul is the table object ID (toid) of the upper-left corner cell in the region from which the copy is taking place.

- • source_lr is the table object ID (toid) of the lower-right corner cell in the region from which the copy is taking place.

- • target_ul is the table object ID (toid) of the upper-left corner cell in the region where the table objects are being inserted.

- • target_lr is the table object ID (toid) of the lower-right corner cell in the region where the table objects are being inserted.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.



---

# tbl_rectangle_dragable_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
source_ul
,
source_lr
,
op
)
```

tbl_rectangle_dragable is called by the table editor user interface before a drag-and-drop operation begins. It lets you grant or deny the user interface permission to initiate a drag and drop operation.

Arguments

- • doc is the identifier of the document containing source_ul and source_lr .

- • source_ul is the table object ID (toid) of the upper-left corner cell in the region to be dragged.

- • source_lr is the table object ID (toid) of the lower-right corner cell in the region to be dragged.

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

Returns

tbl_rectangle_dragable may return:

- • 0 : the drag operation should proceed

- • -1 : the drag operation is forbidden



---

# tooltip_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
oid
,
win
,
str
)
```

tooltip is called when a tooltip is about to be raised over a Arbortext Editor window and allows the tooltip to be suppressed or changed.

Arguments

- • doc the identifier of the document containing the element under the cursor.

- • oid is the object identifier of the element under the cursor.

- • win is the window identifier over which the tooltip is to be raised.

- • str is the text that will be shown in the tooltip.

If an empty string is returned, the tooltip will not be raised. Otherwise, the text returned will be shown as the tooltip.



---

# undo_Callback_Type

Function prototype:

```
function
funcname
(
doc
,
detail
,
startoid
,
startpos
,
endoid
,
endpos
)
```

undo is called after any undo or redo operation completes. The detail argument indicates the reason for the callback. The last four arguments give the range of the document affected by the undo operation.

Arguments

- • doc — The identifier of the current document.

- • detail — A code indicating the type of undo operation as follows:

- • startoid — The object identifier representing the beginning position of the range affected by the undo operation.

- • startpos — The position from startoid (in characters) to the beginning of the range affected by the undo.

- • endoid — The object identifier representing the end position of the range affected by the undo.

- • endpos — The position from endoid (in characters) to the end of the range affected by the undo.