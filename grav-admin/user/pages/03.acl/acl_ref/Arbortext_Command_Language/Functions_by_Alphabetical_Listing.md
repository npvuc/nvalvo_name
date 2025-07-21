

---

# access

# access

access ( pathname , string )

This function returns 1 (True) if the file name specified by the expression pathname is accessible according to the mode given by the string string .

The pathname argument is either a file system path or an HTTP or HTTPS resource. For the latter, the function issues an HTTP HEAD request and uses the response to that request to determine if the resource can be accessed.

The string argument is either e (for exists), or a concatenation of one or more of the strings r (for “read”), w (for “write”), and x (for “executable”) based on system permissions for the file. For example:

```
if (access("doc.sgm", "rw"))
```

tests for both read and write permission to the file doc.sgm . If the file does not exist, or if it does not have each of the permissions specified, 0 is returned.



---

# add

# add

layout::add ([ flags [, file ]])



This function declares the atipl namespace, adds page layout markup to a document, and returns the status of the operation. The added markup consists of atipl singletons. The flags parameter is a bit mask used to control the markup inserted. The file parameter specifies the location of the layout file that drives the operation. This layout file is generated automatically when line numbering is applied to a document.

If the operation fails because the source document was write protected or missing, or the layout file is not found or improper, then this function returns -1 . If the document is modified but some markup could not be inserted in the required location, then this function returns 0 . Otherwise, the call is successful and this function returns 1 .

The failure to insert some layout tags in the appropriate locations is expected in some applications (for example, CALS change pages with generated text, tables of contents, and so on). In these cases the atipl tag is inserted at the nearest previous location where it is legal to do so, and the error attribute of the markup is set to 1 .

The flag bits control the type of structure markup to add to the document. These bits are:

- • 0x1 — line

- • 0x2 — entry

- • 0x4 — row

- • 0x8 — float

- • 0x10 — column

- • 0x20 — span

- • 0x40 — page

The default behavior when flags is not specified is to output all structures.

For more detailed information on the page layout elements and their attributes, see http://www.arbortext.com/namespace/pagelayout . Refer to the Programmer's Reference for more detailed information about line numbering applications.

## Related Topics

- • set pagelayoutmarkers

- • set protectpagelayout

- • linenum function

- • layout::clear function

- • layout::apply function



---

# add_filep_entity

# add_filep_entity

add_filep_entity ( name [, sysid [, pubid ]])

This function allows you to declare a file parameter entity (that is, an external parameter entity) in the document's internal subset and insert a reference to the parameter entity.

name is the name for the entity. A leading percent sign % is optional.

sysid is the entity's system identifier.

pubid is the entity's public identifier.

For example, after this function call:

```
add_filep_entity("myent", "/usr/myent")
```

the document's internal declaration will contain:

```
<!ENTITY % myent SYSTEM "/usr/myent">
%myent;
```

The function call in the example has the same effect as these two function calls:

```
declare_filep_entity("myent", "/usr/myent")
insert_filep_entity("myent")
```

## Related Topics

- • declare_filep_entity function

- • insert_filep_entity function

- • delete_filep_entity function



---

# add_graphic_fallback

# add_graphic_fallback

add_graphic_fallback ( primary , fallbacklist , isPrint )

This function allows you to declare fallback types for graphic formats not natively supported by Arbortext Editor .

primary is the file extension for the primary graphic type without a dot, for example c3di or cnv .

fallbacklist is a comma separated list defining the file extensions to look for in secondary (attachment) content

isPrint is the output type for which the fallback types should apply — 1 for printed output, 0 for screen (online) outputs

For example:

```
add_graphic_fallback("c3di", "pvz,tif", 0)
```

For Arbortext Editor connected via the PTC Server connection , the fallback uses the adapter call sess_get_file() to obtain the fallback rendition.

When publishing a payload with Arbortext Publishing Engine , the fallback uses the ResourceMap in the manifest.xml to determine what attachment to use.

If the fallback graphic is not supplied, or there are no matching attachments, publishing will produce an error message

## Related Topics

- • Supported Graphic File Formats

- • Intelligent Graphics Overview

- • sess_get_file()



---

# add_hook

# add_hook

add_hook ( hookname , funcname [, prepend ])

This function adds a callback function to the list of functions for the specified hook, where hookname is the name of the hook set option. The argument funcname is a string specifying the name of the user-defined function to call. If the optional argument prepend is specified and non-zero, funcname is added to the head of the hook function list. If not specified or zero, funcname is appended to the list

add_hook will not add funcname if it is already present in the hook list.

Refer to Hook functions introduction for a detailed introduction to ACL hooks.

## Related Topics

- • remove_hook function



---

# agettext

# agettext

msg_string= agettext ( msg_id )

This function retrieves the message msg_id from the default message file.

If the function executes correctly, it returns the string for the desired message ID. If the function fails, it returns the value of the msg_id argument.

Example

```
msg_string = agettext('Context checking is disabled')
```

## Related Topics

- • amo_text built-in function



---

# amo_close

# amo_close

amo_close ( msg_file_id )

This function closes the message file specified by the argument msg_file_id . The msg_file_id is the message file ID for a message file previously opened with amo_open .

If the function executes correctly, it returns the message file ID of the closed file. If the function fails, it returns a -1.

Example

```
$ret = amo_close(msg_file_id)
```

## Related Topics

- • amo_open built-in function



---

# amo_open

# amo_open

msg_file_id= amo_open ( path )

This function opens the message file specified by the path parameter. The path parameter should include both a path and file name (including extension) for the desired message file. You must use UNIX path separators (that is, / ) in your path argument.

If the function executes correctly, it returns a message file ID. If the function fails, it returns a -1.

Examples

```
msg_file_id = amo_open('/editor/lib/locale/fr/message.amo')
msg_file_id = amo_open('../custom_messages/message.amo')
```

## Related Topics

- • amo_close built-in function



---

# amo_text

# amo_text

msg_string= amo_text ( msg_file_id , msg_id )

This function retrieves the localized message msg_id within the message file specified by the msg_file_id parameter. The msg_file_id parameter is the message file ID for a message file previously opened with amo_open . The msg_id parameter is the message ID for a message within the open message file.

If the function executes correctly, it returns the string for the desired message ID. If the function fails, it returns the value of the msg_id parameter.

Example

```
msg_string = amo_text(msg_file_id, \
'Context checking is disabled')
```

## Related Topics

- • agettext built-in function



---

# append_catalog_path

# append_catalog_path

append_catalog_path ( dir [, prepend ])

This function appends the directory dir to the set catalogpath option if not already present. If the optional argument prepend is specified and non-zero, dir is added to the beginning of the path list, removing any later occurrence of the directory. If prepend is zero or omitted and if dir is already present in the path list, the path list is returned.

For example, if you wanted to append your document types stored in the doctypes subdirectory of the company directory, so your document types are searched last:

```
append_catalog_path('/company/doctypes')
```

If you wanted to prepend your document types stored in that same doctypes subdirectory, so your document types are searched first:

```
append_catalog_path('/company/doctypes',1)
```

If there is a catalog file in the Arbortext-path \custom\doctypes subdirectory at startup, the \custom\doctypes path is automatically prepended to the catalog path. If there are any subdirectories of the \doctypes directory that contain a catalog file, those subdirectories are also prepended to the catalog path. Putting a catalog file in \custom\doctypes or in subdirectories of it makes them automatically available, avoiding additional steps to add them to the path.

## Related Topics

- • set catalogpath command



---

# append_composer_path

# append_composer_path

append_composer_path ( dir [, prepend ])

The append_composer_path function appends dir to the directories specified by the set composerpath command. If the optional prepend argument is specified and non-zero, dir is added to the beginning of the path list, removing any later occurrence of the directory. If prepend is zero or omitted and if dir is already present in the path list, the path list is returned.

For example, if you want to append a directory stored in the composer subdirectory of the company directory, so your configuration files are searched last:

```
append_composer_path("/company/composer")
```

If you want to prepend your directory stored in the company subdirectory, so your configuration files are searched first:

```
append_copmposer_path('/company/composer',1)
```

If there is an Arbortext-path \custom\composer subdirectory at startup, the \custom\composer path is automatically prepended to the path for .ccf files. Putting your .ccf files in the \custom\composer subdirectory makes them automatically available, avoiding manual steps to add them to the path.

## Related Topics

- • set composerpath command



---

# append_dialogs_path

# append_dialogs_path

append_dialogs_path ( dir [, prepend ])

This function appends the search path for dialog files that can be called from a custom application, such as one that uses the AOM Application.createDialogFromFile method (documented in the Programmer's Reference . The append_dialogs_path function appends dir to the directories specified by the set dialogspath command . If the optional prepend argument is specified and non-zero, dir is added to the beginning of the path list, removing any later occurrence of the directory. If prepend is zero or omitted and if dir is already present in the path list, the path list is returned.

For example, if you want to append your dialog file directory stored in the mydialogs subdirectory of the company directory, so your dialog file path is searched last:

```
append_dialogs_path("/company/mydialogs")
```

If you want to prepend your dialog files directory, so your dialog file path is searched first:

```
append_dialogs_path('/company/mydialogs',1)
```

If there is an Arbortext-path \custom\dialogs subdirectory at startup, the custom\dialogs path is automatically prepended to the path for dialog files. Putting your custom dialog files in the custom\dialogs subdirectory makes them automatically available, avoiding manual steps to add them to the path.



---

# append_dita_path

# append_dita_path

append_dita_path ( dir [, prepend ])

This function appends the directory dir to the set ditapath option to search for content referenced by DITA documents, if the directory is not already present. If the optional argument prepend is specified and non-zero, dir is added to the beginning of the path list, removing any later occurrence of the directory. If prepend is zero or omitted and if dir is already present in the path list, the path list is returned.

For example, if you wanted to append your DITA references directory stored in the ditareferences subdirectory of the company directory, so your DITA references are searched last:

```
append_dita_path("/company/ditareferences")
```

If you wanted to prepend your ditareferences subdirectory, so your DITA references are searched first:

```
append_dita_path('/company/ditareferences',1)
```

If there is an Arbortext-path \custom\ditarefs subdirectory at startup, the custom\ditarefs path is automatically prepended to the DITA references path. Putting your DITA references in the custom\ditarefs subdirectory makes them automatically available, avoiding manual steps to add them to the path.

Graphic references in DITA files are resolved using the graphics path.

## Related Topics

- • set graphicspath command

- • APTDITAPATH environment variable



---

# append_entity_path

# append_entity_path

append_entity_path ( dir [, prepend ])

This function appends the directory dir to the set entitypath option if not already present. If prepend is 1 , prepends dir to the entitypath path, removing any later occurrence of the directory.

Examples

If you wanted to append entities in the /company/entities subdirectory, so your entities are searched last:

```
append_entity_path('/company/entities')
```

If you wanted to prepend entities in the same /company/entities subdirectory, so your entities are searched first:

```
append_entity_path('/company/entities',1)
```

If there is an Arbortext-path \custom\entities subdirectory at startup, the \custom\entities path is automatically prepended to the entities path. Putting your entity files in the \custom\entities subdirectory makes them automatically available, avoiding manual steps to add them to the path.

## Related Topics

- • set entitypath command



---

# append_frameset_path

# append_frameset_path

append_frameset_path ( dir [, prepend ])

This function appends the directory dir to the set framesetpath option if not already present. If prepend is 1 , prepends dir to the framesetpath path, removing any later occurrence of the directory.

If there is an Arbortext-path \custom\framesets subdirectory at startup, the \custom\framesets path is automatically prepended to the frameset path. Putting your entity files in the \custom\framesets subdirectory makes them automatically available, avoiding manual steps to add them to the path.

## Related Topics

- • Specifying framesets for web publishing



---

# append_graphics_path

# append_graphics_path

append_graphics_path ( dir [, prepend ])

This function appends the directory dir to the set graphicspath option if not already present. If the optional argument prepend is specified and non-zero, dir is added to the beginning of the path list, removing any later occurrence of the directory. If prepend is zero or omitted and if dir is already present in the path list, the path list is returned.

For example, if you wanted to append your graphics directory stored in the graphics subdirectory of the company directory, so your graphics are searched last:

```
append_graphics_path("/company/graphics")
```

If you wanted to prepend your graphics directory stored in the graphics subdirectory, so your graphics are searched first:

```
append_graphics_path('/company/graphics',1)
```

If there is an Arbortext-path \custom\graphics subdirectory at startup, the \custom\graphics path is automatically prepended to the graphics path. Putting your graphics in the \custom\graphics subdirectory makes them automatically available, avoiding manual steps to add them to the path.

## Related Topics

- • set graphicspath command



---

# append_javaclass_path

# append_javaclass_path

append_javaclass_path ( dir [, prepend ])

This function appends the directory dir to the set javaclasspath option if not already present. If the optional argument prepend is specified and non-zero, dir is added to the beginning of the path list, removing any later occurrence of the directory. If prepend is zero or omitted and if dir is already present in the path list, the path list is returned.

Arbortext Editor has an embedded Java Virtual Machine that uses this directory list to search for Java classes when a Java method is called. Arbortext Editor automatically searches the distributed JAR files in the Arbortext-path /lib/classes directory.

Note that any specification for Java class path is only evaluated when the first java_ type function is called in a Arbortext Editor session. Subsequent changes to the path will not affect the running Java Virtual Machine until you exit Arbortext Editor and start a new session. Consequently, when using the java_ type functions, you should call the append_javaclass_path function before invoking a java_ type function.

Examples

If you wanted to append your directory for your Java class files stored in the /company/javaclass subdirectory, where your Java class directory would be searched last:

```
append_javaclass_path("/company/javaclass")
```

If you wanted to prepend your directory for your Java class files stored in the /company/javaclass subdirectory, where your Java class directory would be searched first:

```
append_javaclass_path('/company/javaclass',1)
```

If there is an Arbortext-path \custom\classes subdirectory at startup containing any JAR files ( .jar ), the path for each .jar file is automatically prepended to the Java class path for Arbortext Editor . Then the \custom\classes path is prepended, which automatically includes any compiled Java .class files in it. Putting your .class and .jar files in the \custom\classes subdirectory makes them automatically available, avoiding manual steps to add them to the path.

## Related Topics

- • set javaclasspath command

- • java_constructor function

- • java_init function

- • java_instance function

- • java_static function

- • set javadebugport command

- • set javavmargs command

- • set javavmmemory command

- • set javavmpath command



---

# append_load_path

# append_load_path

append_load_path ( dir [, prepend ])

This function appends the directory dir to the set loadpath option if not already present. If the optional argument prepend is specified and non-zero, dir is added to the beginning of the path list, removing any later occurrence of the directory. If prepend is zero or omitted and if dir is already present in the path list, the path list is returned.

If there is an Arbortext-path \custom\scripts subdirectory at startup, the \custom\scripts is automatically prepended to the load path for ACL, JavaScript, JScript, and VBScript files. Putting these supported script file types in the \custom\scripts subdirectory makes them automatically available, avoiding manual steps to add them to the path.

## Related Topics

- • set loadpath command



---

# append_newlist_path

# append_newlist_path

append_newlist_path ( dir [, prepend ])

This function appends dir to, or removes dir from, the set newlist command path. dir can be a directory path, a directory path and a file name, or a directory path relative to a directory in the catalog path. If the optional argument prepend is specified and non-zero, dir is added to the beginning of the path list, removing any later occurrence of the directory. If prepend is zero or omitted and if dir is already present in the path list, the path list is returned.

The set newlist command specifies a list of paths to document types that appear in the Type list in the New Document dialog box.

For example, if you want to append your document type stored in the c:\mydoctypes\guide directory, you would type:

```
append_newlist_path('c:\mydoctypes\guide')
```

You can remove a document type from the Type list in the New Document dialog box. To do this, add a caret (^) character before the document type that you want to remove. You only have to specify the base name of the .dtd file.

For example, if you want to remove the Arbortext Editor XML DocBook V4.0 document type from the list, you would type:

```
append_newlist_path('^axdocbook')
```

where axdocbook is the base name of the DTD ( axdocbook.dtd ).

If any document types are automatically loaded from the Arbortext-path \custom\doctypes subdirectory, their paths are also prepended to the document type paths that appear in the Type list in the New Document dialog box.

## Related Topics

- • set newlist command

- • New Document dialog box



---

# append_path

# append_path

append_path ( pathlist , dir [, prepend ])

This function returns a string formed by concatenating the path list specified by pathlist and the directory specified by dir separated by the path list separator $PLS (a semicolon). If the optional argument prepend is specified and non-zero, dir is added to the beginning of the path list, removing any later occurrence of the directory. If prepend is zero or omitted and if dir is already present in the path list, pathlist is returned.



---

# append_tagtemplate_path

# append_tagtemplate_path

append_tagtemplate_path ( dir [, prepend ])

This function appends the directory specified by dir to the set tagtemplatepath option if not already present. If prepend is 1 , prepends dir to the tagtemplatepath path, removing any later occurrence of the directory.

If there is an Arbortext-path \custom\tagtemplates subdirectory at startup, the custom\tagtemplates path is automatically prepended to the tag template path.

You can put custom tag templates you want associated with a particular document type into a custom\doctypes\ doctype \tagtemplates directory or in the original location of the document type's doctype \tagtemplates directory.

Putting your tag template files in the custom\tagtemplates subdirectory makes them automatically available, avoiding manual steps to add them to the path.

## Related Topics

- • Using tag templates



---

# append_userdict_path

# append_userdict_path

append_userdict_path ( dir [, prepend ])

This function appends the directory dir to the set userdictpath option if not already present. If prepend is 1 , prepends dir to the user dictionary path, removing any later occurrence of the directory.

If there is an Arbortext-path \custom\dictionaries subdirectory at startup, the custom\dictionaries path is automatically prepended to the user dictionary path. Putting your user dictionary files in the custom\dictionaries subdirectory makes them automatically available, avoiding manual steps to add them to the path.

## Related topic

- • APTDICTPATH environment variable



---

# application_name

# application_name

application_name ([ untranslated ])

The application_name function returns the name of the application which is currently running, for instance Arbortext Editor , Arbortext Architect , Arbortext Publishing Engine Interactive or Arbortext Editor with Arbortext Styler . Your custom application might use this function to compare its result with a set of possible values.

If the optional untranslated parameter is present and not zero, the name is returned in English. If no parameter is given or if untranslated is specified as zero, this function returns the value of the built-in variable $main::progname . This value could be a translated version of the name (such as Arbortext Editor con Arbortext Styler for the es Spanish locale).

## Related Topics

- • get_custom_dir function

- • get_custom_property function

- • get_user_property function



---

# apply

# apply

layout::apply ( application [, flags [, doc ]])



This function uses the current print FOSI to add page layout structure to the document and then calls an application specific function. The markup consists of singletons with the atipl namespace prefix, for example atipl:startpage .

The application parameter is the name of a callable function that implements some application specific behavior. Most commonly it will specify a set of generic attributes of the atipl markup to achieve a set of formatting effects. The application function must accept a single parameter: the document to modify, and return a status of 0 for failure or 1 for success. A sample line numbering application is located in the samples\linenumbering folder of your installation directory.

The optional flags parameter is a bit mask used to control the markup inserted. If not specified, then all possible markup is inserted. The bits control the type of structured markup to add to the document. These bits are:

- • 0x1 — line

- • 0x2 — entry

- • 0x4 — row

- • 0x8 — float

- • 0x10 — column

- • 0x20 — span

- • 0x40 — page

- • 0x1000 — generate diagnostics

- • 0x2000 — no atipl markup for lines that contain only generated text

The optional doc parameter specifies the document to modify. The current document is assumed if this parameter is not specified.

If the operation fails the function returns 0 . If the operation succeeds then the function returns 1 .

For more detailed information on the page layout elements and their attributes, see http://www.arbortext.com/namespace/pagelayout . Refer to the Programmer's Reference for more detailed information about line numbering applications.

## Related Topics

- • set pagelayoutmarkers

- • set protectpagelayout

- • layout::add function

- • layout::clear function

- • linenum function



---

# apply_profile_group

# apply_profile_group

apply_profile_group ( apply_profile_group_name , arr [, doc ])

Returns the number of profile classes that are included in the specified apply profile group.

- • apply_profile_group_name — The apply profile group for which the function returns the number of profile classes.

- • arr — Associative array of the values of the profile classes included in the specified apply profile group.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.

If more than one value exists for a particular profile class, the different values will be separated using the value separator. For example:

```
arr[alias1] = value
arr[alias2] = value1;value2
```



---

# apply_profile_group_allowed

# apply_profile_group_allowed

apply_profile_group_allowed ( apply_profile_group_name , oid , arr[] )

Returns 1 if the profile group apply_profile_group_name , is allowed on the element oid .

If the group is not allowed, apply_profile_group_allowed returns 0 and fills the array arr[] with the alias or aliases of the invalid profiles that cause the group to not be allowed. The array is associative. It has the alias name as the index and the profilenode for the alias as the value. For example,

```
arr[ "Security"] = (1, 1, 1)
```



---

# apply_profile_group_value_nodes

# apply_profile_group_value_nodes

apply_profile_group_value_nodes ( apply_profile_group_name , arr [, doc ])

Returns the number of value profilenodes of all the profile classes that are included in the specified apply profile group.

- • apply_profile_group_name — The apply profile group for which the function returns the number of value profilenodes of the profile classes.

- • arr — Array of the value profilenodes of all the profile classes that are included in the specified apply profile group.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# apply_profile_groups

# apply_profile_groups

apply_profile_groups ( arr [, doc ])

Returns the number of apply profile groups specified in the profile configuration file.

- • arr — Array of the names of all the apply profile groups specified in the profile configuration file.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# attr_alias

# attr_alias

attr_alias ( attr [, element [, doc ]])

This function returns the alias of the attribute attr , where attr is the real name of the attribute as defined in the DTD, or the alias. Specify element if you want this function to return an element-specific attribute alias ( element can be the real name or an alias). If element is omitted, this function returns the alias of a global attribute. A null string is returned if attr does not have an alias.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is searched.

## Related Topics

- • Alias map overview

- • attr_real_name function

- • attr_value_real_name function

- • attr_value_alias function

- • tag_real_name function

- • tag_alias function



---

# attr_description

# attr_description

attr_description ( attr [, element [, doc ]])

This function returns the description for attr . Specify element if you want this function to return an element-specific attribute description. If element is omitted, this function returns the description of a global attribute. A null string is returned if attr does not have a description.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is searched.

## Related Topics

- • Creating element and attribute descriptions

- • Viewing element and attribute descriptions in your document

- • tag_description function



---

# attr_real_name

# attr_real_name

attr_real_name ( attr [, element [, doc ]])

This function returns the real name as specified in the DTD of the specified attr , where attr is the real name or alias of the attribute. Specify element if you want this function to return the real name of an element-specific attribute ( element can be a real name or an alias). If element is omitted, this function returns the real name of a global attribute.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is searched.

## Related Topics

- • Alias map overview

- • attr_alias function

- • attr_value_real_name function

- • attr_value_alias function

- • tag_real_name function

- • tag_alias function



---

# attr_value_alias

# attr_value_alias

attr_value_alias ( value [, attr [, element [, doc ]]])

This function returns the alias of the specified attribute value , where value is the real name of the attribute value as defined in the DTD, or its alias. Specify attr and element if you want this function to return the alias of an element-specific attribute value ( element and attr can be real names or aliases). If both attr and element are omitted, this function returns the alias of a global attribute value. A null string is returned if value does not have an alias.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is searched.

## Related Topics

- • Alias map overview

- • attr_value_real_name function

- • attr_real_name function

- • attr_alias function

- • tag_real_name function

- • tag_alias function



---

# attr_value_real_name

# attr_value_real_name

attr_value_real_name ( value [, attr [, element [, doc ]]])

This function returns the real name as specified in the DTD of the specified attribute value , where value is the real name or alias of the attribute value. Specify attr and element if you want this function to return the real name of an element-specific attribute value ( element and attr can be real names or aliases). If both attr and element are omitted, this function returns the real name of a global attribute value.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is searched.

## Related Topics

- • Alias map overview

- • attr_alias function

- • attr_real_name function

- • attr_value_alias function

- • tag_real_name function

- • tag_alias function



---

# base_tag_name

# base_tag_name

base_tag_name ( tagname [, doc ])

This function returns the base element name for the user-defined tag named tagname . Returns null if tagname is not a valid element name. If the tag, tagname , is a base element, and not a user-defined tag, returns tagname .

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# basename

# basename

basename ( path [, sfx ])

This function returns the base name of the file specified by path , removing any leading directory components and the suffix specified by sfx if present. If sfx is .* , then all characters following a trailing . are removed, including the period.



---

# blength

# blength

blength ( str )

Returns the number of bytes in the string specified by str . This contrasts with the length function which returns the number of characters. For example, blength("abc") returns 6 whereas length("abc") returns 3 .



---

# buffer_clipboard_contents

# buffer_clipboard_contents

buffer_clipboard_contents ( buf [, format ])

This function copies the contents of a specified format from the system clipboard to the scalar variable buf . If format is omitted or empty, then the standard clipboard text format is copied and the function returns the number of characters copied into buf . If format is specified and matches an application registered clipboard format (for example, rich text format ), then that format is copied and the function returns the number of bytes copied into buf .

If the set selectionsvc option is off, this function always returns 0 .

Following is an example of a paste callback that pastes Rich Text Format content, instead of normal text content, when RTF is available:

```
global PASTE_RTF_BUFFER_NAME = 'rtfpaste';
function cb_rtf_paste(doc, buff, op) {
if (op != 2) {
return 0;
}
# Check if there is RTF available on the system clipboard
if (! buffer_is_clipboard("rich text format")) {
return 0;
}
local text;
local len = buffer_clipboard_contents(text, "rich text format");
if (len == 0) {
return 0;
}
# There is, so create a named paste buffer
local second_doc = buffer_create(PASTE_RTF_BUFFER_NAME, public_id(doc));
current_doc(second_doc);
# and insert the RTF
insert(mbstoucs(text, len));
current_doc(doc);
# remember original paste buffer
local org_buffer = option('paste');
# paste from our named paste buffer
set paste = $PASTE_RTF_BUFFER_NAME;
paste;
# reset paste buffer
if ('' == org_buffer) {
set paste = default;
} else {
set paste = $org_buffer;
}
# delete the special buffer
delete_buffer $PASTE_RTF_BUFFER_NAME;
return 1;
}
```

## Related Topics

- • set selectionsvc command

- • buffer_clipboard_formats function



---

# buffer_clipboard_formats

# buffer_clipboard_formats

buffer_clipboard_formats ( arr )

This function fills the array arr with the names of the application registered clipboard formats currently available on the system clipboard. The function returns the number of names loaded into the array.

If the set selectionsvc option is off, this function always returns 0 .

## Related Topics

- • set selectionsvc command

- • buffer_clipboard_contents function



---

# buffer_create

# buffer_create

buffer_create ( name [, pubid [, subtype ]])

This function creates a new named paste buffer name and returns a document identifier that may be used on subsequent calls to functions that operate on document trees. The pubid and subtype arguments are used to specify the document type for the paste buffer. See the doc_open function for details. If omitted, the document type of the current document is used.



---

# buffer_doc

# buffer_doc

buffer_doc ( name )

This function returns the document identifier of the paste buffer named by name . buffer_doc returns -1 for the current paste buffer. buffer_doc also returns -1 if name is default , or if the named buffer does not exist.



---

# buffer_empty

# buffer_empty

buffer_empty ( [name] )

This function can be used to tell whether a local buffer contains data. If name is omitted, the default paste buffer is used.

If this function is called from a paste callback function, it will return 0 since the paste buffer always has contents at that point.



---

# buffer_is_clipboard

# buffer_is_clipboard

ret = buffer_is_clipboard ([ format ])

This function returns 1 (True) if the system owns the specified format on the clipboard. If format is omitted or empty, then the standard clipboard text format is assumed and the function returns 0 (False) if either Arbortext Editor 's default paste buffer is not empty (meaning Arbortext Editor owns the clipboard) or the system clipboard is empty. If the set selectionsvc option is off, this function always returns 0 .

This function will return 0 if called from a paste callback function when format is omitted or empty, since at that point Arbortext Editor owns the clipboard.

## Related Topics

- • set selectionsvc command



---

# buffer_is_table

# buffer_is_table

ret = buffer_is_table ( name , $gridId [, external ])

This function returns 1 (true) if the content of the paste buffer name represents a single table for the current document. If name is the empty string, the default paste buffer is assumed.

If buffer_is_table returns 1 , $gridId is set to the TOId (table object identifier) for the grid.

If external is omitted or 0 , the system clipboard is not checked. If external is not 0 , the content of the system clipboard is checked to see if it represents the markup of a single table for the current document.



---

# bulleted_list_block_tag_name

# bulleted_list_block_tag_name

bulleted_list_block_tag_name ( arr [, doc ])

This function returns the name of the primary bulleted list block tag specified in the document type configuration file ( .dcf ) for the document type associated with doc . This tag is inserted when users select the bulleted list button on the Application toolbar .

If a tag name is returned, bulleted_list_block_tag_name function returns arr with an attribute name and attribute value, if they were specified for the tag in the .dcf file.

The function returns the null string if there isn't a bulleted list block tag designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

For example,

```
local tag, arr[];
local attr, val;
tag = bulleted_list_block_tag_name(arr);
attr = arr['attribute'];
val = arr['attribute_value'];
```

## Related Topics

- • Document type configuration files

- • Configuring tags as list elements

- • bulleted_list_block_tag_name_ns function

- • bulleted_list_item_tag_name function

- • set toolbar4 command



---

# bulleted_list_block_tag_name_ns

# bulleted_list_block_tag_name_ns

bulleted_list_block_tag_name_ns ( arr [, doc ])

This function returns the namespace URI prefixed to the primary bulleted list block tag specified in the document type configuration file ( .dcf ) for the document type associated with doc . This tag is inserted when users select the bulleted list button on the Application toolbar .

If a URI is returned, bulleted_list_block_tag_name_ns function returns arr .

The function returns the null string if there isn't a namespace prefix for the tag, if no bulleted list block tag is designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

## Related Topics

- • Document type configuration files

- • Configuring tags as list elements

- • bulleted_list_block_tag_name function

- • bulleted_list_item_tag_name_ns function

- • set toolbar4 command



---

# bulleted_list_item_tag_name

# bulleted_list_item_tag_name

bulleted_list_item_tag_name ( arr [, doc ])

This function returns the name of the primary bulleted list item tag specified in the document type configuration file ( .dcf ) for the document type associated with doc . This tag is inserted, along with the bulleted list block tag, when users select the bulleted list button on the Application toolbar .

If a tag name is returned, bulleted_list_item_tag_name function returns arr with an attribute name and attribute value, if they were specified for the tag in the .dcf file.

The function returns the null string if there isn't a bulleted list item tag designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

For example,

```
local tag, arr[];
local attr, val;
tag = bulleted_list_item_tag_name(arr);
attr = arr['attribute'];
val = arr['attribute_value'];
```

## Related Topics

- • Document type configuration files

- • Configuring tags as list elements

- • bulleted_list_block_tag_name function

- • bulleted_list_block_tag_name function

- • set toolbar4 command



---

# bulleted_list_item_tag_name_ns

# bulleted_list_item_tag_name_ns

bulleted_list_item_tag_name_ns ( arr [, doc ])

This function returns the namespace URI prefixed to the primary bulleted list item tag specified in the document type configuration file ( .dcf ) for the document type associated with doc . This tag is inserted, along with the bulleted list block tag, when users select the bulleted list button on the Application toolbar .

If a URI is returned, bulleted_list_item_tag_name_ns function returns arr .

The function returns the null string if there isn't a isn't a namespace prefix for the tag, if no bulleted list item tag is designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

## Related Topics

- • Document type configuration files

- • Configuring tags as list elements

- • bulleted_list_item_tag_name function

- • bulleted_list_block_tag_name_ns function

- • set toolbar4 command



---

# caller

# caller

caller ([ level ])



This function returns the name of the function that called this routine. If the argument level is given, it specifies the number of call frames to go back before the current one to obtain the information. Use either caller() or caller(0) to return the name of the current function.

## Related Topics

- • caller_file function

- • caller_line function

- • package_name function



---

# caller_file

# caller_file

caller_file ([ level ])

This function returns the file name containing the statement that called this routine. If the argument level is given, it specifies the number of call frames to go back before the current function to obtain the file name of the calling function. For example, caller_file(1) returns the file name of the call to the active function, whose name is returned by caller(0) .

## Related Topics

- • caller function

- • caller_line function

- • package_name function



---

# caller_line

# caller_line

caller_line ([ level ])

This function returns the line number of the statement that called this routine. If the argument level is given, it specifies the number of call frames to go back before the current function to obtain the line number of the calling function. For example, caller_line(1) returns the line number of the call to the active function, whose name is returned by caller(0) .

The caller , caller_line and caller_file functions can be used to generate a function trace back of the active ACL stack frame.

Example

```
function show_callers()
{
local n = 0;
while (caller_line(n)) {
local c = caller(n);
if (c == "") {
c = "*top-level*";
}
eval "Caller[" . n . "] is " . c output=>*;
eval " at line", caller_line(n), "file", caller_file(n) output=>*
n++;
}
}
```

## Related Topics

- • caller function

- • caller_file function

- • package_name function



---

# caret_at

# caret_at

caret_at ([ doc ])

This function specifies the type of object preceding the cursor by returning one of the following strings: text , tag , equation , or, in the case of an empty file, null . The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

## Related Topics

- • mouse_at function



---

# caret_in_selection

# caret_in_selection

caret_in_selection ([ doc ])

This function returns 1 (true) if the caret is within the current selection of the document specified by doc , or the current document if doc is omitted. Returns 0 (false) if the caret is not within the selection, or if nothing is selected in the document identified by doc .

## Related Topics

- • mouse_in_selection function



---

# caret_show

# caret_show

caret_show ([ doc ])

If the caret is within a collapsed region, this function expands all parent elements so that the caret is visible. The function can be directed to operate on a specific document by supplying the optional doc parameter. If doc is omitted, then the current document is used. If the current view is a document map, the hierarchy will be expanded sufficient levels to display the element containing the text caret.



---

# catalog_ids

# catalog_ids

catalog_ids ( kword , arr [, regexp [, path ]])

This function returns all identifiers found in the catalog files specified by the path path for the specified keyword kword and match the regular expression specified by regexp . The number of entries found is returned.

The function has the following parameters:

- • kword — A string that is a keyword indicating the type of entries that should be matched.

- • arr — The name of the numerical array that contains the list of identifiers.

- • regexp — A string that is a regular expression for filtering the entries.

- • path — A string that is the catalog path to use.

Examples

```
# Find the public identifiers for DITA DTDs in the current catalog path.
local A[], cnt
cnt = catalog_ids("PUBLIC", A, "-//.*//DTD DITA")
# Find the universal resource identifiers for DITA schema modules in the current catalog path.
cnt = catalog_ids("URI", A, ":dita:.*:xsd:")
```

## Related Topics

- • Catalog files

- • Catalog path and file



---

# catalog_public_ids

# catalog_public_ids

catalog_public_ids ( regexp , arr [, path ])

This function fills the array arr with all the catalog entries in the specified catalog path list that match the regular expression regexp . The path parameter is optional; if it is not specified, the default catalog path is searched.

This function returns the number of entries found.

Example

```
local dtds[];
catalog_public_ids("-//.*//DTD", dtds,
main::ENV["APTCATPATH"]);
```

This example defines the dtds array, then fills the array with all the catalog entries that match the regular expression -//.*//DTD . This example searches the catalog path defined in the APTCATPATH environment variable.

## Related Topics

- • Catalog files

- • Catalog path and file

- • catalog_resolve function



---

# catalog_resolve

# catalog_resolve

catalog_resolve ( keyword [, p1 [, p2 [, p3 [, catalogpath ]]]])

This function is a general catalog lookup routine. The keyword argument specifies the catalog entry to search. The value of the p1 , p2 , and p3 parameters depends on the keyword specified. The following table describes the values for each of the valid keywords.

pubid is the public identifier and sysid is the system identifier.

The catalogpath argument specifies a list of directories to search for the catalog file. If it is not specified, Arbortext Editor searches the path list specified in the set catalogpath option, which is initialized by the APTCATPATH environment variable .

uri is the namespace URI.

When specifying the catalogpath argument, use null for trailing unused parameters. For example, catalog_resolve("SGMLDECL", "", "", "", catpath) .

The public_id_path(pubid, "", catpath) function is equivalent to catalog_resolve("PUBLIC", pubid, "", "", catpath) .

The dtd_decl_path(pubid, catpath) function is equivalent to catalog_resolve("DTDDECL", pubid, "", "", catpath) .

The entity_resolve(name, pubid, sysid, catpath) function is equivalent to catalog_resolve("ENTITY", name, pubid, sysid, catpath) .

The uri_resolve(uri, catpath) function is equivalent to catalog_resolve("URI", uri, "", "", catpath) .

## Related Topics

- • entity_resolve function

- • public_id_path function

- • dtd_decl_path function

- • catalog_public_ids function

- • path_public_ids function

- • Catalog Files

- • Catalog path and file



---

# catch

# catch

catch ( expr [, noerr ])

This function evaluates the expression expr and traps any run-time or parser errors resulting from evaluation of the expression. It also allows non-local exits from functions invoked by the expression using throw . If the optional argument noerr is specified and non-zero, then any error messages can be suppressed as with eval .

catch returns zero if the expression is evaluated without error. If there was an evaluation error, catch returns 1. If throw was executed during the evaluation of expr , catch returns the value of throw , which must be non-zero.

## Related Topics

- • eval built-in function

- • throw built-in function



---

# change_tracking_accept_change

# change_tracking_accept_change

ret = change_tracking_accept_change ( oid [, flags ])



This function attempts to accept a tracked change in the document and returns the status of the operation. The oid parameter specifies the location of the change markup. The flags parameter is a bit mask used to control the operation.

If oid is not valid change markup,then this function returns -1 . If accepting the change would cause an in-context document to become out of context and nocc bit is not 1 , a confirmation is displayed to allow the user to cancel the acceptance. If the user cancels the command then this function returns 0 . In either case this function does not modify the document. Otherwise, the change is successfully accepted and this function returns 1 .

The flag bit is:

- • 0x1 — nocc



---

# change_tracking_accept_selection

# change_tracking_accept_selection

ret = change_tracking_accept_selection ( isValid [, doc [, oid ]])



This function attempts to accept a tracked change in selected content in the document doc .

- • isValid — A value specifying how the function handles the change.

- • doc — Optional. The document in which to accept changes. If doc is omitted, the current document is used.

- • oid — Optional. If isValid is non-zero and oid is supplied, then oid is set to the change tracking markup that is available to be accepted.

## Related Topics

- • change_tracking_reject_selection



---

# change_tracking_find

# change_tracking_find

oid2 = change_tracking_find ( oid1 [, offset [, flags ]])



This function searches for change tracking markup, highlights it and returns the location in oid2 . It returns the null oid if no change tracking markup is found.

The first parameter, oid1 , is the starting location of the search. If null, the start of the current document is assumed, or the end if searching backward. The second parameter, offset , is the offset from oid1 within the following text. The search does not include the oid1 tag itself, even when the offset is zero.

The third parameter, flags , is a bit mask used to control the search. The possible flag bits are:

- • 0x1 — parent/child

- • 0x2 — reverse

- • 0x4 — no select

- • 0x8 — no message

By default, the search will move forward through the document and highlight any changes found. Wrapping is controlled by the wrapscan set option.

The parent/child bit, if set, causes the search to search the document or to recursively search children for change tracking markup.

The reverse bit reverses the direction of the search.

The no select bit is used to turn off the highlighting.

The no message bit is used so the function will not display a “not found” message. This does not affect the prompt for wrapping which is controlled by the set wrapprompt command.



---

# change_tracking_info

# change_tracking_info

cnt = change_tracking_info ( oid , array )



This function populates the array parameter with information about the change tracking markup at oid and returns the number of elements in the associative array. If the oid is not change tracking markup, then the function returns 0 .

The following fields may appear in the associative array:

- • type — The type of change markup (for example, “add”, “del”).

- • subtype — Subtype if present (for example, “text”).

- • user — ID of user who made the change (for example, “ref”) to be used with change_tracking_user_properties .

- • time — Time of change (expressed in seconds since 1/1/70) to be used with the function ctime .

- • visible — 1 if the current view setting shows this change. 0 otherwise.

- • unacceptable — A description of why attempting to accept this change would fail.

- • unrejectable — A description of why attempting to reject this change would fail.

- • nested — A message explaining that acceptance or rejection of this change would remove another change.



---

# change_tracking_reject_change

# change_tracking_reject_change

ret = change_tracking_reject_change ( oid [, flags ])



This function attempts to reject a tracked change in the document and returns the status of the operation. Rejecting the change is similar to undoing the change. The oid parameter specifies the location of the change markup. The flags parameter is a bit mask used to control the operation.

If oid is not valid change markup,then this function returns -1 . If there is a calling sequence error then this function returns -1 . If rejecting the change would cause an in-context document to become out of context and nocc bit is not 1 , a confirmation is displayed to allow the user to cancel the rejection. If the user cancels, then this function returns 0 . In either case this function does not modify the document. Otherwise, the change is successfully rejected and this function returns 1 .

The flag bit is:

- • 0x1 — nocc



---

# change_tracking_reject_selection

# change_tracking_reject_selection

ret = change_tracking_reject_selection ( isValid [, doc [, oid ]])



This function attempts to reject a tracked change in selected content in the document doc .

- • isValid — A value specifying how the function handles the change.

- • doc — Optional. The document in which to reject changes. If doc is omitted, the current document is used.

- • oid — Optional. If isValid is non-zero and oid is supplied, then oid is set to the change tracking markup that is available to be rejected.

## Related Topics

- • change_tracking_accept_selection



---

# change_tracking_user_list

# change_tracking_user_list

cnt = change_tracking_user_list ( array [, doc ])

This function populates the indexed array with the unique ids of all users in the user list for the document doc . If doc is omitted, all users in the internal user table will appear. The function returns the number of entries in the array.



---

# change_tracking_user_properties

# change_tracking_user_properties

cnt = change_tracking_user_properties ( user , array [, set ])



This function populates the associative array with the set of known properties for the user identified by the unique id user . If the optional set parameter is non-zero, the user is added to the internal table if needed, and the properties in the array are associated with that user in the internal user table.

The keys of the associative array of properties for a new user will include:

fullname — The user's full name.

Any key/value pair may be added.

The internal user table data for a given user is saved with any document that has change records created by that user at the time that the document is written out. A document's user table, including all user properties, is merged into the internal user table when that document is read in a future session.



---

# char_entity_names

# char_entity_names

char_entity_names ( arr [, doc ])

The char_entity_names function fills the array arr with an alphabetical list of character entity names which are valid in the current document type, returning the number of entities.

The first name is stored at index 1. The doc argument specifies the identifier of the document tree to be queried. If omitted or 0 , the current document is used.



---

# chop

# chop

chop ( varname [, len ])

This function removes the last len characters from the variable named by varname , which must be a scalar variable or an array element. The chop function returns the characters removed. If len is omitted, the default 1 is used, removing just the last character. This is useful for removing the trailing newline character returned by getline .

## Related Topics

- • getline built-in function



---

# chr

# chr

chr ( n )



This function returns a string of one character corresponding to the ASCII character number or Unicode character number n . This is the inverse of ord . For example, chr(65) is A , and chr(ord('X')) == 'X' .

## Related Topics

- • ord built-in function



---

# cjk_locale

# cjk_locale

cjk_locale ()



This function returns the following non-zero values if Arbortext Editor is running on a Chinese, Japanese or Korean (CJK) system locale:

It returns a 0 if Arbortext Editor is not running on a CJK system locale.

Execute the following command at the Arbortext Editor command line to determine the system locale:

```
eval cjk_locale()
```

## Related Topics

- • CJK support

- • getlocale function



---

# clear

# clear

layout::clear ([ doc ])



This function removes the atipl namespace declaration and all page layout markup from a document and returns the status of the operation. The doc parameter specifies the document to modify. The current document is assumed if this parameter is not specified.

If the document contains page layout markup and the operation fails, the function returns 0 and the namespace declaration is retained. If the operation succeeds, then the function returns 1 .

For more detailed information on the page layout elements and their attributes, see www.arbortext.com/namespace/pagelayout . Refer to the Programmer's Reference for more detailed information about line numbering applications.

## Related Topics

- • set pagelayoutmarkers

- • set protectpagelayout

- • layout::add function

- • linenum function

- • layout::apply function



---

# clear_stylesheet

# clear_stylesheet

clear_stylesheet ( path )

This function clears the stylesheet indicated by path from the compiled stylesheet cache. Arbortext Editor stores XSL stylesheets in this cache after they've been compiled during a publishing process. By storing these stylesheets, Arbortext Editor avoids having to recompile them during subsequent publishing runs.

You can obtain a list of paths using the list_stylesheets function . If path is not specified or is an empty string, all stylesheets are cleared from the cache.

As an example, if you edited an XSL stylesheet that had previously been used in a publishing run, you would use this function to clear out the stylesheet cache. The updated stylesheet would then be used during the next publishing.

## Related Topics

- • Stylesheet Overview



---

# close

# close

close ( fid )

This function closes the file or channel associated with the identifier fid , which must be a return value of a previous call to open , open_accept , open_connect , or open_listen . close returns 0 if the file was closed successfully, or -1 if the file wasn't closed successfully (such as trying to close an already closed file).

## Related Topics

- • open built-in function

- • open_accept built-in function

- • open_connect built-in function

- • open_listen built-in function



---

# cmd_exists

# cmd_exists

cmd_exists ( cmdname )

This function returns 1 (True) if the string specified by cmdname is a valid built-in command or a currently defined alias. For built-in commands, cmdname may specify an unambiguous initial substring or abbreviation. If the command or alias does not exist or is not valid, 0 is returned.



---

# cmd_key

# cmd_key

cmd_key ( alias [, keymap ])

This function returns the keyboard shortcut bound to the command alias specified by alias for the keyboard shortcut specified by keymap . The result is a string of the same form as the keyname argument for the map command (for example, Ctrl+Shift+A ) or key_cmd function.

keymap is the same as the window argument to map and is a window class (for example, edit , cmd , helpwin ), a window name as returned by the window_name function, or a user-defined keyboard shortcut identified by the prefix character @ (for example, cmd_key("FileSave", "@panel") ). If keymap is omitted, the keyboard shortcut associated with the current window is used.

The function returns a null string if alias is not bound to any keys in the specified keyboard shortcut .

## Related Topics

- • map command

- • show cmdkeys

- • key_cmd

- • Keyboard Shortcuts



---

# color_chooser

# color_chooser

color_chooser ( color )

This function displays a color selection dialog box and returns the user's choice of color. The null string is returned if the user selects Cancel . color specifies the initial color to edit and is either a named color or an RGB specification preceded by # .

Example

```
clr = color_chooser("#ff0000");
myred = color_chooser("red");
```

The look of the Color Chooser dialog box varies across platforms.



---

# color_rgb

# color_rgb

color_rgb ( color [, background ])

This function returns the RGB number of the color specified in the color parameter. The color parameter can be either a named color an RGB specification preceded by # . When the color parameter is set to a named color and the optional background parameter is set to 0 , the foreground color of the named color is returned. If background parameter is not set to 0 , the background color of the named color is returned.



---

# columnview_cell_focus

# columnview_cell_focus

columnview_cell_focus ([ window [, newcol ]])

This function enables you to change the focus from one Column view cell to a different cell.

The window parameter is the view for which you want to change the cell focus. If window is omitted or set to zero, the current window is used.

The newcol parameter is the column number of the cell that you want to assume the focus. Column zero is the Outline column. If a column number larger than the number of columns being displayed is given, the focus is moved to the last cell of the row. If newcol is omitted or set to a negative value, the cell focus is not changed.

The function returns the number of the column that currently has the focus. Column zero is the Outline column. A value of -1 indicates that the view specified by window is not a Column view or is otherwise invalid.



---

# columnview_is_defined

# columnview_is_defined

columnview_is_defined ([ doc ])

This function indicates whether Column view is defined in the document type configuration file ( .dcf ) for the indicated document.

The doc parameter is the document for which you are performing the check. If doc is omitted or set to zero, the current document is used.

The function returns 1 (true) if Column view is defined in the .dcf file or 0 (false) if Column view is not defined. A Column view does not need to be currently displayed for this function to return true.



---

# com_attach

# com_attach

handle = com_attach ( progID )

Returns a handle to a COM object which can be used to invoke a method or access a property on that object. The object must be released when it is no longer needed using com_release .

The progID parameter is either the ProgID or the CLSID of the COM object to attach to. A ProgID is the name registered for the COM object, such as Excel.Application . A CLSID is a character string starting with { represents the GUID that uniquely defines the object to attach to. If the COM object is not running, it will be started either as a separate process or by loading a DLL into the Arbortext Editor process as appropriate. If the COM object doesn't exist or can't be invoked, the function returns a zero ( 0 ).

Example

```
wordh = com_attach("Word.Application")
```

The above code returns a handle that could be used to invoke Microsoft Word.

## Related Topics

- • com_call function

- • com_prop_get function

- • com_prop_put function

- • com_release function



---

# com_call

# com_call

result = com_call ( handle , intname [, arg1 [, argn ]])

Invokes a method in a COM object previously attached to using com_attach or one returned by a method called previously.

The handle parameter is a handle returned by a call to com_attach or returned by a previous call to a COM method or property.

The intname parameter is a character string that gives the name of the method to be invoked.

All other parameters (if any) are passed to the method named by intname in the object specified by the object's handle . Each parameter will be converted to the type expected by the interface being invoked.

The return value will be converted to an appropriate ACL type before being used. If it is a COM interface, it will be converted into a handle to the interface which can be used in subsequent calls to com_call . The handle must be released using com_release when it is no longer needed.

Example

```
result = com_call(wordh, "Quit", -1)
```

invokes the Quit method in the COM object represented by wordh . If this is the handle returned by the example in com_attach , this will cause Microsoft Word to quit while saving open documents. The other two optional parameters to the Quit method are omitted.

## Related Topics

- • com_attach function

- • com_prop_get function

- • com_prop_put function

- • com_release function



---

# com_prop_get

# com_prop_get

result = com_prop_get ( handle , prop [, arg1 [, argn ]])

Retrieves the value of a property in a COM object previously attached to using com_attach or one returned by a method called previously.

The handle parameter is an object handle returned by a call to com_attach or returned by a previous call to a COM method or property.

The prop parameter is a character string that gives the name of the property to be obtained.

All other parameters (if any) are parameters for the property. If a property requires an extra parameter, it is most likely an index for an indexed property. Each parameter will be converted to the type expected by the interface being invoked.

The return value will be converted to an appropriate ACL type before being used. If it is a COM interface, it will be converted into a handle to the interface which can be used in subsequent calls to com_call . The handle must be released using com_release when no longer needed.

Example

```
docsh = com_prop_get(wordh, "Documents")
```

The above example gets a handle to the Documents collection assuming that wordh is the handle returned in the example for com_attach . This handle could then be used to open a document, and return a handle for it, using a call like the following:

```
doch = com_call(docsh, 'C:\Temp\Sample.DOC', 0, -1)
```

## Related Topics

- • com_attach function

- • com_call function

- • com_prop_put function

- • com_release function



---

# com_prop_put

# com_prop_put

result = com_prop_put ( handle , prop , newval [, arg1 [, argn ]])

Sets the value of a property in a COM object previously attached to using com_attach or one returned by a method called previously.

The handle parameter is a handle returned by a call to com_attach or returned by a previous call to a COM method or property.

The prop parameter is a character string that gives the name of the property to be set.

The newval parameter is the new value for the property.

All other parameters (if any) are parameters for the property. If a property requires an extra parameter, it is most likely an index for an indexed property. Each parameter will be converted to the type expected by the interface being invoked.

Setting a property doesn't normally return a value, but if it does, it will be converted to an appropriate ACL type before being used. If it is a COM interface, it will be converted into a handle to the interface which can be used in subsequent calls to com_call . The handle must be released using com_release when no longer needed.

Example

```
com_prop_put(doch, "DefaultTabStop", "36.5")
```

The previous example sets the default tab stop to 36.5 points. Note that when a parameter is a floating point number, you specify it as a string since ACL doesn't have full support for floating point numbers.

## Related Topics

- • com_attach function

- • com_call function

- • com_prop_get function

- • com_release function



---

# com_release

# com_release

result = com_release ( handle )

Releases a handle to a COM object which was previously obtained with com_attach or as the result of a call to com_call or com_prop_get . It is very important to release all COM handles when they are no longer needed since the COM server they are attached to will not exit properly if they are not released. Also, you should release all COM handles before you exit from Arbortext Editor .

The return value from com_release is 1 if it succeeded and 0 if it failed.

Example

```
com_release(wordh)
```

The example above releases the handle that was obtained in the example to com_call .

## Related Topics

- • com_attach function

- • com_call function

- • com_prop_get function

- • com_prop_put function



---

# compare_files

# compare_files

compare_files ( previous_file , current_file , result_file )

This function performs a comparison of two document files. The two files being compared are specified as the first two arguments. The third argument names the comparison results file that can be opened, displayed, and printed in Arbortext Editor .

The previous_file argument is the file name for one of the documents you want to compare. The current_file argument is the file name for the document that will be compared to previous_file .

The result_file argument is the file name you want to give to the comparison results document.

The return value from compare_files is 1 if it succeeded and there are differences in the two files. The return value is 0 if there are no differences in the files. The return value is -1 if it failed (for example, if an input file doesn't exist). If the return value is less than 1 , then a results document isn't created and an error message is stored in the variable main::ERROR .

## Related Topics

- • Document comparison overview

- • Comparing documents

- • Controlling the appearance of Compare results



---

# composer_log

# composer_log

composer_log ( destination , severity , verbosity )

The composer_log function sets the preferences for the Event Log file. Use this log file to troubleshoot publishing problems.

destination specifies the output destination for publishing events:

severity specifies the minimum severity of output events to generate:

verbosity indicates the amount of contextual information to generate in the log:

For example,

```
# Trace all possible publishing events to a file.
composer_log("c:\\temp\\event.log", $eventlog::SEVERITY_INFO, 2)
# Trace warnings and errors (but not informational events) to the
# java console and don’t include traceback information.
composer_log(0, $eventlog::SEVERITY_WARNING, 1);
# Trace only errors (but not warnings and informational events)
# to the event log.
composer_log(1, $eventlog::SEVERITY_ERROR);
```

## Related Topics

- • XSL stylesheet error handling during publishing

- • get_composer_log_doc function

- • get_composer_log_contents function

- • show_composer_log function



---

# content_model

# content_model

content_model ( tagname [, doc [, index ]])

This function returns the canonical form of the content model for the element specified by the expression tagname .

For example, a model declared to be

```
(a, (%ref;)+, d)
```

where the REF parameter entity is declared as

```
b|c
```

will be returned as

```
(a,(b|c)+,d)
```

content_model returns the null string if tagname is not an element declared in the DTD. The tagname may start with the end tag open character / (ETAGO).

The optional doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

Schemas can have no, one, or more than one content model. The optional index parameter lets you control the content model information returned.

- • Setting index to -1 — (The default.) Returns the global content model of the tagname in doc . If the element has no global content model, an empty string is returned.

- • Setting index to a value >=0 — Returns a global or local content model. However, the order of these models is undefined. You can enumerate through all content models by using 0 , 1 , 2 , ... until an empty string is returned (the signal to stop). (For a DTD, 0 and -1 always return the one and only content model and >=1 always return an empty string.)



---

# context_full_paths

# context_full_paths

context_full_paths ( arr , tag [, depth [, maxpaths [, oid [, pos ]]]])

This function fills the array arr with a list of possible context paths to make the target element tag in context at the point in the document given by oid, pos . If one of the paths returned is an empty string, tag can be inserted at the specified position without any elements being added.

If oid is omitted, the cursor position in the current document is used.

Depth specifies the maximum tag nesting depth of the paths returned. If depth is omitted, a depth of 5 is used.

Maxpaths specifies the maximum number of paths at each depth to return. It defaults to 50. If depth is 5, and maxpaths is 50, as many as 250 total paths could be returned. If more paths than maxpaths exist at a given depth , only the first maxpaths paths are returned, with no indication that more paths exist.

context_full_paths returns the number of paths stored in the array. Each path returned is expressed as a context string as formatted by the context_string function. The array is ordered by path depth, with the shallowest paths first.

This function adds required sibling elements to the paths returned. For example, if the content model for chapter is (title, para*) and the cursor is positioned just inside a chapter tag, then context_full_paths(arr,"para") will return "title()" . On the other hand, if the content model for chapter is (title*, para*), where the title is not required, then context_full_paths will return an empty string, because para is valid within chapter without any elements being added.

The siblings that are included do not add to the depth. For example, the following paths both have a depth of two:

```
"abstract("
"title()subtitle()abstract("
```



---

# context_paths

# context_paths

context_paths ( arr , tag [, depth [, oid [, pos ]]])

This function fills the array arr with a list of possible context paths of no more than depth tags to make the target element tag in context at the point in the document given by oid , pos . If oid is omitted, the cursor position in the current document is used. If depth is omitted, a depth of 5 is used.

context_paths returns the number of paths stored in the array. Each path returned is expressed as a context string as formatted by the context_string function. The array is ordered by path depth, with the shallowest paths first.

For compatibility with previous versions, each path returned starts with the enclosing tag at the cursor position or at the oid pos passed in. For example, if the cursor is just inside a chapter tag, then context_paths(arr,"para") will return an array of paths that start with "chapter(" . If that is not the desired result, use the context_full_paths function when writing new applications.

The context_paths function does not add required sibling elements to the paths returned. For example, if the content model for chapter is (title,para*) and the cursor is just inside a chapter tag, then context_paths(arr,"para") will return "chapter(" rather than "chapter(title()" . If you want required siblings to be added, use the context_full_paths function.



---

# context_string

# context_string

context_string ([ doc ])

This function returns a string describing the context of the cursor in the current window. This string consists of a list of element names and parentheses, such as:

```
doc(body(chapter(title()para0(title()para(
```

The left parenthesis following an element name represents a start tag, and the right parenthesis represents the end tag for the corresponding unmatched start tag. If the cursor is before the opening start tag or if context checking is not relevant for the current document, a null string will be returned.

The doc argument specifies the identifier of the document tree to be queried. If omitted or 0 , the current document is used.



---

# count

# count

count ( arr )

This function returns the number of elements in array arr .

## Related Topics

- • high_bound built-in function

- • low_bound built-in function



---

# create_copypaste_map

# create_copypaste_map

create_copypaste_map ( source , destination_path [, doc ])

This function creates a basic Arbortext Import/Export map template for a specified document source format and an XML document type. You can then use the Arbortext Import/Export MapTemplate Editor to customize that map for converting content of the given format to the XML markup for the document type. This map is used to convert source formats stored on the Microsoft Windows clipboard when copying and pasting text from other applications to Arbortext Editor .

The source parameter designates the document source format for which you want to generate the map template. The following values are supported:

- • rtf — Rich Text Format (RTF), the document format supported by several Microsoft applications including Microsoft Word

- • htm — HTML markup

- • mif — Maker Interchange Format (MIF), the document format supported by Adobe FrameMaker

- • txt — Unicode and 8-bit ANSI text

The destination_path parameter is the full path for the generated map template. To be recognized as a customized map for copy and paste conversion, the file must be named according to the following convention: source - doctypename .std , where source_type is the value of the source parameter and doctypename is the name of the specified document's document type. For example: rtf-axdocbook.std

The optional doc parameter designates the document for which you want to generate a map. If you do not supply a doc value, the current document is used.

The function returns 0 on success or an error code on failure. The following error code values are currently supported:

- • 1 — Could not write to map template file

- • 2 — Invalid source parameter value

- • 3 — Invalid doc ID

- • 4 — Invalid document type

## Related Topics

- • Copying and pasting text from other applications

- • Arbortext Import/Export Overview



---

# ctime

# ctime

ctime ( time [, gmt ])



This function converts the value time , as returned by time or file_mtime , into a string of the form produced by time_date . If the optional argument gmt is specified and non-zero, the time is returned in gmt . Otherwise, the time is given in the local time zone.

## Related Topics

- • file_mtime built-in function

- • time built-in function

- • time_date built-in function



---

# current_doc

# current_doc

current_doc ([ doc ])

This function returns the document identifier of the current document tree. If doc is given, this function sets the current document to the specified identifier and returns the previous value. Subsequent commands in the current execution context (either function or alias) will operate on this document tree. The doc argument must be a return value from a previous call to doc_open , window_doc , or oid_doc .

## Related Topics

- • doc_open built-in function

- • oid_doc function

- • window_doc built-in function

- • current_window window function



---

# current_event

# current_event

current_event ([ detail ])

This function returns information about the event that caused the command script containing this function call to be executed. The return value is one of the strings below. If the detail parameter is specified, additional details will be provided about the event.

- • key — a key is pressed. detail is the name of the key, for example, Ctrl+Shift+F3 .

- • toolbar — a toolbar button is pressed. detail is the name of the toolbar button, for example, Toolbar_Save .

- • mouse — a mouse button is pressed. detail is the name of the button, for example, Ctrl+M1 .

- • menu — a menu is selected. detail is the name of the menu item, for example, Save As... .

- • scroll — a scrollbar event is active. detail is null.

- • other — some other event is active. detail is null. Scripts are unlikely to get this return value.

- • none — no event is active. For example, the script is run outside of Windows mode. detail is null.

This function is useful to make a command behave differently depending on whether it is mapped to a key or menu.

## Related Topics

- • map command



---

# current_tag_attr_value

# current_tag_attr_value

current_tag_attr_value ( attr [, doc ])

This function returns the current, or local, value of the attribute named attr for the element markup preceding the cursor. If the markup is an end tag, then attribute values for the start tag are used. The doc argument specifies the identifier of the document tree to be queried. If omitted or 0 , the current document is used.



---

# current_tag_name

# current_tag_name

current_tag_name ([ doc ])

In the Edit view, this function returns the name of the tag to the left of the cursor. In the Document Map view, this function returns the name of the tag to the right of the cursor if the cursor is at the start of a line (that is, between the element icon and the element name); you can control this behavior with the set docmapcurrenttag=off option.

This is similar to the tagname variable except the current window is used. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

## Related Topics

- • set docmapcurrenttag command



---

# current_window

# current_window

current_window ([ window [, doc ]])

This function returns the window identifier of the active window associated with the document specified by doc , or the current document if doc is omitted or 0 .

If window is specified, this function sets the active window for the document to this window, and makes doc the current document. The keyboard focus remains in the same pane as the previous frame.

If no parameters are specified, current_window returns the window which has focus at the time the function is called. Specifying a parameter changes keyboard focus to the specified window for the frame containing that window. For example, you can determine which pane in a split window will get keyboard focus the next time the frame gets focus.

## Related Topics

- • current_doc window function



---

# cut_valid

# cut_valid

cut_valid ([ doc [, ignoreROFileEnt ]])

This function returns 1 (True) if the selected region can be cut without causing context errors. It returns 0 if the region is not balanced, is a protected region, or if context errors would result if the region was deleted. The doc argument specifies the identifier of the document owning the selection. If omitted or 0 , the current document is used.

If the ignoreROFileEnt argument is supplied and is not 0 , any unlocked file entities or XML inclusions that contain the selection will be ignored with respect to determining if the selection is protected.

Note, this function does not consider fix ups (such as adding required tags) when determining whether the cut will succeed.

## Related Topics

- • delete_markup_valid

- • oid_expose

- • oid_paste_valid

- • oid_show_attr



---

# dcf_option

# dcf_option

dcf_option ( attrname [, doc ])

This function returns the value from attributes on the Options element in the document type configuration file ( .dcf ). The attrname argument is the name of an attribute on the Options element (case is significant). The doc argument is an optional document identifier. The .dcf for the document type associated with doc is used for this function. If doc is not provided or set to zero, the current document is used.

The function returns the value of the given attribute or a null string. A null string is returned in the following cases:

- • The attribute has no assigned or default value.

- • The given attribute name is not a valid .dcf Options element attribute name.

- • The given document is not a valid document identifier.



---

# dcf_validate

# dcf_validate

dcf_validate ([ doc ])

This function reads the document type configuration file ( .dcf ) for the document type associated with doc , and checks that its contents are valid. It does not do a context check.

If doc is a .dcf file, then doc is verified. Otherwise, the .dcf file for the document type for doc is used. If doc is omitted or 0 , the current document is used.

This function returns:

Following is a list of errors that the dcf_validate function detects:

- • Graphic definition missing both entity and file name attributes.

- • Graphic definition with scaleToFit attribute set, but with either reproDepth or reproWidth missing.

- • Link definition missing both uri and idref attributes.

- • Target definition missing id attribute on an element without an attribute named "id".

- • ElementDisplay entry contains pair="end" for a singleton entry.

- • Icon entry contains invalid character set or character number.

Following is a list of warnings that the dcf_validate function detects:

- • Element name is not found in the target DTD.

- • Attribute name is not found on element in the target DTD.

- • Element name is duplicated in a InsertAroundToFix list.

- • Element name is duplicated in an element's Substitutions list.

- • Element name is duplicated in a Smart Insert Category list.

- • Substitution list or InsertAuto contents for an element is empty.

- • InsertAutoWithin section contains multiple InsertAutoCaret or InsertAutoSelection elements.

- • InsertAutoWithin section for a singleton element contains an InsertAutoSelection element.

- • ElementDisplay entry refers to an icon that is not declared.

- • Smart Insert list for a category is empty.

- • Allowed value is duplicated in a profile class.

- • Profile class has an empty allowed value.

- • InsertAuto content found for a table element (except when in a cell or caption).

- • InsertAutoCaret or InsertAutoSelection found in InsertAuto contents for a table cell element.

## Related Topics

- • Document type configuration files

- • Editing and validating .dcf files

- • doc_type_dcf_file function



---

# dcfmodel_element_list

# dcfmodel_element_list

dcfmodel_element_list ( arr , type [, doc [, dcfOnly ]])

This function returns the array arr with a list of elements designated as a given type in the document type configuration file ( .dcf ) for the document type associated with doc . The function also returns the number of entries in array arr . If doc is omitted or 0 , the current document is used.

If the document is using a Arbortext Styler stylesheet ( .style ), data on graphic, link, and link target types is obtained from the .style file rather than the .dcf file. If the document is not using a Arbortext Styler stylesheet, or if the dcfOnly parameter is set to 1 , all data is retrieved from the .dcf file.

Following are the valid type values that are sorted. (The primary element is returned first.)

- • bold

- • bulleted_list

- • graphic

- • italic

- • link

- • numbered_list

- • paragraph

- • target

- • underline

- • smallcaps

- • subscript

- • superscript

Following are the valid type values that are not sorted:

- • division

- • division_title

- • list_block

- • list_item

- • webcompose_boundary

## Related Topics

- • Document type configuration files

- • bulleted_list_block_tag_name function

- • numbered_list_block_tag_name function

- • text_style_tag_name function

- • dcf_validate function

- • doc_type_dcf_file function



---

# declare_char_entity

# declare_char_entity

declare_char_entity ( name [, text [, doc [, inEntity ]]])

This function allows you to declare a character entity with a specific replacement value.

name is the name of an existing file entity. A leading & is optional.

text is the replacement value for name , and is usually the name of a special character inside brackets. The text argument in aliases must be enclosed by quotes if brackets are used.

doc is the document identifier. By default, the current document is assumed.

inEntity signifies whether the declaration is within an entity. A non-zero value means the declaration is within an entity.



---

# declare_file_entity

# declare_file_entity

declare_file_entity ( name [, sysid [, pubid [, type [, doc [, confirmDtdOverride [, inEntity ]]]]]])

This function allows you to declare a file entity with a specific name.

name is the name of an existing file entity. A leading & is optional.

sysid is the new system identifier value (if there is one).

pubid is the new public identifier value (if there is one).

type is either empty, normal , or SUBDOC to declare the entity as a SUBDOC entity.

doc is the document identifier. By default the current document is assumed.

confirmDtdOverride prompts the user whether to override the DTD if the entity is already declared in the DTD. A non-zero value will prompt the user.

inEntity signifies whether the declaration is within an entity. A non-zero value means the declaration is within an entity.

## Related topic

modify_file_entity function



---

# declare_filep_entity

# declare_filep_entity

declare_filep_entity ( name [, sysid [, pubid [, doc [, inEntity ]]]])

This function adds a declaration for a file parameter entity (that is, an external file parameter entity) to the document's internal subset.

name is the name of the entity. A leading percent sign % is optional. If the entity hasn't already been declared, an error message is displayed.

sysid is the entity's system identifier.

pubid is the entity's public identifier.

doc is the document identifier. By default, the current document is assumed.

inEntity signifies whether the declaration is within an entity. A non-zero value means the declaration is within an entity.

For example, after the function call:

```
declare_filep_entity("myent", "/usr/myent")
```

the document's internal subset declaration will contain this:

```
<!ENTITY % myent SYSTEM "/usr/myent">
```

The declaration is added to the beginning of the subset.

## Related Topics

- • add_filep_entity function

- • insert_filep_entity function

- • delete_filep_entity function



---

# declare_graphic_entity

# declare_graphic_entity

declare_graphic_entity ( name [, notn [, sysid [, pubid [, doc [, confirmDtdOverride [, inEntity ]]]]]])

This function allows you to declare a graphic entity with a specific name and a specific notation.

name is the name of an existing graphic file entity. A leading & is optional.

notn is the name of the graphic entity's notation. A notation can associate a graphics application with a specific type of graphic file.

sysid is the new system identifier value (if there is one).

pubid is the new public identifier value (if there is one).

doc is the document identifier. By default the current document is assumed.

confirmDtdOverride prompts the user whether to override the DTD if the graphic entity is already declared in the DTD. A non-zero value will prompt the user.

inEntity signifies whether the declaration is within an entity. A non-zero value means the declaration is within an entity.

## Related topic

modify_graphic_entity function



---

# declare_notation

# declare_notation

declare_notation ( name [, sysid [, pubid [, doc [, confirmDtdOverride ]]]])

This function allows you to declare a notation with a specific name.

name is the name of an existing notation. A leading & is optional.

sysid is the new system identifier value (if there is one).

pubid is the new public identifier value (if there is one).

doc is the document identifier. By default the current document is assumed.

confirmDtdOverride prompts the user whether to override the DTD if the notation is already declared in the DTD. A non-zero value will prompt the user.



---

# declare_text_entity

# declare_text_entity

declare_text_entity ( name [, text [, type [, doc [, confirmDtdOverride [, inEntity ]]]]])

This function allows you to declare a text entity with a specific name and a specific replacement value.

name is the name of an existing text entity. A leading & is optional.

text is what replaces the entity reference in the formatted document.

type is either cdata to declare a CDATA entity, or an empty string .

doc is the document identifier. By default the current document is assumed.

confirmDtdOverride prompts the user whether to override the DTD if the graphic entity is already declared in the DTD. A non-zero value will prompt the user.

inEntity signifies whether the declaration is within an entity. A non-zero value means the declaration is within an entity.

## Related topic

modify_text_entity function



---

# defined

# defined

defined ( name )

This function returns 1 if the argument name is defined. This function may be used to test the existence of a scalar or array variable, array element, function or package name. For example:

```
defined($x) or defined("x")
```

returns 1 if x is a scalar or array variable,

```
defined("a[]")
```

returns 1 if a exists as an array variable,

```
defined($a[e1])
```

returns 1 if the expression (e1 in $a) is true,

```
defined("f()")
```

returns 1 if f is a defined function,

```
defined("p::")
```

returns 1 if p is a loaded package.

Variable and function names may be prefixed with a package name, for example,

```
defined(main::x)
defined("utils::f()")
```



---

# delete

# delete

delete ( name )

In this function, the argument name is a scalar or an array variable name or array element. If name is a scalar variable or array element, it is deleted and its value is returned. If name is an array variable, the contents of the array are deleted and the array name is removed from the symbol table. A null string is returned in this case. If the array name is a function formal parameter, then only the contents are deleted. This is useful for functions which take an array name as a parameter and fill it as a side effect. The argument to delete must not be a local variable or scalar function argument.

Example

```
val = delete(stack[p++])
```



---

# delete_filep_entity

# delete_filep_entity

delete_filep_entity ( name [, doc ])

This function pernits you to both remove a reference to a file parameter entity (external parameter entity) and undeclare it from the document’s internal subset.

name is the name for the entity. A leading percent sign (%) is optional.

doc is the document identifier. If doc is not supplied, the current document is assumed (default).

To ensure the file parameter’s declarations are removed from the document’s declaration. save the document then choose File > Revert to Saved .

## Related Topics

add_filep_entity function

declare_filep_entity function

insert_filep_entity function



---

# delete_markup_valid

# delete_markup_valid

delete_markup_valid ([ oid [, pos [, content ]]])

This function returns 1 if the markup identified by oid and pos can be deleted without context errors. It returns 0 if context errors would result if the markup was deleted.

All markup except included marked sections can be identified solely by oid . Both oid and pos must be given to specify an included marked section.

If oid is omitted, then oid_caret is used.

If content is given and non-zero, then this function returns 1 when no context errors would occur if both the markup and its content are deleted.

When testing whether markup can be deleted without context errors, this function will not do context transformations (such as tag substitutions, insert around to fix, insert required tags, remove redundant tags, and so on).



---

# detail_tag

# detail_tag

detail_tag ( tagname [, expand [, doc ]])

This function changes the detailing for all occurrences of the element named tagname in the document specified by doc . If doc is omitted or 0 , the current document is used.

The expand parameter, if given and non-zero, causes the element and its contents to be displayed. If expand is omitted or 0 , all occurrences of tagname are collapsed (detailed).

If tagname is a null string, detail_tag expands all elements in the document. In this case, the expand parameter is ignored.

## Related Topics

- • tag_display command

- • tag_display function

- • oid_expose function



---

# dimen_convert

# dimen_convert

dimen_convert ( dimen )

This function returns a string with dimen converted to inches. dimen must be a double-quoted string containing a number followed by a unit abbreviation. Valid abbreviations are: in (inches), cm (centimeters), mm (millimeters), pt (points), pi (picas), px (pixels), and pc (picas). dimen_convert returns a null string if dimen is not one of the valid abbreviations.

Examples:

- • dimen_convert("2cm") returns 0.79in

- • dimen_convert("25.5pc") returns 4.23in



---

# direction

# direction

direction ([ oid [, pos ]])

This function returns 1 if the location indicated by oid and pos has a right-to-left directionality . It returns -1 if the location indicated by oid and pos has a left-to-right directionality.

If oid is omitted, the function uses oid_caret .

If pos is omitted, the function assumes 0 .

If oid is invalid, the function returns 0 .



---

# dirname

# dirname

dirname ( path )



This function returns all but the last level of the path name in path . If path does not contain any path name components, the function returns the null string. dirname includes a trailing path separator as the last character of the string to permit easy construction of path names, for example,

Example

```
dirname(doc_path(doc)) . "test.sgm"
```

## Related Topics

- • basename built-in function



---

# disable_windows

# disable_windows

ret= disable_windows ( disable [, xid ])

Disables or re-enables user input from all windows (optionally skipping one window).

- • disable — Boolean. When true , user input from all windows is disabled. When false , user input is enabled.

- • xid — The native window system window handle (as would be returned by the function window_xid ) of a window to be skipped. If xid is omitted or invalid, all windows are affected by disable_windows .

The call disable_windows(1) is equivalent to set userinput=off , and disable_windows(0) is equivalent to set userinput=on .

## Related Topics

- • set userinput command



---

# dita_doc_show_rm_tab

# dita_doc_show_rm_tab

dita_doc_show_rm_tab ( tabID [, doc ])

This function displays the Resource Manager tab specified by the tabID parameter for the DITA document specified by the doc parameter. If no document is specified, the current document is used.

The following values are valid for the tabID parameter:

## Related Topics

- • DITA authoring overview

- • Resource Manager overview



---

# dita_rde_xsd_from_map

# dita_rde_xsd_from_map

dita_rde_xsd_from_map ( doc [, file ])

This function generates a resolved document for editing ( rdedit ) XML schema that includes all of the DITA topic document types referenced from the given DITA map. If the ditaincludemapsinrde preference is set to on , DITA map document types are also included.

The doc parameter is the DITA map to use as the basis of the new rdedit schema. The file parameter is the path to the location where you want to write the new schema. The function returns the full path to the generated file.

If file is a null string or omitted, a temporary rdedit schema is generated and will be deleted at the end of the current Arbortext Editor session.

## Related Topics

- • Working with DITA resolved documents

- • set ditaincludemapsinrde command

- • dita_rds_dtd_from_map function

- • flush_dita_rdgen_cache function

- • find_dita_rd_dcf function



---

# dita_rds_dtd_from_map

# dita_rds_dtd_from_map

dita_rds_dtd_from_map ( doc [, file ])

This function generates a resolved document for styling ( rdstyle ) DTD that includes all of the DITA maps and topic document types referenced from the given DITA map. The doc parameter is the DITA map to use as the basis of the new rdstyle DTD. The file parameter is the path to the location where you want to write the new DTD. The function returns the full path to the generated file.

If file is a null string or omitted, a temporary rdstyle DTD is generated and will be deleted at the end of the current Arbortext Editor session.

## Related Topics

- • Working with DITA resolved documents

- • dita_rde_xsd_from_map function

- • flush_dita_rdgen_cache function

- • find_dita_rd_dcf function



---

# dita_reset_rm_state

# dita_reset_rm_state

This function clears all persistent user preferences used to maintain or customize the Resource Manager state. The function also clears the current session’s Resource Manager navigation history.

## Related Topics

- • DITA authoring overview

- • Resource Manager overview



---

# dita_rm_export_favorites

# dita_rm_export_favorites

This function exports the current Resource Manager favorites list to the specified file . The function returns 1 on success or 0 on failure.

## Related Topics

- • DITA authoring overview

- • Resource Manager overview



---

# dita_rm_import_favorites

# dita_rm_import_favorites

This function imports a Resource Manager favorites list from the specified file . If the optional merge parameter is set to 0 , the current favorites list is replaced by the imported list. If merge is omitted or set to any non-zero value, the imported list is appended to the current list of favorites. In this case, any duplicate entries are not added to the list.

The function returns 1 on success or 0 on failure.

## Related Topics

- • DITA authoring overview

- • Resource Manager overview



---

# dita_show_rm_tab

# dita_show_rm_tab

This function displays the Resource Manager tab specified by the tabID parameter for the window specified by the window parameter. If no window is specified, the current window is used.

The following values are valid for the tabID parameter:

## Related Topics

- • DITA authoring overview

- • Resource Manager overview



---

# ditaref_relative_path

# ditaref_relative_path

newpath= ditaref_relative_path ( path [, doc ])

This function converts the absolute path name given by path into a relative path name if possible. If the file referenced by path is in or below the same directory as the document doc , a path name relative to the document directory is returned. If the file is located within a directory given by the ditapath Advanced Preference or set option, a path name relative to that directory is returned. Otherwise, the original input path name is returned.

If doc is zero or omitted, the current document is used.

This function is used by Arbortext Editor when storing file references in DITA documents.

## Related Topics

- • DITA authoring overview

- • set ditapath command



---

# ditaref_resolve

# ditaref_resolve

path= ditaref_resolve ( path , oid [, attrname ])

This function resolves a reference to content in a DITA document and returns the path where the referenced content is located.

- • The path parameter is the file path or file name you want to resolve. The value of path can be a file name, an absolute or relative path, a URI, or a Logical ID. If the value of path is a relative path, it is resolved against the following directories in this order:

- • The oid parameter specifies the context in which path should be resolved. The context includes any base URI associated with the oid and the document directory for the document that contains the oid .

- • The optional attrname parameter is the name of the attribute that contains the path value being resolved.

The returned path is the resolved path name and is usually an absolute path. If path is a relative path and cannot be resolved, the returned path is one of the following values:

- • The absolute path for path in the base URI directory, if one exists.

- • The absolute path for path in the document directory, if one exists.

- • The value of path , if there is no base URI or document directory.

- • An empty string, if oid_null() is used as the value of oid .

## Related Topics

- • set ditapath command

- • oid_null function

- • Symbolic parameters in path list variables

- • reference_path callback type



---

# division_heading_tag

# division_heading_tag

division_heading_tag ( tagname [, doc ])

This function returns 1 (true) if the tag specified by tagname is declared as a division heading in the .dcf file for the document type associated with doc . It returns 0 (false) if it isn't. If doc is omitted or 0 , the current document is used.

## Related topic

- • division_tag function



---

# division_tag

# division_tag

division_tag ( tagname [, doc [, primary ]])



This function returns 1 (true) if the tag specified by tagname is declared as a division in the document type configuration ( .dcf ) file for the document type associated with doc . If doc is omitted or 0 , the current document is used. If primary is specified and equal to 1 , the function returns 1 (true) only if the tagname is also declared as a primary division in the .dcf file.

## Related topic

- • Document type configuration files

- • division_heading_tag function



---

# dl_builtin_addr

# dl_builtin_addr

dl_builtin_addr ( fname )

This function returns the address of specified built-in Arbortext Editor function. This address may be passed to a dynamically loaded function with dl_call to allow such functions to call back into Arbortext Editor to request various services, in particular, to execute and evaluate ACL commands and expressions.

The parameter fname may be one of the following:

The function returns 0 if fname is not recognized.

The following is an example of some C functions that might be part of a dynamically loaded library.

```
typedef unsigned int (*CMDFUNC) (char * acl_string);
CMDFUNC acl_execp;
void set_acl_addr(void *addr)
{
acl_execp = (CMDFUNC) addr;
}
int aclcmd(char *str)
{
if (acl_execp)
return (*acl_execp)(str);
fprintf(stderr, "set_acl_addr() must be called first.\n");
return 0;
}
```

The interpreter address is passed to the library as follows:

```
local set_acl_addr = dl_find(hdll, "set_acl_addr");
dl_call(set_acl_addr, dl_builtin_addr("acl_exec"));
```

## Related Topics

- • dl_call function

- • eval function

- • exec function



---

# dl_call

# dl_call

dl_call ( ref [, arg1 [, argn ]])



This function calls a function in a dynamically loaded library. The ref parameter is a reference to a symbol returned by a previous call to dl_find . The remaining arguments, if any, are the parameters passed to the dynamically loaded function.

Numeric arguments are passed by value.

Strings are passed by reference. If the dynamic library being called expects 8-bit string parameters, dl_call will convert the string to 8-bit before it passes it to the library. If the library expects 16-bit Unicode strings, the string parameter is passed unchanged. Return values are not converted in this way. If necessary, the ACL code that called the library can use unpack to extract a string from a return value.

It is possible to pass a pointer to a C-style structure by using the pack function. See the example that follows.

The return value from dl_call is the value returned by the called function. If the return value is a scalar value, it may be used directly. If the return value is a pointer, then unpack must be used to convert the pointer into a string or extract parts of a structure.

The example that follows shows how to use unpack to unreference a pointer returned by a DLL function called with dl_call . In this case, the Windows API GetCommandLine , defined in kernel32.dll as "GetCommandLineA" — the ANSI version — returns a pointer to a null terminated string. unpack creates a copy of the string to be assigned to the variable cmdline so changing cmdline later does not affect the memory returned by GetCommandLine . Note that the return value is tested for null explicitly in this example, even though unpack can tolerate a null pointer and generate a null string.

```
dll = dl_load("kernel32")
hGetCommandLine = dl_find(dll, "GetCommandLineA")
ptr = dl_call(hGetCommandLine)
cmdline = ptr ? unpack("p", ptr) : ""
```

An example of passing a structure to a dynamically loaded function follows. In this case, the Windows API GetSystemTime is called, which takes a pointer to a SYSTEMTIME structure that has 8 fields of type WORD (short). The pack function creates this structure and unpack is used to convert the result into an array and to extract the member corresponding to the day of the week.

```
function GetDayOfWeek()
{
local dll = dl_load("kernel32")
if (!dll) {
response("Couldn't load kernel32")
return -1
}
local GetSystemTime = dl_find(dll, "GetSystemTime")
if (!GetSystemTime) {
response("Couldn't find GetSystemTime")
dl_unload(dll)
return -1
}
local timebuf = pack("s8")
dl_call(GetSystemTime, timebuf)
dl_unload(dll)
local systime[]
unpack("s8", timebuf, systime)
return systime[3]; # wDayOfWeek
}
```

Since only a single field of the structure is used, the unpack call in the above example could be written more simply as

```
return unpack("x4s", timebuf)
```

which would replace the last three lines of the function.

The following example calls the Windows API FindExecutable to find the executable associated with a specified file name:

```
function find_exe(file, dir="")
{
local dll = dl_load("shell32")
if (!dll) {
response("Couldn't load shell32")
return "";
}
local _FindExecutable = dl_find(dll, "FindExecutableA")
if (!_FindExecutable) {
response("Couldn't find FindExecutable")
dl_unload(dll)
return ""
}
local buf = pack("a255")
local h = dl_call(_FindExecutable, file, dir, buf)
dl_unload(dll)
if (h <= 32) {
response("FindExecutable failed, return " . n)
return ""
}
return unpack("A*", buf)
}
```

A sample call follows:

```
function shell_exe(filename, dir="")
{
local exename = find_exe(filename, dir)
if (exename != "") {
sh $exename $filename &; # launch program
}
}
```



---

# dl_error

# dl_error

dl_error ( )

This function returns an error message describing the reason the last call to dl_load , dl_find , or dl_unload failed. It returns null if the last call succeeded or if the system does not support an error message or code for failed dynamic load calls.

## Related Topics

- • dl_find built-in function

- • dl_load built-in function

- • dl_unload built-in function



---

# dl_find

# dl_find

dl_find ( h , symbol )

This function returns the address of the exported dynamic (shared) library function specified by symbol . The parameter h is the identifier of the dynamic library as returned by a previous call to dl_load . The address returned is an identifier that is passed to dl_call to actually invoke the function. dl_find returns 0 if the symbol cannot be found. The function dl_error , if supported by the operating system, may be called to obtain a message describing the reason for failure.

An example of an Arbortext Command Language interface to the Windows API GetProfileString follows.

```
function GetProfileString(section, key)
{
local dll = dl_load("kernel32")
if (!dll) {
response("Couldn't load kernel32")
return "";
}
local _GetProfileString = dl_find(dll, \
"GetProfileStringA")
if (!_GetProfileString) {
response("Couldn't find GetProfileStringA")
dl_unload(dll)
return ""
}
local buf = pack("a255"); # get a return buffer
dl_call(_GetProfileString, section, key, "", buf, 255)
dl_unload(dll)
return unpack("A*", buf); # trim trailing nulls
}
```

A sample call would be:

```
country = GetProfileString("Intl", "sCountry")
```

If this function is frequently called, or if other APIs from the same DLL are used, it would be better to load the DLL only once and remember the library identifier and function reference in global variables.

See dl_call for additional examples.

## Related Topics

- • dl_call built-in function

- • dl_error built-in function

- • dl_load built-in function



---

# dl_load

# dl_load

dl_load ( file [, world [, type ]])

This function loads the dynamic (or shared) library specified by the path name file . dl_load returns an identifier which can be used in subsequent calls to dl_find and dl_unload . It returns 0 if the library could not be loaded. The function dl_error can be used on some systems to retrieve a message describing the nature of the error.

The library identifier returned by dl_load can be passed to the function dl_find to get the address of a function in the dynamic library to be called using dl_call .

The optional parameter world is ignored except on Solaris systems where it allows the shared library to reference symbols that are part of Arbortext Editor (if set to one ( 1 ). If omitted, it defaults to zero ( 0 ).

The optional parameter type specifies whether the dynamic library expects 16-bit Unicode strings or 8-bit strings in parameters and return values. A type of one ( 1 ) specifies Unicode strings; zero ( 0 ) specifies 8-bit strings. If omitted, it defaults to zero ( 0 ).

dl_load is an interface to the Windows API LoadLibrary and follows the same rules if file does not specify a path name. Because Arbortext Editor is a Win32 executable, the DLL loaded by dl_load must also be a 32-bit library. As with standard Windows APIs, functions exported by the DLL must be declared with the "standard" calling convention, that is, using the keyword __stdcall .

See dl_find and dl_call for examples.

## Related Topics

- • dl_call built-in function

- • dl_error built-in function

- • dl_find built-in function

- • dl_unload built-in function



---

# dl_unload

# dl_unload

dl_unload ( h )

This function unloads the dynamic library specified by the identifier h , which is a return value from a previous call to dl_load . Any function references returned by dl_find for this library become invalid after dl_unload is executed. Note that the operating system normally uses a reference count to manage dynamically loaded libraries, so dl_unload may not actually unload the library. However, the handle h will no longer be valid after the call to dl_unload .

Example

```
dl_unload(hDll)
```

## Related Topics

- • dl_load built-in function



---

# dlgitem_activate

# dlgitem_activate

dlgitem_activate ( window , dlgitem )

Ensures that dlgitem is active when window is open. An active dialog item responds to user activity such as key strokes and mouse clicks.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Notes

Calling this function has the same effect as calling the dlgitem_set function on the ACTIVE attribute of the dialog item with a non-zero value.

Any necessary display updates will be scheduled but not necessarily completed when this functions returns.

Example

```
$ret = dlgitem_activate($win, "Salary")
```

Activates the Salary dialog item.



---

# dlgitem_collapse

# dlgitem_collapse

dlgitem_collapse ( window , dlgitem , listtag , row )

Collapses the list at the given point in the given list tag, within the dialog item dlgitem in window . If successful, this function returns a one (1). If the function fails, it returns a zero (0).

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The listtag parameter instructs the function to get the sublist for this list tag. The row parameter specifies which row of the sublist to collapse.

Notes

This function affects what is seen on the display; it has no effect on any data that is visible to the application.

Example

```
$top = dlgitem_get_listtag($win, "Hierarchy")
$ret = dlgitem_collapse($win, "Hierarchy", $top, 0)
```

Collapses the child of the first entry in the Hierarchy list.



---

# dlgitem_deactivate

# dlgitem_deactivate

dlgitem_deactivate ( window , dlgitem )

Ensures that dlgitem is not active when window is open. An inactive dialog item does not respond to user activity such as key strokes and mouse clicks. If dlgitem does not refer to a list dialog item or a list tag (in outline lists), $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Notes

Calling this function has the same effect as calling the dlgitem_set function on the ACTIVE attribute of the dialog item with a zero (0) value.

Any necessary display updates will be scheduled but not necessarily completed when this functions returns.

Example

```
$ret = dlgitem_deactivate($win, "Salary")
```

Deactivates the Salary dialog item.



---

# dlgitem_display

# dlgitem_display

dlgitem_display ( window , dlgitem )

Ensures that the dlgitem is visible when window is open. This function is specifically useful on the toolbar, since it automatically invokes a re-display of the toolbar, shifting the other toolbar buttons to the right (if necessary) to create space for the button displayed (if the window is already open, you will see a momentary flash as this re-display takes place).

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Example

```
$ret = dlgitem_display($win, "Toolbar_Equation")
```

Shows the Equation toolbar button.



---

# dlgitem_dropdown_list

# dlgitem_dropdown_list

dlgitem_dropdown_list ( window , dlgitem )

This function accesses the dropdown lists in the Arbortext Editor toolbar. The window parameter is a window identifier and indicates in which window you want the dropdown list to be activated. dlgitem is the value of the control's id attribute. For example, the following command would activate the Insert Markup dropdown list.

```
$ret = dlgitem_dropdown_list(current_window(), \
"Toolbar_InsertMarkupDrop")
```

The function returns a one ( 1 ) on success and returns a zero ( 0 ) if the dlgitem was not found or is not a dropdown list.

The following is a list of the available dropdown lists and the values for dlgitem that will activate them.



---

# dlgitem_ensure_listtag_visible

# dlgitem_ensure_listtag_visible

dlgitem_ensure_listtag_visible ( window , dlgitem , listtag )

Instructs Arbortext Editor to scroll the tree control specified by dlgitem so that the treenode listtag is visible.

- • window — The window identifier of the window containing the tree.

- • dlgitem — The value of the tree control's id attribute.

- • listtag — The list tag for which the function returns the sublist.

If listtag refers to a valid list tag, 1 is returned. Otherwise, the function returns 0 .



---

# dlgitem_ensure_table_visible_at

# dlgitem_ensure_table_visible_at

dlgitem_ensure_table_visible_at ( window , dlgitem , row )

Instructs Arbortext Editor to scroll the window so that the row row is displayed.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • row — The 1–based index of the row to be displayed.

If dlgitem does not refer to a table, or if row is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.



---

# dlgitem_exists

# dlgitem_exists

dlgitem_exists ( window , dlgitem )

If the specified control exists in the window, the function returns 1 . Otherwise, dlgitem_exists returns 0 .

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.



---

# dlgitem_expand

# dlgitem_expand

dlgitem_expand ( window , dlgitem , listtag , row )

Expands the list at the given point in the given list tag (in outline lists), within the dialog item dlgitem in window . If successful, this function returns a one (1). If the function fails, it returns a zero (0).

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The listtag parameter instructs the function to get the sublist for this list tag. The row parameter specifies which row of the sublist to expand.

The EXPAND callback will be called to request more rows.

Example

```
$top = dlgitem_get_listtag($win, "Hierarchy")
$ret = dlgitem_expand($win, "Hierarchy", $top, 0)
```

Expands the child of the first entry in the Hierarchy list.



---

# dlgitem_find_table_cell_in_column

# dlgitem_find_table_cell_in_column

dlgitem_find_table_cell_in_column ( window , dlgitem , column , text )

Searches a column in a table for the cell containing text .

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • column — The 1–based index of the column to search.

- • text — The content to search for.

If dlgitem does not refer to a table, or if column is illegal, $ERROR is set and -1 is returned. If no cell in the column contains text , 0 is returned. Otherwise, the 1–based index of the first row containing text is returned.



---

# dlgitem_get

# dlgitem_get

dlgitem_get ( window , dlgitem , attribute )

Returns the value of attribute for dlgitem within window as a string.

- • window — A window identifier.

- • dlgitem — The value of the control's id attribute.

- • attribute — The attribute to get. For a list of attributes, refer to dlgitem_set .

If window is invalid, or if dlgitem does not exist within window, then $ERROR is set and NULL is returned.



---

# dlgitem_get_active_at

# dlgitem_get_active_at

dlgitem_get_active_at ( window , listtag , row )

Returns active state of the specific outline list entry row in the outline list listtag in window . If listtag does not refer to an outline list list tag, $ERROR is set and 0 is returned. Otherwise, the active state is returned (0 = not active, 1 = active).

- • window — The window identifier.

- • listtag — An outline list list tag (case sensitive).

- • row — An offset into listtag (starting from one).

Example

```
$ret = dlgitem_get_active_at($win, "Hierarchy", 3)
```

Gets the active state of the third item in the outline list item Hierarchy .



---

# dlgitem_get_all

# dlgitem_get_all

dlgitem_get_all ( window , attribute , array )

Fills array , an associative array, with the value of the attribute for all of the dialog items in window . If a particular dialog item does not have the attribute, no entry is made in the array. If no dialog items have the attribute, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. The attribute parameter specifies the attribute to get. The values parameter specifies the associative array to fill.

Example

```
$ret = dlgitem_get_all($win, "VALUE", $Values)
```

Returns the following array:

```
$Values["NameField"]: "Jeff"
$Values["AgeField"]:	"35"
$Values["StateField"]:	"MD"
```



---

# dlgitem_get_appdata

# dlgitem_get_appdata

dlgitem_get_appdata ( window , dlgitem )

Returns the application-specific data associated with dialog item dlgitem in window . If successful, the function returns the application-specific data associated with the desired dlgitem . If there is no application-specific data for the desired dlgitem , the routine returns a NULL. If dlgitem does not refer to a list dialog item or a list tag (in outline lists), $ERROR is set and 0 is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Example

```
$ret = dlgitem_get_appdata($win, "Hierarchy")
```

Returns the string "TopOne" when used in conjunction with the sample code for dlgitem_set_appdata .



---

# dlgitem_get_appdata_at

# dlgitem_get_appdata_at

dlgitem_get_appdata_at ( window , listtag , row )

Returns the user-defined data associated with the list entry row in the outline list listtag in window . If dlgitem contains no list or row is out of range of the list, the function returns an empty string. If the function fails, it returns a NULL.

The window parameter is a window identifier. The listtag parameter is an outline list list tag (case sensitive). The row parameter is an offset into listtag (starting from one).

Example

```
$ret = dlgitem_get_appdata_at($win, "Hierarchy", 3)
```

Gets the user-defined data associated with the third item in the outline list item Hierarchy .



---

# dlgitem_get_background_at

# dlgitem_get_background_at

dlgitem_get_background_at ( window , listtag , row )

Returns the background color for the outline list tag identified by listtag in window . If listtag does not refer to an outline list tag, $ERROR is set and 0 is returned. If no color is specified at that location, an empty string is returned. Otherwise, a named color or an RGB specification preceded by # is returned.

## Related Topics

- • dlgitem_get_foreground_at function

- • dlgitem_set_background_at function

- • Using shading for profiled elements



---

# dlgitem_get_check_at

# dlgitem_get_check_at

dlgitem_get_check_at ( window , listtag , row )

Returns the check state of the specific checkable outline list entry row in the checkable outline list listtag in window . If listtag does not refer to a checkable outline list list tag, $ERROR is set and 0 is returned. Otherwise, the check state is returned.

Possible return values:

- • 0 — list entry is not checked.

- • 1 — list entry is checked.

- • –1 — list entry contains intermediate check. This results when a list entry contains a sublisttag with some list entries checked, but not all.

The window parameter is a window identifier. The listtag parameter is a checkable outline list list tag (case sensitive). The row parameter is an offset into listtag (starting from one).

Example

```
$ret = dlgitem_get_check_at($win, "Hierarchy", 3)
```

Returns the check state of the third item in the checkable outline list item Hierarchy .



---

# dlgitem_get_focus

# dlgitem_get_focus

ret = dlgitem_get_focus ( win )

Returns the tag name of the dialog item (case sensitive) that has keyboard focus for the window specified by win . If win is invalid, or if the keyboard focus has not been set for the window, then $ERROR is set and the empty string ( "" ) is returned.

The win parameter is a window identifier.

Example

```
focused_item = dlgitem_get_focus($win)
```

## Related Topics

- • dlgitem_set_focus function



---

# dlgitem_get_foreground_at

# dlgitem_get_foreground_at

dlgitem_get_foreground_at ( window , listtag , row )

Returns the foreground color for the outline list tag identified by listtag in window . If listtag does not refer to an outline list tag, $ERROR is set and 0 is returned. If no color is specified at that location, an empty string is returned. Otherwise, a named color or an RGB specification preceded by # is returned.

## Related Topics

- • dlgitem_get_background_at function

- • dlgitem_set_foreground_at function

- • Using shading for profiled elements



---

# dlgitem_get_list_array

# dlgitem_get_list_array

dlgitem_get_list_array ( window , dlgitem , array )

Returns the entire list of values in the list dialog item or list tag (in outline lists) identified by dlgitem in window . If dlgitem does not refer to a list dialog item or a list tag (in outline lists), $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The array parameter specifies the array for the returned values.

To gather only the selected items in a dialog list item, use the dlgitem_get_select_array function.

Example

```
$ret = dlgitem_get_list_array($win, "Foliage", $Trees)
```

Gathers all the values in the Foliage dialog list item and places them in the array $Trees .

## Related Topics

- • dlgitem_get_select_array function



---

# dlgitem_get_list_at

# dlgitem_get_list_at

dlgitem_get_list_at ( window , dlgitem , index )

Returns the value at index in the list of values in the list dialog item or list tag (in outline lists) identified by dlgitem in window . If index is invalid or if dlgitem does not refer to a dialog item or list tag (in outline lists), $ERROR is set and NULL is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The index parameter specifies the index into list on dlgitem .

Example

```
$ret = dlgitem_get_list_at($win, "Languages", 1)
```

Returns the string "C" for the list used in the sample code for dlgitem_set_list_at .



---

# dlgitem_get_list_count

# dlgitem_get_list_count

dlgitem_get_list_count ( window , dlgitem )

Returns the number of items in the list associated with dlgitem in window . Returns (-1) if the item does not have an associated list; dlgitem may also refer to a list tag (in outline lists).

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Notes

Calling this function has the same effect as calling the dlgitem_get function on the LIST_COUNT attribute of the dialog item.

When used on the root of an outline list item, returns the count of the top-level list tag of the list.

Example

```
$ret = dlgitem_get_list_count($win, "Children")
```

Returns the number of items in the Children dialog item.



---

# dlgitem_get_listtag

# dlgitem_get_listtag

dlgitem_get_listtag ( window , dlgitem )

Returns the top-level list tag (in outline lists) for the dialog item, or sets $ERROR and returns NULL.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Notes

If the dialog item is an outline list item but has no list tag, a list tag will be created and returned.

Example

```
$ret = dlgitem_get_listtag($win, "Hierarchy")
```

Obtains the list tag of the dialog item named Hierarchy.



---

# dlgitem_get_listtag_by_appdata

# dlgitem_get_listtag_by_appdata

dlgitem_get_listtag_by_appdata ( window , dlgitem , appdata )

Searches the tree specified by dlgitem and returns the list tag (in outline lists) of the tree node whose application-specific appdata is the same as the appdata specified in the function call.

- • window — The window identifier of the window containing the tree.

- • dlgitem — The value of the control's id attribute.

- • appdata — The appdata attribute of a tree node.



---

# dlgitem_get_mnemonic

# dlgitem_get_mnemonic

dlgitem_get_mnemonic ( win , dlgitem )

Returns the letter that is the mnemonic for the dialog item specified by dlgitem in the window specified by win . If win or dlgitem are invalid, then $ERROR is set and the empty string ( "" ) is returned. If the specified dlgitem has no mnemonic, the empty string ( "" ) is returned.

The win parameter is a window identifier. dlgitem is the value of the control's id attribute.

Example

```
mnem_letter = dlgitem_get_mnemonic($win, "matchMarkup")
```

## Related Topics

- • dlgitem_set_mnemonic function



---

# dlgitem_get_select_array

# dlgitem_get_select_array

dlgitem_get_select_array ( window , dlgitem , array )

Returns an array of selected values in the list dialog item or list tag (in outline lists) identified by dlgitem in window . If dlgitem does not refer to a list dialog item or a list tag (in outline lists), $ERROR is set and 0 is returned. Otherwise, 1 is returned.

- • window — A window identifier.

- • dlgitem — The value of the control's id attribute.

- • array — Specifies the array for the returned values. If a XUI tree control is in single selection mode, the array will be populated with one entry — the list tag of the only selected tree node. If the tree control is in multiple selection mode, the array will be populated with the list tags of all selected nodes in the tree control.

To gather all the items in a dialog list item, regardless of selection, use the dlgitem_get_list_array function.

Example

Consider a Trees list dialog list item containing the following tree names:

```
Oak
Maple
Gum
Gingko
Birch
Aspen
```

If a user selected the Oak and Gum list items, the following expression would gather the selected items and place them in an array called $SelectTrees .

```
$ret = dlgitem_get_select_array($win, "Trees", $SelectTrees)
```

The $SelectTrees array would contain the following values:

```
Values[1]: "Oak"
Values[2]: "Gum"
```

## Related Topics

- • dlgitem_get_list_array function



---

# dlgitem_get_selected_appdata

# dlgitem_get_selected_appdata

dlgitem_get_selected_appdata ( window , dlgitem )

Returns the user-defined data associated with item dlgitem in window . If dlgitem contains no selection or the selected item contains no data, the function returns an empty string. If the function fails, it returns a NULL.

With XUI tree controls, this function returns the application-specific data for the selected node when in single selection mode. When the tree control is in multiple selection mode, the function returns the application-specific data for the first node in the selection.

- • window — A window identifier.

- • dlgitem — The value of the control's id attribute.

Example

```
$top = dlgitem_get_selected_appdata($win, "Hierarchy")
```

Returns the selected item in the Hierarchy list.



---

# dlgitem_get_selected_listtag

# dlgitem_get_selected_listtag

dlgitem_get_selected_listtag ( window , dlgitem )

Returns the list tag of the selected tree node in the tree control specified by dlgitem when the tree control is in single selection mode. When the tree control is in multiple selection mode, it returns the list tag of the first selected tree node.

- • window — The window identifier of the window containing the tree.

- • dlgitem — The value of the control's id attribute.



---

# dlgitem_get_selected_listtag_array

# dlgitem_get_selected_listtag_array

dlgitem_get_selected_listtag_array ( window , dlgitem , array )

Returns an array containing the list tags of all selected nodes in the tree control specified by dlgitem . When the tree control is in single selection mode the array contains a single value — the list tag of the only selected node in the tree control. When the tree control is in multiple selection mode, the array contains the list tags of each selected node.

- • window — The window identifier of the window containing the tree.

- • dlgitem — The value of the control's id attribute.

- • array — The array of returned values.



---

# dlgitem_get_sublisttag

# dlgitem_get_sublisttag

dlgitem_get_sublisttag ( window , dlgitem , listtag , row [, nobranchconv ])

Returns the list tag of the sublist of the given list tag (in outline lists), or optionally inserts and returns a new, empty sublist as a child of the given row of the existing list tag within item dlgitem in window . If the function fails, it returns an empty string.

- • window — The window identifier.

- • dlgitem — The value of the control's id attribute.

- • listtag — The list tag for which the function returns the sublist.

- • row — Specifies which row of the sublist to return.

- • nobranchconv — Optional. If 1 , and the tree node specified is a leaf, the leaf will not be converted to a branch, allowing users to get the list tag of a leaf without changing anything. If nobranchconv is 0 , the leaf is converted to a branch. The default is 0

Example

```
$top = dlgitem_get_listtag($win, "Hierarchy")
$ret = dlgitem_get_sublisttag($win, "Hierarchy", $Top,0)
```

Returns the child of the first entry in the Hierarchy list.



---

# dlgitem_get_table_cell_at

# dlgitem_get_table_cell_at

dlgitem_get_table_cell_at ( window , dlgitem , row , column )

Returns the value in the cell specified by the intersection of row and column .

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • row — The 1 -based index of the row containing the cell.

- • column — The 1 -based index of the column containing the cell.

If dlgitem does not refer to a table, or if column or row are illegal values, $ERROR is set and NULL is returned. Otherwise, the value of the cell is returned.

## Related Topics

- • dlgitem_set_table_cell_at function



---

# dlgitem_get_table_column_align

# dlgitem_get_table_column_align

dlgitem_get_table_column_align ( window , dlgitem , column )

Returns the alignment information of the column specified by column .

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • column — The 1 -based index of the column. If the table has fewer columns that the value of column , the table is extended.

If dlgitem does not refer to a table, or if column is illegal, $ERROR is set and NULL is returned. Otherwise, the alignment value ( LEFT , RIGHT , or CENTER ) is returned.

## Related Topics

- • dlgitem_set_table_column_align function



---

# dlgitem_get_table_column_count

# dlgitem_get_table_column_count

dlgitem_get_table_column_count ( window , dlgitem )

Returns the number of columns in a table.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the table's id attribute.

If dlgitem does not refer to a table, $ERROR is set and -1 is returned. Otherwise, the number of columns in the table is returned.

## Related Topics

- • dlgitem_set_table_column_count function



---

# dlgitem_get_table_column_header_at

# dlgitem_get_table_column_header_at

dlgitem_get_table_column_header_at ( window , dlgitem , column )

Returns the header label of the column specified by column .

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • column — The 1 -based index of the column. If the table fewer columns than the value of column , the table is extended.

If dlgitem does not refer to a table, or if column is illegal, $ERROR is set and NULL is returned. Otherwise, the header label is returned.

## Related Topics

- • dlgitem_set_table_column_header_at function



---

# dlgitem_get_table_row_count

# dlgitem_get_table_row_count

dlgitem_get_table_row_count ( window , dlgitem )

Returns the number of rows in a table.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the table's id attribute.

If dlgitem does not refer to a table, $ERROR is set and -1 is returned. Otherwise, the number of rows in the table is returned.

## Related Topics

- • dlgitem_set_table_row_count function



---

# dlgitem_get_table_selection

# dlgitem_get_table_selection

dlgitem_get_table_selection ( window , dlgitem [, column ])

Returns the selected row when the selection type of the table control is row selection. If the selection type is cell selection, dlgitem_get_table_selection returns the row of the selected cell. The function returns -1 if the table does not exist. The function returns 0 if nothing is selected.

- • window — The window identifier of the window containing the table control.

- • dlgitem — The value of the table control id attribute.

- • column — If the table control’s selection type is cell selection, this output argument stores the column of the selected cell.

## Related Topics

- • dlgitem_set_table_selection function



---

# dlgitem_get_table_sort

# dlgitem_get_table_sort

dlgitem_get_table_sort ( window , dlgitem [, sortorder ])

Returns the index of the column on which the table is sorted.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • sortorder — The value of the sortorder is set by the function. It reflects the current sort order of the current sorted column. If the value of the sortorder is 0 , the column is sorted in ascending order. Otherwise, the column is sorted in descending order.

If dlgitem does not refer to a table, $ERROR is set and -1 is returned. If the table is not sorted, 0 is returned. Otherwise, the index of the column on which the table is sorted is returned.

## Related Topics

- • dlgitem_set_table_sort function



---

# dlgitem_get_value

# dlgitem_get_value

dlgitem_get_value ( window , dlgitem )

Returns the VALUE attribute of dlgitem within window as a string. If window is invalid, or if dlgitem does not exist within window, then $ERROR is set and NULL is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Examples

```
$ret = dlgitem_get_value($win, "TextField")
```

Notebooks can be queried. By using this function on a gpNotebook item, one can query which tab is active.

```
LINK_NOTEBOOK = "gpNotebookTagName"
# tab_value is an integer, which represents the position
# of the tabs by counting from left to right within
# the notebook.
function query_activate_tab(win) {
return dlgitem_get_value(win, LINK_NOTEBOOK)
}
```



---

# dlgitem_hide

# dlgitem_hide

dlgitem_hide ( window , dlgitem )

Ensures that dlgitem is not visible when window is open.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Notes

Calling this function has the same effect as calling the dlgitem_set function on the VISIBLE attribute of the dialog item with a zero (0) value.

Any necessary display updates will be scheduled but not necessarily completed when this functions returns.

Example

```
$ret = dlgitem_hide($win, "Salary")
```

Hides the Salary dialog item.



---

# dlgitem_insert_list_at

# dlgitem_insert_list_at

dlgitem_insert_list_at ( window , listtag , row , value )

For the location specified by listtag and row , performs one of the following actions:

- • Inserts a new tree node in a tree.

- • Inserts a new list item in a listbox or combobox.

- • Inserts a new row in a tablecontrol.

The label of the new node, list item, or row is specified by value .

- • window — The window identifier of the window containing the tree, listbox, combobox, or tablecontrol.

- • listtag — The list tag (identifier of the node) of the tree branch or the value of the control's id attribute.

- • row — The index of the tree node in the tree branch, list item in the list box or combobox, or row in the tablecontrol.

- • value — The string to insert.



---

# dlgitem_insert_table_column_at

# dlgitem_insert_table_column_at

dlgitem_insert_table_column_at ( window , dlgitem , column [, header ])

Inserts a new column in a table.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • column — The 1-based index of the new column. If the table has fewer columns than the value of column , the table is extended.

- • header — Optional. The header label of the new column.

If dlgitem does not refer to a table, or if column is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_remove_table_column_at function



---

# dlgitem_insert_table_row_at

# dlgitem_insert_table_row_at

dlgitem_insert_table_row_at ( window , dlgitem , row [, text ])

Inserts a new row in a table.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • row — The 1-based index of the new row. If the table has fewer rows than the value of row , the table is extended.

- • text — Optional. The content of the first column in the row.

If dlgitem does not refer to a table, or if row is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_remove_table_row_at function



---

# dlgitem_is_active

# dlgitem_is_active

dlgitem_is_active ( window , dlgitem )

This function tests whether the dlgitem in window is active/enabled or not. If the dlgitem is active/enabled, the function returns a one (1). If the dlgitem is inactive/disabled, the function returns a zero (0). If window is invalid, or if dlgitem does not exist within window , then the function returns -1.

Example

```
$ret = dlgitem_is_active($win, "TextField")
```



---

# dlgitem_is_expandable

# dlgitem_is_expandable

dlgitem_is_expandable ( window , dlgitem , listtag , row )

Returns 1 if the given list entry has a sublist, or 0 if it does not.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The listtag parameter instructs the function to get the sublist for this list tag. The row parameter specifies which row of the sublist to test.

Example

```
$top = dlgitem_get_listtag($win, "Hierarchy")
$ret = dlgitem_is_expandable($win, "Hierarchy", $top, 0)
```

Returns one (1) if the child of the first entry in the Hierarchy is expandable.



---

# dlgitem_is_expanded

# dlgitem_is_expanded

dlgitem_is_expanded ( window , listtag , row )

Returns true if the tree node (specified by listtag ) has children and the children are expanded. Otherwise, returns false .

- • window — The window identifier of the window containing the tree.

- • listtag — The list tag (identifier of the node) of the tree branch.

- • row — The index of the tree node in the tree branch.



---

# dlgitem_remove_list_at

# dlgitem_remove_list_at

dlgitem_remove_list_at ( window , listtag , row )

For the location specified by listtag and row , performs one of the following actions:

- • Removes a tree node in a tree.

- • Removes a list item in a listbox or combobox.

- • Removes a row in a tablecontrol.

The parameters have the following values:

- • window — The window identifier of the window containing the tree, listbox, combobox, or tablecontrol.

- • listtag — The list tag (identifier of the node) of the tree branch or the value of the control's id attribute.

- • row — The index of the tree node in the tree branch, list item in the list box or combobox, or row in the tablecontrol.



---

# dlgitem_remove_table_column_at

# dlgitem_remove_table_column_at

dlgitem_remove_table_column_at ( window , dlgitem , column )

Removes a column from a table.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • column — The 1–based index of the column to be removed.

If dlgitem does not refer to a table, or if column is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_insert_table_column_at function



---

# dlgitem_remove_table_row_at

# dlgitem_remove_table_row_at

dlgitem_remove_table_row_at ( window , dlgitem , row )

Removes a row from a table.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • row — The 1-based index of the row to be removed.

If dlgitem does not refer to a table, or if row is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_insert_table_row_at function



---

# dlgitem_remove_toolbar

# dlgitem_remove_toolbar

dlgitem_remove_toolbar ( window , dlgitem )

Turns off the display of the toolbar specified by dlgitem . If dlgitem does not refer to a toolbar, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.



---

# dlgitem_select_list_at

# dlgitem_select_list_at

dlgitem_select_list_at ( window , listtag , row )

For the location specified by listtag and row , performs one of the following actions:

- • Selects a list item in a list box or combo box.

- • Selects a row in a table control.

- • Selects a tree node in a tree. When the tree control is in single selection mode, the specified tree node will be set as the only selected node. When the tree control is in multiple selection mode, the specified tree node is added to the current selection; no nodes are unselected as a result of this call when a valid row is specified.

The parameters have the following values:

- • window — The window identifier of the window containing the tree, listbox, combobox, or tablecontrol.

- • listtag — The list tag (identifier of the node) of the tree branch or the value of the control's id attribute.

- • row — The index of the tree node in the tree branch, list item in the list box or combo box, or row in the table control.



---

# dlgitem_set

# dlgitem_set

dlgitem_set ( window , dlgitem , attribute [, value,... ])

Sets the value of the attribute named attribute of dlgitem to value . If window is invalid, if dlgitem does not exist within window , if attribute is not a valid attribute given the type of dlgitem , or if value is not valid given the type of attribute , then $ERROR is set and 0 is returned. If successful, the function returns a one ( 1 ).

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The attribute parameter(s) specifies the actual attribute(s) to set. The value parameters contain string data values for attributes.

Any necessary display updates will be scheduled but not necessarily completed when this functions returns.

Example

```
$ret = dlgitem_set($win, "TextField", VALUE,"Machu Pichu")
```



---

# dlgitem_set_active_at

# dlgitem_set_active_at

dlgitem_set_active_at ( window , listtag , row , activestatus )

Activates or deactivates the specific outline list entry row in the outline list listtag in window . If listtag does not refer to an outline list list tag, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. The listtag parameter is an outline list list tag (case sensitive). The row parameter is an offset into listtag (starting from one). The activestatus parameter sets the enabled/disabled status of the list entry (1=enabled; 0=disabled).

Example

```
$ret = dlgitem_set_active_at($win, "Hierarchy", 3, 0)
```

Deactivates the third item in the outline list item Hierarchy .



---

# dlgitem_set_appdata

# dlgitem_set_appdata

dlgitem_set_appdata ( window , dlgitem , appdata )

Associates application-specific appdata with the dialog item specified dlgitem in window . If dlgitem does not refer to a list dialog item or a list tag (in outline lists), $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The appdata parameter the string of application data to associate with the dialog item.

Notes

The application data is passed to dialog item and outline list expansion callbacks.

Example

```
$ret = dlgitem_set_appdata($win, "Hierarchy", "TopOne")
```

Sets the application data of dialog item Hierarchy to TopOne .



---

# dlgitem_set_appdata_at

# dlgitem_set_appdata_at

dlgitem_set_appdata_at ( window , listtag , row , appdata )

Associates application-specific appdata with the outline list entry row in the outline list listtag in window . If listtag does not refer to an outline list listtag, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. The listtag parameter is an outline list listtag (case sensitive). The row parameter is an offset into listtag (starting from one). The appdata parameter is the string of application data to associate with the list item.

Notes

The application data is passed to dialog item and outline list expansion callbacks.

Example

```
$ret = dlgitem_set_appdata_at($win, "Hierarchy", 3, "TopOne")
```

Sets the application data of the third item in the outline list item Hierarchy to TopOne .



---

# dlgitem_set_background_at

# dlgitem_set_background_at

dlgitem_set_background_at ( window , listtag , row , background )

Sets the background color for the outline list tag identified by listtag in window . If listtag does not refer to an outline list tag, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_set_foreground_at function

- • dlgitem_get_background_at function

- • Using shading for profiled elements



---

# dlgitem_set_check_at

# dlgitem_set_check_at

dlgitem_set_check_at ( window , listtag , row , checkstate )

Sets the check state of the specific checkable outline list entry row in the checkable outline list listtag in window . If listtag does not refer to a checkable outline list list tag, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. The listtag parameter is a checkable outline list listtag (case sensitive). The row parameter is an offset into listtag (starting from one). The checkstate parameter indicates the state the check box for the list entry should take. (0 indicates no check, 1 indicates a check).

Example

```
$ret = dlgitem_set_check_at($win, "Hierarchy", 3, 0)
```

Sets the check state for the third item in the checkable outline list item in Hierarchy to unchecked.



---

# dlgitem_set_default_branch_image

# dlgitem_set_default_branch_image

dlgitem_set_default_branch_image ( window , dlgitem , image )

Sets the image resource image as the image to be used for all list entries containing sublisttags that are in a collapsed state in an outline list dialog item dlgitem (unless overridden by a specific branch image setting for a particular listtag list entry) in window window .

The image appears at the front of all the list entries that contain sublisttags that are collapsed. image cannot be defined by a XUI <imagelist> element. It must be defined as a standalone <image> element.

Use dlgitem_set_default_branch_image to set the default image for list items that have children. If you were to create a file browser using an outline list, you may use a closed folder icon as your default branch image. If dlgitem does not refer to an outline list item, $ERROR is set and zero ( 0 ) is returned. Otherwise, one ( 1 ) is returned.

window is a window identifier. dlgitem is the value of the control's id attribute. image specifies the id attribute of an image element in the XUI file. The image is used to replace the image at the front of all list entries containing sublists for outline list item dlgitem .

For example,

```
ret = dlgitem_set_default_branch_image(win, "OutlistItem", "Folder")
```

sets the image for all list entries containing sublists and are collapsed in the outline list item OutlistItem to the Folder image.

## Related Topics

- • dlgitem_set_listtag_branch_image_at



---

# dlgitem_set_default_leaf_image

# dlgitem_set_default_leaf_image

dlgitem_set_default_leaf_image ( window , dlgitem , image )

Sets image as the default image to be used for all list entries that do not contain sublists in an outline list dialog item dlgitem (unless overridden by a specific leaf image setting for a particular listtag list entry) in window window . The image appears at the front of all the list entries that do not contain sublists. If you were to create a file browser using an outline list, you may use a file icon as a default leaf image. If dlgitem does not refer to an outline list item, $ERROR is set and zero ( 0 ) is returned. Otherwise, one ( 1 ) is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Example

```
ret = dlgitem_set_default_leaf_image(win, "OutlistItem", "File")
```

sets the image for all list entries that do not contain sublists in the outline list item OutlistItem to the File image.

## Related topic

- • dlgitem_set_listtag_leaf_image_at



---

# dlgitem_set_default_openbranch_image

# dlgitem_set_default_openbranch_image

dlgitem_set_default_openbranch_image ( window , dlgitem , image )

Sets image as the image to be used for all list entries containing sublisttags that are in an expanded state in an outline list dialog item dlgitem (unless overridden by a specific open branch image setting for a particular listtag list entry) in window window . The image appears at the front of all the list entries that contain sublisttags that are expanded. Use dlgitem_set_default_openbranch_image to set the default image for list items that have children and are expanded. If you were to create a file browser using an outline list, you may use a open folder icon as your default open branch image. If dlgitem does not refer to an outline list item, $ERROR is set and zero ( 0 ) is returned. Otherwise, one ( 1 ) is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Example:

```
ret = dlgitem_set_default_openbranch_image(win, "OutlistItem", "Openfolder")
```

This sets the image for all list entries containing sublists and that are expanded in the outline list item OutlistItem to the Openfolder image.

## Related topic

- • dlgitem_set_listtag_openbranch_image_at



---

# dlgitem_set_focus

# dlgitem_set_focus

dlgitem_set_focus ( win , dlgitem )

Changes the current keyboard focus of the window specified by win to the dialog item specified by dlgitem . If win is invalid, or if dlgitem does not exist within win , 0 is returned. If successful, the function returns 1 .

The win parameter is a window identifier. dlgitem is the value of the control's id attribute.

Note that this function also changes the default focus item for the window so that the next time the window is opened, the specified dlgitem will receive focus. If the window is already open, the current focus item will be unfocused and new item will be given focus.

Example

```
$ret = dlgitem_set_focus($win,"matchMarkup")
```

## Related Topics

- • dlgitem_get_focus function



---

# dlgitem_set_foreground_at

# dlgitem_set_foreground_at

dlgitem_set_foreground_at ( window , listtag , row , foreground )

Sets the foreground color for the outline list tag identified by listtag in window . If listtag does not refer to an outline list tag, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_set_background_at function

- • dlgitem_get_foreground_at function

- • Using shading for profiled elements



---

# dlgitem_set_list_array

# dlgitem_set_list_array

dlgitem_set_list_array ( window , dlgitem , values )

Sets the entire list of values in the list dialog item or list tag (in outline lists) identified by dlgitem in window . If dlgitem does not refer to a list dialog item or list tag, or if values is an associative array, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The values parameter specifies the non-associative array of values to assign.

Example

```
Values[1] = "Oak"
Values[2] = "Maple"
Values[3] = "Gum"
Values[4] = "Ginkgo"
Values[5] = "Birch"
Values[6] = "Aspen"
$ret = dlgitem_set_list_array($win, "Foliage", $Values)
```



---

# dlgitem_set_list_at

# dlgitem_set_list_at

dlgitem_set_list_at ( window , dlgitem , index , value )

Assigns a value to the list of values in the list dialog item or list tag (in outline lists) identified by dlgitem in window . If the list has insufficient entries to accommodate index , it is extended with empty strings. If dlgitem does not refer to a list dialog item or list tag, or if index is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The index parameter specifies the index into list on dlgitem . The value parameter specifies the actual value to assign.

Example

```
$ret = dlgitem_set_list_at($win, "Languages", 1, "C")
$ret = dlgitem_set_list_at($win, "Languages", 2, "C++")
```



---

# dlgitem_set_list_count

# dlgitem_set_list_count

dlgitem_set_list_count ( window , dlgitem , count )

Sets the number of items in the list associated with dlgitem in window to count . If successful, the function returns a one (1). Returns (-1) if the item does not have an associated list; dlgitem may also refer to a list tag (in outline lists).

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The count parameter is an item count

Notes

Calling this function has the same effect as calling the dlgitem_set function on the LIST_COUNT attribute of the dialog item. The list will be shortened or lengthened as needed.

When used on the root of an outline list item, sets the count of the top-level list tag of the list.

Example

```
$ret = dlgitem_set_list_count($win, "Cars", 3)
```

Sets the number of items in the Cars dialog item to 3.



---

# dlgitem_set_listtag_branch_image_at

# dlgitem_set_listtag_branch_image_at

dlgitem_set_listtag_branch_image_at ( window , listtag , row , image )

Associates image with the outline list entry row in the outline list listtag in window . The image appears at the front of the list item. Use this function when you want a specific branch listtag to appear with an image different from the default branch image. If you were to create a file browser using an outline list, you may use a closed folder icon as a default branch image, and a special icon for a locked folder. If listtag does not refer to an outline list listtag, $ERROR is set and zero ( 0 ) is returned. Otherwise, one ( 1 ) is returned.

The window parameter is a window identifier. The listtag parameter is an outline list list tag (case sensitive). The row parameter is an offset into listtag (starting from one).

Example

```
ret = dlgitem_set_listtag_branch_image_at(win, "Hierarchy", 3, "Lockedfolder")
```

This sets the image for the third item in the outline list item Hierarchy to the Lockedfolder image.

## Related topic

- • dlgitem_set_default_branch_image



---

# dlgitem_set_listtag_extra_image_at

# dlgitem_set_listtag_extra_image_at

dlgitem_set_listtag_extra_image_at ( window , listtag , row , image )

Associates image with the outline list entry row in the outline list listtag in window . The image appears at the front of the list item, just to the right of the leaf image set by the dlgitem_set_default_leaf_image function. If listtag does not refer to an outline list listtag, $ERROR is set and zero (0) is returned. Otherwise, one (1) is returned.

The window parameter is a window identifier. The listtag parameter is an outline list listtag (case sensitive). The row parameter is an offset into listtag (starting from one). The image parameter specifies the ACL Designer image resource to place at the front of the list item.

Example

```
ret = dlgitem_set_listtag_extra_image_at(win, "Hierarchy", 3, "Padlock")
```

sets the image for the third item in the outline list item Hierarchy to the Padlock image.

## Related topic

- • dlgitem_set_default_leaf_image



---

# dlgitem_set_listtag_leaf_image_at

# dlgitem_set_listtag_leaf_image_at

dlgitem_set_listtag_leaf_image_at ( window , listtag , row , image )

Associates an ACL Designer image resource image with the outline list entry row in the outline list listtag in window . The image appears at the front of the list item. Use this function when you want a specific listtag to appear with an image different from the default image. If you were to create a file browser using an outline list, you may use a file icon as a default leaf image for file leaves, and a special icon for graphic file leaves. If listtag does not refer to an outline list listtag, $ERROR is set and zero (0) is returned. Otherwise, one (1) is returned.

The window parameter is a window identifier. The listtag parameter is an outline list listtag (case sensitive). The row parameter is an offset into listtag (starting from one). The image parameter specifies the ACL Designer image resource to place at the front of the list item.

Example

```
ret = dlgitem_set_listtag_leaf_image_at(win, "Hierarchy", 3, "Graphic")
```

sets the image for the third item in the outline list item Hierarchy to the Graphic image.

## Related topic

- • dlgitem_set_default_leaf_image



---

# dlgitem_set_listtag_openbranch_image_at

# dlgitem_set_listtag_openbranch_image_at

dlgitem_set_listtag_openbranch_image_at ( window , listtag , row , image )

Associates an ACL Designer image resource image with the outline list entry row in the outline list listtag in window . The image appears at the front of the list item when it is expanded. Use this function when you want a specific expanded branch listtag to appear with an image different from the default image. If you were to create a file browser using an outline list, you may use a open folder icon as a default open branch image and a special icon for open branches with locked contents. If listtag does not refer to an outline list listtag, $ERROR is set and zero ( 0 ) is returned. Otherwise, one ( 1 ) is returned.

The window parameter is a window identifier. The listtag parameter is an outline list listtag (case sensitive). The row parameter is an offset into listtag (starting from one). The image parameter specifies the ACL Designer image resource to place at the front of the list item.

Example

```
ret = dlgitem_set_listtag_openbranch_image_at(win, \
"Hierarchy", 3, "OpenFolderLocked")
```

sets the image for the third item in the outline list item Hierarchy to the OpenFolderLocked image.

## Related topic

- • dlgitem_set_default_openbranch_image



---

# dlgitem_set_mnemonic

# dlgitem_set_mnemonic

dlgitem_set_mnemonic ( win , dlgitem , mnemonic )

Sets the mnemonic of the dialog item specified by dlgitem in the window specified by win to the letter specified by mnemonic . If win is invalid, or if dlgitem does not exist within win , 0 is returned. If successful, the function returns 1 .

The win parameter is a window identifier. dlgitem is the value of the control's id attribute. The mnemonic parameter is a letter to set as the mnemonic for the specified dialog item (lower case). In order for the mnemonic to be properly set on the dialog item, the letter mnemonic specified must occur in the label of the dialog item. To avoid conflicts with other dialog item mnemonics, you should set each dialog item in a given dialog to a unique mnemonic.

Example

```
$ret = dlgitem_set_mnemonic($win,"matchMarkup","r")
```

## Related Topics

- • dlgitem_get_mnemonic function



---

# dlgitem_set_multiple

# dlgitem_set_multiple

dlgitem_set_multiple ( window , attribute , values )

Sets the value of the attribute named attribute to multiple dlgitems within window , per the array in values . The values parameter is an associative array, indexed by the tag names of the dialog items within window , containing new values for the attribute. There need not be an entry in values for every dialog item in the window. It is an error for values to contain a tag name which does not correspond to a dlgitem , however. If an error occurs, $ERROR is set and 0 is returned. If successful, the function returns a one (1).

The window parameter is a window identifier. The attribute parameter specifies the attribute to set. The values parameter is an associative array of new values for dialog items.

Notes:

Assignment of values does not cease when an erroneous entry is detected.

Example

```
$Values["NameField"] = "Jeff"
$Values["AgeField"] = "35"
$Values["StateField"] = "MD"
$ret = dlgitem_set_multiple($win, "VALUE", Values)
```

Sets the following values: NameField dialog item to "Jeff", AgeField dialog item to "35", and StateField dialog item to "MD".



---

# dlgitem_set_refresh

# dlgitem_set_refresh

dlgitem_set_refresh ( window , dlgitem , refreshstatus )

Activates or deactivates the automatic refresh for outline list dlgitem in window . Turning off the refresh is good if you are executing a routine which would redraw the list several times (for example, fill the list, resort the list, etc.). If dlgitem does not refer to an outline list listtag, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The refreshstatus parameter sets the refresh/no refresh status of the list entry (1=refresh; 0=no-refresh).

Example

```
$ret = dlgitem_set_refresh($win, "Filelist", 0)
```

Deactivates automatic refresh for the outline list Filelist .



---

# dlgitem_set_selection

# dlgitem_set_selection

dlgitem_set_selection ( window , dlgitem , start [, end ])

If dlgitem is a outline list item in window, this function selects the entry row that has application data that matches either start or end (when supplied).

If dlgitem is a textbox control (or an editable combobox control) in window , dlgitem_set_selection highlights a range of text in the text field starting at position start and ending at position end . If end is not supplied, the highlighting continues to the end of the text. If start and end are the same, no text is highlighted and the cursor is placed at that position.

If dlgitem_set_selection is called with any other type of dialog box item, it returns 0 and sets $ERROR . Otherwise, the function returns 1 .



---

# dlgitem_set_table_cell_at

# dlgitem_set_table_cell_at

dlgitem_set_table_cell_at ( window , dlgitem , row , column , text )

Assigns a value to the cell specified by the intersection of row and column .

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • row — The 1-based index of the row containing the cell.

- • column — The 1-based index of the column containing the cell.

- • text — Specifies the value in the cell.

If dlgitem does not refer to a table, or if row or column are illegal values, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_get_table_cell_at function



---

# dlgitem_set_table_column_align

# dlgitem_set_table_column_align

dlgitem_set_table_column_align ( window , dlgitem , column , align )

Sets alignment information for the column specified by column .

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • column — The 1-based index of the column. If the table has fewer columns than the value of column , the table is extended.

- • align = LEFT | RIGHT | CENTER

If dlgitem does not refer to a table, or if column or align are illegal values, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_get_table_column_align function



---

# dlgitem_set_table_column_count

# dlgitem_set_table_column_count

dlgitem_set_table_column_count ( window , dlgitem , count )

Specifies the number of columns in the table.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • count — Specifies the number of columns in the table.

If dlgitem does not refer to a table, or if count is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_get_table_column_count function



---

# dlgitem_set_table_column_header_at

# dlgitem_set_table_column_header_at

dlgitem_set_table_column_header_at ( window , dlgitem , column , label )

Assigns a header label to the column specified by column .

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • column — The 1-based index of the column. If the table has fewer columns than the value of column , the table is extended.

- • label — The new header label of the column.

If dlgitem does not refer to a table, or if column is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_get_table_column_header_at function



---

# dlgitem_set_table_row_count

# dlgitem_set_table_row_count

dlgitem_set_table_row_count ( window , dlgitem , count )

Specifies the number of rows in the table.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • count — Specifies the number of rows in the table.

If dlgitem does not refer to a table, or if count is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_get_table_row_count function



---

# dlgitem_set_table_selection

# dlgitem_set_table_selection

dlgitem_set_table_selection ( window , dlgitem , row [, column ])

This function selects a row or a cell depending on the selection type of the table control. dlgitem_set_table_selection returns 0 if the operation failed. Otherwise, it returns 1 .

- • window — The window identifier of the window containing the table control.

- • dlgitem — The value of the table control id attribute.

- • row — The 1 -based index of the row containing the cell.

- • column — The 1 -based index of the column containing the cell. This value is only used when the table control’s selection type is cell selection.

## Related Topics

- • dlgitem_get_table_selection function



---

# dlgitem_set_table_sort

# dlgitem_set_table_sort

dlgitem_set_table_sort ( window , dlgitem , column [, sortorder ])

Specifies on which column the table is to be sorted.

- • window — The window identifier of the window containing the table.

- • dlgitem — The value of the control's id attribute.

- • column — The 1 -based index of the column on which the table is to be sorted. If column is set to 0 , the table will not be sorted.

- • sortorder — When 0 or omitted, the column specified in the function will be sorted in ascending order. Otherwise, the column will be sorted in descending order.

If dlgitem does not refer to a table, or if column is illegal, $ERROR is set and 0 is returned. Otherwise, 1 is returned.

## Related Topics

- • dlgitem_get_table_sort function



---

# dlgitem_set_value

# dlgitem_set_value

dlgitem_set_value ( window , dlgitem , value )

Sets the VALUE attribute of the dlgitem to value . If window is invalid, if dlgitem does not exist within window, or if value does not contain a value of the appropriate type, $ERROR is set and 0 is returned. If successful, the function returns a one ( 1 ).

- • window — The window identifier.

- • dlgitem — The value of the control's id attribute.

- • value — String data for the VALUE attribute.

Notes

Calling this function has the same effect as calling the dlgitem_set function on the VALUE attribute of the dialog item.

Examples

```
$ret = dlgitem_set_value($win, "TextField", "Machu Pichu")
```

This function can be used to set the active tab of a tabbox control.

```
LINK_NOTEBOOK = "id"
# tab_value is an integer, which represents the 1-based
# position of the tabs by counting from left to right
# within the notebook.
function activate_tab(win, tab_value) {
dlgitem_set_value(win, LINK_NOTEBOOK, tab_value)
}
```



---

# dlgitem_show

# dlgitem_show

dlgitem_show ( window , dlgitem )

Ensures that the dlgitem is visible when window is open.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Notes

Calling this function has the same effect as calling the dlgitem_set function on the VISIBLE attribute of the dialog item with a non-zero value.

Any necessary display updates will be scheduled but not necessarily completed when this functions returns.

Example

```
$ret = dlgitem_show($win, "Salary")
```

Shows the Salary dialog item.



---

# dlgitem_withdraw

# dlgitem_withdraw

dlgitem_withdraw ( window , dlgitem )

Ensures that the dlgitem is invisible when window is open. This function is specifically useful on the toolbar, since it automatically invokes a re-display of the toolbar, shifting the other toolbar buttons to the left to fill the space left by the button withdrawn (if the window is already open, you will see a momentary flash as this re-display takes place). If dlgitem does not refer to a list dialog item or a list tag (in outline lists), $ERROR is set and 0 is returned. Otherwise, 1 is returned.

The window parameter is a window identifier. dlgitem is the value of the control's id attribute.

Example

```
$ret = dlgitem_withdraw($win, "Toolbar_Equation")
```

Withdraws the Equation toolbar button.



---

# dobj_is_other_locked

# dobj_is_other_locked

dobj_is_other_locked ( dobj )

Returns a boolean value indicating whether the document object dobj is locked by another user. If dobj is locked by another user, the function returns 1 (one). If dobj is invalid, or is not locked by another user, the function returns 0 (zero).



---

# doc_cache_base

# doc_cache_base

doc_cache_base ( doc )

Call the doc_cache_base function to obtain the base file name that will be used to identify cache files when the document is formatted. If the optional parameter doc is omitted, the current document is used.

If this function were to return the path and base file name /tmp/aptcache/demo000/xyz , then the format command will produce formatting files using the base file name xyz . For example, formatting files would be named /tmp/aptcache/demo000/xyz.dvi , /tmp/aptcache/demo000/xyz.tex , and so on.

## Related Topics

- • Cache directory (.aptcache)

- • doc_cache_dir function



---

# doc_cache_dir

# doc_cache_dir

doc_cache_dir ( doc [, create ])

The doc_cache_dir function returns the path name of the cache directory associated with the document specified by doc . If no cache directory exists, it will be created if the create parameter is specified and is non-zero (True). If the create is not specified or is zero (False), then it returns the null string if the cache directory has not been created.

The cache directory is used by the formatter to store intermediate files.

## Related Topics

- • Cache directory (.aptcache)

- • doc_cache_base function



---

# doc_clean_cache

# doc_clean_cache

doc_clean_cache ( doc )

Use the doc_clean_cache function to remove the auxiliary publishing files stored in the Arbortext Editor cache directory for the document specified by doc . The doc parameter is the document identifier, as returned by the current_doc function. If you invoke this command from the Arbortext Editor command line without the doc parameter, doc_clean_cache applies to the document in the current Edit window.

Examples:

```
doc_clean_cache()
doc_clean_cache(current_doc())
doc_clean_cache(5)
```

## Related Topics

- • Cache directory (.aptcache)

- • Set option scope

- • clean_cache alias



---

# doc_clear

# doc_clear

doc_clear ( doc )

This function removes all the content from the document identified by doc leaving an empty document. It does not remove any entity declarations.

The operation cannot be undone.

## Related Topics

- • doc_close function

- • doc_save function



---

# doc_clone

# doc_clone

doc_clone ( doc [, flags [, viewchgtrk ]])

This function creates an independent copy of the document specified by the doc parameter. This function returns a document identifier that may be subsequently called by other functions.

The following flags can be set:

- • 0x01 — No content will be cloned. This will result in an empty document.

- • 0x02 — Resolve any change tracking markup according to the value of the set viewchangetracking option for the current view of the specified document. If there is no view setting associated with the specified document, this function uses the global value of set viewchangetracking . The set viewchangetracking values interacts with this function in the following ways:

- • 0x04 — Makes the empty document not inherit entity declarations from the source document. Applied only if 0x01 is also set.

- • 0x40 — The cloned document will have the same name as the source document.

Without 0x40 set, the cloned document will have no name. You can use the doc_dir function to obtain the path to the cloned document.

The optional viewchgtrk parameter can override the current setting of the set viewchangetracking option.



---

# doc_close

# doc_close

doc_close ( doc )

This function frees all memory used to represent the document tree identified by doc and marks the document identifier as invalid. You should not use the document specified by doc after you call this function. You cannot use doc to specify a command window document; for example, doc_close(window_doc("cmd")) is illegal. The function returns 1 on success, 0 on failure.

doc_close prompts you to save the document if the document is attached to an edit class window and has been modified. The doc_close function returns 0 if the user selects Cancel on the Save dialog box. To avoid a prompt in this case, a save or set modified=off command should be done before calling doc_close .

If doc specifies a document in a window not created by the window_create function , for example an auxiliary help window created by the help command , doc_close also removes the window. For example, doc_close(window_doc("helpwin2")) would free the document tree representing the contents of the helpwin2 window, and destroy the helpwin2 window.



---

# doc_compose_stylesheets

# doc_compose_stylesheets

doc_compose_stylesheets ([ doc ])

The doc_compose_stylesheets function returns 1 if publish dialog boxes for the document type associated with doc allow you to specify a stylesheet. The function returns a 0 if you can't specify stylesheets in the publish dialog boxes.

If doc is omitted or 0 , the current document is used.

## Related Topics

- • Document type configuration files



---

# doc_default_stylesheet_path

# doc_default_stylesheet_path

doc_default_stylesheet_path ([ use [, doc ]])

This function returns the full path and file name for the stylesheet that will be used by default for the given use and document doc . Valid values for use are:

- • 0 — Arbortext Editor

- • 1 — Print and PDF

- • 2 — HTML File

- • 3 — HTML Help

- • 4 — Web

- • 5 — RTF

If no document is specified, the doc parameter is the value of current_doc .

If, for example, you opened a document with the doc_open() function, and passed the 0x200 flag to not load a stylesheet, you could then use doc_default_stylesheet_path(0, doc) to determine which stylesheet would be used as the editing stylesheet if you were to pass the document to doc_show() .

The value returned does not reflect what stylesheets the document is currently set to use. It reflects what stylesheets would be used for the document if the document were opened in Arbortext Editor with no special application code. If use is 0 ( Arbortext Editor ), the stylesheet returned is determined by stylesheet association if one exists, or name and location. For example, by docname.style or doctype.style if such a file is found. For other uses, an empty string is returned unless there is a stylesheet association for the specified use.



---

# doc_delete_stylesheet_association

# doc_delete_stylesheet_association

doc_delete_stylesheet_association ( doc , i )

This function deletes the i th stylesheet association for document doc .

If doc is not a valid document identifier, or if there is no i th stylesheet association for doc , the function returns 0. Otherwise, it returns 1.



---

# doc_dir

# doc_dir

doc_dir ( doc )

This function returns the directory of the document specified by the doc parameter. If the optional doc parameter is omitted, the current document is assumed.

The doc_dir function can retrieve the document path to a cloned document using the document identifier returned by the doc_clone function .



---

# doc_dtd_not_defined

# doc_dtd_not_defined

doc_dtd_not_defined ([ doc ])

This function can be used to distinguish between the two instances in which the function doc_freeform returns 1 (True). If the document identified by doc is an XML instance without a DTD declaration, doc_dtd_not_defined returns 1 (True). If the document's declared DTD cannot be found, and the user has selected to edit in tagged mode without a DTD, this function will return 0 .

If doc_freeform returns 0 , doc_dtd_not_defined will also return 0 .

The doc argument specifies the identifier of the document to query. If omitted or 0 , the current document is used.

## Related Topics

- • doc_dtd_not_found function

- • doc_freeform function



---

# doc_dtd_not_found

# doc_dtd_not_found

doc_dtd_not_found ([ doc ])

This function can be used to distinguish between the two instances in which the function doc_freeform returns 1 (True). If the document identified by doc is an XML instance with a DTD declaration, but the DTD cannot be found, doc_dtd_not_found returns 1 (True).

If doc_freeform returns 0 , doc_dtd_not_found will also return 0 .

The doc argument specifies the identifier of the document to query. If omitted or 0 , the current document is used.

## Related Topics

- • doc_dtd_not_defined function

- • doc_freeform function



---

# doc_estimate_dfs

# doc_estimate_dfs

doc_estimate_dfs ([ doc ])

This function returns an estimate of the number of document fragments in a document.

Taking into consideration the overall size of the document, this value can help determine the setting for the set bigjobthreshold option . The doc__estimate_dfs function is also used when publishing to determine if content pipeline output should be written to disk rather than to memory. Refer to the description of the set bigjobthreshold option for details.

For more information on using Arbortext Publishing Engine for publishing, refer to the Programmer's Guide to Arbortext Publishing Engine , the Programmer's Reference , and the Content Pipeline Guide .

## Related topic

Using Arbortext Publishing Engine for publishing documents



---

# doc_first_dobj

# doc_first_dobj

doc_first_dobj ( doc )

Returns the first document object in the given document doc . If doc is not specified, the current document is used.



---

# doc_flatten

# doc_flatten

doc_flatten ( type , delete_declarations , doc )

This function flattens a file; substituting the contents of an entity reference with the actual content of the entity. You cannot undo this operation.

The type string specifies:

- • file — flattens file entities only.

- • text — flattens text entities only.

- • both — flattens both text and file entities.

- • include — flattens XIncludes only.

- • all — flattens all text and file entities as well as XIncludes.

- • conref — flattens DITA content references only.

You may specify more than one type by connecting the types with a plus sign ( + ). For example, the following value for type would flatten both XIncludes and DITA content references: include+conref .

delete_declaration is an optional boolean parameter that controls if the entity declarations should be removed from the document. 1 means remove the entity declarations, 0 means keep the entity declarations. The default is to keep the declarations. For example, if type is all , and delete_declaration is 1 , then all file and text entity declarations will be deleted.

doc is an optional document identifier. The default value is the current document.

## Related Topics

- • doc_flatten alias

- • write command



---

# doc_format_needed

# doc_format_needed

doc_format_needed ([ doc [, needed ]])

This function returns and optionally sets the format needed state of an open document as displayed in the status bar. If the needed parameter is specified, the state is set according to the following values:

- • 0 — Clears the format-needed status.

- • 1 — Sets the format-needed status.

- • 2 — Sets the reformat-needed status (when another formatting pass is required).

doc_format_needed returns the previous state. If the doc parameter is omitted or 0 , the current document is used.

## Related Topics

- • doc_formattable function



---

# doc_formattable

# doc_formattable

doc_formattable ([ doc ])

This function returns 1 (true) if the document specified by doc can be formatted for published output. It returns 0 for ASCII documents or FOSIs. In Arbortext Editor , it always returns 0.

If doc is omitted or 0, the current document is used.



---

# doc_freeform

# doc_freeform

doc_freeform ([ doc ])

This function checks whether a document is being edited in tagged mode without a DTD. This function returns 1 (True) if the document identified by doc is an XML instance without a DTD declaration. This function also returns 1 if the document's declared DTD declaration cannot be found and the user selected to edit in tagged mode without a DTD. For all other documents, this function returns 0 .

The doc argument specifies the identifier of the document to query. If omitted or 0 , the current document is used.

## Related Topics

- • doc_dtd_not_found function

- • doc_dtd_not_defined function



---

# doc_from_compare

# doc_from_compare

doc_from_compare ([ doc ])

This function determines whether a specified document was generated by a document comparison operation. The doc parameter is a document identifier.

The return value is 1 if the document was generated by a compare operation. The return value is 0 if it was not.

## Related Topics

- • Document comparison overview

- • Comparing documents

- • Controlling the appearance of Compare results



---

# doc_get

# doc_get

doc_get ( doc , attr )

This function returns the document scope value of the set option attr for the document identified by doc . If attr is a set option with a local scope other than document, or no local scope at all, it returns nothing.

Examples

```
doc_get(doc, "showiconsfulltags")
doc_get(doc, "textentityfontcolor")
```

## Related Topics

- • Set option scope

- • doc_set function

- • window_get function

- • current_doc function

- • option_scope function

- • set command



---

# doc_get_stylesheet_association

# doc_get_stylesheet_association

doc_get_stylesheet_association ( doc , i , params[] )

This function gets information about a stylesheet association. It returns data for the i th stylesheet association of document doc in associative array params where the keys of the array elements are href , type , title , media , charset , and alternate , corresponding to the attributes of the stylesheet processing instruction. The href element will contain a relative path name, an absolute path name, or an http://URL .

For example, the following ACL function would display the information for each existing stylesheet association for a document:

```
function show_ss_associations(doc = current_doc())
{
local n = doc_num_stylesheet_associations(doc);
if (n < 0)
{
response("Bad doc $doc passed to show_ss_associations from " . caller(1));
return 0;
}
local i;
eval "Stylesheet associations:" output=*
for (i=1; i <= n; ++i)
{
local params[];
if (!doc_get_stylesheet_association(doc, i, params))
{
response("Bad call to doc_get_stylesheet_association in " . caller());
return 0;
}
eval "href =", params["href"], " type =", params["type"], \
" title =", params["title"], \
" media =", params["media"], " character set =", params["charset"], \
" alternate =", params["alternate"] output=>*
}
return 1;
}
```

If doc is not a valid document identifier, or if there is no i th stylesheet association for doc , the function returns 0. Otherwise, it returns 1.

## Related Topics

- • Associating a stylesheet with your document

- • Stylesheet association processing instruction



---

# doc_get_translation_locale

# doc_get_translation_locale

doc_get_translation_locale ([ doc ])

Returns the translation locale of a specific document if the document is a translated version of another document. Otherwise, doc_get_translation_locale returns the empty string.

- • doc — (Optional). The identifier of the document for which the translation locale is returned. If doc is omitted or 0 , the current document is used.

## Related Topics

- • doc_set_translation_locale

- • doc_is_translation

- • doc_get_translation_orig_uri

- • doc_set_translation_orig_uri

- • Translation PI



---

# doc_get_translation_orig_uri

# doc_get_translation_orig_uri

doc_get_translation_orig_uri ([ doc ])

Returns the original URI value (if known) of the document for which a specific document is a translation. Otherwise, doc_get_translation_orig_uri returns the empty string.

- • doc — (Optional). The identifier of the document for which the URI is returned. If doc is omitted or 0 , the current document is used.

## Related Topics

- • doc_set_translation_locale

- • doc_get_translation_locale

- • doc_is_translation

- • doc_set_translation_orig_uri

- • Translation PI



---

# doc_has_change_tracking

# doc_has_change_tracking

ret = doc_has_change_tracking ([ doc ])



This function returns 1 only if change records are found in doc . If doc is not specified, the value of current_doc is used.



---

# doc_incomplete

# doc_incomplete

doc_incomplete ([ doc [, flags ]])

This function returns 1 (true) if the document specified by doc is currently marked incomplete. If the flags parameter is specified and non-zero, then a check_completeness command is run first to update the incomplete status.

The flags parameter is a bitmask that controls the options passed to the check_completeness command. It is constructed by using OR for the flags from the following list:

- • 1 — run the check_completeness command

- • 2 — do not insert missing required elements

- • 4 — generate error messages from the check_completeness command, including any parser error messages caused by the loading of required file entities, and display them in dialog windows as needed

- • 8 — generate error messages from the check_completeness command, but do not display them in a window

Note the following when working with doc_incomplete() :

- • If flags is omitted or 0 , the check_completeness command is not run.

- • If doc is omitted or 0 , the current document is used.

- • Running doc_incomplete() will only include checks for empty elements if this combination of settings exists:

## Related Topics

- • check_completeness command

- • set emptyelementswarnings



---

# doc_invalidate_graphics

# doc_invalidate_graphics

doc_invalidate_graphics ([ doc ])

This function resolves, reloads, and redraws (if displayed) all graphics in the document doc .

If doc is omitted or 0 , the current document is used.



---

# doc_is_translation

# doc_is_translation

doc_is_translation ([ doc ])

Determines whether a specific document is a translated version of another document, based on whether the Translation PI is present in the document.

- • doc — (Optional). The identifier of the document for which the translation status is checked. If doc is omitted or 0 , the current document is used.

## Related Topics

- • doc_get_translation_locale

- • doc_set_translation_locale

- • doc_get_translation_orig_uri

- • doc_set_translation_orig_uri



---

# doc_kind

# doc_kind

doc_kind ([ doc ])

This function returns a string indicating what “kind” of document is specified by doc . If the doc parameter is omitted, the current document is assumed. The possible return values are:

- • sgml — indicates an SGML document.

- • xml — indicates an XML document.

- • html — indicates an HTML document.

- • ascii — indicates an untagged ASCII document.



---

# doc_list

# doc_list

doc_list ( arr [, flags ])



This function fills the array arr with a list of all existing documents, returning the number of document identifiers stored in the array.

flags is a bitmask that specifies which document identifiers are returned. It is constructed by ORing the flags from the following list:

- • 1 — include command window documents

- • 2 — include paste buffers

- • 4 — include "textwin" documents, that is, documents associated with the built-in text windows helpwin[1-4] and msgwin[1-4] .

- • 16 — include file entity documents

- • 32 — include FOSI documents

- • 64 — include top level documents that use a DTD and are not file entities or paste buffers.

- • 128 — include documents that use a built-in document type, such as ascii or help , which is not matched by any of the flags specified above (that is, does not include documents matched by bits 1, 2, 4, and 8).

If flags is omitted or 0 , then all documents are returned as if all bits were specified.



---

# doc_name

# doc_name

doc_name ( doc )



This function returns the name associated with the document given by doc , or the null string if the document was created without a name argument specified.



---

# doc_namecase_sensitive

# doc_namecase_sensitive

doc_namecase_sensitive ( doc )

This function determines if the given document is case sensitive when dealing with markup. The function returns a one ( 1 ) or zero ( 0 ) based on the NAMECASE GENERAL setting of the document type definition (DTD) associated with the optional document ID parameter doc . If doc is omitted, the current document is used. A return of zero ( 0 ) means case-insensitive (that is, NAMECASE GENERAL YES ). A return of one ( 1 ) means case-sensitive (that is, NAMECASE GENERAL NO ). This function always returns one ( 1 ), if doc is an XML document, because XML markup is always case-sensitive.



---

# doc_new_stylesheet_association

# doc_new_stylesheet_association

doc_new_stylesheet_association ( doc , params[] )

This function creates a new stylesheet association for document doc with the attribute values specified by the associative array params where the keys of the array elements indicate the attribute name. Valid keys are href , type , title , media , charset , alternate . There must be elements for href and type . Others can be omitted. The href element should contain a relative path name, an absolute path name, or an http://URL . Arbortext Editor processes media values of Editor, Print/PDF, and screen. The screen media type is used to designate the HTML file stylesheet.

For example, the following function creates a new stylesheet association:

```
function add_ss_association(doc = current_doc())
{
local params[];
params["href"] = "htmlhelp.xsl";
params["type"] = "text/xsl";
if (!doc_new_stylesheet_association(doc, params))
{
response("Bad call to doc_new_stylesheet_association in " . caller());
return 0;
}
return 1;
}
```

If doc is not valid, or if params does not include elements for href and type , the function returns 0 . Otherwise, it returns the resulting number of stylesheet associations.

If params includes elements with keys other than those listed above, those elements are silently ignored. There is no validation of the contents of any of the params elements.



---

# doc_next_dobj

# doc_next_dobj

doc_next_dobj ( dobj )

Returns the document object that follows dobj in the same document.



---

# doc_num_stylesheet_associations

# doc_num_stylesheet_associations

doc_num_stylesheet_associations ( doc )

This function returns the number of stylesheet associations that are stored in the document. If doc is not a valid document identifier, the function returns -1 .



---

# doc_open

# doc_open

doc_open ([ path [, flags [, name [, pubid [, sysid [, stylesheet ]]]]]])

This function creates a new document tree and returns an identifier that may be used in subsequent calls to current_doc , oid_caret , insert_tag , and other functions. This function also generates an initial context for fragments so that context rules can be turned on for a partial document when displayed in a window using the doc_show command. The arguments that follow are optional.

path — Specifies the path name of a document directory or file name to load the initial contents of the document tree. If not specified or a null string, the document tree is empty.

flags — A bitmask that specifies open options and is constructed using OR with the following flags:

- • 0x001 — Open for read only and do not lock the underlying file. If this is not set, the underlying file will be locked if possible and the document will be read-only if no lock was acquired.

- • 0x002 — Open for writing and do not lock the underlying file. The document will be modifiable even though the underlying file is not locked. If the document was already open in memory, this will additionally attempt to lock the underlying file.

- • 0x004 — Do not lock the underlying file. Overrides all other flags which might acquire a file lock. The resulting document will not be modifiable unless 0x002 is also given.

- • 0x008 — Do a completeness check when reading the SGML or XML file. This corresponds to the -cc option for startup and the edit command.

- • 0x010 — Do not do a completeness check when reading the SGML or XML file. This corresponds to the -nocc option for startup and the edit command. By default, a completeness check is not done if the file was saved by Arbortext Editor . This bit is ignored if bit 4 is also specified.

- • 0x020 — Do not display any parser error messages in a message window. Instead, ignore all warnings and errors.

- • 0x040 — The document type specified by pubid and sysid should be used to parse the SGML or XML file instead of the document type specified in the file itself.

- • 0x080 — Open a help document. (Used internally by Arbortext Editor .)

- • 0x100 — Open a new document as an XML document when a public or system ID is specified.

- • 0x200 — Open the document without loading a stylesheet. If the document is called later by doc_show , the required stylesheet is loaded at that time.

- • 0x400 — Do not prompt the user if the document type associated with the document does not exist or is not compiled. Instead, return -1 .

- • 0x8000 — Source the associated document type instance files ( instance.acl and instance.js ), the document command files ( docname.acl and docname.js ), and any applications in the custom directory's editinit subdirectory. By default, these files are not processed until the document is displayed in a window with the doc_show function or edit command. The editfilehook is not called by doc_open but only if doc_show or edit is used.

- • 0x10000 — Treat the document as if it were created using File > New . In this case, the path name is set to null and the document name is of the form Document n .

- • 0x20000 — Specifies that if an autosave or recovery file exists for the document, the user should be prompted to select the document to open.

- • 0x40000 — Specifies that the pubid parameter is actually a namespace URI instead of a public identifier. If the 0x040 bit is also specified, then the namespace URI is used to locate the XML schema to parse the document. The sysid , if given, specifies the path to the DTD/schema file and is used if the namespace URI is null or is not resolved by catalog lookup.

- • 0x80000 — Open the document in free form mode, ignoring the document type specified in the file or by the public identifier pubid and system identifier sysid parameters. Flag bit 0x100 (open as XML) is implied by this bit.

- • 0x200000 — Specifies that the path name parameter path is actually a string to parse instead of a file to open. If the string does not contain a DOCTYPE declaration, the pubid and or sysid parameters must be given so the desired document type is used to parse the string. Otherwise, the 0x80000 bit must be specified. If the string contains XML markup but does not start with an XML declaration, the 0x100 bit must also be specified.

- • 0x1000000 — Do not add the document to the File menu's list of most recently used documents if this document is subsequently opened in an Edit view.

name — Specifies a name to be used for informational purposes. If omitted or null, the base name of path if given is used. If path is omitted, an internal name is assigned.

pubid — Specifies the public identifier for the document type.

sysid — Specifies the system identifier of the document type.

The pubid and sysid arguments specify the document type for the document tree if path is omitted or null or if the associated SGML file does not specify a DOCTYPE declaration, or if bit 0x040 is included in flags . The pubid and sysid arguments are ignored if path specifies an SGML file that starts with a DOCTYPE declaration or a binary document file, unless bit 0x040 is included in flags . As a special case, if pubid is "help", the built-in help window document type is used. If the document type is not specified, is “ascii”, or cannot be determined, then the ascii document type is used.

stylesheet — Specifies the stylesheet to be used instead of the default stylesheet for the document. If bit 0x200 is included in the flags parameter, the stylesheet parameter is ignored. If the specified stylesheet does not exist, Arbortext Editor displays an error message and the function returns a -1 .

The document identifier returned should be deleted with the doc_close function when it is no longer needed to unload the document tree from memory.

## Related Topics

- • doc_close function

- • Opening, referencing, and saving files



---

# doc_parent

# doc_parent

doc_parent ( doc )



This function returns the identifier of the document that references the file entity document given by doc , or -1 if doc is not a file entity.



---

# doc_path

# doc_path

doc_path ( doc )



This function returns the path name associated with the document given by doc , or the null string if no path name was specified when the document was created.



---

# doc_read_only

# doc_read_only

ret= doc_read_only ([ docid [, bool ]])

This function returns (and optionally sets) the read-only state specified when opening a document. doc_read_only does not report the file permission setting of a file as defined by the operating system, but the value used to open the document. (Documents can be opened as read-only with Open as read-only checked on the Open dialog box and with the function call open(doc, "r") . Documents can also be set to read-only using the function call doc_read_only(doc,1) .)

If no parameters are included, doc_read_only returns a boolean value ( 1 = read-only, 0 = read/write) for the read-only state of the current document. If the docid parameter is provided, doc_read_only returns the read-only state of the specified docid .

If both a docid parameter and a bool parameter are provided, the function returns the read-only state of the specified docid , and then sets the read-only state of the specified document to the boolean value specified in bool ( 1 = read-only, 0 = read/write).

Note that a standard opening of a read-only file will not cause doc_read_only(doc) to return 1 . This is due to the fact that a read-only file on disk may have references (such as XML inclusions and file entities) to other files that are not-read only. doc_read_only(doc) returns 0 for such a read-only root document because there may be parts of the document that can be edited.

Examples:

```
ret=doc_read_only()
ret=doc_read_only(docid)
ret=doc_read_only(docid,1)
```

To determine if a given oid can be modified, refer to oid_protected() and oid_find_valid_insert() .



---

# doc_revert

# doc_revert

doc_revert ([ doc [, flags ]])

This function reverts the document specified by the doc parameter to the last saved version, discarding any changes. If doc is 0 or omitted, the current document is used.

The flags parameter is a bitmask that specifies revert options and is constructed using OR with the following flags:

- • 0x001 — Revert the document read only. The in-memory document may not be changed in this case.

- • 0x002 — Suppress the prompt that unsaved changes will be discarded.

- • 0x004 — Revert the XML or SGML document in untagged mode. That is, do not interpret any markup.

- • 0x008 — Revert the document using an XML parser.

## Related Topics

- • doc_open function

- • doc_close function



---

# doc_save

# doc_save

doc_save ([ doc [, flags [, path ]]])

This function saves a document. If the doc parameter is 0 , the current document is saved. If both the doc and flags parameter is omitted, the current document is saved. If the flags parameter is omitted, no flags are set. If the path parameter is supplied, the document is saved to the file path set in that parameter instead of the current document. A file name must be supplied in this case if saving an XML document as SGML (or vice-versa).

The following flags are allowed:

- • 0x0001 — For documents with change tracking markup, save as if all changes are rejected (original view).

- • 0x0002 — For documents with change tracking markup, save as if all changes are accepted (latest view).

- • 0x0004 — For documents with change tracking markup, save as if all changes are pending (highlighted view).

- • 0x0008 — Write the document as an SGML document.

- • 0x0010 — Write a text-only version of the document.

- • 0x0020 — Write the document as an XML document.

- • 0x0040 — Removes the DOCTYPE header and internal subset, including any private ENTITY declarations.

- • 0x0080 — Removes processing instructions specific to Arbortext Editor .

- • 0x0100 — Enables entity output conversion.

- • 0x0200 — Suppresses entity output conversion.

- • 0x0400 — Writes non-ASCII characters as character entity references.

- • 0x0800 — Writes non-ASCII characters as characters in the target encoding.

- • 0x1000 — Writes non-ASCII characters as numeric character references.

- • 0x2000 — Used internally for HTML output.

- • 0x4000 — Expands all file entities recursively.

- • 0x8000 — Expands all text entities recursively.

- • 0x10000 — Writes a non-fragment header, if possible.

- • 0x20000 — Expands all XInclude references recursively.



---

# doc_set

# doc_set

$ret= doc_set ( doc , option , value )

For the document with a doc id of doc , this function sets the local document scope for the specified option to value . If you attempt to set an option with no local scope, or a local scope of window, an error occurs. If you set an option with a view scope, all views for the specified document will be updated to reflect the change in option value.

If the function executes successfully, it returns a one ( 1 ). If the specified option is invalid, or does not have a local scope of document or view, or the value is invalid for the option, the function returns a zero ( 0 ).

Examples

```
$ret = doc_set($doc,"showiconsfulltags","on")
$ret = doc_set($doc,"tagdisplay","full")
```

## Related Topics

- • Set option scope

- • doc_get function

- • current_doc function

- • option_scope function

- • set command



---

# doc_set_path

# doc_set_path

doc_set_path ( doc , path [, flags ])



This function changes the path name associated with the document given by doc to path . The new path name will be used to save the document. If path is a null string, the document will no longer have an associated path name. In this case, save_as must be used to save the document. If the second bit of the optional flags parameter is set, then the document will continue to use the same cache directory.



---

# doc_set_stylesheet_association

# doc_set_stylesheet_association

doc_set_stylesheet_association ( doc , i , params[] )

This function sets the i th stylesheet association for document doc to have the attribute values specified by the associative array params where the keys of the array elements indicate the attribute name. Valid keys are href , type , title , media , charset , and alternate . The href element should contain a relative path name, an absolute path name, or an http:// URL. Arbortext Editor processes media values of Editor , Print,PDF , and screen . The screen media type is used to designate the HTML file stylesheet.

For example, this function adds screen as a media type to the i th stylesheet association without changing the other fields.

```
function add_screen_media(i, doc = current_doc())
{
local params[];
if (!doc_get_stylesheet_association(doc, i, params))
{
response("Bad call to doc_get_stylesheet_association in " . caller());
return 0;
}
if (params["media"] != "")
{
params["media"] .= ",";
}
params["media"] .= "screen";
if (!doc_set_stylesheet_association(doc, i, params))
{
response("Bad call to doc_set_stylesheet_association in " . caller());
return 0;
}
return 1;
}
```

If doc is not a valid document identifier, or if there is no i th stylesheet association for doc , the function returns 0 . Otherwise, it returns 1 .

If params includes elements with keys other than those listed above, those elements are silently ignored. There is no validation of the contents of any of the params elements.



---

# doc_set_translation_locale

# doc_set_translation_locale

doc_set_translation_locale ( locale [, doc ])

Sets the translation locale of a specific document and marks the document as a translated version of another document.

- • locale — The translation locale to which the document will be set.

- • doc — (Optional). The identifier of the document for which the translation locale is set. If doc is omitted or 0 , the current document is used.

## Related Topics

- • doc_get_translation_locale

- • doc_is_translation

- • doc_get_translation_orig_uri

- • doc_set_translation_orig_uri

- • Translation PI



---

# doc_set_translation_orig_uri

# doc_set_translation_orig_uri

doc_set_translation_orig_uri ( uri [, doc ])

Sets the original URI value of the document for which a specific document is a translation and marks the document as a translation.

- • uri — The URI of the document for which doc is a translation.

- • doc — (Optional). The identifier of the document for which the URI is returned. If doc is omitted or 0 , the current document is used.

## Related Topics

- • doc_set_translation_locale

- • doc_get_translation_locale

- • doc_is_translation

- • doc_get_translation_orig_uri

- • Translation PI



---

# doc_show

# doc_show

doc_show ( doc , window )



This function shows the document tree identified by doc in the window specified by window , which is a window identifier as returned by window_create or is one of the predefined window names help , helpwin[1-4] , msg , or msgwin[1-4] . In the latter case, the window need not already exist. In both cases, the new document replaces whatever was previously displayed in the window. The specified document must not already be displayed in another window. doc_show returns 1 on success, or 0 if the window is not a supported window for doc_show .

If window specifies an edit class window, doc_show does the same initialization as the edit command (that is, document type instance files ( instance.acl and instance.js ) and document command files ( docname .acl and docname .js ) are read if they exist, and editfilehook is called). Context rules are also enabled for the document.



---

# doc_type

# doc_type

doc_type ([ doc ])

This function returns the external name of the document type associated with the document; for example, docbook. If doc is omitted, the current document is used.

If the given document is an XML instance without a DTD declaration, this function returns the name of the first non-empty tag in the document.



---

# doc_type_dcf_file

# doc_type_dcf_file

doc_type_dcf_file ([ doc ])

This function returns the full path and file name of the document type configuration file ( .dcf ) for the document type associated with doc . If doc is omitted or 0 , the current document is used.

## Related Topics

- • Document type configuration files

- • Editing and validating .dcf files

- • dcf_validate function



---

# doc_type_description

# doc_type_description

doc_type_description ([ doc ])

This function returns the first document type description declared in the document type configuration file ( .dcf ) for the document type associated with doc . This value is displayed in the New Document dialog box. If doc is omitted or 0 , the current document is used.

## Related Topics

- • Document type configuration files

- • Configuring the document type information in the New dialog box



---

# doc_type_dir

# doc_type_dir

doc_type_dir ([ doc ])



This function returns the directory name for the document type associated with doc . If doc is omitted, the current document is used. The document type directory contains the .dtd , .dcf , and .fos files that describe the document type.



---

# doc_type_dita

# doc_type_dita

doc_type_dita ([ doc ])

This function determines whether a given document doc is a DITA document. If doc is omitted or set to zero, the current document is used. The function returns one of the following values:

- • 0 — The document is not a DITA document.

- • 1 — The document is a DITA topic type or a DITA Ditabase.

- • 2 — The document is a DITA map type.

## Related Topics

- • DITA document types overview



---

# doc_type_extension

# doc_type_extension

doc_type_extension ([ doc ])

This function returns the default extension declared in the document type configuration file ( .dcf ) for the document type associated with doc . The default extension is used when saving a new document of the document type. If doc is omitted or 0 , the current document is used.

## Related Topics

- • Document type configuration files

- • Editing and validating .dcf files



---

# doc_type_file

# doc_type_file

doc_type_file ([ doc ])

This function returns the path name of the DTD ( .dtd ) or XML schema ( .xsd ) that defines the document type associated with doc . If doc is omitted, the current document is used.

## Related Topics

- • doc_type_dir function



---

# doc_type_gi

# doc_type_gi

doc_type_gi ([ doc ])

This function returns the generic identifier name from the DOCTYPE declaration for the document given by doc . If doc is omitted or 0, the current document is used.

Note that the return value is normally the root element declared in the DTD (for example, “book”), but it may be a different element name if the file had a DOCTYPE line specifying a lower level element (for example, “chapter”). This function is different from the doc_type function that returns the external name of the document type which need not be an element name.

## Related Topics

- • public_id function

- • system_id function



---

# doc_type_language

# doc_type_language

doc_type_language ([ doc ])

This function returns the string "XML Schema" if the document type associated with the specified document was defined using an XML schema, "DTD" if by a DTD, or the null string for free form or ASCII documents. If doc is not specified or is 0 , the current document is used.

## Related Topics

- • doc_type_xml function

- • doc_freeform function



---

# doc_type_namespace

# doc_type_namespace

doc_type_namespace ([ doc ])

This function returns the target namespace URI declared in the XML schema for the document type associated with doc . If the document type is defined by a DTD but was located using a namespace URI catalog entry, then that namespace URI is returned. Otherwise, a null string is returned.

If doc is omitted, the current document is used.



---

# doc_type_namespaces

# doc_type_namespaces

doc_type_namespaces ( doc , arr )



This function populates an associative array with all of the namespaces imported into the XML Schema for the document type associated with doc . The associative array has the namespace prefix as the key, and the namespace URI as the value. The function returns the number of entries in the array.

If doc is omitted or 0 , then the current document is used.



---

# doc_type_root_tags

# doc_type_root_tags

doc_type_root_tags ( doc , arr )

This function fills the array arr with the names of all elements which are considered root tags for the document type associated with the document given by doc . Any element declared in the XML DTD or XML Schema that is not included in the content model of another element is considered a possible root element.

For compiled document types, only the top tag specified when the document type was compiled is returned.

The function returns the number of elements stored in the array.

## Related Topics

- • doc_type function

- • doc_type_gi function



---

# doc_type_schematron_file

# doc_type_schematron_file

doc_type_schematron_file ([ doc [, newFile ]])

This function retrieves or sets the list of Schematron files used with the document type associated with doc . If doc is not supplied or is 0 , then the current document is used. If newFile is not supplied, then the function returns the full paths to the document type’s Schematron files. If newFile is supplied, then the specified Schematron file is added to the list used with the document type. If newFile is supplied and is an empty string, then no Schematron processing will be done for the document type.

Any Schematron file associated with a document type is used by completeness checking for further validations of a document instance.

For example, the following ACL function call will modify the document type schematron file association for the current document to include the files axdocbook1.sch and axdocbook2.sch :

```
doc_type_schematron_file(0, "axdocbook1.sch;"axdocbook2.sch");
```

Note that the semi colon ( ; ) is the required delimiter.

## Related Topics

- • validate_against_schematron function



---

# doc_type_xml

# doc_type_xml

ret = doc_type_xml ([ doc ])

This function returns 1 if the document type associated with the specified document was compiled as an XML application or 0 otherwise. If doc is not specified, the value of current_doc is used.

## Related Topics

- • doc_kind function



---

# doc_update_display

# doc_update_display

doc_update_display ([ doc [, flag ]])

This function suspends screen updates for the specified document doc if the flag parameter is zero ( 0 ). If the flag parameter is not set, then the function returns the current setting for whether screen updates are suspended for doc ( 1 if the display is not suspended).

Suspending screen updates may speed up a script that makes many edits to a document that is displayed in a window, especially if partial generated text updates are enabled (the default). Before returning, a script that suspended screen updates would need to re-enable screen updates by calling doc_update_display with the flag parameter set to 1 .

Use caution when calling this function. If screen updates are not restored, then the document may be displayed incorrectly to the user.



---

# doc_valid

# doc_valid

doc_valid ( doc )

This function returns 1 (True) if doc is a valid document identifier, otherwise it returns 0 .

doc_valid(0) is always a valid document and is the same as doc_valid(current_doc()) .



---

# doc_window

# doc_window

doc_window ( doc )



This function returns the identifier of the window associated with the document given by doc . If doc is invalid or is not currently attached to a window, it returns -1 .



---

# doc_word_count

# doc_word_count

doc_word_count ([ doc [, flags ]])

Returns the number of words in the current selection or whole document if no selection has been made. The message " nnn words in the current selection" is written to the status bar if not suppressed.

- • If the doc value is omitted, the default is the current doc.

- • flags — Flag bits ORed together, with a default of 0. Initially, only bit 1 is supported. If set, the message is shown, else it is suppressed.



---

# document_export

# document_export

document_export ([ inFile [, outFile [, styleFile [, logFile [, nFlags ]]]]])

This function starts an export process with the specified parameters. This function returns a one ( 1 ) if the export was successful. document_export returns zero ( 0 ) if unsuccessful.

document_export has the following parameters:

- • inFile is the path name of the document to export. If null, the current document is used.

- • outFile is the path name of the converted document.

- • styleFile is the Arbortext Styler -created style sheet to use during the export.

- • logFile is the path name of a log file used to record information about the export process.

- • nFlags is a set of bit flags (that is, an integer argument, not a string argument), defined as follows:

The first three parameters ( inFile , outFile , and styleFile ) are optional in that they need not be specified in the function call. However, if any one of them is not specified, a dialog box will be displayed to allow the user to specify valid values for them. The final two parameters ( logFile , nFlags ) are optional. If they are not specified, default values will be used. If the last parameter, nFlags , is set to 1 , the first three parameters must be specified because no dialog box will be displayed to allow the user to specify valid values for them. If nFlags is set to 1 and one of the first three parameters is not specified, the function will return 0 stating failure of the export process.



---

# dom_address

# dom_address

addr = dom_address ( domId [, interface ])

Returns the address of the DOM object identified by domId . The returned address may be passed to a dynamically-loaded entry point with the ACL function dl_call .

The optional interface parameter specifies the Application Programming Interface that the DOM object will support. If omitted, it defaults to dom L1 V1.0 , meaning Version 1.0 of Level 1 of the W3C Document Object Model.

## Related Topics

- • dl_call function

- • dom_document function

- • dom_free function

- • dom_oid function



---

# dom_document

# dom_document

domId = dom_document ([ doc [, interface ]])

Creates a new DOM document object for the Arbortext Editor document doc and returns the DOM document object's ID. If doc is omitted, the function uses the returned value of current_doc .

The optional interface parameter specifies the Application Programming Interface that the DOM object will support. If omitted, it defaults to dom L1 V1.0 , meaning Version 1.0 of Level 1 of the W3C Document Object Model.

If an error occurs, this function returns the value h::NullDOMId .

After creating a DOM document object with dom_document and finding the object's address with dom_address , the ACL programmer can pass the address to an external dynamically-loaded C++ program using dl_call .

## Related Topics

- • dl_call function

- • dom_address function

- • dom_free function

- • dom_oid function



---

# dom_free

# dom_free

ret = dom_free (domId)

Frees the DOM object identified by domId . Returns 0 if domId is invalid, 1 otherwise.

If the address of a DOM object is passed to an external C++ program, calling dom_free will make the address invalid. Any attempt by the C++ program to call the DOM object from that point forward may cause Arbortext Editor to fail.

## Related Topics

- • dl_call function

- • dom_address function

- • dom_document function

- • dom_oid function



---

# dom_oid

# dom_oid

domid = dom_oid ([ oid ])

Returns the ID of the DOM object associated with the object ID oid . If oid is omitted, the oid containing the current caret position is used.

If the document containing oid does not have an associated DOM document object, a new DOM document object is created and associated with the document; in this case, the default DOM interface code for the document will be set to dom L1 V1.0 .

## Related Topics

- • dom_address function

- • dom_document function

- • dom_free function



---

# drag_start

# drag_start

drag_start ([ cut ])

This function turns on drag-and-drop editing. The function tracks the mouse movement and gives the user visual feedback on whether or not the selected area can be pasted at the cursor location. The function also tracks the state of the ctrl key to determine if the user intends to copy the selection ( ctrl key selected during the drag) or cut the selection ( ctrl key not selected during the drag). The cursor moves with the mouse pointer and indicates where the drop should occur.

You must have something selected in the window for this function to work. Usually, the function is mapped with a mouse button down event.

If the optional cut flag is set to 1 , Arbortext Editor ignores the state of the ctrl key and forces a cut to take place, if it doesn't cause a context error.

To give users visual feedback, part of the selection is drawn under the mouse pointer during the drag.

Use the drag_stop function to stop the mouse tracking initiated by drag_start .

This function returns a 1 on success, and 0 on failure.

## Related Topics

- • drag_stop function



---

# drag_stop

# drag_stop

drag_stop ( do_cut )

This function stops the drag-and-drop mouse tracking initiated by the drag_start function and helps the user determine whether a paste can be performed or not. The do_cut parameter is a user-defined variable that is set by the function. The value of the specified do_cut variable reflects whether the user had the ctrl key down when they completed the drop. If the ctrl key was down, the user intended to copy the selection; the specified do_cut will be 0 . If the ctrl key was up, the user intended to cut the selection, so the specified do_cut will be a 1 .

This function returns one of the following values:

- • 0 — drag_start was not called.

- • -1 — The mouse pointer has not moved since drag_start was called.

- • -2 — The mouse pointer is not in a Arbortext Editor window.

- • -3 — Cut would cause context errors.

- • -4 — Paste would cause context errors.

- • If the return code is greater than 0 , then the value is the identifier of the window that has focus. This indicates that the cursor is at a valid paste location.

## Related Topics

- • drag_start function



---

# drop_file_info

# drop_file_info

drop_file_info ( num )

This function returns the path name of a file involved in a drag and drop operation. You typically call this routine from a drop_file_over callback the first time the callback is called for a particular drag and drop operation. If more than one file is being dropped, then you must call this routine multiple times to obtain information about all of the files. You should only call this function once for each file during a single drag and drop operation.

The num argument is the number of the file for which you want to return the path name. The first file is 1 . The function returns a null string if there is no file available.

## Related Topics

- • drop_file_over callback function



---

# dtd_decl_path

# dtd_decl_path

dtd_decl_path ( pubid [, catalogpath ])



This function returns the storage object identifier (path name) for the public identifier pubid specified on the first SGMLDECL or DTDDECL keyword found in a catalog file.

The catalogpath argument specifies a list of directories to search for the catalog file. If it is not specified, the path list specified in the catalogpath set option, which is initialized from the environment variable APTCATPATH , is searched.

The function returns a null string if neither a SGMLDECL nor a DTDDECL keyword specifying pubid is found in any of the catalogs searched.



---

# dtd_tag

# dtd_tag



This function returns 1 (True) if tagname is the name of an element defined in the DTD. dtd_tag returns 0 (False) if tagname is not a valid tag name or if it is a Arbortext Editor supplied tag (for example, the processing instructions _font or _ignore ).

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# dupl

# dupl

dupl ( s , n )



This function returns a copy of string s , duplicated n times. For example, dupl('*', 5) would return "*****" .



---

# edit_id

# edit_id

edit_id ([ doc [, flags ]])

This function returns the current edit "id". The edit id is a number which gets incremented for each edit operation performed on the document. Command scripts can use this number to determine if the document was changed between two alias or user-defined function calls. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used. If the flags argument is set and has a value of 1 , then the function returns the edit id for the last structural change to doc .



---

# edit_new_window

# edit_new_window

edit_new_window ( filename )

This function opens a secondary Edit window from within Arbortext Editor . A secondary edit window allows the same functions as the Edit window.

The argument filename specifies the path name of a document to be loaded into the new Edit window.

## Related Topics

- • edit command



---

# elapsed_time

# elapsed_time

elapsed_time ( )



This function returns the elapsed time in 100ths of a second since the current session of Arbortext Editor was started. This is the wall clock time as opposed to the CPU time (which is returned by times ).

## Related Topics

- • times built-in function



---

# entity

# entity

entity ( entity [, doc ])



This function returns the value of the text or character entity named name . The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used. For a text entity, the function returns the replacement value. For example, if the DTD has the definition <!ENTITY AT “ PTC Inc. ”> the function entity ("AT") would return " PTC Inc. .". If the entity is a character entity, this function searches the file APSPATH/lib/charent.cf for an entry matching name , returning the character given in the Unicode column if found. If it is not found, the return value varies depending on whether the document is an XML or SGML instance. For XML documents, the function returns the resolved single character replacement value, for example, for the declaration <!ENTITY Auml “&#38;#x00C4”> the function entity ("Auml") returns "D" (character 0xc4). For SGML documents, a character entity is normally declared as a SDATA entity, for example, <!ENTITY Auml SDATA “[Auml]”> and the function entity ("Auml") returns "[Auml]".



---

# entity_doc

# entity_doc

entity_doc ( entity [, doc ])



This function returns the document identifier of the text or file entity specified by entity (for the specified doc or the current document if doc is not specified). entity_doc returns -1 if entity is not a file or text entity. If entity is a file entity reference, the document identifier returned will be different from the specified doc . If entity is a text entity, the document identifier returned will be doc .



---

# entity_exists

# entity_exists

entity_exists ( entity [, doc ])



This function returns 1 (True) if the entity name specified by entity is defined in the DTD or in the section of the document instance that contains document-specific markup declarations. The entity name need not start with `&'. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# entity_expand

# entity_expand

entity_expand ( value [, flags [, doc ]])

This function expands character and text entity references in the given value string and returns the expanded string.

- • value is the value to be expanded

- • flag is a bitmask that controls the expansion of the entity:

- • doc is the document which defines the entities. If omitted, the current document is used.

In XML the < and & characters must be escaped inside an attribute value; for example, in an attribute value, the string A<B&C>D should be encoded as A&lt;&amp;C.D .

To get the expanded value of the src attribute on the tag containing the caret:

```
local expandedValue = entity_expand( oid_attr( oid_caret(), 'src' ) )
```



---

# entity_first

# entity_first

entity_first ( entity [, doc ])



This function returns the OID of the first element within the text or file entity specified by entity (for the specified doc or the current document if doc is not specified). entity_first the null OID if entity is not a file or text entity, or if there are no elements within the entity.



---

# entity_last

# entity_last

entity_last ( name [, doc ])



This function returns the OID of the last element within the text or file entity specified by name , for the specified doc (or current document, if none given). Returns the null OID if entity is not a file or text entity or if there are no elements within the entity.



---

# entity_name

# entity_name

entity_name ( oid )



If oid is an object within a text or file entity, this function returns the name of the entity (for example, chap1 ). Returns the null string if oid is not contained within an entity, but is in a top-level document tree.



---

# entity_notation

# entity_notation

entity_notation ( name [, doc ])

This function returns the notation value from the declaration for the entity name . It returns the null string if the entity does not exist or is not a graphic entity.

The doc argument specifies the identifier of the document to query. If omitted or 0 , the current document is used.



---

# entity_parfile

# entity_parfile

entity_parfile ( name [, doc ])

This function returns the name of the parameter file entity in which the entity was declared (if the entity was declared in a parameter file entity). Otherwise, the null string is returned.

name is the name of the entity. A leading & is optional for general entities. The leading percent sign % must be supplied for parameter entities.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# entity_path

# entity_path

entity_path ( name [, doc ])

This function returns the resolved absolute path name for the external entity given by name . If the entity given by name is not defined or is not a file or graphic entity name, the function returns the null string. The doc parameter specifies the identifier of the document tree to query. If omitted or 0, the current document is used. This callback should always be set globally.

For example,

```
$path = entity_path("prodname")
```

would return the full path and file name of the prodname file entity in the $path variable.

## Related Topics

- • entity_path callback type to doc_add_callback

- • oid_type function

- • oid_name function



---

# entity_pubid

# entity_pubid

entity_pubid ( name [, doc ])

The entity_pubid function returns the PUBLIC identifier from the declaration for the entity name . A leading & is optional for general entities. The leading percent sign % must be supplied for parameter entities.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

It returns the null string if the entity does not exist or if no PUBLIC identifier was specified.



---

# entity_relative_path

# entity_relative_path

newpath= entity_relative_path ( path , dir , type )

This function converts the absolute path name given by path into a relative path name if possible. If the file is in or below the same directory as the supplied directory dir , then a path name relative to that directory is returned. If the file is not in or below dir , depending on the value of type, if the file is in or below a directory from one of the path list options being considered, then a path name relative to that directory is returned. Otherwise, the original input path name is returned.

The type parameter can have one of the following values:

- • 0 if the reference is to a graphic.

- • 1 if the reference is to a file entity.

- • 2 if the reference is to an XML inclusion.

- • 3 if the reference is a DITA reference.

## Related topic

- • entity_path function

- • graphic_relative_path function



---

# entity_resolve

# entity_resolve

entity_resolve ( name [, pubid [, sysid [, catalogpath ]]])

This function does a catalog lookup to resolve the entity specified by the name , pubid and sysid parameters, returning the system path name. If the identifier is not found in any of the catalog files in the search path, the entity_resolve function returns a null string.

The name argument specifies the entity name to be used in the catalog lookup. If can be a null string if the pubid and/or sysid are non-null. The name must not start with the & general delimiter.

The pubid argument specifies an optional public identifier associated with the entity declaration.

The sysid argument specifies an optional system identifier associated with the entity declaration.

The catalogpath argument specifies a list of directories to search for the catalog file. If it is not specified, the path list specified in the set catalogpath option, which is initialized from the environment variable APTCATPATH , is searched.

The function public_id_path(pubid, "", catpath) is equivalent to entity_resolve("", pubid, "", catpath) .

The function entity_resolve(name, pubid, sysid, catpath) is equivalent to catalog_resolve("ENTITY", name, pubid, sysid, catpath) .

## Related Topics

- • catalog_resolve function

- • public_id_path function

- • catalog_public_ids function

- • path_public_ids function

- • entity_pubid function

- • entity_sysid function



---

# entity_source

# entity_source

entity_source ( name [, doc ])



The entity_source function returns a number indicating the origin of the declaration for the entity named name . The return value is one of the following integers:

- • -1 — entity not declared.

- • 0 — entity defaulted.

- • 1 — entity declared in declaration subset (private markup) only.

- • 2 — entity declared in DTD only.

- • 3 — entity declared in both DTD and declaration subset.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# entity_sysid

# entity_sysid

entity_sysid ( name [, doc ])



The entity_sysid function returns the SYSTEM identifier from the declaration for the entity name . A leading & is optional for general entities. The leading percent sign % must be supplied for parameter entities.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

It returns the null string if the entity does not exist or if no SYSTEM identifier was specified.



---

# entity_tag

# entity_tag

entity_tag ( tagname [, doc ])

This function returns 1 (True) if the markup named tagname is really a tag used to represent an SGML entity declaration. If the markup is not an SGML entity declaration, 0 is returned. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# entity_to_unicode

# entity_to_unicode

entity_to_unicode ( entname )

Provided the character entity name entname , this function returns the unicode equivalent. For example, if you were to give entname the value of 'Theta' , the function would return the value 920 .

If there is no unicode equivalent for the character entity entname , the function returns a zero ( 0 ).

Note that the available character entity names depend on the document type you are using. Use the Arbortext-path \lib\charent.cf file a reference to character entity names.

## Related Topics

- • unicode_to_entity function



---

# entity_type

# entity_type

entity_type ( name [, doc ])



The entity_type function returns a string describing the type for the entity named name . The return value is one of the strings:

- • accent — character (SDATA) entity that is an accent

- • char — character (SDATA) entity

- • file — external entity

- • filep — parameter file entity

- • graphic — external graphic (NDATA) entity

- • msp — marked section parameter entity

- • text — internal general entity

If name is not a valid entity, the null string is returned.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# eof

# eof

eof ( fid )



This function returns 1 if an end-of-file condition has occurred on file identifier fid , or 0 otherwise. fid must be a return value from a previous call to open .

## Related Topics

- • open built-in function



---

# error

# error

error ( message )

This function sounds a beep and displays the error message specified by message in the status bar of the current window if possible, otherwise in a separate window. The message is also assigned to the $ERROR predefined variable.

The error function is used by Arbortext Editor to display most error messages.

## Related Topics

- • response function

- • message command



---

# errors_suppressed

# errors_suppressed

errors_suppressed ( )



This function returns 1 if errors are currently being suppressed in ACL. This is usually the case when an eval or execute command is active.



---

# eval_(Function)

# eval (Function)

eval ( expr [, package ])

This function parses and evaluates the value of the expression expr . The result is returned as a string or number depending on the context. When called from a user-defined function, the expression is compiled within the current scope, so local variables are accessible.

package , if specified, changes the effective package used to evaluate the expression. By default, the current package is used.

If there is a syntax or runtime error, the variable $ERROR gives the error message. If there is no error, then $ERROR is set to the null string. This function does not generate error popup messages. The caller must display the value of $ERROR if desired.

Here is an example of how to call a function whose name is not known until runtime (that is, the value of the variable $funcname is unknown at compilation):

```
eval("$funcname($$x)")
```

In this case, the argument is the variable x . The double dollar-sign is not needed if eval is called from the context of a user-defined function.



---

# event_process

# event_process

event_process ([ blockall ])

This function enters a nested event loop to block the current thread of ACL execution until some until other event causes an event_stop_process call. If the blockall parameter is specified and non-zero, then all user input events are blocked. This might be useful to block the user while waiting for input from a network channel; the callback set with channel_set_callback would resume the execution thread by calling event_stop_process .

This function returns the value passed to the event_stop_process call that terminated the nested event loop.

Example:

```
function timerCallback()
{
event_stop_process(1);
return 0;	# cancel timer
}
timer_add_callback(500, "timerCallback");
window_set(0, "message", "waiting...");
# wait 5 seconds, blocking all input
$result = event_process(1);
window_set(0, "message", "event_process returned $result");
```

## Related Topics

- • event_stop_process function

- • channel_set_callback function

- • timer_add_callback function

- • disable_windows function



---

# event_stop_process

# event_stop_process

event_stop_process ( code )

This function terminates the nested event loop entered by the last event_process call. When the event that resulted in the event_stop_process call is finished, ACL execution resumes after the event_process call.

The code parameter becomes the return value from event_process .

Example:

```
function timerCallback()
{
event_stop_process(1);
return 0;	# cancel timer
}
timer_add_callback(500, "timerCallback");
window_set(0, "message", "waiting...");
# wait 5 seconds, blocking all input
$result = event_process(1);
window_set(0, "message", "event_process returned $result");
```

## Related topic

- • event_process function



---

# execute_(Function)

# execute (Function)

execute ( cmds [, package ])

This function parses and executes cmds as a sequence of Arbortext Editor commands. The result is the value of the last command executed (that is, what the $status variable is set to): 0 if success, 1 if a runtime error, or 2 if a syntax error. If there is a syntax or runtime error, the variable $ERROR gives the error message.

When called from a user-defined function, the expression is compiled within the current scope, so local variables are accessible. The argument package may be specified to change the effective package used to execute the command. By default, the current package is used.

This function does not generate error popup messages. The caller must display the message if desired. For example, the execute command could be written as an alias using this function:

```
alias execute {
if (execute("$*") != 0) {
beep;
response($ERROR)
}
}
```



---

# exit_editor

# exit_editor

exit_editor ([ rc [, code ]])

This function terminates the application with rc , which is a return code you assigned, or 0 if not supplied, as the exit program code. The argument code determines if the user is prompted for unsaved changes or not and has one of the values:

- • 0 — prompt about any unsaved changes, that is, quit

- • 1 — save all modified documents without prompting, that is, exit

- • 2 — do not prompt about unsaved changes and quit without saving modified documents, that is, quit ok

The default is 0.



---

# expand_file_name

# expand_file_name

expand_file_name ( pathname )



This function returns the path name corresponding to pathname . Any environment variables in the string expression are expanded.

A leading ~ expands to the value of the HOME environment variable. If the HOME environment variable is not set, the ~ resolves to the value of the HOMEDRIVE and HOMEPATH environment variables (which are usually set on Windows). If neither HOME or HOMEPATH are set, the ~ is not substituted and will remain in the path.

Examples

```
$f = 'C:\source_files\graphics\home.tif'
g$example = expand_file_name($f)
```



---

# file_close

# file_close

file_close ([ win [, flags ]])

This function closes (destroys) the window specified by the win parameter. If win is not specified, it closes the current window. Executing this function is similar to choosing the File > Close menu option.

The flags parameter is a bitmask specifying special file closing settings and is constructed by ORing the flags from the following list:

- • 0x0001 — Set this flag to suppress all prompts to save the document open in the window.

- • 0x0002 — Set this flag to close the very last Arbortext Editor window. By default, closing the very last window causes it to remain open but display an empty text document. Note that even when the very last Arbortext Editor window is closed, the Arbortext Editor process remains running. Be careful when using this flag.

- • 0x0004 — Set this flag to not offer the option to Cancel during any prompts to save a document.

If the document in the specified win (or current window) appears in both an Edit view and a Document Map view, both view “windows” will be closed. If there are other window frames open for the current session, the window frame is destroyed as well.

The first view “window” in a window frame cannot be destroyed. If the current session has only one window frame, 0x0002 was not specified, and the function closes the document in the first view “window” in the window frame, a blank ASCII document is placed in the first view window.

This function does not affect the windows in any other window frames that contain the same document appearing in the window specified by win .



---

# file_directory

# file_directory

file_directory ( path )



This function returns 1 (True) if the path name specified by path is a directory.



---

# file_entity_names

# file_entity_names

file_entity_names ( arr [, doc ])



The file_entity_names function fills the array arr with an alphabetical list of file entity names which are valid for the current document, returning the total number. The first name returned is stored at index 1. All previous elements in arr are discarded.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# file_entity_tag

# file_entity_tag

file_entity_tag ( tagname [, doc ])



This function returns 1 (True) if the tag named tagname is really a tag used to represent an SGML file entity declaration. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# file_is_graphic

# file_is_graphic

file_is_graphic ( path )

This function returns 1 (True) if the path name specified by path is a recognized graphic file, or ends with an extension specified by the set othergraphicsextensions option.

## Related Topics

- • set othergraphicsextensions option



---

# file_is_zip

# file_is_zip

file_is_zip ( path )

This function returns a non-zero number (True) if the path name specified by path is a recognized zip archive file. It returns zero if the file is not a recognized zip archive file or on any error.

Note that this function does not detect other forms of compressed files, such as tar or rar files.



---

# file_mtime

# file_mtime

file_mtime ( path )



This function returns the last modification time of the file specified by path or 0 if the file does not exist. The time is given in seconds since the epoch (which is operating system-specific). This time can be converted into a string for display using the ctime function.

The path argument is either a file system path or an HTTP or HTTPS resource. For the latter, the function issues an HTTP HEAD request and uses the response header called Last-Modified to determine the modification time. On any error, or if the desired response header is missing, this returns 0 .

Examples

```
eval ctime(file_mtime("memo.sgm"))
eval ctime(file_mtime("/
Arbortext-path
/memo.sgm"))
eval ctime(file_mtime('c:\memo.sgm'))
eval ctime(file_mtime("c:\\memo.sgm"))
```

## Related Topics

- • ctime built-in function



---

# file_newer

# file_newer

file_newer ( file1 , file2 )



This function returns 1 (True) if the modification date of the file specified by file1 is greater, or more recent, than that of the file specified by file2 .



---

# file_public_id

# file_public_id

file_public_id ( path )

The file_public_id function returns the public identifier for the SGML document instance path . It returns the null string if the file indicated by path does not exist, or does not have a public identifier.



---

# file_selector

# file_selector

file_selector ( dir [, ext [, filter [, title [, flags ]]]])

This function displays a file selection dialog box and returns the user's response. The null string is returned if the user selects Cancel .

dir is the directory initially displayed in the dialog box. If the dir directory is not a valid drive, then the dialog box uses the last drive the Open dialog box used to open a file in Arbortext Editor .

The remaining arguments are optional:

- • filter is a string specifying a list of file types to display in the List Files of Type pulldown list. A vertical bar “|” is used to separate each list item. There are two parts to each item, which are also separated by a vertical bar “|”. The first part is the string displayed in the pulldown list. The second part is the corresponding pattern used to filter the files displayed in the dialog box. See the example that follows.

- • ext specifies the default extension to display in the File Name control. It should be one of the extensions given in the filter list filter . The extension separator "." must not be included.

- • title specifies the window title for the dialog box.

- • flags is a bitmask specifying special file selector settings and is constructed by ORing the flags from the following list:

Example

```
l="SGML Files|*.sgm|Command Files|*.acl|All Files|*.*"
fname = file_selector(".", "sgm", l, "Open Document")
```

The * wildcard will include all files.



---

# file_size

# file_size

file_size ( path )



This function returns the size in bytes of the file specified by path . The path argument is either a file system path or an HTTP or HTTPS resource. For the latter, the function issues an HTTP HEAD request and uses the response header called Content-Length to determine the modification time. On any error, or if the desired response header is missing, this returns -1 .

The file_size function can be written using file identifier functions as follows:

```
function file_size(path)
{
local fid = open(path, "rb")
if (fid < 0) {
return -1
}
seek(fid, 0, 2); # to eof
local off = tell(fid)
close(fid)
return off
}
```



---

# file_system

# file_system

file_system ([ path ])



This function returns a string which identifies the type of file system containing the file specified by path .The return value is "fat" if the path name specifies a DOS file system, "ntfs" if a Windows file system, and so on. If path is omitted, the current working directory is used.



---

# filename_encode

# filename_encode

filename_encode ( name [, escape [, translateSlash ]])

This function returns the string name encoded according to internet RFC 1738. Most non-printable characters in name , including all characters with ASCII values over 255, are encoded as 2 or 4 digit hexadecimal sequences following an escape character.

This function has the following parameters:

- • name — The character string to encode.

- • escape — Optional. Specifies the character to note the start of the hexadecimal representation of an encoded character. If escape is omitted or specified as the empty string, filename_encode uses the % (percent) character. If escape contains more than one character, only the first character is used.

- • translateSlash — Optional. If translateSlash has any value other than 0 or "" (the null string), backslash (Windows) separators ( \ ) are converted to forward slashes ( / ) and forward slashes are not encoded. If the parameter is omitted, or has a value of either 0 or the null string, backslashes are not converted to forward slashes, and both backslash and slash characters are encoded.

The calls:

```
filename_encode("abc def");
filename_encode("abc def", "");
filename_encode("abc def", "%");
filename_encode("abc def", "%XYZ");
```

Return:

```
abc%20def
```

The call:

```
filename_encode("abc def", "_")
```

Returns:

```
abc_20def
```

The call:

```
filename_encode( "abc def\", "%", 1)
```

Returns:

abc%20def/



---

# filename_to_url

# filename_to_url

filename_to_url ( path )

This function returns the file name path converted to a UTF8–encoded file-scheme URL conforming to RFC 1738. It converts the file name to an absolute path name, replaces all file separator characters with ' / ', and encodes all non-alphanumeric characters (except for $ , - , _ , . , + , ! , * , ' , ( , ) , / , and : ) into a sequence of one or more 3-character strings % XX , where the XX values are the two digit hexadecimal codes for the UTF-8 encoding of the character. It returns the result prefixed with file:// . If the file name is a directory, a trailing / is appended to the result.

For example, the following function:

```
filename_to_url('article#1.xml')
```

would return a string like the following:

```
file:///C:/documents/article%231.xml
```

As another example, the function:

```
filename_to_url('c:\file' . chr(0x3042) . '.txt')
```

would produce:

```
file:///C:/file%E3%81%82.txt
```

## Related Topics

- • url_decode function

- • url_encode function

- • Opening, referencing, and saving files



---

# filep_entity_names

# filep_entity_names

filep_entity_names ( arr [, doc ])



The filep_entity_names function fills the array arr with an alphabetical list of file parameter entity names which are valid for the current document, returning the total number. The first name returned is stored at index 1. All previous elements in arr are discarded.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# find

# find

find ( searchStr [, flags [, element [, doc ]]])



This function searches for the specified string searchStr . The search ignores generated text and returns 1 on success, 0 on failure.

- • searchStr — String to search for.

- • flags — Bit mask for modifying the search.

- • element — Search only the contents of elements with this name.

- • doc — Current document instance is used if not specified.



---

# find_dita_rd_dcf

# find_dita_rd_dcf

find_dita_rd_dcf ( rdType [, doc ])

This function returns the document type definition ( .dcf ) file that will be used by a resolved document generated for the given DITA map. The rdType parameter is the type of resolved document for which you want to determine the .dcf file. Allowed values are ditaRDStyle for the resolved document for styling and ditaRDEdit for the resolved document for editing. The doc parameter is the DITA map that would be used to generate the resolved document.

## Related Topics

- • Working with DITA resolved documents

- • Document type configuration files

- • dita_rds_dtd_from_map function

- • dita_rde_xsd_from_map function

- • flush_dita_rdgen_cache function



---

# find_file_in_path

# find_file_in_path

find_file_in_path ( filename [, mode [, pathlist [, defaultpath ]]])

This function searches the list of directories specified by pathlist for the file given by filename returning the path name of the first match if found.

The mode parameter specifies the permissions for the file and is one of the following characters:

- • e — exists

- • r — read

- • w — write

- • x — executable

If mode is omitted, e is assumed.

If pathlist is omitted, the value of the PATH environment variable is used. Each directory component in pathlist is expanded using expand_file_name so home directory and environment variable references are permitted.

The defaultpath parameter specifies the default value for a %D qualifier given as part of pathlist , that is, the value of defaultpath will be substituted for %D . If omitted, no substitution is done. See the third example below.

The function returns the null string if filename is not found within the pathlist, or is not accessible according to mode .

Examples

```
browser = find_file_in_path("Netscape");
logofile = find_file_in_path("logo.gif", "r", option("graphicspath"));
cfile = find_file_in_path("catalog", "r", ".${main::PCS}%D", \
option("catalogpath"));
```

## Related Topics

- • expand_file_name function



---

# flush

# flush

flush ( fid )



This function flushes any output buffered for the file identifier fid , which must be a return value from a previous call to open . flush returns 0 on success or -1 on failure (for example, if the associated file was not opened for writing).



---

# flush_dita_rdgen_cache

# flush_dita_rdgen_cache

flush_dita_rdgen_cache ()

This function deletes all temporary DITA resolved document for styling DTDs and resolved document for editing XML schemas and unloads the internal data structures representing those document types. All future requests to retrieve a resolved document will result in a new file being generated.

## Related Topics

- • Working with DITA resolved documents

- • Document type configuration files

- • dita_rds_dtd_from_map function

- • dita_rde_xsd_from_map function

- • find_dita_rd_dcf function



---

# font_families

# font_families

font_families ( arr )

This function fills the array arr with an alphabetical list of font family names available for display on the current system. The first name returned is stored at index 1 . The function returns the number of font family names added to the array.

All previous elements in arr are discarded when the function executes.



---

# formatting

# formatting

formatting ()



This function returns 1 (true) if a format , print , or preview command is currently running. Otherwise, formatting returns 0 .



---

# forward_char

# forward_char

forward_char ( count [, doc ])



This function moves the cursor count characters to the right in the document given by doc , or the current document if doc is omitted. If count is negative, then the logical cursor is moved left count characters. Each non-text object (that is, tags, equations, graphics) counts as one character. This function returns 1 (True) if the cursor was moved the specified distance. It returns 0 (False) if the end (or beginning) of the document was reached. Note, that forward_char(1) is similar to the command caret 0,+1 , except that the function always moves one character.

The caret command treats the case of the cursor at the end of a screen line specially and moves the cursor to the beginning of the next line, which is before the same character. Because of this, for cases where the screen representation is not important or relevant (for example, for a document loaded with doc_open ), forward_char is more useful.

## Related Topics

- • caret command

- • doc_open built-in function



---

# fosi_public_id

# fosi_public_id

fosi_public_id ( fdoc )

This function returns the public identifier for the instance document associated with the FOSI document given by fdoc , or the null string if fdoc is not an attached FOSI.



---

# fosivar_value

# fosivar_value

fosivar_value ( window , varname , oid )

You can call fosivar_value from functions that are called as a result of the attloc=system-func FOSI setting.

The fosivar_value function works the same as #FOSI, except that it can be called from within functions invoked by the system-func feature.

window is the window ID that was passed as an argument to the function called by the system-func function. The value of this parameter can be -1 .

varname is the name of the FOSI string variable or counter variable whose value is to be returned.

oid is the object identifier (OID) of the element in the user's document whose e-i-c is being processed



---

# framesets

# framesets

framesets ( descriptionArr , locationArr [, doc ])

The framesets function fills the descriptionArr array with frameset descriptions and the locationArr array with the paths and file names of framesets declared in the document type configuration file ( .dcf ) for the document type associated with doc . If doc is omitted or 0 , the current document is used.

The arrays are returned in the order in which the framesets are declared in the .dcf file. The function also returns the number of entries in each array. The first entry is stored at index 1.

## Related Topics

- • Framesets overview

- • Document type configuration files



---

# function_argc

# function_argc

function_argc ( name [, varname ])

The function_argc function returns the number of arguments with which function name is declared. -1 is returned if name is not a known function.

If varname is given, the minimum number of arguments is assigned to that variable. varname must be either a scalar variable or array element.

function_argc works for both built-in functions and those defined in ACL. If name is an ACL function not yet loaded but declared via autoload, function_argc will cause the function to be loaded to return the actual argument counts.

## Related Topics

- • function_file

- • function_names

- • package_file



---

# function_file

# function_file

function_file ( name [, load ])

The function_file function returns the path name of the file which defines the function name . If name is a built-in function, the string built-in is returned. If name is not a known function, function_file returns the null string.

If name is an ACL function not yet loaded but declared via autoload, function_file will return the null string by default. If the optional parameter load is specified and has a non-zero value, function_file will cause the function to be loaded to return the actual path name.

## Related Topics

- • function_argc

- • function_names

- • package_file



---

# function_names

# function_names

function_names ( arr [, package ])

The function_names function fills the array arr with a list of all functions defined in the specified package and returns the number of functions.

If package is omitted, the list of all built-in functions is returned.

## Related Topics

- • function_argc

- • function_file

- • packages



---

# generate_id

# generate_id

generate_id ( doc , oid , attrname [, text [, flags ]])

The generate_id function generates an ID and optionally adds a suffix to the ID to make it more likely that the ID will be unique. The function will generate the ID through one of the following methods:

- • Call the generate_id callback, if it is available.

- • Generate an initial ID based on title, text, and element information from the document. If a unique ID is called for, append a string to the initial ID value. The string will be a hyphen ( - ) followed by eight hexadecimal characters representing the current time and date.

The generate_id function has the following arguments.

- • doc — (Optional.) The identifier of the document for which the ID is being generated. A value of 0 (zero, the default) refers to the current document.

- • oid — (Optional.) The object identifier of the element for which the ID is being generated. When an ID is being generated in a context that does not involve a particular element, the value of oid will be oid_null( ) .

- • attrname — (Optional.) The name of the attribute for which the ID is being generated or a null string when the ID is not being generated for use as an attribute value.

- • text — (Optional.) An initial text string that can be used to help generate the ID. For example, this text could be used when the function is called without valid doc or oid arguments.

- • flags — (Optional.) A bitmask that determines whether the suffix is added to the ID.



---

# get_appdata_dir

# get_appdata_dir

get_appdata_dir ([ subpath [, flags ]])

When called with no arguments, this function returns the full path to the application data directory.

This directory typically is: C:\Documents and Settings\ <login> \Application Data\PTC\Arbortext\Editor

The APTAPPDATADIR environment variable can be used to override the default location.

- • subpath — Optional. A relative directory structure such as onedir\twodir . When subpath is given, the function returns a full path to the given subpath of the application data directory.

- • flags — Optional directory options. The following bit values are supported in the flags parameter.

If errors are encountered, the return value will be an empty string and main::ERROR will be contain an error message.

Example:

```
path = get_appdata_dir('acme/customizations', 0x01);
```

## Related Topics

- • appdata predefined variable



---

# get_cache_dir

# get_cache_dir

get_cache_dir ()

Returns the location of the Arbortext Editor cache directory ( .aptcache ).

## Related Topics

- • Cache directory (.aptcache)

- • APTCACHE — Specifying alternate directory for auxiliary files for formatter

- • clean_cache



---

# get_composer_log_contents

# get_composer_log_contents

get_composer_log_contents ([ html ])

The get_composer_log_contents function returns the contents of the log file associated with the last publish operation as a formatted multiline string. If the html parameter is present and non-zero, the string is HTML wrapped in a pre element.

## Related Topics

- • XSL stylesheet error handling during publishing

- • get_composer_log_doc function

- • composer_log function

- • show_composer_log function



---

# get_composer_log_doc

# get_composer_log_doc

get_composer_log_doc ( )

The get_composer_log_doc function returns the ID of the read-only document containing the log output from the last publish operation.

## Related Topics

- • XSL stylesheet error handling during publishing

- • get_composer_log_contents function

- • composer_log function

- • show_composer_log function



---

# get_custom_dir

# get_custom_dir

get_custom_dir ([ app_or_index ])

The get_custom_dir function returns the full path of the directory in which a given application is installed. An application is not required to be installed inside the Arbortext Editor or Arbortext Publishing Engine install tree, as long as you use the APTAPPLICATION or APTCUSTOM environment variable to specify another path or path list to search for custom applications (using a file system specification for APTAPPLICATION ; HTTP references are not supported).

In cases where APTCUSTOM cites a zipped custom directory, application, or CMS adapter, get_custom_directory returns a full path to the locally expanded form of the zipped customization. The expanded form is stored in the Arbortext Editor cache ( .aptcache\zc ) directory. For example, if APTCUSTOM is set to the following value:

```
http://server/apps/custom.zip
```

The get_custom_directory function returns a path similar to the following value:

```
C:\Documents and Settings\
user
\Local Settings\
Application Data\PTC\Arbortext\Editor\.aptcache\zc\1
```

If APTCUSTOM points to a zipped application called com.acme.app and is set to the following value:

```
http://server/apps/app.zip
```

The get_custom_directory(com.acme.app) function returns a path similar to the following value:

```
C:\Documents and Settings\
user
\Local Settings\
Application Data\PTC\Arbortext\Editor\.aptcache\zc\3\com.acme.app
```

The app_or_index parameter is optional; if omitted, 0 is assumed. If specified, it can be one of the following:

- • The application's uniquely named directory (usually a Java class name, such as com.arbortext.sample ).

- • An integer greater than or equal to zero.

- • A negative integer.

## Related Topics

- • Cache directory (.aptcache)

- • get_custom_property function

- • get_user_property function

- • application_name function



---

# get_custom_property

# get_custom_property

get_custom_property ( key [, default ])

The get_custom_property function retrieves the value of a global parameter or variable that has been configured in an application.xml file.

The function returns the value for the name of the variable or other property specified by key . The return value is the Unicode string associated with the specified key (as defined in the application.xml file). This value may be an empty string if no value is configured. Specify key using the following format:

```
application.qualified.name.property-name
```

For example, if the application's unique full name is com.arbortext.sample and the preference name specified in application.xml is Color , then you would specify com.arbortext.sample.Color .

The optional default parameter specifies a value to substitute if the key parameter name is not specified in the application.xml file. If there is no matching parameter for the specified key as defined by application.xml , the default parameter value (if specified) will be returned instead.

## Related Topics

- • get_custom_dir function

- • get_user_property function

- • application_name function



---

# get_default_printer

# get_default_printer

get_default_printer ()

This function returns the name of the default printer, or the empty string if no default printer is available.



---

# get_newlist_entry

# get_newlist_entry

get_newlist_entry ( entry , array[] )

Given a new dialog entry (name, description, or path), this function returns an associative array containing information about the entry. The function return code is 1 for success, 0 for failure.

- • entry — String indication entry. It is the base name of the document type DTD (e.g. article), the full DTD path (for example, APTPATH /doctypes/article/axdocbook.dtd ), or the description that appears in the New Document dialog box (for example, Arbortext XML DocBook V4.0 ).

- • array — Associative array that will contain entry information on success. The indexes are:



---

# get_num_printers

# get_num_printers

get_num_printers ()

This function returns the number of available printers. This number is determined by querying the operating system for the set of installed printers.



---

# get_preferences_path

# get_preferences_path

get_preferences_path ([ write ])

This function returns the path name of the user's preferences file. If the optional write parameter is present and not zero, the function returns the path name that will be used to write the preferences file. This may be different than the path name used to read the preferences file if an upgrade has been performed. For example, an old epic.wcf may still be read and a new arbortext.wcf may be written to.

## Related Topics

- • write_preferences function



---

# get_printers

# get_printers

get_printers ( (printers[]) )

This function populates the array 'printers' with the names of the available printers.This list is determined by querying the operating system for the set of installed printers.



---

# get_user_property

# get_user_property

get_user_property ( key [, default ])

The get_user_property function returns the value for a property that has been set in one of the following ways:

- • a value specified by the set_user_property function .

- • a value subsequently stored in the arbortext.wcf preferences file after being set initially by the set_user_property function.

The return value is the Unicode string associated with the user preference or other property specified by key . This value may be an empty string if no value is configured.

Specify key using the following format:

```
application.qualified.name.property-name
```

For example, if an application's fully qualified name is com.arbortext.sample and the user setting is windowVisible , then you would specify the key parameter as com.arbortext.sample.windowVisible .

The optional default parameter specifies the value to substitute if the key parameter name is not specified. If there is no matching parameter, the default parameter value (if any) will be returned if specified.

## Related Topics

- • set_user_property function

- • get_custom_dir function

- • get_custom_property function

- • application_name function



---

# getline

# getline

getline ( fid [, varname ])



This function reads the next line from the file associated with the file identifier fid , which must be a return value from a previous call to open .

fid must refer to a file that was opened for reading.

varname must be either a scalar variable or an array element. If varname is given, then the line is placed in the variable by that name. The return value in this case is the number of characters read. If the end of the file is reached before reading any characters, getline returns 0 and sets varname to the null string. If varname is not given, then getline returns the line or a null string if the end of file has been reached.

- • getline does not remove the terminating newline character. If desired, use the function chop to do this.

- • getline has an internal limit of 3000 characters. If a newline character is not found within the limit, then that many characters are returned without the terminating newline character.

- • getline does not support reading lines that contain null characters (\000), that is, binary data, because it is implemented using the C language function fgets . The read function can be used to read binary data.

Examples

The following is an example of a function to copy one file to another, using getline and put :

```
function fid_copy(from, to)
{
local inf, outf, line
inf = open(from, "r")
if (inf < 0) {
eval "Couldn't open file for read:", from
return 0
}
outf = open(to, "w")
if (outf < 0) {
close(inf)
eval "Couldn't open file for write:", to
return 0
}
while (getline(inf, line)) {
put(outf, line)
}
close(outf)
close(inf)
return 1; # True
}
```

## Related Topics

- • close built-in function

- • open built-in function

- • put built-in function

- • read built-in function



---

# getlocale

# getlocale

getlocale ([ full ])

This function returns a string of the current system locale name. You will need the system locale if you are creating localized message files.

If the optional full parameter is present and non-zero, the function returns the full locale name (for example, English_United States.1252 ) as opposed to the shorter form of the locale name (for example, ENU ).

Execute the command below at the Arbortext Editor command line to display the system locale name.

```
eval getlocale()
```

## Related topis

- • cjk_locale function



---

# getpid

# getpid

getpid ( )



This function returns Arbortext Editor process ID which can be used for constructing unique file names.



---

# glob

# glob

glob ( filepat [, arr ])

This function fills the array arr with a list of file names that match the pattern specified by filepat . It returns the number of files matching the pattern or zero if nothing matched. The file names are returned in alphabetical order.

Currently, if the file pattern contains any directory components, only the last component may contain the file match patterns *, ? and [].

Examples

```
glob("*.sgm", doclist)
```



---

# goto_cell

# goto_cell

goto_cell ( row , col )



This function moves the cursor to the end of the cell given by row , col where the upper left cell is at row 1 , column 1. Returns 1 if successful, 0 if there is no such cell in the current table, or -1 if the cursor is not in a table.

## Related Topics

- • insert built-in function

- • insert_column command

- • insert_row command

- • tbl_caret_col built-in function

- • tbl_caret_row built-in function

- • tbl_col_count built-in function

- • tbl_row_count built-in function



---

# goto_oid

# goto_oid

goto_oid ( oid [, pos ])

This OID function moves the cursor to the position given by oid , pos . goto_oid does not reposition the screen when moving the cursor.

pos can be any of the following values:

- • -1 — The cursor is placed immediately before the end tag of the element identified by oid .

- • -2 — The cursor is placed immediately before the start tag.

- • -3 — If oid is a start tag the cursor is placed immediately after the end tag. Otherwise the cursor is placed at the end of the object.

If pos is omitted, the cursor is placed after the start tag identified by oid .

## Related Topics

- • caret command

- • scroll_to_oid built-in function



---

# graphic_attr_name

# graphic_attr_name

graphic_attr_name ( tagname , role [, doc ])

This function returns the name of the graphic tagname attribute for the graphic trait role defined in the document type's .dcf file .

The optional doc argument specifies the identifier of the document to query. If omitted or 0 , the current document is used.

Valid values for role correspond to graphic element attributes that are set in the document type's .dcf file. The following table associates the valid values for role to the graphic attributes in the .dcf file.

If tagname is not defined as a graphic element in the .dcf file, or if no attribute is assigned to the specified role , this function returns the null string.

## Related Topics

- • graphic_entity_attr_name function

- • graphic_file_attr_name function

- • Enabling graphics support for a document type



---

# graphic_entity_attr_name

# graphic_entity_attr_name

graphic_entity_attr_name ( tagname [, doc ])

This function returns the name of the graphic entity attribute for the graphic element specified by tagname that is defined in the document type's .dcf file . If an entity attribute is not defined for the tagname element, graphic_entity_attr_name returns the null string. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

## Related Topics

- • graphic_attr_name function

- • Enabling graphics support for a document type



---

# graphic_entity_names

# graphic_entity_names

graphic_entity_names ( arr [, doc ])



The graphic_entity_names function fills the array arr with an alphabetical list of graphic entity names that are valid for the current document, returning the total number. The first name returned is stored at index 1. All previous elements in arr are discarded.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# graphic_entity_tag

# graphic_entity_tag

graphic_entity_tag ( tagname [, doc ])



This function returns 1 (true) if the tag specified by tagname represents an SGML graphic entity declaration. The doc argument specifies the identifier of the document tree to query. If doc is omitted or 0 , the current document is used.



---

# graphic_file_attr_name

# graphic_file_attr_name

graphic_file_attr_name ( tagname [, doc ])

This function returns the name of the graphic file name attribute for the graphic tag specified by tagname . If there is no file name attribute defined for tagname , graphic_file_attr_name returns the null string. The doc argument specifies the identifier of the document tree to query. If doc is omitted or 0 , the current document is used.

The function graphic_attr_name( tagname , "filename") function returns the same value as the graphic_file_attr_name( tagname ) function.

## Related Topics

- • graphic_attr_name function

- • graphic_entity_attr_name function

- • Enabling graphics support for a document type



---

# graphic_format

# graphic_format

graphic_format ( path )

This function returns the graphic file format of the graphic identified by the path parameter. The value path must be the absolute path to a graphics file. If the path does not identify a graphic, the function returns an empty string.

The returned value can be one of the following formats:

- • sunbm — Sun Bitmap

- • xbm — X Bitmap

- • eps — Encapsulated PostScript file

- • cur — Windows Cursor file

- • drw — IslandDraw DRW file

- • sunicon — Sun Icon file

- • tif — Tag Image File Format

- • drwunc — IslandDraw DRAW file (not compressed)

- • png — Portable Network Graphics

- • wmf — Windows metafile

- • icon — Windows icon

- • pcx — PC Paintbrush File Format

- • bmp — Windows Bitmap

- • cgm — Computer Graphics Metafile

- • gif — Graphic Interchange Format

- • jpg — Joint Photographic Exports Group

- • calsG4 — CALS raster (G4)

- • svg — Scalable Vector Graphics

- • idr — Arbortext IsoDraw file

- • idrz — Arbortext IsoDraw file

- • iso — Arbortext IsoDraw file

- • isoz — Arbortext IsoDraw file

- • edz — Creo View file

- • pvz — Creo View file

## Related Topics

- • oid_graphic_format function



---

# graphic_information

# graphic_information

graphic_information ( image , arr )



This function fills the array arr with a list of attributes of the specified graphic, image , where image is the full path and file name of the graphic. graphic_information returns 1 if image exists, otherwise, it returns 0 .

arr is filled with the following values:

- • arr[' format '] contains the name of the graphic format. If Arbortext Editor does not recognize the format, arr[' format '] will be unknown .

- • arr[' resolution '] contains the resolution value (in dpi) if the file has a specified resolution. Otherwise, arr[' resolution '] contains 0 .

- • arr[' width '] contains the width of the image.

- • arr[' height '] contains the height of the image.



---

# graphic_relative_path

# graphic_relative_path

graphic_relative_path ( path [, doc ])

This function converts the absolute path name given by path into a relative path name if possible. If the graphic file is in or below the same directory as the document doc , then a path name relative to the document directory is returned. If the file name is located within a directory given by the graphicspath option, or a subdirectory of a directory given by the graphicspath option, then the base name is returned. Otherwise, the input path name is returned.

If doc is zero or omitted, the current document is used.

This function is used by oid_set_graphic_pathname and insert_graphic_file functions when storing a graphic file reference.

## Related Topics

- • insert_graphic_file function

- • oid_set_graphic_pathname function

- • set graphicspath option



---

# graphic_tag

# graphic_tag

graphic_tag ( tagname [, doc ])

This function returns 1 if the tag tagname is declared as a graphic element in the .dcf file for the document type associated with doc . If doc is omitted or 0 , the current document is used.



---

# graphic_tag_name

# graphic_tag_name

graphic_tag_name ([ doc [, flags ]])

This function returns the name of the primary graphic element defined in the document type's .dcf file or .style file for the document specified by doc . The function returns the null string if no graphic tag was designated for the document type or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

The following flags can be set:



---

# graphic_viewer

# graphic_viewer

graphic_viewer ( path )

This function returns the name of the embedded ActiveX dialog used to display the intelligent graphic identified by path . The value of path must be an absolute directory path.

If the intelligent graphic is an EDZ graphic and displayed by ProductView, the function returns pview . If the intelligent graphic is an ISO graphic and displayed by Arbortext IsoView , the function returns iview . If path does not reference an intelligent graphic, the function returns an empty string.

## Related Topics

- • Intelligent graphics overview

- • oid_graphic_viewer function



---

# graphic_views

# graphic_views

graphic_views ( path , arr )

This function fills the array arr with all of the views that are defined in the intelligent graphic file identified by path . A view is a custom display of the intelligent graphic that was created and saved inside of the graphic. If path exists and is an intelligent graphic file, the function returns the size of the array. If path does not exist or is not an intelligent graphic file, the function returns 0 .

The value of path must be an absolute directory path.

## Related Topics

- • Intelligent graphics overview

- • PTC server connection overview

- • graphic_information



---

# gsub

# gsub

gsub ( regexp , repl [, string , lvalue ])



This function globally replaces all substrings of string that match the regular expression regexpr and replaces the substring with the string repl . The resulting string is assigned to lvalue , which must be a variable name or array element. If string is omitted, then the value of lvalue is used as the source string. When copying the string to lvalue , the part that was matched by regexpr is replaced according to the string repl .

If repl contains a “&” or “\0”, then it is replaced with the substring that matched regexpr . If repl contains a “\ n ”, where n is a digit between 1 and 9, then it is replaced with the substring that matched the n th parenthesized subexpression of regexpr . n must not be greater than the number of parenthesized expressions in regexpr .

gsub returns the number of substrings that were replaced or 0 if no match occurred. The lvalue is not changed if 0 is returned.

Examples

For the example, where $x = "this":

```
gsub('t', 'T', $x), $x results in "This".
```

In another example, after

```
gsub('\((a)(b)\)', '(\2\1)', "(ab)c(ab)c", $r)
is executed, the value of $r is (ba)c(ba)c.
```

## Related topic

Using regular expressions



---

# hex

# hex

hex ( expr )



This function returns the decimal value of expr interpreted as a hex string. For example, the value of hex("f") is 15 .



---

# hidden_tag

# hidden_tag

hidden_tag ( tagname [, doc ])

This function returns 1 if the tag specified by tagname is declared as a hidden element in the document type configuration file ( .dcf ) for the document type associated with doc . If doc is 0 or omitted, the current document is used.

A hidden tag is one that does not display in Arbortext Editor dialog boxes that provide lists of DTD tags , such as the Find Tag/Attribute dialog box ). However, a hidden tag is returned when you request a list of elements in a document type are requested (for example, when calling the tag_names function ). Also, hidden tags are automatically excluded by the exclude_tag callback .

## Related Topics

- • Document type configuration files

- • Suppressing the display of tags in Arbortext Editor dialog boxes

- • set showscreenhiddenattrs command



---

# high_bound

# high_bound

high_bound ( arr )

This function returns the maximum subscript allowed for the array arr . If the array was not declared a fixed size with the local or global statement, then high_bound returns the highest subscript used. If arr is an associative array, the function returns a null string.



---

# hook_call

# hook_call

hook_call ( name [, arg1 [, arg2 … ]])

This function calls the ACL hook function specified by name . The remaining arguments, if any, are passed to the hook function.

The function returns 0 if all functions on the hook function list succeed, -1 if a function in the hook function list aborts the operation, and -2 if there is an error.

Example

```
hook_call("preferencehook", win)
```



---

# hook_eval

# hook_eval

hook_eval ( hookname [, arg1 [, arg2 … ]])

This function calls the ACL hook function specified by hookname . The remaining arguments, if any, are passed to the hook function.

The function returns the value returned by the called hook function. If more than one function is registered for the hook, hook_eval returns the return value of the last function called.

Example:

```
newpath = hook_eval("graphicpathhook", graphicfile, oid)
```

## Related Topics

- • hook_call function

- • add_hook function

- • remove_hook function



---

# htmldoc

# htmldoc

htmldoc ( doc [, source_loc [, css_mode [, encodingstring ]]])

This function creates, in memory, a virtual HTML document conforming to the html DTD. The generated document is based on the current FOSI. It uses the print FOSI, if set. If a print FOSI is not set, it uses the Editor FOSI.

Upon successful completion, it returns the document ID for the virtual HTML document. If an error occurs, it returns a -1 .

The document identifier doc specifies the source document.

Set source_loc to 1 (true) to add the srctreeloc attribute to the elements in the virtual HTML document. The srctreeloc attribute value is a tree location string indicating the element's location in the source document. The default is 0 .

Specify css_mode to set the level of Cascading Stylesheet (CSS) information you want to incorporate in the HTML document. Following are the valid parameters and what they generate:

- • 0 — No CSS mode. Generates HTML without any CSS style or class information. This is the default.

- • 1 — CSS style. Generates HTML with CSS properties specified within the style attribute of various HTML elements, but no classes are defined or used.

- • 2 — CSS classes. Generates HTML with CSS properties specified by classes only. These classes are defined within the content of the HTML <style> element, and are referred to within the class attribute of various HTML elements.

- • 3 — CSS style and classes. Generates HTML with CSS properties specified by classes that are defined within the HTML <style> element, and augmented by CSS properties specified within the style attribute of various HTML elements.

Set encoding to a string that specifies the encoding for the HTML document. The following encodings are supported:

- • ISO-8859-1

- • ISO-8859-2

- • ISO-8859-5

- • ISO-8859-7

- • ISO-8859-9

- • Windows-1252

- • UTF-8

To display the HTML document, create a new window and perform a doc_show using the document ID that was returned.

## Related Topics

- • htmlimginserthook



---

# http_cache_flush

# http_cache_flush

http_cache_flush ([ url ])

http_cache_flush clears one or more files from the URL cache . If the optional url parameter is omitted, the function clears the entire URL cache except for any WebDAV URLs that are currently locked. If the optional url parameter is provided, the function removes the file corresponding to the specified URL (unless it is a WebDAV URL that is currently locked). The url parameter must be included as the remote URL reference and not the actual file name within the local URL cache.

http_cache_flush returns one ( 1 ) on success. If the optional url parameter is provided but does not correspond to any file in the URL cache, http_cache_flush returns a zero ( 0 ).

The following example removes all files from the URL cache and stores the return value in the $ret variable:

```
$ret = http_cache_flush()
```

The following example removes the cached file for the URL http://www.company.com/files/plan.ent and stores the return value in the $ret variable:

```
$ret = http_cache_flush("http://www.company.com/files/plan.ent")
```

## Related Topics

- • Managing the URL cache



---

# in_context

# in_context

in_context ( tagname [, doc [, flags ]])



This function determines if the tag specified by tagname can be inserted at the cursor. If markup is selected, this function determines if the tag can be inserted surrounding the selected markup.

- • The tagname string may be delimited by the start and end tag delimiters ( < and > ) but need not be in most cases. Special cases include the following:

- • The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

- • The flags parameter is an optional bitmask 0x001 , which takes auto-insertions into account (those specified by InsertAroundToFix in the .dcf file). If flags is not supplied, 0 is used.

in_context returns one of the following integers:

- • 0 — The tag cannot be inserted.

- • 1 — The tag can be inserted.

- • 2 — The tag can be inserted after modifications. For example, after adding required tags.



---

# in_context_list

# in_context_list

in_context_list ( arr [, ct [, oid [, pos [, filter [, alias ]]]]])



This function fills the array arr with a list of element names that are valid for insert_tag (or change_tag if ct is 1 ) at the point given by oid , pos . If oid is omitted, the cursor position in the current document is used. in_context_list returns the number of elements stored in an array.

If the optional parameter filter is given and non-zero, the exclude_tag callback is called to remove undesired entries from the context list. To skip the exclude_tag callback, either omit the filter parameter or set it to zero.

If the optional parameter alias is passed the value 1 , in_context_list returns the alias names instead of the actual names of the elements allowed in the current context. By default, alias is 0 .

## Related Topics

- • The doc_add_callback function exclude_tag callback



---

# index

# index

index ( s1 , s2 )



This function returns the position in string s1 of the first occurrence of string s2 , based at 1 . If the substring is not found, 0 is returned. For example, the value of index("rnotes9302", "9302") would be 7 .



---

# indexproc

# indexproc

indexproc ( view_id , userule_id , userule_parameter )

This function is useful when used with the userulehook if you wish to alter the preliminary index before index processing, and/or alter the final index after index processing.

These three arguments to indexproc are the same first three values that are passed to the userulehook function.



---

# init_done

# init_done

init_done ( )



This function returns 1 (True) if initialization has completed. Only a subset of commands are legal before initialization is finished.



---

# insert

# insert

insert ( string [, dest ])



This function inserts the string value of the expression string into the destination specified by dest , which is either a document identifier or a window name. If omitted, the current document is used. It can be one of the window types returned by the window function (for example, edit , cmd , helpwin1 ).

string is interpreted as an SGML -coded string unless the destination window contains an ASCII document-type. Tabs and 8–bit characters are not stripped from text inserted into help windows using this function.

An example of this function is:

```
insert("find", window_doc(" cmd"))
```

This function is similar to the insert_string -sgml command except that the string argument may be an expression, it is not limited in size, and does not replace any text that might be selected.

This function interprets the processing instruction <?Pub Caret> to set the cursor to a specific position within the inserted fragment. The <?Pub Caret> must come after a character or tag in the SGML - or XML-coded string. If the <?Pub Caret> processing instruction is not included in the string, the cursor is placed according to the following rules:

- • If the cursor is in the Edit view, the cursor is placed after the inserted string.

- • If the cursor is in the Document Map view, the cursor is placed before the inserted string, though you can control this behavior with the set docmappastecaret=off option.

The insert function will not do a pending delete regardless of the setting of set pendingdelete .

## Related Topics

- • insert_string command

- • window_doc built-in function

- • set docmappastecaret command



---

# insert_buffer

# insert_buffer

insert_buffer ( string , markup [, buffer [, append ]])

This function inserts the string value of the expression string into the paste buffer named by buffer , or if not specified, the default paste buffer. If the value of markup is not 0 , then the string is interpreted as an XML (or SGML) string. Otherwise no markup is recognized.

If the value of append is not specified or is non-zero, the string is appended to the buffer. Otherwise, the string replaces the contents of the buffer.



---

# insert_filep_entity

# insert_filep_entity

insert_filep_entity ( name )

This function provides a reference to an existing file parameter entity (that is, an external parameter entity), which is then used in the current document's internal subset.

name is the name of the entity. A leading percent sign % is optional. If the entity has not already been declared, an error message is displayed.

The reference is added in the subset immediately after the declaration of the same entity. For example, if %myent has already been declared after the function call

```
insert_filep_entity("myent")
```

the document's SGML file will contain this:

```
<!ENTITY % myent SYSTEM "/usr/myent">
%myent;
```

## Related Topics

- • add_filep_entity function

- • declare_filep_entity function

- • delete_filep_entity function



---

# insert_graphic_file

# insert_graphic_file

insert_graphic_file ( path [, tagname [, doc ]])

This function inserts the graphic tag specified by tagname at the cursor and sets the appropriate file or entity reference attribute to the file name specified by path . If tagname is not specified, a prompt dialog is displayed listing all the graphic tags (as declared in the .dcf file) that are valid at the current location. If only one graphic element is valid, then that is used without prompting. If no graphic elements are valid (or are declared in the .dcf file), the function returns 0 (False). The function returns 1 (True) if the graphic reference was successfully inserted.

If doc is zero or omitted, the current document is used.

The path parameter is set using the oid_set_graphic_pathname function and stored as a relative path name if possible, as determined by the graphic_relative_path function.

## Related Topics

- • insert_graphic command

- • insert_graphic_entity command

- • oid_set_graphic_pathname function

- • graphic_relative_path function



---

# insert_pi

# insert_pi

insert_pi ( contents [, doc [, showErr ]])

This function inserts a generic processing instruction with the given contents . In Arbortext Editor , a processing instruction is represented with a _pi element. If doc is not supplied or is 0 , then the current document is used. If showErr is supplied and is not 0 , then any errors from the operation are reported.

The function returns 1 if the processing instruction is inserted successfully. Otherwise, 0 is returned.



---

# insert_string_(Function)

# insert_string (Function)

insert_string ( string [, dest ])

This function inserts the string value of the expression string into the destination specified by dest , which is either a document identifier or a window name. The window can be one of the window types returned by the window function. (For example, edit or cmd .)

string specifies the text to be inserted at the cursor location. No markup is recognized in the string; the characters are inserted as-is. If dest is omitted, the current document is used.

This function is similar to the insert_string command, except its string argument may be an expression and it is not limited in size.

Unlike the insert function, insert_string obeys the setting of the set pendingdelete option.



---

# insert_symbol

# insert_symbol

ret = insert_symbol ( code [, font [, doc ]])

This function inserts the character specified by code into the document specified by doc (or the current document if doc is 0 or not supplied). If the font parameter is supplied, a touchup processing instruction specifying the given font will be inserted if necessary.

The function returns 1 on success and 0 if it fails to insert the character.



---

# insert_tag_(Function)

# insert_tag (Function)

insert_tag ( tagname [, dest [, noprompt ]])

This function inserts an element into the destination specified by dest .

- • tagname — An expression specifying the element to insert.

- • dest — Optional. A document identifier or a window name. It can be one of the window types returned by the window function (for example, edit , cmd , helpwin1 ). If dest is not specified, the current document is used.

- • noprompt — Optional. If set to a value of 1 , any prompts due to the promptattrs , requireattrs , and promptgraphicbrowser set options are suppressed.

This function returns one ( 1 ) on success and zero ( 0 ) on failure.

Example:

```
insert_tag("emphasis", window_doc("edit"),1)
```

## Related Topics

- • insert_tag command



---

# inside_tag

# inside_tag

inside_tag ( tagname [, doc ])

This function returns 1 (True) if the cursor is within the tag pair whose start-tag is named tagname , regardless of level. If the cursor is not within this tag pair, 0 is returned.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# interpreter_addr

# interpreter_addr

interpreter_addr ( )

The interpreter_addr function returns the address of the Arbortext Command Language interpreter as an integer. This address may be passed to a dynamically loaded function using dl_call to allow such functions to call back into Arbortext Editor to execute an Arbortext Command Language string.

The interpreter takes a single argument, the string to execute, and returns 1 if the command was executed successfully, or 0 if it failed.

Following is an example of some C functions that might be part of a dynamically loaded library.

```
typedef unsigned int (*CMDFUNC) ();
CMDFUNC acl_interp;
void set_acl_addr(void *addr)
{
acl_interp = (CMDFUNC) addr;
}
int aclcmd(char *str)
{
if (acl_interp)
return (*acl_interp)(str);
fprintf(stderr, "set_acl_addr() must be \
called first.\n");
return 0;
}
```

The interpreter address is passed to the library as follows:

```
local set_acl_addr = dl_find(hdll, "set_acl_addr");
dl_call(set_acl_addr, interpreter_addr());
```



---

# is_postscript_printer

# is_postscript_printer

is_postscript_printer ( printer )

This function returns 0 (false) or 1 (true), depending on whether the specified printer is a PostScript printer. The printer driver is interrogated to determine whether it renders PostScript output. If the printer is not found, this function returns false.



---

# item_tag

# item_tag

item_tag ( tagname [, doc ])

This function returns 1 (true) if the tag named tagname is declared as an item element in the .dcf file for the document type associated with doc . If doc is omitted or 0 , the current document is used.

## Related Topics

- • list_tag



---

# ixkey_charent

# ixkey_charent

ixkey_charent ( oid )

This is useful if the ixkeycharent hook does some examination and decides it would like to use the built-in processing. The oid parameter is the oid of the character entity reference entity name.



---

# java_array_from_acl

# java_array_from_acl

java_array_from_acl ( arr , descriptor )

This function converts the ACL array arr to a Java object and returns the Java object. The class of the Java object is specified by the descriptor .

The arr is an ACL array. It can be a normal array or an associative array, depending on the value of the descriptor .

The descriptor is either a fully-qualified class name, such as java.util.HashMap , or a class descriptor, such as java/util/HashMap or [I . The class descriptor follows Oracle’s Java Native Interface Specification. descriptor must be the name or the descriptor of one of the following classes:

- • A class that implements the java.util.Map interface. For example:

- • A class that implements the java.util.List interface. For example:

- • A one dimensional primitive type array. The arr must be an ACL normal array.

- • A one dimensional String array.

This function returns the newly created Java object. It returns 0 if the array conversion failed.

```
local arr[];
# Create an ACL associative array
arr["cereal"] = "breakfast";
arr["steak"] = "dinner";
# Convert the ACL array to a HashMap object
local obj = java_array_from_acl(arr, "java/util/HashMap");
if (obj != 0) {
# Get the size of this HashMap object
response("size = " . java_instance(obj, "size"));
java_delete(obj);
}
```

## Related Topics

- • java_array_to_acl function

- • java_static function

- • java_constructor function

- • java_instance function



---

# java_array_to_acl

# java_array_to_acl

java_array_to_acl ( obj , arr )

This function converts the Java object obj to the ACL array arr . All previous elements in the arr are discarded.

The obj parameter is a Java object. It belongs to one of the following classes:

- • A class that implements the java.util.Map interface. For example:

- • A class that implements the java.util.List interface. For example:

- • A one dimensional primitive type array.

- • A one dimensional String array.

Each element in the obj can be any Java object. Java String objects will be directly converted to ACL values. Other Java objects will be turned into Java String objects by using the Java toString method before converting to ACL values.

This function returns the size of the arr after the conversion. It returns -1 if the conversion failed.

```
# Create an ArrayList object
local obj = java_constructor("java.util.ArrayList");
java_instance(obj, "add", "English");
java_instance(obj, "add", "French");
local arr[];
local i;
# Convert the ArrayList object to an ACL array
local size = java_array_to_acl(obj, arr);
java_delete(obj);
for (i = 1; i <= size; i++) {
response("item " . i . " = " . arr[i]);
}
```

## Related Topics

- • java_array_from_acl function

- • java_static function

- • java_constructor function

- • java_instance function



---

# java_console

# java_console

java_console ([ show [, geometry ]])

If the show parameter is non-zero or omitted, this function displays the Java Console window. If show is 0 , it closes the Java Console.

You can specify the size and position of the Java Console window using the geometry parameter. The geometry parameter is a string of the form WxH+X+Y, where W and H are the width and height of the window in pixels, and X and Y give the location of the upper left corner of the window. Negative X and Y values give the location of lower right corner of the window with respect to the bottom right corner of the screen. The format of the string allows just the width and height or position to be set by omitting fields. If the Java Console is already displayed, then you can change the size and position of the window by specifying geometry .

For example,

```
java_console(1, "500x300-50-50")
java_console(1, "+3+3")
java_console(0)
```

## Related Topics

- • java_init function



---

# java_constructor

# java_constructor

ret = java_constructor ( class [, arg1 [, arg2 [, arg3 [, ...arg20 ]]]])

This function creates a Java object by calling class and passing it the provided arguments arg1 , arg2 , arg3 , and so on. Up to 20 arguments can be passed to the called class . The value returned by the java_constructor function is the object created by the called constructor.

## Related Topics

- • java_constructor_modal function

- • java_delete function

- • java_instance function

- • java_static function

- • set javaclasspath command



---

# java_constructor_modal

# java_constructor_modal

ret = java_constructor_modal ( class [, arg1 [, arg2 [, arg3 [, ...arg20 ]]]])

This function is identical to the java_constructor function except that Arbortext Editor creates a new thread for the Java call and puts itself in a mode as if a modal dialog box is displayed. The primary advantage to this function is that the Arbortext Editor window will be able to refresh while the Java call is running. The disadvantage of this function is that it is significantly slower than using the java_constructor function.

This function creates a Java object by calling class and passing it the provided arguments arg1 , arg2 , arg3 , and so on. Up to 20 arguments can be passed to the called class . The value returned by the java_constructor function is the object created by the called constructor.

## Related Topics

- • java_constructor function

- • java_delete function

- • java_instance function

- • java_static function

- • append_javaclass_path function

- • set javaclasspath command



---

# java_delete

# java_delete

java_delete ( javaobject )

This function deletes a Java object reference returned by one of the following functions:

- • java_constructor function

- • java_constructor_modal function

- • java_instance function

- • java_instance_modal function

- • java_static function

- • java_static_modal function

Use java_delete to remove Java object references that are no longer needed. If you do not delete these references, memory leaks may occur.

```
object = java_constructor("Document", filename)
count = java_instance(object, "countElements")
# the object is no longer in use, delete it
java_delete(object)
```



---

# java_init

# java_init

java_init ([ init ])

This function returns 1 (true) if the Java Virtual Machine (JVM) has been initialized. It returns 0 if the JVM has not been started.

If init is specified and non-zero, the JVM is initialized, if necessary. In this case, java_init will return 1 if the JVM is initialized successfully, or 0 if it failed to initialize.

For example,

```
inited=java_init()
java_init(1)
```

## Related Topics

- • java_static function

- • java_static_modal function

- • java_constructor function

- • java_instance function



---

# java_instance

# java_instance

ret = java_instance ( object , method [, arg1 [, arg2 [, arg3 [, ...arg20 ]]]])

This function executes Java code by calling method within object and passing it the provided arguments arg1 , arg2 , arg3 , and so on. Up to 20 arguments can be passed to the called method . The value returned by the java_instance function is the returned value from the called method .

The called method must be an instance method. Use the java_static function to call static methods and the java_constructor function to call a constructor. When Java objects are no longer in use, you need to explicitly delete them by using the java_delete

## Related Topics

- • java_instance_modal function

- • java_constructor function

- • java_delete function

- • java_static function

- • append_javaclass_path function

- • set javaclasspath command



---

# java_instance_modal

# java_instance_modal

ret = java_instance_modal ( object , method [, arg1 [, arg2 [, arg3 [, ...arg20 ]]]])

This function is identical to the java_instance function except that Arbortext Editor creates a new thread for the Java call and puts itself in a mode as if a modal dialog box is displayed. The primary advantage to this function is that the Arbortext Editor window will be able to refresh while the Java call is running. The disadvantage of this function is that it is significantly slower than using the java_instance function.

This function executes Java code by calling method within object and passing it the provided arguments arg1 , arg2 , arg3 , and so on. Up to 20 arguments can be passed to the called method . The value returned by the java_instance function is the returned value from the called method .

The called method must be an instance method. Use the java_static function to call static methods and the java_constructor function to call a constructor.

## Related Topics

- • java_instance function

- • java_constructor function

- • java_static function

- • append_javaclass_path function

- • set javaclasspath command



---

# java_static

# java_static

ret = java_static ( class , method [, arg1 [, arg2 [, arg3 [, ...arg20 ]]]])

This function executes Java code by calling the static method called method within class and passing the arguments arg1 , arg2 , arg3 , and so on. Up to 20 arguments can be passed to the called method . You should supply the package name as part of the class name for the class parameter.

The called method must be a static method. The value returned by the java_static function is the value returned from the called method .

Use the java_instance function to call instance methods and the java_constructor function to call a constructor.

You can use the java_static function to call the Java garbage collector by following the example:

```
java_static('java.lang.System','gc');
```

## Related Topics

- • java_static_modal function

- • java_constructor function

- • java_delete function

- • java_instance function

- • append_javaclass_path function

- • set javaclasspath command



---

# java_static_modal

# java_static_modal

ret = java_static_modal ( class , method [, arg1 [, arg2 [, arg3 [, ...arg20 ]]]])

This function is identical to the java_static function except that Arbortext Editor creates a new thread for the Java call and puts itself in a mode as if a modal dialog box is displayed. The primary advantage to this function is that the Arbortext Editor window will be able to refresh while the Java call is running. The disadvantage of this function is that it is significantly slower than using the java_static function.

This function executes Java code by calling the static method called method within class and passing it the provided arguments arg1 , arg2 , arg3 , and so on. Up to 20 arguments can be passed to the called method . The value returned by the java_static function is the returned value from the called method .

The called method must be a static method. Use the java_instance function to call instance methods and the java_constructor function to call a constructor.

## Related Topics

- • java_static function

- • java_constructor function

- • java_instance function

- • append_javaclass_path function

- • set javaclasspath command



---

# javascript

# javascript

javascript ( expr [, private ])

This function sends the string expr to the JavaScript interpreter to be evaluated, returning the result as a string. By default, the JavaScript expression is evaluated in the global shared scope, so previously defined JavaScript functions are accessible. If the private parameter is specified and non-zero, the expression is evaluated in a temporary scope. As a result, top-level objects created during evaluation will be discarded on return.

The following example uses an ACL expression to create a corresponding JavaScript expression to evaluate. In this case, it calls the JavaScript Date.parse method on the current time and date as returned by the ACL time_date function, returning the number of milliseconds between the current time and date and midnight, January 1, 1970 GMT.

```
msecs = javascript('Date.parse("' . time_date() . '")')
```

The following example returns the same result as the previous example using only JavaScript. The time ACL function returns a similar result in seconds instead of milliseconds.

```
msecs = javascript('var d = new Date(); d.getTime()')
```

## Related Topics

- • js command

- • js_source function

- • source command



---

# join_(Function)

# join (Function)

join ( arr [, delim [, quote ]])

This function concatenates all the elements of the array arr and returns the string result. Each element is converted to a string and those strings are concatenated, separated by the specified delimiter string delim . If delim is omitted, then a comma is used as the separator. If delim is a null string, then no separator character is used. If an array element is undefined, for example, arr is a sparse array, then a null string is used for the element value so that adjacent delimiters will appear in the string result.

If the quote parameter is specified and non-zero, then each element string value is surrounded by double quotes ( " ), and double quote, backslash and newline characters in the value are escaped with a backslash to form a valid ACL string term. For example, the array element value a "quote" would be represented in the result string as "a \"quote\"" , if the quote was non-zero.

If arr is an associative array, then each element value is prefixed by the element's key followed by a colon. The order of the keys is unspecified.

The following example shows join reversing the effect of split :

```
local arr[];
split("1 2 3", arr);
local str = join(arr, " ");
# str is "1 2 3"
```

This example shows using join for an associative array to create a corresponding JavaScript associative array using object literal syntax:

```
color["red"] = 0xff0000;
color["green"] = 0x00ff00;
color["blue"] = 0x0000ff;
javascript("var color={" . join(color,',',1) . "}")
```

## Related topic

- • split function



---

# js_source

# js_source

js_source ( filename [, args [, private ]])

This function reads and executes the JavaScript program from filename . The optional args parameter is converted from a string to an array and passed to the script in the JavaScript arguments global object. The arguments are delimited by blanks and follow the normal quoting conventions .

If the specified file name does not contain any slashes and is not found in the current directory, the js_source function searches the list of directories in the set loadpath command . The .js extension is appended to the file name if necessary.

By default, the JavaScript program is evaluated in the global shared scope, so previously defined JavaScript functions are accessible. If the optional parameter private is specified and non-zero, the expression is evaluated in a temporary scope, so global shared scope functions are not available. As a result, top-level objects (including function definitions) created during evaluation are discarded on return. The default value is false .

Example

```
js_source("deletetags.js")
js_source("jsdoc.js","sample.js",1)
```

## Related Topics

- • source command

- • js command

- • javascript function



---

# jscript

# jscript

jscript ( expr [, window ])

This function sends the string expr to the Microsoft Windows JScript interpreter to be evaluated, returning the result as a string. If the window parameter is not specified, the JScript expression is evaluated in the global JScript script context so previously defined JScript functions are accessible.

The optional window parameter is the identifier of a XUI dialog box that has a script context. If window is provided, the script executes in that dialog box’s script context.

Example

```
name = jscript('Application.prompt("Name", "")')
```

## Related Topics

- • javascript function

- • vbscript function

- • perlscript function



---

# key_cmd

# key_cmd

key_cmd ( keyexpr [, keymap ])

This function returns the command bound to the key specified by keyexpr for the keyboard shortcut specified by keymap . keyexpr is the same as the keyname argument to the map command (for example, Control + Shift + A ). keymap is the same as the window argument to map and is a window class (for example, edit , cmd , or helpwin ), a window name as returned by the window_name function, or a user-defined keyboard shortcut denoted by the prefix character @ (for example, CTRL + S ). If keymap is omitted, the keymap associated with the current window is used.



---

# keymap_exists

# keymap_exists

keymap_exists ( name )

This function returns a value that is not zero if the keymap named name exists. This function returns a value of zero the keymap named name does not exist. name need not begin with the keymap prefix character '@'. If the keymap exists, the function actually returns 1 + the number of references to the keymap, that is, where each window that attaches the keymap is counted as one reference.



---

# languages

# languages

languages ( arr )

This function fills the associative array arr with the list of language dictionaries which are used by spell checking and the thesaurus. The array is indexed by the language name (see the set language command) and the values are the language descriptions shown by the user interface. The number of entries in the array is returned.

Example

```
$ret = languages($langs)
```

Returns the following array:

```
$langs["English"]: "English (US)"
$langs["German"]: "German (Deutsch)"
.
.
.
$langs["Catalan"]: "Catalan (CatalÀ)"
```



---

# legal_name

# legal_name

legal_name ( name [, doc [, unqualified ]])

This function determines whether a given element or attribute name name is a valid XML name. If name is a valid XML element or attribute name, this function returns 1 (True). Otherwise, this function returns 0 .

The doc argument specifies the identifier of the document to query. If omitted or 0 , the current document is used.

The unqualified argument specifies whether namespace qualified names are considered valid for XML documents. If omitted or 0 , then qualified names (a colon separating a valid prefix and a valid name) are considered valid. If 1 , then qualified names are not considered valid.



---

# length

# length

length ( string )

This function returns the length of string taken as a string. For example, the value of length("rnotes9302") is 10 .



---

# license

# license

license ( string )

This function returns a non-zero value if the capability specified by string has been licensed at your site.

The following table lists the currently supported strings and the capability each represents.

## Related Topics

- • Product options



---

# license_info

# license_info

license_info ( arr )

This function fills the array arr with the following elements that give licensing information about the current session>:

- • [1] Obsolete – empty string

- • [2] Service contract number(s).

- • [3] host owning current license

- • [4] Obsolete – empty string

- • [5] Obsolete – empty string

- • [6] Obsolete – empty string

- • [7] host name that is running the application

- • [8] GUI name, for example, Windows

- • [9] time that session started in time_date format

- • [10] license source

- • [11] Obsolete – empty string

- • [12] Obsolete – empty string

- • [13] number of (physical) processor cores

- • [14] number of processor packages (sockets)

- • [15] license type – either Floating license or Node-locked license

- • [16] host ID – the host ID unique to the system



---

# license_release

# license_release

license_release ( string )

This function releases the license for the product option specified by string . It returns 1 (true) if the license specified by string was successfully released.

The following table lists the currently supported strings and the product options they represent.

## Related Topics

- • Product options



---

# linenum

# linenum

linenum ([ doc ])



This function applies the sample line numbering application found in the samples folder of your installation directory. It looks for atipl markup in the document and specifies a set of generic attributes, clearing all others. In particular, it sets the attr1 attribute of atipl:startpage tag to the value of the number attribute. It also the sets the attr1 attribute of atipl:startline tags to the current line number. The line number is reset with every start page.

The doc parameter specifies the document to modify. The current document is assumed if this parameter is not specified.

If the operation fails the function returns 0 . If the operation succeeds then the function returns 1 .

For more detailed information on the page layout elements and their attributes, see http://www.arbortext.com/namespace/pagelayout . Refer to the Programmer's Reference for more detailed information about line numbering applications.

## Related Topics

- • set pagelayoutmarkers command

- • set protectpagelayout command

- • layout::add function

- • layout::clear function

- • layout::apply function



---

# link_idref_attr_name

# link_idref_attr_name

link_idref_attr_name ( tagname [, doc ])

This function returns the name of the IDREF attribute (for example, “linkend”) for the link tag named tagname . If no such attribute is defined for the tag, link_idref_attr_name returns the null string. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

The IDREF attribute is used by the Insert Link dialog box for document (internal) links.

## Related Topics

- • Insert Link dialog box

- • oid_id_attr_name function



---

# link_tag

# link_tag

link_tag ( tagname [, doc ])

This function returns 1 (true) if the tag named tagname is declared as a link element in the .dcf file for the document type associated with doc . If doc is omitted or 0 , the current document is used.

## Related Topics

- • link_tag_name function

- • link_uri_attr_name function



---

# link_tag_name

# link_tag_name

link_tag_name ([ doc ])

This function returns the name of the primary link element for the document type associated with doc . It returns the null string if no link tag was designated for the document type or if doc is invalid or an ASCII file. If doc is omitted or 0, the current document is used.

## Related Topics

- • link_tag function

- • link_uri_attr_name function



---

# link_uri_attr_name

# link_uri_attr_name

link_uri_attr_name ( tagname [, doc ])

This function returns the name of the Universal Resource Indicator (URI) attribute (for example, “url”) for the link tag named tagname . If no such attribute is defined for the tag, link_uri_attr_name returns the null string.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

## Related Topics

- • link_tag function

- • link_tag_name function



---

# link_valid

# link_valid

link_valid ([ back [, doc ]])

This function determines whether a link operation is valid at the current location in the document specified by doc .

The following arguments are optional:

back — if not supplied or 0, the function will test the validity of returning to the position before the previous link operation. If non-zero, it will test whether there is a link to be followed at the current location.

doc — if not supplied or 0, the current document is used. Specify an alternative document with this argument if required.

The function returns 1 if a valid link operation is possible, otherwise it returns 0.



---

# list_response

# list_response

list_response ( arr [, title [, label [, default [, verify [, help ]]]]])

This function displays a scrolling list dialog panel and returns the user's response. The null string is returned if the user selected Cancel or dismissed the panel without selecting anything. The array of choices is specified by the argument arr , which must be the name of a normal array. That is, the choices are obtained from:

arr [1].. arr [count( arr )]

The remaining arguments may all be expressions and are optional:

title specifies the window manager title for the panel.

label specifies the label displayed at the top of the scrolling list panel.

default gives the default choice and is displayed in the input field; if not specified, there is no default.

If verify is non-zero or not specified, then the user's response is restricted to the array of choices.

help is the text displayed if the user presses the Help button on the panel. If not specified, then the Help button is insensitive.

## Related Topics

- • readvar command

- • response function



---

# list_stylesheets

# list_stylesheets

list_stylesheets ( )

The list_stylesheets function returns the paths to all stylesheets in the compiled stylesheet cache. Arbortext Editor stores XSL stylesheets in this cache after they have been compiled during a publishing process. By storing these stylesheets, Arbortext Editor avoids having to recompile them during subsequent publishing runs.

You can use a path returned by this function as an argument to the clear_stylesheet function.

## Related Topics

- • clear_stylesheets function

- • Stylesheet Overview



---

# list_tag

# list_tag

list_tag ( tagname [, doc ])

This function returns 1 (true) if the tag named tagname is declared as a list element in the .dcf file for the document type associated with doc . If doc is omitted or 0 , the current document is used.

## Related Topics

- • item_tag



---

# locale_file_name

# locale_file_name

path= locale_file_name ( file [, dir ])

This function returns the location of the localized file specified by the file parameter (remember to include the extension). The optional dir parameter is available for manually specifying a directory for searching. If, for example, you specified a dir of /test , the function would search for the specified file in the following locations:

The syslocale subdirectory corresponds to the current system locale setting. You can determine the current system locale using the getlocale function. If the three-character locale directory is not found (for example, "ENU"), Arbortext Editor tries the two-character version formed by dropping the last letter (for example, "EN").

If the optional dir parameter is not specified, the function automatically substitutes the Arbortext Editor installation directory ( Arbortext-path ) for the dir parameter and searches the same set of subdirectories.

If the function executes successfully, it returns the string for the path to the desired file . If the function fails, it returns the value Arbortext-path \lib\ file , where Arbortext-path is the Arbortext Editor installation directory, and file is the value of the file argument.

Examples

```
path = locale_file_name('message.amo')
path = locale_file_name('message.amo','/test')
```

## Related Topics

- • getlocale function



---

# looking_at

# looking_at

looking_at ( regexp [, doc ])

This function returns 1 (True) if the text following the cursor matches the regular expression regexp . The regular expression is compiled with tag scanning enabled (that is, as if set tagscan=on ). Thus, looking_at("</title>") returns 1 (True) if the cursor is positioned before an end title tag.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

Because double quoted strings in expressions get interpreted for backslash escape sequences when the command is parsed, if you wish for a character not to be interpreted as a regular expression meta character, you must double the \ . For example, to match the literal character < , you would specify:

```
looking_at(“\\<”)
```

Alternatively, single quotes may be used to suppress backslash interpretation, making the following statement equivalent to the previous one.

```
looking_at('\<')
```

The set case option determines whether the case of letters is significant when performing the match. For example, if set case=off , then

```
looking_at("[aB]")
```

would match A or b as well as a or B .

## Related Topics

- • set case command

- • Using regular expressions



---

# lookup

# lookup

lookup ( word , definitions[] )

This function retrieves the definitions for the specified word . If word is empty or contains spaces, or markup is included or is not found, this function returns 0. Otherwise, the number of definitions found is returned.

definitions is a numeric indexed array containing the word part of speech and definition in the form <part-of-speech>:<definition> .



---

# lookup_replacements

# lookup_replacements

lookup_replacements ( index , replacements[] , typeFlag = 0x01 )

This function retrieves the possible replacements for the definition of the word specified in the previous call to the lookup function. If there was no previous call or the word was not found, then 0 is returned. Otherwise the number of replacements is returned.

index is the numeric index for the definition returned in the previous call to the lookup function or 0 if a list of suggestions is requested.

replacements is a numeric indexed array containing the possible replacement words.

typeFlag is one of the following flags to specify the type of replacement:

- • 0x01 — Synonym

- • 0x02 — Compared

- • 0x04 — Related

- • 0x08 — Contrast

- • 0x10 — Antonym

index is the numeric index for the definition returned in the previous call to the lookup function.



---

# lookup_types

# lookup_types

lookup_types ( index )

This function returns a bit mask indicating the possible word types for the definition index of the word specified in the previous call to the lookup function. If there was no previous call or the word was not found, then 0 is returned. Possible flags are:

- • 0x01 - Synonym

- • 0x02 - Compared

- • 0x04 - Related

- • 0x08 - Contrast

- • 0x10 - Antonym

index is the numeric index for the definition returned in the previous call to the lookup function.



---

# low_bound

# low_bound

low_bound ( arr )

This function returns the minimum subscript allowed for the array arr . If the array was not declared a fixed size with the local or global statement, then low_bound returns the lowest subscript used or 1 if the array is empty. If arr is an associative array, the function returns a null string.



---

# macro_exists

# macro_exists

macro_exists ( name [, doc ])

This function returns 1 ( True ) if the macro specified by name is defined in the scope specified by the document doc . If doc is omitted or 0 , the current document is used. Predefined commands and aliases are not recognized as macros in this context.

- • doc — The identifier of the document tree.

This function also returns 1 if no arguments are supplied and one or more macros are defined.

## Related Topics

- • macro_record built-in function

- • cmd_exists built-in function



---

# macro_pause_recording

# macro_pause_recording

macro_pause_recording ([ resume ])

This function pauses recording if a macro is being recorded. If the optional parameter resume is given and non-zero, then macro recording is resumed if it was paused.

If the Macros toolbar is displayed, this function changes the state of the corresponding toggle button.

## Related Topics

- • macro_record built-in function

- • macro_stop_recording built-in function



---

# macro_record

# macro_record

macro_record ( name [, scope [, desc [, key [, doc ]]]])

This function starts a macro recording session on the specified document.

- • name — The name of the macro. It must consist of valid XML name characters. If a macro named name already exists in the specified scope, the new macro will replace it. Do not use an ACL command name as the name of a macro. Using an ACL command name as a macro name may cause unexpected results when running the macro or ACL command.

- • scope — Specifies the target macro scope which determines which macro file is updated or created. scope and is one of the following values:

- • desc — Optional. A description of the macro to be displayed in the Macros dialog box.

- • key — Optional. A key binding for the macro. It has the same form as the keyname argument to the map command.

- • doc — Optional. The identifier of the document on which the macro recording session is started. If doc is omitted or 0 , the current document is used.

macro_record function displays the Macros toolbar and changes the window cursor to indicate that mouse operations are ignored while recording. Macro recording continues until the macro_stop_recording function is called.

macro_record returns 1 ( True ) if recording was started or 0 ( False ) if a macro is already being recorded.



---

# macro_record_cmd

# macro_record_cmd

macro_record_cmd ( command [, doc ])

If a macro is being recorded on the document specified by doc , this function assigns the string specified by command as the command to be recorded for the current event.

- • command — The string to assign as the command recorded for the current event.

- • doc — Optional. The identifier of the document on which the macro recording session is started. If doc is omitted or 0 , the current document is used.

## Related Topics

- • macro_record built-in function



---

# macro_recording

# macro_recording

macro_recording ([ doc ])

If doc is not specified, this function returns 1 ( True ) if a macro is currently being recorded on any document.

If doc is specified, macro_recording returns 1 if macro recording was started on the document specified by doc . If a macro is being recorded on another document, macro_recording returns 0 . If doc is 0 , the current document is used.

- • doc — Optional. The identifier of the document tree.

## Related Topics

- • macro_record built-in function



---

# macro_run

# macro_run

macro_run ( name [, doc ])

This function runs the macro named name in the document-scope specified by doc .

This function returns 1 ( True ) if the macro was executed. macro_run returns 0 if no such macro exists in the current scope. macro_run can not be used to execute command aliases.

- • name — The macro to run.

- • doc — Optional. The identifier of the document tree. If doc is omitted or 0 , the current document scope is used.

## Related Topics

- • macro_record built-in function



---

# macro_running

# macro_running

macro_running ()

This function returns non-zero if a macro is running.

## Related Topics

- • macro_run built-in function



---

# macro_stop_recording

# macro_stop_recording

macro_stop_recording ([ cancel ])

This function finishes recording if a macro is being recorded. If the optional parameter cancel is given and non-zero, then macro recording is aborted. Otherwise, the recorded macro is saved as specified by the parameters to the corresponding macro_record function.

If the Macros toolbar is displayed, this function hides it.

## Related Topics

- • macro_pause_recording built-in function



---

# marked_section_tag

# marked_section_tag

marked_section_tag ( tagname [, doc ])

This function returns 1 (True) if the tag specified by the entity tagname is an SGML marked section declaration. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# marking

# marking

marking ([ doc ])

This function determines whether a selection operation is in progress for the given document doc . If doc is omitted or set to zero, the current document is used.

The function returns 1 if a selection operation is in progress. Otherwise, the function returns 0 .

## Related Topics

- • mark command



---

# match

# match

match ( string , regexp )

This function searches string for the first substring matching regexp . regexp is a regular expression, the same as for the caret commands or looking_at function except that tag delimiters < and > are not meta-characters. match returns an index of start of match, if match succeeds, or 0 if the match fails.

## Related topic

Using regular expressions



---

# match_length

# match_length

match_length ( n )

This function returns the length of the n th subexpression matched from the previous call to match . If n is 0 , then the length of the entire matched string is returned.



---

# match_result

# match_result

match_result ( n )

This function returns n th subexpression matched from previous call to match . If 0 , match_result returns entire matched string. This is equivalent to: substr( string , match_start( n ), match_length( n )) where string is the first argument to the previous call to match .



---

# match_start

# match_start

match_start ( n )

This function returns the index of the first character of the n th subexpression matched from the previous call to match . If n is 0 , then the index of the first character matched is returned.



---

# max

# max

max ( n1 , n2 )

This function returns the maximum of numbers n1 and n2 .



---

# mblen

# mblen

mblen ( bytestr [, charset ])

This function returns the number of bytes in bytestr that form whole characters in the character set specified by charset , which may be a single-byte character set (SBCS), multi-byte character set (MBCS), or double-byte character set (DBCS). The length returned should be passed to mbstoucs to convert the string to Unicode. charset is one of the following strings:

- • iso8859-1

- • iso8859-2

- • iso8859-3

- • iso8859-4

- • iso8859-5

- • iso8859-7

- • iso8859-8

- • iso8859-9

- • ps_ascii

- • ps_symbol

- • jeuc

- • sjis

- • big5hku

- • gb2312

- • koi8

- • ksc5601

- • utf-8

- • Unicode

If charset is not specified, the system character set is assumed.



---

# mbstoucs

# mbstoucs

mbstoucs ( bytestr , len [, charset ])

This function converts the byte string bytestr encoded in the character set charset to a Unicode string. len specifies the number of bytes in bytestr to examine, and is normally the return value from a call to mblen .

charset is one of the character sets listed in the description of mblen . If charset is not specified, the system character set is assumed.

If the character set is a multi-byte character set, then it is possible that the last few bytes in bytestr do not form a whole character but are the prefix of a multi-byte character. In this case, they should be joined with the rest of the character for a subsequent call to mbstoucs . See the following example.

Example

This example shows how to convert a Japanese file encoded in JEUC into SJIS. For brevity, no error checking is done. Also, this example would need additional code to handle converting from or to 16-bit character sets, for example, to handle byte-swapping or the Unicode text file signature.

```
inf = open(jeucfile, "rb")
outf = open(sjisfile, "wb")
while ((len = read(inf, buf, 512)) 0)
{
# append what we just read to any left over bytes
# from previous read
bstr = remb . buf;
# compute how many bytes form whole characters
mb_len = mblen(bstr, "jeuc");
# and copy the remainder to REMB
remb = substr(bstr, mb_len+1);
# convert to Unicode
ucsstr = mbstoucs(bstr, mb_len, from_charset);
# and out to SJIS
mbstr = ucstombs(ucsstr, "sjis");
write(outf, mbstr);
}
close(inf);
close(outf);
```



---

# menu_active

# menu_active

ret = menu_active ( menupath [, active ])

This function returns the enabled state ( 1 or 0 ) of the menu item specified by menupath . If the parameter active is supplied, the menu item is enabled or disabled based on the value of active and the function returns the previous state of the menu item.

The function returns -1 if menupath does not specify an existing menu item.



---

# menu_checked

# menu_checked

menu_checked ( menupath )

This function returns 1 (True) if the menu item specified by menupath is checked. It returns 0 if the menu item is not checked or menupath does not specify a toggle-style item.

The menupath is a string that defines the path to the menu. Refer to the related topics for more information on menu paths.

## Related Topics

- • Menu paths

- • Modifying the default menus

- • Special characters in menu paths

- • Shortcut menus



---

# menu_cmd

# menu_cmd

menu_cmd ( menupath )

This function returns the command bound to the menu item specified by menupath . If there is no such menu, it returns the null string. If the menu item specified by menupath is not a command type item, it returns one of the following keywords:

- • #title — item is a menu title

- • #menu — item is a pullright menu

- • #nop — item is not-selectable

- • #help — item has only help text associated with it.

The menupath is a string that defines the path to the menu. Refer to the related topics for more information on menu paths.

Examples

```
menu_cmd(".File.Print")
menu_cmd(":EditPopup.Paste")
menu_cmd(".Options.Full Menus")
menu_cmd(".File.Preview.All Passes")
```

## Related Topics

- • Menu paths

- • Modifying the default menus

- • Special characters in menu paths

- • Shortcut menus



---

# menu_exists

# menu_exists

menu_exists ( menupath )

This function returns 1 (True) if the menu or item specified by menupath exists.

The menupath is a string that defines the path to the menu. Refer to the related topics for more information on menu paths.

## Related Topics

- • Menu paths

- • Modifying the default menus

- • Special characters in menu paths

- • Shortcut menus



---

# menu_item_array

# menu_item_array

menu_item_array ( menupath , arr )

This function fills the array arr with all the menu item labels in the menu specified by menupath , returning the number of items. Menu titles are not returned.

Each menu item label is prefixed by the name of the menu to form a menu path for use in other menu functions or commands as shown in the following example.

Menu separators are returned using the form menuname .# N , where N specifies the position in the menu. For example, Insert.#10 specifies a menu separator which is the tenth item on the Insert menu.

The menupath is a string that defines the path to the menu. As a special case, "." refers to the menu bar for the current window and all top level menu items are returned.

The function returns the number of labels stored in the array.

Example:

```
function show_menu_items(menu)
{
local items[];
local cnt = menu_item_array(menu, items);
local i;
for (i = 1; i <= cnt; i++) {
local label = items[i];
local cmd = menu_cmd(label);
eval label, "\t", cmd output=>*
if (cmd == "#menu") {
show_menu_items(label);
}
}
}
# Recursively enumerate the menu items and commands for the Insert menu
show_menu_items(".Insert")
```

## Related Topics

- • Menu paths

- • menu_item_count function

- • menu_cmd function



---

# menu_item_count

# menu_item_count

menu_item_count ( menupath )



This function returns the number of items in the menu specified by menupath . Returns -1 if menupath does not specify an existing menu. If menupath specifies an item, that is, not pulldown menu, the number of items in the containing menu is returned. Menu titles do not count as items.

The menupath is a string that defines the path to the menu. Refer to the related topics for more information on menu paths.

## Related Topics

- • Menu paths

- • Modifying the default menus

- • Special characters in menu paths

- • Shortcut menus



---

# menu_popup

# menu_popup

menu_popup ( menu [, window [, geometry ]])

This function posts the shortcut menu named menu in the window containing the current document or in a XUI dialog box. menu_popup returns 1 if the menu was posted, or 0 if no such shortcut menu exists. This function can be mapped to a button or key press. Typically, the right mouse button is used to post shortcut menus.

- • menu — The name of a shortcut menu defined within a menu configuration file. If window is specified and is the window ID of a XUI dialog box, menu may also be the XUI ID of a context or dropdown menu defined within the dialog box. Any ACL event dispatched for this menu can be processed by adding an ACL event callback. For more details, refer to the XUI documentation in the Customizer's Guide .

- • window — Optional. Specifies the ID of the parent window.

- • geometry — Optional. Specifies the location for posting the menu. The value of geometry takes the form + X + Y

## Related Topics

- • dlgitem_get function



---

# message_box

# message_box

message_box ( message , flags [, title ])

This function displays a message box with the text message and optional title title . The flags parameter determines what predefined buttons and icons display in the message box, and is formed by ORing the flags from the following groups of flag bits.

Specify one of the following flags to indicate the buttons that will display in the message box:

- • 0x00 — Display OK button only. This is the default.

- • 0x01 — Display OK and Cancel buttons.

- • 0x02 — Display Abort, Retry, and Ignore buttons.

- • 0x03 — Display Yes, No, and Cancel buttons.

- • 0x04 — Display Yes and No buttons.

- • 0x05 — Display Retry and Cancel buttons.

Specify one of the following flags to indicate the icon to display in the message box. If you do not specify one of these flags, an icon does not display.

- • 0x10 — Display the Error (Stop) icon. This icon is typically used with the Abort, Retry, and Ignore buttons.

- • 0x20 — Display the Question icon. This icon is typically used with the Yes and No buttons.

- • 0x30 — Display the Warning icon.

- • 0x40 — Display the Information icon.

Specify one of the following flags to indicate the default button:

- • 0x000 — The first button is the default. This is the default if no other default button flag is specified.

- • 0x100 — The second button is the default.

- • 0x200 — The third button is the default.

If title is not specified or is a null string, the default title $progname Message is used.

The return value is one of the following:

- • 1 — The first button (Yes, OK, Abort, or Retry) was pressed.

- • 2 — The No button was pressed.

- • 3 — The third button (Cancel or Ignore) was pressed.

If the dialog box has a Cancel or Ignore button, the function returns 3 if the Cancel or Ignore button or ESC key was pressed, or if the dialog box was closed from the Close system menu or Close button. If the dialog box does not have a Cancel or Ignore button and is closed with the ESC key or by the Close system menu or Close button, the function returns 2 if the dialog has only Yes and No buttons. If the dialog box only has an OK button, it returns a 1 .

Examples

```
message_box("Save new file?", 0x03+0x20)
message_box("Document is incomplete.", 0x40, "Incomplete")
```

## Related Topics

- • response function

- • message command



---

# min

# min

min ( n1 , n2 )

This function returns the minimum of the two numbers n1 and n2 .



---

# modified

# modified

modified ([ doc [, value ]])

This function returns 1 (True) if current document has been modified (otherwise, zero). The doc parameter specifies the identifier of the document tree to query. If omitted or 0 , the current document is used. The value parameter specifies the new value for the “modified” state of doc . Note that the change to value takes place after determining the return value.



---

# modify_attr

# modify_attr

modify_attr ( attrname , value [, doc ])

This function sets the attribute attrname to value for the element to the left of the cursor in the document specified by doc . If doc is omitted or 0 , the current document is used.

If successful, modify_attr returns 1 ( True ). If attrname doesn't exist for the element, or the document is read-only, modify_attr returns 0 .

modify_attr can be used to assign XML namespace attributes to elements in an XML document.

The function call:

```
modify_attr(name, value, doc)
```

is the same as:

```
oid_modify_attr(oid_current_tag(doc), name, value)
```

## Related Topics

- • oid_modify_attr built-in function

- • modify_tag command



---

# modify_file_entity

# modify_file_entity

modify_file_entity ( name [, sysid [, pubid [, type [, doc ]]]])

This function allows you to modify a file entity declaration.

name is the name of an existing file entity. The leading & is optional.

sysid is the new system identifier value (if there is one).

pubid is the new public identifier value (if there is one).

type is either empty, normal , or SUBDOC to declare the entity as a SUBDOC entity.

doc is the document identifier. By default, the current document is assumed.

## Related topic

declare_file_entity function



---

# modify_graphic_entity

# modify_graphic_entity

modify_graphic_entity ( name , notn [, sysid [, pubid ]])

This function allows you to modify a graphic entity declaration.

name is the name of an existing graphic entity.

notn is the name of the entity's new notation. The leading & is optional.

sysid is the new system identifier value (if there is one).

pubid is the new public identifier value (if there is one).

## Related topic

declare_graphic_entity function



---

# modify_text_entity

# modify_text_entity

modify_text_entity ( name , text [, type ])

This function allows you to change the declaration of a text entity.

name is the name of an existing text entity. The & prefix is optional.

text is the new replacement text.

type is supplied, and should be one of the following:

- • CDATA — character data

- • PI — processing instruction

- • MS — marked section

- • MD — markup declaration

If omitted, the entity is a normal entity (that is, the markup within the replacement text is recognized).

## Related topic

declare_text_entity function



---

# mouse_at

# mouse_at

mouse_at ([ window [, flags ]])

This function returns a string describing the object beneath the mouse cursor in the window specified by window . If the argument is omitted or 0 , the current window is used.

The following strings are returned by mouse_at :

- • attr. Name — in the Document Map, the object is an attribute line and Name is the attribute name displayed, for example, attr.id .

- • attrval. Name — in the Document Map (or an expanded attribute in Column view), the object is an attribute value and Name is the attribute name for which the value is displayed, for example, attrval.id .

- • cellattrval. Name — over a cell in Column view, and Name is the attribute name for which the value is displayed in the cell, for example, cellattrval.id . If no attribute exists for the element in a Column view cell, then Name is set to unknown .

- • columnview.ruler_boundary — in Column view, the object is a boundary between two columns in the heading (used for column resizing).

- • equation — object is an equation image.

- • icon. icontype — object is the display icon icontype for the current element. Possible return values for icontype are in the following table.

- • icon.ElementInlineContent — in Column view, the object is an element with content (text or inline elements) that is not displayed.

- • name. TagName — in the Document Map, the object is the name field next to the icon and TagName is the name displayed, for example, "name.para" if over the paragraph element <para> .

- • null — no object, in the case of an empty file.

- • tag — object is a tag (either start or end). This includes entity references, processing instructions, and all other non-image markup.

- • tabl. location — the object is the location pertaining to the current table. Possible return values for location are:

- • text — object is text.

flags is an optional bitmask that controls the value returned when the cursor is over a tag in a table cell. It has the following flag:

- • 0x001 — Being over a table cell is more significant than being over the cell’s contents. For example, if the cursor is over a tag that is inside a table cell, the function returns tabl.cell when this bit is set. Otherwise, the function returns tag .

Note, that this function is most useful when called from a mouse button mapping. If invoked outside a mouse button mapping, then the previous mouse pointer position in the specified window is used.

## Related Topics

- • caret_at function



---

# mouse_in_selection

# mouse_in_selection

mouse_in_selection ([ doc ])

This function returns 1 (True) if the mouse pointer is within the current selection of the document specified by doc , or the current document if doc is omitted. Returns 0 (False) if the pointer is not within the selection, or if there is no selection in the document identified by doc .

## Related Topics

- • caret_in_selection function



---

# mouse_set_waiting

# mouse_set_waiting

mouse_set_waiting ( )

This function changes the mouse cursor to the standard waiting cursor to indicate that the application is blocked. The cursor will be restored to the normal one after the current event has completed.



---

# msp_entity_names

# msp_entity_names

msp_entity_names ( arr [, doc ])

The msp_entity_names function fills the array arr with an alphabetical list of marked section parameter entity names which are valid for the current document, returning the total number. The first name returned is stored at index 1. All previous elements in arr are discarded.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# notation_exists

# notation_exists

notation_exists ( name [, doc ])

The notation_exists function returns 1 (True) if the notation named name is a valid notation in the current document. If the notation is not declared, 0 is returned.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# notation_names

# notation_names

notation_names ( arr [, doc [, exclude ]])

The notation_names function fills the array arr with an alphabetical list of notation names which are valid for the current document, returning the total number. The first name returned is stored at index 1. All previous elements in arr are discarded.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

If the exclude argument is 1 , then the excludegraphicnotation hook is called to potentially exclude any notations from the array. If omitted or 0 , all notations are included.



---

# notation_parfile

# notation_parfile

notation_parfile ( notation [, doc ])

This function returns the name of the parameter file entity in which the notation was declared (if the entity was declared in a notation file entity). Otherwise, the null string is returned.

notation is the name of the entity.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# notation_pubid

# notation_pubid

notation_pubid ( name [, doc ])

The notation_pubid function returns the PUBLIC identifier from the declaration for the notation name . It returns the null string if the notation does not exist or if no PUBLIC identifier was specified.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# notation_source

# notation_source

notation_source ( name [, doc ])

The notation_source function returns a number indicating the origin of the declaration for the notation named name . The return value is one of the integers:

- • -1 — notation not declared.

- • 0 — notation defaulted.

- • 1 — notation declared in declaration subset (private markup) only.

- • 2 — notation declared in DTD only.

- • 3 — notation declared in both DTD and declaration subset.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# notation_sysid

# notation_sysid

notation_sysid ( name [, doc ])

The notation_sysid function returns the SYSTEM identifier from the declaration for the notation name . It returns the null string if the notation does not exist or if no SYSTEM identifier was specified.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# ns_schema_validate_batch

# ns_schema_validate_batch

ns_schema_validate_batch ( ns_schema[] [, schema [, doc [, flag ]]])

Validates a document against a set of schema definitions, including non-namespaced and namespaced schema definitions.

- • ns_schema[] — An array of path and file names for namespaced schema definition ( XSD ) files.

- • schema — Path and file name of a non-namespaced schema definition ( XSD ) file. Defaults to empty if not supplied.

- • doc — The document to validate against the schemas. If not specified, the current document is used.

- • flag — Enables you to control how the doc is validated against the schema . The following flags are available:

The function returns one of the following values:

- • 0 — The validation failed.

- • 1 — doc is valid.

All ns_schema_validate_batch results are shown in the event-log document. Refer to schema_validate for similar functionality.

## Related Topics

- • schema_validate_batch

- • get_schema_log_doc()



---

# numbered_list_block_tag_name

# numbered_list_block_tag_name

numbered_list_block_tag_name ( arr [, doc ])

This function returns the name of the primary numbered list block tag specified in the document type configuration file ( .dcf ) for the document type associated with doc . This tag is inserted when users select the numbered list button on the Application toolbar .

If a tag name is returned, numbered_list_block_tag_name function returns arr with an attribute name and attribute value, if they were specified for the tag in the .dcf file.

The function returns the null string if there isn't a numbered list block tag designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

For example,

```
local tag, arr[];
local attr, val;
tag = numbered_list_block_tag_name(arr);
attr = arr['attribute'];
val = arr['attribute_value'];
```

## Related Topics

- • Document type configuration files

- • Configuring tags as list elements

- • numbered_list_item_tag_name function

- • set toolbar4 command



---

# numbered_list_block_tag_name_ns

# numbered_list_block_tag_name_ns

numbered_list_block_tag_name_ns ( arr [, doc ])

This function returns the namespace URI prefixed to the primary numbered list block tag specified in the document type configuration file ( .dcf ) for the document type associated with doc . This tag is inserted when users select the numbered list button on the Application toolbar .

If a tag name is returned, numbered_list_block_tag_name function returns arr .

The function returns the null string if there isn't a namespace prefix, if no numbered list block tag is designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

## Related Topics

- • Document type configuration files

- • Configuring tags as list elements

- • numbered_list_block_tag_name function

- • numbered_list_item_tag_name_ns function

- • set toolbar4 command



---

# numbered_list_item_tag_name

# numbered_list_item_tag_name

numbered_list_item_tag_name ( arr [, doc ])

This function returns the name of the primary numbered list item tag specified in the document type configuration file ( .dcf ) for the document type associated with doc . This tag is inserted, along with the numbered list block tag, when users select the numbered list button on the Application toolbar .

If a tag name is returned, numbered_list_item_tag_name function returns arr with an attribute name and attribute value, if they were specified for the tag in the .dcf file.

The function returns the null string if there isn't a numbered list item tag designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

For example,

```
local tag, arr[];
local attr, val;
tag = numbered_list_item_tag_name(arr);
attr = arr['attribute'];
val = arr['attribute_value'];
```

## Related Topics

- • Document type configuration files

- • Configuring tags as list elements

- • numbered_list_block_tag_name function

- • set toolbar4 command



---

# numbered_list_item_tag_name_ns

# numbered_list_item_tag_name_ns

numbered_list_item_tag_name_ns ( arr [, doc ])

This function returns the namespace URI prefixed to the primary numbered list item tag specified in the document type configuration file ( .dcf ) for the document type associated with doc . This tag is inserted, along with the numbered list block tag, when users select the numbered list button on the Application toolbar .

If a tag name is returned, numbered_list_item_tag_name_ns function returns arr .

The function returns the null string if there isn't a namespace prefix, if no numbered list item tag is designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

## Related Topics

- • Document type configuration files

- • Configuring tags as list elements

- • numbered_list_item_tag_name function

- • numbered_list_block_tag_name_ns function

- • set toolbar4 command



---

# oct

# oct

oct ( value )

This function returns the decimal value of value interpreted as an octal string. For example, the value of oct("10") is 8 .



---

# oid_asis

# oid_asis

oid_asis ([ oid ])

This function returns whether or not the contents of oid constitutes an “asis” region. The function returns a 1 if the oid is an “asis” region or a 0 if the oid is not an “asis” region. If the oid argument is omitted, then the current oid of the current document is assumed.

An “asis” region is one where newlines in the document content are preserved and cause line breaks both in the Editor pane and in published output. A region is “asis” if the FOSI specified justification (that is, quadding) in effect is “asis”, or if the document is an untagged ASCII file.



---

# oid_attr

# oid_attr

oid_attr ( oid , attrname )

This function returns the value of the attribute attrname for the specified object oid , or the null string if the element identified by oid has no such attribute.

## Related Topics

- • current_tag_attr_value function

- • graphic_file_attr_name function

- • tag_attr_value function

- • tag_has_attr function



---

# oid_attr_list

# oid_attr_list

oid_attr_list ( oid , arr [, dflt ])

This function fills the associative array arr with a list of attributes set for the element identified by oid . This function returns the number of attributes in the array or 0 if the element has no attributes. Each attribute is stored in the array using the attribute name as the key, and its value as the array element value.

dflt is an optional third argument, which if non-zero, results in all attributes for the element identified by oid to be returned. For those attributes whose values are unspecified on the start tag oid , the default values are returned. For namespaced tags, oid_attr_list returns the namespace and any undefined attributes.

For example, the oid_attr function could be written using this function as:

```
function oid_attr(oid, attrname)
{
local al[]
oid_attr_list(oid, al)
return (attrname in al) ? al[attrname] : ""
}
```

The built-in function is more efficient, however, since it does not need to create an array using oid_attr_list to obtain the value.



---

# oid_attr_required

# oid_attr_required

oid_attr_required ( oid , attrname )

This function returns 1 (True) if the attribute attrname for the element specified by OID is a required attribute, that is, declared as #REQUIRED in the DTD.



---

# oid_attr_type

# oid_attr_type

oid_attr_type ( oid , attrname )

This function returns the declared attribute value type for the attribute named attrname of the element specified by oid .

If the attribute was declared as a name group, this is a string of the form "CDATA", "ENTITY", "ENTITIES", "ID", "IDREF", "IDREFS", "NAME", "NAMES", "NMTOKEN", "NMTOKENS", "NOTATION", "NUMBER", "NUMBERS", "NUTOKEN", "NUTOKENS", or "NAMEGROUP".

This function is equivalent to:

```
tag_attr_type(oid_name(oid), attr, oid_doc(oid))
```



---

# oid_backward

# oid_backward

oid_backward ( oid )

This function returns the oid of the element preceding the element specified by oid in linear (galley strip) order. Returns oid_null if oid is the first object in the document.

Examples

The oid_backward function could be written using oid_prev and oid_child as follows:

```
function oid_backward(o)
{
if (!oid_valid(o)) {
return oid_null()
}
# if no left sibling, return parent
local lsib = oid_prev(o)
if (!oid_valid(lsib)) {
return oid_parent(o)
}
# return deepest, rightmost child of the
# immediate left sibling, if there is one
local rchild = lsib, last
while (oid_valid(rchild)) {
last=rchild
rchild=oid_child(rchild, -1)
}
return last
}
```

## Related Topics

- • oid_child function

- • oid_null function

- • oid_prev function



---

# oid_caret

# oid_caret

oid_caret ([ doc ])

This function returns the object identifier of the object containing the cursor. For singleton tags, this function returns the object identifier of the singleton immediately to the left of the cursor. If the cursor is outside the outermost element or if the document has no objects (that is, an ASCII file or an empty document), this function returns an invalid OID (that is, oid_null ). The oid_caret takes an optional argument, doc , that specifies the identifier of the document tree. If doc is omitted or is 0 , then the current document is used.

## Related Topics

- • caret command

- • oid_caret_pos function

- • oid_current tag function



---

# oid_caret_offset

# oid_caret_offset

oid_caret_offset ([ oid ])



This function returns the position of the cursor in characters from the specified oid , or oid_caret if oid is not supplied. This function is the same as oid_caret_pos except that it always returns a character offset. Each non-text object (that is, markup, equations, tables, graphics) counts as one character. oid_caret_pos will return -1 as a special case if the cursor is positioned before the end tag of the object, since this is more efficient than calculating the offset. The offset is sometimes needed, however, if characters or other objects are inserted after the cursor.

## Related Topics

- • caret command

- • oid_caret_pos function



---

# oid_caret_pos

# oid_caret_pos

oid_caret_pos ([ oid ])

This function returns the position of the cursor in characters from the specified oid , or oid_caret if oid is not supplied. oid_caret_pos will return -1 as a special case if the cursor is positioned before the end tag of the object, since this is more efficient than calculating the offset. Each non-text object (that is, markup, equations, tables, graphics) counts as one character. This position may be used with oid_caret and goto_oid o restore the cursor to a previous location in the document, for example:

```
oid = oid_caret()
pos = oid_caret_pos(oid)
...
goto_oid(oid, pos)
```

## Related Topics

- • goto_oid function

- • oid_caret function



---

# oid_check_attr

# oid_check_attr

oid_check_attr ( oid , attr , value )

This function returns a null string if value specifies a valid setting for the attribute named attr for the element identified by oid . If value is illegal, it returns a message describing the error.



---

# oid_child

# oid_child

oid_child ( oid [, n ])

This function returns the OID of the n th child of the element identified by oid or oid_null if there is no such child. If n is omitted, then the OID of first child is returned. If n is -1 , then the OID of the last child is returned.

## Related Topics

- • oid_children function



---

# oid_children

# oid_children

oid_children ( oid )

This function returns the number of children of the element specified by OID or 0 if the element contains no elements.

Examples

This function can be written using the oid_child primitives as follows:

```
function oid_children(parent)
{
local n = 0;
local o = oid_child(parent)
while (oid_valid(o)) {
n++
o = oid_next(o)
}
return n;
}
```

## Related Topics

- • oid_child function



---

# oid_content

# oid_content

oid_content ( oid [, flags ])

This OID function returns the content of the element specified by oid as a markup-coded string.

The optional argument flags is a bitmask that controls the markup included in the returned string and is constructed using OR with the following flags:

- • 0x1 — Include the start tag (and end tag if not EMPTY) markup for oid in the string. If not specified, then only the content is included.

- • 0x2 — Include only the start tag for oid markup if applicable (no content nor end tag). If this bit is specified, then the 0x1 bit is ignored.

- • 0x4 — Don't convert non-ASCII characters to entity references (as though set writenonasciichar=char option was in effect). If this bit is not specified, non-ASCII characters are converted based on the set writenonasciichar command setting.

- • 0x8 — Suppress insignificant line breaks, which are line breaks that occur where a record end is not significant. If this bit is not specified, insignificant line breaks are included based on the set outputrecordlength command setting.

- • 0x10 — Suppress Arbortext processing instructions. Arbortext processing instructions can also be suppressed using the set writepi command.

- • 0x20 — Use XML syntax in the string returned even if the selection is in an SGML document.

- • 0x40 — Use SGML syntax in the string returned even if the selection is in an XML document.

- • 0x80 — Do not include the markup in the result. This option takes precedence over any other flag bits that control how markup is generated.

- • 0x100 — For XInclude elements, expand the element and return its content only (do not include the <xi:include> tag).

Because of memory requirements, you should not request the content of large elements such as the entire document, chapters, or sections.

Example:

Consider the following string of tagged content. In these examples, assume that your text caret is within this paragraph.

```
<para id="P1">This is a test.</para>
```

To return the content only, use the following function call:

```
oid_content(oid_caret())
```

To return the content and the surrounding tags, use the following function call:

```
oid_content(oid_caret(),1)
```

To return the start tag markup only, use the following function call:

```
oid_content(oid_caret(),2)
```

## Related Topics

- • oid_select function

- • selection_markup function

- • oid_empty function

- • goto_oid function

- • set writenonasciichar command



---

# oid_content_model

# oid_content_model

oid_content_model ( oid [, doc ])

This function returns the canonical form of the content model for the element specified by oid .

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

## Related Topics

- • content_model



---

# oid_context_string

# oid_context_string

oid_context_string ( oid [, include ])

This OID function returns the context string of the element specified by oid . If the optional parameter include is given and non-zero, the start tag (and end tag if not EMPTY) for oid is included in the string.

## Related Topics

- • File entities and the CX processing instruction



---

# oid_current_tag

# oid_current_tag

oid_current_tag ([ doc [, forward ]])

In the Edit window view, this function returns the identifier of the tag object that is backward from the cursor in the document if forward is 0 or omitted. If forward is non-zero, oid_current_tag returns the identifier of the tag object that is forward from the cursor.

In the Document Map view, this function returns a tag object identifier based on the cursor location and the value of the set docmapcurrenttag command.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is searched.

Unlike oid_caret this only returns tag objects, never equation images. Also unlike oid_caret , if the encountered tag is an end tag, oid_current_tag returns the OID of its start tag instead of the parent object.

## Related Topics

- • current_tag_name built-in function

- • oid_caret function

- • set docmapcurrenttag command



---

# oid_declared_tag

# oid_declared_tag

oid_declared_tag ( tagname [, oid [, doc ]])

This function returns 1 (true) if tagname is the name of an element declared in the document type (defined in a DTD or schema). The function returns 0 (false) when:

- • tagname is not a valid tag name, or

- • tagname is a Arbortext Editor supplied tag (for example, the processing instructions _font or _ignore ),or

- • the tag is from a foreign namespace.

tagname is looked up with respect to the position in the document represented by oid . If oid is not supplied, the current caret point of the current document is assumed. If oid is supplied and is oid_null() , tagname is looked up independent of any document instance and is only looked up with respect to the document type of doc .

Note that the doc parameter is only used if oid is supplied and is oid_null() . If doc is not supplied or is 0 , the current document is used.



---

# oid_delete

# oid_delete

oid_delete ( oid [, flags ])

This function deletes the object identified by oid and its content depending on the flags parameter.

The optional flags parameter is a bitmask that controls what is deleted and is constructed using OR with the following flags:

- • 0x1 — delete only the tag (and end tag if not EMPTY).

- • 0x2 — delete only the content if an element.

If flags is omitted or 0 both the element and its content are deleted. If oid does not specify an element, only the object is deleted.

## Related Topics

- • oid_content function

- • delete_tag command



---

# oid_delete_attr

# oid_delete_attr

oid_delete_attr ( oid , attrname )

This function deletes the attribute named attrname from the element specified by oid .

Returns 1 (True) if the attribute was deleted, or 0 (False) if oid is invalid or does not have an attrname attribute. If attrname specifies a required attribute, then the document is marked incomplete.



---

# oid_detail

# oid_detail

oid_detail ( oid , flag )

This function can expand or collapse an element in the Edit window. The element is specified by oid .

If flag is 1 , the content of the element specified by oid is replaced by a plus sign ( + ) enclosed in a box in the Edit window (in other words, the element is collapsed). If flag is 0 , the element is expanded. Note that this function does nothing when the specified oid is a division heading element and the current window is the Edit window.

As shown below, the element containing the oid (the caret in this case) will be collapsed.

```
oid_detail(oid_caret(), 1)
```

Use 0 instead of 1 to expand detailing.

The oid_expose function can also be used if the Edit window is synchronized with the Document Map window.

## Related Topics

- • oid_detailed function

- • oid_expose function



---

# oid_detailed

# oid_detailed

oid_detailed ( oid )

This function returns 1 (True) if the contents of the element identified by oid is detailed. Detailed means it's represented by a plus sign ( + ) enclosed in a box in the Edit window (in other words, the element is collapsed).

## Related Topics

- • oid_detail function

- • oid_expose function



---

# oid_dialog

# oid_dialog

oid_dialog ( oid )

This function returns the window ID of the XUI dialog associated with the specified oid . The dialog can be either the embedded ActiveX dialog associated with an intelligent graphic or a dialog that is associated with the element referenced by the oid through the document type configuration file ( .dcf file). If the dialog does not exist, the function returns -1 .

Refer to the Customizer's Guide for more information about XUI dialogs.

## Related Topics

- • Intelligent graphics overview

- • Document type configuration files



---

# oid_doc

# oid_doc

oid_doc ( oid )

This function returns the document ID for the specified oid .



---

# oid_effective_dita_attr

# oid_effective_dita_attr

oid_effective_dita_attr ( oid , attr )

For DITA documents, this function returns the value of the specified attribute attr at the specified oid . The attribute values the function can return include explicitly set values, document type specified default values, processor default values, and inherited values. For example, assume you have the following markup in a DITA map:

```
<topicgroup format="ditamap">
<topicref href="myMap.ditamap"/>
</topicgroup>
```

Calling this function for the format attribute on the topicref element would return ditamap .

## Related Topics

- • oid_effective_dita_attrs function

- • oid_effective_default_dita_attrs function



---

# oid_effective_dita_attrs

# oid_effective_dita_attrs

oid_effective_dita_attrs ( oid , array[] )

For DITA documents, this function populates an array with all of the effective attributes at the specified oid . The effective attributes include explicitly set values, document type specified default values, processor default values, and inherited values. For example, assume you have the following markup in a DITA map:

```
<topicgroup format="ditamap">
<topicref href="myMap.ditamap"/>
</topicgroup>
```

Calling this function for the topicref element would return ditamap for the format attribute.

## Related Topics

- • oid_effective_dita_attr function

- • oid_effective_default_dita_attrs function



---

# oid_effective_dita_default_attrs

# oid_effective_dita_default_attrs

oid_effective_dita_default_attrs ( oid , array[] )

For DITA documents, this function populates an array with all of the effective default attributes at the specified oid . The effective attributes include document type specified default values, processor default values, and inherited values. This function does not return explicitly set attribute values. If the given array is not empty, only those attributes with names that match keys in the array will be populated. Otherwise, all attributes with default values are populated.

For example, assume you have the following markup in a DITA map:

```
<topicgroup format="ditamap">
<topicref format="dita" href="myTopic.dita"/>
</topicgroup>
```

Calling this function for the topicref element would return ditamap for the format attribute. It would not return dita , because that is an explicitly set value instead of the default value.

## Related Topics

- • oid_effective_dita_attrs function

- • oid_effective_dita_attr function



---

# oid_empty

# oid_empty

oid_empty ( oid )

This function returns 1 (True) if the element identified by oid has no content.



---

# oid_encl_include

# oid_encl_include

oid_encl_include ( oid [, pos ])

This function returns the oid of the of the nearest enclosing included object to the location specified by oid and pos , regardless of whether or not the object is expanded. If the specified oid is not in an included object, this function returns a null string.

pos can be any of the following values:

- • 0 — (The default.) pos is immediately after the start tag identified by oid .

- • -1 — pos is immediately before the end tag of the element identified by oid .

- • -2 — pos is immediately before the start tag.

- • -3 — If oid is a start tag, pos is immediately after the end tag. Otherwise, pos is at the end of the object.



---

# oid_entity_first

# oid_entity_first

oid_entity_first ( oid )

This function returns the OID of the first element within the text or file entity specified by OID oid . This function returns the null OID if oid is not a file or text entity, or if there are no elements within the entity. If oid is a file entity reference, the OID returned would be the top of a different document tree than the one oid is in. If oid is a text entity, the OID returned is in the same doc as the one oid is in.



---

# oid_entity_last

# oid_entity_last

oid_entity_last ( oid )

This function returns the OID of the last element within the text or file entity specified by OID oid . This function returns the null OID if oid is not a file or text entity or if there are no elements within the entity. If oid is a file entity reference, the OID returned is in a different document tree than the one oid is in. If oid is a text entity, the OID returned would be in the same document as the one oid is in.



---

# oid_entity_lock

# oid_entity_lock

oid_entity_lock ( oid [, resultcode [, showerror [, pos ]]])

This function locks a file entity or XML inclusion for editing and calls entitylockhook or includelockhook if appropriate. The function only operates if the given oid at cursor position pos is in a file entity or XML inclusion, and if the entity or inclusion is not stored in a Document Management System (DMS). DMS objects must be checked out according to the user's system administration practices before they can be edited.

If the oid is in an entity or inclusion (or is an entity or inclusion referencing itself) and the entity or inclusion is not stored in a DMS, then the entity or inclusion will be locked for editing. If an entitylockhook is defined it will be called first and the entity or inclusion will be locked only if the hook returns a value of 0 . oid_entity_lock returns 0 only if it tries to lock an entity or inclusion and fails. In all other cases this function will return 1 .

resultcode , if supplied, must be a variable set to a code indicating the status of the lock operation. The possible values are:

- • 0 — Locked and not refreshed.

- • 1 — The entity or inclusion was locked, but had been modified on disk since it was opened and was reloaded.

- • 2 — The entity or inclusion could not be locked because someone else has it locked.

- • 3 — The entity or inclusion could not be locked because the file it is in is read only.

- • 4 — The entity or inclusion could not be locked for some other reason.

If showError is supplied and non-zero, an error message will be displayed for any failure to lock the include or entity.

pos can be any of the following values:

- • 0 — (The default.) pos is immediately after the start tag identified by oid .

- • -1 — pos is immediately before the end tag of the element identified by oid .

- • -2 — pos is immediately before the start tag.

- • -3 — If oid is a start tag, pos is immediately after the end tag. Otherwise, pos is at the end of the object.

## Related Topics

- • entitylockhook

- • includelockhook



---

# oid_expose

# oid_expose

oid_expose ( oid [, newval [, descend ]])

This function returns 1 (True) if the content for the element identified by oid are displayed in the Document Map window. Otherwise, it returns 0 .

If newval is specified, it changes the state of the content display for oid . If 0 , the content is collapsed. If non-zero, the content lines for the element are displayed.

If descend is specified and non-zero, then oid_expose changes the exposed state of all children of oid , recursively.

Note, the effect of this function is visible in the Document Map and Column view only. The expose bit is independent of detailing, which is shown only in non-Document Map or Column views.

## Related Topics

- • cut_valid function

- • delete_markup_valid function

- • oid_detail function

- • oid_detailed function

- • oid_paste_valid function

- • oid_show_attr function



---

# oid_find_child_attrs

# oid_find_child_attrs

oid_find_child_attrs ( oid , arr , attr [, value [, flags ]])

This function fills the array arr with all the oids of the descendents of oid that contain the attribute attr with the value of value . If OID is oid_null() , then the entire document tree for the current document is searched. If value is null, then the descendent is returned if attr is set to any value. The flags parameter is a bitmask specifying the search options, and is constructed by using OR with the flags from the following list:

- • 0x01 — Return after first match

- • 0x04 — Match case (search case-sensitive)

- • 0x08 — The supplied value is a regular expression (flag 0x04 is ignored)

- • 0x10 — Match only attributes of declared type ID . If attr and value are both null, then all elements having an ID attribute are returned.

- • 0x20 — Match only attributes of declared type IDREF or IDREFS . If attr and value are both null, then all elements having an IDREF or IDREFS attribute are returned. This bitmask is ignored if the document is freeform XML.

This function returns the number of oids stored in the array arr .

## Related Topics

- • oid_find_parent_attrs function



---

# oid_find_children

# oid_find_children

oid_find_children ( oid , arr , tag [, flags ])

This function fills the array arr with all the oids of the descendents of oid that match the tag name tag . If OID is oid_null( ) , the entire document tree for the current document is searched. The flags parameter is a bitmask specifying the search options, and is constructed by ORing the flags from the following list:

- • 0x01 — Return after first match

- • 0x04 — Match case (search case-sensitive)

- • 0x08 — The supplied tag is a regular expression (flag 0x04 is ignored)

This function returns the number of oids stored in the array arr .

## Related Topics

- • oid_find_child_attrs function



---

# oid_find_parent_attrs

# oid_find_parent_attrs

oid_find_parent_attrs ( oid , arr , attr [, value [, flags ]])

This function fill the array arr with all the oids of the ancestors of oid that contain the attribute attr with the value of value . If value is null, then the ancestor is returned if attr is set to any value. The flags parameter is a bitmask specifying the search options, and is constructed by using OR for the flags from the following list:

- • 0x01 — Return after first match

- • 0x02 — Ascend into ancestor file entities (this flag will not function properly if the file entity is open in its own window)

- • 0x04 — Match case (search case-sensitive)

- • 0x08 — The supplied value is a regular expression (flag 0x04 is ignored)

- • 0x10 — Match only attributes of declared type ID . If attr and value are both null, then all elements having an ID attribute are returned. This bitmask is ignored if the document is freeform XML.

- • 0x20 — Match only attributes of declared type IDREF or IDREFS . If attr and value are both null, then all elements having an IDREF or IDREFS attribute are returned. This bitmask is ignored if the document is freeform XML.

This function returns the number of oids stored in the array arr .

## Related Topics

- • oid_find_child_attrs function



---

# oid_find_valid_insert

# oid_find_valid_insert

oid_find_valid_insert ( oid [, offset [, flags ]])

This function returns the nearest valid insertion point if the oid passed in is within generated text, a protected region, a text entity, or a protected change tracking region. The offset parameter is modified indirectly. The optional flags parameter controls the search and defaults to 0 (search forward).

- • 0x1 — backward (search backward if set, otherwise forward)

- • 0x2 — autoreverse (if search fails try the other direction)

- • 0x4 — Returns an insertion point that is not read-only even if the location does not allow markup such as a comment or CDATA section. Otherwise, the function will disallow these areas.

If no valid insertion point is found, this function returns the null oid .



---

# oid_first

# oid_first

oid_first ([ doc ])

This function returns the OID of the first object in the document. oid_first takes an optional argument, doc , that specifies the identifier of the document tree. If doc is omitted or 0 , then the current document is used.

## Related Topics

- • oid_first_tag



---

# oid_first_tag

# oid_first_tag

oid_first_tag ([ doc ])

This function returns the OID of the first element start tag in the document. oid_first_tag takes an optional argument, doc , that specifies the identifier of the document tree. If doc is omitted or 0 , then the current document is used.

Use oid_first_tag instead of oid_first , when you do not want comments and processing instructions at the beginning of the document.



---

# oid_forward

# oid_forward

oid_forward ( oid )

This function returns the object identifier of the element following the element specified by oid in linear (galley strip) order. This function returns oid_null f oid is the last element in the document.

Examples

The loop shown in the following excerpt from a function lists all elements in the document instance from first to last:

```
for (o = oid_first(); oid_valid(o); o = oid_forward(o)) {
eval oid_name(o) output=>*
}
```

The oid_forward function can be written using oid_next and oid_child as follows:

```
function oid_forward(o1)
{
if (!oid_valid(o1)) { return oid_null();}
local o = oid_child(o1);
if (oid_valid(o)) { return o;}
while (oid_valid(o1)) {
o = oid_next(o1);
if (oid_valid(o)) { return o;}
o1 = oid_parent(o1)
}
return oid_null()
}
```

## Related Topics

- • oid_child function

- • oid_first function

- • oid_name function

- • oid_next function

- • oid_null function

- • oid_parent function

- • oid_valid function



---

# oid_gentext

# oid_gentext

oid_gentext ( oid [, after ])

The oid_gentext function returns the generated text for the oid as an SGML string. It returns the null string if the oid does not exist or does not have any generated text.

The after parameter specifies that generated text that follows the element's content (that is with placemnt=after ) should be returned. If this parameter is omitted (or 0 ), generated text that precedes the element content, (that is with placemnt=before ) is returned.



---

# oid_gentext_source

# oid_gentext_source

oid_gentext_source ( oid )

The oid_gentext_source function returns the object identifier of the source element that was used in #CONTENT to create the generated text object specified by oid . If oid is not a generated text OID or is not from #CONTENT , oid_gentext_source returns oid_null() .

The oid_gentext_source function is intended to be called from functions that are called as a result of the attloc=system-func FOSI setting.

## Related Topics

- • oid_gentext function

- • oid_is_gentext function

- • fosivar_value function



---

# oid_get_icon

# oid_get_icon

oid_get_icon ( oid [, index ])

This function returns the name of the display icon that appears to the left of the specified oid . The icons appear in the Document Map and also appear in the Edit window. However, whether the icons appear in the Edit window is dependent on the settings of the set showiconsfulltags , set showiconspartialtags , and set showiconsnotags commands. A list of returnable icon names is available in the help topic for the oid_set_icon function.

An element can have one or two icons associated with it through oid_set_icon . The index parameter may be set to 1 or 2 to retrieve the first or second icon, respectively. If index is omitted, then the first icon is returned.

If the specified oid does not have the specified icon, index is something other than 1 or 2 , or oid is invalid, the function returns the string None .

The following example gets the icon for the oid to the left of the cursor:

```
$icontype = oid_get_icon(oid_current_tag())
```

## Related Topics

- • Document Map icons



---

# oid_graphic_current_view

# oid_graphic_current_view

oid_graphic_current_view ( oid )

This function returns the current view displayed for the EDZ or ISO intelligent graphic referenced by oid . A view is a custom display of the intelligent graphic that was created and saved inside of the graphic. If oid is invalid or does not refer to an intelligent graphic, the function returns an empty string. If the current view of the intelligent graphic is the default view, the function also returns an empty string.

## Related Topics

- • Intelligent graphics overview



---

# oid_graphic_format

# oid_graphic_format

oid_graphic_format ( oid )

This function returns the graphic file format of the graphic referenced by oid . If the oid is invalid or does not reference a graphic, the function returns an empty string.

The returned value can be one of the following formats:

- • sunbm — Sun Bitmap

- • xbm — X Bitmap

- • eps — Encapsulated PostScript file

- • cur — Windows Cursor file

- • drw — IslandDraw DRW file

- • sunicon — Sun Icon file

- • tif — Tag Image File Format

- • drwunc — IslandDraw DRAW file (not compressed)

- • png — Portable Network Graphics

- • wmf — Windows metafile

- • icon — Windows icon

- • pcx — PC Paintbrush File Format

- • bmp — Windows Bitmap

- • cgm — Computer Graphics Metafile

- • gif — Graphic Interchange Format

- • jpg — Joint Photographic Exports Group

- • calsG4 — CALS raster (G4)

- • svg — Scalable Vector Graphics

- • idr — Arbortext IsoDraw file

- • idrz — Arbortext IsoDraw file

- • iso — Arbortext IsoDraw file

- • isoz — Arbortext IsoDraw file

- • edz — Creo View file

- • pvz — Creo View file

## Related Topics

- • graphic_format function



---

# oid_graphic_pathname

# oid_graphic_pathname

oid_graphic_pathname ( oid )

If oid is a graphic tag, this function returns the path name for the graphic. If oid is invalid, or is not the oid for a graphic tag, this function returns the null string. If the path name comes from a tag attribute value, this function expands character and entity references.

The function attempts to resolve relative paths using the base URI for the location where the graphics element is located before attempting to resolve the path using the document directory or directories from the graphicspath . The base URI and the document directory are often the same, but may be different when the graphic element is contained in an XInclude, file entity, or other included content.

In addition, if the graphics reference value is a relative filename that cannot be resolved to an absolute path name because the file does not exist, the string returned will be the absolute path name for the document directory concatenated to the relative name. This prevents the relative name from being inadvertently resolved to a file in the current working directory. However, if the document in question has not been saved, there is no document directory and the graphic name (which may be an absolute or a relative name) will be returned as is.

Consider the following markup:

```
<inlinegraphic
fileref="http://server/cgi-bin/script?param1=value1&amp;param2=value3"/>
```

If the oid for this tag is contained in the variable o , and you call oid_graphic_pathname :

```
local path = oid_graphic_pathname( o )
```

then the path name would contain the string:

```
http://server/cgi-bin/script?param1=value1&param2=value3
```

Note that the &amp; character entity reference was expanded to the & character.

## Related Topics

- • set graphicspath command



---

# oid_graphic_size

# oid_graphic_size

oid_graphic_size ( oid , width , height , switch )

This function returns the size of the image displayed for the graphic or equation identified by oid . The image width in pixels is returned in the output variable given by width , the height in pixels in the output variable given by height .

If switch is 0 (the default), oid_graphic_size returns the displayed size of the graphic, which may be scaled. If switch is 1 , then oid_graphic_size returns the defined size of the graphic.

This function returns 1 (true) if it succeeds, and 0 (false) if it fails, for example, if oid is not an equation or graphic. If it fails, the function writes an error message to the $ERROR predefined variable .

## Related Topics

- • oid_write_graphic function



---

# oid_graphic_viewer

# oid_graphic_viewer

oid_graphic_viewer ( oid )

This function returns the name of the embedded ActiveX dialog used to display the intelligent graphic identified by oid . If the intelligent graphic is an EDZ graphic and displayed by ProductView, the function returns pview . If the intelligent graphic is an ISO graphic and displayed by Arbortext IsoView , the function returns iview . If oid does not reference an intelligent graphic, the function returns an empty string.

## Related Topics

- • Intelligent graphics overview

- • graphic_viewer function



---

# oid_has_attr

# oid_has_attr

oid_has_attr ( oid , attrname )

This function returns 1 (True) if the start tag identified by oid specifies a value for the attribute named attrname . If the start tag does not specify a value for attrname , or if oidattrname is not a valid attribute name, this function returns 0 .

This is different from the function tag_has_attr that tests if a given attribute is declared for the element in the DTD.

## Related Topics

- • tag_has_attr function



---

# oid_id_attr_name

# oid_id_attr_name

oid_id_attr_name ( oid )

This function returns the name of the ID attribute for the element specified by oid . oid_id_attr_name returns the null string if the oid is not valid or the element does not declare an ID-type attribute.

## Related Topics

- • link_idref_attr_name function

- • target_id_attr_name function



---

# oid_in_doc

# oid_in_doc

oid_in_doc ( oid , doc )

This function returns 1 (True) if oid belongs to the document tree specified by doc .



---

# oid_include_expand

# oid_include_expand

oid_include_expand ( oid [, pos [, flags ]])

This function returns the state of the nearest enclosing included object for the specified oid and character location pos , either expanded or collapsed.

If flags is omitted, and the specified oid is not in an included object, this function returns a -1 . If flags is omitted, this function returns a 1 if the enclosing object is expanded, and a 0 if it is collapsed.

The flags parameter is a bitmask that controls the following options. It is constructed by using OR for the flags from the following list:

- • 0x01 — Causes the include to be expanded (if it is not already) to show the contents of the included object. If not set, the include will be collapsed (if it is not already) to show the xinclude markup itself

- • 0x02 — Prompts the user to save any unsaved changes if the collapse or expand would cause those changes to be lost. If not set, no prompting or saving occurs.

pos can be any of the following values:

- • 0 — (The default.) pos is immediately after the start tag identified by oid .

- • -1 — pos is immediately before the end tag of the element identified by oid .

- • -2 — pos is immediately before the start tag.

- • -3 — If oid is a start tag, pos is immediately after the end tag. Otherwise, pos is at the end of the object.



---

# oid_invalid_markup

# oid_invalid_markup

oid_invalid_markup ( oid )

This function returns 0 if the start tag identified by oid contains no invalid markup. This means it is a foreign namespace element, or it is a declared element and all of its attributes are declared and have valid values.

If this function does not return 0 then the result is a bit mask that can be inspected to determine which parts of the tag are invalid.

- • 0x01— This bit will be set if the element is not declared and is not a foreign namespace element.

- • 0x02— This bit will be set if a declared attribute has a value which is invalid for that attribute type.

- • 0x04— This bit will be set if there are attributes which are undeclared for that element.

Example:

```
function give_invalid_status(oid)
{
local oim
local result
oim = oid_invalid_markup(oid)
result = ""
if (oim == 0){
result .= "Start tag contains no invalid markup."
} else {
if (oim & 0x01) {
result .= "Start tag is undeclared. "
}
if (oim & 0x02) {
result .= "Start tag contains an invalid \
attribute value for a declared attribute. "
}
if (oim & 0x04) {
result .= "Start tag contains an undeclared \
attribute. "
}
}
response(result)
}
```

## Related Topics

- • oid_unknown function

- • oid_unknown_attr_list function



---

# oid_invalidate_graphic

# oid_invalidate_graphic

oid_invalidate_graphic ( oid )

This function resolves, reloads, and redraws (if displayed) the graphic associated with oid . This function does not modify the document, so it can be used with a read-only document or an unlocked entity.

## Related Topics

- • doc_invalidate_graphics function



---

# oid_is_gentext

# oid_is_gentext

oid_is_gentext ( oid )

This function returns a one (1) if oid is valid and is generated text. This function returns a zero (0) if oid is invalid, or is part of the loaded document instance.



---

# oid_last

# oid_last

oid_last ([ doc ])

This function returns the object identifier of the last object in the document tree given by doc , or the current document if doc is omitted or 0 .

Examples

This function could be written using oid_child as follows:

```
function oid_last(doc = 0)
{
local o = last = oid_first(doc)
# just go right as deep as we can
while (oid_valid(o)) {
last = o
o = oid_child(o, -1); # get last child
}
return last
}
```

However, using the built-in oid_last function is more efficient.

## Related Topics

- • oid_child function

- • oid_first function

- • oid_valid function



---

# oid_level

# oid_level

oid_level ( oid1 , oid2 )

This function returns the number of levels of ancestry between the elements specified by oid1 and oid2 or 0 if the elements are not related, that is, neither OID contains the other. If oid1 contains oid2 , then the level number is positive. If oid2 contains oid1 , then the level number is negative.

Examples

This function could be written using oid_parent as follows:

```
function oid_level(o1, o2)
{
local i, p, o
if (o1 == o2) { return 0;}
if (o1 < o2) {
o = o1
p = oid_parent(o2)
} else {
o = o2
p = oid_parent(o1)
}
# walk up parent tree until o is found
for (i = 0; oid_valid(p); ) {
i++;
if (p == o)
{ return o == o1 ? i : -i;}
p = oid_parent(p)
}
return 0; # not related
}
```

## Related Topics

- • oid_parent function



---

# oid_logical_mate

# oid_logical_mate

oid_logical_mate ( oid )

This function returns the logical mate of an oid. The logical mate is a singleton that acts as a mate to the first parameter, but is not an end tag in the XML structure. The function can also return the start mate that matches an end mate.

The function returns the null oid if the argument is not a valid oid, an oid that cannot take a logical mate, or if the logical mate is not present in the document. The latter condition means that the document is semantically incomplete or unbalanced.



---

# oid_modified

# oid_modified

oid_modified ( oid [, value ])

This function returns the current “modified” state for the specified oid . If the specified oid has been modified since the last save operation (or since oid_modified was used to set the oid to “unmodified”), the function returns a one (1). If the oid has not been modified, the function returns a zero (0).

If the optional value parameter is included, the function still returns the current “modified” state of the specified oid , but also sets the “modified” state to the specified value . The value parameter must be either a one (1) for “modified”, or a zero (0) for “unmodified.”

Examples:

```
$mod = oid_modified(oid_current_tag())
$ret = oid_modified(oid_next(),1)
```



---

# oid_modify_attr

# oid_modify_attr

oid_modify_attr ( oid , [attrname] , [value] )

This function sets the attribute named attrname to value for the element specified by oid . If you do not specify either attrname or value , the Modify Attributes dialog is raised.

Returns 1 (True) unless:

- • there is no such attribute for the element, or

- • oid is invalid, or

- • the document is read-only

oid_modify_attr can be used to assign XML namespace attributes to elements in an XML document.



---

# oid_mouse_pos

# oid_mouse_pos

$oid = oid_mouse_pos ( pos [, doc [, flag ]])

This function returns the oid corresponding to the current mouse position. If the mouse pointer is pointing directly at the begin or end tag of an element, the oid returned corresponds to that element.

The pos parameter is an output variable to hold the character offset from the element's start tag to the character closest to the mouse pointer.

The doc parameter specifies the document to operate upon. If doc is omitted or 0 , the value returned by current_doc is used.

When the mouse pointer is not pointed directly at the begin or end tag of an element, the value of flag has no effect. But when the mouse pointer is pointed directly at the begin or end tag of an element, flag works as follows:

- • If flag is 1 , then oid_mouse_pos evaluates whether the mouse pointer is closer to the left or right side of a tag. The function will return the oid that is outside the tag pair if the mouse is pointing at the left half of the begin tag or the right half of the end tag.

- • If flag is omitted or 0 , then oid_mouse_pos returns the oid which is inside the tag under the mouse pointer.

The following code will produce a result similar to the command caret mouse , unless the mouse is pointing directly at a begin or end tag. If the mouse is pointing directly at a begin or end tag, the caret will always be positioned inside the tag pair. With the caret mouse command, however, the caret will be positioned outside the tag pair if the mouse is pointing at the left half of the begin tag or the right half of the end tag.

```
local oid, pos
oid = oid_mouse_pos(pos)
goto_oid(oid, pos)
```



---

# oid_name

# oid_name

oid_name ( oid )

This function returns the name of the element identified by oid or the null string if the oid is not valid. If this function returns _file_ent , you can use the entity_name function to find the name of the entity.



---

# oid_namespace_prefix

# oid_namespace_prefix

oid_namespace_prefix ( oid , uri )

This function returns the prefix for the uri that is active at the specified oid . If no prefix is declared for the namespace URI, then the function returns a null string.

## Related Topics

- • oid_namespace_uri function



---

# oid_namespace_prefix_defined

# oid_namespace_prefix_defined

oid_namespace_prefix_defined ( oid , uri )

This function determines whether a uri is defined at an oid . If the given uri is not defined at the specified oid , then the function returns a 0 . If the given uri is defined at the specified oid , then the function returns a 1 .

Following is some example code using this function:

```
if (oid_namespace_prefix_defined(oid, uri)) {
local prefix = oid_namespace_prefix(oid, url);
if (prefix == "") {
# This namespace is the default namespace at this oid.
}
else {
# This namespace is not the default namespace at this oid.
# However, it is defined and has a prefix whose value is in
# the variable 'prefix'.
}
}
else {
# This namespace is not defined at this oid.
}
```

## Related Topics

- • oid_namespace_prefix function



---

# oid_namespace_stack

# oid_namespace_stack

oid_namespace_stack ( oid , prefixArray , uriArray )

This function fills prefixArray and uriArray with the prefixes and URIs that are active at oid . This function returns the number of prefix and URI pairs stored in the arrays.

## Related Topics

- • oid_namespace_uri function



---

# oid_namespace_uri

# oid_namespace_uri

oid_namespace_uri ( oid [, prefix ])

This function returns the URI for the prefix that is active at oid . If prefix is not supplied, the function returns the URI of the active default namespace at oid .

## Related Topics

- • oid_namespace_stack function

- • oid_namespace_prefix function



---

# oid_next

# oid_next

oid_next ( oid )

This function returns the OID of the sibling following the element specified by oid or oid_null if oid is the last child.

## Related Topics

- • oid_level function

- • oid_parent function



---

# oid_null

# oid_null

oid_null ( )

This function returns an OID that represents no object. Several OID functions return oid_null ; for example, oid_parent returns oid_null for the outermost element in a document. By definition, oid_valid(oid_null) is 0 .

## Related Topics

- • oid_caret function

- • oid_child function

- • oid_next function

- • oid_parent function

- • oid_prev function

- • oid_valid function



---

# oid_offset

# oid_offset

oid_offset ( oid , pos1 , oid2 , pos2 )

This function returns the character offset between the two document locations specified by oid1,pos1 and oid2,pos2 respectively. Each non-text object (that is, markup, equations, graphics) counts as one character. The offset returned will be negative if the location specified by oid2,pos2 comes before the position specified by oid1,pos1 .

## Related Topics

- • Object identifier (OID) functions



---

# oid_parent

# oid_parent

oid_parent ( oid )

This function returns the OID of the immediate ancestor of the object specified by oid or oid_null if oid has no parent.

## Related Topics

- • oid_child function

- • oid_next function

- • oid_prev function



---

# oid_paste_valid

# oid_paste_valid

oid_paste_valid ( oid [, pos [, pastedoc ]])

This function determines if it is valid to paste the contents of the paste buffer at the document location specified by oid , pos . If pos is omitted or 0 , the location to the right of the start tag identified by oid is used. The pastedoc argument specifies the document identifier of the paste buffer to test. If 0 or omitted, the default paste buffer is used.

oid_paste_valid returns one of the following integers:

- • 2 — Paste is valid after fix ups, for example, adding required tags.

- • 1 — Paste is valid.

- • 0 — Paste is invalid. For example, the destination is protected, the region to paste is unbalanced, or context errors would result.

- • -1 — Paste may be valid, but involves pasting tags from a different document type, or the paste buffer is the default paste buffer and the system currently owns the clipboard.

Note, oid_paste_valid does not check if it is valid to paste tags from a different document type, for example, where the structures are same.

## Related Topics

- • cut_valid function

- • delete_markup_valid function

- • oid_expose function

- • oid_show_attr function



---

# oid_prev

# oid_prev

oid_prev ( oid )

This function returns the OID of the sibling preceding the element specified by oid or oid_null if oid is the first child.

## Related Topics

- • oid_next function



---

# oid_prompt_attrs

# oid_prompt_attrs

oid_prompt_attrs ( oid )

This function opens the Modify Attributes dialog box for the tag associated with oid if the tag has unspecified required attributes and the requireattrs set option is on , or if the tag has any declared attributes and the promptattrs set option is on .

If oid is not associated with a valid tag, the function returns 0 . If the dialog box is not required to be opened, or if the dialog box is opened and is accepted, the function returns 1 . If the dialog box is opened and the user cancels, the function returns 0 and the current operation is undone.

This function is useful when a tag needs to be inserted with prompts temporarily turned off, but then later the prompts are desirable.



---

# oid_protected

# oid_protected

oid_protected ( oid )



This function returns 1 (True) if the content of the element specified by oid is protected so that no edits are allowed.

## Related Topics

- • set protection command



---

# oid_read_only

# oid_read_only

oid_read_only ( oid [, value ])

This function returns the current “read only” state for the specified oid . The oid-level read only state is a feature that is not manipulated by the default Arbortext Editor features and functions. The oid-level read only state is only changed/used if an ACL programmer specifically uses this function to change the read only state.

If the specified oid has been set to a “read only” state, the function returns a one (1). If the oid has not been set to a “read only” state), the function returns a zero (0).

If the optional value parameter is included, the function still returns the current “read only” state of the specified oid , but also sets the “read only” state to the specified value . The value parameter must be either a one (1) for “read only”, or a zero (0) for “not read only”.

Examples:

```
$mod = oid_read_only(oid_current_tag())
$ret = oid_read_only(oid_next(),1)
```



---

# oid_root

# oid_root

oid_root ([ doc ])

This function returns the OID of the root element (the first element start tag in a well formed document) in the document. oid_root takes an optional argument, doc , that specifies the identifier of the document tree. If doc is omitted or 0 , then the current document is used.

oid_root returns oid_null if the document is not well formed. (For example, if doc is a fragment that has multiple top level elements.)



---

# oid_same_doc

# oid_same_doc

oid_same_doc ( oid1 , oid2 )



This function returns 1 (True) if oid1 and oid2 belong to the same document tree.



---

# oid_select

# oid_select

oid_select ( oid [, invert [, primary [, include ]]])

This function marks the contents of the element specified by oid . The contents may be obtained by referencing the main::selection variable. This function returns 1 (True) if oid was marked or 0 (False) if the element has no content. If invert is 0 , then the marked region is not highlighted. The default is 1 , that is, the region is inverted.

If primary is 0 , then the primary selection is not claimed. The default is 1 , that is, the selection is asserted.

The optional fourth argument include , if non-zero, causes the start tag (and end tag if not EMPTY) for the element given by oid to be included in the selection. The default is 0 , that is, the element tags are not included.

This function returns the content of an element without affecting the screen display:

```
function oid_content(o)
{
if (oid_empty(o)) { return "";}
oid_select(o, 0, 0)
return main::selection
}
```

## Related Topics

- • mark command

- • Packages ( main::selection variable)

- • oid_content function



---

# oid_set_graphic_pathname

# oid_set_graphic_pathname

oid_set_graphic_pathname ( oid , path )

If oid is a graphic tag, this function sets the path name for the graphic. If the graphic element supports a file reference attribute, that is used to set the path. If the element only supports an entity reference attribute, then a new graphic entity is declared and assigned to the attribute. When the parent document is a file system object, the new entity name is formed from the base name of the file (modified to be a valid entity name, if necessary). When the parent document is an object stored in a content management system, the new entity name is formed by prepending &E to a Universal Unique Identifier (UUID). If the path name is already declared as a graphic entity, then the existing entity name is used.

The path name value is stored as a relative path (as determined by graphic_relative_path ) if possible, so that the reference is still valid if the document and graphic are moved to a different file system.

If oid is invalid, or is not the oid for a graphic tag, this function generates an error.

## Related Topics

- • oid_graphic_pathname function

- • graphic_relative_path function

- • insert_graphic_file function



---

# oid_set_icon

# oid_set_icon

oid_set_icon ( oid , icon [, index ])

This function sets the display icon that appears to the left of the specified oid . The icons appear in the Document Map and also appear in the Edit window. However, whether the icons appear in the Edit window is dependent on the settings of the set showiconsfulltags , set showiconspartialtags , and set showiconsnotags commands.

Specify the icon by specifying one of the supported icon names or by specifying a path and file name to a .bmp . If an invalid display icon is set, the built-in icon None will be displayed.

Specify a .bmp file using either a full or relative path. If you use a relative path, the graphicspath is searched. You can save icons in .bmp files in the Arbortext-path \custom\graphics directory. Icon graphics should have the BMP transparency set to pink. If the .bmp file is not found, then the behavior is as though no file was specified. The number of unique icons specified using a .bmp file are limited to 200. If this limit is reached, additional specified .bmp files behave as though no file was specified. If the .bmp is not found, the built-in icon None will be displayed.

You can use the icon names listed in the following table, which are case sensitive.

An element can have one or two icons associated with it. The index parameter may be set to 1 or 2 to set the first or second icon, respectively. If index is omitted, then the first icon is set.

If the specified oid is invalid or index is something other than 1 or 2 , the function returns a zero ( 0 ).

Otherwise, this function returns a one ( 1 ). If you specify an invalid icontype , the element is given an icon of None and the function still returns a one ( 1 ).

The following example sets the icon for the oid to the left of the cursor to the Locked icon.

```
$ret = oid_set_icon(oid_current_tag(),"Locked")
```

## Related Topics

- • oid_get_icon function

- • Document Map icons



---

# oid_show_attr

# oid_show_attr

oid_show_attr ( oid [, newval ])

This function returns 1 (True) if the attribute lines for the element identified by oid are displayed in the Document Map window. It returns 0, otherwise.

If newval is specified, it changes the state of the attribute display for oid . If 0 , the attribute lines are removed (collapsed). If non-zero, the attribute lines are displayed (if the element has any non-default attributes).

Note, the effect of this function is visible in the Document Map and Column view only.

## Related Topics

- • cut_valid function

- • delete_markup_valid function

- • oid_expose function

- • oid_paste_valid function



---

# oid_split_tag

# oid_split_tag

newoid = oid_split_tag ([ flags [, oid [, pos ]]])

This function divides the element based on the location specified by oid and pos .

- • flags — Optional. Sets options for the split operation. A value of one ( 1 ) specifies that all non-default attributes on the original element be duplicated on the newly created element. ID attributes (which should be unique across a document) are not duplicated. A value of zero ( 0 ) ensures that no attributes are duplicated on the newly created element. If the flags parameter is not specified, a value of 0 is assumed.

- • oid — Optional. The oid of the element to split. If oid is omitted, the function uses oid_caret .

- • pos — Optional. The character position at which to split. If pos is omitted, a value of 0 is assumed.

The split command is equivalent to calling the oid_split_tag function with no parameters. The EditSplit alias (used by the UI) is equivalent to calling oid_split_tag with a flags parameter of 1 .

## Related Topics

- • split command



---

# oid_tbl_obj_list

# oid_tbl_obj_list

count= oid_tbl_obj_list ( oid , array )

This function fills array with the IDs of the table objects associated with oid , which must refer to a markup tag. It returns the number of IDs . Note that a zero return is not necessarily an error; not all OIDs have associated table objects.

The array is an associative array with the following indices:



---

# oid_top_pos

# oid_top_pos

oid_top_pos ( pos [, doc ])



This function returns the OID of the object displayed in column 1 on the top line of the window containing the document specified by doc . If doc is omitted or 0 , the current document is used. The oid_top_pos function also sets the output variable pos to the character position following the top left column of the window.

This function is useful for restoring a screen position using scroll_to_oid , for example,

```
o = oid_top_pos(pos)
...
scroll_to_oid(o, pos)
```

## Related Topics

- • scroll_to_oid built-in function



---

# oid_treeloc

# oid_treeloc

oid_treeloc ( oid [, sep_char [, top_level_oid ]])

This function returns a string indicating the tree location in the current document of the tag specified by oid . For example, the returned string 1.3.2 refers to the second tag ( 2 ) of the third tag ( 3 ) of the first tag ( 1 ) in the document.

Specify a separator character sep_char to delineate the values in the string with a character other than “.”, which is the default.

To limit the size of the returned value, specify a top_level_oid . This sets the parent tag at which the tree location will begin. If you do not specify a top_level_oid , the first value in the returned tree location represents the first tag in the document containing oid .



---

# oid_type

# oid_type

oid_type ( oid )



This function returns a number that identifies the type of the object specified by oid . The return value is one of the following integers:

- • -1 — OID is invalid

- • 0 — object is an element

- • 1 — object is a user-defined tag alias of a DTD tag

- • 4 — object is an equation image

- • 7 — object is a processing instruction (includes Arbortext Editor -supplied tags)

- • 8 — object is a user-defined alias of a processing instruction or unknown element

- • 9 — object is an SGML comment

- • 10 — object is an IGNORE marked section

- • 11 — object is a CDATA marked section

- • 12 — object is an RCDATA marked section

- • 30 — object is a change tracking markup tag

## Related Topics

- • oid_unknown function

- • oid_invalid_markup function

- • tbl_oid_cell function



---

# oid_unknown

# oid_unknown

oid_unknown ( oid )

This function returns 1 (True) if the start tag identified by oid is not a declared element in the DTD, or if the start tag is a declared element, this function returns 0 .

## Related Topics

- • oid_invalid_markup function

- • oid_unknown_attr_list function



---

# oid_unknown_attr_list

# oid_unknown_attr_list

oid_unknown_attr_list ( oid , arr )

This function fills the associative array arr with a list of unknown attributes set for the element identified by oid . This function returns the number of unknown attributes in the array or 0 if the element has no unknown attributes. Each unknown attribute is stored in the array using the attribute name as the key, and its value as the array element value.

Example:

```
function show_unknown_attrs(oid)
{
local ual[]
local count
count = oid_unknown_attr_list(oid, ual)
if (count == 0){
response("The given oid has no unknown attributes.")
} else {
local ua
local i = 1
local ual2[]
# Convert from an associative array to a normal array
# so it can be used with list_response().
for (ua in ual) {
ual2[i++] = ua . "=" . ual[ua]
}
list_response(ual2, "List of Unknown Attributes")
}
}
```

## Related Topics

- • oid_attr_list function

- • oid_invalid_markup function

- • oid_attr function

- • oid_modify_attr function

- • oid_delete_attr function



---

# oid_valid

# oid_valid

oid_valid ( oid )

This function returns 1 (True) if the object identified by oid is valid, such that the object still exists and oid !=oid_null() .

## Related Topics

- • oid_null function



---

# oid_visible_change_tracking

# oid_visible_change_tracking

0|1 = oid_visible_change_tracking ( oid [, mode ])

This function determines if the element specified by oid is visible with respect to a given change tracking view.

- • oid — The element being checked. oid_visible_change_tracking returns 0 or 1 if oid is not visible or is visible, respectively, when the document is shown in the given change tracking view.

- • mode — Optional. Specifies a particular change tracking view. Valid values include:



---

# oid_write_graphic

# oid_write_graphic

oid_write_graphic ( oid , path [, type [, attrmask [, quality [, cgmprofile ]]]])

This function creates a graphic file based on the element identified by oid in the file format specified by type and writes the output file to the specified path . The attrmask parameter indicates how the graphic element should be scaled. The quality parameter can be used for JPEG graphics to better control the output file size balanced against output quality. The cgmprofile parameter can be used for CGM graphics to specify the CGM profile for the graphic.

A relative path is relative to the current working directory.

If oid refers to an intelligent graphic, the type can be eps , jpg , png , or cgm . If the type is set to cgm , the cgmprofile parameter can be used to specify the CGM profile for the graphic.

The settings of the reproDepth and reproWidth attributes on oid are used to create the graphic file. If none of these attributes are specified, the default values are used.

For graphics other than intelligent graphics, type can be "gif" , "png" , "jpg" , or "jpeg" . If type is omitted, the function will convert the element to GIF format.

attrmask can have the following values:

- • 0 — Indicates the graphic should be scaled exactly as displayed in the Edit pane.

- • 1 — Indicates the graphic should be scaled based on the screen resolution.

If the graphic is an intelligent graphic, attrmask is ignored.

You can specify quality for a JPEG graphic. Set the value to a number from 1 to 100, where 1 is lowest quality and smallest file size and 100 is highest quality and largest file size. You may need to experiment with this setting for best results. The default is 80 . If type is "gif" or "png" or if the graphic is an intelligent graphic, any value specified for quality is ignored.

You can specify the cgmprofile for a CGM graphic. If cgmprofile is not set, then the value of the set cgmprofile preference is used. If that preference is also not set, the WebCGM 2.0 profile is used. The following CGM profiles are supported:

- • WebCGM_2.0

- • WebCGM_1.0

- • ISO_8632_:_1999

- • ATA_GREXCHANGE_V2.10

- • ATA_GREXCHANGE_V2.9

- • ATA_GREXCHANGE_V2.8

- • ATA_GREXCHANGE_V2.7

- • ATA_GREXCHANGE_V2.6

- • ATA_GREXCHANGE_V2.5

- • ATA_GREXCHANGE_V2.4

- • ATA_GREXCHANGE_V2.5/IsoDraw

- • CALS_MIL-D-28003A

- • SAE_J2008

- • Model_Profile_(ISO_8632:1992/Am.1:1994)

- • ISO_ISP_12071-1_(FCG11)_(Draft)

- • ISO_ISP_12071-2_(FCG23)_(Draft)

- • ISO_ISP_12071-3_(FCG32)_(Draft)

- • ISO_ISP_12071-4_(FCG33)_(Draft)

- • S1000D_V2.3

- • S1000D_V2.2

This function returns 1 (True) if the conversion succeeds, and 0 (False) if it fails. If it fails, the function writes an error message to the $ERROR predefined variable .

The following example converts every graphic and equation in a document to GIF format:

```
$g=0
$e=0
$o=oid_first()
while (oid_valid($o)) {
if (oid_is_graphic($o))
{
$gname = "c:\\temp\\graphic" .$g. ".gif"
oid_write_graphic($o,$gname)
$g = $g + 1
}
if (oid_type($o)== 4)
{
$ename = "c:\\temp\\equation" .$e. ".gif"
oid_write_graphic($o,$ename)
$e = $e + 1
}
$o = oid_forward($o)
}
```

## Related Topics

- • EPS

- • GIF

- • JPEG

- • PNG

- • Enabling graphics support for a document type

- • Intelligent Graphics Overview

- • Graphic Conversion Support



---

# oid_xpath_boolean

# oid_xpath_boolean

This function evaluates an XPath expression in the context of an OID and returns 1 (true) if expr is true, otherwise it returns 0 (false).

- • oid — The object to use as the context node.

- • expr — A valid XPath expression.

- • nsOid (optional) — The node used for resolving namespace prefixes in the XPath expression.

A typical boolean expression will use one of the XPath boolean operators ( = , != , < , > , >= , <= ). For example,

```
count(sect1)=0
```

Non-boolean results are converted to boolean using standard XPath rules:

- • The numbers zero ( 0 ) and NaN (not a number) are converted to false . Other numbers are converted to true .

- • Node set expressions returning at least one node are converted to true . Empty node sets are converted to false .

- • Strings are converted to true if they contain at least one character (including white space). Empty strings are converted to false .

To handle errors, call this function from within a catch .

## Related Topics

- • xpath_boolean function

- • oid_xpath_integer function

- • oid_xpath_nodeset function

- • oid_xpath_string function



---

# oid_xpath_integer

# oid_xpath_integer

This function evaluates an XPath expression in the context of an OID. This function evaluates expr as a floating-point number, rounds to the nearest integer, and returns that integer.

- • oid — The object to use as the context node.

- • expr — A valid XPath expression that can be represented as an integer.

- • nsOid (optional) — The node used for resolving namespace prefixes in the XPath expression.

Non-numeric results are converted to numbers using standard XPath rules:

- • Strings are parsed as floating-point numbers.

- • Boolean expressions are converted to 1 or 0 .

- • Node set expressions are first converted to strings, then parsed. A run-time error occurs if the result cannot be represented as an integer.

To handle errors, call this function from within a catch .

## Related Topics

- • xpath_integer function

- • oid_xpath_boolean function

- • oid_xpath_nodeset function

- • oid_xpath_string function



---

# oid_xpath_matches

# oid_xpath_matches

oid_xpath_matches ( oid , expr [, nsOid ])

This function tests whether an OID matches an XPath pattern. expr follows the same form as XSLT pattern matching expressions ( xsl:template match attribute). Returns 1 if oid matches expr and 0 if not. To handle errors, call this function from within a catch.

This function has the following parameters:

- • oid — The object to test.

- • expr — A valid XPath pattern.

- • nsOid (optional) — The node used for resolving namespace prefixes in the XPath expression.

Examples:

```
oid_xpath_matches(oid_caret(), "para")
```

Returns 1 for any para element.

```
oid_xpath_matches(oid, "chapter/para[1]")
```

Returns 1 for the first para in any chapter .



---

# oid_xpath_nodeset

# oid_xpath_nodeset

This function evaluates an XPath expression in the context of an OID and returns the result as an array of OIDs. This function can be used to identify a group of elements to be iterated through. It can also be used for navigation, for example, by passing one of the returned OIDs to goto_oid .

- • oid — The object to use as the context node.

- • arr — An unordered array of OIDs returned by expr .

- • expr — A valid XPath expression that evaluates to a node set containing only XPath nodes that have associated OIDs.

- • nsOid (optional) — The node used for resolving namespace prefixes in the XPath expression.

This function fills the array arr with the first OID of each XPath node returned by expr . The return value is the number of OIDs stored in arr . Duplicate OIDs may be returned if more than one XPath node resolves to the same OID. oid_null is returned for any XPath node that cannot be converted to an OID (for example, namespace nodes and attributes).

To handle errors, call this function from within a catch .

## Related Topics

- • xpath_nodeset function

- • oid_xpath_boolean function

- • oid_xpath_integer function

- • oid_xpath_string function



---

# oid_xpath_string

# oid_xpath_string

This function evaluates an XPath expression with respect to an OID and returns the result of expr converted to a string.

- • oid — The object to use as the context node.

- • expr — A valid XPath expression.

- • nsOid (optional) — The node used for resolving namespace prefixes in the XPath expression.

Non-string results are converted to strings using standard XPath rules:

- • Boolean expressions are converted to the string “ true ” or “ false ”

- • Node set expressions return the string value of the first node, or an empty string if the node set is empty.

- • Numbers are not specially formatted.

To handle errors, call this function from within a catch .

## Related Topics

- • xpath_string function

- • oid_xpath_boolean function

- • oid_xpath_integer function

- • oid_xpath_nodeset function



---

# open

# open

open ( path [, access ])

This function opens the file specified by path and returns an identifier that may be used in subsequent calls to getline , put , close , and other I/O functions. The path name is expanded using expand_file_name to resolve directory references and environment variables.

The access argument determines how the file is to be accessed. It must have one of the following values:

- • r — open for reading only. The file must already exist.

- • w — open for writing only. The file is created if it does not exist or truncated if it does.

- • a — open for writing only. The file is created if it does not exist; if it does, then the pointer is positioned so that new output is added to the end of the file.

- • r+ — open for reading and writing. The file must already exist.

- • w+ — open for reading and writing. The file is created if it does not exist or truncated if it does.

- • a+ —open for reading and writing. The file must already exist and the pointer is positioned so that new output is added to the end of the file.

In addition, the following character may be appended to any of the access strings:

- • b — open in binary mode. This is required to read/write binary files using the read and write functions. If b is not specified, then characters read from a file will be converted from the system character set to Unicode and vice-versa on output.

The default for access is r .

If a file is opened for both reading and writing, then a seek must be used between a read and a write operation.

There is a limit of, at most, 20 open file identifiers. The number may be less depending on the operating system.

If the file cannot be opened, open returns -1 .

The open function also supports the special path names allowed for the output= option of the eval and show commands. If the first character of the output file starts with a question mark ? , then the file name is actually a variable name whose value is set to the output written to the file identifier. If the second character is > , then the output is appended to the current value of the variable instead of replacing it. For example,

```
fid = open("?OUTPUT", "w")
```

returns a file identifier that can be used with put to write to a variable. The open function also supports the "*" (asterisk) output specification to write to the message window, thus

```
fid = open("*", "w")
```

returns a file identifier that can be used with put to send output to the message window. These extensions allow a generic output function to be written that can write to a file, variable or message window.

## Related Topics

- • expand_file_name built-in function

- • put built-in function

- • seek built-in function

- • Opening, referencing, and saving files



---

# open_accept

# open_accept

open_accept ( ch )



This function opens a network connection to a client using the channel identifier ch returned by a previous call to open_listen . open_accept returns -1 on failure and sets the predefined variable api_error o an error message describing the error.

open_accept is normally called from the callback established by open_listen , which responds to an open notification for the listening channel. Otherwise, open_accept locks until a connection is made.

By default, the channel is opened in a blocking mode. This means that a read from the channel blocks until the operation completes. channel_set_callback can be used to change the channel so that subsequent reads (and writes) can be non-blocking.

The original listening channel remains open.

See open_listen for an example.

## Related Topics

- • channel_set_callback built-in function

- • close built-in function

- • open_listen built-in function

- • read built-in function

- • write built-in function



---

# open_connect

# open_connect

open_connect ( host , port )



This function opens a network channel to a TCP service on the specified host. host is the name of the host to connect to or its IP address. port is the integer port number to connect to (for example, 25), or the name of the service desired, such as, “smtp”.

open_connect returns a channel identifier on success that can be used in subsequent calls to read , write , close and other channel functions. It returns -1 on failure and sets the predefined variable api_error to an error message describing the error.

By default, the channel is opened in a blocking mode. This means that a read from the channel blocks until the operation completes. channel_set_callback can be used to change the channel so that subsequent reads (and writes) can be non-blocking.

The sample function that follows uses open_connect to fetch an HTML document from an HTTP server (well known port 80). For clarity, it does minimal error checking and does not deal with the MIME headers that are normally transmitted preceding the actual document. This example also reads from the channel using blocking reads. See channel_set_callback for an example using asynchronous reads, the preferred method to use.

Examples

```
function http_get(host, remotepath, lclfile)
{
local of = open(lclfile, "wb")
if (of < 0) {
message "http_get: couldn't open $lclfile for write"
return 0;
}
local ch = open_connect(host, 80)
if (ch < 0) {
message "http_get: $main::api_error"
return 0;
}
write(ch, "GET " . remotepath . " HTTP/1.0\r\n\r\n")
local buf, len
while ((len = read(ch, buf, 512)) > 0) {
write(of, buf, len)
}
close(ch);
close(of)
return len == 0
}
```

## Related Topics

- • channel_set_callback built-in function

- • close built-in function

- • read built-in function

- • write built-in function



---

# open_listen

# open_listen

open_listen ( port , funcname [, data ])



This function creates a channel to listen for incoming connections to implement a TCP service. open_listen returns a channel identifier on success that can be used in subsequent calls to open_accept . It returns -1 on failure and sets the pre-defined variable api_error to an error message describing the error.

port is the integer port on which to listen (for example, 21) or the name of the service provided, such as, “ftp”. funcname is the name of the function that can be called when a connection becomes available and must be declared as: function funcname ( ch , op [, data ]) where ch is the channel identifier returned by open_listen and op is an integer specifying the type of notification (which is always 0). This means that a connection is pending. data is the value of the user data argument passed to open_listen .

The callback function must call open_accept to create a channel for the new connection. As with the underlying Berkeley socket function, listen , open_listen limits the number of pending connections (the backlog) to 5.

The channel created by open_listen is non-blocking. It remains open until explicitly closed by calling close .

The example of the simple server that follows accepts and executes Arbortext Editor commands over a network channel. It uses a simple protocol where each incoming command is delimited by a CTRL+A character (“\001”) since commands may include embedded new lines. After executing the command, the server writes back the value of the predefined variable status as a string, again terminated by CTRL+A . The client should read the reply before sending another command.

```
package server
RE="\001"; # used as a message delimiter
function listen(port) {
local ch = open_listen(port, 'server::doaccept')
if (ch < 0) {
message "server::listen: $main::api_error"
}
return ch
}
function doaccept(ch, what) {
if (what == 0) {
local fid = open_accept(ch)
if (fid < 0) {
message "server: $main::api_error"
close(ch);
}
# set the connection to non-blocking mode
channel_set_callback(fid, 'server::notify')
}
}
function async_read(ch) {
local cmd, len
len = read(ch, cmd, 512, RE)
if (len == -2) {
return; # incomplete read
}
if (len <= 0) {
if (len == -1) {
message "server: $main::api_error"
}
close(ch)
return
}
chop(cmd); # remove RE
execute(cmd); # in context of current_doc()
# send back reply containing $status for command
write(ch, "=" . main::status . RE)
}
# Callback for I/O on server connection
function notify(ch, what) {
switch(what) {
case 0: # open
break;
case 1: #close
close (ch);
break;
case 2: # read
async_read(ch)
break;
}
}
```

## Related Topics

- • close built-in function

- • open_accept built-in function



---

# option

# option

option ( string [, session ])

This function returns the local scope (window, document, or view) value of the set option specified by string , which may be an initial substring. If the optional boolean session parameter is true, the option returns the session scope value for the set option specified by string . The result is a string which may be passed to the set command. Boolean values return on or off .

Examples

```
$ptr = option("printer");
$cxon = option("contextrules") == "on";
if (option("tabletags",1) == "off") { ...}
```

## Related Topics

- • Set option scope

- • option_scope function

- • set command



---

# option_path_list

# option_path_list

option_path_list ( name , arr )

This function returns in array variable arr the value of the path-list set option name .  It returns the number of items placed in array variable arr .  If name is not a path-list set option, or the set option has a null (empty) value, it returns 0.

Values are returned by splitting the list in the set option into separate file paths and returning one path in each array element.  For example, if set option catalogpath has the value a;b;c , where a, b, and c are each absolute paths to directories containing document type information,  this function will return a in arr[1] , b in arr[2] , and c in arr[3] .  The function itself will return 3 in this case.



---

# option_persists

# option_persists

option_persists ( option )

This function returns 1 if the value of the preference specified in option automatically persists across sessions (written to the arbortext.wcf preferences file on exit). The function return 0 if the Preferences dialog box must be used to save option . The function also returns 0 if option is not a valid preference.



---

# option_scope

# option_scope

option_scope ( option )

This function returns the scope for the specified option . Available return values are:

- • global — specified option has no local scope, only a session scope.

- • window — specified option has a session scope and a local scope of window.

- • doc — specified option has a session scope and a local scope of document.

- • view — specified option has a session scope and a local scope of view.

If the specified option is invalid, the function returns nothing.

Examples

```
eval option_scope("tagdisplay")
$ret = option_scope("showentities")
eval option_scope("gentext")
```

## Related Topics

- • Set option scope

- • set command



---

# option_set

# option_set

option_set ( name , value )

This function sets the global-scope set option name to the value value .



---

# option_type

# option_type

option_type ( option )

This function returns the type of the specified option . Possible return values are:

- • string — type is a string.

- • token — type is a token.

- • file — type is a file name.

- • pathlist — type is a path list (a list of file paths separated by a semicolon).

- • bool — type is a boolean ( on or off ).

- • number — type is an integer.

- • float — type is a floating point number.

- • color — for options that specify foreground colors, type is a color (named color or a RGB value).

- • bgcolor — for options that specify background colors, type is a color (named color or a RGB value).

- • dimen — type is a dimension (value and a unit).

- • percent — type is a dimension like dimen , but the unit may also be % .

- • enum — type is an enumerated type.

- • num_enum — type is a combination of an integer and an enumerated type.

- • hook — type is a hook function.

If the specified option is invalid, then the function returns invalid .

Examples

```
eval option_type("tagdisplay")
eval option_type("gentext")
option_type("showentities")
```



---

# option_value_max

# option_value_max

option_value_max ( option )

This function returns the maximum allowable value for the specified option .

If the specified option is invalid, or is not numeric, then the function returns -1 .

Example

```
option_value_max("fontpercent")
```

If the option's value is expressed in units, you can return the kind of units with option_value_units .

## Related Topics

- • option_values function

- • option_value_min function

- • option_value_validate function



---

# option_value_min

# option_value_min

option_value_min ( option )

This function returns the minimum allowable value for the specified option .

If the specified option is invalid or is not numeric, then the function returns -1 .

Example

```
option_value_min("outputrecordlength")
```

If the option's value is expressed in units, you can return the kind of units with option_value_units .

## Related Topics

- • option_values function

- • option_value_max function

- • option_value_validate function



---

# option_value_units

# option_value_units

option_value_units ( option )

This function returns the units being used by the specified option .

If the specified option is invalid or doesn't use units, then the function returns an empty string.

The following example obtains the unit of measure for the set docmapwrapwidth command option.

```
option_value_units("docmapwrapwidth")
```

## Related Topics

- • option_values function

- • option_value_max function

- • option_value_min function



---

# option_value_validate

# option_value_validate

option_value_validate ( option , value )

This function validates the specified value for the specified option .

If the specified value is valid, the function returns 1 . If the specified value is invalid, the function returns 0 and an explanation in an error dialog box.

Example

```
option_value_validate("tagdisplay", "full")
option_value_validate("tagdisplay", "notvalid")
```

## Related Topics

- • option_values function

- • option_value_max function

- • option_value_min function



---

# option_values

# option_values

option_values ( option , arr )

This function fills the array arr with a list of permissible values for the specified option and returns the number of entries in the array.

If the specified option is invalid or is not an enumerated type, then the function returns 0 .

Example

```
option_values("tagdisplay", $arr)
```

## Related Topics

- • option_value_max function

- • option_value_min function

- • option_value_validate function



---

# ord

# ord

ord ( value )

This function returns integer value of first character in string value of value . If the character is a Unicode character, the numeric sixteen-bit number is returned. For example the value of ord("a") is 97 .



---

# pack

# pack

pack ( template , … )

This function packs one or more values into a binary data structure, returning a byte string containing the structure. This is very similar to the Perl function of the same name. The template parameter is a sequence of characters that specify the type of each value, as follows:

- • a — an ASCII string, null padded

- • A — an ASCII string, blank value

- • c — a signed character value

- • C — an unsigned character value

- • d — a double-precision floating point number in native format

- • f — a single-precision floating point number in native format

- • i — a signed integer (32–bit) value

- • I — an unsigned integer (32–bit) value

- • l — a signed long value

- • L — an unsigned long value

- • n — a short integer value in network (big-endian) order

- • N — a long (32–bit) value in network (big-endian) order

- • p — a pointer to a null terminated string

- • s — a signed short (16–bit) value

- • S — an unsigned short (16–bit) value

- • x — a null byte

- • X — back up a byte

- • z — a Unicode string in big-endian (network) order, null padded

- • Z — a Unicode string in little-endian order, null padded

- • @ — null fill to absolute position

Each character may be followed by a number that specifies a repeat count. The character and repeat count comprise a field specifier. Field specifiers may be separated by white space. For all type specifiers except a , A , x , X , and @ , the repeat count specifies how many values from the list of arguments are to be used. For example:

```
pack("s2", 1, 2)
```

packs values 1 and 2 , into a structure of 2 shorts. If the repeat count is *, then all remaining values are used, for example:

```
pack("i*", 3, 4, 5, 6)
```

produces a structure of four integers.

The repeat code for z and Z is the number of Unicode characters. Thus, z4 results in 8-bytes written to the packed string. To get a blank-padded Unicode string, use:

```
pack("z20", ustr . dupl(" ", 20 - length(ustr)))
```

For specifiers a and A , only a single value is used. The repeat count specifies the size of the output string, padded with nulls if a , or space if A was given. The type specifiers x , X , and @ do not use up any values. The repeat count for x and X specify how much of the output string should be expanded or contracted. @ is similar to x but the repeat count specifies an absolute instead of relative position.

Since Arbortext Editor does not support floating point as a basic type, the values corresponding to the f and d type specifiers must be written as strings. For example:

```
pack("df", "1.5e-4", "72.27")
```

The binary representation of real numbers is the native machine format which is not portable.

If an argument specifies an array name, then all the elements of the array from 1 to high_bound( array name ) are used if the template specifies enough fields. For example,

```
split("1 2 3 4 5", array)
split("1 2 3 4 5", array)
n5 = pack("i*", arry)
```

generates a structure of 5 integers. Currently, there is a limit of 250 field values.

The following three examples generate a string of four characters (and are equivalent):

```
pack("cccc", 97, 98, 99, 100)
pack("c4", 97, 98, 99, 100)
pack("a4", "abcdefg")
```

Note that in the latter case, only the first four characters of the value are used.

The example that follows involves writing a port number in network order to a network channel (possibly connected to a non-Intel based machine):

```
write(ch, pack("n",portno))
```

If the other end was a Arbortext Editor client, unpack would be used to convert the port number. For example:

```
read(ch, buf, 2)
portno = unpack("n", buf)
```

pack may also be used to preallocate a string to a particular size, for example,

```
str = pack("x1000");str = ''
```

creates a string of 1000 bytes and gives it a null initial value. This is useful in cases where a large string is created by appending many small strings using the concatenation assignment operator .= in a loop. Preallocating the string to a size close to the final size reduces the number of times Arbortext Editor has to reallocate the string as characters are appended. This also reduces the execution time needed for the loop.

To pack a Unicode character, use s or n . For example,

```
pack("s2", ord("a"), chr(0x2665))
```

The a and A designators convert a Unicode string into a possibly multi-byte string in the system character set. Note, if a field length is specified, for example, a7 , this could result in a partial character being stored if the system character set is a multi-byte character set.

If you are converting a Unicode string parameter to an 8-bit string for passing to a dynamic library, it is best to pass the string as a parameter to the dl_call function and let dl_call to the conversion for you. One case in which it is necessary to use pack is if the parameter is an output parameter and one needs to allocate enough space to hold the return value. Then the ACL code will need to use pack with something like "a2000" to allocate a big enough string to hold the result. Note that this assumes that the DLL is an 8-bit DLL and conversion is necessary.

## Related Topics

- • unpack built-in function



---

# package_(Function)

# package (Function)

package ( package )

This function changes the current package to the name given by package which must specify a package previously defined by the package command. The function returns the name of the package previously in effect on success. It returns a null string if package does not exist.

Unlike the package command, the package name is not evaluated until the package function is executed.

## Related Topics

- • Packages

- • package command

- • eval function



---

# package_file

# package_file

package_file ([ package ])



This function returns the path name associated with package package, or the current package if no argument is specified. Note that if more than one command file uses package , the first file loaded that defines the package with the package command is considered the package file.



---

# package_name

# package_name

package_name ([ level ])



This function returns the name of the current package. If the argument level is given, it specifies the number of call frames to go back before the current one to obtain the package name For example, package_name returns the name of the package active at the time of the call to function containing the call to package_name .

## Related Topics

- • caller function

- • caller_file function

- • caller_line function



---

# packages

# packages

packages ( arr )

This function fills the associative array arr with a list of all loaded packages. It returns the number of loaded packages. The package name is used as the key and the associated file name is the value of each array element.



---

# panel_popup

# panel_popup

panel_popup ( name )



This function displays the predefined dialog box named name and is one of the following strings:

- • bookmarks — the Bookmarks dialog box (from Insert > Insert Bookmark )

- • hyperlink — the Create Hyperlink dialog box (from Tools > Create Hyperlink ; this command is available only if the set hyperlinkmenus command is set to on .

- • macros — the Macros dialog box (from Tools > Macro > Macros )

- • record — the Record Macro dialog box (from Tools > Macro > Record New Macro )

- • symbols — the Windows Insert Symbol dialog box (from Insert > Symbol )

- • tagtemplates — the Tag Templates dialog box ( Tools > Tag Templates )



---

# paragraph_tag_name

# paragraph_tag_name

paragraph_tag_name ( doc )

This function returns the name of the primary paragraph tag specified in the .dcf file for the document type associated with doc . This tag is inserted when users select the paragraph button on the Application toolbar .

The function returns the null string if there isn't a paragraph tag designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

## Related Topics

- • set toolbar4 command



---

# path_doc

# path_doc

path_doc ( path )

This function searches the list of open documents for the path name given by path , which may be the name of a document directory or a plain file, and returns the corresponding document identifier if found, or -1 if not. If path does not specify an absolute path name, the current directory is prepended.

Examples

This function can be written using other built-ins as follows:

```
function path_doc(name) {
local i, n, L[], path
path = absolute_file_name(name);
if (file_directory(path)) {
path .= "/" . basename(name) . ".sgm"
}
n = doc_list(L)
for (i = 1; i <= n; i++) {
if (path == doc_path(L[i])) {
return L[i];
}
}
return -1;
}
```



---

# path_public_ids

# path_public_ids

path_public_ids ( path , arr [, first_only [, catpath ]])



This function returns an array of public ids mapped to the specified path PUBLIC and DTDDECL catalog entries. The function returns the number of elements in the array. If first_only is non-zero, then only the first match (if found) is returned. Otherwise, all public ids mapped to the path are returned (the default). If catpath is not specified, then the value of the option catalogpath is used for the list of catalog files to search. Otherwise, catpath specifies an alternate path list to search.



---

# paths_equal

# paths_equal

paths_equal ( path1 , path2 )

Determines if the two given paths actually represent the same file or directory. This will allow “subst” and “network mapped” drives to obtain the final target path for purposes of comparison.

Returns non-zero if the paths represent the same file or directory. Otherwise, paths_equal returns 0 .



---

# perlscript

# perlscript

perlscript ( expr [, window ])

This function sends the string expr to the Microsoft Windows PerlScript interpreter to be evaluated, returning the result as a string. If the window parameter is not specified, the PerlScript expression is evaluated in the global PerlScript script context so previously defined PerlScript functions are accessible.

The optional window parameter is the identifier of a XUI dialog box that has a script context. If window is provided, the script executes in that dialog box’s script context.

This function requires that a PerlScript interpreter be installed.

Example:

```
name = perlscript('$Application->prompt("Name", "")')
```

## Related Topics

- • javascript function

- • jscript function

- • vbscript function



---

# preference

# preference

preference ( string [, factory ])

This function returns the preference scope value of the set option specified by string , which may be an initial substring. This value is the value of the set option when Arbortext Editor is first started, which is also the .associated setting in the Preferences dialog box.

Set the optional boolean factory parameter to true to return the default value for the set option specified by string . The result is a string which may be passed to the set command.

Examples

```
$tgfntclr = preference("tagfontcolor");
if (preference("pagebreaktext",1) == "off") { ...}
```

## Related Topics

- • option_scope function

- • set command



---

# procins_tag

# procins_tag

procins_tag ( name [, doc ])

This function returns 1 (True) if the name specified by name is an SGML processing instruction. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# profile_alias

# profile_alias

profile_alias ( attr [, doc ])

Returns the alias name for the specified profile attribute.

- • attr — The attribute for which the alias name is returned. If no such alias exists, null is returned.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_aliases

# profile_aliases

profile_aliases ( arr [, doc ])

Returns the number of profile aliases defined in the current (or other) profiling configuration file.

- • arr — An array of the profile aliases defined in the configuration file associated with the profiling session. profile_aliases returns the count of the array arr .

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_allowed

# profile_allowed

profile_allowed ( alias , oid )

Returns 1 if the specified element can be profiled using the specified profile. Returns 0 if the element cannot be profiled, or if either oid or alias is invalid.

- • alias — The profile to apply.

- • oid — The element to be profiled.



---

# profile_attr

# profile_attr

profile_attr ( alias [, doc ])

Returns the name of the profile attribute for the specified profile.

- • alias — The alias for which the name of the profile attribute is returned. If no such attribute exists, null is returned.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_attrs

# profile_attrs

profile_attrs ( arr [, doc ])

Returns the number of profile attributes defined in the configuration file associated with the profiling session.

- • arr — An array of the profile attributes defined in the configuration file associated with the profiling session. profile_attrs returns the count of the array arr .

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_class_values

# profile_class_values

profile_class_values ( arr , profile [, doc ])

This function fills the array arr with a list of allowed values that are defined for the given profile attribute in the document type configuration file ( .dcf ) for the document type associated with doc .

The function returns the allowed values in the order in which they are declared in the .dcf file. This function also returns the number of entries in the array. The first entry is stored at index 1.



---

# profile_classes

# profile_classes

profile_classes ( attributeArr , aliasArr [, doc ])

This function fills the arrays attributeArr and aliasArr with a list of the profile attributes and their aliases declared in the document type configuration file ( .dcf ) for the document type associated with doc . If doc is omitted or 0 , the current document is used.

This function returns the array values in alphabetical order. It also returns the number of entries in each array. The first entry is stored at index 1.



---

# profile_config

# profile_config

profile_config ([ doc ])

Returns a document identifier for the current (in-memory) profiling configuration file.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used. If doc is invalid or no configuration file is defined for profiling, profile_config returns -1 .



---

# profile_conflictshadingbackground

# profile_conflictshadingbackground

profile_conflictshadingbackground ([ doc ])

Returns the conflict color set for the profile for a particular document.

- • doc — Optional. The target document . If doc is not supplied, the current document is used.

The function returns a color name or a color number in the form #rrggbb . If no color is defined for the profile, an empty string is returned.



---

# profile_default_value

# profile_default_value

profile_default_value ( alias [, doc ])

Returns the default value for the specified RADIO_PROFILE type node.

- • alias — The alias of the RADIO_PROFILE type node for which the default value is returned. If alias is not a RADIO_PROFILE type node or if the default value has not been set, profile_default_value returns an empty string .

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used. If doc is invalid or no configuration file is defined for profiling, profile_config returns -1 .



---

# profile_default_value_node

# profile_default_value_node

profile_default_value_node ( alias [, doc ])

Returns the default value profilenode for the specified RADIO_PROFILE type node.

- • alias — The alias of the RADIO_PROFILE node for which the default value is profilenode returned. If alias is not a RADIO_PROFILE type node or if the default value has not been set, profile_default_value returns profilenode_null .

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used. If doc is invalid or no configuration file is defined for profiling, profile_config returns -1 .



---

# profile_element_allowed

# profile_element_allowed

profile_element_allowed ( alias , tagname [, doc ])

Returns 1 if the specified element can be profiled using the specified profile. Returns 0 if the element cannot be profiled, or if the specified element or profile is invalid.

- • alias — The alias of the profile to be applied.

- • tagname — The element to be profiled.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_element_attr_tests

# profile_element_attr_tests

profile_element_attr_tests ( alias , tagname , arr [, doc ])

Returns the number of attribute name(s) and value(s) for the specified element that the specified profile can be applied to (if the not_indicator of profile_elements_list is 0 ) or not applied to (if not_indicator is 1 ).

- • alias — The alias of the profile to be applied (or not applied).

- • tagname — The element to be profiled (or not profiled).

- • arr — An array of the attribute name(s) and value(s) for tagname that alias could be applied to or not applied to. profile_element_attr_tests returns the count of the array arr .

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_elements_list

# profile_elements_list

profile_elements_list ( alias , arr , not_indicator [, doc ])

Returns the number of elements the specified profile could be applied to or not applied to.

- • alias — The alias of the profile to be applied (or not applied).

- • arr — An array of elements to which alias can (or cannot) be applied. profile_elements_list returns the count of the array arr .

- • not_indicator — When set to 0 , specifies that alias can be applied to the elements listed in arr . When set to 1 , specifies that alias cannot be applied to the elements listed in arr .

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_is_foldered

# profile_is_foldered

profile_is_foldered ( alias [, doc ])

Returns 1 if the specified profile class is a FOLDERED_PROFILE class. Otherwise, profile_is_foldered returns 0 .

- • alias — The profile class to be evaluated.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_is_radiochoice

# profile_is_radiochoice

profile_is_radiochoice ( alias [, doc ])

Returns 1 if the specified profile class is a RADIO_PROFILE class. Otherwise, profile_is_radiochoice returns 0 .

- • alias — The profile class to be evaluated.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_is_standard

# profile_is_standard

profile_is_standard ( alias [, doc ])

Returns 1 if the specified profile class is a STANDARD_PROFILE class. Otherwise, profile_is_standard returns 0 .

- • alias — The profile class to be evaluated.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_resolution

# profile_resolution

profile_resolution ( oid , logical_expression )

Returns 1 if the specified element would be included if the profile was resolved using the specified logical expression. Otherwise, profile_resolution returns 0 .

- • oid — The element to be evaluated.

- • logical_expression — XML markup used for resolving the profile. The markup conforms to the structure of the <LogicalExpression> element in the profile configuration file.



---

# profile_rootnode

# profile_rootnode

profile_rootnode ( alias [, doc ])

Returns the profilenode of type STANDARD_PROFILE , RADIO_PROFILE , or FOLDERED_PROFILE of a profile class.

- • alias — The profile class for which the profilenode is returned.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_rootnodes

# profile_rootnodes

profile_rootnodes ( arr [, doc ])

Returns the number of profilenodes of type STANDARD_PROFILE , RADIO_PROFILE , or FOLDERED_PROFILE defined in the current (or other) profile configuration file.

- • arr — An array of profilenodes identifiers of type STANDARD_PROFILE , RADIO_PROFILE , or FOLDERED_PROFILE for each profile defined in the profile configuration file. profile_rootnodes returns the count of the array arr .

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_shadingbackground

# profile_shadingbackground

profile_shadingbackground ( alias [, doc ])

Returns the shading color set for a profile attribute in a particular document.

- • alias — The alias of the profile attribute

- • doc — Optional. The target document . If doc is not supplied, the current document is used.

The function returns a color name or a color number in the form #rrggbb . If no color is defined for the alias, an empty string is returned.



---

# profile_type

# profile_type

profile_type ( alias [, doc ])

Returns an integer identifying the profile type of the specified alias.

- • alias — The profilenode for which the type is returned. profile_type returns the following values:

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_valid

# profile_valid

profile_valid ( alias [, doc ])

Returns 1 if the specified alias is a valid profile. Otherwise, profile_valid returns 0 .

- • alias — The profile to be evaluated.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_value_node

# profile_value_node

profile_value_node ( alias , value [, doc ])

Returns the allowed value profilenode for the specified value in the profile class identified by the specified alias.

- • alias — The profile class containing value .

- • value — The value for which the profilenode is returned.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_value_nodes

# profile_value_nodes

profile_value_nodes ( alias , arr [, doc ])

Returns the number of allowed value profilenodes for the profile class identified by the specified alias.

- • alias — The profile class to be evaluated.

- • arr — An array of allowed value profilenodes for the profile class alias . The array is populated in the order in which the values are specified in the associated profiling configuration file. profile_value_nodes returns the count of the array arr .

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_value_separator

# profile_value_separator

profile_value_separator ( alias [, doc ])

Returns the value separator for the specified profile.

- • alias — The profile for which the value separator is returned. The value separator is specified on the <Profile> element in the profile configuration file. the separator separates multiple values from each other. The default value is a semicolon.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_values

# profile_values

profile_values ( alias , arr [, doc ])

Returns the number of allowed values for the profile class identified by the specified alias.

- • alias — The profile class to be evaluated.

- • arr — An array of the allowed values for alias . The array is populated in the order in which the values are specified in the profiling session configuration file. profile_values returns the count of the array arr .

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# profile_values_shadingbackground

# profile_values_shadingbackground

profile_values_shadingbackground ( alias , arr[] [, doc [, includeProfileElement ]])

This function populates the array array[] with the colors for the profile attribute for alias for document doc .

If doc is not supplied, the current document is used. If includeProfileElement is supplied and has a non-zero value, the profile shading color for the Profile element is also included as the last element in the array.

The function returns the color names or color numbers in the form #rrggbb . If no color is defined for the profile value, an empty string will be in that array position. The array is filled in the same order as the function call profile_values() .



---

# profilenode_ancestors

# profilenode_ancestors

profilenode_ancestors ( profilenode , arr )

Returns the number of folders that are ancestors of the node identified by the specified node.

- • profilenode — The node for which the number of ancestors is determined.

- • arr — An array of the profilenode identifiers of the folders that are ancestors of the node identified by profilenode . The list of values includes the profilenode of type STANDARD_PROFILE , RADIO_PROFILE , or FOLDERED_PROFILE for that particular profile branch. The array is populated in the order in which the ancestors are listed in the profile configuration file, starting with the STANDARD_PROFILE , RADIO_PROFILE , or FOLDERED_PROFILE profilenode. profilenode_ancestors returns the count of the array arr .



---

# profilenode_attr

# profilenode_attr

profilenode_attr ( profilenode )

Returns the name of the profile attribute for a profilenode.

- • profilenode — The node for which the profiling attribute is returned.

profilenode_attr returns the name of the profile attribute for the node specified by profilenode . profilenode_attr returns the null string if no such attribute exists.



---

# profilenode_children_nodes

# profilenode_children_nodes

profilenode_children_nodes ( profilenode , arr )

Returns the number of nodes that are children of a node.

- • profilenode — The node for which the number of child nodes is returned.

- • arr — An array of the profilenode identifiers of the nodes that are children of profilenode . profilenode_children_nodes returns the count of the array arr .



---

# profilenode_default_value

# profilenode_default_value

profilenode_default_value ( profilenode )

Returns the default value for a RADIO_PROFILE node as specified in the profile configuration file.

- • profilenode — The node for which the default value is returned.

profilenode_default_value returns an empty string if profilenode does not pertain to a RADIO_PROFILE node, or if the default value has not been set in the configuration file.



---

# profilenode_default_value_node

# profilenode_default_value_node

profilenode_default_value_node ( profilenode )

Returns the default value profilenode for a RADIO_PROFILE node as specified in the profile configuration file.

- • profilenode — The node for which the default value profilenode is returned.

profilenode_default_value returns an empty string if profilenode does not pertain to a RADIO_PROFILE node, or if the default value has not been set in the configuration file.



---

# profilenode_element_allowed

# profilenode_element_allowed

profilenode_element_allowed ( profilenode , tagname )

Determines if an element can be profiled using a given profilenode. Returns 0 if the element cannot be profiled, or if either the element or profilenode is invalid.

- • profilenode — The node defining the profiling to be applied.

- • tagname — The element to be profiled.

profilenode_element_allowed returns 1 if tagname can be profiled using profilenode or if either tagname or profilenode is invalid.



---

# profilenode_element_attr_tests

# profilenode_element_attr_tests

profilenode_element_attr_tests ( profilenode , tagname , arr )

Returns the number of attribute name(s) and value(s) for an element that a particular profile could be applied to or not applied to.

- • profilenode — The node defining the profiling.

- • tagname — The element to be profiled as defined in the <ProfileElement> or <NotProfileElement> elements in the profile configuration file.

- • arr — An array of the attribute name(s) and value(s) for tagname that the profile represented by profilenode could be applied to or not applied to. Attribute names and values are specified on the <AttributeTest> element in the <ProfileElement> or <NotProfileElement> elements in the profile configuration file.

profilenode_element_attr_tests returns the count of the array arr .



---

# profilenode_elements_list

# profilenode_elements_list

profilenode_elements_list ( profilenode , arr , not_indicator )

Returns the number of elements that a particular profile could be applied to or not applied to.

- • profilenode — The node defining the profiling.

- • arr — An array of the elements at the profile identified by profilenode could (or couldn't) be applied to, as specified in the <ProfileElement> or <NotProfileElement> elements in the profile configuration file.

- • not_indicator — If 0 the profile can only be applied to the list of element names. If 1 the profile can be applied to any element NOT in the list of element names.

profilenode_elements_list returns the count of the array arr .



---

# profilenode_is_foldered

# profilenode_is_foldered

profilenode_is_foldered ( profilenode )

Determines if the root node of a node is a FOLDERED_PROFILE node.

- • profilenode — The node for which the type of root node is determined.

profilenode_is_foldered returns 1 if the root node of profilenode is a FOLDERED_PROFILE node. Otherwise, profilenode_is_foldered returns 0



---

# profilenode_is_radiochoice

# profilenode_is_radiochoice

profilenode_is_radiochoice ( profilenode )

Determines if the root node of a node is a RADIO_PROFILE node.

- • profilenode — The node for which the type of root node is determined.

profilenode_is_radiochoice returns 1 if the root node of profilenode is a RADIO_PROFILE node. Otherwise, profilenode_is_radiochoice returns 0



---

# profilenode_is_standard

# profilenode_is_standard

profilenode_is_standard ( profilenode )

Determines if the root node of a node is a STANDARD_PROFILE node.

- • profilenode — The node for which the type of root node is determined.

profilenode_is_standard returns 1 if the root node of profilenode is a STANDARD_PROFILE node. Otherwise, profilenode_is_standard returns 0



---

# profilenode_name

# profilenode_name

profilenode_name ( profilenode )

Returns the profile alias, folder name, or profile value of profilenode as follows:

- • Returns the profile alias if profilenode is a STANDARD_PROFILE , RADIO_PROFILE , or FOLDERED_PROFILE node.

- • Returns the folder name if profilenode is a PROFILE_FOLDER node.

- • Returns the profile value if profilenode is an ALLOWED_VALUE node.

An empty string if profilenode is invalid.



---

# profilenode_parent

# profilenode_parent

profilenode_parent ( profilenode )

Returns the profilenode of the immediate ancestor of a profilenode.

- • profilenode — The node for which the immediate ancestor is returned.

profilenode_null is returned if profilenode has no parent or is invalid.



---

# profilenode_rootnode

# profilenode_rootnode

profilenode_rootnode ( profilenode )

Returns the top-level or root node of a profile class.

- • profilenode — The node having the profile class for which the top-level node is returned.

profilenode_rootnode returns a profilenode of type STANDARD_PROFILE , RADIO_PROFILE , or FOLDERED_PROFILE for the profile class identified by profilenode . profilenode_null is returned if no top-level node exists.



---

# profilenode_shadingbackground

# profilenode_shadingbackground

profilenode_shadingbackground ( profilenode )

Returns the color for the profile node profilenode .

The function returns the color name or color number, in the form #rrggbb , of the node or of an ancestor of the node if the color is not found on that node. If no color is defined for profilenode , or if the parameter is invalid, an empty string will be returned.



---

# profilenode_type

# profilenode_type

profilenode_type ( profilenode )

Returns a value based on the profilenode TYPE as follows:

- • 0 — Returned if TYPE is an INVALID_PROFILE node.

- • 1 — Returned if TYPE is an STANDARD_PROFILE node.

- • 2 — Returned if TYPE is an RADIO_PROFILE node.

- • 3 — Returned if TYPE is an FOLDERED_PROFILE node.

- • 4 — Returned if TYPE is an PROFILE_FOLDER node.

- • 5 — Returned if TYPE is an ALLOWED_VALUE node.



---

# profilenode_valid

# profilenode_valid

profilenode_valid ( profilenode )

Returns 1 if profilenode is a valid profilenode identifier. Otherwise, profilenode_valid returns 0 .



---

# profilenode_value_nodes

# profilenode_value_nodes

profilenode_value_nodes ( profilenode , arr )

Returns the number of value profilenodes for a node.

- • profilenode — The node for which the number of value profilenodes is returned.

- • arr — An array of the allowed values profilenodes for profilenode . The array is populated in the order in which the values are specified in the profile configuration file.

profilenode_value_nodes returns the number of profilenodes stored in the array arr .



---

# profilenode_value_separator

# profilenode_value_separator

profilenode_value_separator ( profilenode )

Returns the value separator corresponding to the specified node.

- • profilenode — The node for which the value separator is returned.

The value separator is specified on the <Profile> element in the profile configuration file. It is used to separate multiple values from each other. The default value for it is semicolon.



---

# profilenode_values

# profilenode_values

profilenode_values ( profilenode , arr )

Returns the number of allowed values for the specified node.

- • profilenode — The node for which the number of allowed values is returned.

- • arr — An array of the allowed values for profilenode . The array is populated in the order in which the values are specified in the profile configuration file.

profilenode_values returns the number of values stored in the array arr .



---

# progressbar_available

# progressbar_available

progressbar_available ()

Returns 1 if the progress bar dialog is currently available. If the function returns 0 , all other progressbar_* functions ( progressbar_visible() , progressbar_start_job() , progressbar_update() , progressbar_cancelled() , progressbar_close() ) will fail silently.

The progress bar dialog will not be available if the environment is running in Publishing Engine or on a non-Windows platform.



---

# progressbar_cancelled

# progressbar_cancelled

progressbar_cancelled ()

Returns 1 if the Cancel button on the progress bar dialog box has been activated. Returns 0 if not, or if there is no current progress bar dialog box.



---

# progressbar_close

# progressbar_close

progressbar_close ()

Closes the progress bar dialog box. This function is the only way to dismiss the progress bar dialog box. It cannot be closed by the user. For this reason, it is important that scripts that use progressbar_start_job() also call this function before exiting.



---

# progressbar_start_job

# progressbar_start_job

progressbar_start_job ( jobLabel , taskLabel [, nTasks=0 [, allowCancel=1 [, delay=0 ]]])

Initializes a new job to be reported in the progress bar dialog box. If the progress bar dialog boxis already being shown, the new job replaces any existing job. If the dialog box is not currently visible this function raises it, after a delay if delay has a non-zero value.

- • jobLabel — a short description of the overall job. This will be shown in bold text above the progress bar in the dialog box.

- • taskLabel — a short description of the initial task. This will be shown in regular text below the progress bar in the dialog box.

- • nTasks — the total number of steps required by the job. If set to 0 (the default) or a negative value, the progress bar will be shown in indeterminate, or waiting, mode.

- • allowCancel — whether to enable the Cancel button on the dialog box. The default is 1 (enable).

- • delay — the number of seconds to wait before showing the progress bar dialog box.

It is important that scripts that use this function also call progressbar_close() before exiting, since the progress bar dialog box cannot be dismissed by the user..



---

# progressbar_update

# progressbar_update

progressbar_update ( curTask [, taskLabel="" [, nTasks=-1 ]])

Updates the state of the progress bar dialog box.

- • curTask — the current task index. This value should be less than or equal to nSteps , if specified, or less than or equal to the nSteps value passed to the most recent call to progressbar_start_job() .

- • taskLabel — a short description of the current step. If the empty string is specified, the step label field is left unchanged. This is the default. To specify an empty step label, use a single space ( " " ).

- • nTasks — the number of known steps in the current job. The known number of steps may change during the course of a job — using this parameter allows programs to update the number of steps as the job progresses. A negative value leaves the number of steps reflected by the progress bar unchanged. A value of 0 puts the progress bar into indeterminate, or waiting, mode.



---

# progressbar_visible

# progressbar_visible

progressbar_visible ()

Returns 1 if the progress bar dialog is currently visible, 0 otherwise.



---

# public_id

# public_id

public_id ([ doc ])

This function returns the SGML public identifier for the document being edited, but it returns the null string for an ASCII file. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# public_id_path

# public_id_path

public_id_path ( pubid [, unused [, catalogpath ]])

This function returns the system path name for the SGML public identifier string pubid . If the identifier is not found in any of the catalog files in the search path given by the set catalogpath option, the public_id_path function returns a null string.

The second argument, unused , is no longer used. It should be the null string.

The catalogpath argument specifies a list of directories to search for the catalog file. If it is not specified, the path list specified in the set catalogpath option, which is initialized from the environment variable APTCATPATH , is searched.



---

# put

# put

put ( fid , str )



This function writes the characters given by str to the file identified by fid , which must be a return value from a previous call to open . The file associated with fid must have been opened for writing.

- • put does not add any newline characters after str . If linefeeds are desired, they must be given as part of the string. The output to the stream is buffered; flush can be used to force characters to be written.

- • put returns the number of characters written or -1 on failure (such as an attempt to write to a file identifier opened exclusively for reading).



---

# pwd

# pwd

pwd ([ startup ])

This function returns the current working directory.

The flag argument startup is optional. If non-zero, the function returns the working directory at the time Arbortext Editor was started. If it is omitted or zero, pwd returns the current working directory.



---

# qsort

# qsort

qsort ( arr [, flags ])

The qsort function sorts the array arr in place according to the options specified by flags . It returns 1 on success, or 0 if the array is not a regular array (that is, an associative array).

flags is a bitmask that specifies sort options and is constructed by ORing the flags from the following list:

- • 0x1 — ignore the case of the characters.

- • 0x2 — reserved for future use.

- • 0x4 — reverse the sense of the comparisons so the greatest value becomes the first array element.

- • 0x8 — sort in numerical order. Bit 1 is ignored if this bit is set.

If flags is 0 or omitted, the sort is according to the collating sequence of the current locale.



---

# quote

# quote

quote ( string [, flags ])

This function returns a copy of the string represented by string with embedded backslash ( \ ), quote ( " ), and dollar sign ( $ ) characters escaped with \ to form a valid ACL string operand. Each literal new line character in the string is replaced with the sequence \n . The resulting string is delimited with double quotes. For example, quote('String with \ and $ embedded') would return "String with \\ and \$ embedded" .

If the flags parameter is 0x01 then dollar signs are not escaped, allowing variable substitution to be performed on the resulting string.

## Related Topics

- • Operands

- • join function

- • varsub function



---

# read_(Function)

# read (Function)

read ( fid , buf , len [, re ])

This function reads up to len characters from the file or channel identified by fid into the scalar variable buf . This function returns the number of characters read, or 0 at the end of the file if the channel was closed. It returns -1 if an error occurred. fid is a file identifier returned by open for reading or a network channel identifier returned by open_connect or open_accept .

If re is specified, it specifies a single character that marks the end of the record. In this case, read copies characters into buf until the re character is found and transferred into buf , or len bytes are read. If re is null character (\000) or omitted, then the data stream is not searched for a record end character.

When reading from a channel in non-blocking mode (from a callback established by channel_set_callback ), the read may return fewer than len bytes. The return value is the actual number of bytes read. If the read would block, that is, there is no data pending on the channel, read returns -2 . read also returns -2 if re is given, but the data pending on the channel does not contain the record end character. In this case, Arbortext Editor queues the data internally until a complete record is available to return to a subsequent read from the channel callback read notification.

Unlike getline , read can handle binary data, that is, null characters. The following example is a function that can be used to make an exact copy of a file that may contain binary data. Note, that the “b” flag must be specified when opening both files.

```
function file_copy(from, to) {
local inf, outf
inf = open(from, "rb")
if (inf < 0) {
response("Couldn't open file for read:" . from)
return 0
}
outf = open(to, "wb")
if (outf < 0) {
close(inf)
response("Couldn't open file for write:" . to)
return 0
}
local buf, n=0, len
while ((len = read(inf, buf, 512)) > 0) {
n += write(outf, buf, len)
}
close(outf)
close(inf)
return n;
}
```

## Related Topics

- • channel_set_callback built-in function

- • getline built-in function



---

# read_preferences

# read_preferences

read_preferences ( path [, doc ])

This function reads the preferences stored in the preferences file specified by path , and uses them to update the current local scope (window, document, and view) values, updating the current window display. Note that the path to the preferences file cannot contain just single backslashes ("\"). The path must contain single forward slashes ("/"), double backslashes ("\\"), or single backslashes with the entire path enclosed in single quotes.

If the function executes successfully, it returns a one ( 1 ). If the path is invalid, the function returns a zero ( 0 ).

Example:

```
read_preferences("C:/temp/arbortext.wcf")
read_preferences("C:\\temp\\arbortext.wcf")
```

## Related Topics

- • Set option scope

- • option_scope function

- • set command



---

# registerApplicabilitySyntax

# registerApplicabilitySyntax

registerApplicabilitySyntax ( name , test_xpath , expr_path , parser_class , parser_namespace [, "parser_and_operator" [, "parser_or_operator" [, "parser_not_operator" ]]])

Registers a custom syntax for applicability.

- • name — the name of the syntax

- • test_xpath — an XPath expression that, when evaluated on an element, will advise if there is applicability for that element

- • expr_path — an XPath expression that retrieves the applicability expression for a particular element

- • parser_class — the classname of the parser for the syntax

- • parser_namespace — the namespace used for the syntax

- • parser_and_operator (optional)— the And operator used for syntax expressions in applicability attributes (default "&&")

- • parser_or_operator (optional)— the Or operator used for syntax expressions in applicability attributes (default "||")

- • parser_not_operator (optional) — the Not operator used for syntax expressions in applicability attributes (default "!!")

For example, this syntax is registered for ATO, the default applicability type shipped with Arbortext Editor :

```
applic::registerApplicabilitySyntax("ATO", "boolean(@*[namespace-uri() = 'http://arbortext.ptc.com/namespace/ATO' and local-name() = 'applic'])", "@*[namespace-uri() = 'http://arbortext.ptc.com/namespace/ATO' and local-name() = 'applic']" , "com.ptc.arbortext.applicability.representation.ATOParser", "appl")
```

Arbortext Editor ships with two applicability syntaxes: APEX and ATO.

Once registered, a custom syntax must be assigned to the current environment using inlineapplicabilitysyntax (as set command or advanced preference) before it can be referenced.

## Related Topics

- • set inlineapplicabilitysyntax

- • Working with Applicability



---

# remove_hook

# remove_hook

remove_hook ( hookname , funcname )

This function removes a callback function from the list of functions for the specified hook, where hookname is the name of the hook set option. The argument funcname is a string specifying the name of the user-defined function to call.

Refer to Hook functions introduction for a detailed introduction to ACL hooks.

## Related Topics

- • add_hook function



---

# rename_ms_parameter

# rename_ms_parameter

rename_ms_parameter ( entity )

This function allows you to rename a marked section parameter entity.

entity is the name of an existing marked section parameter entity.



---

# replace

# replace



This function searches for searchStr and replaces it with replaceStr . Returns 0 on failure. For success, if replace all is specified, then the number of replacements, else 1 .

- • searchStr — The string to search for.

- • replaceStr — The string to replace searchStr .

- • flags — The bit mask for modifying the search.

- • element — Search only the contents of elements with this name

- • doc — Current doc instance if not specified.



---

# require_(Function)

# require (Function)

require ( package [, filename ])

This function loads the package specified by package from the file filename if not already loaded. If filename is not specified, the list of directories specified in the set loadpath command option is searched for a file named package .acl , where .acl is the Arbortext Command Language file name suffix. Returns 1 (True) if the package was loaded or 0 (False) if the package file could not be opened or if the specified package is not defined after the file is read.

## Related Topics

- • Packages

- • require command

- • set loadpath command

- • source command

- • Opening, referencing, and saving files



---

# response

# response

response ( s1 [, s2 ,...])

This function displays the message specified by s1 in a panel with push buttons labeled by the following strings ( s2 , s3 , and so on). This function returns the ordinal number of the button pressed by the user. If the dialog box is dismissed without a button press (by a window manager function, for example), this function returns 0 . However, if button two or three is Cancel , the function returns the ordinal number of the Cancel button. The prompt message may contain newline characters. If no button arguments are given, then an OK button is supplied. In this case, the response function displays the message and does not execute the next command until the user presses the OK button.

If the response function panel has just one push button, or if any button is labeled OK or Yes , the ENTER key works as an accelerator to activate the selection and dismiss the panel. The ESCAPE key is an accelerator for the cancel action if the response function panel has a button labeled Cancel or No .

To establish a mnemonic (hot key) for a particular dialog box item, precede the mnemonic letter with the '&' character in the associated string. Use “&&” anyplace you want a single '&' to show.

Example

```
response("Choose direction", "&Forward", "&Backward", "&Stop"
```

## Related Topics

- • list_response function

- • readvar command

- • Predefined variables



---

# reverse

# reverse

reverse ( s )



This function returns a copy of string s with the characters in reverse order. For example, reverse("abcd") returns "dcba".



---

# rindex

# rindex

rindex ( s1 , s2 )



This function returns the position in the string s1 of the last (rightmost) occurrence of string s2 , based at 1 . If the substring is not found, 0 is returned. If s2 is the null string, this function returns length( s1 ) .



---

# save_as_html_file

# save_as_html_file

save_as_html_file ([ pathname [, overwrite [, doc ]]])

This function converts the specified document to an HTML file and saves it using the name specified by pathname . The presentation of the HTML file is based on the characteristics of the current Arbortext Editor stylesheet with tags off.

- • pathname — Optional. Specifies full path for the resulting HTML file. If not supplied, the user will be prompted for the full path.

- • overwrite — Optional. Specifies whether to automatically replace an existing file specified by pathname . If set to 0 , the user will be prompted to verify overwriting the file. If set to 1 , the file will be silently overwritten. The default value is 0 .

- • doc — Specifies the document identifier of the document to be saved as HTML. The doc argument must be a return value from a previous call to doc_open , window_doc , or oid_doc . If doc is omitted or 0 , the current document is used.

For example,

```
$d=doc_open("c:/temp/artdoc.sgm");
save_as_html_file("c:/temp/artdoc.htm", 1, $d);
```

## Related Topics

- • Saving a document as an HTML file



---

# save_as_windchill_template_source

# save_as_windchill_template_source

save_as_windchill_template_source ( )

This function is only available when you are connected to a PTC server through the PTC Server connection in Arbortext Editor . The function enables you to save the currently open DITA topic document to the PTC server where it will be used as the source for a Dynamic Document template. Note that the function should only be used for a DITA topic template document opened from the New Document dialog box. The intention is to retain the feature that automatically sets the topic ID for the DITA template document stored on the PTC server.

Entering save_as_windchill_template_source() at the Arbortext Editor command line opens the Save As Properties dialog box. Use the dialog box to save the template to the desired location on the PTC server.

## Related Topics

- • Saving a DITA document to be used as a PTC server template

- • Save As Properties Dialog Box



---

# save_some_docs

# save_some_docs

save_some_docs ([ noprompt ])

This function loops through the list of modified documents and prompts the user whether to save each one. If noprompt is true (non-zero), it saves all changes without prompting. The exit_editor function calls this function if its second argument is not 2.

The function returns 1 on success, 0 if there was an error saving a document, or -1 if the user selected Cancel on a prompt to save a document.

## Related Topics

- • exit_editor function



---

# schema_validate

# schema_validate

schema_validate ([ doc ])

Validates a document against a schema the user selects from a dialog box. The dialog box offers schemas specific to the namespaces used in the document and, at most, one non-namespaced schema.

- • doc — The document to validate against the schema. If not specified, the current document is used.

The function returns one of the following values:

- • 0 — The validation against one or more schemas failed.

- • 1 — doc is valid.

- • -1 — The user canceled the validation.

Error results are displayed in the Completeness Check Log window and linked to the area of the document causing each error. If no errors are encountered, a message is sent to the status bar. Refer to ns_schema_validate_batch and schema_validate_batch for similar functionality when developing Arbortext Publishing Engine applications.



---

# schema_validate_batch

# schema_validate_batch

schema_validate_batch ( schema [, doc [, flag ]])

Validates a document against a non-namespaced schema.

- • schema — The path and file name of a non-namespaced schema definition ( XSD ) file.

- • doc — The document to validate against schema . If not specified, the current document is used.

- • flag — Enables you to control how the doc is validated against the schema . The following flags are available:

The function returns one of the following values:

- • 0 — The validation failed.

- • 1 — doc is valid.

All schema_validate_batch results are shown in the event-log document. Refer to schema_validate for similar functionality.

## Related Topics

- • ns_schema_validate_batch



---

# scroll_to_oid

# scroll_to_oid

scroll_to_oid ( oid [, pos [, adjcaret ]])



This function positions the window displaying the document containing oid so that the object given by oid , pos is at column 1 on the top line of the screen. If adjcaret is specified and non-zero, then the cursor position is also moved so that the insertion point is visible.



---

# seek

# seek

seek ( fid , offset [, origin ])



This function sets the position of the next input or output operation on the file identified by fid , which must be a return value from a previous call to open .

The new position is given by offset , which is the signed distance offset bytes from the beginning, the current position, or the end of the file, according to the value of origin which must be 0, 1, or 2. If origin is omitted, 0 is used.

seek returns 0 on success or -1 on failure, for example, if an attempt is made to seek on a file ID associated with a non-seekable device.

seek(fid, 0) rewinds the file associated with fid .



---

# selected

# selected

selected ([ doc [, type ]])

This function returns 1 (True) if there is a selection in the current window. Note that this is faster than testing length($selection) .

- • doc — Specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.

- • type — A qualifier defining a particular type of selection:



---

# selected_element

# selected_element

$oid = selected_element ([ doc [, flags ]])

This function returns the oid for the containing element if the current selection is limited to an entire element. An entire element includes the start and end tags and any content that they encompass. By definition, the oid_select function selects entire elements.

This function returns the value of the oid_null function if there is no selection, or if the selection doesn't encompass an entire element (for example, start tag and content, but not the end tag).

The optional doc parameter specifies the identifier for the document containing the selection. If omitted or 0 , the value for the current_doc function is used.

The flags parameter is an optional bitmask specifying various options, and is constructed by ORing the flags from the following list:

- • 0x1 — Ignore an optional leading and/or trailing blank before considering the selection.

## Related Topics

- • oid_select function

- • selected function

- • selection_start function

- • selection_end function



---

# selection_anchor

# selection_anchor

selection_anchor ( pos [, doc ])

This function returns the oid of the object containing the anchored end of the selection in the window containing the document specified by doc , or the current document if omitted. Also returns the character offset of the end of the selection from oid in the output variable pos .

The anchor point of the selection is the point at which the selection was started, for example, the same as selection_end if the region was highlighted from right to left.

## Related Topics

- • selection_start function

- • selection_end function



---

# selection_balanced

# selection_balanced

selection_balanced ([ doc ])



This function returns 1 (True) if the selection in the current window is balanced, meaning that a tag pair (start and end tag) have been selected.

The doc argument specifies the identifier of the document tree to query. If omitted or 0, the current document is used.



---

# selection_end

# selection_end

selection_end ( pos [, doc ])



This function returns the OID of the object containing the end of the selection in the window containing the document specified by doc , or the current document if omitted. Also returns the character offset of the end of the selection from OID in the output variable pos .

## Related Topics

- • selection_start built-in function



---

# selection_has_change_tracking

# selection_has_change_tracking

ret = selection_has_change_tracking ([ doc ])



This function returns 1 if change records are found in the selected region of doc . If doc is not specified, the value of current_doc is used.



---

# selection_markup

# selection_markup

selection_markup ([ doc [, flags ]])

This function returns a string representing the selected region in the given document (if no selection exists in that document, its value is null). The string includes any XML/SGML codes (markup).

flags — A bitmask that controls the markup included in the returned string and is constructed using OR with the following flags:

- • 0x1 — Include the contents of the selected region. This is the default option if flags is 0 or unspecified.

- • 0x2 — Include the XML or SGML header associated with the selected region. If the region does not include the entire document, this will be a fragment (file entity) header.

- • 0x4 — Ignore the selection and act on the entire document instead.

- • 0x8 — Use XML syntax in the string returned even if the selection is in an SGML document.

- • 0x10 — Use SGML syntax in the string returned even if the selection is in an XML document.

- • 0x20 — Don't convert non-ASCII characters into entity references (as though the set writenonasciichar=char option was in effect). If this bit is not specified, non-ASCII characters are converted according to the current set writenonasciichar setting.

- • 0x40 — Don't include insignificant line breaks. If this bit is not specified, insignificant line breaks will be included based on the set outputrecordlength command setting.

- • 0x80 — Suppress Arbortext processing instructions. Arbortext processing instructions can also be suppressed using the set writepi command.

- • 0x100 — Don't include the markup in the result. This option takes precedence over any other flag bits that control how markup is generated.

Calling selection_markup with no parameters will return the same string as the predefined variable $selection if set sgmlselection=on .



---

# selection_start

# selection_start

selection_start ( pos [, doc ])



This function returns the start of the selection in the window containing the document specified by doc , or the current document if omitted. Also returns the character offset of the start of the selection from OID in the output variable pos .

Examples

The functions selection_start and selection_end can be used to restore a selection, for example:

```
local o1, p1, o2, p2
o1 = selection_start(p1)
o2 = selection_end(p2)
...
goto_oid(o1, p1)
mark begin
goto_oid(o2, p2)
mark end
```

## Related Topics

- • selection_end built-in function



---

# set_custom_property

# set_custom_property

set_custom_property ( key , value )

This function defines a value for the specified key that will be stored in memory. These keys and values can be used by customizations, applications, and repository adapters for configuration purposes.

- • key — String value as defined by the customization, application or adapter.

- • value — Any value, including an empty string.

set_custom_property returns any previous value associated with the specified key. This function will return an empty string if there is either no previous value or the previous value is an empty string.

Use the get_custom_property function to retrieve a parameter and its associated value.



---

# set_profile_group

# set_profile_group

set_profile_group ( set_profile_group_name [, doc ])

Returns the profile configuration file markup for the specified set profile group as a string. If such a string cannot be constructed, an empty string will be returned.

- • set_profile_group_name — The configuration file from which the markup is to be returned.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# set_profile_groups

# set_profile_groups

set_profile_groups ( arr [, doc ])

Returns the number of set profile groups specified in the profile configuration file.

- • arr — Array of the names of the set profile groups specified in the profile configuration file.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# set_profile_groups_expressions

# set_profile_groups_expressions

set_profile_groups_expressions ( arr [, doc ])

Returns the number of set profile groups, and the profile classes and relationships between profile values for the corresponding resolution group specified in the profiling configuration file.

- • arr — Array of the names of the set profile groups and the portion of the markup from the profile configuration file that represents the profile classes or the relationships between profile values for the corresponding resolution group.

- • doc — Optional. The identifier of the document tree. If doc is omitted or is 0 , the current document is used.



---

# set_user_property

# set_user_property

set_user_property ( key , value )

The set_user_property function defines a value for a specified parameter or variable that will be stored in memory. The parameter and its value are subsequently saved to the arbortext.wcf preferences file when the Arbortext Editor session exits. When Arbortext Editor exits, all parameters specified by set_user_property are saved to the user's preferences file. The next time Arbortext Editor starts, these parameters and their values will be loaded into memory. A custom application can call this function anytime during a Arbortext Editor session.

To avoid conflicts with other applications that may be using the same memory during a Arbortext Editor session, use a unique qualified name (following the Java class naming convention) for the key parameter. For example, the key name could be something like com.arbortext.sample.Verbose , where com.arbortext.sample is the Java class for the application, and Verbose is the specific property.

The value parameter can be any value, including an empty string.

The function returns any previous value associated with the specified key . This function will return an empty string if there is either no previous value or the previous value is an empty string.

Use the get_user_property function to retrieve a parameter and its associated value.

When Arbortext Editor starts, it loads these values into memory before processing the custom and application directories. This action makes the parameters available during the initialization phase of a custom application.

## Related Topics

- • get_user_property function

- • get_custom_dir function

- • get_custom_property function

- • application_name function



---

# sgml_feature

# sgml_feature

sgml_feature ( feature [, doc ])



This function returns information about one SGML Declaration feature for the document type associated with doc , or the current document if omitted. feature is one of the strings subdoc , formal , concur , explicit , implicit , simple , rank , datatag , omittag , or shorttag . The return value is 1 , 0 , or -1 . Some features may be 1 (on) or 0 (off) and others are 0 or a positive number. This command returns -1 if feature is invalid. The case of the string is not important.



---

# show_composer_log

# show_composer_log

show_composer_log ()

The show_composer_log function displays the Event Log window. If there is no Event Log window, this function creates it.

## Related Topics

- • XSL stylesheet error handling during publishing

- • get_composer_log_doc function

- • get_composer_log_contents function

- • composer_log function



---

# smart_insert_categories

# smart_insert_categories

smart_insert_categories ( arr [, doc ])

The smart_insert_categories function fills the array arr with the list of Smart Insert category names defined in the document type configuration file ( .dcf ) for the document type associated with doc . These categories are used in the Insert Markup dialog box when Smart Insert is turned on. If doc is omitted or 0 , the current document is used.

The function returns an array containing the category names in alphabetical order. The function also returns the number of entries in each array. The first entry is stored at index 1.

## Related Topics

- • Document type configuration files

- • Configuring Smart Insert



---

# smart_insert_category_elements

# smart_insert_category_elements

smart_insert_category_elements ( arr , category [, doc ])

The smart_insert_category_elements function fills the array arr with a list of element names for the Smart Insert category defined in the document type configuration file ( .dcf ) for the document type associated with doc . These category elements are used in the Insert Markup dialog box when Smart Insert is turned on. If doc is omitted or 0 , the current document is used.

The function returns an array containing the element names in the order in which they are declared in the .dcf file. The function also returns the number of entries in the array. The first entry is stored at index 1.

## Related Topics

- • Document type configuration files

- • Configuring Smart Insert

- • smart_insert_categories function



---

# span

# span

span ( s1 , s2 )

This function is like the C function strspn and returns the length of the initial substring of the string s1 containing only characters in the string s2 . Returns 0 if no characters in s2 match.



---

# spellskip_tag

# spellskip_tag

spellskip_tag ( tagname [, doc ])

This function returns a 1 (true) if the element name tagname is listed in the current document type's .dcf file as an element whose content should be skipped when doing a spelling check.

The tagname parameter can be either a real element name as defined in the document type definition (DTD) or a tag alias configured by a user.

The optional doc parameter specifies the document identifier for the desired document instance and defaults to the return value for current_doc if omitted.

If the specified tagname is either an element whose contents should be spell checked, or an element that does not exist in the DTD, the function returns a 0 (false).

Examples

```
#Test computeroutput tag for spellcheck tag skipping.
#
$ret=spellskip_tag("computeroutput")
#Do something if the tagname in $elementname is
#set to be skipped.
if (spellskip_tag($elementname)) {
...
)
```

## Related Topics

- • set spellskiptags command

- • Configuring elements to be ignored during a spelling check



---

# split_(Function)

# split (Function)

split ( string , arr [, fs ])

This function splits the string represented by string into array arr and returns the number of fields. The string value of the optional third argument fs specifies the field separator. fs is a list of break characters. For example: split("a:b;c", $arr, ":;") splits the string a:b;c into three fields, storing a in $arr[1] , b in $arr[2] , and c in $arr[3] .)

The fs argument is optional; if omitted or null, the break characters are space, tab, and newline. Fields may be separated by multiple occurrences of white space. If fs is given, only a single instance of the field separator character separates each field. Any previous elements in the array arr are discarded before split stores the fields.

## Related topic

- • join function



---

# strcoll

# strcoll

ret = strcoll ( string_a , string_b )

This function compares string_a with string_b according to the collation rules specified by the indexing collation configuration file indicated by the environment variable APTIXLANG .

The function returns -1 if string_a collates before string_b , 0 if string_a and string_b sort the same, and 1 if string_a collates after string_b .

This function is useful in the ixsorthook function or if you wish to write your own index processing.



---

# styler

# styler

styler ([ oid ])

This function opens a new Arbortext Styler window or brings an existing one to the front for editing the current Editor view stylesheet for the document to which oid belongs. The oid element is selected in the Arbortext Styler Elements list. If no oid is specified, the default is oid_current_tag(current_doc()) .



---

# styler_enabled

# styler_enabled

styler_enabled ([ doc ])

This function returns a non-zero value if the stylesheet associated with doc can be modified using Arbortext Styler . This non-zero value indicates the Arbortext Styler version that the stylesheet was created by, or has been updated for use by. Updating from one Arbortext Styler version to the next happens automatically. If the stylesheet cannot be modified using Arbortext Styler , the function returns 0 .

This function uses the stylesheet for the current document if no document is specified.



---

# styler_get_styled_elements

# styler_get_styled_elements

style_get_styled_elements ( sspath [, flags ])

This function takes a the stylesheet path sspath and returns the document identifier of a Free-form XML document containing a list of all of the styled elements in the stylesheet, that is, all of the elements with an assigned style other than Unstyled . If the stylesheet is not already loaded in memory, the function loads the stylesheet and leaves it loaded.

The sspath argument must be the path to a Arbortext Styler stylesheet.

The optional flags argument can have one of the following values:

- • 0 — User Formatting Elements and Styler Formatting Elements are not included in the output. This is the default.

- • 1 — User Formatting Elements are included in the output.

- • 2 — Styler Formatting Elements are included in the output.

- • 3 — User Formatting Elements and Styler Formatting Elements are both included in the output.

The Free-form document identified by this function has the following format:

```
<?xml version="1.0"?>
<doc
namespace declarations
>
<chapter/>
<section/>
<
namespace
:
element
/>
...
</doc>
```

The doc element is the wrapper element and contains all of the necessary namespace declarations used with elements in the stylesheet. Other elements represent the styled elements in the stylesheet. These elements are listed in alphabetical order in singleton syntax with any necessary namespace prefixes.



---

# stylesheet

# stylesheet

stylesheet ([ use [, doc ]])

This function returns the full path and file name for the stylesheet specified by use for a given document doc .

Valid values for use are:

If no document is specified, the doc parameter is the value of current_doc .



---

# stylesheet_export_fosi

# stylesheet_export_fosi

stylesheet_export_fosi ([ path [, doc ]])

This function writes the current editor Arbortext Styler stylesheet ( .style ) to path . If path is not specified, the Export FOSI Stylesheet dialog box is launched to let the user specify the path. When no doc is specified, Arbortext Editor defaults to the document returned by current_doc . The function returns 1 if the stylesheet is successfully exported, and 0 if there is any error. An error is returned if the current editor stylesheet can not be modified by Arbortext Styler .



---

# stylesheet_export_xsl

# stylesheet_export_xsl

stylesheet_export_xsl ([ path [, doc [, target ]]])

This function exports the current editor Arbortext Styler stylesheet ( .style ) for doc as an XSL stylesheet to the path specified by path . The stylesheet_export_xsl function is only valid when the stylesheet for doc is a Arbortext Styler stylesheet. If doc is not supplied, it defaults to current_doc . If path is not specified, a dialog box is launched to let the user specify the path.

The target parameter must be on the following types:

- • fo — Exports an XSL-FO stylesheet for creating print or PDF output.

- • html — Exports an XSL stylesheet for creating HTML output.

- • htmlhelp — Exports an XSL stylesheet for creating HTML Help output using the Arbortext Editor Publish > For HTML Help capability.

- • web — Exports an XSL stylesheet for creating web output using the Arbortext Editor Publish > For Web capability.

If target is not specified, html is assumed.

The function returns 1 if the stylesheet was successfully exported, 0 if there was an error.



---

# stylesheet_gentext_lang_stats

# stylesheet_gentext_lang_stats

stylesheet_gentext_lang_stats ( lang , stats [, doc ])

This function provides information about the translation for the specified lang imported from an XLIFF file into a stylesheet to provide translations of generated text. stats populates an array that provides information on the results of the requested translation from the XLIFF file. doc is optional - specify a stylesheet document or a user document with which the stylesheet is associated.

Values for the parameters are listed below:

When successful, the function will return 1, otherwise it will return 0. The function can be unsuccessful if:

- • Stylesheet is not found

- • lang does not match a target generated text language on the XLIFF file

If the function is unsuccessful, all stats will be zero.

Refer to Using ACL to Import XLIFF Files in Arbortext Styler help for some sample ACL code demonstrating the use of this function.

## Related Topics

- • stylesheet_import_xlf



---

# stylesheet_get_list_dir

# stylesheet_get_list_dir

stylesheet_get_list_dir ( labels[] , paths[] , is_Styler[] , use [, dir [, maxlabelchars [, labeltitleonly ]]])

This function returns information on the valid stylesheets in directory dir in the labels , paths , and is_Styler arrays.

The labels for valid stylesheets in directory dir fill the labels[] array. Arbortext Editor generates labels by combining the stylesheet title (if any) and path into a string and truncating it if necessary so that it is no longer than maxlabelchars . A stylesheet title is specified in the Stylesheet ID processing instruction in the stylesheet file ( <?APT StylesheetID ... Title="title" ...> ). These labels are displayed in the Arbortext Editor user interface.

The absolute path of each valid stylesheet fills the paths[] array.

Values of 0 and 1 fill the is_Styler[] array. A 1 indicates you can use the stylesheet with Arbortext Styler , a 0 indicates that you cannot use the stylesheet with Arbortext Styler .

Valid stylesheets are .style , .xsl , and .fos files whose publishing type matches use . A stylesheet's type is derived from the CompositionTypes attribute on the StylesheetID processing instruction. Valid use types are any , htmlfile , htmlhelp , print , pdf , web , wordxml , and xsl . If use is any , all .style , .xsl , and .fos files are returned.

The following table describes the default stylesheet publishing types if a stylesheet file does not have a StylesheetID processing instruction, and whether editor will be added:

If dir is omitted, the current directory is used.

maxlabelchars controls the maximum number of characters included in the returned labels. If maxlabelchars is omitted, the label length defaults to 50.

If labeltitleonly is 1 , then the label is the stylesheet title, if it exists. If the stylesheet title doesn't exist, the label is the path to the stylesheet.

## Related Topics

- • Stylesheet overview

- • stylesheet_get_list_doc function

- • stylesheet_list_add function

- • Select Stylesheets dialog box

- • Stylesheet ID processing instruction

- • Associating a stylesheet with your document

- • Stylesheet association processing instruction

- • Using Arbortext Publishing Engine for publishing documents



---

# stylesheet_get_list_doc

# stylesheet_get_list_doc

stylesheet_get_list_doc ( labels[] , paths[] , is_styler[] , use [, doc [, maxlabelchars [, labeltitleonly ]]])

This function returns information on valid stylesheets for doc in the labels , paths , and is_styler arrays.

The labels for valid doc stylesheets fill the labels[] array. Arbortext Editor generates labels by combining the stylesheet title (if any) and path into a string and truncating it if necessary so that it is no longer than maxlabelchars . A stylesheet title is specified in the Stylesheet ID processing instruction in the stylesheet file ( <?APT StylesheetID ... Title="title" ...> ). These labels are what Arbortext Editor displays in the user interface.

The absolute path of each valid stylesheet fills the paths[] array.

Values of 0 and 1 fill the is_styler[] array. A 1 means you can use the stylesheet with Arbortext Styler , a 0 means that you cannot use the stylesheet with Arbortext Styler .

Valid stylesheets are .style , .xsl , and .fos files whose publishing type matches use . A stylesheet's type is derived from the CompositionTypes attribute on the StylesheetID processing instruction.

Valid use types are any , htmlfile , htmlhelp , print , pdf , web , wordxml , and xsl . If use is any , all .style , .xsl , and .fos files are returned.

The following table describes the default stylesheet publishing types if a stylesheet file does not have a StylesheetID processing instruction:

If doc is omitted or 0 , the current document is used.

maxlabelchars controls the maximum number of characters included in the returned labels. If maxlabelchars is omitted, the label length defaults to 50.

If labeltitleonly is 1 , then the label is the stylesheet title, if it exists. If the stylesheet title doesn't exist, the label is the path to the stylesheet.

## Related Topics

- • Stylesheet overview

- • Select Stylesheets dialog box

- • stylesheet_get_list_dir function

- • stylesheet_list_add function

- • Stylesheet ID processing instruction

- • Associating a stylesheet with your document

- • Stylesheet association processing instruction

- • Using Arbortext Publishing Engine for publishing documents



---

# stylesheet_import_xlf

# stylesheet_import_xlf

stylesheet_import_xlf ( path , flags , stats [, doc ])

This function imports the XLIFF file ( .xlf ) found at path into a stylesheet to provide translations of generated text. Use flags to control how to process translations when certain questions occur. stats populates an array that provides information on the number of translation units that were found in the XLIFF file and updated in the stylesheet, and the number that not imported or not found in the XLIFF file. doc is optional - specify a stylesheet document or a user document with which the stylesheet is associated.

Values for the parameters are listed below:

When successful, the function will return 1, otherwise it will return 0. The function can be unsuccessful if:

- • Stylesheet is not found

- • XLIFF file cannot be opened

- • XLIFF file is not valid

- • One of more stylesheet modules is read only, preventing a translation being imported

If the function is unsuccessful because of the read-only nature of a stylesheet module, generated text in the writable modules will still be updated and the results reflected in the import statistics. If it is unsuccessful for any of the other listed reasons, all stats will be zero.

Refer to Using ACL to Import XLIFF Files in Arbortext Styler help for sample ACL demonstrating the use of this function.

## Related Topics

- • stylesheet_gentext_lang_stats



---

# stylesheet_list_add

# stylesheet_list_add

stylesheet_list_add ( path , use , doctype )

This function adds path to a list of stylesheet paths for the specified doctype and use . The stylesheet_get_list_doc function searches this list for valid stylesheets during the current Arbortext Editor session. Arbortext Editor verifies that the path specifies a stylesheet that supports the use .

Valid use types are any , htmlfile , htmlhelp , pda , print , pdf , web , wml , and xsl . If use is any , all .style , .xsl , and .fos files are returned.

For a stylesheet to be returned by stylesheet_get_list_doc , the use passed to stylesheet_get_list_doc must match the use passed to stylesheet_list_add .

The doc passed to stylesheet_get_list_doc must use the same doctype passed to stylesheet_list_add .

If you are using Arbortext Publishing Engine for publishing documents , the path must be specified by a URL or it will be ignored by Arbortext Editor . A stylesheet used for editing must always be specified using a local absolute or relative path.

An example for adding stylesheets using stylesheet_list_add :

```
# Let users select a stylesheet for a given "doc" and "use"
# from a list of stylesheets in their document and document
# type directories or by browsing; if they browse to select
# a stylesheet, include that stylesheet in the list the
# next time they ask for the same "use" with either the
# same document, or another document of the same document
# type.
# Valid "use" values are any of the Type attributes
# of publish elements in the document type's .dcf file,
# plus "editor"
function stylesheet_get(doc, use)
{
# First get list of stylesheets that we show by label;
#
# The list includes those valid for "use" in the
# document directory, document type directory, or
# that were previously selected for this use and
# document type;
local labels[], paths[], is_styler[];
local n = stylesheet_get_list_doc(labels, paths, is_styler, use, doc);
# Display this list to users, let them pick a stylesheet
# from the list or by browsing.
# NOTE: this function does not actually exist;
local path = stylesheet_pick(labels, paths, use);
# If users browsed to the stylesheet, add it to the
# list of stylesheets that stylesheets_get_list_doc
# will consider returning the next time;
stylesheet_list_add(path, use, doc_type(doc));
return path;
}
```

## Related Topics

- • Stylesheet overview

- • Select Stylesheets dialog box

- • stylesheet_get_list_dir function

- • stylesheet_get_list_doc function

- • Associating a stylesheet with your document

- • Stylesheet association processing instruction



---

# stylesheet_new

# stylesheet_new

stylesheet_new ([ doc ])

This function creates a new stylesheet using an existing template, makes this new stylesheet the Editor view stylesheet, and launches Arbortext Styler .

The temporary name Stylesheet n is assigned to the new stylesheet; it displays on the document title bar. The number n increments during an entire Arbortext Editor session.



---

# stylesheet_revert

# stylesheet_revert

stylesheet_revert ([ doc ])

This function causes the editor stylesheet for document doc to revert to the last saved version. If doc is not supplied, the value of current_doc is used. This function is enabled only if the current stylesheet has been used before. The function is disabled when working with a new stylesheet.

This function corresponds to the Format > Revert Stylesheet menu item.



---

# stylesheet_save

# stylesheet_save

stylesheet_save ([ doc ])

This function saves the current editor stylesheet for document doc ; if doc is not supplied, the function defaults to current_doc . Arbortext Styler stylesheets are saved as .style files. FOSIs are saved as .fos files. If the stylesheet has not previously been saved, this function launches the Save Stylesheet As dialog box.

This function corresponds to Format > Save Stylesheet .

## Related Topics

- • stylesheet_export_fosi

- • stylesheet_export_xsl

- • Default stylesheet locations



---

# stylesheet_saveas

# stylesheet_saveas

stylesheet_saveas ([ pathname [, doc ]])

This function lets you save a modified stylesheet. If the current stylesheet was created or modified by Arbortext Styler , it is automatically saved as a .style file.

This function will save the stylesheet in one of three ways:

- • As a document level stylesheet, using the current doc directory as the target directory, and the current docname to create a document-specific stylesheet, (the resulting stylesheet is written to doc-pathname / docname .xsl )

- • As an application level stylesheet, using the current doc directory as the target directory, and the current application-name to create a local version of the application stylesheet (the resulting stylesheet is written to doc-pathname / application-name .xsl )

- • As an independent stylesheet, using a target directory and name specified by the user.

If no pathname is supplied, this function launches the Save Stylesheet As dialog box for document doc .

If doc is omitted or 0 , the current document is used.

The two possible return values from the dialog box are:

The Save Stylesheet As menu item corresponds to stylesheet_saveas .

## Related Topics

- • Save Stylesheet As dialog box

- • Default stylesheet locations



---

# stylesheet_select

# stylesheet_select

stylesheet_select ([ name [, use [, doc ]]])

This function controls the selection of a stylesheet; it corresponds to the Format > Select Stylesheets menu item. All parameters are optional.

If you do not supply a name , the function launches the Select Stylesheets dialog box for document doc ; (the value of current_doc() is used if you do not specify doc ).

If you supply a name , this function selects the named stylesheet and returns its full path name. name can be specified in the following ways:

- • The name can be the path and file name of the stylesheet, with or without the .fos , .xsl , or .style extension. Arbortext Editor first looks for a .fos file, and then an .xsl file, and then a .style file.

- • The name can be the base name of the stylesheet file (the file name without the path). If just the base name is supplied, Arbortext Editor looks for the file in the document directory, and, if not found, in the application directory.

## Related Topics

- • Default stylesheet locations

- • Select Stylesheets dialog box



---

# sub

# sub

sub ( regexpr , repl [, string , lvalue ])

The sub function is similar to gsub , except that this function attempts only one match and substitution of string that matches the regular expression regexpr and replaces the substring with the string repl . The resulting string is assigned to lvalue , which must be a variable name or an array element. If string is omitted, then the value of lvalue is used as the source string. When copying the string to lvalue , the part that was matched by regexpr is replaced according to the string repl .

If repl contains a & or \0 , then it is replaced with the substring that matched regexpr . If repl contains a \ n , where n is a digit between 1 and 9, then it is replaced in the substitution with that part of the string that matched the n th parenthesized subexpression of regexpr . n must not be greater than the number of parenthesized expressions in regexpr .

sub returns 1 (True) if the substring was replaced, or 0 if no match occurred. The lvalue is not changed if 0 is returned. Note that because the expression parser interprets backslash sequences in double quoted strings, you must use two backslashes to get a single \ character in regexp or repl or use single quotes to delimit strings.

## Related topic

Using regular expressions



---

# substr

# substr

substr ( string , n1 [, n2 ])

This function extracts a substring from string , starting at position n1 , of n2 characters. The first character of string is position 1. If n1 is larger than length( string ) , the null string is returned. If n1 + n2 is longer than string , then the remainder of string is returned. The n2 argument is optional; if omitted, the remainder of the string is returned.

For example, the value of substr("rnotes9302", 2, 5) is "notes" .



---

# system

# system

system ( cmd [, flags ])

Use this function to run applications outside of the Arbortext Editor environment. The cmd parameter is a command to execute in a DOS window. If flags is set to one ( 1 ) the command will be executed in a hidden window.

If the process fails to launch, the function returns a negative one (-1) and stores an error message in the $main::ERROR variable.

## Related Topics

- • sh command



---

# system_id

# system_id

system_id ([ doc ])

This function returns the system identifier from the DOCTYPE declaration for the document doc or the null string if none was specified. If doc is omitted or 0 , the current document is used.

## Related Topics

- • public_id function

- • doc_type_gi function



---

# tag_alias

# tag_alias

tag_alias ( tagname [, doc ])

This function returns the alias of tagname , where tagname is the real name of the tag as defined in the DTD. A null string is returned if tagname does not have an alias.

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

## Related Topics

- • Alias map overview

- • tag_real_name function

- • attr_real_name function

- • attr_alias function

- • attr_value_real_name function

- • attr_value_alias function



---

# tag_attr_choices

# tag_attr_choices

tag_attr_choices ( tagname , attr , arr [, doc ])

This function fills the array arr with the list of declared values for the NAMEGROUP type attribute named attr of the element specified by tagname , returning the number of choices. The first attribute value is returned as index 1.

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

## Related Topics

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attr_value function

- • tag_attrs function

- • tag_has_attr function

- • tag_has_conref function

- • tag_content function



---

# tag_attr_conref

# tag_attr_conref

tag_attr_conref ( tagname , attr [, doc ])

This function returns 1 (True) if the attribute attr for the element specified by tagname is declared as a #CONREF attribute in the DTD for the specified document. If the document type definition for your document instance includes the NAMECASE GENERAL NO setting, then the tagname parameter will be case sensitive. (If you have applied an alias map to the document, tagname and attr can be either aliases or real names.)

The doc argument specifies the identifier of the document tree. If omitted or 0 , the current document is used.

## Related Topics

- • tag_attr_choices function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attr_value function

- • tag_attrs function

- • tag_has_attr function

- • tag_has_conref function

- • tag_content function



---

# tag_attr_default

# tag_attr_default

tag_attr_default ( tagname , attr [, doc ])

This function returns the default value of the attribute attr for the element tagname as defined in the DTD for the specified document.

It returns a null string if attr does not have a default value or if no such attribute or element exists. If doc is omitted or 0 , the current document is used.

## Related Topics

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attr_value function

- • tag_attrs function

- • tag_has_attr function

- • tag_has_conref function

- • tag_content function



---

# tag_attr_fixed

# tag_attr_fixed

tag_attr_fixed ( tagname , attr [, doc ])

This function returns 1 (True) if the attribute named attr for the element tagname is declared as a #FIXED attribute in the DTD for the specified document.

If doc is omitted, the current document is used.

## Related Topics

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attr_value function

- • tag_attrs function

- • tag_has_attr function

- • tag_has_conref function

- • tag_content function



---

# tag_attr_required

# tag_attr_required

tag_attr_required ( tagname , attr [, doc ])

This function returns 1 (True) if the attribute named attr for the element named tagname is declared as a #REQUIRED attribute in the DTD for the specified document.

If doc is omitted, the current document is used.

## Related Topics

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_type function

- • tag_attr_value function

- • tag_attrs function

- • tag_has_attr function

- • tag_has_conref function

- • tag_content function



---

# tag_attr_type

# tag_attr_type

tag_attr_type ( tagname , attr [, doc ])

This function returns the declared attribute value type for the attribute named attr for the element specified by tagname . The returned value is one of the following strings:

.

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

## Related Topics

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_value function

- • tag_attrs function

- • tag_has_attr function

- • tag_has_conref function

- • tag_content function



---

# tag_attr_value

# tag_attr_value

tag_attr_value ( tagname , attr [, doc ])

This function returns the current global value of the attribute named attr for the tag specified by tagname .

If attr is not a valid attribute or tagname is not a valid tag, a null string is returned.

The doc argument specifies the identifier of the document tree. If doc omitted or 0 , the current document is used.

## Related Topics

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attrs function

- • tag_has_attr function

- • tag_has_conref function

- • tag_content function



---

# tag_attrs

# tag_attrs

tag_attrs ( tagname , arr [, doc ])

This function fills the array arr with the list of attribute names declared for the tag specified by tagname . This function returns the number of attributes. The first attribute name is returned as index 1.

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

## Related Topics

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attr_value function

- • tag_has_attr function

- • tag_has_conref function

- • tag_content function



---

# tag_content

# tag_content

tag_content ( tagname [, doc ])

This function returns the declared content of the tag specified by tagname . The returned value is one of the following strings:

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

If the tag is a Arbortext Editor defined tag (such as _font ), the function returns “ UNDEFINED ”. If the tag is not declared in the DTD and is not a Arbortext Editor defined tag, the function returns an empty string.

## Related Topics

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attr_value function

- • tag_attrs function

- • tag_has_attr function

- • tag_has_conref function



---

# tag_create

# tag_create

tag_create ( qname [, uri [, empty [, doc ]]])

This function is used to either create new tags in Free-form XML document instances or to create foreign namespace tags in XML documents. The qname parameter provides the name of the new tag with an optional prefix. The uri parameter, if supplied, specifies the URI for the new tag. If it is not specified, then the target namespace for the document is used (none for a Free-form XML document). If the empty parameter is supplied and not zero, then the element is not allowed to have content.

The function returns 1 on success.

If the doc parameter is 0 or omitted, then the current document is used.



---

# tag_description

# tag_description

tag_description ( tagname [, doc ])

This function returns the description for the specified tag. A null string is returned if tagname does not have an description. The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

## Related Topics

- • Creating element and attribute descriptions

- • Viewing element and attribute descriptions in your document

- • attr_description function



---

# tag_display_(Function)

# tag_display (Function)

tag_display ( tagname [, doc ])

This function returns a string describing the global tag display mode of the tag specified by tagname .

If doc is omitted or 0 , the current document is used.

The returned string corresponds to the option set by the tag_display command and is one of the following: "full" , "partial" , "icon" , "none" , or "default" . If the tag display mode has not been changed for tagname , the function returns "default" .

## Related Topics

- • set showemptyelement command



---

# tag_display_name

# tag_display_name

tag_display_name ( tagname [, doc ])

This function returns the alias of the tag specified by tagname , if the tag has an alias. If the tag doesn't have an alias, tag_display_name returns the tag's real name. tagname can be an alias or a real name.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is searched.

## Related Topics

- • Alias Map Editor



---

# tag_exists

# tag_exists

tag_exists ( tagname [, doc ])

This function returns 1 (True) if the tag named tagname is a valid tag name (including user-defined tags) in the current document (regardless of whether the tag is currently in use). If the tag name is not valid, 0 is returned.

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.



---

# tag_has_attr

# tag_has_attr

tag_has_attr ( tagname , attr [, doc [, dtdOnly ]])

This function returns 1 (True) if the tag tagname has an attribute named attr . If the tag doesn't have the specified attribute, 0 is returned.

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

If the value specified by dtdOnly is omitted or is 1 , then the function will only return 1 for tags and attributes that are declared in the DTD or XML schema. If the value specified by dtdOnly is 0 , then the function will also return 1 if attr is an undeclared attribute that has been seen on the tag tagname .

For a Free-form XML document, the dtdOnly parameter is ignored. The function will return 1 if attr is seen on the tag tagname .

## Related Topics

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attr_value function

- • tag_attrs function

- • tag_has_conref function

- • tag_content function



---

# tag_has_conref

# tag_has_conref

tag_has_conref ( tagname [, doc ])

This function returns 1 (True) if the tag specified by tagname has an attribute declared as #CONREF in the DTD. If the tag doesn't have this attribute, the function returns 0 . If the DTD for your document includes the NAMECASE GENERAL NO specification, then the tagname parameter will be case sensitive. (If you have applied an alias map to the document, tagname can be either an alias or a real name.)

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

## Related Topics

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attr_value function

- • tag_attrs function

- • tag_has_attr function

- • tag_content function



---

# tag_names

# tag_names

tag_names ( arr [, dtd [, doc ]])

The tag_names function fills the array arr with an alphabetical list of elements and similar markup icons for the current document type, returning the total number. The first name returned is stored at index 1. All previous elements in arr are discarded.

If the value specified by dtd is non-zero, then the array includes only names of elements defined in the DTD.

If dtd is omitted or is 0 , the array arr includes:

- • The DTD element names.

- • The names of markup icons supplied by Arbortext Editor . (For example, _ignore , _font , and so on.)

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

## Related Topics

- • file_entity_names function

- • filep_entity_names function

- • text_entity_names function



---

# tag_names_ns

# tag_names_ns

tag_names_ns ( arr [, namespace [, doc ]])

The tag_names_ns function fills the array arr with an alphabetical list of tags for the given document. If the namespace parameter is specified and not empty, then only those tags declared with that namespace URI are returned. If the namespace parameter is specified and is an empty string, then only those tags with no namespace are returned. If the namespace parameter is not specified, then all declared tags in the document type are returned, as well as tags in any foreign namespaces with the names qualified in the form { namespace-uri } local-name .

The function returns the number of entries loaded in the array.

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.

This function is meant for XML documents. If doc refers to a non-XML document, the namespace parameter is ignored, and the function acts like tag_names ( arr , 1, doc ) was called.



---

# tag_real_name

# tag_real_name

tag_real_name ( tagname [, doc ])

This function returns the real name (as specified in the DTD) of tagname . The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is searched.

## Related Topics

- • Alias map overview

- • tag_alias function

- • attr_real_name function

- • attr_alias function

- • attr_value_real_name function

- • attr_value_alias function



---

# tag_substitutions

# tag_substitutions

tag_substitutions ( tagname , arr [, doc ])

This function fills the array arr with the list of elements specified in the .dcf file as being possible substitutions for the element specified by tagname . The function returns the number of elements added to the array. The order of the array matches the order specified in the .dcf file.

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.



---

# target_id_attr_name

# target_id_attr_name

target_id_attr_name ( tagname [, doc ])

This function returns the name of the ID attribute (for example, id ) for the target tag specified by tagname . If the tag has no such attribute, target_id_attr_name returns the null string.

The doc argument specifies the identifier of the document tree. If doc is omitted or 0 , the current document is used.



---

# target_tag

# target_tag

target_tag ( tagname [, doc ])

The target_tag function returns 1 (true) if the tag named tagname is declared as a target element in the .dcf file for the document type associated with doc . If doc is omitted or 0 , the current document is used.

## Related Topics

- • target_tag_name function

- • target_id_attr_name function



---

# target_tag_name

# target_tag_name

target_tag_name ([ doc ])

The target_tag_name function returns the name of the primary target element for the document type associated with doc . It returns the null string if no target tag was designated for the document type, or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

## Related Topics

- • target_tag function

- • target_id_attr_name function



---

# tbl_area_celllist

# tbl_area_celllist

count = tbl_area_celllist ( upperLeftCellId , lowerRightCellId , array )

This function fills array with the ID of each cell in the rectangle of cells defined by upperLeftCellId and lowerRightCellId and returns the number of IDs. The IDs are returned in row major order.



---

# tbl_caret_col

# tbl_caret_col

tbl_caret_col ( )

This function returns the column number (starting with 1) of the cell containing the cursor. Returns 0 if the cursor is not in a table cell.

## Related Topics

- • insert built-in function

- • insert_column command

- • insert_row command

- • goto_cell built-in function

- • tbl_caret_row built-in function

- • tbl_col_count built-in function



---

# tbl_caret_row

# tbl_caret_row

tbl_caret_row ( )

This function returns the row number (starting with 1) of the cell containing the cursor. Returns 0 if the cursor is not in a table cell.

## Related Topics

- • insert built-in function

- • insert_column command

- • insert_row command

- • goto_cell built-in function

- • tbl_caret_col built-in function

- • tbl_col_count built-in function

- • tbl_row_count built-in function



---

# tbl_cell_clear

# tbl_cell_clear

[0|1] = tbl_cell_clear ( cellId , content , span , attributes )

If the content , span , and attribute parameters are non-zero values, tbl_cell_clear deletes the content and attributes of cellId and deletes the multicell that contains cellId .

## Related Topics

- • tbl_obj_attr_clear

- • tbl_cell_unspan



---

# tbl_cell_col

# tbl_cell_col

columnId = tbl_cell_col ( cellId )

This function returns the ID of the column containing cell cellId .



---

# tbl_cell_fontpi

# tbl_cell_fontpi

oid = tbl_cell_fontpi ( cellId , command )

This function attempts to insert, locate, or delete a cell font processing instruction for cell cellId as indicated by command , which may have the value insert , find , or delete . After doing so, this function returns the OID of the cellfont PI, if it still exists, or null_oid .



---

# tbl_cell_in_multicell

# tbl_cell_in_multicell

[0|1] = tbl_cell_in_multicell ( cellId )

This function returns 1 if cell cellId is a member of a multicell, 0 otherwise. Note that this routine is equivalent to the expression tbl_cell_is_spanning( cellId ) || tbl_cell_is_spanned( cellId ) .



---

# tbl_cell_instantiate

# tbl_cell_instantiate

[0|1] = tbl_cell_instantiate ( cellId )

This function marks cell cellid as being non-sparse. Some table models, such as CALS, allow sparse markup, where some cells of a table are not explicitly described in markup. We add “generated” cell markup to the document when we read a sparse table so that there is markup underlying every table cell. When we save a document containing a table, we delete this “generated” markup, unless the cell has acquired content, attributes, or some other reason for existence. This function allows the user to require that the markup corresponding to a cell NOT be discarded, even if it is generated markup.

Note that we never strip out “real” markup, only generated markup.



---

# tbl_cell_is_spanned

# tbl_cell_is_spanned

[0|1] = tbl_cell_is_spanned ( cellId )

This function returns 1 if cell cellId is a member of a multicell but not the master (spanning) cell, 0 otherwise.



---

# tbl_cell_is_spanning

# tbl_cell_is_spanning

[0|1] = tbl_cell_is_spanning ( cellId )

This function returns 1 if cell cellId is the master (spanning) cell of a multicell, 0 otherwise.



---

# tbl_cell_neighbor

# tbl_cell_neighbor

cellId = tbl_cell_neighbor ( cellId , direction , offset )

This function returns the ID of the cell offset cells away in direction direction from cell cellId . It returns h::tblNullToid if the surrounding grid doesn't contain a cell as far away as specified.



---

# tbl_cell_next_galley_cell

# tbl_cell_next_galley_cell

cellId = tbl_cell_next_galley_cell ( cellId [, wrap ])

This function returns the ID of the cell after cell cellId in galley order, or h:tblNullToid if no such cell exists. If wrap is present and non-zero, tbl_cell_next_galley_cell will return the ID of the first cell in the sequence when the last cell in the sequence is reached.



---

# tbl_cell_on_multicell_edge

# tbl_cell_on_multicell_edge

[0|1] = tbl_cell_on_multicell_edge ( cellId , direction )

This function returns 1 if cell cellId is on a specific edge of a multicell, 0 otherwise.



---

# tbl_cell_prev_galley_cell

# tbl_cell_prev_galley_cell

cellId = tbl_cell_prev_galley_cell ( cellId [, wrap ])

This function returns the ID of the cell before cell cellId in galley order, or h:tblNullToid if no such cell exists. If wrap is present and non-zero, tbl_cell_next_galley_cell will return the ID of the first cell in the sequence when the last cell in the sequence is reached.



---

# tbl_cell_row

# tbl_cell_row

rowId = tbl_cell_row ( cellId )

This function returns the ID of the row containing cell cellId .



---

# tbl_cell_ruleneighbor

# tbl_cell_ruleneighbor

ruleId = tbl_cell_ruleneighbor ( cellId , direction )

This function returns the ID of the rule bounding cell cellId on side direction .



---

# tbl_cell_setcaret

# tbl_cell_setcaret

[0|1] = tbl_cell_setcaret ( cellId , end )

This function places the caret at the beginning (if end is zero) or end of cell cellId.



---

# tbl_cell_span

# tbl_cell_span

[0|1] = tbl_cell_span ( upperLeftCellId , lowerRightCellId )



This function combines the rectangle of cells specified by upperLeftCellId and lowerRightCellId into a multicell.

It does this by constructing a new rectangle with the coordinates [sumUpperLeft, sumLowerRight]

where:

```
sumUpperLeft.X = min(oldUpperLeft.X, newUpperLeft.X)
sumUpperLeft.Y = min(oldUpperLeft.Y, newUpperLeft.Y)
sumLowerRight.X = max(oldLowerRight.X, newLowerRight.X)
sumLowerRigth.Y = max(oldLowerRight.Y, newLowerRight.Y)
```

and trying to span that.

This will fail if any cell in the resulting rectangle is a member of any other multicell.



---

# tbl_cell_unspan

# tbl_cell_unspan

[0|1] = tbl_cell_unspan ( cellId )



This function deletes the multicell containing cellId , which may be any member of the multicell.



---

# tbl_cell_unspanned_neighbor

# tbl_cell_unspanned_neighbor

cellId = tbl_cell_unspanned_neighbor ( cellId , direction , offset )

This function returns the ID of the cell offset cells away in direction direction from cell cellId ; it considers only unspanned cells in calculating how far to go.



---

# tbl_col_cell

# tbl_col_cell

cellId = tbl_col_cell ( columnId , rowIndex )

Returns the ID of the cell that is positioned rowIndex rows from the top of column columnId . The uppermost row in a column is row 1.



---

# tbl_col_celllist

# tbl_col_celllist

count = tbl_col_celllist ( columnId , array )

This function fills array with the ID of each cell in column columnId from top to bottom and returns the number of IDs.



---

# tbl_col_count

# tbl_col_count

tbl_col_count ([ oid ])

This function returns the number of columns in the table given by object identifier oid . If oid is omitted, this function returns the number of columns in the table containing the cursor. Returns —1 if the cursor is not inside a table.

## Related Topics

- • insert built-in function

- • insert_column command

- • insert_row command

- • goto_cell built-in function

- • tbl_caret_col built-in function

- • tbl_caret_row built-in function

- • tbl_row_count built-in function



---

# tbl_col_index

# tbl_col_index

index = tbl_col_index ( columnId )

Returns the position of column columnId within its grid. The leftmost column in a grid has index 1.



---

# tbl_col_neighbor

# tbl_col_neighbor

columnId = tbl_col_neighbor ( columnId , offset )

Returns the ID of the column offset columns to the left ( offset <0) or right ( offset >0) of column columnId .



---

# tbl_col_rulelist

# tbl_col_rulelist

count = tbl_col_rulelist ( columnId , direction , array )

This function fills array with the IDs of the rules on the edge direction of the column columnId .



---

# tbl_coltool_mouse

# tbl_coltool_mouse

columnId = tbl_coltool_mouse ( viewid )

This function returns the ID of the column with which the mouse pointer is vertically aligned in view viewId (or the active view if viewId is omitted). It returns h::tblNullToid if the view doesn't contain an active table or if the mouse pointer isn't in a table column.



---

# tbl_dlg_target

# tbl_dlg_target

tbl_dlg_target ([ type [, doc ]])

This function returns the table object that table-related dialog boxes (such as the Table Properties dialog box) operate on. The return value is either a table selection object if one or more cells are selected, the ID of the cell containing the caret if there is no table selection, or h::tblNullToid if the caret is outside a table.

- • type — Optional. Determines the type of table object returned and is one of the strings returned by the tbl_obj_type function. Values include cell , row , column , grid , set , and selector . For example, tbl_dlg_target("row") returns the row id of the cell containing the caret, or the row id of the first cell in the table selection.

- • doc — Optional. Specifies the identifier of the document containing the table. If omitted or 0 , the current document is used.

## Related Topics

- • tbl_selection_get function

- • tbl_oid_cell function

- • tbl_obj_type function



---

# tbl_edit_close

# tbl_edit_close

1 = tbl_edit_close ( success , [doc] )

This function decrements the table-edit count for document doc (or the active document, if doc is omitted). If the count is zero and success is also zero, it calls undo to discard any changes to the document since the corresponding call to tbl_edit_open .

This function always returns 1.



---

# tbl_edit_open

# tbl_edit_open

tbl_edit_open ( toid [, doc [, undolabel ]])

This function increments the table-edit count for document doc (or for the active document if doc is omitted). This function returns 1 if it is completed successfully.

If toid is not equal to h::tblNullToid , it is used to indicate how much information Arbortext Editor must rescan if tbl_edit_close is used to undo document changes.

The optional string argument undolabel is used as the name of the operation for the Undo and Redo menu items. The function returns a 0 if the undolabel refers to a cancelled operation that cannot be tracked within a doc .

Example

```
tbl_edit_open(toid, doc, "Insert Row");
```



---

# tbl_grid_cell

# tbl_grid_cell

cellId = tbl_grid_cell ( gridId , colIndex , rowIndex )

This function returns the ID of the cell whose position is given by colIndex and rowIndex in grid gridId . The upper-left cell in the grid has coordinates (1,1).



---

# tbl_grid_celllist

# tbl_grid_celllist

count = tbl_grid_celllist ( gridId , array )

This function fills array with the IDs of each cell in grid gridId and returns the number of IDs. The cell IDs are returned in row-major order.



---

# tbl_grid_col

# tbl_grid_col

columnId = tbl_grid_col ( gridId , colIndex )

This function returns the ID of column colIndex in grid gridId . The left-most column has an index of 1.



---

# tbl_grid_colcount

# tbl_grid_colcount

count = tbl_grid_colcount ( gridId )

This function returns the number of columns in grid gridId .



---

# tbl_grid_collist

# tbl_grid_collist

count = tbl_grid_collist ( gridId , array )

This function fills array with the IDs of the columns in grid gridId ordered from left to right and returns the number of IDs.



---

# tbl_grid_first_galley_cell

# tbl_grid_first_galley_cell

cellId = tbl_grid_first_galley_cell ( gridId )

This function returns the first cell in grid gridId in galley order.



---

# tbl_grid_insert

# tbl_grid_insert

gridId = tbl_grid_insert ( gridId , addBefore , rowCount , columnCount )

This function inserts a new grid with rowCount rows and columnCount columns into the table containing grid gridId . If addBefore is nonzero, the new grid is inserted before gridId . It returns the ID of the new grid or h::tblNullToid upon failure.



---

# tbl_grid_last_galley_cell

# tbl_grid_last_galley_cell

cellId = tbl_grid_last_galley_cell ( gridId )

This function returns the last cell in grid gridId in galley order.



---

# tbl_grid_neighbor

# tbl_grid_neighbor

gridId = tbl_grid_neighbor ( gridId , offset )

This function returns the ID of the grid located offset grids before or after grid gridId in the table containing gridId .



---

# tbl_grid_row

# tbl_grid_row

rowId = tbl_grid_row ( gridId , rowIndex )

This function returns the ID of the row located rowIndex rows from the top of grid gridId . The uppermost row in any grid has an index of 1.



---

# tbl_grid_rowcount

# tbl_grid_rowcount

count = tbl_grid_rowcount ( gridId )

This function returns the number of rows in grid gridId .



---

# tbl_grid_rowlist

# tbl_grid_rowlist

count = tbl_grid_rowlist ( gridId , array )

This function fills array with the IDs of the rows in grid gridId ordered from top to bottom and returns the number of IDs.



---

# tbl_grid_rule

# tbl_grid_rule

ruleId = tbl_grid_rule ( gridId , startColIndex , startRowIndex , endColIndex , endRowIndex )

This function returns the ID of the rule that connects the vertices ( startColIndex , startRowIndex ) and ( endColIndex , endRowIndex ) in grid gridId .



---

# tbl_grid_rulelist

# tbl_grid_rulelist

count = tbl_grid_rulelist ( gridId , array )

This function fills array with the IDs of the rules in grid gridId sorted into row-major order and returns the number of IDs.



---

# tbl_grid_split

# tbl_grid_split

[0|1] = tbl_grid_split ( toid )

This function splits the grid containing toid into two separate grids, with the row containing toid as the uppermost row in the second grid. It fails if the table model doesn't support multiple grids in the same table or if performing the split would result in either or both grids being invalid in any way according to the table model's rules. toid may be the ID of either a row or a cell.



---

# tbl_hline_rulelist

# tbl_hline_rulelist

count = tbl_hline_rulelist ( gridId , y , x1 , x2 , array )

This function fills array with the IDs of the rules occupying the horizontal line identified by the coordinates y , x1 , and x2 in grid gridId ordered from left to right and returns the number of IDs.



---

# tbl_insert

# tbl_insert

id = tbl_insert ( tmid , oid , pos , rows , cols , [tagname] )

This function inserts a new table, specified by table model tmid , with rows rows and cols columns, into the document at the point indicated by oid and pos . If tmid is zero (0), then the primary table model for the document type will be used.

tagname is only used by document types that use wrappers. Some document types allow several different tags to serve as the wrapper tag surrounding a table. tagname is used to specify a wrapper tag; if tagname is omitted, the outer wrapper tag is chosen at random.

For custom tables, the cols value is ignored.

It returns the ID of the newly-inserted table set if successful, h::tblNullToid otherwise.

The tbl_insert function will not do a pending delete regardless of the setting of set pendingdelete .



---

# tbl_insert_rows_cols_dlg

# tbl_insert_rows_cols_dlg

[0|1] = tbl_insert_rows_cols_dlg ( [win] )

This function displays the Insert Rows and Columns dialog box, which attempts to insert a user-specified number of rows and columns at the cursor in the document shown in window win (or in the active window if win is omitted). It returns 0 if no table is active. It returns 1 on success.

## Related Topics

- • Insert Rows and Columns dialog box



---

# tbl_insert_table_dlg

# tbl_insert_table_dlg

[0|1] = tbl_insert_table_dlg ( [win] )

This function displays the Select a Table Model dialog box in which you can choose a table model if the following conditions are true:

- • If your document type supports multiple table models.

- • set prompttablemodels is set to on .

- • The cursor is in a location in which it is valid to insert more than one table model.

Once you have chosen a table model, or, if your DTD doesn't support multiple table models, the Insert Table dialog box opens, in which you can specify table configuration options.

The function then attempts to insert the table at the cursor location in the document shown in window win (or in the active window if win is omitted).

The function returns 0 if a table cannot be inserted at the cursor location. It returns 1 if a table is inserted.

## Related Topics

- • set prompttablemodels

- • tblmodelprompthook

- • tbl_model_prompt callback type



---

# tbl_insertion_valid

# tbl_insertion_valid

[0|1} = tbl_insertion_valid ([ doc ])

This function returns 1 if a table can be inserted at the cursor point in document doc (or in the active document if doc is omitted).

If context checking is turned off, this function returns 1 regardless of where the cursor is located in the document. If set autotaginserts is set to on , this function returns 1 if the cursor is at a point in the document where a tag can be automatically inserted that would then make the insertion of a table valid.



---

# tbl_mod_borders_dlg

# tbl_mod_borders_dlg

[0|1] = tbl_mod_borders_dlg ( [win] )

This function displays the Table Properties dialog box and attempts to modify the borders of the active table in window win (or in the active window if win is omitted). It returns 0 if the window contains no active table. It returns 1 on success.

## Related Topics

- • Table Properties dialog box



---

# tbl_mod_cellfont_dlg

# tbl_mod_cellfont_dlg

[0|1] = tbl_mod_cellfont_dlg ( [win] )

This function displays the Font dialog box and attempts to modify the cell font of the active table in window win (or in the active window if win is omitted). It returns 0 if the window contains no active table. It returns 1 on success.

## Related Topics

- • Modify Font dialog box



---

# tbl_mod_cells_dlg

# tbl_mod_cells_dlg

[0|1] = tbl_mod_cells_dlg ( [win] )

This function displays the Table Properties dialog box and attempts to modify the cell attributes of the active table in window win (or in the active window if win is omitted). It returns 0 if the window contains no active table. It returns 1 on success.

## Related Topics

- • Table Properties dialog box



---

# tbl_mod_table_dlg

# tbl_mod_table_dlg

[0|1] = tbl_mod_table_dlg ( [win] )

This function displays the Table Properties dialog box and attempts to modify the table attributes of the active table in window win (or in the active window if win is omitted). It returns 0 if the window contains no active table. It returns 1 on success.

## Related Topics

- • Table Properties dialog box



---

# tbl_model_celllist

# tbl_model_celllist

count = tbl_model_celllist ( tmid , array , [hdr] )

This function fills array with the names of the cell tags used in the table model whose ID is tmid . If hdr is supplied and is non-zero, then the names of the header cell tags will be returned in array .

If tmid is invalid, the function returns a zero (0); otherwise, it returns the number of cells tags in array .

## Related Topics

- • tbl_model_row

- • tbl_model_table_title

- • tbl_model_tablelist



---

# tbl_model_id

# tbl_model_id

tmid = tbl_model_id ( name [, doc ])

This function returns the table model ID (tmid) corresponding to the table model name ( OASIS Exchange , ATI , or HTML ) for the document specified by doc . If doc is omitted or 0, the current document is used.

If name is a null string, the primary table model configured for the document is used.

The tbl_model_id function returns -1 if no tables are configured for the document.

## Related Topics

- • tbl_model_name built-in function



---

# tbl_model_list

# tbl_model_list

count = tbl_model_list ( array , [doc] )

This function fills array with the IDs of the table models valid for document doc (or for the active document if doc is omitted) and returns the number of IDs. It returns 0 if doc is invalid or if doc has no table models.



---

# tbl_model_name

# tbl_model_name

return = tbl_model_name ( tmid )

This function returns the name of the table whose table model ID is indicated by tmid . The table model name may be one of: “OASIS Exchange,” “ATI,” “HTML”, “XSL-FO”, or if the table is a custom table, the name specified in the document type configuration file (.dcf) from the attribute name on the element CustomTableModel .

If tmid is invalid, the function returns the string ”unknown”.



---

# tbl_model_operation

# tbl_model_operation

result = tbl_model_operation ( opcode , toid , ... )

This function requests a table-model-specific function. The parameters and result value are determined by the operation requested by opcode .

- • All operations are supported for tables managed by the OASIS Exchange table model.

- • No operations are supported for tables managed by the HTML, XSL-FO, or PTC Arbortext table models.

toid specifies different items based on the value of opcode . opcode can be 0 , 1 , 2 , 3 , 4 , or 5 .

- • If opcode is 0 , all colspec tags within thead or tfoot tags are deleted, and every entry tag in the table is adjusted to refer to the colspec tags that are children of the tgroup tag.

- • If opcode is 1 , Arbortext Editor deletes spanspec tags and updates entry tags to refer to colspec tags. If the document type does not allow namest or nameend attributes on entry tags, tbl_model_operation does nothing.

- • If opcode is 2 , Arbortext Editor updates the colname attribute of every colspec tag in a table.

- • If opcode is 3 , Arbortext Editor scans a table and reorganizes the attributes of the various table tags to minimize the number of attributes required to describe the table.

- • If opcode is 4 , Arbortext Editor renames a single colspec tag by updating the tag's colname attribute and adjusting all spanspec and entry tags to refer to the colspec by its the new value for the colname attribute.

- • If opcode is 5 , Arbortext Editor renames a single spanspec tag by adjusting the tag's spanname attribute and modifying every entry tag that refers to it.



---

# tbl_model_row

# tbl_model_row

tagname = tbl_model_row ( tmid , [hdr] )

This function returns the tag name of the row tag used in the table whose table model ID is tmid . If hdr is supplied and is non-zero, then the name of the header row tag, if it exists, is returned instead.

If tmid is invalid or hdr is specified and there is no header row, then, the function returns an empty string.

## Related Topics

- • tbl_model_celllist

- • tbl_model_table_title

- • tbl_model_tablelist



---

# tbl_model_support

# tbl_model_support

ret = tbl_model_support ( tmid , opcode )

This function returns 1 if the given table model id ( tmid ) supports the feature specified by the opcode . If it does not or if either parameter is invalid, the function returns a zero (0).

Valid opcode values are:

- • 0 – multiple table grids in a single table set

- • 1 – header rows

- • 2 – footer rows

- • 3 – background color on cells

- • 4 – an attribute to set frame property

- • 5 – attributes to set cell spacing and cell padding



---

# tbl_model_table_title

# tbl_model_table_title

tagname = tbl_model_table_title ( tmid )

This function returns the tag name of the title or caption tag used in the table model whose ID is tmid .

If tmid is invalid, the function returns an empty string.

## Related Topics

- • tbl_model_celllist

- • tbl_model_row

- • tbl_model_tablelist



---

# tbl_model_tablelist

# tbl_model_tablelist

count = tbl_model_tablelist ( tmid , array )

This function fills array with the names of the table root tags used in the table model whose ID is tmid . The root tag is the grid tag for the table.

If tmid is invalid, the function returns a zero (0); otherwise, it returns the number of tags in array .

## Related Topics

- • tbl_model_celllist

- • tbl_model_row

- • tbl_model_table_title



---

# tbl_model_taglist

# tbl_model_taglist

count = tbl_model_taglist ( tmid , array )

This function fills array with the names of all the table tags used in the table model tmid , and returns the number of tags inserted in the array. If tmid is invalid, the function returns a zero (0).

This function does not return table wrapper tags; these are retrieved by the tbl_model_wrapperlist function.



---

# tbl_model_wrapperlist

# tbl_model_wrapperlist

count = tbl_model_wrapperlist ( tmid , array )

This function fills array with the names of the wrapper tags used in the table model tmid , and returns the number of tags inserted in the array. If tmid is invalid, the function returns a zero (0).



---

# tbl_multicell_border

# tbl_multicell_border

count = tbl_multicell_border ( cellId , direction , outArray )

This function fills outArray with the ID of each rule on side direction of multicell cellId sorted from top to bottom or left to right and returns the number of IDs.



---

# tbl_multicell_celllist

# tbl_multicell_celllist

count = tbl_multicell_celllist ( cellId , array )

This function fills array with the ID of each cell in multicell cellId sorted into row-major order and returns the number of IDs.



---

# tbl_multicell_neighborlist

# tbl_multicell_neighborlist

count = tbl_multicell_neighborlist ( cellId , whichSide , outArray )

This function fills outArray with the ID of each cell adjacent to edge whichSide of multicell cellId and returns the number of values placed in array . The cell IDs are returned in row-major order.



---

# tbl_multicell_size

# tbl_multicell_size

[0|2] = tbl_multicell_size ( cellId , array )

This function returns the number of rows and columns occupied by multicell cellId in the output array . The first array element contains the row count, and the second array element contains the cell count. The function returns a value of 0 if the cell is either not in a multicell or the cellId is invalid. Otherwise, the function returns a value of 2 .

The following example returns the number of rows or cells spanned by a given cell based on its oid . Note that this example might be used by a FOSI system-func call, so the window argument is required but not used.

```
function row_count(window,oid) {
return span_count($window,$oid,1);
}
function col_count(window,oid) {
return span_count($window,$oid,0);
}
function span_count(window,oid,rowchk) {
local rowcount;
local colcount;
local size[];
if (!tbl_cell_in_multicell(tbl_oid_cell($oid))) {
return 1;
}
tbl_multicell_size(tbl_oid_cell($oid), size);
rowcount = size[1];
colcount = size[2];
if ($rowchk == 1) {
return rowcount;
} else {
return colcount;
}
}
```



---

# tbl_multicell_spanner

# tbl_multicell_spanner

cellId = tbl_multicell_spanner ( cellId )

Returns the cell ID of the spanning cell of multicell cellId . cellId may indicate any cell in the multicell.



---

# tbl_obj_add

# tbl_obj_add

toId = tbl_obj_add ( toId , addBefore , [tagname] )



This function inserts a new row or column, of the same type as table object toid , before or after toid as indicated by a nonzero value in addBefore . It returns the ID of the newly-inserted row or column.

For custom tables, when multiple elements are acceptable to be used as the row element, if the tagname parameter is supplied, then the tagname element is inserted.



---

# tbl_obj_attr_clear

# tbl_obj_attr_clear

[0|1] = tbl_obj_attr_clear ( toid )

This function deletes all of table object toid 's attribute values by resetting the table markup attributes from which they're derived to default values.

If toid is invalid, the function returns a zero ( 0 ). If the function executes successfully, it returns a one ( 1 ).

The toid parameter is the table object ID of the table object whose attributes are to be cleared.

## Related Topics

- • Table object attributes

- • Shared table attributes

- • Set table attributes

- • Grid table attributes

- • Column table attributes

- • Row table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_delete

- • tbl_obj_attr_get

- • tbl_obj_attr_set



---

# tbl_obj_attr_delete

# tbl_obj_attr_delete

[0|1] = tbl_obj_attr_delete ( toid , attrName )



This function deletes table object attribute attrName from table object toid by resetting the markup from which the attribute was derived to a default value.

If toid or attrName is invalid, the function returns a zero ( 0 ). If the function executes successfully, it returns a one ( 1 ).

The toid parameter is the table object ID of the table object whose attribute value is to be deleted. The attrName parameter is a string for the name of the attribute. Note that names are case insensitive.

## Related Topics

- • Table object attributes

- • Shared table attributes

- • Set table attributes

- • Grid table attributes

- • Column table attributes

- • Row table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_get

- • tbl_obj_attr_set



---

# tbl_obj_attr_get

# tbl_obj_attr_get

[0|1] = tbl_obj_attr_get ( toid , attrName , attrval )



This function places the value of table object attribute attrName for table object toid in attrval .

If toid or attrName is invalid, the function returns a zero ( 0 ). If the function executes successfully, it returns a one ( 1 ).

The toid parameter is the table object ID of the table object whose attribute value is to be retrieved. The attrName parameter is a string for the name of the attribute. Note that names are case insensitive. The attrval parameter is a variable in which the attribute value is returned. Some values are numbers, some are strings. String values are case insensitive.

## Related Topics

- • Table object attributes

- • Shared table attributes

- • Set table attributes

- • Grid table attributes

- • Column table attributes

- • Row table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_set



---

# tbl_obj_attr_set

# tbl_obj_attr_set

[0|1] = tbl_obj_attr_set ( toid , attrName , attrval )

This function sets table object attribute attrName for table object toid to attrval .

If toid or attrName is invalid, the function returns a zero ( 0 ). If the function executes successfully, it returns a one ( 1 ).

The toid parameter is the table object ID of the table object whose attribute value is to be set. The parameter is a string for the name of the attribute. Note that names are case insensitive. The attrval parameter is the new value for the attribute attrName . Some values are numbers, some are strings. String values are case insensitive.

## Related Topics

- • Table object attributes

- • Shared table attributes

- • Set table attributes

- • Grid table attributes

- • Column table attributes

- • Row table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_get



---

# tbl_obj_attr_valid

# tbl_obj_attr_valid

[0|1] = tbl_obj_attr_valid ( toid , attrName [, attrval ])

This function determines if setting table object attribute attrName for table object toid is valid or if setting table object attribute attrName for table object toid to attrval is valid.

If toid or attrName is invalid, or setting the table object attribute is not valid, tbl_obj_attr_valid returns zero ( 0 ). If setting the table object attribute is valid, tbl_obj_attr_valid returns one ( 1 ).

- • toid — The table object ID of the table object whose attribute value is to be set.

- • attrName — A string for the name of the attribute. Names are case insensitive.

- • attrval — Optional. The new value for the attribute attrName . Values are numbers or strings. String values are case insensitive. If attrval is not supplied, the function tests whether the table model supports setting the attrName table object attribute at all. If attrval is supplied, then the function is testing whether the table model supports setting the attrName table object attribute to the specific value.

## Related Topics

- • tbl_obj_attr_set function



---

# tbl_obj_delete

# tbl_obj_delete

[0|1] = tbl_obj_delete ( toId )

This function deletes table object toid from its document. toid may indicate a table set, a grid, a row, or a column.



---

# tbl_obj_grid

# tbl_obj_grid

gridId = tbl_obj_grid ( toId )

This function returns the ID of the grid containing table object toId .



---

# tbl_obj_insert

# tbl_obj_insert

[0|1] = tbl_obj_insert ( ulSourceCellId , lrSourceCellId , targetToid , addBefore )

This function inserts a new grid, row rectangle, or column rectangle into an existing set or grid and copies the contents of the source rectangle into the new one. The source rectangle is defined by upper-left corner cell ulSourceCellId and lower-right corner cell lrSourceCellId ; the target grid, row, or column is identified by targetToid . The width or height of the source rectangle must specify one or more complete rows or columns if targetToid is a row or a column.



---

# tbl_obj_mark

# tbl_obj_mark

[0|1] = tbl_obj_mark ( toId , newRegion , primarySelection , doInvert )

This function begins or ends a mark operation on a rectangle of table objects.

toId : the table object id of the table object to start or end the mark on.

newRegion : [0|1]. If non-zero, start a separate table object selection. Only relevant on 3rd and successive odd numbered calls to tbl_obj_mark .

primary : may be 1, 0, or -1, to set, clear, or leave alone the primary selection.

doInvert : [0|1]. If non-zero, invert the selection in all views.

This function implements a finite state machine with three states: empty, marking, and bound. We start empty; the first call to tbl_obj_mark saves toid as the selection anchor and changes state to marking . The second call to tbl_obj_mark saves toid as the selection endpoint and changes state to bound .

A third call to tbl_obj_mark discards the previous endpoint and switches back to marking state; a fourth call switches back to bound .

Issuing the clear_mark command is the only way to get back to empty state.

If our state is marking or bound , we know two points: the anchor and the endpoint . Unless these two points are identical, we can invert the display region between them to clue the user in about what's marked.

tbl_obj_mark allows discontiguous rectangles of table objects to be selected. We handle discontiguity by checking for the newRegion flag on odd-numbered calls (state == empty or state == bound) and pushing the anchor and end points onto a stack before starting a new mark operation.

While our state is marking , the user may adjust the region endpoint by calling tbl_obj_markdrag ; the state stays at marking , but the point (and hence the inverted region) changes.

Note that calling tbj_obj_mark will clear any text selection, and that selecting text will clear any table object selection.

Note that invoking the mark command also forces a state transition.

Returns 1 if successful. 0 (indicating failure) is returned when TOId doesn't identify a valid table object.



---

# tbl_obj_markdrag

# tbl_obj_markdrag

[0|1] = tbl_obj_markdrag ( toId )

This function changes the endpoint of the currently-active selection rectangle to table object toid . It returns 1 if a table selection was defined and its endpoint successfully changed.



---

# tbl_obj_marked

# tbl_obj_marked

[0|1] = tbl_obj_marked ( toId )

This function returns 1 if table object toid is selected (that is included in the selection object belonging to its document).



---

# tbl_obj_modifiable

# tbl_obj_modifiable

[0|1] = tbl_obj_modifiable ( toId )

This function returns 1 if table object toid is unprotected.



---

# tbl_obj_set

# tbl_obj_set

setId = tbl_obj_set ( toId )

This function returns the id of the table set that contains table object toId .



---

# tbl_obj_type

# tbl_obj_type

objectType = tbl_obj_type ( toId )

This function returns the object type of table object toId .



---

# tbl_obj_valid

# tbl_obj_valid

[0|1] = tbl_obj_valid ( toId )

This function returns 1 if table object toId is valid.



---

# tbl_obj_viewimage

# tbl_obj_viewimage

[0|1] = tbl_obj_viewimage ( id , [win] )

This function returns 1 if table object id is part of a table image in window win (or in the active window, if win is omitted).



---

# tbl_oid_cell

# tbl_oid_cell

id = tbl_oid_cell ( oid , [pos] )

This function returns the ID of the cell containing the point indicated by oid and pos . If the point is not in a table cell, it returns h::tblNullToid .



---

# tbl_oid_nodelete

# tbl_oid_nodelete

[0|1] = tbl_oid_nodelete ( oid )

This function returns 1 if the table model managing the tag indicated by oid should be protected from deletion. This allows GUI elements to delete the content of a cell without deleting PIs and other things that a table model might care about.



---

# tbl_oid_object

# tbl_oid_object

toid = tbl_oid_object ( oid , [pos] )

This function returns the toid of the deepest table object (a cell, row, grid, or set) that fully contains the specified oid and optional parameter pos . If the specified combination of oid and pos is not inside table markup, the function returns h::tblNullToid .



---

# tbl_oid_viewimage

# tbl_oid_viewimage

[0|1] = tbl_oid_viewimage ( oid , [win] )

This function returns 1 if oid is contained in a table that is displayed as an image (instead of as tags) in window win (or in the active window if win is omitted.



---

# tbl_row_cell

# tbl_row_cell

cellId = tbl_row_cell ( rowId , index )

This function returns the ID of cell index in row rowId . The leftmost cell in a row has an index of 1.



---

# tbl_row_celllist

# tbl_row_celllist

count = tbl_row_celllist ( rowId , array )

This function fills array with the IDs of the cells in row rowId ordered from left to right and returns the number of IDs.



---

# tbl_row_count

# tbl_row_count

count = tbl_row_count ([ oid ])

This function returns the number of rows in the table image given by object identifier oid . If oid is omitted, it returns the number of rows in the table containing the cursor. Returns —1 if the cursor is not inside a table.

## Related Topics

- • insert built-in function

- • insert_column command

- • insert_row command

- • goto_cell built-in function

- • tbl_caret_col built-in function

- • tbl_caret_row built-in function

- • tbl_col_count built-in function



---

# tbl_row_index

# tbl_row_index

index = tbl_row_index ( rowId )

This function returns the index of row rowId relative to the top row in the containing grid. The uppermost row in a grid has an index of 1.



---

# tbl_row_neighbor

# tbl_row_neighbor

rowId = tbl_row_neighbor ( rowId , offset )

This function returns the ID of the row offset rows above ( offset <0) or below ( offset >0) row rowId .



---

# tbl_row_rulelist

# tbl_row_rulelist

count = tbl_row_rulelist ( rowId , direction , array )

This function fills array with the IDs of the rules in row rowId in direction direction . The IDs are ordered from left to right. It returns the number of IDs.



---

# tbl_rowtool_mouse

# tbl_rowtool_mouse

rowId = tbl_rowtool_mouse ( viewid )

This function returns the ID of the row in the active grid in view vidId (or the active view, if viewId is omitted) that contains the mouse pointer.



---

# tbl_rule_cellneighbor

# tbl_rule_cellneighbor

cellId = tbl_rule_cellneighbor ( ruleId , direction )

This function returns the ID of the cell bordering rule ruleId on side direction .



---

# tbl_rule_is_suppressed

# tbl_rule_is_suppressed

[0|1] = tbl_rule_is_suppressed ( ruleId )

This function returns 1 if rule ruleId is suppressed because it is inside a multicell.



---

# tbl_rule_orientation

# tbl_rule_orientation

orientation = tbl_rule_orientation ( ruleId )

This function returns the orientation of rule ruleId .



---

# tbl_rule_ruleneighbor

# tbl_rule_ruleneighbor

ruleId = tbl_rule_ruleneighbor ( ruleId , direction , offset )

This function returns the ID of the rule offset cells away from rule ruleId in direction direction .



---

# tbl_rule_vertices

# tbl_rule_vertices

[0|1] = tbl_rule_vertices ( ruleId , startColIndex , startRowIndex , endColIndex , endRowIndex )

This function places the coordinates of the start and end points of rule ruleId in the output variables startColIndex , startRowIndex , endColIndex and endRowIndex .



---

# tbl_selection_clone

# tbl_selection_clone

id = tbl_selection_clone ( selectionId )

This function returns the ID of a new table selection object that contains the same table object IDs as table selection object selectionId . The user is responsible for freeing the object by calling tbl_obj_delete .

This routine can be used in conjunction with tbl_selection_restore and in circumstances where executing some ACL command would result in prematurely clearing a document's table object selector.



---

# tbl_selection_empty

# tbl_selection_empty

[0|1] = tbl_selection_empty ( selectionId )

This function returns 1 if the table selection object selectionId contains no table object IDs.



---

# tbl_selection_get

# tbl_selection_get

id = tbl_selection_get ( [doc] )

This function returns the ID of the selection object used to manage table selections in the indicated document (or in the active document if doc is omitted).



---

# tbl_selection_matchbegin

# tbl_selection_matchbegin

[0|1] = tbl_selection_matchbegin ( selectionId , wantSets , wantGrids , wantColumns , wantRows , wantCells , wantRules , contiguous , preferColumns )

This function organizes the contents of selection object selectionId and prepares for subsequent calls to tbl_selection_matchnext . A selection object contains a series of rectangles, each of which might cover an entire grid, one or more entire rows or columns, or simply a smaller area within a single grid. At different times, it may be advantageous to iteratively examine every cell in every rectangle; at others, a user might want to require ensure that only complete rows are selected, and iteratively process each row. tbl_selection_matchbegin supports all such possibilities by analyzing the selection object and organizing the rectangles it contains into the largest requested units. It returns '0' if the selection object contains a rectangle that can't be so organized, and '1' if the selection object contains rectangles that can be interpreted as the user indicates. In the latter case, calls to tbl_selection_matchnext can be used to retrieve the interpreted table objects.



---

# tbl_selection_matchnext

# tbl_selection_matchnext

toid = tbl_selection_matchnext ( selectionId )

This function supports iteration over the contents of selection object selectionId by returning the Table Object ID (toid) of the next table object matching the search criteria specified on the most recent call to tbl_selection_matchbegin . If this function is used immediately after a call to tbl_selection_matchbegin , it will find the first match (that is, the match found by tbl_selection_matchbegin ). A subsequent call to this function will find the next match.

If there is no such object, it returns the value of h::tblNullToid .

This function searches for Table Object IDs per the following rules:

- • Row, column, and cell toids from a single rectangle are returned in row-major order.

- • Rule toids are returned in row major order.

- • Set toids are returned in no particular order.



---

# tbl_selection_nextrectangle

# tbl_selection_nextrectangle

[0|1] = tbl_selection_nextrectangle ( selectionId , startFlag , ulCellId , lrCellId )

This function iterates over the contents of selection object selectionId , returning in the output variables ulCellId and lrCellId the Cell IDs of the upper-left and lower-right corners of the first or next rectangle ( startFlag = 1 or 0, respectively) within. It returns '0' if there is no first or next rectangle, '1' otherwise.



---

# tbl_selection_pasterectangle

# tbl_selection_pasterectangle

[0|1] = tbl_selection_pasterectangle ( selectionId )

This function returns '1' if the selection object indicated by selectionId contains TOIds that describe a single rectangle.

The rectangle of cells identified this way is suitable for use as the target of a paste operation.



---

# tbl_selection_pastetype

# tbl_selection_pastetype

type = tbl_selection_pastetype ( selectionId , targetId )

This function indicates whether pasting the table objects whose IDs are contained in selection object selectionId into the destination cell, row, column, or grid indicated by targetId will replace an entire grid, one or more entire rows, one or more entire columns, or just a rectangle of cells.

This routine returns h::tblTypeUndef (undefined type) if either parameter is invalid, if the selection object doesn't contain TOIds describing a single rectangle, or if the targetId indicates a table object not contained in a grid.



---

# tbl_selection_restore

# tbl_selection_restore

[0|1] = tbl_selection_restore ( selectionId )

This function selects the table objects whose IDs are contained by the selection object selectionId .



---

# tbl_selection_tmid

# tbl_selection_tmid

tmid = tbl_selection_tmid ( selectionId )

This function returns the ID of the table model responsible for managing the table objects whose IDs are contained in selection object selectionId .



---

# tbl_selection_valid

# tbl_selection_valid

[0|1] = tbl_selection_valid ( selectionId )

This function returns 1 if all of the table object IDs in selection object selectionId are valid.



---

# tbl_set_first_galley_cell

# tbl_set_first_galley_cell

toid = tbl_set_first_galley_cell ( SetId )

This function returns the ID of the first cell in set setid in galley order.



---

# tbl_set_grid

# tbl_set_grid

gridId = tbl_set_grid ( setId , gridIndex )

This function returns the ID of grid number gridIndex in set setId . The first grid in a set is grid number 1.



---

# tbl_set_gridlist

# tbl_set_gridlist

count = tbl_set_gridlist ( setId , array )

This function fills array with the IDs of each grid in set setId and returns the number of IDs.



---

# tbl_set_last_galley_cell

# tbl_set_last_galley_cell

toid = tbl_set_last_galley_cell ( setId )

This function returns the ID of the last cell in set setId in galley order.



---

# tbl_table_title_delete

# tbl_table_title_delete

[0|1] = tbl_table_title_delete ( toidId )

This function deletes the table title (caption) from the table containing toidId . The function returns 1 if a table title existed and was deleted. Otherwise, tbl_table_title_delete returns 0 .



---

# tbl_table_title_insert

# tbl_table_title_insert

oid = tbl_table_title_insert ( toidId [, str ])

This function inserts the table title (caption) str into the table containing toidId . The function returns the oid of the new table title if one was inserted, or it returns the oid of a previously existing table title. If the table's table model does not allow table titles or the insert otherwise fails, the function returns null_oid .

The HTML table model supports table titles with the caption element. Custom table models may be configured to support table titles. The CALS and Arbortext table models do not support table titles.



---

# tbl_vline_rulelist

# tbl_vline_rulelist

count = tbl_vline_rulelist ( gridId , x , y1 , y2 , array )

This function fills array with the IDs of the rules that occupy the vertical line identified by the coordinates x , y1 , and y2 in grid gridId and returns the number of IDs.



---

# tell

# tell

offset = tell ( fid )

This function returns the offset of the current byte relative to the beginning of the file associated with the identifier fid , which must be a return value from a previous call to open .

tell returns -1 on failure, for example, if fid is not a valid file identifier.



---

# temp_name

# temp_name

$tempfile = temp_name ( name [, ext [, dir ]])

This function creates a new temporary log file. The name parameter specifies the base name for the file. The optional ext parameter specifies the extension to use for the file name. If the ext parameter is omitted, it defaults to .log .

The optional dir parameter specifies the where to store the new temporary file. If the dir parameter is omitted, it defaults to the value of the environment variable TMPDIR . If TMPDIR , is not set, it defaults to the c:\temp directory.

The return value is the name of the newly created temp file. Note that this function will automatically append a number (1 to 99) to the end of the base file name as necessary to avoid duplicate file names.

Be aware that another process could feasibly create a file with the same name in the time between when this function is called and when the file is actually created.



---

# terminal_mode

# terminal_mode

[0|1] = terminal_mode ([ flags ])

This function determines whether windows are available in Arbortext Editor . If the type is not supplied or is 0 , this function returns 1 if windows are not available or 0 if windows are available. Windows are not available if Arbortext Editor is run in -c (command) mode or -S (server) mode. To test for a specific non windows mode, then type should be set to 2 for -c (command) mode or 3 for -S (server) mode.



---

# text_entity_names

# text_entity_names

count = text_entity_names ( arr [, doc ])

The text_entity_names function fills the array arr with an alphabetical list of text entity names which are valid for the current document, returning the total number. The first name returned is stored at index 1. All previous elements in arr are discarded.

The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# text_entity_tag

# text_entity_tag

[0|1] = text_entity_tag ( tagname [, doc ])

This function returns 1 (True) if the tag specified by the expression tagname is really a tag used to represent an SGML text entity declaration. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# text_style_tag_name

# text_style_tag_name

tagname = text_style_tag_name ( style , arr [, doc ])

This function returns the name of the primary element for the given style specified in the document type configuration file ( .dcf ) for the document type associated with doc . Valid style values are bold , italic , and underline .

If a tag name is returned, text_style_tag_name function returns arr with an attribute name and attribute value, if they were specified for the tag in the .dcf file.

The function returns the null string if there is no element defined for the specified style , or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

For example,

```
local tag, arr[];
local attr, val;
tag = text_style_tag_name("bold", arr);
attr = arr['attribute'];
val = arr['attribute_value'];
```

## Related Topics

- • Document type configuration files

- • Configuring Tags as Text Style Elements

- • text_style_tag_name_ns function

- • set toolbar4 command



---

# text_style_tag_name_ns

# text_style_tag_name_ns

tagname = text_style_tag_name_ns ( style , arr [, doc ])

This function returns the namespace URI prefixed to the primary element for the given style specified in the document type configuration file ( .dcf ) for the document type associated with doc . Valid style values are bold , italic , and underline .

If a tag name is returned, text_style_tag_name_ns function returns arr .

The function returns the null string if there isn’t a namespace prefix, if no element is defined for the specified style , or if doc is invalid or an ASCII file. If doc is omitted or 0 , the current document is used.

## Related Topics

- • Document type configuration files

- • Configuring tags as text style elements

- • text_style_tag_name function

- • set toolbar4 command



---

# thesaurus

# thesaurus

thesaurus ([ doReplace [, word ]])

This function opens the Thesaurus dialog box , using the selected word in the active document as the default value of word . If no word is selected, the word nearest to the cursor is used.

The function looks up word in the Looked Up: box. If doReplace is set to a non-zero value (or is not specified), clicking Replace on the dialog box will substitute the preferred word. If doReplace is set to zero ( 0 ), clicking Replace will close the dialog box without performing a word replacement.



---

# throw

# throw

throw ( expr )

This function transfers control by returning from the innermost active catch function. The value of the expression expr becomes the return value from catch . expr must not evaluate to zero; if it does, 1 is used instead.

If throw is used outside the context of a catch , control is transferred to the top level, aborting the command execution.

## Related Topics

- • catch built-in function



---

# time_(Function)

# time (Function)

seconds = time ()

This function returns the current time in seconds since the epoch, which is operating system-specific. This time can be converted into a string for display using the ctime function.

Example

```
ctime(time())
```

is equivalent to

```
time_date()
```

## Related Topics

- • ctime built-in function



---

# time_date

# time_date

string = time_date ([ gmt ])

This function returns the current time as a string in the following format:

```
Mon Dec 28 17:23:52 1992
```

All the fields have constant width.

The argument gmt is optional. If non-zero, the time returned is in GMT. The local time is returned if the argument is omitted or zero. Note that the string returned does not include time zone information.



---

# times

# times

time = times ([ arr ])

The times function fills the array arr with four elements giving the user and system CPU times, in 1/100th seconds, for this process and the children of this process. It returns the sum of arr [1] and arr [2], that is, the total user and system time for the process. If arr is not given, then only the total time is returned. For example, to time a section of Arbortext Command Language code:

```
times($t1)
# whatever code here
times($t2)
$tdiff = $t2[1] - $t1[1]
eval "user time:", $tdiff/100 . '.' . $tdiff%100
$tdiff = $t2[2] - $t1[2]
eval "system time:", $tdiff/100 . '.' . $tdiff%100
```



---

# tolower

# tolower

string = tolower ( string )

This function returns the string specified by string with all letters converted to lowercase.



---

# toupper

# toupper

string = toupper ( string )

This function returns the string specified by string with all letters converted to uppercase.



---

# treeloc_oid

# treeloc_oid

oid = treeloc_oid ( treeloc [, sep_char [, top_level_oid ]])

This function returns the oid in the current document of the tag specified by treeloc .

Specify a separator character sep_char to delineate the values in the string with a character other than “,”, which is the default.

To limit the size of the returned value, specify a top_level_oid . This sets the parent tag at which the oid will begin. If you do not specify a top_level_oid , the first value in the returned string represents the first tag in the document.



---

# trim

# trim

string = trim ( string )

This function returns the string specified by string with leading and trailing white space removed.



---

# truncate

# truncate

[0|–1] = truncate ( fid , length )

This function sets the size of the file identified by fid to length bytes. fid must refer to a file that was opened for writing. If the file is currently larger than length , the extra bytes are removed. If the file is shorter, then zero bytes are added. The function returns 0 on success or -1 on failure.



---

# ucstombs

# ucstombs

return = ucstombs ( str [, charset ])

This function converts the Unicode string str to a byte string in the specified character charset, which may be a multi-byte character set. charset is one of the character sets listed in the description of mblen . If charset is not specified, the system character set is assumed.

Because the resulting string is a byte string, not all string operations are appropriate. The result would normally be written to a binary file or network channel. See the example with mbstoucs .

Example

```
write(ch, ucstombs("get toc.htm\r\n", "iso8859-1"))
```



---

# umask

# umask

mask = umask ([ newmask ])



This function sets the process's file creation mask to newmask and returns the previous value of the mask. newmask will affect all files created subsequently by Arbortext Editor , and will be inherited by any processes it spawns. If newmask is omitted, umask just returns the current mask.



---

# undeclare_ms_parameter

# undeclare_ms_parameter

undeclare_ms_parameter ( entity )

This function allows you to remove a marked section parameter entity declaration.

entity is the name of an existing marked section parameter entity that isn't referenced in the document.



---

# undo_menu_description

# undo_menu_description

[0|1] = undo_menu_description ( label [, doc ])

This function assigns label as the menu label for the next undoable operation on document doc . If doc is not specified, the value of current_doc is used.

If this function is called multiple times during a single undoable operation, only the label from the first call is used. Subsequent calls are ignored. The function returns a one (1) if the label will be used, or zero (0) if the call is ignored. To clear a label set by a previous call, see the undo_menu_description_clear function.

An example follows:

```
local undoMsg = undo_menu_description("Great Operation", doc);
...
local ret = great_operation_action(...);
# If the above failed so doc was not modified, then clear the
# undo label (if not, it will be applied to the next operation)
if ((! ret) && undoMsg) {
undo_menu_description_clear(doc);
}
```



---

# undo_menu_description_clear

# undo_menu_description_clear

[0|1] = undo_menu_description_clear ([ doc ])

This function clears the menu label for the next undoable operation on document doc . If doc is not specified, the value of current_doc is used. This function should only be called to clear a label set by a previous call to undo_menu_description .

This function returns 1 if the undo menu label was cleared.

An example follows:

```
local undoMsg = undo_menu_description("Great Operation", doc);
...
local ret = great_operation_action(...);
# If the above failed so doc was not modified, then clear the
# undo label (if not, it will be applied to the next operation)
if ((! ret) && undoMsg) {
undo_menu_description_clear(doc);
}
```

## Related topic

- • tbl_edit_open function



---

# unicode_to_entity

# unicode_to_entity

name = unicode_to_entity ( unicodenumber [, doc ])

Provided the Unicode character number unicodenumber , this function returns the equivalent character entity name. For example, if you were to give unicodenumber the value of 920 , the function would return the value 'Theta' .

If the doc parameter is not provided, the current document will be used.

If there is no character entity name for the unicode character number unicodenumber , the function returns an empty string.

Note that the returned character entity names are case-sensitive and depend on the document type you are using. Use the Arbortext-path /lib/charent.cf file a reference to character entity names.

## Related Topics

- • entity_to_unicode function



---

# universal_file_name

# universal_file_name

string = universal_file_name ( path )

This function returns the universal naming convention (UNC) name for the drive-based network path name path . The path parameter should refer to a remote file system that has been mounted as a local drive or a drive mapped using the Windows subst command. If path is not a network path, the absolute file name, possibly drive-based, is returned.

Example

```
$ret = universal_file_name('f:\users\george')
```

## Related Topics

- • absolute_file_name function



---

# unpack

# unpack

count = unpack ( template , expr [, arr ])

This function does the reverse of pack — it unpacks the binary data structure expr into the array arr , returning the number of elements stored in the array. If arr is omitted, then unpack extracts a single value and returns it instead.

This is similar to the Perl function of the same name. template has the same format as pack and is a sequence of characters that specify the type of each value, as follows:

- • a — an ASCII string, unstripped

- • A — an ASCII string, with trailing nulls and spaces removed

- • c — a signed 8–bit character value

- • C — an unsigned 8–bit character value

- • d — a double-precision floating point number in native format

- • f — a single-precision floating point number in native format

- • i — a signed integer (32–bit) value

- • I — an unsigned integer (32–bit) value

- • l — a signed long value

- • L — an unsigned long value

- • n — a short integer value in network (big-endian) order

- • N — a long (32–bit) value in network (big-endian) order

- • p — a pointer to a null terminated byte string

- • P — a pointer to a null terminated Unicode string

- • s — a signed short (16–bit) value

- • S — an unsigned short (16–bit) value

- • x — skip forward a byte

- • X — back up a byte

- • z — a Unicode string in big-endian (network) order, null padded

- • Z — a Unicode string in little-endian order, null padded

- • @ — go to absolute position for next field

Each character may be followed by a number that specifies a repeat count. The character and repeat count comprise a field specifier. Field specifiers may be separated by white space. For all type specifiers except, a , A , x , X , and @ , the repeat count specifies how many values from the list of arguments are to be used. If the repeat count is * , then all remaining values are used.

If you specify * as the first character of the template , you are indicating that the second argument is a pointer to a buffer to unpack, and not the buffer itself. Normally, this is not needed for ACL strings but the dl_call function could return such a pointer. If a number follows the leading * , it is the size of the buffer. If the size is omitted, the unpack function will not detect if the template exceeds the bounds of the buffer. This feature should be used with caution since an incorrect template or invalid input could cause Arbortext Editor to terminate unexpectedly.

For specifiers a and A , only a single value is used. The repeat count specifies the size of the field in the input data structure and is also the size of the output string for type a . If type A was specified, then trailing nulls and spaces are stripped from the output string. The type specifiers x , X , and @ do not use up any values. The repeat count for x and X specify how many bytes can be skipped in the input string from the current position before unpacking the next field. The field specified @* tells to move to the end of the string. For example:

```
unpack("@*X3a3", "abcxyz")
```

returns the last three bytes of the string, “xyz.”

Since Arbortext Editor does not support floating point as a basic type, the unpacked values corresponding to the f and d type specifiers are returned as strings. For example:

```
unpack("d", pack("d", "72.27")))
```

returns “72.

The a and A designators convert a possibly multi-byte string in the system character set to a Unicode string. Note, if a field length is specified, for example, a7 , not all bytes may be converted to Unicode if the field ends in the middle of a multi-byte character.

The c and C designators unpack 8-bit characters, not Unicode characters.

The p designator points to a null terminated byte string. The resulting string variable could then be converted by calling unpack or mbstoucs .

The z and Z designators create a byte string of Unicode characters, since strings are normally 8-bit Latin1 (ISO 8859–1) characters.

Here is an example of how to byte-swap a file containing Unicode characters:

```
while ((len = read(inf, buf, 512)) > 0) {
ustr = unpack("z*", buf);
write(outf, pack("Z*", ustr));
}
```

This works whether the original file was in big-endian or little-endian order.

If a function called by dl_call returns a pointer to a string, the ACL code must convert this to an ACL string using unpack . A typical method would be unpack("p", result) . This will work but it is much better to use unpack("*a*", result) . Using “p” will simply widen the 8 bit string to 16 bits without doing any multi-byte to Unicode conversion. Consequently, this method does not work if the string contains any multibyte characters. Using “*a*” will convert the result string from a multibyte string to Unicode using the current locale. In both cases you are assuming that the result is an 8-bit string. If it is a Unicode string you can use unpack with “P”, “*z*”, or “*Z*”. In all cases the ACL code must know whether the result is an 8-bit string or a Unicode string.

The Perl type specifiers % , b , B , h , H , and u are currently not supported.

## Related Topics

- • pack function

- • dl_call function



---

# uri_resolve

# uri_resolve

string = uri_resolve ( uri [, catalogpath ])

This function performs a catalog lookup to resolve the URI specified by uri , returning the system path name for the resource. If the identifier is not found in any of the catalog files in the search path, the uri_resolve function returns a null string.

catalogpath specifies a list of directories to search for the catalog file. If it is not specified, the path list specified in the set catalogpath option, which is initialized from the environment variable APTCATPATH , is searched.

The uri_resolve(uri, catpath) function is equivalent to catalog_resolve("URI", uri, "", "", catpath) .

## Related Topics

- • catalog_resolve function



---

# url_decode

# url_decode

string = url_decode ( str [, charset ])

This function decodes the URL-encoded string str as encoded by url_encode returning its original value. If the optional charset is supplied and the given string contains any URL encoded multi-byte character sequences, then those sequences are decoded back into their original Unicode characters.

The following charset values are supported:

- • iso8859-1

- • iso8859-2

- • iso8859-3

- • iso8859-4

- • iso8859-5

- • iso8859-7

- • iso8859-8

- • iso8859-9

- • ps_ascii

- • ps_symbol

- • jeuc

- • sjis

- • big5hku

- • gb2312

- • koi8

- • ksc5601

- • utf-8

- • Unicode

For example, the following ACL call:

```
url_decode("A%CE%A9B", "utf-8")
```

returns the following string:

```
AΩB
```

The %CE%A9 sequence is interpreted as a multi-byte character sequence in UTF-8. It was decoded into the Greek Omega symbol (Ω), which is Unicode character 937.

## Related Topics

- • url_encode function



---

# url_encode

# url_encode

string = url_encode ( str [, charset ])

This function returns the string str converted to into the MIME format called “ x-www-form-urlencoded ”. Most non-alphanumeric characters are converted into the 3-character string “ % XX ”, where XX is the two-digit hexadecimal representation of the 8–bit character. The following punctuation characters are not encoded: “-_.*”.

If any Unicode character in str is greater than 255, then a null string is returned unless you also supply the optional charset (character set) parameter. If a charset parameter is supplied, such characters are encoded in a multi-byte sequence using the given character set and then the resulting sequence will be URL encoded.

The following charset values are supported:

- • iso8859-1

- • iso8859-2

- • iso8859-3

- • iso8859-4

- • iso8859-5

- • iso8859-7

- • iso8859-8

- • iso8859-9

- • ps_ascii

- • ps_symbol

- • jeuc

- • sjis

- • big5hku

- • gb2312

- • koi8

- • ksc5601

- • utf-8

- • Unicode

For example, Unicode character 937 is a Greek Omega symbol (Ω). The following ACL call:

```
url_encode("A" . chr(937) . "B", "utf-8")
```

returns the following string:

```
A%CE%A9B
```

The UTF-8 encoding of Unicode character 937 is a multi-byte sequence consisting of: 0xCE and 0xA9 .

## Related Topics

- • filename_to_url function

- • url_decode function



---

# user_tag_names

# user_tag_names

count = user_tag_names ( arr [, doc ])

This function fills the array arr with a list of user-defined tags for the current document type, returning the number of tags. The first tag is stored at index 1. All previous elements in arr are discarded. The doc argument specifies the identifier of the document tree to query. If omitted or 0 , the current document is used.



---

# username

# username

string = username ()

This function returns the login name for the current user or a null string if no user name can be found.



---

# validate_against_schematron

# validate_against_schematron

validate_against_schematron ( sch_out [, doc [, sch_file [, output_file [, phase [, xpath_node ]]]]])

This function is used to validate the document instance doc against a given list of Schematron files, defined by sch_file . If doc is not supplied or is 0 , then the current document is used. If sch_file is not supplied, then the Schematron file for the instance’s document type is used. Each error reported by the Schematron is filled into an entry of the array sch_out . The array content is a string that contains both an XPath expression to the element in error and the error description from the Schematron file, separated by the | character. If output_file is specified and not empty, then the XML file with the Schematron results is saved to that file. If phase is supplied and not empty, then that value is passed as the phase parameter to the Schematron. If xpath_node is supplied and not empty, then the Schematron is only applied to the XPath node expressed by that variable.

For example, the following ACL call will validate the current document against the associated Schematron files axdocbook1.sch and axdocbook2.sch :

```
validate_against_schematron($S, 0, "axdocbook1.sch;axdocbook2.sch");
```

Note that the semi colon ( ; ) is the required delimiter.

If the document or Schematron file is not valid, then the function returns -1 . If any errors occur during the schema validation, then the function returns -1 . Otherwise, the function returns the number of errors found, which is also the number of entries put into the sch_out array.

## Related Topics

- • doc_type_schematron_file function

- • Specifying a Schematron File



---

# varsub

# varsub

string= varsub ( string )

This function substitutes variable names within a string . This function is quite useful for delaying the substitution of variables until after a call to amo_text or agettext functions.

Example

You need to display the following message from the default message file.

Error: No file named $name exists.

The problem is that the message includes a variable, $name , containing the file name test.sgm . The message is listed in the catalog with the variable name in place. Let's assume you execute agettext as follows:

```
msg_string = agettext \
("Error: No file named $name exists.")
```

The actual string passed to agettext would include the substituted value for the $name variable:

```
Error: No file named test.sgm exists.
```

This does not match the listing in the catalog, so the agettext would fail. Executing agettext within varsub solves this problem (note the use of single quotes).

```
msg_string = varsub(agettext \
('Error: No file named $name exists.')
```

In the sample above, the actual string passed to agettext would be:

```
Error: No file named $name exists.
```

This entry matches the entry in the default message file, so the returned message (variable name in place) is passed to varsub , which performs the variable substitution. The final result, stored in the variable msg_string would be:

```
Error: No file named test.sgm exists.
```

If the string includes a variable name that you do not want substituted, include an extra dollar sign ( $ ) for the non-substituted variable. For example:

```
msg_string = varsub('The $$name variable is equal to $name.')
```

In this example, the result stored in msg_string would be:

```
The $name variable is equal to test.sgm.
```



---

# vbscript

# vbscript

string = vbscript ( expr [, window ])

This function sends the string expr to the Microsoft Windows VBScript interpreter to be evaluated, returning the result as a string. If the window parameter is not specified, the VBScript expression is evaluated in the global VBScript script context so previously defined VBScript functions are accessible.

The optional window parameter is the identifier of a XUI dialog box that has a script context. If window is provided, the script executes in that dialog box’s script context.

Example

```
path = vbscript('Application.ActiveDocument.DocumentURI')
```

## Related Topics

- • javascript function

- • jscript function

- • perlscript function



---

# window_activate

# window_activate

window_activate ([ window ])

This function brings to keyboard focus (activates) the window identified by window and sets its document to the current document. If window is omitted or 0 , the window associated with the current document is used.



---

# window_add_recent_documents

# window_add_recent_documents

window_add_recent_documents ( pathname )

This function adds the specified document to the Windows Start⇒Documents menu. If pathname is a null string, the Start⇒Documents menu is cleared.



---

# window_cascade_all

# window_cascade_all

window_cascade_all ([ topwindow ])

This function cascades all Arbortext Editor windows leaving topwindow at the top of the cascade. If topwindow is omitted or 0 , the current window is used.

This function does not cascade non- Arbortext Editor windows.



---

# window_class

# window_class

window_class ([ window ])

This function returns the class name (for example, edit , cmd , helpwin2 ) for the window identified by window , which must be valid window identifier. Window identifiers are returned by several ACL functions, including window_create , doc_window , and window_id . If window is omitted or is 0 , the window associated with the current document is used.

## Related Topics

- • doc_window built-in function

- • window_create built-in function

- • window_id built-in function

- • window_list function



---

# window_close

# window_close

window_close ([ window ])

This function iconizes the window identified by window . If omitted or 0 , the window associated with the current document is used.



---

# window_count

# window_count

window_count ([ class [, firstonly ]])

This function returns the number of existing windows of class , or all windows if class is not specified. If the argument firstonly is specified and non-zero, then window_count counts only the first window of each frame. For example, window_count("edit",1) would return the number of edit-class frames while window_count("edit") would include all edit windows, including those in split frames.

## Related Topics

- • window_list function



---

# window_create

# window_create

window_create ( class [, flags [, doc [, geom [, parent [, xuipath ]]]]])

This function creates a window of the specified class with optional components given by flags and returns a unique identifier that may be used in subsequent calls to the window_ xxx functions. The window created is not initially displayed. Use the window_show function to make the window appear.

Windows are of two types:

- • Document class windows that display a document tree and have a class of edit , helpwin[1-4] , or msgwin[1-4] .

- • Dialog class windows that display either a list selection dialog box of class list or xui .

The class determines the default geometry and, for classes other than list , the class-specific keymap. By default, a new keymap is created for the window on the first map command processed for the window. This keymap has the name window n , where n is the identifier of the window, and is deleted when the window is destroyed. If a set keymap=user command is executed for the window, or if bit 0x00040 is specified in flags , the global keymap for the class will be used. See the flags bit descriptions below.

The flags parameter is a bit mask that depends on the class and is defined below:

The following are the flag bits for list and xui class windows.

- • 0x1 — Supply vertical scrollbar.

- • 0x2 — Verify input (that is, set verify Item attribute).

- • 0x4 — Supply an Apply button,

- • 0x8 — Supply a Help button.

- • 0x10 — For XUI dialog boxes, delete the document after the window is destroyed. In the following example, $doc will be destroyed automatically after $win is destroyed:

- • 0x040000 — Make the new window a top-level window with its parent being the desktop. This flag is only useful to the xui and list class windows; the windows of all other window classes are created as top-level windows.

OK and Cancel buttons are always supplied.

The following are the flag bits for document class (all non- list ) windows. The “(pane)” note indicates a flag that, when returned by window_mask , reflects the status for the pane containing the cursor (that is, last active window).

- • 0x00001 — Supply vertical scrollbar (pane).

- • 0x00002 — Supply menu bar.

- • 0x00004 — Supply command subwindow if class is edit .

- • 0x00008 — Supply message footer subwindow.

- • 0x00010 — Automatically call doc_close on the attached document when the window is destroyed. (pane).

- • 0x00020 — Supply edit toolbar (that is, Toolbar 1) (pane).

- • 0x00040 — Attach the global window class keymap to the window instead of creating a private keymap (pane).

- • 0x00080 — Supply horizontal scrollbar (pane).

- • 0x00100 — Do edit command initializations, include reading the document type instance command files ( instance.acl and instance.js ) and document command files ( docname .acl and docname .js ) if they exist, and calling editfilehook when a document is attached to the window. This bit applies only to edit class windows (pane).

- • 0x00200 — Split the window into two side–by–side (that is, next to one another other) panes.

- • 0x00400 — Split the window into two top/bottom (that is, one over the other) panes.

- • 0x00800 — Make the window a typical user edit window (as opposed to a display window).

- • 0x01000 — Supply a table column width ruler (pane).

- • 0x02000 — Supply a table row height ruler (pane).

- • 0x04000 — Supply the Markup toolbar (that is, Toolbar 2).

- • 0x08000 — Supply the Table toolbar (that is, Toolbar 3).

- • 0x10000 — Supply the Application toolbar (that is, Toolbar 4).

- • 0x080000 — Do not update the filelist option, the Arbortext Editor File menu list of recently edited documents, or the Microsoft Windows list of recently edited documents with the path name associated with the doc parameter (if the 0x00800 flag is specified). Note that this does not apply to documents subsequently loaded in the window.

If a menu bar is requested, it must be initialized using the menu_load or menu_add commands before the window is first displayed.

If a message footer is created, error messages and output from the message command are displayed in the left part of the footer if the message is short enough (otherwise a dialog box is used). The message attribute of the window_set function may also be used to set the message text. Any messages directed to the message footer are considered transient and are erased on the next key or button event received in the window.

The doc parameter specifies the identifier of the document tree to be attached to the window. The document must not already be displayed in another window. If it is, the function returns -1 . If doc is -1 , a scratch document is created that will automatically be destroyed when the window is destroyed. In this case, the associated document type is ascii for edit class windows or the built-in help document type for other classes.

If the flags argument specifies bit 16 , the doc_close is called on doc when the window is destroyed by window_destroy . In this case, the normal quit/exit processing is done. If there are unsaved changes, and if an exit command was used to dismiss the window, changes are saved without prompting. If a quit command caused the call to window_destroy , you are prompted to save any unsaved changes. The doc parameter does not apply to list class windows and is ignored if given.

geom specifies the initial geometry for the window and is a string of the form WxH+X+Y, where W and H are the width and height of the window in pixels, and X and Y give the location of the upper left corner of the window. Refer to the description of the geometry attribute of window_set for details.

window_set may be used to set various attributes for the window such as its title, status bar message, and destroy callback.

window_create returns -1 if the window cannot be created.

parent it is an optional parameter used as the parent window for the new window. Only supports dialog class. If parent is 0 , then the active window is used.

xuipath is an optional parameter used only by edit windows to supply an alternative XUI file to define the toolbars used by the edit window. If xuiPath is not supplied (or empty), then Arbortext-path \lib\dialogs\editwindow.xml is used.



---

# window_cur_table

# window_cur_table

gridId = window_cur_table ( [window] )

This function returns the ID of the active grid in window window (or in the active window, if window is omitted).



---

# window_destroy

# window_destroy

window_destroy ( window )

This function destroys the window identified by window , releasing all resources allocated. If a scratch document was allocated by window_create , that is, no document identifier was passed to window_create , then it will be freed also. If a destroyCallback is set on the window, it will be called before the window is actually destroyed. If you execute this function on the only remaining window, Arbortext Editor will exit.



---

# window_doc

# window_doc

window_doc ([ window ])

This function returns the document identifier for the document tree displayed in the window specified by window . The window argument is a window identifier as returned by window_create or is one of the window classes such as edit or cmd . In the latter case, the window of the specified class last having focus is used. If no argument is given or is 0 , the current window is used.



---

# window_empty

# window_empty

window_empty ([ window ])

This function returns 1 (True) if the window identified by window contains an empty scratch document.



---

# window_enable

# window_enable

window_enable ( window [, enable ])

This function can be used to enable or disable a window. It can also be used to query the current enabled status of a window.

- • win — A valid window identifier.

- • enable — One of the following values:

A disabled window cannot receive input from the user. The return value is the previous enabled state of the window:

- • 0 — The window was disabled.

- • non-zero — The window was enabled.



---

# window_get

# window_get

window_get ( window , attr [, arr ])

This function returns the value of the attribute attr for the window identified by window . If the supplied attr is a set option, the function returns the window or view scope value of the option. If attr is a set option with a document local scope or no local scope at all, it returns nothing.

In all but one case, the attribute value is the return value of the function and the third argument arr should not be given. If attr is “items”, then arr specifies the name of an array which is filled with a list of all items displayed in the list selection dialog box identified by window . In this case, the function returns the number of items stored in arr . See window_set for a list of all available window attributes.

Examples

```
window_get(w, "geometry")
window_get(listw, "items", arr)
window_get(w, "destroyCallback")
```

## Related Topics

- • Set option scope

- • window_set function

- • doc_get function

- • current_window function

- • option_scope function

- • set command



---

# window_get_columnview

# window_get_columnview

window_get_columnview ( window , colnamesArr , colwidthArr )

This function enables you to retrieve the Column view settings for a window view.

The window parameter is the window view for which Column view settings are being retrieved.

The colnamesArr parameter is an array of the column names for all columns defined in the .dcf file for the document type. The order of the entries in the array represents the order in which the columns are currently displayed. The first or Outline column is not included in the array, since it cannot be reordered and it never scrolls.

The colwidthArr parameter is an array parallel to colnamesArr that indicates the column width or whether each column is being displayed. Positive values indicate that the column is being displayed and gives the width of the column in pixels. Negative values indicate that the column is not being displayed and the default width of the column if it were showing.

The special column name, *ScrollBoundary* , is used to position the scroll boundary. Columns that come before the scroll boundary do not scroll horizontally and columns that come after the scroll boundary do scroll. Only one scroll boundary can be present. If a scroll boundary is not present, then only the Outline column is not scrolled.

The function returns the number of columns in the arrays. A zero indicates that Column view is not defined for this window. A –1 is returned for other errors.

## Related Topics

- • window_set_columnview function



---

# window_id

# window_id

window_id ([ class_or_index_or_title ])

This function returns different values in the following situations:

- • If class_or_index_or_title is a number n , window_id returns the identifier of the n th subwindow in the main window associated with the current document. For example, if the current document is displayed in an edit class window, window_id(1) would return the identifier of the edit subwindow and window_id(2) would return the associated command subwindow identifier.

- • If class_or_index_or_title is one of the classes helpwin1 through helpwin4 , or msgwin1 through msgwin4 , window_id returns the window identifier of the corresponding predefined window, or -1 if it does not exist. window_id never returns a window of one of these classes created by window_create , only built-in windows.

- • If class_or_index_or_title is edit or cmd , window_id returns the identifier of the window of the specified class that last had focus. If the current document is associated with a window of one of these classes, window_id returns that window.

class_or_index_or_title may also be one of the following predefined modeless dialog class names:

class_or_index_or_title may also specify a string to match either the title of a window or the name of a document open in a window. For example, window_id("Document1") returns the window identifier of the window displaying the document named “Document1”. If the string does not match a document name, the string is matched against the titles of all open windows. For example, window_id(window_get(0,"title")) would return the id of the current window, the same as window_id(0) .

## Related Topics

- • doc_name function

- • window_class function

- • window_get function

- • window_list function



---

# window_list

# window_list

window_list ( arr [, class [, window [, flags ]]])

This function fills the array arr with a list of all existing windows of class class , or all windows if class is not specified. It returns the number of window identifiers stored in the array. The window identifiers are returned in no particular order.

If window is specified, only the subwindows belonging to the frame containing window are returned. If the flags parameter is given, window may be given as -1 to mean unspecified.

The optional flags parameter is a bitmask that limits the window ids returned. The value is constructed using OR with the following flags:

- • 0x01 — Return only the active window in a given frame. For example, if the frame has a window split or command window, return only the window which last had keyboard focus.

- • 0x02 — Return only top level windows. That is, return only those windows that do not have a parent window.

Example:

```
window_list(arr, "edit", win)
```

The function call above would return all the edit panes associated with the window specified by win .

## Related Topics

- • window_id function

- • window_class function

- • window_count function



---

# window_load_component_file

# window_load_component_file

window_load_component_file ( window , xuifile )

window_load_component_file adds toolbars and menus to an existing window based on the XUI definition in the specified file. Existing toolbars and menus will not be affected by the addition.

- • window — The value of the id attribute of the window to be changed. This window can be an edit window or a dialog box.

- • xuifile — The XML file defining the XUI controls to be added to the window.

Refer to the Working with XUI (XML-based User Interface) dialog boxes section of the Customizer's Guide for detailed information on XUI dialog boxes.



---

# window_lower

# window_lower

window_lower ([ window ])

This function moves the window identified by window to the bottom of the stacking order, that is, below all other windows. If window is omitted or 0 , the window associated with the current document is used.



---

# window_mask

# window_mask

window_mask ([ window ])

This function returns the flags bit mask used to create the window identified by window , that is, the second argument to window_create . This mask can be inspected to see if the window has a scrollbar, menu bar, command window, and or message footer. If window is omitted or 0 , the window associated with the current document is used.

A listing of the bits in the bit mask appears in the description of the window_create function.

## Related Topics

- • window_create function



---

# window_name

# window_name

window_name ([ window ])

This function converts the window identifier window into a character string that can be used on commands like caret and map , for example, "window14". If window is omitted or 0 , the window associated with the current document is used.

Examples

```
local win_name = window_name(win_id)
caret $win_name
```



---

# window_open

# window_open

window_open ([ window ])

This function un-iconizes the window identified by window . If the window is already visible or is not mapped, this function does nothing. If window is omitted or 0 , the window associated with the current document is used.



---

# window_raise

# window_raise

window_raise ([ window ])

This function moves the window identified by window to the top of the stacking order, that is, on top of all other windows. If window is omitted or 0 , the window associated with the current document is used.



---

# window_redisplay

# window_redisplay

window_redisplay ([ window [, flags ]])

Redraws the given window. The redrawing takes effect immediately. This is useful in command scripts to show an intermediate state. By default, changes to windows made inside command scripts do not show up until the script completes.

- • window — The window to redraw.

- • flags — Redraw options. The following bit values are supported in the flags parameter.

## Related Topics

- • redisplay command



---

# window_remove_split

# window_remove_split

window_remove_split ( window [, flag ])

This function removes one or more split windows from the frame containing the window identified by window . Note, that window is not removed.

flag specifies which split to remove and is one of the following:

- • 1 — remove the vertical split

- • 2 — remove the horizontal split

- • 3 — remove both the horizontal and vertical splits.

If flag is omitted or 0 , then 3 is used, that is, both splits are removed.

window_remove_split returns the number of split windows removed.

## Related Topics

- • window_split function

- • window_sync_pane function



---

# window_reset_configuration

# window_reset_configuration

window_reset_configuration ([ win ])

This function resets all of the display options to their default settings for the window specified by win . If win is omitted or 0, the current window is used.

See the set savewindowconfiguration command option for the list of options reset by this function.



---

# window_set

# window_set

window_set ( window , attr , value , … )

This function sets the values of the specified attributes for the specified window. Several attributes are generic and apply to all window classes. Other attributes are specific to a particular window class, for example, edit and list .

If attr is a set option, this function sets the window or view scope value of the option. If attr is a set option with a document local scope or no local scope, no value is set.

Description of attributes:

appendItem string — Appends a new item with the specified value to the list displayed in the specified list class window.

applyLabel string — Sets the label on the APPLY button of the list class window to the specified string.

background color — Sets the background color for the entire dialog box specified by window . color is either a named color or an RGB specification preceded by # .

callback func ( win but seln pos ) — Specifies the name of a function to be called when a button is pressed in the specified list class window. The function is called with four arguments:

- • win — The identifier of the list window

- • but — A code indicating which button was pressed:

- • seln — A string giving the current selection.

- • pos — The ordinal number of the selection within the list or 0 if the selection is not a element of the list ( verifyItem must be 0 in this case).

The callback function should act on the button as follows:

- • -1 — Destroy the window using window_destroy .

- • 0 — Dismiss the window using window_show(win, 0) or destroy it with window_destroy .

- • 1 — Act on the selection and dismiss or destroy the window.

- • 2 — Act on the selection and leave the window up.

- • 3 — Display a help message only.

This recommended behavior assumes the default button labels.

canvasbackground color — Sets the background color for the edit canvas specified by window . color is either a named color or an RGB specification preceded by # .

canvasforeground color — Sets the foreground color for the edit canvas specified by window . color is either a named color or an RGB specification preceded by # . Setting the foreground color is only effective when editing in ASCII mode. canvasforeground cannot be set when editing in SGML or XML mode

caretMovedCallback func ( win new old [, oldpos ]) — Specifies the name of a function to be called when the cursor is moved such that either the containing OID or the OID to the right of the cursor has changed. The function is passed up to four arguments:

- • win — The identifier of the window.

- • new (optional) — The new OID, that is, oid_caret .

- • old (optional) — The old value of oid_caret .

- • oldpos (optional) — The old position of the cursor as would be returned by oid_caret_pos(OID) .

If a cut operation causes the cursor to be moved, the old object identifier old may no longer be valid. The callback function should call oid_valid(old) before using old . Since computing the old position oldpos could be time consuming in large flat documents, it is recommended that the oldpos argument not be used unless necessary, for example, if the callback function may need to restore the old cursor position, in effect, cancelling the cursor movement.

cancelLabel string — Sets the label on the CANCEL button of the list class window to the specified string.

default string — Sets the default selection for the list class window to the specified string (which must be a member of the list). Normally, this attribute should be set when the window is created, before it is displayed.

deleteItem string — Removes the first item matching the specified string from the list displayed in the specified list class window.

destroyCallback func ( win ) — Specifies the name of a function to be called when the window is destroyed. The function is passed a single argument, the ID of the window being destroyed.

embedded — Determines the type of Arbortext Editor window. This is a read-only attribute that can only be used by the window_get function. Returns 0 for a full frame or normal Arbortext Editor window. Returns 1 for an embedded frame Arbortext Editor window running in an ActiveX control.

focusCallback func ( win ) — Specifies the name of a function to be called when the window obtains focus. The function will be called only when the window changes from an unfocused state to a focused state. The function is not called when Arbortext Editor receives focus and the desired window had focus the last time Arbortext Editor had focus. The function is passed a single argument, the ID of the window receiving focus.

geometry string — Sets the geometry of the window to the specified value, which is a string of the form WxH+X+Y, where W and H are the width and height of the window in pixels, and X and Y give the location of the upper left corner of the window. The format of the string allows just the width and height and/or position to be set by omitting fields, for example:

```
window_set(w, "geometry", "500x350")
window_set(w, "geometry", "+5-5")
```

foreground color — Sets the foreground color for the entire dialog box specified by window . color is either a named color or an RGB specification preceded by # . Setting the foreground color will only affect those dialog box elements that inherit the window color. For example, scrollbars and toolbars will not respond to foreground color changes.

helpLabel string — Sets the label on the HELP button of the list class window to the specified string.

items array or 0 — Sets the list of items displayed in the list class window to the contents of the specified array. The first element is stored at index 1. If the attribute value is 0 or the null string instead of an array name, then an empty list replaces the contents of the scrolling list.

label string — Sets the label displayed at the top of the list class window to the specified value.

menuPostCallback func ( win , menu ) — Specifies the name of a function to be called when a top level menu is posted from the menu bar associated with the window. The function is passed two arguments: win is the identifier of the window and menu is the name of the menu being posted, for example, “File”. The callback function may use the menu_change command to disable or enable menu items, change item labels, and so on. The function may not change the menu bar using the menu_load , menu_reset , or menu_delete commands. The function is not called for shortcut menus.

message string — Sets the left field message footer to the specified string. The message will appear immediately after the window_set function is executed since a call to window_sync is done automatically. This makes the message footer useful for status messages as a script progresses. The message is erased automatically when the next key or button event is received in the window. If the specified window does not have a message footer, that is, (window_mask(w) & 8) == 0 then this attribute is ignored.

parentWindow windowID — Sets the parent window to the window identified by parenwindowID .

okLabel string — Sets the label on the OK button of the list class window to the specified string.

option value — Sets the specified option to the specified value . The option must be one of the Arbortext Editor set options (see the set command ). The specified option must have a local scope of either window or view. For options that take string values, enter the value. For options that take a boolean value (that is, on or off ), enter either a one ( 1 ) or a zero ( 0 ).

prompt string — Sets the command window prompt (which is normally Command: ) associated with the specified edit (or cmd ) class window. If the value is a null string "" , then the prompt is erased. This attribute is ignored if the window does not have a cmd subwindow.

quitCallback func ( win , code ) — Specifies the name of a function to be called when the window receives a quit event, that is, the window is dismissed from the window manager or by a key or menu mapped to the quit or exit commands. The function is then passed two arguments:

- • The ID of the window being dismissed.

- • A code that indicates how the window is dismissed and has one of the values:

If this function returns -1 , then quit will be cancelled.

selection string — Sets the selection (the type-in field) of the list class window to the specified string.

title string — Sets the window manager title for the window to the specified string. For example:

```
window_set(w, "title", main::progname . " Messages")
```

Once a window has its title set with the window_set function, Arbortext Editor will no longer change the window's title on its own (as it normally does when a new document is loaded or following a SaveAs). To get Arbortext Editor to resume setting the window title, use window_set(win, 'title', '') . An empty title sent to the window_set function will not cause the window title to be blanked, but instead clears the state that says the title can only get updated through window_set . If a user really wants a blank title, then window_set(win, 'title', ' ') would work.

verifyItem value — Changes the verification mode of the list class window. If the value is true (non-zero), then any input typed in the selection field must be an element of the list displayed. If false ( 0 ), then the selection does not need to be a member of the list. Normally, this attribute should be set when the window is created, before it is displayed.

view value — Changes the current view to the indicated value. The following values are supported:

- • edit — Changes the current view to Edit view.

- • docmap — Changes the current view to Document Map.

- • column — Changes the current view to Column view.

viewmode value — Changes the view in the current window based on the indicated value. The following values are supported:

- • edit — Changes the window to Edit view.

- • docmap — Changes the window to a split view with Document Map and Edit view positioned based on the current settings of the docmapside and docmappercent options.

- • column — Changes the window to a split view with Column view and Edit view positioned based on the current settings of the docmapside and docmappercent options.

## Related Topics

- • Set option scope

- • option_scope function

- • set command



---

# window_set_columnview

# window_set_columnview

window_set_columnview ( window , colnamesArr , colwidthArr )

This function enables you to set the Column view settings for a window view.

The window parameter is the window view for which Column view settings are being set, or zero to indicate that the current view should be used.

The colnamesArr parameter is an array of the column names for all columns defined in the .dcf file for the document type. The order of the entries in the array represents the order in which the columns should be displayed. The first or Outline column is not included in the array, since it cannot be reordered and it never scrolls.

The colwidthArr parameter is an array parallel to colnamesArr that indicates the column width and whether each column should be displayed. Positive values indicate that the column should be displayed and gives the width of the column in pixels. Negative values indicate that the column should not be displayed and the default width of the column if it were showing. A value of zero indicates there should be no change to the status or width of that particular column, but its order may have changed. Valid widths are between 10 and 1200 pixels. Widths outside of that range are ignored.

The special column name, *ScrollBoundary* , is used to position the scroll boundary. Columns that come before the scroll boundary do not scroll horizontally and columns that come after the scroll boundary do scroll. Only one scroll boundary can be present. If a scroll boundary is not present, then only the Outline column is not scrolled.

The function returns 1 for success and 0 for failure.

## Related Topics

- • window_get_columnview function



---

# window_show

# window_show

window_show ( window , map )

This function changes the state of the window identified by window . If map is true (non-zero), then the window is mapped, that is, displayed. If map is false (zero), then the window is withdrawn, that is, no longer displayed. In this case, the window still exists and may be redisplayed by calling window_show with map =1 , or could be destroyed with window_destroy .



---

# window_split

# window_split

window_split ( win [, horiz [, percent ]])

This function splits the current edit window into two panes containing the currently open document (if any). The win parameter defines the window to split. The horiz parameter is a boolean: 1 creates a top/bottom split, 0 creates a right/left split. The percent parameter defines the initial proportions of the split panes, with the specified percent applying to the left pane for a right/left split, or the bottom pane for a top/bottom split.

By issuing this function twice using different values for horiz , you can create a Arbortext Editor window with one left pane, and two (top/bottom split) right panes.

## Related Topics

- • window_remove_split function

- • window_sync_pane function



---

# window_state

# window_state

window_state ( window )

This function returns an integer describing the current state of the window identified by window , which is a window identifier as returned by window_create , or is one of window classes edit or cmd , or is a predefined window name msgwin[1-4] , or helpwin[1-4] . The state is one of the following:

- • -1 — invalid or non-existent window

- • 0 — window is unmapped (hidden or withdrawn)

- • 1 — window is minimized

- • 2 — window is visible (normal)



---

# window_sync

# window_sync

window_sync ( )

This function forces all pending WM_PAINT messages to be processed. These actions may be necessary in some lengthy scripts to update the display immediately instead of waiting until the script finishes.



---

# window_sync_pane

# window_sync_pane

window_sync_pane ( window )

This function synchronizes the window in the other pane to the window identified by window . If window is omitted or 0 , the current window is used.

Synchronizing the window includes setting the caret in the other window to the specified window's caret and also repositioning the other window so that the lines containing the caret are aligned, if the frame is split horizontally, that is, the windows are separated by a vertical pane.

If the frame is split into more than two windows, window_sync_pane behaves as follows. If window specifies a Document Map window, then the synced pane is the edit (non-Document Map) window which most recently had focus. If window specifies a non-Document Map window, then the corresponding Document Map pane is used if it exists. If there are no Document Map panes in the frame containing window , then the pane which previously had focus is used.

The function returns 1 (True) on success or 0 (False) if nothing was done (for example, there is no other pane or the other pane has a different document).

## Related Topics

- • window_remove_split function

- • window_split function



---

# window_sys_close

# window_sys_close

window_sys_close ([ window ])

This function activates the Close item on the window system control menu for the window identified by window . If omitted or 0 , the current window is used.



---

# window_sys_keymenu

# window_sys_keymenu

window_sys_keymenu ([ window ])

This function gives focus to the menu for the window identified by window . The resulting behavior is the same as if the ALT key was pressed and released. If window is omitted or 0 , the current window is used.



---

# window_sys_maximize

# window_sys_maximize

window_sys_maximize ([ window ])

This function activates the Maximize item on the window system control menu for the window identified by window . If omitted or 0 , the current window is used.



---

# window_sys_minimize

# window_sys_minimize

window_sys_minimize ([ window ])

This function activates the Minimize item on the window system control menu for the window identified by window . If omitted or 0 , the current window is used.



---

# window_sys_move

# window_sys_move

window_sys_move ([ window ])

This function activates the Move item on the window system control menu for the window identified by window . If omitted or 0 , the current window is used.



---

# window_sys_restore

# window_sys_restore

window_sys_restore ([ window ])

This function activates the Restore item on the window system control menu for the window identified by window . If omitted or 0 , the current window is used.



---

# window_sys_size

# window_sys_size

window_sys_size ([ window ])

This function activates the Size item on the window system control menu for the window identified by window . If omitted or 0 , the current window is used.



---

# window_table_left_column

# window_table_left_column

columnId = window_table_left_column ( window , gridId )

This function returns the ID of the left most visible column of grid gridId in window window (or in the active window, if window is omitted).



---

# window_table_right_column

# window_table_right_column

columnId = window_table_right_column ( window , gridId )

This function returns the ID of the rightmost visible column of grid gridId in window window (or in the active window, if window is omitted).



---

# window_update

# window_update

window_update ( )

This function forces all open document view windows to be reformatted internally (does not cause view window display to change) and sets the caret and mouse cursor for each view window.



---

# window_xid

# window_xid

window_xid ([ window ])

This function returns the native window system window id or handle associated with the window specified by window , where window is one of the strings returned by the window function or "root" to indicate the root window. If window is not given, then the current window is used.



---

# windows_disabled

# windows_disabled

windows_disabled ( )

This function returns 1 (true) if a modal dialog is currently displayed or the user interface is disabled, for example, by a call to the disable_windows function .

This function may be useful in a timer or channel callback to delay or avoid processing if the user interface is blocked.

## Related Topics

- • set userinput command

- • timer_add_callback built-in function

- • channel_set_callback built-in function



---

# write_(Function)

# write (Function)

write ( fid , buf [, len ])

This function writes len bytes from the scalar variable buf to the file or channel identified by fid , which is an open identifier returned by open_connect or open_accept . If len is omitted, all data in buf is written. write returns the number of characters written or –1 on failure.

Unlike put , write can handle binary data (that is, null characters). See the description of read for an example of a function which copies a binary file using read and write .

For output to a file identifier, write is implemented using the standard I/O function fwrite so it is acceptable to mix put and write calls.

When writing to a network channel, Arbortext Editor automatically queues any data that is not immediately transferred, for example, if the write operation would block. Unlike read , you do not have to be concerned about asynchronous writes.

Example

```
write(sock, "GET" . path. "HTTP/1.0/r/r/r/n")
```

If writing to a binary stream, that is, a file opened with "wb" or a network channel, write writes Unicode characters. Thus,

```
write(fid, "abc\n")
```

would write 8 bytes. A Unicode text file normally starts with the Unicode byte-order mark U+FEFF which can be written to a binary stream as:

```
write(fid, chr(0xfeff))
```

The byte-order mark written to a binary file this way is in the native machine order so that on a little-endian machine like an Intel-based PC, the byte-order mark would actually appear as U+FFFE in the file. Since Unicode characters are also written in native order, this will identify the Unicode file as written on a little-endian machine.

## Related Topics

- • open_accept built-in function

- • open_connect built-in function

- • pack built-in function

- • put built-in function

- • read built-in function



---

# write_preferences

# write_preferences

write_preferences ( path [, doc ])

This function writes the current session scope values for all the preference items to the preferences file specified by path without updating the current window display. If no path is supplied, then the preferences are written to the file Arbortext Editor looks for when reading preferences.

If a document identifier is supplied in the optional doc parameter, the function will write the current local scope (window, document, and view) values to the preferences file specified by path . In this case, the function will set the session values as well. A document identifier of -1 writes the current session scope values to the preferences file. If document identifier is omitted, then the function writes the preference scope values to the preferences file.

If the function executes successfully, it returns a one ( 1 ). If the path is invalid, the function returns a zero ( 0 ).

Examples

```
write_preferences("~/arbortextuser/.arbortext.wcf")
write_preferences("C:\\arbortextuser\\arbortext.wcf",-1)
```

In Windows, a double-quoted string uses a backslash to denote an escape sequence, so you need to supply two backslashes to represent the path separator.

## Related Topics

- • Set option scope

- • current_doc function

- • option_scope function

- • set command



---

# xpath_boolean

# xpath_boolean

This function evaluates an XPath expression with respect to a document and returns 1 (true) if expr is true, otherwise it returns 0 (false).

- • expr — A valid XPath expression.

- • doc — The identifier of the document tree to use as the context node. If omitted or 0 , the current document is used.

A typical boolean expression will use one of the XPath boolean operators ( = , != , < , > , >= , <= ). For example,

```
count(sect1)=0
```

Non-boolean results are converted to boolean using standard XPath rules:

- • The numbers zero ( 0 ) and NaN (not a number) are converted to false . Other numbers are converted to true .

- • Node set expressions returning at least one node are converted to true . Empty node sets are converted to false .

- • Strings are converted to true if they contain at least one character (including white space). Empty strings are converted to false .

To handle errors, call this function from within a catch .

## Related Topics

- • oid_xpath_boolean function

- • xpath_integer function

- • xpath_nodeset function

- • xpath_string function



---

# xpath_integer

# xpath_integer

This function evaluates an XPath expression with respect to a document. This function evaluates expr as a floating-point number, rounds to the nearest integer, and returns that integer.

- • expr — A valid XPath expression that can be represented as a number.

- • doc — The identifier of the document tree to use as the context node. If omitted or 0 , the current document is used.

Non-numeric results are converted to numbers using standard XPath rules:

- • Strings are parsed as floating-point numbers.

- • Boolean expressions are converted to 1 or 0 .

- • Node set expressions are first converted to strings, then parsed. A run-time error occurs if the result cannot be represented as an integer.

To handle errors, call this function from within a catch .

## Related Topics

- • oid_xpath_integer function

- • xpath_boolean function

- • xpath_nodeset function

- • xpath_string function



---

# xpath_nodeset

# xpath_nodeset

This function evaluates an XPath expression with respect to a document and returns the result as an array of OIDs. This function can be used to identify a group of elements to be iterated through. It can also be used for navigation, for example, by passing one of the returned OIDs to goto_oid .

- • arr — An unordered array of OIDs returned by expr .

- • expr — A valid XPath expression that evaluates to a node set containing only XPath nodes that have associated OIDs.

- • doc — The identifier of the document tree to use as the context node. If omitted or 0 , the current document is used.

This function fills the array arr with the first OID of each XPath node returned by expr . The return value is the number of OIDs stored in arr . Duplicate OIDs may be returned if more than one XPath node resolves to the same OID. oid_null is returned for any XPath node that cannot be converted to an OID (for example, namespace nodes and attributes).

To handle errors, call this function from within a catch .

## Related Topics

- • oid_xpath_nodeset function

- • xpath_boolean function

- • xpath_integer function

- • xpath_string function



---

# xpath_string

# xpath_string

This function evaluates an XPath expression with respect to a document and returns the result of expr converted to a string.

- • expr — A valid XPath expression.

- • doc — The identifier of the document tree to use as the context node. If omitted or 0 , the current document is used.

Non-string results are converted to strings using standard XPath rules:

- • Boolean expressions are converted to the string “ true ” or “ false ”

- • Node set expressions return the string value of the first node, or an empty string if the node set is empty.

- • Numbers are not specially formatted.

To handle errors, call this function from within a catch .

## Related Topics

- • oid_xpath_string function

- • xpath_boolean function

- • xpath_integer function

- • xpath_nodeset function



---

# xpath_valid

# xpath_valid

xpath_valid ( expr )

This function checks the syntax of an XPath expression without evaluating it. It does not validate namespace prefixes, element or attribute names. xpath_valid returns 1 if expr has correct syntax. If expr does not have correct syntax, the function returns 0 and stores an error message in the $main:ERROR variable.

This function has the following parameter:

- • expr — An XPath pattern.

Examples:

```
xpath_valid("foo()")
```

Returns 0 , because foo is not an XPath function.

```
xpath_valid("foo/bar")
```

Returns 1 , regardless of whether foo and bar are valid element names or not.

```
xpath_valid("myns:foo/bar")
```

Returns 1 .



---

# zip_extract

# zip_extract

zip_extract ( zippath , outdir [, flags ])

This function expands the given zip file into the specified output directory. Whether any existing files are automatically overwritten is under control of the optional flags parameter. This function does not remove any existing files from the output directory, but may overwrite some of them in some cases. If you want the output directory to be empty before expanding the zip file, then you must do that before calling this function.

The zippath parameter is a full path to a zip file or resource. Both file system and HTTP or HTTPS paths are supported.

The outdir parameter is a full path to an existing file system directory. An HTTP path is not supported.

The flags parameter supports the following bits:

- • 0x01 — Will attempt to overwrite any existing files during extraction. If not set, the function call will fail and not overwrite any pre-existing file. Note that this will not overwrite read-only files.

- • 0x02 — Will ignore any directory information encoded inside the zip file and just extract all files into the output directory itself. That is, it will flatten any existing directory structure.

- • 0x04 — The same as 0x01 , but will attempt to overwrite even read-only files.

The function returns non-zero on success and zero on failure. On failure, main::ERROR will be setup with an appropriate error message. On failure, some files might have already been extracted. Any such files will be left alone.