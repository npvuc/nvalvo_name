

---

# adapterstatehook

# adapterstatehook

ret = hook ( op , adapterid , arr [])

You register this hook using add_hook to receive information about state changes from a repository adapter. The op argument is an operation code that indicates one of the following notifications:

- • 1 — Repository adapter session connected

- • 2 — Repository adapter session disconnected

- • 3 — Repository adapter to give up user interface control

- • 4 — Additional repository adapter results are available

The adapterid argument is the identifier for the repository adapter. The arr [] argument is the name of an array of returned state information. It is currently only used for an adapter results available ( 4 ) operation and contains a list of Logical IDs that are selected in the repository adapter Browser .

The hook returns a return code ret with one of the following values:

- • 1 — The operation completed successfully

- • 0 — The operation was ignored

- • -1 — The operation returned an error

## Related Topics

- • add_hook function



---

# catalogpathhook

# catalogpathhook

catalogpathhook



Function prototype:

hook ( pathlist )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is catalogpathhook .

This hook is called whenever the catalogpath option is changed.

## Argument

pathlist is a string giving the new list of directories to search for catalogs.



---

# changetrackingaccepthook

# changetrackingaccepthook

ret = hook ( oid1 , oid2 , nonacceptable )



This hook is called before change tracking markup is removed by a call to change_tracking_accept_change . The first and second arguments are oids of the one or two start tags used to mark up a single change track record. The first oid is suitable for a call to change_tracking_info . The nonacceptable parameter is set to 1 if the change record cannot be accepted , otherwise it is 0 .

The return value of the hook may have the following values:

- • –2 — to abort the operation with an error

- • 0 — to perform the operation

- • -1 — to abort the operation without warning



---

# changetrackingafterhook

# changetrackingafterhook

hook ( oid1 , oid2 , optimized )



This hook is called after change tracking markup is inserted. The first and second arguments are oids of the one or two start tags used to mark up a single change track record. The first oid is suitable for a call to change_tracking_info . The optimized parameter is set to indicate the type of optimization done on the markup. 0 means that no optimization was done. Arbortext Editor will automatically optimize (or merge) two changes made by the same user to a single area of text or markup.



---

# changetrackingrejecthook

# changetrackingrejecthook

ret = hook ( oid1 , oid2 , nonrejectable )



This hook is called before change tracking markup is removed by a call to change_tracking_reject_change . The first and second arguments are oids of the one or two start tags used to mark up a single change track record. The first oid is suitable for a call to change_tracking_info . The nonrejectable parameter is set to 1 if the change record cannot be rejected , otherwise it is 0 .

The return value of the hook may have the following values:

- • –2 — to abort the operation with an error

- • 0 — to perform the operation

- • -1 — to abort the operation without warning



---

# chdirhook

# chdirhook

chdirhook

Function prototype:

hook=( wd )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is chdirhook .

This hook is called after the working directory is changed by the cd command or by the Open or Save As dialog boxes.

## Argument

wd is the path name of the new working directory.



---

# completenesseventloghook

# completenesseventloghook

completenesseventloghook

Function prototype:

function celhook( step , message , errorFlag , linkType , linkTarget , linkName )

## Synopsis

If completeness checking is invoked via either the check_completeness command or the doc_incomplete() function with option 4 or 8 set, this hook will be called each time Arbortext Editor finds a completeness error, just before the error is written to the completeness check event log.

## Arguments

- • step is the processing phase that produced the error:

- • message is the actual error message

- • errorFlag is 1 for errors and 0 for warnings

- • linkType is 1 if linkTarget is an OID, 2 if linkTarget is an ACL function

- • linkTarget is either an OID or an ACL function, as determined by linkType :

- • The hook function can return 0 or -1. If it returns -1, the message is written to the completeness checking event log. If the function returns 0, the message is discarded and not written anywhere.



---

# compositionframeworkhook

# compositionframeworkhook

compositionframeworkhook

Function prototype:

hook( doc , type , where , params[] )

This hook is called at several points during the publishing operation. Each time the publishing framework calls the hook, it passes a different where value based on the point in processing. The hook function should check the where value.

The hook will be called for both Arbortext Editor and Arbortext PE server publishing. For Arbortext PE server publishing, the hook needs to be installed on both the client and server if the publishing operation runs a pipeline on the Arbortext PE server .

The publishing framework will invoke the hook function before compose_for_ type () ACL functions start executing, after each operation compose_for_ type () runs, and before compose_for_ type () returns to its caller. Your hook function can return 0 to allow compose_for_ type () to continue executing or return a negative value to terminate the publishing operation. It can modify any or all values in the publishing parameter array, thereby controlling the future flow of execution in compose_for_ type () .

For DITA publishing, at least two pipelines will run, and the hook will be called several times during each pipeline run. Some run only on the client, others can run on either the client or the server. The DITA createPrds pipeline (a pre-process pipeline) always runs on Arbortext Editor client. The regular or post-process pipeline may run on the client or on the Arbortext PE server . Install a compositionframeworkhook on both to avoid problems with pipeline handling. Creating a hook function that can be installed on both client and server assures the appropriate action is performed, whether the processing is taking place on the client or on the server.

For more information on publishing framework processing and the compose_for_ type () functions, refer to The Publishing Framework chapter of the Programmer's Guide to Arbortext Publishing Engine .

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is compositionframeworkhook .

## Arguments

- • doc is the document identifier of the document being published.

- • type is the name of the pipeline or type of published output as represented by its .ccf base file name.

- • where is the point in processing where the hook is called. It is a literal string value that is passed by the publishing framework to the hook function each time the framework calls it. For each string, there is a corresponding ACL variable that specifies the point of operation.

- • params[] is the parameter array that holds the parameters and values to be used by the pipeline.

## Related Topics

- • add_hook function

- • remove_hook function



---

# dcfreloadhook

# dcfreloadhook

dcfreloadhook

Function prototype:

hook(docid)

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is dcfreloadhook .

This hook is called when a document type's configuration file ( .dcf ) is reloaded. This occurs when a .dcf file is saved by Arbortext Editor , when a .dcf file is saved externally to Arbortext Editor and a document of the document type is reverted, or when a .dcf file is loaded by the set dcffile command. The hook is called for each document of the document type.

docid is the document identifier of the document whose associated .dcf file was reloaded.



---

# doc_create_hook

# doc_create_hook

doc_create_hook

This hook is invoked whenever a document is created, such as when opening a document. This hook can be used with Arbortext Publishing Engine applications where running code in advance of a publishing run is difficult.

The following code gives an example of using this hook.

```
package myapp;
function doc_create_hook(doc)
{
response(doc_path(doc));
$ no return value is expected
}
add_hook("doccreatehook", "myapp::doc_create_hook")
```



---

# editbeforehook

# editbeforehook

editbeforehook



Function prototype:

hook (name)

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is editbeforehook .

This hook is called before the document or file specified by name is opened. If this function returns -1 , the switch to a new document is canceled.

For the revert case ( edit -current ), editbeforehook is passed the path name of the document being reverted. The hook detects this case by comparing name to the current document's path name, doc_path(0) .

editbeforehook is called twice if the edit command is used without a path name (that is, to bring up the Open Document dialog box). editbeforehook is called with name equal to the null string before the dialog box appears, and then (if the first call does not return -1 to abort the operation) called a second time with the path name selected from the dialog box.

## Argument

name is the name of the document or file being opened.



---

# editfilehook

# editfilehook

editfilehook

Function prototype:

hook ( code )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is editfilehook .

This hook is called whenever a file is edited, just after the document type instance files ( instance.acl and instance.js ) or document command files ( docname.acl and docname.js ), if any, are read.

## Argument

code is an integer specifying detail about type of edit occurring:

- • 0 — The document is being displayed into a new or empty window.

- • 1 — The document is being reverted.

- • 2 — The document replaces another document in the current window (for example, from an edit command without the -newwindow option, or a doc_show call).

- • 3 — The document is being reverted from its untagged state to its tagged state.



---

# editshowhook

# editshowhook

editshowhook



## Synopsis

Use with:

```
add_hook('editshowhook',
func
[,
prepend
])
remove_hook('editshowhook',
func
)
```

This hook is called before showing a document which is already open. If this function returns -1 , the operation is canceled.

If the hook closes the already open document and returns 0 , the document will be opened.

## Argument

path is the path of the document or file being opened.



---

# entitydeclconflicthook

# entitydeclconflicthook

entitydeclconflicthook



Function prototype:

hook ( docid , dobj , entityname , entitytype , entitysubtype , pubid , sysid , notn , text )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
)
remove_hook(
hookname
,
func
)
```

where hookname is entitydeclconflicthook .

This hook will be called when there is an entity whose declaration in the internal subset and one in the external subset (usually called the DTD).

## Arguments

- • docid is the document identifier of the document in which the declaration was found.

- • dobj is the document object identifier of the document object in which the declaration was found.

- • entityname is the entity name with either & or % prefix.

- • entitytype is the entity type (that is: file , text , graphic , char , filep , msp , accent ).

- • entitysubtype is the entity subtype, that is:

- • pubid is the point in processing where the hook is called. It is a literal string value that is passed by the publishing framework to the hook function each time the framework calls it. For each string, there is a corresponding ACL variable that specifies the point of operation.

- • sysid is the parameter array that holds the parameters and values to be used by the pipeline.

- • notn is the document identifier of the document being published.

- • text is the document identifier of the document being published.

The hook function should return a string to use as the entity name, either without any prefix at all, or with the same prefix as was passed in (& or % ). There are two cases with regards to the string returned:



---

# entityflattenhook

# entityflattenhook

entityflattenhook

Function prototype:

hook ( oid )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
)
remove_hook(
hookname
,
func
)
```

where hookname is entityflattenhook .

This hook will be called when flattening entity references in a document. The hook will be called each time the process encounters a region inside a _file_ent or _text_ent processing instruction tag pair.

## Argument

oid is the oid of a processing instruction “tag pair” that wraps the contents of the entity, at the place where the flattened entity will appear in the saved document. This tag pair is the same as would wrap the entity if it were displayed inline using View > File Entities , or View > Text Entities (that is, oid_name(oid) will return either _file_ent or _text_ent .

If the hook returns -1, that entity reference will not be flattened, but will be left displayed inline, wrapped by the _file_ent or _text_ent tag pair. Any other return value will result in the entity being flattened.



---

# entitylockhook

# entitylockhook

entitylockhook



Function prototype:

hook ( oid, entname )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is entitylockhook .

This hook will be called before an entity is locked, either explicitly (for example, by using the oid_entity_lock function) or implicitly (for example, by typing in the expanded entity). It will only be called if the entity is a locally stored file (entity files stored in a Document Management System cannot be locked this way). It can override or cancel the locking operation similar to using the editbeforehook to detect when the user is about to edit an entity in a separate window.

If the lock operation is not a result of inline editing, then the oid parameter will be null. If this hook returns 0 the code proceeds as if the hook was not called and locks the entity. If it returns –1 the lock operation is cancelled and the attempted locking operation fails, unless the hook locked the entity itself.

## Arguments

- • oid is the oid of the reference to the entity.

- • entname is the name of the entity being locked.



---

# formatbeforehook

# formatbeforehook

formatbeforehook



Function prototype:

hook ( COMMAND , want_final )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is formatbeforehook .

This hook is called immediately before the first formatting pass when printing, previewing, or formatting a document. The want_final flag indicates that the command that caused formatting ( print , preview , format , and so on) was requested to do as many formatting passes as necessary to produce the a final version of the document. For example, if the command that started formatting was

```
preview allpasses
```

formatbeforehook will be invoked with the command parameter set to preview and the want_final parameter set to 1 before each formatting pass.

This hook is allowed to modify the document. When modifying the document, generated text is recalculated and the .tex file is rewritten. This hook cannot be used to invoke formatting.

Returning true writes a new .tex file. Returning false allows a .tex file write but does not force the write. Returning true is appropriate if the hook changes state in such a way that it would affect the result of system functions called from the stylesheet. Typically, a .tex file is rewritten only if the document instance changes or if generated text must be recalculated. The hook assumes formatting is being done on current_doc() .

## Arguments

- • command is a string specifying the command requesting formatting: format , preview , or print .

- • want_final is 1 if all formatting passes are specified. Otherwise, want_final is 0 .



---

# formatcompletehook

# formatcompletehook

formatcompletehook



Function prototype:

hook ( pageno )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is formatcompletehook .

This hook is called when document formatting completes after print or preview processing, if any, has been initiated.

## Argument

pageno is the ordinal page number of the last page formatted.



---

# formatcontinuehook

# formatcontinuehook

formatcontinuehook



Function prototype:

hook ( pageno , doc )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is formatcontinuehook .

This hook is called after formatting has completed, but before print processing or previewing is initiated. It allows you to modify the document and request additional formatting passes.

## Arguments

- • pageno is the ordinal page number of the last page formatted.

- • doc is the document being formatted.

## Return Values

This hook function should return one of the following values:

- • 0 — no more formatting is necessary; continue with normal post-format processing (e.g. initiate printing, update preview window)

- • 1 — perform one additional formatting pass (after which this hook will be called again)

- • 2 — perform as many additional formatting passes as necessary for final output (after which this hook will be called again)

- • 3 — perform additional formatting passes using the -onepass|allpasses modifier on the original formatting command to determine how many to do (after which this hook will be called again)

The output of the additional passes will reflect any changes made to the document by the hook function.

## Related Topics

- • print command

- • preview command

- • formatcompletehook



---

# formaterrorhook

# formaterrorhook

formaterrorhook



Function prototype:

hook ( errorFlag , pageNumber , passNumber , message )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
)
remove_hook(
hookname
,
func
)
```

where hookname is formaterrorhook .

This hook is called if formatting produces an error. If the ACL set formatwarnings option is set to off , this function will not be called for format warning messages.

## Arguments

- • errorFlag is 1 for an error and 0 for a warning.

- • pageNumber is the page being generated when the error or warning is detected, or is -1 if no page number can be determined.

- • passNumber is the formatting pass number. The first pass is number zero.

- • message is the actual error message.



---

# formatpagestatushook

# formatpagestatushook

formatpagestatushook



Function prototype:

hook ( doc , pageno )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is formatpagestatushook .

This hook is called when document formatting starts formatting a new page. Just before formatting begins, this hook is called with a pageno of zero ( 0 ).

## Arguments

- • doc is the document identifier of document being formatted.

- • pageno is the ordinal page number of the page about to be formatted.



---

# graphicpathhook

# graphicpathhook

graphicpathhook

Function prototype:

newname = hook ( filename , oid )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is graphicpathhook .

This hook is used to resolve a graphic file name to display the graphic image in the Edit pane.

## Arguments

- • filename is the path and file name of the graphic as determined from the document instance, after any entity path name resolution has been done. The hook may substitute a different file name by returning its path and file name. Otherwise, the hook must return filename

- • oid is the object ID of the graphic tag identified by filename .



---

# htmldoccompletehook

# htmldoccompletehook

htmldoccompletehook

Function prototype:

hook=( htmldocid, srcdocid )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
)
remove_hook(
hookname
,
func
)
```

where hookname is htmldoccompletehook .

Arbortext Editor calls this hook before returning a virtual HTML document generated from htmldoc function. The hook passes the document's virtual HTML document ID and the associated source document ID to the function func . You can perform any type of supported Arbortext Editor action on the document while it's in memory, such as finding and replacing text. The function is especially useful for changing markup in HTML elements or adding new tags.

## Arguments

- • htmldocid is the document identifier of the virtual HTML document returned by htmldoc .

- • srcdocid is the document identifier of the source document.

The hook function should perform actions that conform to valid standardized HTML markup.



---

# htmlfloathook

# htmlfloathook

htmlfloathook

Function prototype:

hook=( floatnum, fclassname, floattype, src_oid, a_oid, div_oid) )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
)
remove_hook(
hookname
,
func
)
```

where hookname is htmlfloathook .

Arbortext Editor calls this hook when it encounters a float while converting a document to HTML. The hook passes the float's arguments (described below) to the associated function func .

## Arguments

- • floatnum is an integer unique to each float, in order of the float's anchor, such that the first float encountered in the in the document is 1, the next 2, and so on.

- • fclassname is a string which is the floatloc floatid from the FOSI, or in the case of footnotes, it is the string __footnote .

- • floattype is an integer representing the floatloc floattyp from the FOSI where 0 means once, 1 means atpgbrk, 2 means atcolbrk, and 3 means multiref.

- • src_oid is the oid in the SGML or XML document which caused the float per the FOSI. This makes it possible to customize behavior based on which element floated (e.g., a graphic or a table) or based on one of its attribute values, its context, etc.

- • a_oid is the oid of the a element which is inserted into the output virtual document (vdoc). It is the responsibility of the ACL code to assign an href to this element which points to the float, and to insert whatever content is to be used for the hot spot.

- • div_oid is the oid of the div element which is placed around all of the content for a given float in the output vdoc. Unless the float is to be left inline, the function called by the hook should select and cut this oid and its content, and paste or write it elsewhere.



---

# htmlimginserthook

# htmlimginserthook

htmlimginserthook

Function prototype:

hook=( oid,filename )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
)
remove_hook(
hookname
,
func
)
```

where hookname is htmlimginserthook .

Arbortext Editor calls this hook when it encounters a graphic or equation while converting a document to HTML using the htmldoc function. The hook passes the graphic or equation's OID and file name to the associated function func .

## Arguments

- • oid is the object identifier (OID) of the graphic or equation.

- • filename is the complete path and file name of the graphic or equation.

The hook function should return a string that Arbortext Editor will assign to the SRC attribute for the respective IMG element in the HTML document.



---

# includeflattenhook

# includeflattenhook

includeflattenhook

Function prototype:

hook ( dobj )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
)
remove_hook(
hookname
,
func
)
```

where hookname is includeflattenhook .

This hook will be called when flattening XML inclusions in a document. The hook will be called each time the process encounters an XML inclusion.

## Argument

dobj is the document object representing the inclusion to be flattened.

If the hook returns - 1, that inclusion will not be flattened, but will be left displayed inline. Any other return value will result in the inclusion being flattened.



---

# includelockhook

# includelockhook

includelockhook



Function prototype:

hook ( oid, entname )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is includelockhook .

This hook will be called before an XML inclusion is locked, either explicitly (for example, by using the oid_entity_lock function) or implicitly (for example, by typing in the expanded inclusion). It will only be called if the inclusion is a locally stored file (XML inclusion files stored in a Document Management System cannot be locked this way). It can override or cancel the locking operation (similar to using the editbeforehook to detect when the user is about to edit an entity or inclusion in a separate window).

If this hook returns 0 the code proceeds as if the hook was not called and locks the entity.

If it returns – 1 the lock operation is cancelled and the attempted locking operation fails, unless the hook locked the entity itself.

## Arguments

- • oid is the oid of the reference to the XML inclusion.

- • entname is the name of the inclusion being locked.



---

# ixkeycharenthook

# ixkeycharenthook

ixkeycharenthook

Function prototype:

hook ( oid )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is ixkeycharenthook .

The index key character entity hook handles a subset of the problem addressed by the index head to key hook. It allows the user to customize the strings used to replace symbols in index headings.

## Argument

oid is the oid of the desired character entity reference entity name.

The hook function must return a character string to use in the index key in place of the character entity. If an empty string is returned, it means to ignore this entity for sorting purposes. To have default character entity mapping done for an entity, the hook should return the results of the ixkey_charent function.

This is useful when the character entity mapping that Arbortext Editor does based on the configuration files in the Arbortext-path /lib/ixlang directory of the installation tree is not sufficient. For example, your mapping may need to be conditional on the context of an entity's use.



---

# ixkeymarkuphook

# ixkeymarkuphook

ixkeymarkuphook

Function prototype:

hook ( oid )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is ixkeymarkuphook .

Normally, elements and pseudo-tags inside index headings do not affect sorting. (However, if they have generated text in the context of the preliminary index, the generated text does affect sorting.

The index key markup hook allows the user to have markup affect the conversion of an index heading to an index key. Again, this is a subset of the index heading to key conversion process that can be handled by the index head to key hook.

## Argument

oid is the oid of a start tag.

The hook function must return a character string to use in the index key in place of the markup. If an empty string is returned, it means to ignore this markup for sorting purposes.



---

# keybaselistchangedhook

# keybaselistchangedhook

keybaselistchangedhook



Function prototype:

hook ( doc, path )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is keybaselistchangedhook .

This hook will be called any time a DITA document’s ditakeybaselist option is updated.

## Arguments

- • doc is the ACL ID of the document for which the ditakeybaselist option is updated.

- • path is the updated list of paths.



---

# keyrefResolveHook

# keyrefResolveHook

keyrefResolveHook



Function prototype:

hook ( key, type, oid, flag )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is keyrefResolveHook .

This hook will be called any time the keyref or conkeyref attribute on an element in a DITA document is being resolved to an absolute reference.

## Arguments

- • key is the key name that is being resolved.

- • type is the type of reference that is being resolved. Valid values are keyref and conkeyref

- • oid is the object identifier (OID) of the element for which the attribute value is being resolved.

- • flag provides additional information about the type of resolution. If this is set to 0x001 , that indicates the attribute is being used for publishing. If this is not set, that indicates the attribute is being used for editing.



---

# menuloadbeforehook

# menuloadbeforehook

menuloadbeforehook

Function prototype:

hook( window , cmd )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is menuloadbeforehook .

This hook is called before a new set of menus is loaded into the menu bar by a menu_load command or when a new document is loaded.

The hook function can be used to substitute a different set of menus by issuing a recursive menu_load command and returning -1 to signal that the hook function handled the menu load.

## Arguments

- • window is the window identifier of the window containing the menu bar.

- • cmd is the full menu_load command string that will be executed. The hook can modify this command (or replace it) and execute it with the execute function. It should return -1 in this case.



---

# menuloadhook

# menuloadhook

menuloadhook



Function prototype:

hook( window , filename )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is menuloadhook .

This hook is called after a new set of menus is loaded into the menu bar by a menu_load command or by Arbortext Editor when loading a new document. Note, this contrasts with the menuloadbeforehook function which is called before the menu bar has been loaded. Arbortext Editor will not reload menus when switching documents if no menu changes were done. The hook function can be used to add a custom menu to the standard menus using menu_add commands without the need to change the system menu configuration file, editmenu.cf .

## Modifying default menus

You can do the following to modify default menus:

- • For a particular document type, place the commands to modify or load menus in the document type instance command files ( instance.acl and instance.js ).

- • For a specific document, place the commands to modify or load menus in the document command files ( docname .acl and docname .js ) in the directory containing the document docname .

## Arguments

- • window is the window identifier of the window containing the menu bar.

- • filename is the path name of the menu configuration defining the menus. It is null if the system configuration is not read and the default set of menus were loaded.



---

# newfilehook

# newfilehook

newfilehook

Function prototype:

hook ()

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is newfilehook .

This hook is called before the New Document panel is displayed to open a new document.



---

# parsererrorhook

# parsererrorhook

parsererrorhook



Function prototype:

hook(err, msg, file, line)

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is parsererrorhook .

This hook is called before a parser error or warning is output. The hook function is passed err , a boolean specifying 1 if msg is an error and 0 if msg is a warning, and msg is a string containing the parser message. file is the name of the file to which the message applies, and line is the line number in the file producing the error.

If the hook function returns -1 , the message is suppressed. Otherwise, the message is output as usual.

In this example, the hook function suppresses warnings but not errors.

```
function ParserErrorHook(err, msg)
{
if (! err)
{
return -1; # suppress message
}
return 0;
}
add_hook("parsererrorhook", "ParserErrorHook");
```



---

# postexporthook

# postexporthook

postexporthook

Function prototype:

hook(outFile)

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is postexporthook .

The post export hook is called after a successful export operation. The input parameter is the path name of the exported document. The hook is not called if the export fails. The return value of the function is ignored.

## Argument

outFile is the path name of the exported document.



---

# postimporthook

# postimporthook

postimporthook

Function prototype:

hook(doc)

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is postimporthook .

The post import hook is called after the document has been successfully imported, but before the document is displayed in a window (if not batch mode). The input parameter is the document identifier of the imported document. The hook is not called if the import operation fails. If the hook returns -1 , the document will not be displayed in a window (if not batch mode). It is the application's responsibility to close the document in this case.

## Argument

doc is the document identifier of the resulting document.



---

# preexporthook

# preexporthook

preexporthook

Function prototype:

hook(arr[])

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is preexporthook .

This hook is called before the export process begins, just after the user supplies the desired parameters on the Export Document dialog box. The hook function is passed an array containing all the input parameters as specified on the document_export function (or from the dialog box), and may override the settings by altering the array. If the hook function returns -1 , the export operation will be cancelled, causing document_export to return 0 . If the hook modifies any of the parameters in the array, it must return 1 . Otherwise, the function should return 0 .

## Argument

arr is an array parameter whose elements contain the document_export parameters indexed as follows:

- • 1 — the input path name inFile

- • 2 — the output path name outFile

- • 3 — the output file format outFileFmt

- • 4 — the map file path name mapFile

- • 5 — the style template file path name styleTmplt

- • 6 — the log file path name logFile

- • 7 — the boolean batchMode value

## Example

In the following example, the hook function forces the export process to use a different style template by changing the styleTmplt parameter.

```
function PreExportHook(arr[])
{
arr[5] = "//server/templates/company.dot";
return 1; # signal array was changed
}
add_hook("preexporthook", "PreExportHook");
```

## Related Topics

- • document_export function

- • add_hook function

- • preimporthook hook

- • postexporthook hook

- • postimporthook hook



---

# preferencehook

# preferencehook

preferencehook



Function prototype:

hook=(win)

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is preferencehook .

This hook is called just before the Preferences dialog box is displayed. Use this hook to make changes to the dialog box before it displays.

## Argument

win is the window identifier for the desired window.

## Example

In the following example, the preferencehook callback invokes the prefhook function, which hides the Full Menus item on the dialog box.

```
function prefhook(win)
{
dlgitem_hide(win, "fullmenus");
return 0
}
add_hook("preferencehook","prefhook")
```



---

# previewlinkhook

# previewlinkhook

previewlinkhook

Function prototype:

hook ( pageno )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is previewlinkhook .

The previewlinkhook function is called after Arbortext Editor repositions the cursor in the Edit pane due to a request from Print Preview to match the text at the cursor in the Edit pane to the text under the pointer in the Print Preview window. You can get the repositioned location within the document using the oid_caret function.

## Argument

pageno is the ordinal page number displayed in the Print Preview window.



---

# printcompletehook

# printcompletehook

printcompletehook



Function prototype:

hook ()

## Synopsis

This hook is called when a Print Composed request is finished.



---

# profiledochook

# profiledochook

profiledochook



Function prototype:

hook( doc )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is profiledochook .

The profile_config() built-in function calls this hook to allow an alternate profiling configuration document to be specified in place of the one specified in the .dcf file.

## Argument

doc is the document identifier of the instance being loaded.

The hook function can return -1 to disable profiling for the document, 0 to use the default profile document as returned by profile_config() , or the document identifier of a profiling configuration document loaded by the hook function. The hook function may call profile_config() if necessary.



---

# tblmodelprompthook

# tblmodelprompthook

tblmodelprompthook

Function prototype:

ret = hook ( tmIDs[] )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is tblmodelprompthook .

If the current document type supports multiple table models, the tblmodelprompthook function is called when a user inserts a table and the cursor is in a location in which it is valid to insert more than one table model. This hook lets users choose the table model they want to insert.

## Arguments

tmIDs is an array of valid table model IDs.

## Return Arguments

- • -1 — Cancels the table insertion.

- • 0 — Displays the prompt if set prompttablemodels is on , or automatically inserts the primary table model if set prompttablemodel is off .

- • Non-zero integer — A one-based index value into the tmIDs array that indicates the table model to be inserted.

## Related Topics

- • tbl_model_prompt callback type

- • set prompttablemodels



---

# untrackedchangehook

# untrackedchangehook

ret = hook ( doc , type )



This hook is called before a change is made to the document that will not be tracked. In general, the change is permitted but a warning is issued. doc is the document in which the change is being attempted. type is a string containing the name of the attempted operation (command or function) that is being called.

The return value of the hook ret may have the following values:

- • 0 — to perform the operation and warn the user

- • –1 — to silently abort the operation

- • –2 — to abort the operation with an error



---

# userulehook

# userulehook

userulehook

Function prototype:

hook ( window useruleid useparam oid value state docid )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is userulehook .

The userule hook allows the user to customize processing of FOSI usetexts that have non-zero userule values. It can be used either to customize Arbortext Editor 's built-in userule processing (indexing and userule exporting), or to perform entirely different custom processing. The userule hook can be used for any of the following purposes:

- • To alter the preliminary index document and then invoke index processing

- • To change an ACL variable or set option that affects index processing or export handling

- • To alter the contents of a usetext before it is inserted as generated text

- • To conditionally decide whether a usetext should be inserted as generated text

- • To replicate built-in processing for exporting and indexing

The hook is called:

- • when generated text is updated

- • before formatting for published output

- • after a formatting pass if either of these happens:

## Arguments

- • window is the integer id of the window in which index processing occurs. The hook is not expected to use this value except as a “handle” to pass to the indexproc and fosivar_value ACL functions.

- • useruleid is the integer userule id (sequence number). This is also a “handle” to be passed to the indexproc ACL function.

- • useparam is the string value for the useparam.

- • oid is the oid of the element being processed in the user's document instance whose element-in-context (e-i-c) contains the usetext with the non-zero userule.

- • value is the integer userule value.

- • state is the integer indicating userule state. If the state is 1 , this is the first time that the userulehook is being called for this oid and this specific usetext (since it is possible for an oid to have more than one usetext). The contents of the document referenced by docid are from the first pass of formatting. If the state is 2 , the userulehook is being called again for this oid and this specific usetext and the content of the document referenced by docid is different from the previous call. Usually this is because some page numbers have changed. If you are trying to save the contents to a file or drive some external system, you may want to reprocess because of the changes. If the state is 3 , the userulehook is being called again for this oid and this specific usetext and the content of the document referenced by docid has not changed. If you are trying to save the contents to a file or drive some external system, you do not have to reprocess as the contents have not changed.

- • docid is the integer id of the document containing the preliminary content that can be modified.

The hook function must return 1 or -1 . -1 means do not insert the usetext contents into the output stream; 1 means to insert.

If the preliminary document is modified, and it is desired to then insert the preliminary document into the published output stream, the function must return 1 . If nothing is to be inserted in the published output stream, the function must return -1 . (This can be useful if the preliminary userule is written to a file, which is referenced elsewhere in the document or is otherwise processed.)

When using the name of an index coding pseudo-element (perhaps when searching for tag occurrence in the document), you must append an asterisk to the pseudo-element name, (for example, ixpt* ).

## Examples

The following example shows how to alter the preliminary index document and then invoke index processing using the indexproc built in function. This sample code returns the result of indexproc .

```
# example userulehook: change index to uppercase
function simpleuserulefunc(view_id, userule_id, \
userule_param, userule_oid, userule_value, userule_state, \
userule_doc_id)
{
local otop, obot
local savedoc = current_doc(userule_doc_id)
# translate the prelim doc to upper case
otop = oid_first(userule_doc_id)
obot = oid_last(userule_doc_id)
goto_oid(otop)
mark begin
goto_oid(obot)
mark end
translate uc
# convert the prelim index doc into the final index doc
indexproc(view_id, userule_id, userule_param)
current_doc(savedoc)
return 1
}
```

This example shows how to replicate built-in processing for exporting and indexing, and how to add custom processing for userule value 3:

```
function process_userule3(predoc_postdoc)
{
...
}
function ur(view_id, userule_id, userule_param, \
userule_oid, userule_value, userule_state, \
userule_doc_id)
{
local otop, obot
local savedoc = current_doc(userule_doc_id)
if (userule_value == 1 && userule_state < 3)
{
Local filename
filename = "index1.sgml"
write -ok -sgml -nopi -noheader $filename
current_doc(savedoc)
return -1
}
else if (userule_value == 2)
{
indexproc(view_id, userule_id, userule_param)
current_doc(savedoc)
return 1;
}
else if (userule_value == 3)
{
process_userule3(userule_doc_id)
current_doc(savedoc)
return 1
}
return -1;
}
```



---

# writetexafterhook

# writetexafterhook

writetexafterhook

Function prototype:

hook ( command , final )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is writetexafterhook .

This hook is called before the .tex file is written to restart the formatter.

## Arguments

- • command specifies the name of the command requesting formatting: format , preview , or print .

- • final is 1 if final formatting was specified, otherwise is 0 .



---

# writetexhook

# writetexhook

writetexhook

Function prototype:

hook ( command , final )

## Synopsis

Use with:

```
add_hook(
hookname
,
func
[,
prepend
])
remove_hook(
hookname
,
func
)
```

where hookname is writetexhook .

This hook is called before the .tex file is written to restart the formatter.

## Arguments

- • command specifies the name of the command requesting formatting: format , preview , or print .

- • final is 1 if final formatting was specified, otherwise is 0 .