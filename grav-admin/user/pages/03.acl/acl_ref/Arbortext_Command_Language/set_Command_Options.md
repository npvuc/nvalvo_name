

---

# set_acceptcmdextension

# set acceptcmdextension

set acceptcmdextension= { on | off}

This option determines whether the source and require commands will add the .cmd extension to the file name if no extension was specified. If on , the .cmd extension will be tried after .acl if the file is not found. If off (the default), only .acl is supplied.

The option does not affect files specified explicitly with the .cmd extension. For example:

```
source myfuncs.cmd
```



---

# set_accessibility

# set accessibility

set accessibility= { on | off}

If this option is set to on , Arbortext Editor operates in a manner compatible with screen readers such as JAWS. This option allows screen readers to read menus more easily, and the edit cursor displays as a line one pixel thick.

You can set this option as a preference from the Tools > Preferences dialog box. Click the Advanced button and choose set accessibility . Click the option button on in the dialog box.

You can also set it in an ACL script loaded from the Arbortext-path \custom\init directory or from the command line (available if Full Menus is checked in the Tools > Preferences > Window dialog box).

If a screen reader can notify the system that it has been started or stopped, the set accessibility option switches between off and on if the screen reader starts or stops while Arbortext Editor is running.

Note that as of 4.51, JAWS does not have this capability. You can either turn on the set accessibility option or make sure that JAWS is running before you start Arbortext Editor .

## Related topic

Using accessibility features in Arbortext Editor



---

# set_addrequiredtags

# set addrequiredtags

set addrequiredtags= { on | off}

When set to on , this command inserts any required elements at the same time a tag is entered (as long as such insertion is not ambiguous). The default setting is on .

addreq is a synonym for addrequiredtags .



---

# set_aliaslocale

# set aliaslocale

set aliaslocale= localename

This command specifies a localename (such as French or German) for a document type's alias map file. The default is the system locale, which is defined by the operating system. Arbortext Editor will try to find the map file specified by the aliasmap option in doctypename \locale\ localename , where doctypename is the directory in which the document type is located. If Arbortext Editor does not find doctypename \locale\ localname , or the map file cannot be found in the localename subdirectory, Arbortext Editor will search for the map file in the doctypename directory.

For example,

```
set aliaslocale=French
set aliasmap=docbookfr
```

where docbookfr is an alias map file located in the doctypename \locale\French directory.

## Related Topics

- • set aliasmap command

- • Specifying a default alias map for a document type



---

# set_aliasmap

# set aliasmap

set aliasmap= { none | mapname }

Use this command to apply or remove an alias map for the current document. mapname can be a file name or the full path name of an alias map file. If mapname is a file name, Arbortext Editor appends an .alias suffix to it and tries to locate the file in the doctypename \ locale \ localename directory, where doctypename is the directory in which the document type is located. If the file does not exist in this location, Arbortext Editor tries to locate it in the doctypename directory.

Every time you change the aliasmap setting, the Edit Window will be refreshed to reflect the change.

You can add the set aliasmap command to the instance.acl file in the doctypename directory to specify a default alias map.

## Related Topics

- • set aliaslocale command

- • Specifying a default alias map for a document type



---

# set_allowinvalidmarkup

# set allowinvalidmarkup

set allowinvalidmarkup= { on | off}

This command controls whether invalid markup is allowed in during the loading of a file. If set to off , a file containing invalid markup would lose the invalid markup at load time.

The default is on .

## Related Topics

- • Invalid markup — overview



---

# set_allowsvgexternalresources

# set allowsvgexternalresources

set allowsvgexternalresources= { on | off}

This command controls whether links to external resources in SVG images are supported. If set to off, Arbortext Editor throws an error when previewing or publishing such SVG file containing external resources.

The default is off .

## Related Topics

- • SVG



---

# set_appconfigfile

# set appconfigfile

set appconfigfile= filename

This command specifies an alternate location for an .appcf PDF configuration file for the PTC APP engine.

The command may have one of three values:

- • " " (empty string) — the command is ignored

- • absolute path to an .appcf PDF configuration file

- • simple filename, i.e. filename .appcf

The list of known PTC APP configuration files is built by searching directories on the PE server (for PE composition) or directories on the local machine (for local composition) for APP configuration files ( .appcf ). Files found in a directory are added to the list in alphabetical order.

The directory search order is:

Example:

```
set appconfigfile=memo.appcf
```

## Related Topics

- • PDF Configuration File for the APP Engine

- • set pdfconfigfile



---

# set_appsnapshot

# set appsnapshot

set appsnapshot= { yes | no}

When set to yes , this command collects the transformed XML document that was submitted to PTC APP for printing or publishing to PDF into a zip archive for troubleshooting. The collection also includes the graphics it references and other supporting files. When you set this command to yes , the publishing process creates a zip for each subsequent publishing operation that uses PTC APP . The default setting is no .

The PTC APP snapshot file contains the following:

- • manifest.xml — An XML document that contains information about the publishing parameters in effect when the publishing request was made.

- • inputDoc.xml — The document sent to PTC APP that has been modified for troubleshooting. It will be flattened and its graphic references will point to the doc-graphics directory.

- • doc-graphics — A directory containing a copy of the graphics referenced by inputDoc.xml .

- • appsnap.log — A log of the events from generating the PTC APP snapshot. If the snapshot is not complete, the appsnap.log will contain information about it.

- • dynamic.dtd or dynamic.xsd — An XML document type definition (DTD) file or an XML schema (XSD) file may be necessary to read inputDoc.xml . The snapshot may contain one of these files if the snapshot also contains an inputDoc.xml .

The location where the PTC APP snapshot zip file is saved depends on how the publishing request is made.

- • If you are sending publishing requests to Arbortext Publishing Engine , the snapshot will be generated and the transaction will be archived on the Arbortext PE server . If set debugcomposition is set to on , then the snapshot file will be included with the intermediate files returned to the Arbortext Editor client.

- • If you are publishing locally using Arbortext Editor with Arbortext Styler , the PTC APP snapshot is placed in the Cache Directory (.aptcache) . If you use the Editor menu choices for publishing PDF or printing, a dialog box will confirm the action and notify you where the snapshot has been saved. It will also open the target directory for you if you click Browse to directory . See set appsnapshotprompt for more information.

You can run set appsnapshot from an ACL script loaded from the Arbortext-path \custom\init directory or from the command line in Editor (available if Full Menus is checked in the Tools > Preferences > Window dialog box).

Consult Troubleshooting PTC APP Publishing for more information. Using snapshots for troubleshooting should be done with the help of Technical Support.



---

# set_appsnapshotprompt

# set appsnapshotprompt

set appsnapshotprompt= { yes | no}

When set to yes (the default), this command will launch a dialog box confirming the action that an PTC APP snapshot has been generated and giving its location. Refer to set appsnapshot for more information.

This command applies to the Editor print and publishing to PDF outputs. Set it to no if you are publishing using publishing rules or from a script.

Consult Troubleshooting PTC APP Publishing for more information. Using snapshots for troubleshooting should be done with the help of Technical Support.



---

# set_asciiattributecolor

# set asciiattributecolor

set asciiattributecolor= { colorname | # rgbspec }

This option determines the color value used to display attributes in ASCII documents with markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is blue .

Examples

```
set asciiattributecolor=blue
set asciiattributecolor=#dd00dd
```

## Related Topics

- • set asciicommentcolor

- • set asciideclarationcolor

- • set asciiendtagcolor

- • set asciientitycolor

- • set asciistarttagcolor

- • set asciisyntaxcolor

- • set asciitextcolor

- • asciixslresultattributecolor

- • set asciixslresultendtagcolor

- • set asciixslresultstarttagcolor



---

# set_asciicommentcolor

# set asciicommentcolor

set asciicommentcolor= { colorname | # rgbspec }

This option determines the color value used to display comments in ASCII documents with markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is violet .

Examples

```
set asciicommentcolor=blue
set asciicommentcolor=#dd00dd
```

## Related Topics

- • set asciiattributecolor

- • set asciideclarationcolor

- • set asciiendtagcolor

- • set asciientitycolor

- • set asciistarttagcolor

- • set asciisyntaxcolor

- • set asciitextcolor

- • asciixslresultattributecolor

- • set asciixslresultendtagcolor

- • set asciixslresultstarttagcolor



---

# set_asciideclarationcolor

# set asciideclarationcolor

set asciideclarationcolor= { colorname | # rgbspec }

This option determines the color value used to display declarations and processing instructions in ASCII documents with markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is green .

Examples

```
set asciideclarationcolor=blue
set asciideclarationcolor=#dd00dd
```

## Related Topics

- • set asciiattributecolor

- • set asciicommentcolor

- • set asciiendtagcolor

- • set asciientitycolor

- • set asciistarttagcolor

- • set asciisyntaxcolor

- • set asciitextcolor

- • asciixslresultattributecolor

- • set asciixslresultendtagcolor

- • set asciixslresultstarttagcolor



---

# set_asciiendtagcolor

# set asciiendtagcolor

set asciiendtagcolor= { colorname | # rgbspec }

This option determines the color value used to display end tags in ASCII documents with markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is red .

Examples

```
set asciiendtagcolor=blue
set asciiendtagcolor=#dd00dd
```

## Related Topics

- • set asciiattributecolor

- • set asciicommentcolor

- • set asciideclarationcolor

- • set asciientitycolor

- • set asciistarttagcolor

- • set asciisyntaxcolor

- • set asciitextcolor

- • asciixslresultattributecolor

- • set asciixslresultendtagcolor

- • set asciixslresultstarttagcolor



---

# set_asciientitycolor

# set asciientitycolor

set asciientitycolor= { colorname | # rgbspec }

This option determines the color value used to display entity references in ASCII documents with markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is olive .

Examples

```
set asciientitycolor=blue
set asciientitycolor=#dd00dd
```

## Related Topics

- • set asciiattributecolor

- • set asciicommentcolor

- • set asciideclarationcolor

- • set asciiendtagcolor

- • set asciistarttagcolor

- • set asciisyntaxcolor

- • set asciitextcolor

- • asciixslresultattributecolor

- • set asciixslresultendtagcolor

- • set asciixslresultstarttagcolor



---

# set_asciiextension

# set asciiextension

set asciiextension= ext

This command specifies the extension to use for newly saved ASCII (non- SGML ) files. The default value is txt . The Save As dialog box and save_as command add this extension if the specified file does not already have an extension and the -asciiextension option is non-null.

A period should not be included as part of the extension.

Examples

```
set asciiextension=txt
```

## Related Topics

- • set defaultfilter command

- • set htmlextension command

- • set sgmlextension command



---

# set_asciistarttagcolor

# set asciistarttagcolor

set asciistarttagcolor= { colorname | # rgbspec }

This option determines the color value used to display start tags in ASCII documents with markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is red .

Examples

```
set asciistarttagcolor=blue
set asciistarttagcolor=#dd00dd
```

## Related Topics

- • set asciiattributecolor

- • set asciicommentcolor

- • set asciideclarationcolor

- • set asciiendtagcolor

- • set asciientitycolor

- • set asciisyntaxcolor

- • set asciitextcolor

- • asciixslresultattributecolor

- • set asciixslresultendtagcolor

- • set asciixslresultstarttagcolor



---

# set_asciisyntaxcolor

# set asciisyntaxcolor

set asciisyntaxcolor= { on | off}

This command determines whether ASCII documents with markup are displayed with colors to distinguish different markup constructs. The default is on .

## Related Topics

- • set asciiattributecolor

- • set asciicommentcolor

- • set asciideclarationcolor

- • set asciiendtagcolor

- • set asciientitycolor

- • set asciistarttagcolor

- • set asciitextcolor

- • asciixslresultattributecolor

- • set asciixslresultendtagcolor

- • set asciixslresultstarttagcolor



---

# set_asciitextcolor

# set asciitextcolor

set asciitextcolor= { colorname | # rgbspec }

This option determines the color value used to display text in ASCII documents with markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is black .

Examples

```
set asciitextcolor=blue
set asciitextcolor=#dd00dd
```

## Related Topics

- • set asciiattributecolor

- • set asciicommentcolor

- • set asciideclarationcolor

- • set asciiendtagcolor

- • set asciientitycolor

- • set asciistarttagcolor

- • set asciisyntaxcolor

- • asciixslresultattributecolor

- • set asciixslresultendtagcolor

- • set asciixslresultstarttagcolor



---

# set_asciixslresultattributecolor

# set asciixslresultattributecolor

set asciixslresultattributecolor= { colorname | # rgbspec }

This option determines the color value used to display result tree attributes in ASCII documents with XSL markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is teal .

Examples

```
set asciixslresultattributecolor=blue
set asciixslresultattributecolor=#dd00dd
```

## Related Topics

- • set asciiattributecolor

- • set asciicommentcolor

- • set asciideclarationcolor

- • set asciiendtagcolor

- • set asciientitycolor

- • set asciistarttagcolor

- • set asciisyntaxcolor

- • asciitextcolor

- • set asciixslresultendtagcolor

- • set asciixslresultstarttagcolor



---

# set_asciixslresultendtagcolor

# set asciixslresultendtagcolor

set asciixslresultendtagcolor= { colorname | # rgbspec }

This option determines the color value used to display result tree end tags in ASCII documents with XSL markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is maroon .

Examples

```
set asciixslresultendtagcolor=blue
set asciixslresultendtagcolor=#dd00dd
```

## Related Topics

- • set asciiattributecolor

- • set asciicommentcolor

- • set asciideclarationcolor

- • set asciiendtagcolor

- • set asciientitycolor

- • set asciistarttagcolor

- • set asciisyntaxcolor

- • asciitextcolor

- • set asciixslresultattributecolor

- • set asciixslresultstarttagcolor



---

# set_asciixslresultstarttagcolor

# set asciixslresultstarttagcolor

set asciixslresultstarttagcolor= { colorname | # rgbspec }

This option determines the color value used to display result tree start tags in ASCII documents with XSL markup when asciisyntaxcolor is set to on . The value is either a named color or an RGB specification preceded by # . The default is maroon .

Examples

```
set asciixslresultstarttagcolor=blue
set asciixslresultstarttagcolor=#dd00dd
```

## Related Topics

- • set asciiattributecolor

- • set asciicommentcolor

- • set asciideclarationcolor

- • set asciiendtagcolor

- • set asciientitycolor

- • set asciistarttagcolor

- • set asciisyntaxcolor

- • asciitextcolor

- • set asciixslresultattributecolor

- • set asciixslresultendtagcolor



---

# set_autocorrect

# set autocorrect

set autocorrect= { on | off}

When the autocorrect option is set to on , each word entered or changed when editing a document is looked up in the autocorrect.xlf auto correct map file. If that word is found in the map file, the word is automatically replaced by the replacement word specified in the auto correct map file. The default setting is on .

Arbortext Editor can support multiple language-based versions of autocorrect.xlf . For more information, see autocorrect.xlf .

## Related Topics

- • Autocorrection and Spelling Checks

- • Automatically correcting spelling errors



---

# set_autosave

# set autosave

set autosave= { n | off}

When the autosave option is set to a positive number, Arbortext Editor saves any changes to the document every n seconds if there are unsaved changes. 600 , or 10 minutes, is the default. The maximum setting is 7200, or 2 hours.

When Arbortext Editor performs an autosave for a document, it doesn't write to the original file. Instead, Arbortext Editor saves the document to a temporary file (based on the document name) with the extension .asv . If this file exists when the document is reopened, Arbortext Editor will prompt for which version to use. The autosave file, if any, is removed when the document is saved.

Examples

```
set autosave=60
set autosave=off
```



---

# set_autotaginserts

# set autotaginserts

set autotaginserts= { on | off}

When the autotaginserts option is set to on , it obeys the .dcf file setting for automatic tag insertion.

When set to off , this command disables automatic tag insertion.

## Related Topics

- • Replacing or modifying invalid elements

- • Inserting elements and text automatically



---

# set_backgroundcoloraqua

# set backgroundcoloraqua

set backgroundcoloraqua= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named aqua . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorblack

# set backgroundcolorblack

set backgroundcolorblack= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named black . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorblue

# set backgroundcolorblue

set backgroundcolorblue= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named blue . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorbrown

# set backgroundcolorbrown

set backgroundcolorbrown= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named brown . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorgray

# set backgroundcolorgray

set backgroundcolorgray= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named gray . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorgray1

# set backgroundcolorgray1

set backgroundcolorgray1= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named gray1 . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorgray2

# set backgroundcolorgray2

set backgroundcolorgray2= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named gray2 . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorgray3

# set backgroundcolorgray3

set backgroundcolorgray3= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named gray3 . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorgray4

# set backgroundcolorgray4

set backgroundcolorgray4= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named gray4 . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorgray5

# set backgroundcolorgray5

set backgroundcolorgray5= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named gray5 . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorgreen

# set backgroundcolorgreen

set backgroundcolorgreen= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named green . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorlime

# set backgroundcolorlime

set backgroundcolorlime= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named lime . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolormaroon

# set backgroundcolormaroon

set backgroundcolormaroon= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named maroon . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolornavy

# set backgroundcolornavy

set backgroundcolornavy= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named navy . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorolive

# set backgroundcolorolive

set backgroundcolorolive= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named olive . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolororange

# set backgroundcolororange

set backgroundcolororange= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named orange . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorred

# set backgroundcolorred

set backgroundcolorred= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named red . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorteal

# set backgroundcolorteal

set backgroundcolorteal= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named teal . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorviolet

# set backgroundcolorviolet

set backgroundcolorviolet= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named violet . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcolorwhite

# set backgroundcolorwhite

set backgroundcolorwhite= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named white . The value is either a named color or an RGB specification preceded by # .



---

# set_backgroundcoloryellow

# set backgroundcoloryellow

set backgroundcoloryellow= { colorname | # rgbspec }

This preference determines the color value used to display the background (shading) color named yellow . The value is either a named color or an RGB specification preceded by # .



---

# set_balancedselections

# set balancedselections

set balancedselections= { on | off}

When the balancedselections option is set to on , it automatically extends the selection so that tags are balanced. For example, if you select either a start or an end tag when this option is set, the region will be expanded to include the entire tag pair. The default is on .

When the balancedselections option is set to off and an unbalanced selection portion of markup is deleted, all selected content and balanced portions of the selection are deleted. However, no tagging is removed that would result in unbalanced markup or out-of-context errors.



---

# set_bigjobthreshold

# set bigjobthreshold

set bigjobthreshold= { n | off}

This option helps determine if and when the output from a content pipeline is too large to be written to memory, and should be written to disk instead. When the number of document fragments in the document being published exceeds the threshold value n , the document is considered large enough to write the content pipeline output to disk rather than to memory. Setting n to 0 causes pipeline output to be written to disk for all publishing requests.

This set option has document scope. The default value is off .

Some documents are so large that a content pipeline may not be able to write its output to memory. Writing a document into memory uses more memory than reading a document from disk into memory. Arbortext Editor and Arbortext Publishing Engine normally write output to memory, but can, under specified conditions, write pipeline output for a large document to disk to minimize memory consumption.

If content pipeline output is written to disk, then Arbortext Editor or the Arbortext PE sub-process immediately reads the document from disk into memory and proceeds as if the content pipeline had written the document into memory. After the pipeline output is in memory (regardless of the method used), processing continues with other tasks, such as running the formatter, the HTML Help compiler, or some other action.

Set the level at which the pipeline output is written to disk by specifying n for the number of document fragments (tags, text entities, file entities, and XML inclusions) in the document. For example, if you set bigjobthreshold=25 , any document containing more than 25 document fragments will be written to disk during pipeline processing.

The ACL function doc_estimate_dfs can be helpful in determining what values to use for the bigjobthreshold option.

When publishing a DITA map document, the overall size of the document produced by the content pipeline is determined by the size of the DITA topics that are referenced from the map rather than by the size of the map itself. To help account for this difference, the number of document fragments in the map is multiplied by 80 before being compared to the threshold. This approximation allows a common threshold to be used for DITA topic, DITA map, and non-DITA document publishing. This means the bigjobthreshold value should be set to a value roughly 80 times larger than the value returned by the doc_estimate_dfs function for a DITA map for which the output should be written to disk.

For more information on using Arbortext Publishing Engine for publishing, refer to the Programmer's Guide to Arbortext Publishing Engine , the Programmer's Reference , and the Content Pipeline Guide .

## Related Topics

- • Using Arbortext Publishing Engine for publishing documents

- • Set option scope

- • set command



---

# set_bitmapdisplay

# set bitmapdisplay

set bitmapdisplay= { on | off}

This command determines whether graphics and equations can be displayed in the Edit window or icons. This command overrides all previous equationdisplay and graphicdisplay option settings. on is the default.

bitmaps is a synonym for bitmapdisplay .



---

# set_browserpath

# set browserpath

set browserpath= path

This command sets the path and file name of the default HTML browser that Arbortext Editor will use to access URLs and preview documents on the Web.

You do not need to specify this command if you have a file association to a browser for HTML files, as Arbortext Editor automatically detects this association. However, you can use the browserpath option to override this file association.

You can set the path to a web browser in the Tools > Preferences File Locations dialog box.

```
set browserpath=""C:\\Program Files\\Internet Explorer\\iexplore.exe""
```

## Related Topics

- • set browserpreview command



---

# set_browserpreview

# set browserpreview

set browserpreview= { on | off}

When browserpreview is set to on , which is the default setting, the .htm file generated by File > Save as HTML displays in a browser. The .htm file will not display unless you also have a file association for .htm files, the browser path preference specified in Tools > Preferences > File Locations , or the path specified by the set browserpath command.

When set to on , browserpreview also selects the View HTML option in the publish dialog boxes.

The default setting is on .



---

# set_caretcolor

# set caretcolor

set caretcolor= { colorname | # rgbspec }

This command specifies the color of the editing cursor. The value is either a named color or an RGB specification preceded by # .

Examples (the following are equivalent):

```
set caretcolor=red
set caretcolor=#ff0000
```

## Related Topics

- • Using accessibility features in Arbortext Editor

- • set caretthickness command

- • set carettype command



---

# set_caretmovement

# set caretmovement

set caretmovement= { logical | visual}

This command sets the movement of the text cursor within documents that contain mixed left-to-right (LTR) and right-to-left (RTL) content. RTL editing is required for the Arabic and Hebrew locales.

The default is logical , which means cursor movements that are usually interpreted as moving to the left or right are instead interpreted as moving towards the start or end of a document. For example, pressing the left arrow key in RTL text will move the cursor towards the right. When you set this command to visual , the cursor moves to the literal left or right regardless of the locale.

## Related Topics

- • Complex script language support

- • Controlling directionality in a document



---

# set_caretthickness

# set caretthickness

set caretthickness= n

This preference changes the thickness of the insertion cursor (caret). The value n must be in the range 1 to 10. If greater than 3, then the caret is drawn as a block cursor. The default value is 2.

## Related Topics

- • Using accessibility features in Arbortext Editor

- • set caretcolor command

- • set carettype command



---

# set_carettype

# set carettype

set carettype= { ibeam | block | line}

This command sets the style of the text caret in the Arbortext Editor window. There are three available values: ibeam , block , and line . If this command is not set, the default is ibeam .

## Related Topics

- • Using accessibility features in Arbortext Editor

- • set caretcolor command

- • set caretthickness command



---

# set_case

# set case

set case= { on | off}

The case option enables or disables case-sensitive searches. off is the default.

For example, when setting case to off , the search find 'Basil' finds both Basil and basil ; however, when setting case to on , only Basil is found.



---

# set_catalogpath

# set catalogpath

set catalogpath= dir1 [: dirn ]

This command specifies the list of directories to search to locate catalog files. These files resolve public identifiers for both entities and document types. The initial setting is the value of the APTCATPATH environment variable if set. Otherwise catalogpath defaults to the Arbortext-path \doctypes directory.

If there is a catalog file in the Arbortext-path \custom\doctypes subdirectory at startup, the \custom\doctypes path is automatically prepended to the catalog path. If there are any subdirectories of the \doctypes directory that contain a catalog file, those subdirectories are also prepended to the catalog path. Putting a catalog file in \custom\doctypes or in subdirectories of it makes them automatically available, avoiding additional steps to add them to the path.

If there is a catalog file in the Arbortext-path \custom\composer subdirectory at startup, the \custom\composer path is automatically prepended to the catalog path.

The Arbortext-path \custom\doctypes directory is also automatically included if you include %D in the path.

Example

```
set catalogpath="c:\\tmp2\\testdir;c:\\dauser;"
```

Multiple directories are delimited with semicolons, and the entire path must be enclosed in quotation marks.

You can use the append_catalog_path function to update the catalog path.

## Related Topics

- • append_catalog_path function

- • Symbolic parameters in path list variables

- • Catalog files

- • Catalog path and file

- • option_path_list function



---

# set_catalogwarnings

# set catalogwarnings

set catalogwarnings= { on | off}

This command enables or disables any warning messages when a catalog file is read. The default is off .

The command applies to TR9401 catalogs only.

## Related Topics

- • Catalog files



---

# set_cgmprofile

# set cgmprofile

set cgmprofile= profile

This preference is used in conjunction with the graphicwebtransform preference to indicate the type of CGM profile to which specified graphic file formats should be transformed during publishing to HTML outputs. When cgm is the target graphic file format for graphicwebtransform , Arbortext Editor uses the value of the cgmprofile preference to determine the CGM profile to use for the transformation. If cgmprofile is not set, then the graphics are transformed to the WebCGM 2.0 profile.

The following values for the CGM profile are supported:

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

Examples:

```
set cgmprofile=WebCGM_1.0
set cgmprofile=Model_Profile_(ISO_8632:1992/Am.1:1994)
```

## Related Topics

- • set graphicwebtransform



---

# set_changetracking

# set changetracking

set changetracking= { on | off}



Enables and disables change tracking for the current document. The state of this option is preserved in the document itself when it is saved. The default is off .



---

# set_changetrackingkeepdict

# set changetrackingkeepdict

set changetrackingkeepdict= { on | off}



When this option is set to off , all change tracking markup is removed from a file when it is saved, if no change-tracked changes persist (i.e. all changes have been accepted or rejected). Any <atict:info> and <atict:user> elements in the document are deleted, and the xmlns:atict attribute that declares the namespace is removed from the top level document.

The default is on .

To restore the namespace declaration attribute, perform an undo action immediately after such a save.

The option is not saved as a preference.Set the option to off in a startup command file to maintain it as a permanent setting.



---

# set_changetrackingmarkers

# set changetrackingmarkers

set changetrackingmarkers= { none | full}



This command controls how the change tracking markup tags are displayed in the edit window.

- • none — Change tracking markup is not displayed.

- • full — All change tracking markup is displayed.

Change tracking markup never appears in the Document Map pane. The default setting is none .

The following attributes are common to all change tracking markup:

For more detailed information on change tracking attributes, see http://www.arbortext.com/namespace/atict/change-tracking-markup-spec.html .



---

# set_changetrackingverbose

# set changetrackingverbose

set changetrackingverbose= { on | off}



Controls the display of change tracking warnings. The default is on .



---

# set_charentdisplay

# set charentdisplay

set charentdisplay= { on | off}



Changes the display of character entities in the edit window. If set to off , character entities are displayed as tags instead of glyphs or symbols. The default is on .

The set entityinputconvert option must be set to off when opening the document for set charentdisplay=off to have an effect.



---

# set_charentmapfile

# set charentmapfile

set charentmapfile= { filename | none}

This command changes the mapping table used by Arbortext Editor when converting non-ASCII characters into entity references on output. filename is the path name of an ASCII file containing two columns separated by white space; the first column specifies the entity name and the second specifies the character code in decimal, octal (with leading 0), or hexadecimal (with leading 0x). For example:

```
nbsp 160
iexcl 161
```

The default output mapping is given in the isolat1.cf file in the lib subdirectory of Arbortext-path . The actual translation table is built into Arbortext Editor so changing that file will have no effect unless the charentmapfile option is used.

none restores the default translation.

Examples

```
set charentmapfile=/
user-path
/charent.map
set charentmapfile=none
```



---

# set_cmdline

# set cmdline

set cmdline= { on | off}

This option enables or disables the command line window. The default value is off . The default value can be changed through the Show Command Line setting in the Window category of the Arbortext Editor Preferences dialog box.

## Related Topics

- • Preferences dialog box overview

- • Window category in the Preferences dialog box



---

# set_cmsautoconnect

# set cmsautoconnect

set cmsautoconnect= { on | off}

This option determines whether a repository adapter connect dialog box is automatically displayed when you attempt to open a file that is stored in the repository and no session is currently established with the repository. For example, you could select the file from the list of recently edited files on the Arbortext Editor File menu.

The default is on .



---

# set_colbreaktext

# set colbreaktext

set colbreaktext= string

This command specifies the string, centered in the horizontal rule, that is used to denote a forced column break when breaks are displayed in the current tag display mode. The default is Forced Column Break .

Examples

```
set colbreaktext=""
set colbreaktext="New Column"
```



---

# set_columnrulerunit

# set columnrulerunit

set columnrulerunit= { in | cm | mm | pt | pc | pi}

This command sets the unit of measure for the Column Ruler . Available units are:

- • in — inches (default)

- • cm — centimeters

- • mm — millimeters

- • pt — points

- • pc — picas

- • pi — picas

## Related Topics

- • set tablerulers command



---

# set_compilesgml

# set compilesgml

set compilesgml= { on | off}

This command states whether a document type is SGML or XML. When Arbortext Architect loads a document type, it checks for the XML PI at the beginning of the document type. If the XML PI is present, the document type is XML, and Arbortext Architect automatically sets compilesgml to off . If the XML PI is absent, the document type is SGML, and Arbortext Architect automatically sets compilesgml to on .

The value of compilesgml also determines whether the SGML Application or XML Application option is selected on the following menus:

- • Arbortext Architect Compile menu

- • Arbortext Architect DTD Editor Tools menu

If the you change the application value on these menus, the compilesgml value is also changed.

The default value of compilesgml is on .

## Related Topics

- • Arbortext Architect overview



---

# set_composedcharactersubstitution

# set composedcharactersubstitution

set composedcharactersubstitution= { on | off}

This option specifies whether the publishing engine will replace some ASCII characters with their typographical equivalents.

When composedcharactersubstitution is set to on , the characters get replaced by their typographical equivalents as described in the example. The replacements happen for elements that do not have the allowCharacterSubstitution control set to off in the .dcf file.

When composedcharactersubstitution is set to off (the default), ASCII characters are never replaced in any context.

Replacements never occur when publishing using XSL-FO.

```
39 (single quote ') -> 0x2019
96 (grave accent `) -> 0x2018
```



---

# set_composerpath

# set composerpath

set composerpath= dir1 [: dirn ]

This command specifies a list of directories (each directory separated by a semicolon) in which publishing configuration files ( .ccf ) are located. These files are for customizing publishing processes. The default path is Arbortext-path \composer .

If there is an Arbortext-path \custom\composer subdirectory at startup, the \custom\composer path is automatically prepended to the path for .ccf files. Putting your .ccf files in the \custom\composer subdirectory makes them automatically available, avoiding manual steps to add them to the path.

Arbortext Editor also looks at the value of composerpath to locate character entity substitution files used for HTML and XML output from publishing processes.

Example

```
set composerpath="c:\\user\\compfile.ccf;%D"
```

You can use the append_composer_path function to update the publishing configuration file path.

## Related Topics

- • append_composer_path function

- • option_path_list function

- • Symbolic parameters in path list variables

- • option_path_list function



---

# set_contextrules

# set contextrules

set contextrules= { on | off}

This command enables or disables context checking. Note that if you have turned context to “off”, it does not reset when you leave and reenter a document. It remains off until you explicitly turn it on again. Because complex document structures can be difficult to maintain without context checking, PTC recommends that you leave context checking on. on is the default.



---

# set_contextwarnings

# set contextwarnings

set contextwarnings= { on | off}



This command enables or disables the warning message about disabling context checking. on is the default.



---

# set_creoviewdownloaduri

# set creoviewdownloaduri

set creoviewdownloaduri= uri

This command specifies a uri where the Creo View web installer ( .cab file) is located. The uri parameter contains a URI (Uniform Resource Identifier) value.

Arbortext Editor writes the specified uri location to a generated HTML file when an intelligent graphic is published in the HTML file. This enables Internet Explorer to install Creo View when the HTML file is displayed in the browser. Creo View enables users to interact with the intelligent graphics in the HTML file.

If creoviewdownloaduri is not set or contains an empty value, you can still view intelligent graphics in a published HTML file. To support viewing intelligent graphics, Creo View must already be installed on the workstation where Internet Explorer is running.

Refer to the Creo View documentation for more information about Creo View .

Examples:

```
set creoviewdownloaduri=http://www.acme.com/creoview/creoviewexp1_PTC.cab
```

## Related Topics

- • Intelligent graphics overview



---

# set_creoviewfileformats

# set creoviewfileformats

set creoviewfileformats=" [edz] [;iso] [;pvz] [;cgm] "

This command specifies both the graphic file formats that should be displayed using the embedded Creo View control in Arbortext Editor and the graphic types that should be published using Creo View . By default, the following types of graphics are displayed in the embedded control:

- • EDZ ( .edz )

- • PVZ ( .pvz )

You can also set the dialog box to also display CGM ( .cgm ) graphics. The arguments are the file extensions for the graphic types separated by semicolons. If you set the value to more than one graphic type, you must enclose the arguments in quotes. If you set the value of this option to an empty string, the Creo View control will not be used to display any graphics.

Publishing intelligent graphics using Creo View is also supported for all intelligent graphics types. Refer to the Creo View documentation for more information about Creo View .

Examples:

```
set creoviewfileformats=pvz
set creoviewfileformats="pvz;cgm"
```

## Related Topics

- • Intelligent graphics overview



---

# set_datamergepath

# set datamergepath

set datamergepath= dir1 [: dirn ]



This command specifies a list of directories in which data merge configuration files ( .dmf ) are located. These files are for customizing data merging operations. The default path is Arbortext-path \datamerge .

If there is an Arbortext-path \custom\datamerge subdirectory at startup, the \custom\datamerge path is automatically prepended to the path for data merge configuration files. Putting your .dmf files in the \custom\datamerge subdirectory makes them automatically available, avoiding manual steps to add them to the path.

Refer to the Customizer's Guide for details on configuring your site to merge data.



---

# set_datamergereadonly

# set datamergereadonly

set datamergereadonly= { on | off}



This command specifies the read-only status of merged data regions in documents. If set to on (the default), merged data regions are read-only.

Refer to the Customizer's Guide for details on configuring your site to merge data.



---

# set_dcffile

# set dcffile

set dcffile= { name | none}

This command specifies the document type configuration file ( .dcf ) to be used in place of the default .dcf file ( doctype .dcf ) for the current document's document type. name is the path and file name of the .dcf file, with or without a file extension. If you don't specify a file extension, Arbortext Editor searches for name with a .dcf file extension.

For example,

```
set dcffile="C:\doctypes\test\mydoctype.dcf"
```

## Related Topics

- • Document type configuration files



---

# set_debugcomposition

# set debugcomposition

set debugcomposition= { on | off}

When this option is on , Arbortext Editor creates a log directory for each publishing operation and stores the Event Log and intermediate files for the publishing request. After each publishing operation finishes, the log directory will be saved to a zip archive and then the directory will be deleted. The default is off .

When an application save directory is created (using Tools > Save Application ), the save directory will contain a file named compose.zip , which contains the zipped temporary directory for each publishing operation performed while set debugcomposition was set to on . When Arbortext Editor exits, the temporary files will be deleted.

For sites using Arbortext Publishing Engine to fulfill publishing requests from Arbortext Editor clients, refer to Programmer's Guide to Arbortext Publishing Engine and the Using Arbortext Publishing Engine for publishing documents online help topic.



---

# set_deepcontentsplitting

# set deepcontentsplitting

set deepcontentsplitting= { on | off | never}

This set option is used to enable and disable deep content splitting, which allows page breaks in table rows, algroups, and boxed regions. Deep content splitting is enabled using on , disabled using off . The default setting is on .

You can insert a _deepsplit tag pair to circumvent the off setting for set deepcontentsplitting using Format > Touchup > Deepsplit Region . To prevent deep content splitting overrides, set this command to never .

To disable deep content splitting in your document:

```
set deepcontentsplitting=off
```

## Related topic

- • Deep content splitting overview



---

# set_defaultfilter

# set defaultfilter

set defaultfilter= filterstring

This command specifies the default list of file types to display in the Filter menu (or pull-down) on the Open dialog box.

filterstring specifies a list of file types separated by a vertical bar “|”. There are two parts to each item, which are also separated by a vertical bar “|”. The first part is the string to display in the menu or pop-up menu. The second part is the corresponding pattern to use to filter the files displayed in the dialog box. Multiple patterns may be specified by separating them with a semicolon.

Example

```
set defaultfilter="SGML Files|*.sgm;*.sgml|\
HTML Files|*.htm;*.html|\
Text Files|*.txt|All Files|*.*"
```

## Related Topics

- • set asciiextension command

- • set htmlextension command

- • set sgmlextension command



---

# set_defaultprintdpi

# set defaultprintdpi

set defaultprintdpi= value

This command specifies the resolution value in images resulting from Arbortext Editor converting SVG and PVZ images for print and PDF output . value is a positive integer specifying the resolution in dpi (dots per inch). If defaultprintdpi is not set, Arbortext Editor assumes a value of 300 .

## Related Topics

- • set defaultscreendpi



---

# set_defaultscreendpi

# set defaultscreendpi

set defaultscreendpi= value

This command specifies the screen display resolution value for images resulting from Arbortext Editor converting SVG images to PNG images and for graphics files which do not have a resolution specified internally within the graphic. value is a positive integer specifying the resolution in dpi (dots per inch). If defaultscreendpi is not set, the default resolution values is 96 .

## Related Topics

- • set defaultprintdpi

- • APTCOPYGRAPHICEXTS



---

# set_deferotherreferenceupdates

# set deferotherreferenceupdates

set deferotherreferenceupdates= { on | off}

If this option is set to on Arbortext Editor will not update other references to entities, includes, or DMS objects which change if the other reference is in a document that is open in a window that doesn't have focus or is not open in any window. The reference without the focus will be updated when it gets the focus or if Arbortext Editor needs to update it (for example when saving the document or updating gentext for it).

If you open a file entity in its own window, turning this option on might make editing of the entity faster at the expense of not showing the most recent changes in the document that refers to the entity.



---

# set_deletespaces

# set deletespaces

set deletespaces= { on | off}

When this option is set to on (the default), Arbortext Editor will remove a space when a cut or delete operation results in two consecutive spaces. When this option is set to off , both spaces will remain. Setting the option to off is useful for developers that perform a delete and an insert in separate steps and do not want to lose the space.



---

# set_dialogdisplay

# set dialogdisplay

set dialogdisplay= { on | off}

If set to on , embedded XUI dialog boxes will be displayed in the Edit pane. If set to off , the XUI markup is displayed in the Edit pane. The default is on .



---

# set_dialogspath

# set dialogspath

set dialogspath= dir1 [: dirn ]

This command specifies a search path for dialog files that can be called from a custom application, such as one that uses the AOM Application.createDialogFromFile method. The default path is Arbortext-path \lib\dialogs . Each directory specified must be separated by a semicolon. You can specify the %D or %H symbolic parameters in the path list .

If an Arbortext-path \custom\dialogs subdirectory exists at startup, the custom\dialogs path is automatically prepended to the path for dialog files. Putting your custom dialog files in the \custom\dialogs subdirectory makes them automatically available, avoiding manual steps to add them to the path.

Example

```
set dialogspath="c:\mydialogs;%D"
```

You can use the append_dialogs_path function to update the dialog file path.

## Related Topics

- • option_path_list function



---

# set_diffattrmodcolor

# set diffattrmodcolor

set diffattrmodcolor= { inherit | colorname | # rgbspec }

This command determines the font color used in the Compare window to display attribute modifications. If inherit is set, elements with changed attributes are displayed in the font color specified by the FOSI. The value is either inherit , or a named color, or an RGB specification preceded by # . The default is inherit .

Examples

```
set diffattrmodcolor=inherit
set diffattrmodcolor=red
set diffattrmodcolor=#ff0000
```



---

# set_diffattrmodname

# set diffattrmodname

set diffattrmodname= name

This command allows you to specify the name of the tag/processing instruction that encloses attribute modifications in the Compare window.



---

# set_diffdelcolor

# set diffdelcolor

set diffdelcolor= { inherit | colorname | # rgbspec }

This command determines the color used in the Compare window to display text marked for deletion. If inherit is set, deleted elements are displayed in the color specified by the FOSI. The value is either inherit , or a named color, or an RGB specification preceded by # . The default is inherit .

Examples

```
set diffdelcolor=inherit
set diffdelcolor=red
set diffdelcolor=#ff0000
```



---

# set_diffdelname

# set diffdelname

set diffdelname= name

This command allows you to specify the name of the tag or processing instruction that encloses deleted text in the Compare window.



---

# set_diffencltype

# set diffencltype

set diffencltype= { pi | tag}

This command takes the value of pi if differences in the Compare window are to be enclosed within processing instructions. If tag is specified, the values of diffinsname , diffdelname , and diffattrmodname must all be valid elements of the DTD for the document being compared. Also, these elements must be able to appear anywhere in the document. The default is pi .



---

# set_diffentities

# set diffentities

set diffentities= { on | off}

If on is specified, entities will be expanded in the Compare window and the entity contents compared between the source and target documents. In this case, the expanded content appears in the Compare window. If the Compare document is saved, then the expanded entity content is flattened and saved in the Compare document.

If off is specified, the entity references are compared instead of their content. The default is off .



---

# set_diffignoreattrs

# set diffignoreattrs

set diffignoreattrs= { on | off}

When this command is set to on (the default), modifications to attributes are not reported in the Compare window.



---

# set_diffincludes

# set diffincludes

set diffincludes= { on | off}

If on is specified, files included using XML inclusions will be expanded in the Compare window and the contents will be compared between the source and target documents. In this case, the expanded content appears in the Compare window. If the Compare document is saved, then the expanded included content is flattened and saved in the Compare document.

If off is specified, XML inclusion references are compared instead of their content. The default is off .



---

# set_diffinscolor

# set diffinscolor

set diffinscolor= { inherit | colorname | # rgbspec }

This command determines the color used in the Compare window to display inserted text. If inherit is set, inserted text is displayed in the color specified by the FOSI. The value is either inherit , or a named color, or an RGB specification preceded by # . The default is inherit .

Examples

```
set diffinscolor=inherit
set diffinscolor=red
set diffinscolor=#ff0000
```



---

# set_diffinsname

# set diffinsname

set diffinsname= name

This command allows you to specify the name of the tag or processing instruction that encloses inserted text in the Compare window.



---

# set_diffmemory

# set diffmemory

set diffmemory= n

This option specifies the maximum memory allocation used by Arbortext Editor during document comparison processing. The value is in megabytes. The default value is 256. If memory allocation is insufficient, you'll get an error message instructing you to set a larger value.

## Related Topics

- • Document comparison overview



---

# set_diffstrikethrough

# set diffstrikethrough

set diffstrikethrough= { on | off}

This command controls the appearance of deleted text in the Compare window. When diffstrikethrough is set to on (the default), deleted text appears in the assigned color and in strike-though characters. When diffstrikethrough is set to off , deleted text appears in the assigned color and in regular characters.



---

# set_diffunderline

# set diffunderline

set diffunderline= { on | off}

This command controls the appearance of inserted text in the Compare window. When set to on (the default), inserted text appears in the assigned color and in underlined characters. When diffunderline is set to off , inserted text appears in the assigned color and in regular characters.



---

# set_ditacheckreferences

# set ditacheckreferences

set ditacheckreferences= { on | off}

This option determines whether the Arbortext Editor enhanced completeness checking for DITA documents opens referenced documents and performs the enhanced check on them as well as the current document. Set this option to on to check references during enhanced completeness checking and to off to just check the current document. The default is on . This option has global scope.

## Related Topics

- • Using check completeness with DITA documents



---

# set_ditaexpectedformats

# set ditaexpectedformats

set ditaexpectedformats=dita [;ditamap] [;xml] [;html] [;pdf] [;txt] [;sgm] [;sgml]

This option contains a semicolon-separated list of possible values for the DITA format attribute. The list is used during enhanced completeness checking for DITA documents when checking that the attribute has a valid value. The following default format values are used:

- • dita

- • ditamap

- • xml

- • html

- • pdf

- • txt

- • sgm

- • sgml

This option has global scope.

## Related Topics

- • Using check completeness with DITA documents



---

# set_ditahideids

# set ditahideids

set ditahideids= { on | off}

This option determines whether the ID option is displayed on the Resource Manager dialog's New Topic tab and whether IDs are displayed in the Resource Manager browser. Set this option to on to hide DITA IDs and to off to display IDs. The default is on . This option has global scope.



---

# set_ditaincludecommentsinrds

# set ditaincludecommentsinrds

set ditaincludecommentsinrds= { none | all | map | topic}

This option specifies whether authored comments are included in the Resolved Document for Styling (RDS).

- • none (default) — no comments are included

- • all — comments from maps and topics

- • map — comments from map only

- • topic — comments from topics only



---

# set_ditaincludemapsinrde

# set ditaincludemapsinrde

set ditaincludemapsinrde= { on | off}

This option determines whether the markup for DITA maps is included in an automatically generated resolved document for editing. If you use a custom document type for the resolved document for editing that includes DITA maps, the option also determines whether maps are included in the resolved document in this case. If you use a custom document type that does not include DITA maps, the option has no effect.

Set this option to on to include DITA map markup and to off to not include map markup. The default is off . This option has global scope.



---

# set_ditainsertallwarnings

# set ditainsertallwarnings

set ditainsertallwarnings= { off | n }

This option determines whether Arbortext Editor displays a warning dialog box when more than a designated number of topic references are being inserted into a DITA map in a single operation. The default is 20 . Set this option to off to prevent a warning dialog box from being displayed. Set this option to a different number to change the default threshold. Setting this option to 0 has the same effect as setting it to off . This option has global scope.

Examples

```
set ditainsertallwarnings=off
set ditainsertallwarnings=30
```



---

# set_ditakeybaselist

# set ditakeybaselist

set ditakeybaselist= URI [; URI ]

This option contains a semicolon-separated list of URIs of DITA maps containing key definitions. The keys in those maps are used to populate the Insert Key Reference dialog box and are also used to populate the Keyref field on the various Resource Manager tabs and versions when an object with a matching key is selected. This preference can be updated for a specific document using the Add/Remove Map dialog box. However, changes made to this preference are only persistent if the value is set from the Advanced Preferences dialog box or by using the command itself.

This option has document scope and does persist across sessions.

## Related Topics

- • Using keys and key references

- • set ditakeycontext command



---

# set_ditakeycontext

# set ditakeycontext

set ditakeycontext= URI

This option contains the URI of the source of key definitions for key references in the current document. You can also set this option explicitly or Arbortext Editor sets it automatically in some cases. For example, when a user opens a topic from within a map, Arbortext Editor automatically sets that topic's ditakeycontext value to the URI of the map. The elements in the topic with keyref attributes referencing keys will then use the key definitions defined in that map.

This map is also used, in addition to the maps set in the ditakeybaselist preference, to populate the Keyref field on the various Resource Manager tabs and versions. This option has document scope and does not persist across sessions.

## Related Topics

- • Using keys and key references

- • set ditakeybaselist command



---

# set_ditakeynamequalifier

# set ditakeynamequalifier

set ditakeynamequalifier= qualifier

This option contains a string that is automatically added as a prefix or suffix to the key names you enter from the Resource Manager ’s Key Definition tab. This helps ensure that your key names are unique. This option has document scope.

Whether the qualifier is added as a prefix or suffix is determined by how the qualifier string begins or ends. The following rules apply for key name qualifiers:

- • If a qualifier begins with a . or - , the qualifier is a suffix.

- • If a qualifier ends with a . or - , the qualifier is a prefix.

- • if a qualifier neither ends nor begins with a . or - , the qualifier is a suffix.

It is recommended that you use a suffix as the name qualifier and that you use a . to separate the parts of the qualifier.

Examples

If you set ditakeynamequalifier to the following value:

```
set ditakeynamequalifier=.dita.acme.com
```

Your key names will have a name qualifier suffix:

```
keyname
.dita.acme.com
```

If you set ditakeynamequalifier to the following value:

```
set ditakeynamequalifier=com.dita.acme.
```

Your key names will have a name qualifier prefix:

```
com.dita.acme.
keyname
```

## Related Topics

- • Using keys and key references



---

# set_ditakeyreffallback

# set ditakeyreffallback

set ditakeyreffallback= { on | off}

When entering key references via the Insert Key Reference dialog box, this option determines whether an @href and other attributes will also be added to the reference elements that are added, such as xrefs and links. The fallback markup is used when processing the topic during publishing. If the key reference cannot be resolved, the fallback markup is used to resolve the reference.

The default is on .

## Related Topics

- • Using keys and key references



---

# set_ditakeyrefui

# set ditakeyrefui

set ditakeyrefui= { on | off}

This option determines whether the user interface options for keys and key reference support are displayed in the Arbortext Editor interface. Set this option to on to display the key reference user interface and to off to hide the interface. The default is on . This option has global scope.

Refer to Using keys and key references in the Arbortext Editor help for details about the key reference user interface options.



---

# set_ditanewfilelang

# set ditanewfilelang

set ditanewfilelang= { lang | none}

This option determines the default language to which Arbortext Editor sets the value of the xml:lang attribute on the root tag of DITA maps and topics created from templates. If this preference is not set to a value, then the default language of the stylesheet associated with the document is used. If the default language of the stylesheet is en , then the system locale is used for the language.

If you set this preference to none , then no xml:lang value is set on new documents. However, this is not recommended. This option has global scope.

Examples

```
set ditanewfilelang=de
set ditanewfilelang=none
```



---

# set_ditapath

# set ditapath

set ditapath= d1 [; dn ]

This command specifies a list of directories to search for content referenced by DITA documents when their references do not specify either an absolute path name or a path name relative to the current document directory. Separate each directory in the DITA references path by a semicolon.

You can use symbolic parameters in the DITA references path. The DITA references resolved by this variable include topic references, content references, links, cross references, and any other DITA element that references content. The only exception to this is graphic references, as they are resolved using the set graphicspath option.

The initial setting is the value of the APTDITAPATH environment variable, if set. Otherwise, it defaults to the Arbortext-path \ditarefs directory. If a ditarefs subdirectory exists in either the Arbortext-path \application or Arbortext-path \custom directory, that subdirectory is also part of the default DITA references path.

The base URI for the current element and the document directory, if different from the base URI, are included by default before any directories on the DITA references path to resolve relative references. When any set ditapath directory parameter is set to a value of %^ , the document directory and the base URI for the current element will not be included when searching for DITA references. Only the paths specified will be searched.

The DITA references path can also be set in the File Locations category of the Tools > Preferences dialog box.

Examples

```
set ditapath="c:\\Program Files\\Arbortext\\documents\\dita;%^;c:\\DITA\\content"
```

A list of multiple directories must be enclosed in quotation marks.

You can use the append_dita_path function to update the DITA references path.

## Related Topics

- • Symbolic parameters in path list variables

- • File Locations preferences

- • option_path_list function



---

# set_ditareltableautoinsert

# set ditareltableautoinsert

set ditareltableautoinsert= { on | off}

This option determines whether a topic reference entered into a DITA relationship table through drag-and-drop is automatically put into the table column that matches the DITA topic type. Set this option to on to automatically put the topic reference into the matching table column and to off to put the topic reference into the column where the reference is dropped. The default is on . This option has global scope.



---

# set_ditasynctabs

# set ditasynctabs

set ditasynctabs= { on | off}

This option determines whether the Synchronize Location Across Tabs choice is on or off by default in the Resource Manager menus. The default is on . When set to on, the location you browse to on a Resource Manager tab is maintained when you switch to another tab or open a new Resource Manager dialog box. This option has global scope.



---

# set_ditatextkeyrefs

# set ditatextkeyrefs

set ditatextkeyrefs= { on | off}

This option determines whether non-linking DITA elements are included in the Insert Key Reference dialog box’s Insert option. The default is off . When set to on , non-linking elements that allow a key reference are included in the Insert option. This option has global scope.

## Related Topics

- • Using keys and key references

- • Insert Key Reference dialog box



---

# set_ditausenewrds

# set ditausenewrds

set ditausenewrds= { on | off}

This option specifies whether to use a new format Resolved Document for Styling (RDS) that was introduced in release 6.1 M030 for styling and publishing of DITA content.

The new format RDS displays certain differences to the old format:

- • No ReferredTopics section

- • Does not contain all the metadata from topics in the FlattenedMap section

- • Does not include some of the options controlled by dita.acl (control of certain customizations)

The new format RDS is used by default. Set the command to off to use the old format RDS.



---

# set_ditavaldebug

# set ditavaldebug

set ditavaldebug= { on | off}

This option determines whether debugging information is displayed in the DITAVAL Preview Window when a DITAVAL file is tested. Set this option to on to display debugging information. The default is off . This option has global scope.

When debugging is turned on, the following information is included in the DITAVAL Preview Window when testing a DITAVAL file:

- • A comment is inserted at the beginning of the document listing all of the DITAVAL files used to process the document.

- • A comment is inserted before any affected tags describing why the content was included, excluded, or flagged. The comment includes the DITAVAL file that the rule came from with a description of the rule.

- • All exclude rules are flagged in red with a yellow background and strikethrough text.

## Related Topics

- • Using DITAVAL files



---

# set_docmapcurrenttag

# set docmapcurrenttag

set docmapcurrenttag= { on | off}

This option controls how the oid_current_tag() and current_tag_name() ACL functions and the $tagname predefined variable determine the “current tag” in the Document Map view. It is provided for backward compatibility with certain pre-Adept 7.0 ACL scripts.

If this option is set to on (the default), Arbortext Editor determines the “current tag” per the following rules:

- • If the cursor is anywhere in the Edit view, the current tag is always the tag to the left of the cursor.

- • If the cursor is at the start of a line in the Document Map view (that is, between the element icon and the element name), the current tag is the element to the right of the cursor.

- • If the cursor is anywhere else in the Document Map, the current tag is the element to the left of the cursor.

If the option is set to off , then the current tag is always the tag to the left of the cursor in both the Document Map and Edit views.

If you have an ACL script from a pre-7.0 version of Adept that uses the current tag, you may want to add the set docmapcurrenttag=off command to the beginning of the script. This will guarantee that the “current tag” will always be to the left of the cursor, even if the cursor is at the start of a line in the Document Map view. When your script completes, it should execute the set docmapcurrenttag=on command to restore the default value.

If your script relies on a user's interaction with Arbortext Editor , you may wish to leave docmapcurrenttag set to its default value of on .

For example, assume that your script makes specific modifications to element attributes for the current element (tag). If a user executes your script using a menu command or control-key, you are relying on them to position the cursor such that they modify the attributes for the desired element. In this case, you would want to exploit the intuitive nature of “current tag” determination in the Document Map view.

## Related Topics

- • oid_current_tag function

- • current_tag_name function

- • change_tag command

- • delete_tag command

- • modify_tag command

- • Predefined variables ( $tagname variable)



---

# set_docmapendtags

# set docmapendtags

set docmapendtags= { full | partial | none}

Use this set command to control the display of end tags in the Document Map view. This window-specific setting is retained whether a Document Map view is in the current window or not. If the Document Map is currently disabled, this command will have not visible affect until the Document Map is enabled in that window.

The valid settings are:

- • full — Shows both the end tag icon and element name.

- • partial — Shows the end tag icon only.

- • none — Shows neither the end tag icon nor the element name.



---

# set_docmapgentext

# set docmapgentext

set docmapgentext= { on | off}

This command determines if generated text is displayed in the Document Map pane within the Edit window. When set to on , the text is displayed, when set to off it is not. The default is on .

When displayed, the generated text will update according to the setting of the gentextautoupdate option.

## Related Topics

- • set gentextautoupdate



---

# set_docmaphighlight

# set docmaphighlight

set docmaphighlight= { colorname | # rgbspec }

This command specifies the color value used to highlight the Document Map line containing the cursor. The value is either a named color or an RGB specification preceded by # . The default is no highlighting. Set the value of this option to default to remove any existing highlighting.

The docmaphighlight command is an advanced preference with global scope. When you edit this preference, click on the down arrow to display the Color palette .

Examples

```
set docmaphighlight=blue
set docmaphighlight=#dd00dd
```



---

# set_docmapmode

# set docmapmode

set docmapmode= { on | off}

If set to on , the current window is split into two side by side panes with the Document Map in the left view and the document in the right view. If set to off , the current window consists of a single view containing the document (not the Document Map).

The position of the split between the windows is set by the docmappercent option. To turn the Document Map on/off in the current view, use the docmapview option.

## Related Topics

- • set viewmode command

- • set docmapview command

- • set docmappercent command



---

# set_docmappastecaret

# set docmappastecaret

set docmappastecaret= { on | off}

This option determines the position of the caret (cursor) in the Document Map view after a paste , insert_string , or insert_entity command or insert() function completes. This option is provided for backward compatibility with certain pre-Adept 7.0 ACL scripts.

In the Edit view, the caret is always positioned immediately after the pasted region.

In the Document Map view, the caret is placed immediately before the pasted region if the docmappastecaret option is set to on (the default). This default setting in the Document Map minimizes horizontal scrolling after a paste or insert operation. If docmappastecaret is set to off , the caret is positioned at the end of the region after the paste or insert.

If you have an ACL script from a pre-7.0 version of Adept that relies on the cursor being placed after pasted regions, you should set the set docmappastecaret=off command at the beginning of the script. This will guarantee that the “current tag” will always be to the left of the cursor, even if the cursor is at the start of a line in the Document Map view. When your script completes, it should execute the set docmappastecaret=on command to restore the default value.

## Related Topics

- • paste command

- • insert_string command

- • insert_entity alias

- • insert function



---

# set_docmappercent

# set docmappercent

set docmappercent= n

This option determines the percentage of the window devoted to the Document Map or Column view display when it is activated. The value n must be in the range 0 to 100 . If 0 , the Document Map is hidden, if 100 the Document Map will occupy the entire window. The default is 33 percent.

n is a number, excluding a percent ( % ) symbol.



---

# set_docmapshowattrs

# set docmapshowattrs

set docmapshowattrs= { on | off}

This option controls the display of attributes in the Document Map or Column view. This window-specific setting is retained whether a Document Map or Column view is in the current window or not. If the Document Map or Column view is currently disabled, this command will have no visible effect until the view is enabled in that window.

The current valid settings are:

- • on — Displays each element attribute in the Document Map or Column view as a single non-wrapped line.

- • off — Displays no element attributes in the Document Map or Column view. This is the default setting.

This setting is the same as choosing the View > Expand Attributes menu choice.



---

# set_docmapside

# set docmapside

set docmapside= { left | right | top | bottom}

This option determines where Arbortext Editor will place the Document Map or Column view in a split window view. The default is left in most locales. However, in the Arabic and Hebrew locales where right-to-left editing is required, the default is right .



---

# set_docmapsync

# set docmapsync

set docmapsync= { on | off}

This option determines whether Arbortext Editor will automatically synchronize when a document is displayed in both an Edit view and a Document Map or Column view. This command has the same affect as choosing the Synchronized Views preference in the View category of the Preferences dialog box.



---

# set_docmaptextdisplay

# set docmaptextdisplay

set docmaptextdisplay= { none | nowrap | wrap}

This command controls the appearance of the content text displayed in the Document Map view. This window-specific setting is retained whether a Document Map view is in the current window or not. If the Document Map is currently disabled, this command will have no visible effect until the Document Map is enabled in that window.

Valid settings are:

- • none — Displays no content text in the Document Map view (Displays structure only).

- • nowrap — Displays content text in the Document Map view as single non-wrapped lines. Using this setting is the same as choosing the View⇒Document Map⇒Line Text in Map menu option. You can control how your content text is lined up with the docmapusetabs option.

- • wrap — Displays content text in the Document Map view text-wrapped lines. The width of the text-wrap column is controlled by the docmapwidth option. Using this setting is the same as choosing the View⇒Document Map⇒Wrap Text in Map menu option. You can control how your content text is lined up with the docmapusetabs option.

## Related Topics

- • set docmapwrapwidth command

- • set docmapusetabs command



---

# set_docmapusetabs

# set docmapusetabs

set docmapusetabs= { on | off}

This command controls how your Document Map content text displays when using the nowrap and wrap settings for docmaptextdisplay . This window-specific setting is retained whether a Document Map view is in the current window or not. If the Document Map is currently disabled, this command will have not visible affect until the Document Map is enabled in that window.

Valid settings are:

- • on — Lines up the content text in hierarchical fashion.

- • off — Does not line up content text; content text starts a fixed distance from the end of the element name.

## Related Topics

- • set docmaptextdisplay command



---

# set_docmapview

# set docmapview

set docmapview= { on | off}

When set to on , the current view changes to a Document Map.

To split the window and show the Document Map in the left view, use the docmapmode option.

## Related Topics

- • set view command

- • set docmapmode command



---

# set_docmapwrapwidth

# set docmapwrapwidth

set docmapwrapwidth= width

This command controls how your Document Map content text lines up when using the wrap setting for docmaptextdisplay . This window-specific setting is retained whether a Document Map view is in the current window or not. If the Document Map is currently disabled, this command will have no visible affect until the Document Map is enabled in that window.

Enter the desired column width for the content text in width argument. (For example, 8cm , 5in , and so on.) The default units is inches. Settings that would result in a content text column of less than two (2) inches are ignored.

## Related Topics

- • set docmaptextdisplay command



---

# set_doctypecachesize

# set doctypecachesize

set doctypecachesize= size

This command controls the size of an internal cache that retains document type information and associated stylesheets during a Arbortext Editor or Arbortext Publishing Engine session. The first time a document is opened, the associated document type and stylesheet are compiled (if needed) and loaded. When the doctypecachesize option is enabled, an empty document for the same document type and stylesheet is created and loaded in the cache. This causes Arbortext Editor and Arbortext Publishing Engine to retain the associated document type and stylesheet, improving performance when another document of the same type is opened.

The default cache size is 20 , which is the number of document type and stylesheet pairs retained in the cache. If the cache size is exceeded, the oldest document type and stylesheet pair is removed from the cache. You can set the cache to a value between 0 and 50 . Setting the cache size to 0 clears and disables the cache, causing a document's document type and stylesheet to be loaded every time you open a document.



---

# set_documenttypewarnings

# set documenttypewarnings

set documenttypewarnings= { on | off}

Specifies whether warnings should be emitted when parsing a DTD or Schema.

- • on — The default when running Arbortext Architect . Warnings are reported.

- • off — The default when running Arbortext Editor . Warnings are suppressed.

The potential warnings include:

- • A notation already exists

- • An attribute already exists

- • Contradictory encoding

- • Undeclared elements referenced in a content model

- • Undeclared elements referenced in an attribute



---

# set_editduringformat

# set editduringformat

set editduringformat= { yes | no | prompt}

This option determines whether Arbortext Editor allows the user to continue editing a document while it's being formatted for a publishing request. The settings are:

- • yes — Allow editing.

- • no — Do not allow editing. When set to no, Arbortext Editor reports the document is read only.

- • prompt — Prompt the user to decide whether to allow editing. This is the default setting.



---

# set_editfontpercent

# set editfontpercent

set editfontpercent= n

This command increases or decreases the point sizes of all fonts in the Edit window to the percentage specified, subject to the availability of fonts. By default, fonts are displayed at 92% of their point size. Fonts cannot be displayed at less than 40% of their point size.

n is a number, excluding a percent ( % ) symbol.

## Related Topics

- • set fontpercent command

- • set helpfontpercent command

- • set tagfontpercent command



---

# set_editselectionrecordlength

# set editselectionrecordlength

set editselectionrecordlength= { n | infinity}

The editselectionrecordlength enables you to set the record length (line breaks) of the part of a document selected in Arbortext Editor . Only the selected part of a document is affected by this command. The record length is set in the XML or SGML source. If you set the record length to infinity , no line breaks are included in the source of the selection.

Examples

```
set editselectionrecordlength=70
set editselectionrecordlength=infinity
```



---

# set_emptyelementswarnings

# set emptyelementswarnings

set emptyelementswarnings= { on | off}

The emptyelementswarnings option controls whether Completeness Checking tests for the presence of empty elements. Its default value is off .

## Related Topics

- • Check completeness

- • Empty Elements dialog box



---

# set_encodemediafilenames

# set encodemediafilenames

set encodemediafilenames= { on | off}

The encodemediafilenames option controls whether filenames of media objects, for example graphics, may be encoded to remove non-ASCII characters.

Encoded filenames are longer than their original versions and may exceed Windows maximum file path lengths. This can cause issues with copy and move actions during publishing.

The default value is on .



---

# set_entityinputconvert

# set entityinputconvert

set entityinputconvert= { on | off}

The entityinputconvert option controls how Arbortext Editor stores character entities in memory when a document is opened, or when character entities are pasted or inserted in a document. When entityinputconvert is set to on , which is the default, Arbortext Editor converts character entity references to characters. This method saves memory space.

When entityinputconvert is set to off , Arbortext Editor stores character entities in a special data structure, which can be displayed in the Edit window as a character. This preserves the identity of the character entity, so that it can be written out in the same way that it was read in.

## Related Topics

- • set entityoutputconvert command

- • set writenonasciichar command



---

# set_entitylist

# set entitylist

set entitylist= c1 [ cn ]

This command specifies the list of character entities to display in the tool bar Insert Symbol pulldown list. The entities are separated by a space character. The list can contain numeric references as well as character entity names. When a numeric reference is specified, the character will be shown in the Insert Symbol pulldown list if the character is defined in charent.cf . If the character is not defined in charent.cf , the hexadecimal value will be listed instead. If entitylist is set to a null string, no entities are displayed.

Entities which are not valid for a given document are ignored, although they remain in the option list. Each new document is initialized to this list, which may be overridden by a processing instruction in the file.

Examples:

```
set entitylist="alpha beta copy trade"
set entitylist="alpha &#x2126; #255"
set entitylist=""
```



---

# set_entityoutputconvert

# set entityoutputconvert

set entityoutputconvert= { on | off}

The entityoutputconvert option controls how Arbortext Editor writes out character entities it stores in special data structures. It works with the entityinputconvert and writenonasciichar options.

If entityoutputconvert is set to off , which is the default, Arbortext Editor writes out character entities in the same format as they were read in.

If entityoutputconvert is set to on , Arbortext Editor writes out character entities as characters, numeric character references, or entity references, depending on the value of the writenonasciichar option.

## Related Topics

- • set entityinputconvert command

- • set writenonasciichar command

- • write command



---

# set_entitypath

# set entitypath

set entitypath= d1 [: dn ]

This command specifies a list of directories to search for entities that do not specify an absolute path name or a path name relative to the current directory (each directory separated by a semicolon). The initial setting is the value of the APTENTPATH environment variable if set. Otherwise, it defaults to the entities subdirectory of Arbortext-path . This path option supports file entities as well. Use %D to refer to the Arbortext-path \entities subdirectory. Use %B to refer to directories relative to the current document’s directory.

The document's parent directory and current working directory are included by default in the directories searched for entities. When any set entitypath directory parameter is set to a value of %^ , the parent document directory and the current working directory will not be included when searching for entities. Only the paths specified will be searched.

If there is an Arbortext-path \custom\entities subdirectory at startup, the \custom\entities path is automatically prepended to the entities path. Putting your entity files in the \custom\entities subdirectory makes them automatically available, avoiding manual steps to add them to the path.

The Arbortext-path \custom\entities directory is also automatically included if you use %D in the path.

Examples:

```
set entitypath="c:\\Program Files\\Arbortext\\editor\\entities;%^;
c:\\Arbortext\\editor\\packages\\entities"
```

The list of multiple directories must be enclosed in quotation marks.

You can use the append_entity_path function to update the entities path.

## Related Topics

- • append_entity_path function

- • option_path_list function

- • APTENTPATH environment variable

- • Symbolic parameters in path list variables



---

# set_entityscan

# set entityscan

set entityscan= { on | off}

This command controls the default for the entityscan parameter on the spell and find commands and the default setting for the Search Entities check box on the Find and Spelling dialog boxes.

If entityscan is set on , file entities will be scanned during spelling check and find operations. You can override this default setting by using the -es or -noes options with the spell and find ACL commands, or by changing the Search Entities check box in the Find and Spelling dialog boxes.

The default is on .

## Related Topics

- • find command

- • spell command



---

# set_epubinstalldir

# set epubinstalldir

set epubinstalldir= path

This command specifies the directory in which Calibre is installed.

A valid Calibre install directory must contain the files ebook-convert.exe and ebook-viewer.exe .



---

# set_epubstylesheet

# set epubstylesheet

set epubstylesheet= { name | none}

This command specifies the stylesheet to be used as the default for the Publish > For EPUB option on the File menu.

name is the path and file name of a .style or .xsl stylesheet file. If you don't specify an extension for the stylesheet, Arbortext Editor first looks for a .style file, and then a .xsl file.

The stylesheet ID processing instruction must specify epub as the publishing type.

If you specify only the stylesheet's base name, Arbortext Editor first looks for the file in the document directory, and then looks in the document type directory. If you specify a relative path (other than one that just gives the base name), Arbortext Editor looks for the file using the given path relative to the current working directory.

If you are using Arbortext Publishing Engine for publishing, it must be able to locate the stylesheet. If a document references a stylesheet using a URL, that stylesheet can be found by both Arbortext Editor and Arbortext Publishing Engine . Stylesheets that are available on the Arbortext PE server appear in the Stylesheet selection fields preceded by the notation (pe) .

When you are using Arbortext Publishing Engine , be aware of the following when setting a value for this option:

- • If you try to set the location to a local path for any type of published output, you will get an error that the stylesheet is not the name of a stylesheet on the server. The following example produces an error if Arbortext Publishing Engine publishing is enabled:

- • If you try to set the location to a stylesheet file name only (no path), Arbortext Publishing Engine looks for a stylesheet with a matching name. The following example would succeed if a stylesheet of the same name exists in a location where the Arbortext PE server looks for stylesheets.

If epubstylesheet is set to none or is not set, Arbortext Editor and Arbortext Publishing Engine use the Editor/Default stylesheet.

Examples

```
set epubstylesheet=memo2
set epubstylesheet=~/mydocs/memo/memo2.style
set epubstylesheet=http://www.some_site.com/examples/techman.xsl
```

## Related Topics

- • set stylesheet command

- • Stylesheets overview

- • Displaying your XML document in a browser

- • Configuring stylesheet order in a list

- • Using Arbortext Publishing Engine for publishing documents

- • Opening, referencing, and saving files



---

# set_equationdisplay

# set equationdisplay

set equationdisplay= { on | off}

This command determines whether equations will be displayed in the Edit window. on is the default.

equations is a synonym for equationdisplay .



---

# set_expandinclusions

# set expandinclusions

This option determines whether XML inclusions will be expanded when a document is opened. The default value is true . If the value is false , when opening a document to be displayed, XML inclusions will not be expanded and the inclusion markup will appear in the document. (In Arbortext Editor , you can choose View > Included Object to individually expand the inclusions.



---

# set_expressions

# set expressions

set expressions= { on | off}

This option allows or disallows the use of regular expressions when specifying a string with the find , substitute , caret , and window commands without the -e modifier. The default is off .

This option also specifies the default values for matching patterns with the Find/Replace dialog box.

## Related Topics

- • Using regular expressions

- • Searching for patterns



---

# set_extendselection

# set extendselection

set extendselection= { on | off}

When this option is set to on , it turns on extend selection mode and displays EXT in the status bar. When enabled, any cursor movement, such as using the arrow keys, causes the highlighted region to be extended to the new cursor position. This mode remains in effect until extendselection is set to off , which ends the selection. The default is off .

## Related Topics

- • caret command



---

# set_featureChangetracking

# set featureChangetracking

set featureChangetracking= { on | off}

This command enables ( on ) and disables ( off ) the user interface and underlying program for the change tracking feature. This option can only be changed in the installprefs.acl file that is loaded at program startup. The default installprefs.acl file is located in the Arbortext-path \lib directory of your Arbortext Editor installation directory.

If you create a custom installprefs.acl , copy the default Arbortext-path \lib\installprefs.acl file, and set the set featureChangetracking command.

You can make a custom installprefs.acl file automatically available by putting it in the user's Arbortext-path \custom\lib directory to load it automatically upon startup (avoiding manual steps to add it to the path).

## Related topic

- • APTINSTALLPREFS environment variable



---

# set_featureDMS

# set featureDMS

set featureDMS= { on | off}

This command enables ( on ) and disables ( off ) the user interface and underlying program for the PTC Server connection . This command must be included in the installprefs.acl file that is loaded at program startup. The default installprefs.acl file is located in the Arbortext-path /lib directory.

You can make a custom installprefs.acl file automatically available by putting it in the user's Arbortext-path \custom\lib directory to load it automatically upon startup (avoiding manual steps to add it to the path).

## Related Topics

- • Product options

- • APTINSTALLPREFS environment variable



---

# set_featureImportExport

# set featureImportExport

set featureImportExport= { on | off}

This command enables ( on ) and disables ( off ) Arbortext Import/Export . This option can only be changed in the installprefs.acl file that is loaded at program startup. The default installprefs.acl file is located in the Arbortext-path \lib directory of your Arbortext Editor installation directory.

If you create a custom installprefs.acl , copy the default Arbortext-path \lib\installprefs.acl file, and set the set featureImportExport command.

You can make a custom installprefs.acl file automatically available by putting it in the user's Arbortext-path \custom\lib directory to load it automatically upon startup (avoiding manual steps to add it to the path).



---

# set_featurePrintPublishing

# set featurePrintPublishing

set featurePrintPublishing= { on | off}

This command enables ( on ) and disables ( off ) the user interface and underlying program for the Print Composer product option. This option can only be changed in the installprefs.acl file that is loaded at program startup. The default installprefs.acl file is located in the Arbortext-path \lib directory of your Arbortext Editor installation directory.

If you create a custom installprefs.acl , copy the default Arbortext-path \lib\installprefs.acl file, and set the set featurePrintPublishing command.

You can make a custom installprefs.acl file automatically available by putting it in the user's Arbortext-path \custom\lib directory to load it automatically upon startup (avoiding manual steps to add it to the path).

## Related Topics

- • Product options

- • APTINSTALLPREFS environment variable



---

# set_featureWebPublishing

# set featureWebPublishing

set featureWebPublishing= { on | off}

This command enables ( on ) and disables ( off ) the user interface and underlying program for the Web/Wireless Composer product option. This option can only be changed in the installprefs.acl file that is loaded at program startup. The default installprefs.acl file is located in the Arbortext-path \lib directory of your Arbortext Editor installation directory.

If you create a custom installprefs.acl , copy the default Arbortext-path \lib\installprefs.acl file, and set the set featureWebPublishing command.

You can make a custom installprefs.acl file automatically available by putting it in the user's Arbortext-path \custom\lib directory to load it automatically upon startup (avoiding manual steps to add it to the path).

## Related Topics

- • Product options

- • APTINSTALLPREFS environment variable



---

# set_fileentityfontcolor

# set fileentityfontcolor

set fileentityfontcolor= { inherit | colorname | # rgbspec }

This command determines the font color used to display file entities in the Edit window. If inherit is set, the file entities are displayed the same as the text of the Edit window document. The value is either inherit , or a named color, or an RGB specification preceded by # . The default is inherit .

You can determine whether Arbortext Editor ignores this setting by using the set usecolorsettings option.

Examples

```
set fileentityfontcolor=inherit
set fileentityfontcolor=red
set fileentityfontcolor=#ff0000
```



---

# set_fileentitymarkers

# set fileentitymarkers

set fileentitymarkers= { none | full | partial | default}

This command determines the display of file entity markup in the Edit window document.

- • default — File entity markup takes on the same setting as the Edit window document tag display

- • none — (The default.) No file entity tags or markers are displayed.

- • full — All file entity markup tags and markers are displayed.

- • partial — Only the file entity markers around the file entity are displayed.

- • icon — Only icons and fully-collapsed entity content are displayed.

- • hide — Only file entity icons are displayed.



---

# set_filelist

# set filelist

set filelist= f1 [ f1 , label ] [; f2 ; f3 ;…; f8 ] [; f2 , label ; f3 , label ;…; f8 , label ]

This command specifies the list of file names to display in the File menu as the most recently opened files. You can specify up to eight file names separated by the path list separator character (a semicolon). Each file name should be an absolute path name. You can supply an optional label to display in the list of file names instead of the path to the file. The label must follow the path name and be separated from the path name by a comma (',').

Arbortext Editor automatically updates this list each time a new document is opened. If set to a null string, no files will be listed in the File menu.

Examples

```
set filelist="C:\docs\art.xml;C:\packages\_main.acl"
set filelist="C:\process\initial.xml,Initial Process;
C:\process\final.xml,Final Process"
set filelist=""
```



---

# set_filereference

# set filereference

set filereference= { xinclude | entity}

This set command specifies the method that will be used for inserting file references. The default value is xinclude indicating to insert references as XML inclusions. Set the value to entity to insert file entity references.



---

# set_fmtfaultfloat

# set fmtfaultfloat

set fmtfaultfloat= { ignore | report | stopafterpass | stopatonce}

This command determines how a float formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.



---

# set_fmtfaultgraphicoverset

# set fmtfaultgraphicoverset

set fmtfaultgraphicoverset= { ignore | report | stopafterpass | stopatonce}

This command determines how a graphic overset (horizontal) formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtthreshgraphicoverset command



---

# set_fmtfaulthardkeeps

# set fmtfaulthardkeeps

set fmtfaulthardkeeps= { ignore | report | stopafterpass | stopatonce}

This command determines how a hard keeps formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.



---

# set_fmtfaulthdrftroverset

# set fmtfaulthdrftroverset

set fmtfaulthdrftroverset= { ignore | report | stopafterpass | stopatonce}

This command determines how a header or footer overset formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtthreshhdrftroverset command



---

# set_fmtfaultlineoverset

# set fmtfaultlineoverset

set fmtfaultlineoverset= { ignore | report | stopafterpass | stopatonce}

This command determines how a line overset formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtthreshlineoverset command



---

# set_fmtfaultlineunderfull

# set fmtfaultlineunderfull

set fmtfaultlineunderfull= { ignore | report | stopafterpass | stopatonce}

This command determines how a line underfull formatting fault is handled while formatting a document instance. The available options are:

- • ignore — (the default) Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.



---

# set_fmtfaultoverstretched

# set fmtfaultoverstretched

set fmtfaultoverstretched= { ignore | report | stopafterpass | stopatonce}

This command determines how a overstretched text formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtthreshoverstretched command



---

# set_fmtfaultpageoverset

# set fmtfaultpageoverset

set fmtfaultpageoverset= { ignore | report | stopafterpass | stopatonce}

This command determines how a page overset formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtthreshpageoverset command



---

# set_fmtfaultpageunderfull

# set fmtfaultpageunderfull

set fmtfaultpageunderfull= { ignore | report | stopafterpass | stopatonce}

This command determines how a page underfull formatting fault is handled while formatting a document instance. The available options are:

- • ignore — (the default) Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtthreshpageunderfull command



---

# set_fmtfaultsoftkeeps

# set fmtfaultsoftkeeps

set fmtfaultsoftkeeps= { ignore | report | stopafterpass | stopatonce}

This command determines how a soft keeps formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtthreshsoftkeeps command



---

# set_fmtfaulttablehorizoverset

# set fmtfaulttablehorizoverset

set fmtfaulttablehorizoverset= { ignore | report | stopafterpass | stopatonce}

This command determines how a table horizontal overset formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtthreshtablehorizoverset command



---

# set_fmtfaulttablevertoverset

# set fmtfaulttablevertoverset

set fmtfaulttablevertoverset= { ignore | report | stopafterpass | stopatonce}

This command determines how a table vertical overset (in rows) formatting fault is handled while formatting a document instance. The available options are:

- • ignore — Do not log the fault; do not display the fault in the Formatter Messages window.

- • report — (the default) Log the fault and display the fault in the Formatter Messages window.

- • stopafterpass — Stop formatting after the end of the current formatting pass.

- • stopatonce — Stop formatting immediately.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtthreshtablevertoverset command



---

# set_fmtthreshgraphicoverset

# set fmtthreshgraphicoverset

set fmtthreshgraphicoverset= size

This command sets the threshold for determining a graphic overset (horizontal) formatting fault while formatting a document instance. The size argument is a non-negative distance and unit specification. Valid units of measurement are points, picas, millimeters, centimeters, and inches. The default setting is 0pt .

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

Examples

```
set fmtthreshgraphicoverset=10pt
set fmtthreshgraphicoverset=2pi
set fmtthreshgraphicoverset=7.5mm
set fmtthreshgraphicoverset=1.1cm
set fmtthreshgraphicoverset=0.125in
```

## Related Topics

- • set fmtfaultgraphicoverset command



---

# set_fmtthreshhdrftroverset

# set fmtthreshhdrftroverset

set fmtthreshhdrftroverset= size

This command sets the threshold for determining a header/footer overset formatting fault while formatting a document instance. The size argument is a non-negative distance and unit specification. Valid units of measurement are points, picas, millimeters, centimeters, and inches. The default setting is 0pt .

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

Examples

```
set fmthreshhdrftroverset=10pt
set fmtthreshhdrftroverset=2pi
set fmtthreshhdrftroverset=7.5mm
set fmtthreshhdrftroverset=1.1cm
set fmtthreshhdrftroverset=0.125in
```

## Related Topics

- • set fmtfaulthdrftroverset command



---

# set_fmtthreshlineoverset

# set fmtthreshlineoverset

set fmtthreshlineoverset= size

This command sets the threshold for determining a line overset formatting fault while formatting a document instance. The size argument is a non-negative distance and unit specification. Valid units of measurement are points, picas, millimeters, centimeters, and inches. The default setting is 0pt .

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

Examples

```
set fmtthreshlineoverset=10pt
set fmtthreshlineoverset=2pi
set fmtthreshlineoverset=7.5mm
set fmtthreshlineoverset=1.1cm
set fmtthreshlineoverset=0.125in
```

## Related Topics

- • set fmtfaultlineoverset command



---

# set_fmtthreshoverstretched

# set fmtthreshoverstretched

set fmtthreshoverstretched= { min | med | max}

This command sets the threshold for determining an overstretched text formatting fault while formatting a document instance. The available options are:

- • min — Any overstretched text is considered a format fault.

- • med — (the default) Up to a medium stretch is not considered a fault.

- • max — No amount of stretch is considered a fault.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtfaultoverstretched command



---

# set_fmtthreshpageoverset

# set fmtthreshpageoverset

set fmtthreshpageoverset= size

This command sets the threshold for determining a page overset formatting fault while formatting a document instance. The size argument is a non-negative distance and unit specification. Valid units of measurement are points, picas, millimeters, centimeters, and inches. The default setting is 0pt .

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

Examples

```
set fmtthreshpageoverset=10pt
set fmtthreshpageoverset=2pi
set fmtthreshpageoverset=7.5mm
set fmtthreshpageoverset=1.1cm
set fmtthreshpageoverset=0.125in
```

## Related Topics

- • set fmtfaultpageoverset command



---

# set_fmtthreshpageunderfull

# set fmtthreshpageunderfull

set fmtthreshpageunderfull= size

This command sets the threshold for determining a page underfull formatting fault while formatting a document instance. The size argument is a non-negative distance and unit specification. Valid units of measurement are points, picas, millimeters, centimeters, and inches. The default setting is 0pt .

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

Examples

```
set fmtthreshpageunderfull=10pt
set fmtthreshpageunderfull=2pi
set fmtthreshpageunderfull=7.5mm
set fmtthreshpageunderfull=1.1cm
set fmtthreshpageunderfull=0.125in
```

## Related Topics

- • set fmtfaultpageunderfull command



---

# set_fmtthreshsoftkeeps

# set fmtthreshsoftkeeps

set fmtthreshsoftkeeps= { 1 | 2 | 3 | 4 | 5 | 6}

This command sets the threshold for determining a soft keeps formatting fault while formatting a document instance. The available options are integers from 1 to 6 . The default setting is 1 .

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

## Related Topics

- • set fmtfaultsoftkeeps command



---

# set_fmtthreshtablehorizoverset

# set fmtthreshtablehorizoverset

set fmtthreshtablehorizoverset= size

This command sets the threshold for determining a table overset (horizontal) formatting fault while formatting a document instance. The size argument is a non-negative distance and unit specification. Valid units of measurement are points, picas, millimeters, centimeters, and inches. The default setting is 0pt .

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

Examples

```
set fmtthreshtablehorizoverset=10pt
set fmtthreshtablehorizoverset=2pi
set fmtthreshtablehorizoverset=7.5mm
set fmtthreshtablehorizoverset=1.1cm
set fmtthreshtablehorizoverset=0.125in
```

## Related Topics

- • set fmtfaulttablehorizoverset command



---

# set_fmtthreshtablevertoverset

# set fmtthreshtablevertoverset

set fmtthreshtablevertoverset= size

This command sets the threshold for determining a table overset (vertical, in rows) formatting fault while formatting a document instance. The size argument is a non-negative distance and unit specification. Valid units of measurement are points, picas, millimeters, centimeters, and inches. The default setting is 0pt .

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is sent to the Arbortext PE server with a publishing request and applied. After the request is fulfilled, the setting for this option on the server reverts to its last set value.

Examples

```
set fmtthreshtablevertoverset=10pt
set fmtthreshtablevertoverset=2pi
set fmtthreshtablevertoverset=7.5mm
set fmtthreshtablevertoverset=1.1cm
set fmtthreshtablevertoverset=0.125in
```

## Related Topics

- • set fmtfaulttablevertoverset command



---

# set_fontcoloraqua

# set fontcoloraqua

set fontcoloraqua= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named aqua . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorblack

# set fontcolorblack

set fontcolorblack= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named black . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorblue

# set fontcolorblue

set fontcolorblue= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named blue . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorbrown

# set fontcolorbrown

set fontcolorbrown= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named brown . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorgray

# set fontcolorgray

set fontcolorgray= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named gray . For backward compatibility, gray is a synonym for gray3 . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorgray1

# set fontcolorgray1

set fontcolorgray1= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named gray1 . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorgray2

# set fontcolorgray2

set fontcolorgray2= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named gray2 . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorgray3

# set fontcolorgray3

set fontcolorgray3= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named gray3 . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorgray4

# set fontcolorgray4

set fontcolorgray4= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named gray4 . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorgray5

# set fontcolorgray5

set fontcolorgray5= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named gray5 . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorgreen

# set fontcolorgreen

set fontcolorgreen= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named green . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorlime

# set fontcolorlime

set fontcolorlime= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named lime . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolormaroon

# set fontcolormaroon

set fontcolormaroon= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named maroon . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolornavy

# set fontcolornavy

set fontcolornavy= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named navy . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorolive

# set fontcolorolive

set fontcolorolive= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named olive . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolororange

# set fontcolororange

set fontcolororange= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named orange . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorred

# set fontcolorred

set fontcolorred= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named red . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorteal

# set fontcolorteal

set fontcolorteal= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named teal . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorviolet

# set fontcolorviolet

set fontcolorviolet= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named violet . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcolorwhite

# set fontcolorwhite

set fontcolorwhite= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named white . The value is either a named color or an RGB specification preceded by # .



---

# set_fontcoloryellow

# set fontcoloryellow

set fontcoloryellow= { colorname | # rgbspec }

This preference determines the color value used to display the font (foreground) color named yellow . The value is either a named color or an RGB specification preceded by # .



---

# set_fontpercent

# set fontpercent

set fontpercent= n

This command increases or decreases the point sizes of all fonts in the currently active window to the percentage specified, subject to the availability of fonts. By default, fonts are displayed at 92% of their point size. Fonts cannot be displayed at less than 40% of their point size.

n is a number, excluding a percent ( % ) symbol.

## Related Topics

- • set editfontpercent command

- • set helpfontpercent command

- • set tagfontpercent command



---

# set_formatsnapshot

# set formatsnapshot

set formatsnapshot= { on | off}

When the set formatsnapshot command is set to on , the contents of the cache directory is saved for each formatting pass made on the document. If you report a problem to PTC Technical Support, you may be instructed to run this command and gather the data for analysis. This command works for both local and Arbortext Publishing Engine publishing. The default is off .



---

# set_formatstatus

# set formatstatus

set formatstatus= { on | off}

When the set formatstatus command is set to on , Arbortext Editor displays format status messages in the right side of the status bar of the Edit window.

When set to off , these messages are disabled. The default value is on for all document types except those that have a profiling configuration file.



---

# set_formatwarnings

# set formatwarnings

set formatwarnings= { on | off}

When this is set to on , any warning messages produced when the document is formatted are displayed in a window of their own. off is the default.

When this option is set for Arbortext Editor clients using Arbortext Publishing Engine for publishing documents , the setting is applied to a publishing request sent to the Arbortext PE server .



---

# set_fosiedit

# set fosiedit

set fosiedit= { on | off}

This command determines whether FOSI specific menus and menu items are displayed in the menu bar. The default is off . Before updating menus and menu items for a FOSI, this command calls the menuloadhook function . For example, loading a stylesheet can change custom tables, which in turn can affect the Insert > Table menu items and require the menu to be reloaded. However, simply changing a FOSI that enables or disables specific menu items may not require reloading the menu.



---

# set_fosiview

# set fosiview

set fosiview= { default | edit | html | print}

This command forces a FOSI to be interpreted for a particular view (for example, print) when displayed in any arbitrary view (for example, edit).

For example, with a document open in Arbortext Editor , setting fosiview to print and updating the generated text causes Arbortext Editor to display the same generated text and formatting used when printing or publishing the document to PDF.

This option affects all views, not just the edit view. For example, setting fosiview to edit and previewing the document will preview the document using the same generated text and formatting used when editing the document.

Setting fosiview to default returns Arbortext Editor to interpreting the FOSI according to the current view.

This option can be particularly useful in the following situations:

- • When printed generated text is very different from that shown when editing the document.

- • When working with PDF bookmarks.

- • When working with index formatting.

- • When working with table of contents formatting.



---

# set_fosiwarnings

# set fosiwarnings

set fosiwarnings= { on | off}

The set fosiwarnings command enables or disables the display of warning messages when a FOSI is attached to format the Editor view. The default is off .



---

# set_fragmentheader

# set fragmentheader

set fragmentheader= { none | comment | document}

This set option specifies the format of the fragment header that is written at the beginning of an XML inclusion when it is saved. This header information contains information that is used by Arbortext Editor to allow the inclusion to be edited separately. The default value is comment .

- • none — No header information is written.

- • comment — The fragment is written as an XML comment.

- • document — When set to document :

## Related Topics

- • set filereference command



---

# set_fragmentheaderpreserve

# set fragmentheaderpreserve

set fragmentheaderpreserve= { on | off}

The set fragmentheaderpreserve command controls how fragments such as XML inclusions and file entities are written when a document is saved.

- • off — (The default.) Fragments are written with headers binding each fragment to the document type of the root document. The root document is the document which is ultimately referencing each fragment.

- • on — Fragments are written with the document type bindings they had when read into memory.

This setting has document scope.



---

# set_framesetpath

# set framesetpath

set framesetpath= d1 [: dn ]

This command specifies a list of directories to search for framesets. Specify each directory separated by a semicolon. A list of multiple directories must be enclosed in quotation marks.

Framesets must be defined in your .dcf file.

If there is an Arbortext-path \custom\framesets subdirectory at startup, the \custom\framesets path is automatically prepended to the frameset path. Putting your framesets in the \custom\framesets subdirectory makes them automatically available, avoiding manual steps to add them to the path.

You can use the append_frameset_path function to update the frameset path.

## Related Topics

- • Frameset overview



---

# set_freeformpis

# set freeformpis

set freeformpis= { on | off}

When an XML instance with no DTD declaration is edited, the user may add new elements and attributes and associate style categories with elements Formerly, for this information to persist across multiple editing sessions required saving the instance in the form of processing instructions (PIs) at the beginning of the file. This is no longer the case.

If freeformpis is set to on , existing PIs are preserved in Free-form XML documents. If freeformpis is set to off , existing PIs are removed from Free-form XML documents..

The default value of freeformpis is on .



---

# set_fulljust

# set fulljust

set fulljust= { on | off}

This command determines whether text can be displayed as fully justified in the Edit window. off is the default. The setting does not affect the justification of text inside table cells.



---

# set_fullmenus

# set fullmenus

set fullmenus= { on | off}

This command determines whether all available menus and menu items are displayed in the menu bar (if set on ), or if only the most frequently used items are included (if set off ). The default is off .

## Related Topics

- • set liteui command

- • menu_load command



---

# set_fullname

# set fullname

set fullname= string



Declares the full name of the current user (as defined by the user option) to be string . The default value is defined by the system and may be specific to the value of user . If this option is not set and the system provides no default, then the value of user will be used for fullname as well.

This value of fullname is added to the document's list of users when the current user creates his or her first change record in that document.

Example

```
set fullname="Edgar Allen Poe"
```



---

# set_generateuniqueid

# set generateuniqueid

set generateuniqueid= { on | off}

This option determines whether generated IDs have an additional string appended to them that makes it very likely that the ID will be unique across a set of documents. The additional string is generated by the generate_id function and consists of a hyphen followed by eight hexadecimal characters representing the current date and time. Set this option to on to append the additional string to generated IDs and to off to not append the additional string. The default is on . This option has global scope.

## Related Topics

- • generate_id function



---

# set_gentext

# set gentext

set gentext= { on | off}

This command determines if generated text is displayed in the Edit window document. When set to on , the text is displayed, when set to off it is not. The default is on .

When displayed, the generated text will update according to the setting of the set gentextautoupdate command. You can also set the generated text display using the View > Generated Text > Show menu command. The Window preference Show Full Menus must be on to access it.



---

# set_gentextautoupdate

# set gentextautoupdate

set gentextautoupdate= { full | partial | none}

This command determines how the generated text in the Edit window updates. It can be changed when generated text is not visible, but the change won't affect program performance until you display the generated text (for example, by setting gentext to on ).

The available settings are:

- • full — Updates the generated text in the current document, including tables of contents, indices and cross references. This setting works best with small documents without indices.

- • partial — (default setting) Updates the generated text in the current document, but does not update FOSI Time Independent Variables (TIVs). The most common examples of TIVs are tables of contents, indices and cross references. Other generated text, such as bullets for lists, and numbers for numbered lists or numbered sections, are updated.

- • none — The generated text does not automatically update. Updates to generated text must be manually initiated by choosing View > Generated Text > Update . Large documents work best with this setting.

To display generated text, use the set gentext command. You can set the gentextautoupdate option from several places in the user interface. From View > Generated Text , you can choose Full Auto-Updates , Partial Auto-Updates , or No Auto-Updates .

## Related Topics

- • ACL coding for better generated text performance

- • Processing speed and generated text

- • set gentextdisableautoupdate



---

# set_gentextcurrent

# set gentextcurrent

set gentextcurrent= { on | off}

When set to on , marks generated text for the current view as being up-to-date with regard to changes made in the document.

When Arbortext Editor detects generated text as current, setting this option to on does nothing. Arbortext Editor automatically detects whether generated text is current or not. (When a document is changed, generated text is marked as not current. When generated text is updated, it is marked as current.)

You may want to set it to on if changes to the environment are made that affect generated text. For example when an ACL variable that is tested by a stylesheet is altered.

You may want to set gentextcurrent to off in a formatcontinuehook function to force generated text to be regenerated before a subsequent formatting pass.

Because this command works on the current view, and document publishing is done in a separate view, set gentextcurrent does not affect the generated text for formatted output except in contexts where the print view is the current view. These contexts include the formatcontinuehook and the userulehook .

This option does not alter whether partial generated text auto-updates are performed.

If you want to force generated text to be regenerated before additional formatting passes are performed, set gentextcurrent to off .



---

# set_gentextdisableautoupdate

# set gentextdisableautoupdate

set gentextdisableautoupdate= { default | small | medium | large | huge}

This command lets you specify when to disable generated text auto-updating to prevent unacceptable processing times for various size documents. The option has document and session scope. Refer to the set command for more information on specifying document and session scope values.

Generated text automatic updating can slow down processing of documents. The points at which the slowing occurs is based on several factors and varies by document type. The points at which the slowing impacts the user also varies. Setting gentextdisableautoupdate to one of the following values can improve document processing times.

- • default — Sets the document scope value of gentextdisableautoupdate to use the session scope value of gentextdisableautoupdate . Sets the session scope value to use the system default ( huge ).

- • small — Generated text automatic updating is disabled on documents with 5,000 or more elements.

- • medium — Generated text automatic updating is disabled on documents with 20,000 or more elements.

- • large — Generated text automatic updating is disabled on documents with 50,000 or more elements.

- • huge — (The default session scope value.) Generated text automatic updating is disabled on documents with 100,000 or more elements.

## Related Topics

- • ACL coding for better generated text performance

- • Processing speed and generated text

- • set gentextautoupdate



---

# set_gentextfontcolor

# set gentextfontcolor

set gentextfontcolor= { inherit | colorname | # rgbspec }

This command determines the font color used to display generated text in the Edit window. If inherit is set, the generated text is displayed the same as the text of the Edit window document. The value is either inherit , or a named color, or an RGB specification preceded by # . The default is inherit .

You can determine whether Arbortext Editor ignores this setting by using the set usecolorsettings option.

Examples

```
set gentextfontcolor=inherit
set gentextfontcolor=red
set gentextfontcolor=#ff0000
```



---

# set_gentexttagdisplay

# set gentexttagdisplay

set gentexttagdisplay= { none | default | full}

This command determines the display of generated text in a document in the Edit window. The default is none .

- • none — No tags are displayed in generated text.

- • default — Generated text markup takes on the same setting as the Edit window document tag display.

- • full — Displays generated text markup, regardless of whether other tags are displayed fully or not.



---

# set_gentexttrace

# set gentexttrace

set gentexttrace= { #NONE | #ALL | [-] varname1 [, [-] varname2 ] [..., [-] varnamen ]}

This command traces the listed varnameN variables declared in the FOSI's rsrcdesc . Use the special variable names #ALL or #NONE to turn tracing on or off (respectively) for all variables. Multiple variables may be specified by listing names separated by commas. Tracing may be turned off for a variable by preceding the variable name ( varnamen ) with a minus sign.

Examples:

The following command would trace all variables defined in a FOSI's rsrcdesc .

```
set gentexttrace=#ALL
```

The following command would trace the variables divs1ct , divs2ct , and divs3ct .

```
set gentexttrace="divs1ct, divs2ct, divs3ct"
```

The following command would trace all variables defined in a FOSI's rsrcdesc , except the variables divs1ct , divs2ct , and divs3ct .

```
set gentexttrace=#ALL, "-divs1ct, -divs2ct, -divs3ct"
```

The following command would turn off all FOSI variable tracing.

```
set gentexttrace=#NONE
```

## Related Topics

- • set gentexttracemaxlen command

- • set gentextxreftrace command



---

# set_gentexttracemaxlen

# set gentexttracemaxlen

set gentexttracemaxlen= length

This command sets the length (in characters) of the FOSI variable values (including cross-reference FOSI variable values) displayed in the FOSI Generated Text Variable Trace window. If the variable is longer than the specified length , “...” is appended to the value. The default (and maximum) length is 4096 characters.

## Related Topics

- • set gentexttrace command

- • set gentextxreftrace command



---

# set_gentextwarnings

# set gentextwarnings

set gentextwarnings= { 0 | 1 | 2 | 3}

This command determines what messages Arbortext Editor displays when it detects errors and anomalies in how a FOSI's variables are used. The following settings are available.

- • 0 — Display no generated text errors, warnings, or informational messages.

- • 1 — Display generated text error messages only.

- • 2 — Display generated text error messages and warnings.

- • 3 — Display generated text error messages, warnings, and informational messages.

The default setting for Arbortext Editor is 1 ; for Arbortext Architect , the default is 3 .

The resulting messages appear in the FOSI Generated Text Messages window when formatting is complete, or when an update of the generated text is complete (if triggered independently of formatting).



---

# set_gentextxreftrace

# set gentextxreftrace

set gentextxreftrace= { #NONE | #ALL | [-] varname1 [, [-] varname2 ] [..., [-] varnamen ]}

This command traces the listed varnameN cross-reference FOSI variables. A cross-reference FOSI variable is a variable created using fillval to a savetext:texid or using #xref . Use the special variable names #ALL or #NONE to turn tracing on or off (respectively) for all cross-reference variables. Multiple cross-reference variables may be specified by listing names separated by commas. Tracing may be turned off for a cross-reference variable by preceding the variable name ( varnamen ) with a minus sign.

Examples:

The following command would trace all cross-reference FOSI variables in an instance.

```
set gentextxreftrace=#ALL
```

The following command would trace the cross-reference FOSI variables intro , parttwo , and comlist .

```
set gentextxreftrace=intro, parttwo, comlist
```

The following command would trace all cross-reference FOSI variables in an instance, except the variables intro , parttwo , and comlist .

```
set gentextxreftrace=#ALL, -intro, -parttwo, -comlist
```

The following command would turn off all cross-reference FOSI variable tracing.

```
set gentextxreftrace=#NONE
```

## Related Topics

- • set gentexttrace command

- • set gentexttracemaxlen command



---

# set_graphicapptransform

# set graphicapptransform

set graphicapptransform= transformstring

This command specifies a set of graphic file formats that should be transformed to a different graphic file format when using PTC Advanced Print Publisher to publish a document for print or PDF.

The transformstring is one or more transformation rules. Multiple rules are separated by a vertical line ( | ). Each transformation rule has two parts separated by a colon ( : ). The first part of the rule is a list of graphic formats to be converted separated by a comma ( , ). The second part of the rule is the graphic file format to which the first set of graphic formats should be transformed during publishing.

The following graphic formats are supported for transformation:

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

- • pdf — Portable Document format file

- • + — Represents all graphic file formats that are not web-friendly

- • * — Represents all graphic file formats

For graphic file formats that are also included in the isoviewfileformats preference, those formats can be transformed to one of the following types:

- • png

- • jpg

All other graphic file formats can be transformed to one of the following types:

- • png

- • jpg

- • gif

- • –

Examples:

```
set graphicapptransform=cgm,idr,idrz,iso,isoz:pdf
set graphicapptransform=iso,isoz,pvz:jpg|svg:png
set graphicapptransform=*:png
```

## Related Topics

- • Intelligent Graphics Overview

- • set isoviewfileformats

- • Graphic Conversion Support



---

# set_graphicdefaultwebformat

# set graphicdefaultwebformat

set graphicdefaultwebformat= { png | jpg | gif}

This command specifies the default graphic file format to which graphics that are not web-friendly are converted when publishing for the following types of HTML output:

- • Web

- • HTML Help

- • HTML File

Supported graphic file format values are png , jpg , or gif . The default value is png .

## Related Topics

- • set graphicwebtransform

- • Graphic Conversion Support



---

# set_graphicdisplay

# set graphicdisplay

set graphicdisplay= { on | off}

This command determines whether graphics will be displayed in the Edit window. on is the default.

graphics is a synonym for graphicdisplay .



---

# set_graphicfilter

# set graphicfilter

set graphicfilter= filterstring

This command specifies the default list of graphics file types to display in the Files of type pulldown list of the Locate Graphic File to Reference dialog box when inserting a new graphic.

filterstring specifies a list of file types separated by a vertical bar “|”. There are two parts to each item, which are also separated by a vertical bar “|”. The first part is the string to display in the menu or pop-up menu. The second part is the corresponding pattern to use to filter the files displayed in the dialog box. Multiple patterns may be specified by separating them with a semicolon.

The default list contains:

```
All Graphics (*.bmp,*.cgm,*.edz,*.eps,*.gif,*.idr,*.idrz,*.iso,*.isoz,*.jpg,*.pdf,*.png,
*.pvz,*.svg,*.tif)|*.bmp;*.cgm;*.edz;*.eps;*.gif;*.idr;*.idrz;*.iso;*.isoz;*.jpg;*.pdf;*.png;
*.pvz;*.svg;*.tif;*.tiff|
Bitmap Graphics (*.bmp)|*.bmp|
Creo View Graphics (*.edz, *.pvz)|*.edz;*.pvz|
Graphics Interchange Format (*.gif)|*.gif|
IsoDraw Graphics (*.idr, *.idrz, *.iso, *.isoz)|*.idr;*.idrz;*.iso;*.isoz|
JPEG File Interchange Format (*.jpg)|*.jpg|
Portable Network Graphics(*.png)|*.png|
Scalable Vector Graphics (*.svg)|*.svg|
Tag Image File Format (*.tif, *.tiff)|*.tif;*.tiff|
Vector Graphics (*.cgm, *.eps, *.pdf)|*.cgm;*.eps;*.pdf|
All Files|*
```



---

# set_graphicrtftransform

# set graphicrtftransform

set graphicrtftransform= transformstring

This command specifies a set of graphic file formats that should be transformed to a different graphic file format when using Arbortext Import/Export to export a document to RTF.

The transformstring is one or more transformation rules. Multiple rules are separated by a vertical line ( | ). Each transformation rule has two parts separated by a colon ( : ). The first part of the rule is a list of graphic formats to be converted separated by a comma ( , ). The second part of the rule is the graphic file format to which the first set of graphic formats should be transformed during publishing.

The following graphic formats are supported for transformation:

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

- • + — Represents all graphic file formats that are not web-friendly

- • * — Represents all graphic file formats

If the source graphic file format is included in the isoviewfileformats preference, those graphic file formats can be transformed to one of the following types:

- • png

- • jpg

- • cgm

- • eps

All other graphic file formats can be transformed to one of the following types:

- • png

- • jpg

- • gif

- • –

Examples:

```
set graphicrtftransform=iso,isoz,edz,pvz:cgm|svg:png
set graphicrtftransform=*:png
```

## Related Topics

- • Intelligent Graphics Overview

- • set isoviewfileformats

- • Graphic Conversion Support



---

# set_graphicspath

# set graphicspath

set graphicspath= d1 [: dn ]

This command specifies a list of directories to search for graphic files when their references do not specify an absolute path name (each directory separated by a semicolon). The initial setting is the value of the APTGRPATH environment variable if set. Otherwise, it defaults to the graphics subdirectory of Arbortext-path . If a graphics subdirectory exists in either the Arbortext-path \application or Arbortext-path \custom directory, that subdirectory is also part of the default graphics path. Use %D to refer to the Arbortext-path \graphics directory. Use %B to refer to directories relative to the current document’s directory.

Any base URI and the document's parent directory (if different from the base URI) are included by default in the directories searched for graphics. When any set graphicspath directory parameter is set to a value of %^ , the parent document directory will not be included when searching for graphics. Only the paths specified will be searched. If you want to include the current working directory in the graphics path, add a period ( . ) to the list of directories. However, it is recommended that you do not include the current working directory in your graphics path list, as this can cause inconsistent results.

If there is an Arbortext-path \custom\graphics subdirectory at startup, the \custom\graphics path is automatically prepended to the graphics path. Putting your graphics in the \custom\graphics subdirectory makes them automatically available, avoiding manual steps to add them to the path.

The Arbortext-path \custom\graphics directory is also automatically included if you specify %D in the path.

Example

```
set graphicspath="c:\\Program Files\\Arbortext\\editor\\graphics;%^;
c:\\Arbortext\\editor\\packages\\graphics"
```

A list of multiple directories must be enclosed in quotation marks.

You can use the append_graphics_path function to update the graphics path.

## Related Topics

- • append_graphics_path function

- • option_path_list function

- • oid_graphic_pathname function

- • Symbolic parameters in path list variables



---

# set_graphicwebtransform

# set graphicwebtransform

set graphicwebtransform= transformstring

This command specifies a set of graphic formats that should be transformed to a different graphic format when publishing for the following types of HTML output:

- • Web

- • HTML Help

- • HTML File

The transformstring is one or more transformation rules. Multiple rules are separated by a vertical line ( | ). Each transformation rule has two parts separated by a colon ( : ). The first part of the rule is a list of graphic formats to be converted separated by a comma ( , ). The second part of the rule is the graphic file format to which the first set of graphic formats should be transformed during publishing.

The following graphic formats are supported for transformation:

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

- • + — Represents all graphic file formats that are not web-friendly

- • * — Represents all graphic file formats

These graphic file formats can be transformed to one of the following types:

- • png

- • jpg

- • gif

- • webcgm

- • iview

- • –

When determining whether to transform a graphic, Arbortext Editor checks several ACL preferences. The graphicwebtransform preference takes precedence over all other preferences, except cgmprofile . The following other preferences can affect graphics transformations:

- • intelligentgraphicsconversion

- • graphicdefaultwebformat

- • isoviewfileformats

- • cgmprofile

For example, if graphicwebtransform is set to iso,pvz:iview , but isoviewfileformats does not include pvz , that graphic file format will still be displayed by Arbortext IsoView in the HTML output.

The graphicwebtransform preferences also overrides the value of the Convert Intelligent Graphics check box in the publishing dialog boxes.

For each graphic during publishing, Arbortext Editor checks to see whether that graphic file format is in one of the first part of the graphicwebtransform setting. If it is, Arbortext Editor transforms the graphic based on the target of the rule. If the format is not included in graphicwebtransform , Arbortext Editor processes the graphic based on whether the graphic is intelligent and whether the intelligentgraphicsconversion preference is set to on . If intelligentgraphicsconversion is set to off and the graphic is an intelligent graphic, the graphic is not transformed. Otherwise, if the graphic is not web-friendly, Arbortext Editor will transform the graphic based on the graphic file format specified by the graphicdefaultwebformat preference. A graphic is considered an intelligent graphic if it is a format specified by the isoviewfileformats preference.

Examples:

```
set graphicwebtransform=iso,isoz,edz,pvz:cgm|svg:png
set graphicwebtransform=*:png
```

## Related Topics

- • Intelligent Graphics Overview

- • set intelligentgraphicsconversion

- • set graphicdefaultwebformat

- • set cgmprofile

- • set isoviewfileformats

- • Graphic Conversion Support



---

# set_helpfontpercent

# set helpfontpercent

set helpfontpercent= n

This command increases or decreases the point sizes of all fonts in all message windows to the percentage specified, subject to the availability of fonts. The default value of n is system dependent. Fonts cannot be displayed at less than 40% of their point size. This command does not affect the font size of Help Center content.

n is a number, excluding a percent ( % ) symbol.

## Related Topics

- • set editfontpercent command

- • set fontpercent command

- • set tagfontpercent command



---

# set_hiddentagscan

# set hiddentagscan

set hiddentagscan= { on | off}

Controls whether elements configured by the tag_display command to not be displayed will be recognized and operated on by find and spelling check operations. When set hiddentagscan is set to on , the content of elements that are not displayed will be operated on. The default setting is off , meaning the non-displayed content will not be operated on.

## Related Topics

- • find command

- • spell command



---

# set_hidesuppressed

# set hidesuppressed

set hidesuppressed= { on | off}

When set hidesuppressed is set to on , the content of elements that are configured by a Arbortext Styler stylesheet to be hidden or by a screen FOSI to be suppressed is hidden in the Editor view. The default setting is off , meaning suppressed content is displayed in the Editor view. This allows you to edit content that is suppressed where it occurs in the document, but that is inserted in generated text.

For example, you might add end note content to a paragraph, and then create generated text that inserts the content of the end note. When set hidesuppressed is on , the end note content in the paragraph is hidden in Editor view, while the generated text version displays. When set to off , the content displays in both the paragraph and the generated text version.

If you insert a suppressed element within generated text, the content of the element is not shown in the Editor view regardless of the setting of this option.



---

# set_highlightinvalidmarkup

# set highlightinvalidmarkup

set highlightinvalidmarkup= { on | off}

This command modifies the display of invalid markup. By default, invalid markup is shown in red strike-through. If this command is set to off , invalid markup is displayed in the same manner as valid markup.

The default is on .

## Related Topics

- • Invalid markup — overview



---

# set_htmlextension

# set htmlextension

set htmlextension= ext

This command specifies the extension to use for newly saved HTML files. htm is the default. The Save As dialog box and save_as command add this extension if the specified file does not already have an extension and the htmlextension option is non-null.

Do not include a period as part of the extension.

## Related Topics

- • set defaultfilter command

- • set asciiextension command

- • set sgmlextension command



---

# set_htmlhelpstylesheet

# set htmlhelpstylesheet

set htmlhelpstylesheet= { name | none}

This command specifies the stylesheet to be used as the default for the Publish > For HTML Help option on the File menu.

name is the path and file name of a .style or .xsl stylesheet file. If you don't specify an extension for the stylesheet, Arbortext Editor first looks for a .style file, and then a .xsl file.

The stylesheet ID processing instruction must specify htmlhelp as the publishing type.

If you specify only the stylesheet's base name, Arbortext Editor first looks for the file in the document directory, and then looks in the document type directory. If you specify a relative path (other than one that just gives the base name), Arbortext Editor looks for the file using the given path relative to the current working directory.

If you are using Arbortext Publishing Engine for publishing, it must be able to locate the stylesheet. If a document references a stylesheet using a URL, that stylesheet can be found by both Arbortext Editor and Arbortext Publishing Engine . Stylesheets that are available on the Arbortext PE server appear in the Stylesheet selection fields preceded by the notation (pe) . The Arbortext PE server must have the HTML Help Workshop installed to create the .chm file.

When you are using Arbortext Publishing Engine , be aware of the following when setting a value for this option:

- • If you try to set the location to a local path for any type of published output, you will get an error that the stylesheet is not the name of a stylesheet on the server. The following example produces an error if Arbortext Publishing Engine publishing is enabled:

- • If you try to set the location to a stylesheet file name only (no path), Arbortext Publishing Engine looks for a stylesheet with a matching name. The following example would succeed if a stylesheet of the same name exists in a location where the Arbortext PE server looks for stylesheets.

If htmlhelpstylesheet is set to none or is not set, Arbortext Editor and Arbortext Publishing Engine use the Editor/Default stylesheet.

Examples

```
set htmlhelpstylesheet=memo2
set htmlhelpstylesheet=~/mydocs/memo/memo2.style
set htmlhelpstylesheet=http://www.some_site.com/examples/techman_hh.xsl
```

## Related Topics

- • set stylesheet command

- • Stylesheet overview

- • Configuring stylesheet order in a list

- • Using Arbortext Publishing Engine for publishing documents

- • Opening, referencing, and saving files



---

# set_htmlstylesheet

# set htmlstylesheet

set htmlstylesheet= { name | none}

This command specifies the stylesheet to be used for the Save as HTML and Publish > HTML File options on the File menu and for browser display.

name is the path and file name of a FOSI, XSL, or Arbortext Styler stylesheet. If you do not specify an extension for the stylesheet, Arbortext Editor first looks for a .style file, then a .fos file, and finally a .xsl file.

If you specify only the stylesheet's base name, Arbortext Editor first looks for the file in the document directory, and then looks in the document type directory. If you specify a relative path (other than one that just gives the base name), Arbortext Editor looks for the file using the given path relative to the current working directory.

If you are using Arbortext Publishing Engine for publishing, it must be able to locate the stylesheet. If a document references a stylesheet using a URL, that stylesheet can be found by both Arbortext Editor and Arbortext Publishing Engine . Stylesheets that are available on the Arbortext PE server appear in the Stylesheet selection fields preceded by the notation (pe) .

When you are using Arbortext Publishing Engine , be aware of the following when setting a value for this option:

- • If you try to set the location to a local path for any type of published output, you will get an error that the stylesheet is not the name of a stylesheet on the server. The following example produces an error if Arbortext Publishing Engine publishing is enabled:

- • If you try to set the location to a stylesheet file name only (no path), Arbortext Publishing Engine looks for a stylesheet with a matching name. The following example would succeed if a stylesheet of the same name exists in a location where the Arbortext PE server looks for stylesheets.

If htmlstylesheet is set to none or is not set, Arbortext Editor and Arbortext Publishing Engine use the Editor/Default stylesheet.

Examples

```
set htmlstylesheet=memo2
set htmlstylesheet=~/mydocs/memo/memo2.fos
set htmlstylesheet=http://www.some_site.com/examples/techman.xsl
```

## Related Topics

- • set stylesheet command

- • Save a document as an HTML file

- • Stylesheet overview

- • Displaying your XML document in a browser

- • Configuring stylesheet order in a list

- • Using Arbortext Publishing Engine for publishing documents

- • Opening, referencing, and saving files



---

# set_hyperlinkmenus

# set hyperlinkmenus

set hyperlinkmenus= { on | off}

When this command is set to on , the Create Hyperlink , Delete Hyperlink , and Show Hyperlinks commands are added to the Tools menu . When set to off , these commands are not available on the Tools menu.

The default is off because these menu commands have been replaced by Insert > Link and Insert > Link Target . Set this command to on if your document type does not support link markup.

## Related Topics

- • Link and target processing instructions



---

# set_importexportpath

# set importexportpath

set importexportpath= dir1 [: dirn ]

This command specifies the directory that Arbortext Import/Export searches for library, configuration, MapTemplate, and RTF style template files supporting Arbortext Import/Export Import MapTemplate and Export stylesheet development.



---

# set_includefontcolor

# set includefontcolor

set includefontcolor= { inherit | colorname | # rgbspec }

This command determines the font color used to display XML inclusions in the Edit window. If inherit is set, the included text is displayed the same as the text of the Edit window document. The value is either inherit , or a named color, or an RGB specification preceded by # . The default is inherit .

You can determine whether Arbortext Editor ignores this setting by using the set usecolorsettings option.

Examples

```
set includefontcolor=inherit
set includefontcolor=red
set includefontcolor=#ff0000
```



---

# set_indent

# set indent

set indent= { on | off}

When this command is set to on , divisions are inset from the left margin of the Edit window display according to level (for example, sections and section headings are indented more than chapters). When set to off , divisions are not indented.

This command does not affect the indentation of the formatted document.



---

# set_inlineapplicabilitycolor

# set inlineapplicabilitycolor

set inlineapplicabilitycolor= color

Changes the current color setting for applicability highlighting.

- • color — the required color, for example:

The default color is lime .

You can also set this option with the inlineapplicabilityfontcolor advanced preference.

Applicability shading is activated with the set showprofileshading option.

## Related Topics

- • set profileshowshading

- • Working with Inline Applicability



---

# set_inlineapplicabilitynamecheck

# set inlineapplicabilitynamecheck

set inlineapplicabilitynamecheck= { on | off}

Specifies whether to allow values in inline applicability expressions that are not defined in the referenced option sets.

If this option is activated with set inlineapplicabilitynamecheck=on , expressions that use undefined values are not allowed. For example, if a product’s defined options are cat and mouse , the inline applicability expression “cat” or “dog” will not be allowed when the expression is validated in the Apply Inline Applicability dialog box.

You can also set this option with the inlineapplicabilitynamecheck advanced preference.

## Related Topics

- • Apply Inline Applicability Dialog Box

- • Working with Inline Applicability



---

# set_inlineapplicabilitysyntax

# set inlineapplicabilitysyntax

set inlineapplicabilitysyntax= syntax

Sets the applicability syntax for the current Arbortext Editor environment.

- • syntax — the required applicability syntax, for example:

Setting this option with any non-blank value also enables Arbortext Editor ’s interface for authoring inline applicability.

You can also set this option with the inlineapplicabilitysyntax advanced preference.

Arbortext Editor ships with two applicability syntaxes: APEX and ATO.

To register a custom syntax, use the registerApplicabilitySyntax() applicability function.

To retrieve the syntax that is currently specified for the environment, use eval option(inlineapplicabilitysyntax) .

## Related Topics

- • registerApplicabilitySyntax function

- • Working with Inline Applicability



---

# set_inlineapplicabilityui

# set inlineapplicabilityui

set inlinepplicabilityui= [ symbols | words | wordsexclude]

This command specifies the way in which the constructs in inline applicability expressions are represented when in Arbortext Editor ’s inline applicability interface.

- • symbols — use symbols

- • words — use words, variety 1 (default)

- • wordsexclude — use words, variety 2

For example:

```
set inlineapplicabilityui=symbols
```

You can also set this option with the inlineapplicabilityui advanced preference.

## Related Topics

- • Apply Inline Applicability dialog box

- • Modify Attributes dialog box

- • Working with Inline Applicability



---

# set_inlineediting

# set inlineediting

set inlineediting= { on | off}

This option turns inline editing of file entities and XML inclusions on and off. The default is on . This setting does not apply to documents, entities, and inclusions stored CMS and accessed using a repository adapter.



---

# set_inputmode

# set inputmode

set inputmode= { insert | overstrike | toggle}

This command determines whether new text can be inserted at the point of the cursor (the default) or will overwrite existing text. toggle changes from the existing setting to the other setting.

## Related Topics

- • set pendingdelete command



---

# set_insertpreviewlinktext

# set insertpreviewlinktext

set insertpreviewlinktext= { on | off}

This option determines whether preview text from the link target is inserted and displayed in the Arbortext Editor window for DITA xref and link tags. The preview text is taken from the content of either the navtitle , title , or searchtitle tags and from the shortdesc tag in the link target. The preview text is highlighted in the Arbortext Editor window.

Set this option to on to insert the preview text and to off to not insert it. The default is on .



---

# set_insertsymboldlgnosymbols

# set insertsymboldlgnosymbols

set insertsymboldlgnosymbols= { on | off}

If set to on (the default), the Symbol tab of the Insert Symbol dialog box is disabled, allowing the user to insert only character entities from the Character Entities tab.

If insertsymboldlgnosymbols is set to off (the default), the Symbols tab on the Insert Symbols dialog box is enabled.

## Related Topics

- • Inserting symbols

- • set insertsymbolfontpi



---

# set_insertsymbolfontpi

# set insertsymbolfontpi

set insertsymbolfontpi= { on | off}

If set to on (the default), when inserting symbols from the Symbol tab of the Insert Symbol dialog box, a _font PI (processing instruction) is inserted around the symbol character code if the inserted symbol is of a different font family than the font family at the current cursor location. The PI will be added if Arbortext Editor is unable to translate the requested character from the Symbol character set to Unicode.

If insertsymbolfontpi is set to off , the Unicode character value is inserted with no _font PI.

## Related Topics

- • Inserting symbols

- • set insertsymboldlgnosymbols



---

# set_intelligentgraphicsconversion

# set intelligentgraphicsconversion

set intelligentgraphicsconversion= { on | off | prompt}

This command specifies whether converting intelligent graphics to web-friendly graphic formats is needed for the File > Publish > For Web and File > Publish > HTML File operations.

If set to on , all intelligent graphics in the document will be converted to web-friendly graphics in the published HTML file. EDZ graphics will be converted to GIF. ISO/IDR graphics will be converted to PNG or JPEG, depending on the setting of the graphicdefaultwebformat option. If set to off , intelligent graphics will be included in the published HTML file. If set to prompt , the Convert Intelligent Graphics check box is enabled in the Publish for Web and Publish HTML File dialog boxes.

The default is prompt .

## Related Topics

- • Intelligent Graphics Overview

- • set graphicdefaultwebformat

- • Graphic Conversion Support



---

# set_isoviewdownloaduri

# set isoviewdownloaduri

set isoviewdownloaduri= uri

This command specifies a uri where the Arbortext IsoView web installer is located. The uri parameter contains a URI (Uniform Resource Identifier) value.

Arbortext Editor writes the specified uri location to a generated HTML file when an intelligent graphic is published in the HTML file. This enables Internet Explorer to install Arbortext IsoView when the HTML file is displayed in the browser. Arbortext IsoView enables users to interact with the intelligent graphics in the HTML file.

If isoviewdownloaduri is not set or contains an empty value, you can still view intelligent graphics in a published HTML file. To support viewing intelligent graphics, Arbortext IsoView must already be installed on the workstation where Internet Explorer is running.

Refer to the Arbortext IsoView documentation for more information about Arbortext IsoView .

Examples:

```
set isoviewdownloaduri=http://www.acme.com/isoview/isoviewx6_PTC.cab
```

## Related Topics

- • Intelligent graphics overview



---

# set_isovieweditorfileformats

# set isovieweditorfileformats

set isovieweditorfileformats=" [cgm] [;idr] [;idrz] [;iso] [;isoz] [;svg] "

By default, Arbortext Editor uses different underlying technologies to display images of different formats. The set isovieweditorfileformats option lets you override these default settings to specify additional graphic file formats display using the embedded Arbortext IsoView control in Arbortext Editor .

This preference has no default value in the full installation of Arbortext Editor , where the set isoviewfileformats preference specifies both the graphic file formats displayed and published using Arbortext IsoView .

The arguments are the file extensions for the graphic types separated by semicolons. If you set the value to more than one graphic type, enclose the arguments in quotes.

Refer to the Arbortext IsoView documentation for more information about Arbortext IsoView . .

Examples:

```
set isovieweditorfileformats=cgm
set isovieweditorfileformats="svg;cgm"
```

## Related Topics

- • Intelligent graphics overview

- • set isoviewfileformats



---

# set_isoviewfileformats

# set isoviewfileformats

set isoviewfileformats=" [cgm] [;idr] [;idrz] [;iso] [;isoz] [;svg] "

This command specifies both the graphic file formats that should be displayed using the embedded Arbortext IsoView control in Arbortext Editor and the graphic types that should be published using Arbortext IsoView . By default, the following types of graphics are displayed in the embedded dialog box:

- • CGM ( .cgm )

- • IDR ( .idr )

- • IDRZ ( .idrz )

- • ISO ( .iso )

- • ISOZ ( .isoz )

You can set the dialog box to also display SVG ( .svg ) graphics. The arguments are the file extensions for the graphic types separated by semicolons. If you set the value to more than one graphic type, you must enclose the arguments in quotes. If you set the value of this option to an empty string, the Arbortext IsoView control will not be used to display any graphics.

Publishing intelligent graphics using Arbortext IsoView is also supported for all intelligent graphics types. Refer to the Arbortext IsoView documentation for more information about Arbortext IsoView .

Examples:

```
set isoviewfileformats=iso
set isoviewfileformats="iso;svg"
```

## Related Topics

- • Intelligent graphics overview



---

# set_isoviewhighlightcolor

# set isoviewhighlightcolor

set isoviewhighlightcolor= { colorname | # rgbspec }

This command determines the color used to highlight an object in an intelligent graphic displayed using the embedded Arbortext IsoView control in Arbortext Editor . The highlight color is used when the object is the target of a link. The default value is red . The supported values are either one of the Arbortext supported named colors or an RGB specification value. Refer to the glossary in the Arbortext Editor help for more information about named colors and RGB values.

You can specify the highlighting style with the isoviewhighlightstyle command.

The value of this preference is used in both editing and publishing. The value is passed along to HTML output during publishing.

Examples:

```
set isoviewhighlightcolor=green
set isoviewhighlightcolor=#33FFFF
```

## Related Topics

- • Intelligent graphics overview

- • set isoviewhighlightstyle



---

# set_isoviewhighlightstyle

# set isoviewhighlightstyle

set isoviewhighlightstyle= { circle | fill | flash | frame}

This command determines the style used to highlight an object in an intelligent graphic displayed using the embedded Arbortext IsoView control in Arbortext Editor . The highlight style is used when the object is the target of a link. The following values are supported:

- • circle — a circle is drawn around the object

- • flash — the object flashes

- • fill — the object’s color is changed

- • frame — a thick line is drawn along the outline of the object

You can specify the highlighting color by using the isoviewhighlightcolor preference. The highlighting color is used by all four styles.

The value of this preference is used in both editing and publishing. The value is passed along to HTML output during publishing.

Example:

```
set isoviewhighlightstyle=flash
```

## Related Topics

- • Intelligent graphics overview

- • set isoviewhighlightcolor



---

# set_javaclasspath

# set javaclasspath

set javaclasspath= dir1 [: dirn ]

This command specifies the list of directories that the Arbortext Editor embedded Java Virtual Machine (JVM) should search to locate Java classes when Java methods are called from within Arbortext Editor . The initial path setting of set javaclasspath is empty.

Whether javaclasspath is set or not, Arbortext Editor automatically includes the distributed Java JAR files in the directory Arbortext-path \lib\classes .

The setting for javaclasspath is only evaluated when the first java_ type function is called in an Arbortext Editor session. Subsequent changes to set javaclasspath will not affect the running Java Virtual Machine unless you exit Arbortext Editor and start a new session. Consequently, when using the java_ type functions, you should set javaclasspath before invoking a java_ type function.

Examples:

```
set javaclasspath="c:\\winnt\\java\\classes;c:\\myjava\\myjava.jar"
```

Multiple directories are delimited with semicolons and the entire set enclosed in quotes.

If there is an Arbortext-path \custom\classes subdirectory at startup containing any JAR files ( .jar ), the path for each .jar file is automatically prepended to the Java class path for Arbortext Editor . Then the \custom\classes path is prepended, which automatically includes any compiled Java .class files in it. Putting your .class and .jar files in the \custom\classes subdirectory makes them automatically available, avoiding manual steps to add them to the path.

You should use the append_javaclass_path function to update the Java class path for Arbortext Editor to avoid problems resulting from overlooking a Java class path when using set javaclasspath .

If set javaclasspath is used with Arbortext Publishing Engine , you should protect it from being sourced again after the JVM has started. Put the set javaclasspath statement inside an appropriate if statement. For example:

```
# Try to change this value only if the JVM has not started yet.
# This protects from failure in case this file is sourced again
# after the JVM has already started.
if (!java_init()) {
set javaclasspath="c:\\winnt\\java\\classes;D:\\myjava\\myjava.jar"
}
```

## Related Topics

- • option_path_list function

- • append_javaclass_path function

- • java_constructor function

- • java_init function

- • java_instance function

- • java_static function

- • set javadebugport command

- • set javavmargs command

- • set javavmmemory command

- • set javavmpath command



---

# set_javadebugport

# set javadebugport

set javadebugport= { off | auto | n }

When Arbortext Editor loads the Java Virtual Machine (JVM), it checks the value of the set javadebugport option. If set javadebugport is set to a positive number, Arbortext Editor turns on the JVM debug mode and establishes communication with Java debuggers by using the socket port number specified by set javadebugport . If set javadebugport is set to auto , Arbortext Editor randomly selects an unused socket port number, sets set javadebugport to the selected port number, and performs the remaining tasks for establishing communication. If the set javadebugport is set to off (the default), Arbortext Editor will not turn on the JVM debug mode.

To establish communication between the Java debugger and Arbortext Editor , pass the socket port number to the Java debugger. For example, if the set javadebugport is set to 3539 and the jdb (Java debugger) is running on the same machine as Arbortext Editor , issue the following command:

```
c:\> jdb -connect com.sun.jdi.SocketAttach:port=3539
```

Refer to OracleJava documentation on jdb — The Java debugger for information on the jdb command and its options, which is available from the java.sun.com web site.

The setting for javadebugport is only evaluated when the first java_ type function is called in a Arbortext Editor session. Subsequent changes to set javadebugport will not affect the running Java Virtual Machine unless you exit Arbortext Editor and start a new session. Consequently, when using the java_ type functions, you should set javadebugport before invoking a java_ type function.

Example:

```
set javadebugport=auto
# Load the JVM
java_console()
# Get the socket port number for Java debugging
eval option('javadebugport')
```

If set javadebugport is used with Arbortext Publishing Engine , you should protect it from being sourced again after the JVM has started. Put the set javadebugport statement inside an appropriate if statement. For example:

```
# Try to change this value only if the JVM has not started yet.
# This protects from failure in case this file is sourced again
# after the JVM has already started.
if (!java_init()) {
set javadebugport=8090
}
```

## Related Topics

- • java_constructor function

- • java_instance function

- • java_static function

- • append_javaclass_path function

- • set javaclasspath command

- • set javavmargs command

- • set javavmmemory command

- • set javavmpath command



---

# set_javascriptinterpreter

# set javascriptinterpreter

set javascriptinterpreter= { rhino | jscript}

The javascriptinterpreter option specifies the default JavaScript engine to be used when a file's extension is the only determining factor as to which engine to use.

If javascriptinterpreter is set to rhino , files with a .js extension will be processed by the Rhino JavaScript engine. If javascriptinterpreter is set to jscript , files with a .js extension will be processed by the Microsoft JScript engine.

The default value of javascriptinterpreter is rhino .

## Related Topics

- • set windowsscriptdebugger



---

# set_javavmargs

# set javavmargs

set javavmargs= vmargs

The value of this option will be passed to the Java Virtual Machine (JVM) as command line arguments when the JVM is loaded. This option can't specify the class path. Set the class path using the set javaclasspath option.

The setting for javavmargs is only evaluated when the first java_ type function is called in a Arbortext Editor session. Subsequent changes to set javavmargs will not affect the running Java Virtual Machine unless you exit Arbortext Editor and start a new session. Consequently, when using the java_ type functions, you should set javavmargs before invoking a java_ type function.

Example:

```
# Define system property my.preferences and set the JVM
# initial memory pool to six megabytes.
set javavmargs="-Dmy.preferences=c:\prefs.txt -Xms6m"
```

If set javavmargs is used with Arbortext Publishing Engine , you should protect it from being sourced again after the JVM has started. Put the set javavmargs statement inside an appropriate if statement. For example:

```
# Try to change this value only if the JVM has not started yet.
# This protects from failure in case this file is sourced again
# after the JVM has already started.
if (!java_init()) {
set javavmargs="-Xms10m"
}
```

When using XSL-FO to publish documents of any size, XSL-FO may require more Java stack size than that set by default. If the stack size is insufficient, Arbortext Publishing Engine or Arbortext Editor may terminate unexpectedly. If this scenario occurs, increase the Java stack size by adding the following line to an ACL file stored in the custom\init directory:

```
set javavmargs="-Xss2m"
```

## Related Topics

- • java_static function

- • java_constructor function

- • java_init function

- • java_instance function

- • java_delete function

- • append_javaclass_path function

- • set javaclasspath command

- • set javadebugport command

- • set javavmmemory command

- • set javavmpath command

- • Using Arbortext Publishing Engine for publishing documents



---

# set_javavmmemory

# set javavmmemory

set javavmmemory= n

This option specifies the maximum size, in megabytes, of the Java Virtual Machine (JVM) memory allocation pool. The default value is 2048 for 64-bit machines, and 256 for 32-bit machines. Reduce this value if Arbortext Editor or Arbortext Publishing Engine cannot allocate enough memory as specified by this option.

If APTJAVAVMMEMORY is not set, the setting for set javavmmemory is evaluated when the first java_ type function is called in a Arbortext Editor session. Subsequent changes to set javavmmemory will not affect the running Java Virtual Machine unless you exit Arbortext Editor and start a new session. Consequently, when using the java_ type functions, you should set javavmmemory before invoking a java_ type function.

If set javavmmemory is used with Arbortext Publishing Engine , you should protect it from being sourced again after the JVM has started. Put the set javavmmemory statement inside an appropriate if statement. For example:

```
# Try to change this value only if the JVM has not started yet.
# This protects from failure in case this file is sourced again
# after the JVM has already started.
if (!java_init()) {
set javavmmemory=500
}
```

If you experience difficulty starting the JVM, it's possible that the memory allocation is higher than your operating system can accommodate. Try setting the javavmmemory value lower (for example, on a 32-bit machine, to a value below 900) to see if the JVM will start.

On a 64-bit machine, the maximum size is essentially unlimited. However, setting the value too high can decrease performance due to paging of virtual memory to disk. Commonly, it should be substantially less than the physical RAM on the system. For example, if you have 4GB RAM, try setting javavmmemory to 2000 . If publishing extremely large documents results in failures with the error FATAL ERROR - Java has run out of memory. messages, try increasing the value until the error no longer occurs.

For more information about tuning the JVM, go to:

java.sun.com/performance/reference/whitepapers/tuning.html

## Related Topics

- • java_constructor function

- • java_instance function

- • java_static function

- • java_delete function

- • append_javaclass_path function

- • set javaclasspath command

- • set javadebugport command

- • set javavmargs command

- • set javavmpath comand



---

# set_javavmpath

# set javavmpath

set javavmpath= { vmpath }

This command specifies the type and location of the Java Virtual Machine (JVM) to use when calling Java classes from Arbortext Editor .

This command can be set to either a full path ( vmpath ).

If the option is set to a full path ( vmpath ), then Arbortext Editor uses the specified JVM for the current session.

If this option is not set, Arbortext Editor checks the Windows registry to locate an Oracle JVM. If this check is not successful, then Arbortext Editor will have no JVM available and will return an error if you attempt to invoke Java code from within Arbortext Editor .

The setting for javavmpath is only evaluated when the first java_ type function is called in an Arbortext Editor session. Subsequent changes to set javavmpath will not affect the running Java Virtual Machine unless you exit Arbortext Editor and start a new session. Consequently, when using the java_ type functions, you should set javavmpath before invoking a java_ type function.

Examples:

```
set javavmpath=msjava.dll
```

If set javavmpath is used with Arbortext Publishing Engine , you should protect it from being sourced again after the JVM has started. Put the set javavmpath statement inside an appropriate if statement. For example:

```
# Try to change this value only if the JVM has not started yet.
# This protects from failure in case this file is sourced again
# after the JVM has already started.
if (!java_init()) {
set javavmpath="D:\jre\lib\jvm.dll"
}
```

## Related Topics

- • java_init function

- • java_constructor function

- • java_instance function

- • java_static function

- • java_delete function

- • append_javaclass_path function

- • set javaclasspath command

- • set javadebugport command

- • set javavmargs command

- • set javavmmemory command



---

# set_keymap

# set keymap

set keymap= { user | system | name }

This command attaches the specified keymap to the current window. name is the name of a keymap previously created by the define_keymap or copy_keymap commands, or is a keymap automatically created by a map command on a window with no attached keymap. In the latter case, the name of the keymap is the same as the window name, that is, as returned by window_name() .

Any subsequent map commands in the current window not specifying a keymap argument will affect this keymap.

If the keymap is user , then the user keymap for the current window class is used. For example, the edit class map can be used for an Edit window. If the keymap is system , then the system level keymap for the current window class is used. The system map does not contain any user-level mappings. If a map command is issued with the system keymap attached, then map creates a new keymap with a name the same as the window name. This then becomes the current keymap. This automatically created keymap is deleted when the window is destroyed, if no other window has attached it.

If name specifies a prefix keymap, then the keymap remains attached only for the next key or button event. After the key or button event is looked up in the keymap, the keymap for the active window reverts to the previous keymap, unless the mapping for the event switches keymaps explicitly with another set keymap command. If the prefix keymap does not contain a mapping for the next key or button event, an error is signalled and the keymap reverts to the previous setting.

Examples

```
set keymap=user
define_keymap -prefix ctrl_x_map
define_keymap -prefix ctrl_x_4_map
map @ctrl_x_4_map d directory
map @ctrl_x_map 4 set keymap=ctrl_x_4_map
map control-x set keymap=ctrl_x_map
```

## Related Topics

- • copy_keymap command

- • define_keymap command

- • keymap_exists() built-in function

- • map command

- • undefine_keymap command



---

# set_language

# set language

set language= string

This command enables you to switch the Proximity/Merriam-Webster Linguibase to a different language dictionary. The default dictionary is English (US).

Dictionaries are available for the following languages:

- • Arabic

- • Bulgarian

- • Brazilian

- • British

- • Canadian-English

- • Canadian-French

- • Catalan

- • Croatian

- • Czech

- • Danish

- • Dutch

- • English

- • Estonian

- • Finnish

- • French

- • German

- • Greek

- • Hebrew

- • Hungarian

- • Italian

- • Latvian

- • Legal+English

- • Lithuanian

- • Medical+English

- • Norwegian

- • Nynorsk

- • Polish

- • Portuguese

- • Romanian

- • Russian

- • Slovak

- • Slovenian

- • Spanish

- • Swedish

- • Swiss-German

- • Thai

- • Turkish

- • Vietnamese

To set a different default language to be used for a document, add the set language command to the document's .acl file. You can retrieve the list of language dictionaries being used by calling the languages function.

## Related Topics

- • Supported authoring languages



---

# set_libpath

# set libpath

set libpath= dir1 [: dirn ]

This command specifies a search path for shared modules, formatting files, and font configuration files. The default path is Arbortext-path \lib . If you are running in a supported locale, the default path also includes the appropriate subdirectory of Arbortext-path \lib\locale .

Each directory specified must be separated by a semicolon. You can specify the %D , %H , or %L symbolic parameters in the path list to include the default search path.

If an Arbortext-path \custom\lib subdirectory exists at startup, the custom\lib path is automatically prepended to the path. If you are running in a supported locale, the default path also includes the associated locale subdirectory of Arbortext-path \lib\locale .

Putting your custom shared modules, formatting files, and font configuration files in the \custom\lib directory or one of its Arbortext-path \lib\locale subdirectories makes them automatically available, avoiding manual steps to add them to the path.

Example

```
set libpath="c:\mylib;%D"
```

## Related Topics

- • option_path_list function



---

# set_liteui

# set liteui

set liteui= { on | off}

This command determines the user interface used by Arbortext Editor . If set to on , this command enables a simplified user interface with a reduced set of menus and a single tool bar. If set to off , the standard user interface is presented. The default is off .

## Related Topics

- • Lightweight user interface overview

- • set fullmenus command

- • set toolbar2 command

- • set toolbar3 command



---

# set_loadmessages

# set loadmessages

set loadmessages= { on | off}

The set loadmessages command enables or disables the display of "Loading file" messages in the message area at the bottom of the Edit window when a command file is read. The default is off .



---

# set_loadpath

# set loadpath

set loadpath= d1 [: dn ]

The loadpath option lets you specify the list of directories to search when loading a package given in the require command, the require built-in function, the source command, or the JavaScript load function. A path list determines the directories to search. The default is initialized from the value of the APTLOADPATH environment variable if set, otherwise it is the packages subdirectory of Arbortext-path , the main subdirectory of packages , and the tools subdirectory of packages .

You must include the system default packages in the load path to ensure proper operation of Arbortext Editor .

If there is an Arbortext-path \custom\scripts subdirectory at startup, the \custom\scripts is automatically prepended to the load path for ACL, JavaScript, JScript, and VBScript files. Putting these supported script file types in the \custom\scripts subdirectory makes them automatically available, avoiding manual steps to add them to the path.

The path list is also automatically prepended to include any scripts added to the Arbortext-path \custom\scripts directory if you include %D in the path.

Example:

```
append_load_path("/packages")
```

Examples

```
set loadpath="c:\\Program Files\\Arbortext\\editor\\packages;
c:\\Arbortext\\editor\\packages\\main"
```

Multiple directories are delimited with semicolons, and the entire set must be enclosed in quotation marks.

You can use the append_load_path function to update the script load paths.

## Related Topics

- • append_load_path function

- • require command

- • require function

- • Symbolic parameters in path list variables



---

# set_localebackslash

# set localebackslash

set localebackslash= { on | off}

This set option controls the published rendering of the ASCII backslash character ( \ ) when running in Japanese and Korean locales. (In the Japanese locale, the backslash appears as a yen. In the Korean locale, the backslash appears as a won.)

When using font styles and requesting a specific font, the backslash will be rendered in that font. Because the backslash is an ASCII character, it is usually classified as English. However, setting localebackslash to on causes the backslash to be rendered based on the current locale. Therefore, when running in a Japanese locale with localebackslash set to on , the backslash will be rendered in a Japanese font in published output, and will appear as a yen.

Setting localebackslash impacts the publishing of the backslash character as follows:

When running in the English locale:

- • If localebackslash is set to off , classify as English.

- • If localebackslash is set to on , classify as CJK. (Resolved to the value of localedefault if is set. Otherwise, classify as Japanese.)

When running in any non-English locale:

- • If localebackslash is set to off , classify as English.

- • If localebackslash is set to on in a CJK locale, classify as the current system locale. (For example, Japanese, Korean, and so on.)

- • If localebackslash is set to on in a non-CJK locale, classify as English.



---

# set_localedefault

# set localedefault

set localedefault= { japanese | korean | simplifiedchinese | traditionalchinese}

This set option only applies if Arbortext Editor is running in English locale and if a font style, such as “serif” is specified, as opposed to a specific font. In this case, Arbortext Editor will try to classify a given Unicode character into a language.

localedefault has a default value of japanese . If a character is determined to be CJK but not assignable to a particular language, it will be assigned to this language. Also, certain Unicode blocks will be classified into this language if localefavored is set to on . The following Unicode blocks are affected:

Example: The following setting causes the ideographs to be classified as Korean. Hangul will be classified as Korean in any case.

```
set localedefault=korean
```



---

# set_localefavored

# set localefavored

set localefavored= { on | off}

This set option only applies if Arbortext Editor is running in English locale and if a font style, such as “serif” is specified, as opposed to a specific font. In this case, Arbortext Editor will try to classify a given Unicode character into a language.

When this set option is set to on , certain Unicode blocks will be considered to be characters in the locale indicated by localedefault rather than English. Default is off .

The following Unicode blocks are affected:



---

# set_markupscan

# set markupscan

set markupscan= { on | off}

This option lets you use search strings with the find command without specifying the -markup modifier. This option also specifies the default values for matching markup on the Find dialog box.

off is the default.



---

# set_menuaccelerators

# set menuaccelerators

set menuaccelerators= { on | off}

This command determines whether menu bar accelerators will be active. on is the default.

When set to off , you can still select a menu by pressing and releasing the Alt key and then typing the first letter of the menu name. (For example type F for the File menu.)



---

# set_messagelocation

# set messagelocation

set messagelocation= { statusbar | messagebox | either}

This command controls where error messages are displayed in the Arbortext Editor interface. When set to statusbar , error messages are always displayed in the status bar. In this case, messages will be truncated if necessary. When set to messagebox , error messages are always displayed in a separate message window. The default is either , which means to display error messages in the status bar if they fit, or in a message window otherwise.

```
set messagelocation=statusbar
set messageloc=messagebox
```



---

# set_modified

# set modified

set modified= { on | off}

When this command is set to on , it marks the document as modified. When this command is set to off , it marks the document as not modified. In this case, the prompt to save unsaved changes when exiting or switching documents does not occur.



---

# set_modifyattrsdeleteempty

# set modifyattrsdeleteempty

set modifyattrsdeleteempty= { on | off}

This option determines whether a CDATA attribute is deleted from a tag when you delete the last character of the attribute’s value in the Modify Attributes dialog box. The default is on meaning to delete the attribute in this case. When set to off , deleting the last character of a CDATA attribute in the Modify Attributes dialog box results in the attribute value being set to an empty string. In this case, the value (empty string) appears for the attribute value in the Modify Attributes dialog box.

This option has global scope. It corresponds to the Allow Empty String Attribute Values option in the Edit category of the Preferences dialog box.

## Related Topics

- • Modify Attributes dialog box

- • Edit preferences



---

# set_modifyattrssorted

# set modifyattrssorted

set modifyattrssorted= { on | off}

When this command is set to on (the default), Arbortext Editor alphabetically sorts the attribute names in the Modify Attributes dialog box .

When modifyattrssorted is set to off , Arbortext Editor sorts the attribute names for in the order they are defined in the (SGML) DTD. XML document attributes will remain alphabetized.

## Related Topics

- • Attributes — Overview



---

# set_movemode

# set movemode

set movemode= { on | off}

When this option is set to on , it enables a mode used to move or copy a highlighted selection using only the keyboard. When enabled, the insertion cursor is changed to the drag and drop insertion cursor and it can be moved away from the highlighted selection using normal cursor keys to the new cursor position. This mode remains in effect until either the Enter key is pressed (which accepts the move or copy) or Escape (which cancels it). The default is off .

By default, F2 enables move mode and Shift+F2 enables copy mode.



---

# set_msgfontpercent

# set msgfontpercent

set msgfontpercent= n

This command increases or decreases the point sizes of all fonts in all message windows to the percentage specified, subject to the availability of fonts. The default value is system dependent. Fonts cannot be displayed at less than 40% of their point size.

n is a number, excluding a percent ( % ) symbol.



---

# set_newlist

# set newlist

set newlist= doctype_dir1 [; doctype_dirn ]

This command specifies a list of paths to custom document type directories, which are used to populate the Document Type list in the New Document dialog box . It also enables you to remove a document type or a description of a document type from the list.

doctype_dir can be specified in the following formats:

- • an absolute path to a DTD or a document type directory

- • the base name of a document type directory

- • a path to a document type directory that is relative to one of the directory paths in the catalog path

Each document type is included in a category in the New Document dialog box. When a document type is included in the set newlist list, Arbortext Editor determines the document type’s category. If the category has already been included, the document type is added to the end of that category list. If the category is included for the first time, then the category is added to the end of the category list and the document type is its first entry. The following rules are used to determine a document type’s category:

- • Use the name of the category configured in the document type configuration file ( .dcf ) file.

- • Else, use the document type’s application or custom name configured in the application.xml or custom.xml file in the application or custom directory.

- • Else, use the name of the custom directory.

- • Else, use the Other category.

Use %D in the path to include the document types that are distributed with Arbortext Editor ( Arbortext-path \doctypes ). If you don't want to include the distributed document types, omit %D. You can specify document type directories before or after %D.

The order in which the document types appear in the list is determined by their order in the set newlist command. When you use %D, the distributed document types are listed in the following order in the New Document dialog box:

For example, if you want to add the corpmemo document type before the distributed document types and the mydoctype document type after the distributed document types in the Document Type list, set newlist to the following value:

```
set newlist="C:\\doctypes\\corpmemo;%D;mydoctype"
```

Note that the category in which these document types appear in the New Document dialog box is controlled by the category placement rules covered earlier.

You can also use the set newlist command to remove a distributed document type from the Document Type list. To do this, add a caret ( ^ ) before the document type that you want to remove.

For example, to remove the Arbortext XML DocBook V4.0 document type, set newlist to the following value:

```
set newlist="%D;^axdocbook"
```

Further, you can use the set newlist command to remove one or more descriptions of a document type from the Document Type list. Document type descriptions are defined in the DCF file associated with the document type. To remove descriptions, add a caret ( ^ ) before the document type with the description you want remove. Follow this with a pipe character ( | ) and the name of the description. You can add as many descriptions as you want, as long as a pipe character separates each description name. If the name of the description has a pipe character in its name, precede the pipe character in the name with another pipe character to escape the character in the description name.

For example, assume the corpmemo document type had two associated descriptions named hrmemo and execmemo . Set the newlist command to the following value: to remove those descriptions from the Document Type list:

```
set newlist="C:\\doctypes\\corpmemo;%D;^C:\\doctypes\\corpmemo|hrmemo|execmemo"
```

Note that in addition to using the set newlist command, you can also use the New List Configuration dialog box to control the contents of the New Document dialog box. You invoke the New List Configuration dialog box from the Advanced preferences dialog box.

The newlist option is automatically updated in your preferences file after you close a Arbortext Editor session in which you've changed the list of document types.

You can use the append_newlist_path ACL function to update the document type paths that appear in the Document Type list in the New Document dialog box.

## Related topic

- • set catalogpath command

- • New Document dialog box

- • New List Configuration dialog box

- • Advanced preferences



---

# set_objectboundarycolor

# set objectboundarycolor

set objectboundarycolor= { colorname | # rgbspec }

This option determines the color used to display object boundary borders in the Edit window. The default value for this option is gray5 . The value is either a named color or an RGB specification preceded by # . If objectboundarycolor is set to values of inherit or default , the boundaries are displayed with the default color of text in the Edit window (The default color is set with the window_set canvasforeground attribute or determined by the operating system default if otherwise not set.)

Examples:

```
set objectboundarycolor=inherit
set objectboundarycolor=blue
```



---

# set_openusesworkingdirectory

# set openusesworkingdirectory

set openusesworkingdirectory= { on | off}

When the openusesworkingdirectory option is on , the File > Open browser will display the current working directory whenever it is opened. By default, (corresponding to the off setting) the file browser remembers the last directory navigated (even across sessions) and returns to it the next time the browser is opened.



---

# set_othergraphicextensions

# set othergraphicextensions

set othergraphicextensions= extensions

This option specifies a list of additional file extensions that are recognized as graphic files when inserting graphics using drag and drop. The extensions are also added to the default list of graphics file types displayed in the Files of type drop down list of the Locate Graphic File to Reference dialog box when inserting a new graphic.

extensions specifies a list of file extension patterns of the form *. ext1 ;*. ext2 ;*. ext3 , separated by semi-colons.

Example

```
set othergraphicextensions="*.ppt;*.ico"
```

Arbortext Editor will not display such graphic files if they are not one of the supported graphic formats, unless an appropriate Active-X control is configured in the document type's .dcf file.

## Related Topics

- • set graphicsfilter option



---

# set_outputlinebreak

# set outputlinebreak

set outputlinebreak= { unix | mswin | mac}

This option controls the line break characters written when a document or text file is saved by the save or write commands. When this option is set to mswin , Arbortext Editor writes line breaks with CR/LF (Carriage Return, Line Feed) line delimiters, the normal ASCII coding for Windows. When this option is set to unix , Arbortext Editor writes text and SGML files with LF (Line Feed) line delimiters, the normal ASCII coding for UNIX platforms. When this option is set to mac , Arbortext Editor writes text and SGML files with CR (Carriage Return) line delimiters, the normal ASCII coding for Macintosh platforms. The default value is platform specific.

Arbortext Editor can read files saved in any of the formats.

## Related Topics

- • set writeunixfiles command



---

# set_outputrecordlength

# set outputrecordlength

set outputrecordlength= { n | infinity}

This command specifies the preferred maximum length, n , of output lines written when saving a file. All characters (including tags and their delimiters) are counted against outputrecordlength . Lines that are longer than the outputrecordlength command setting are broken where a record end is not significant. Lines in "asis" sections (including SGML/XML comments) or lines ending with strings where line breaks may be significant (such as in attribute values or entity declarations) may exceed the outputrecordlength setting.

The minimum value for outputrecordlength is 40 . The default is 72 .

Setting outputrecordlength to infinity , causes no specific output record length to be set and no insignificant line breaks will be included in the selection or file, preventing line breaks in PCDATA.

You can specify the -local option (as part of the set command option list) to cause outputrecordlength to have a document-scope setting, only affecting the current document. Otherwise, outputrecordlength affects the session, meaning all documents use the current session value. You can override the current value by issuing a subsequent outputrecordlength setting.

orl is a synonym for outputrecordlength .

## Related Topics

- • set writenobreakattag



---

# set_overlaypagenumbers

# set overlaypagenumbers

set overlaypagenumbers= { on | off}

When set to on , Arbortext Editor will attempt to use pass reduction to speed the formatting documents. When set to off , it makes no attempt to use pass reduction. This affects all commands that format documents ( format , print , preview ). The default value is on .

## Related Topics

- • Formatting pass reduction in ACL

- • print command

- • preview command

- • format command

- • set overlayunderflowtolerance command



---

# set_overlayunderflowtolerance

# set overlayunderflowtolerance

set overlayunderflowtolerance= { 0 | 1 | 2 | 3 | 4}

This option controls the tolerance for pass reduction. When pass reduction is enabled, this option sets the amount of disparity to accept when a final page variable value is smaller than the space it is overlaid in. Arbortext Editor never accepts an overlay if the new value is larger than the space it is overlaid on (the default is one character).

## Related Topics

- • Formatting pass reduction in ACL

- • print command

- • preview command

- • format command

- • set overlaypagenumbers command



---

# set_pagebreaktext

# set pagebreaktext

set pagebreaktext= string

This command specifies the string to display centered in the horizontal rule used to denote a forced page break when breaks are displayed in the current tag display mode. If set to a null string, then only the horizontal rule is displayed. The default is Forced Page Break .

Examples

```
set pagebreaktext=""
set pagebreaktext="New Page"
```



---

# set_pagelayoutmarkers

# set pagelayoutmarkers

set pagelayoutmarkers= { none | full}



This command controls how the page layout markup tags are displayed in the Edit view.

- • none — Page layout markup is not displayed.

- • full — All page layout markup is displayed.

This option is global. Page layout markup never appears in the document map.

The default setting is none .

The caret command is affected by the display of page layout markers. If page layout markers are displayed ( full ), they are counted during forward and backward motion.

For more detailed information on the page layout elements and their attributes, see www.arbortext.com/namespace/pagelayout . Refer to the Programmer's Reference for more detailed information about line numbering applications.

## Related Topics

- • set protectpagelayout

- • layout::add function

- • layout::clear function

- • layout::apply function

- • linenum function



---

# set_papersize

# set papersize

set papersize= { default | usletter | uslegal | a4 | b5}

This command specifies the paper size setting for the print command. The default option uses the current printer's paper size setting to initialize the document in Print Editor View , Print Published View , and the Print Preview > Print dialog boxes. If set papersize specifies one of the remaining four settings, then that specified setting is used.



---

# set_parserdeletespaces

# set parserdeletespaces

set parserdeletespaces= { on | off}

When this option is on , the parser converts runs of white space in mixed content to a single space. This is useful for reading document instances written by other applications that add additional spaces, new-lines, and tabs intended to format the document when printed, even in adding mixed content where white space is significant. The default setting is off .

This option does not apply to free-form documents, asis sections, or xml:space="preserve" sections.



---

# set_parservalidate

# set parservalidate

set parservalidate= { on | off}

This command alters the behavior of the parser used when an edit -cc is performed. This can be helpful when loading certain classes of files which are “out of balance”.

By default, all Arbortext Editor documents are normalized (that is, balanced). This means that every start tag has an end tag, no matter whether the DTD declares them as being optional or not. When you use Arbortext Editor to open a document that was authored outside of Arbortext Editor , Arbortext Editor will attempt to normalize the document by adding start and/or end tags. This is the behavior indicative of the parservalidate option being on. In some cases, these added tags may be unwanted, as the algorithm that adds them cannot always anticipate the author's original intent or compensate for a document that is well out of context. When the addition of start and end tags makes a document harder to work with (rather than easier), close the document (without saving changes), turn the parservalidate option off, and reload the document.

Be aware that the parservalidate option affects the document load process. It does not affect the editing or saving of a loaded document.

The default is on .



---

# set_paste

# set paste

set paste= { buffername | default}

This command creates a paste buffer of the name specified by buffername and makes it the current paste buffer. By default, the current paste buffer is a special buffer named default .

The current paste buffer is the buffer used by the copy_mark , paste , delete_mark , read , and write commands when no paste buffer name is specified.

Examples

```
set paste=seealso
set paste=Ifandonlyif
set paste=intropara
set paste=yrendtable
```

## Related Topics

- • copy_mark command

- • delete_mark command

- • Creating a named paste buffer

- • paste command

- • read command

- • save_buffers command

- • write command



---

# set_pasteduplicateids

# set pasteduplicateids

set pasteduplicateids= { prompt | ignore | remove | replace | show}

This command determines the action to be taken when duplicate IDs are created in a document during a paste action.

You can set the following values:

- • prompt — invoke the Paste — Duplicate IDs dialog box .

- • ignore — take no action, and write a warning to the status bar.

- • remove — strip any duplicate IDs and ID references from the pasted content.

- • replace — replace any duplicate IDs and ID references with generated unique IDs.

- • show — invoke the IDs and ID References dialog box .

Examples:

```
set pasteduplicateids=replace
```



---

# set_pastegraphicspath

# set pastegraphicspath

set pastegraphicspath = dir

This command determines the directory where graphics embedded in a Microsoft Word document are stored during a copy and paste operation. If you copy and paste part of a Microsoft Word document that contains embedded graphics, those graphics are not embedded in your XML document. Instead, they are removed from the Word document, stored on the file system, and referenced from your XML document. By default, the graphics are stored in a directory named pastegraphics in your Arbortext Editor Microsoft Windows application data directory. For example, if your Windows home directory is on the C: drive, the graphics would be stored in C:\Document and Settings\ Your Login \Application Data\PTC\Arbortext\Editor\pastegraphics .

You can set dir to the following values:

- • The full or relative path to a directory

- • %D — Represents the default pastegraphicspath subdirectory of the application directory.

- • %B — Represents the directory of the target XML document, if that directory exists and is writable.

Note that the pastegraphicspath directory is separate from the graphicspath directories. If you want the graphics in the pastegraphicspath directory to be generally available to Arbortext Editor , you must add them to the graphicspath directory list. If you add the pastegraphicspath directory to the graphicspath , then the converted graphic references will not include the directory path.

## Related Topics

- • Copying and pasting text from other applications

- • APTAPPDATADIR — Specifying an alternative application data directory

- • set graphicspath command



---

# set_pastenamespaceattrs

# set pastenamespaceattrs

set pastenamespaceattrs= { on | off}

This option controls whether necessary namespace attributes are added when certain clipboard functions are performed. For example, consider the following document fragment:

```
<parent xmlns:ns="http://www.xyz.com">
<ns:child>text</ns:child>
</parent>
```

If a user copies the child element ( <ns:child>text</ns:child> ) and pastes that somewhere in the document (or any other Arbortext Editor document that has not declared the ns prefix), the resulting pasted fragment will have the namespace attributes automatically added, resulting in the following:

```
<ns:child xmlns:ns="http://www.xyz.com">text</ns:child>
```

The namespace attributes would not be added automatically if the same fragment was:

- • Placed into a named paste buffer.

- • Pasted into another application.

In you want the namespace attributes to be automatically added in these cases, you must set the option pastenamespaceattrs to on . The default is off .

## Related Topics

- • XML namespaces



---

# set_pastepreserve

# set pastepreserve

set pastepreserve= { on | off}

This command controls the behavior of the paste command when the paste buffer contains tags or attributes which are not legal markup according to the target document's DTD. If this setting is off , such markup will be lost during a paste. If this setting is on , such markup will be preserved by inserting the non-legal tags and attributes as invalid markup.

The default value of pastepreserve is off .

## Related Topics

- • paste command

- • Invalid markup — overview



---

# set_pastesource

# set pastesource

set pastesource= [mif] [;htm] [;rtf] [;txt]

This command specifies the Microsoft Windows clipboard formats that will be converted to XML markup during Arbortext Editor copy and paste operations from other applications. The command also enables and disables the conversion of clipboard formats. To disable the conversion of clipboard formats during copy and paste operations from other applications, set this preference to an empty string.

The preference is set to some typical types of document formats that are stored on the Microsoft Windows clipboard when text is copied in an application other than Arbortext Editor , separated by semicolons ( ; ). The pastesource preference has the following default value:

```
mif;htm;rtf;txt
```

The following values are supported:

- • mif — Maker Interchange Format (MIF), the document format supported by Adobe FrameMaker

- • htm — HTML markup

- • rtf — Rich Text Format (RTF), the document format used by several Microsoft applications including Microsoft Word

- • text — Unicode and 8-bit ANSI text

If a document format is removed from the default list, that format is no longer processed during conversion for copy and paste operations. However, note that many applications put more than one document format on the clipboard when text is copied. For example, Adobe FrameMaker puts both MIF and RTF formats on the clipboard when text is copied, so you could remove mif from the pastesource list and Arbortext Editor could still use the RTF version of the copied text for the conversion operation.

Examples:

```
set pastesource=""
set pastesource="rtf"
set pastesource="htm;rtf;txt"
```

## Related Topics

- • Copying and pasting text from other applications



---

# set_pdfconfigfile

# set pdfconfigfile

set pdfconfigfile= path-and-filename

This option specifies the path and file name of the configuration file to use when publishing PDF files with the FOSI and XSL-FO engines.

If no path is specified, Arbortext Editor looks for the file in the path specified by the set composerpath option.

You can put a set pdfconfigfile statement in a custom ACL file placed in Arbortext-path \custom\init\ custom-file-name .acl , where it will be loaded at start time.

You can also put a custom configuration file in APTCUSTOM \app\ custom-file-name .appcf (APP) or in Arbortext-path \custom\lib\ custom-file-name .pdfcf (FOSI), where it will be automatically accessible.

Example:

```
set pdfconfigfile=memo.pdfcf
```

## Related topic

set appconfigfile



---

# set_pdfprinter

# set pdfprinter

set pdfprinter= printer

This option specifies a Windows printer driver for producing PDF files during the current Arbortext Editor editing session.

You can also specify a set pdfprinter statement in a custom ACL file placed in Arbortext-path \custom\init\ custom-file-name .acl , where it will be loaded at start time.

Example:

```
set pdfprinter=HP11PS
```

If the name includes spaces or special characters, it must be enclosed with quotes.

The set pdfprinter option does not work for the Arbortext Publishing Engine . The default printer that the Arbortext Publishing Engine uses is configured using the Arbortext Publishing Engine Configuration program.

## Related Topics

- • Publishing a document as a PDF File



---

# set_pecompositionemail

# set pecompositionemail

set pecompositionemail= { email_address | ""}

This option specifies an email address that is transmitted to the Arbortext PE server with every publishing request. The empty string (the default) does not transmit an email address. The value for this option persists across sessions.

The Arbortext Publishing Engine global configuration parameter com.arbortext.e3.compositionEmailPolicy and a notifier application must be set up on the Arbortext PE server to use the email when sending notification. See your Arbortext Publishing Engine administrator or Configuration Guide for Arbortext Publishing Engine for information.

## Related Topics

- • set pecompositionid command

- • set pequeuecomposition command

- • set pequeuedisplay command

- • set pequeuedeleteafterdownload command

- • set pequeuedeleteprompt command

- • set pequeuedtransactionnames command

- • set petransactionoptions command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_pecompositionid

# set pecompositionid

set pecompositionid= { user_id | ""}

This option specifies the user ID that is transmitted to the Arbortext PE server with a publishing request. The empty string (the default) does not transmit a user ID. The value for this option persists across sessions.

The value is used as the value of the HTTP query parameter name specified by the Arbortext PE server global configuration parameter com.arbortext.e3.compositionIdentificationPolicy . See your Arbortext Publishing Engine administrator or Configuration Guide for Arbortext Publishing Engine for information.

## Related Topics

- • set pecompositionemail command

- • set pequeuecomposition command

- • set pequeuedisplay command

- • set pequeuedeleteafterdownload command

- • set pequeuedeleteprompt command

- • set pequeuedtransactionnames command

- • set petransactionoptions command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_pendingdelete

# set pendingdelete

set pendingdelete= { on | off}

When set pendingdelete is set to on (the default), selected text is deleted when new characters or single tags are inserted (but only if the cursor is immediately to the left, right, or inside the selection). When this command is set to off , selected text must be explicitly cut or deleted.



---

# set_pequeuecomposition

# set pequeuecomposition

set pequeuecomposition= { on | off}

This option specifies whether Queue Transaction is checked in the Arbortext Editor File > Publish dialog boxes. When set to on , Queue Transaction is checked when the publish dialog boxes open. The default is off . The value for this option persists across sessions.

The pequeuecomposition option corresponds to the Tools > Preferences > Publishing Engine preference Queue composition transactions .

The ability to set Queue Transaction is available to Arbortext Editor users if the Arbortext PE server queueCompositionOperations global parameter is set to optional . The user can still clear Queue Transaction in the publish dialog boxes unless queuing is explicitly required to be on or off by the Arbortext Publishing Engine queueCompositionOperations parameter. In those cases, pequeuecomposition is ignored. See your Arbortext Publishing Engine administrator or Configuration Guide for Arbortext Publishing Engine for information.

## Related Topics

- • set pecompositionid command

- • set pecompositionemail command

- • set pequeuedisplay command

- • set pequeuedeleteafterdownload command

- • set pequeuedeleteprompt command

- • set pequeuedtransactionnames command

- • set petransactionoptions command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_pequeuedeleteafterdownload

# set pequeuedeleteafterdownload

set pequeuedeleteafterdownload= { on | off}

This option specifies whether Arbortext Editor should automatically delete a transaction result from the Tools > Queued Transactions viewer after the user downloads it. The default is off . The value for this option persists across sessions.

The pequeuedeleteafterdownload option corresponds to the Tools > Preferences > Publishing Engine preference Delete transaction after downloading .

## Related Topics

- • set pecompositionid command

- • set pecompositionemail command

- • set pequeuecomposition command

- • set pequeuedisplay command

- • set pequeuedeleteprompt command

- • set pequeuedtransactionnames command

- • set petransactionoptions command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_pequeuedeleteprompt

# set pequeuedeleteprompt

set pequeuedeleteprompt= { on | off}

This option specifies whether Arbortext Editor should prompt the user to confirm cancelling a queued transaction or deleting a transaction result from the Tools > Queued Transactions viewer. The default is on . The value for this option persists across sessions.

The pequeuedeleteprompt option corresponds to the Tools > Preferences > Publishing Engine preference Prompt before deleting a transaction .

## Related Topics

- • set pecompositionid command

- • set pecompositionemail command

- • set pequeuecomposition command

- • set pequeuedisplay command

- • set pequeuedeleteafterdownload command

- • set pequeuedtransactionnames command

- • set petransactionoptions command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_pequeuedisplay

# set pequeuedisplay

set pequeuedisplay= { on | off}

This option specifies whether the Tools > Queued Transactions viewer is displayed after each Arbortext Editor queued publishing request. Queue Transaction must be checked in the Arbortext Editor File > Publish dialog box to treat the publishing request as a queued transaction. pequeuedisplay is ignored if a publishing operation is not queued. The default is on . The value for this option persists across sessions.

The pequeuedisplay option corresponds to the Tools > Preferences > Publishing Engine preference Show transaction viewer after queuing .

## Related Topics

- • set pecompositionid command

- • set pecompositionemail command

- • set pequeuecomposition command

- • set pequeuedeleteafterdownload command

- • set pequeuedeleteprompt command

- • set pequeuedtransactionnames command

- • set petransactionoptions command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_pequeuedtransactionnames

# set pequeuedtransactionnames

set pequeuedtransactionnames= [' type-specification ] [; type-specification ] [...']

This option specifies the transaction name for a queued transaction being sent to Arbortext Publishing Engine .

type-specification specifies output type and transaction identifiers that can include a set of supported variables of the form:

```
type
:
specification
```

- • type

- • specification

Transaction name strings can be specified alone, with text, or in any combination, as part of the transaction name specification:

Special escape characters may be needed to produce the desired result. For example, because a ; is used as the type : specification separator, you would specify a semicolon in the transaction name using the special character combination \; .

- • Specify a semicolon as part of a transaction name by entering \; .

- • Specify a single quote as part of a transaction name by entering two single quotes.

Other special characters, such as $ , \ , : , or , may be coded as you would type them in a transaction name.

Examples:

```
set pequeuedtransactionnames='*:inventory_$t'
set pequeuedtransactionnames='pdf:$u-$d-$o;html,htmlhelp:$u-htmlpage-$d'
set pequeuedtransactionnames='pdf:''Docs\;$\:'''
set pequeuedtransactionnames='rtf:document\: my document'
```

## Related Topics

- • set pecompositionid command

- • set pecompositionemail command

- • set pequeuecomposition command

- • set pequeuedeleteafterdownload command

- • set pequeuedeleteprompt command

- • set pequeuedisplay command

- • set pequeueoverwritedirprompt command

- • set petransactionoptions command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_pequeueoverwritedirprompt

# set pequeueoverwritedirprompt

set pequeueoverwritedirprompt= { on | off}

This option specifies whether to prompt the user about overwriting an existing directory when retrieving and saving a published result from the Queued Transactions viewer ( Tools > Queued Transactions ). Some publishing types return a file and a subdirectory of related graphics files, such as HTML, RTF, or XSL. When the user chooses an existing location for saving the file, the subdirectory name and contents are checked. The default is on , prompting the user to confirm overwriting files in an existing subdirectory that is not empty.

This option only applies if Arbortext Editor is using Arbortext Publishing Engine for publishing and has Queue Transaction checked for File > Publish > HTML File , File > Publish > Using XSL , or File > Publish > RTF File .

## Related Topics

- • set pecompositionid command

- • set pecompositionemail command

- • set pequeuecomposition command

- • set pequeuedeleteafterdownload command

- • set pequeuedeleteprompt command

- • set pequeuedisplay command

- • set pequeuedtransactionnames command

- • set petransactionoptions command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_peserverurl

# set peserverurl

set peserverurl= URL

To enable the Arbortext Editor client to communicate with the Arbortext Publishing Engine , specify a valid URL (HTTP or HTTPS) to the Arbortext PE Request Manager using set peserverurl . The set peservices command must also be turned on.

Arbortext Editor retrieves information about the Arbortext Publishing Engine when Arbortext Editor starts. The returned information is stored in memory. There may be a waiting period associated with this process.

There is no default value. If you do not know your Arbortext PE Request Manager URL, ask your Arbortext Publishing Engine administrator.

In the following example, the URL specifies the server, port number, and the unique Arbortext Publishing Engine servlet specification as configured by the web server and servlet container where the Arbortext Publishing Engine is installed.

```
http://PEserver.mycompany.com:8000/e3/servlet/e3
```

Users can set this as a preference in Arbortext Editor . Choose the Tools > Preferences > Publishing Engine and enter the URL . They will also need to check Use Publishing Engine .

You can also place the set peserverurl command in a custom ACL file and put the file in the Arbortext-path \custom\init directory.

## Related Topics

- • set pequeuecomposition command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_peservices

# set peservices

set peservices= { on | off}

To enable the Arbortext Editor client to communicate with the Arbortext Publishing Engine , use set peservices=on and specify the URL to the Arbortext PE Request Manager using set peserverurl . Arbortext Editor retrieves information about the Arbortext Publishing Engine when Arbortext Editor starts. The returned information is stored in memory. There may be a waiting period associated with this process.

The default value is off . When set peservices is off , you can perform local publishing if your Arbortext Editor installation also has the appropriate licensing for Arbortext Styler , Print Composer, or Web/Wireless Composer.

Users can set this as a preference in Arbortext Editor . Choose the Tools > Preferences and choose Publishing Engine . Check the Use Publishing Engine option from the list. They will also need to specify the URL following the form:

```
http://PEserver.mycompany.com:8000/e3/servlet/e3
```

You can also place the set peservices command in a custom ACL file and put the file in the Arbortext-path /custom/init directory.

## Related Topics

- • set pequeuecomposition command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_petransactionoptions

# set petransactionoptions

set petransactionoptions= { name1:value1;name2:value2;...nameN:valueN | ""}

This option specifies additional parameters that are transmitted to the Arbortext PE server with every publishing request. The empty string (the default) does not transmit any parameters. The value for this option persists across sessions.

name1:value1;name2:value2;...nameN:valueN is a series of name : value pairs separated by semicolons, where each name is separated from its value by a colon. To include a semicolon in a name or value, specify \; . To include a colon in a name, specify \: . To include a backslash in a name, specify \\ .

See your Arbortext Publishing Engine administrator or Configuration Guide for Arbortext Publishing Engine for information.

## Related Topics

- • set pecompositionid command

- • set pecompositionemail command

- • set pequeuecomposition command

- • set pequeuedisplay command

- • set pequeuedeleteafterdownload command

- • set pequeuedeleteprompt command

- • set pequeuedtransactionnames command

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_preferentityreference

# set preferentityreference

set preferentityreference= { on | off}

For documents using a document type that supports inserting graphics as both file references and entity references, this option determines which attribute value is set when inserting graphics. In rare cases where a document contains a graphic element with both attributes set, this setting determines which attribute to use when displaying the graphic.

- • off — (The default.) Use the file reference attribute.

- • on — Use the entity reference attribute.



---

# set_prefersystemid

# set prefersystemid

set prefersystemid= { on | off}

This command determines whether the system identifier (if on ) or public identifier and entity name (if off ) is given priority when searching a catalog file to resolve an entity. The default is off , meaning that the public identifier and entity name are preferred over the system identifier.



---

# set_prefersystemidxmlcatalogs

# set prefersystemidxmlcatalogs

set prefersystemidxmlcatalogs= { on | off}

This command determines whether the system identifier is given priority when searching an XML catalog file to resolve an entity (if set to on ). The default is off , meaning that the public identifier and entity name are preferred over the system identifier.



---

# set_preservereferencepaths

# set preservereferencepaths

set preservereferencepaths= { on | off}

This option determines whether full file paths in the DITA reference attribute (usually the href attribute) are converted to relative paths during either an update references operation or the first save of a new DITA document. Set this option to on to preserve full reference paths and to off to convert full reference paths to relative paths. The default is off . This option has global scope.

Paths are only converted for file paths if a relative path can be determined from the current base URI, the DITA document directory, and any folders included in the DITA references path and graphics path. Paths are never converted for content management system (CMS) Logical IDs. Paths are also never converted for DITA references where the scope attribute is set to external or peer .

## Related Topics

- • set ditapath command

- • set graphicspath command



---

# set_printcolor

# set printcolor

set printcolor= { on | off}

When you use Print Preview or Print Published with a black and white printer driver, you can set printcolor=off to print black and white instead of grayscale for color. The default is on .



---

# set_printeditorfooter

# set printeditorfooter

set printeditorfooter= { datemark | none | pageno | "string" }

This option specifies the content included at the bottom of a printed page when choosing File > Print Editor View . The following options are available:

- • datemark — Prints a datemark that identifies the document name, date, time, and user ID for the job.

- • none — Suppresses the printing of footers. (The default footer.)

- • pageno — Prints the ordinal page number.

- • ”string” — Allows you to specify a string delimited by a pair of single quotes (') or double quotes (”) to include in the footer.



---

# set_printeditorheader

# set printeditorheader

set printeditorheader= { datemark | none | pageno | "string" }

This option specifies the content included at the top of the printed page when choosing File > Print Editor View . The following options are available:

- • datemark — Prints a datemark that identifies the document name, date, time, and user ID for the job. (The default header.)

- • none — Suppresses the printing of headers.

- • pageno — Prints the ordinal page number.

- • ”string” — Allows you to specify a string delimited by a pair of single quotes (') or double quotes (”) to include in the header.



---

# set_printeditorleftmargin

# set printeditorleftmargin

set printeditorleftmargin= dimension

This option specifies the indentation from the left edge of the paper to the point at which the text area is to begin. Enter the desired margin in the dimension argument. (For example, 8cm , 5in , 36pt , and so on.) The default units is inches.



---

# set_printeditortopmargin

# set printeditortopmargin

set printeditortopmargin= dimension

This option specifies the indentation from the top edge of the paper to the point at which the text area is to begin. Enter the desired margin in the dimension argument. (For example, 8cm , 5in , 36pt , and so on.)



---

# set_printengineoverride

# set printengineoverride

set printengineoverride= { no | app | fosi | xslfo}

This command allows you to specify the publishing engine for the current editing session, thus temporarily overriding settings made in a stylesheet’s properties. The default value is no . Using a no value after a previous override action during the same session will return the environment to its effective print engine.

See Logic for print/preview engine selection in Arbortext Styler help for further information.



---

# set_printer

# set printer

set printer= { printername | default}

This command allows you to specify the default printer for the current editing session. The default setting restores the system default for printer name. If the name includes spaces or special characters, the name must be enclosed with quotes.

Examples

```
set printer=lw
set printer="HP LaserJet"
set printer=default
```



---

# set_printstylesheet

# set printstylesheet

set printstylesheet= { name | none}

This command specifies the stylesheet to be used in place of the default stylesheet for published output (printing, print preview, and publish to PDF).

name is the path and file name of a FOSI, XSL, or Arbortext Styler stylesheet. If you don't specify an extension for the stylesheet, Arbortext Editor first looks for a .style file, then a .fos file, and finally a .xsl file.

If you specify only the stylesheet's base name, Arbortext Editor first looks for the file in the document directory, and then looks in the document type directory. If you specify a relative path (other than one that just gives the base name), Arbortext Editor looks for the file using the given path relative to the current working directory.

If you are using Arbortext Publishing Engine for publishing, it must be able to locate the stylesheet. If a document references a stylesheet using a URL, that stylesheet can be found by both Arbortext Editor and Arbortext Publishing Engine . Stylesheets that are available on the Arbortext PE server appear in the Stylesheet selection fields preceded by the notation (pe) .

When you are using Arbortext Publishing Engine , be aware of the following when setting a value for this option:

- • If you try to set the location to a local path for any type of published output, you will get an error that the stylesheet is not the name of a stylesheet on the server. The following example produces an error if Arbortext Publishing Engine publishing is enabled:

- • If you try to set the location to a stylesheet file name only (no path), Arbortext Publishing Engine looks for a stylesheet with a matching name. The following example would succeed if a stylesheet of the same name exists in a location where the Arbortext PE server looks for stylesheets.

If none is specified, or if the set printstylesheet command is not set, then the stylesheet specified by the set stylesheet command is used for published printing and print preview, as well as for the Editor view. Arbortext Publishing Engine looks for a stylesheet with a matching name.

Examples

```
set printstylesheet=memo2.style
set printstylesheet=~/mydocs/memo/memo2.fos
set printstylesheet=http://www.some_site.com/examples/techman.xsl
```

## Related Topics

- • set stylesheet command

- • Stylesheet overview

- • Configuring stylesheet order in a list

- • Using the Arbortext Publishing Engine for publishing documents

- • Opening, referencing, and saving files



---

# set_promptattrs

# set promptattrs

set promptattrs= { on | off}

When set to on , this command opens the Modify Attributes dialog box whenever an element having attributes is inserted. The default is off .



---

# set_promptentitydir

# set promptentitydir

set promptentitydir= { doc | current | entitypath}

This command sets the default location for the starting directory in two dialog boxes:

- • The Locate File to Reference dialog box displays a starting directory where you can choose a file entity. Selecting Insert > File Reference from the Arbortext Editor menu brings up the Locate File to Reference dialog box.

- • The Assign System ID dialog box displays a starting directory where you can choose a file entity. Selecting Entities > File from the Arbortext Editor menu brings up the File Entities dialog box. Selecting the Browse button next to the System ID field brings up the Assign System ID dialog box.

The doc setting is the path for the current document. The current setting is the current working directory for Arbortext Editor . The entitypath setting is the first path specified by the Entities Path preference. To find the Entities Path preference, select Tools > Preferences , and then select the File Locations category.

The default setting is doc .



---

# set_promptgraphicbrowser

# set promptgraphicbrowser

set promptgraphicbrowser= { on | off}

This command opens a file selector dialog box when a graphic tag is added. The default is on .

When set promptgraphicbrowser is off , use attribute settings to control file selection.



---

# set_promptgraphicdir

# set promptgraphicdir

set promptgraphicdir= { doc | current | graphicspath}

This command sets the default location for the starting directory in two dialog boxes:

- • The Locate Graphic File to Reference dialog box displays a starting directory where you can choose a graphic file. Selecting Insert > Graphic from the Arbortext Editor menu brings up the Locate Graphic File to Reference dialog box.

- • The Assign System ID dialog box displays a starting directory where you can choose a graphic entity. Selecting Entities > Graphic from the Arbortext Editor menu brings up the Graphic Entities dialog box. Selecting the Browse button next to the System ID field brings up the Assign System ID dialog box.

The doc setting is the path for the current document. The current setting is the current working directory for Arbortext Editor . The graphicspath setting is the first path specified by the Graphics Path preference. To find the Graphics Path preference, select Tools > Preferences , and then select the File Locations category.

The default setting is doc .



---

# set_promptgraphictags

# set promptgraphictags

set promptgraphictags= { on | off}

This command specifies whether Arbortext Editor prompts users for a choice of graphics tags when they insert a graphic at a location where more than one graphic element is valid. The default is on . Graphic tags are identified in the .dcf file .

When this option is set to off , Arbortext Editor automatically uses the primary graphic tag.



---

# set_promptnodtd

# set promptnodtd

set promptnotdtd= { on | off}

When a document is loaded for which the DTD or Schema cannot be found and promptnodtd is set to on , the user is prompted whether to perform one of the following actions:

- • Browse for the DTD/Schema.

- • Edit the document in free-form XML mode.

- • Edit the document as an ASCII document.

If promptnodtd is set to off , the use can only edit the document as an ASCII document. A document instance without a DOCTYPE declaration will be opened in free-form XML mode, without prompting if promptnodtd is set to off .

The default value of promptnodtd is on .



---

# set_promptstylesheetassociations

# set promptstylesheetassociations

set promptstylesheetassociations= { on | off}

This command options determines whether to display a dialog box warning the user that a stylesheet association in the document being published will be ignored. The default is on , which displays the warning. At the warning prompt, you can choose to turn the option off . The setting is saved and no further warnings are displayed.

This option applies when publishing documents using the Arbortext Publishing Engine , the stylesheet association applies to the type of publishing requested, and the stylesheet association specifies a stylesheet by file path rather than by URL.

If a document contains a stylesheet association specified with a path, Arbortext Publishing Engine will attempt to locate a stylesheet of the same name on the Arbortext PE server . The path in the stylesheet association will be ignored, and only the stylesheet name is used by the server to determine a match.

## Related Topics

- • set stylesheetassociations command

- • Associating a stylesheet with your document

- • Stylesheet association processing instruction

- • Using the Arbortext Publishing Engine for publishing documents

- • doc_get_stylesheet_association function



---

# set_prompttablemodels

# set prompttablemodels

set prompttablemodels= { on | off}

When set to on (the default), this command prompts users for a choice of table models when they insert a table if the cursor is in a location in which it is valid to insert more than one table model.

When this option is set to off , Arbortext Editor uses the default table model, which is set in the .dcf file .



---

# set_protection

# set protection

set protection= { write | none}

This setting allows you to change the protection on specific regions within a document type.

You can protect a document type in the .dcf file, which means you cannot edit documents that use the document type. However, you can also specify tags that are not protected in the .dcf file, allowing you to edit content within these tags. The protected status you set remains constant for tags in all instances of this document type. You can also restrict editing for individual elements in a document type in the .dcf file.

When set protection is write (the default), protected regions are displayed, but editing is prevented.

When set to none , the protection is overridden, and protected regions are displayed and can be edited.

## Related Topics

- • Restricting editing in documents



---

# set_protectpagelayout

# set protectpagelayout

set protectpagelayout= { on | off}



This command controls whether page layout markup tags are read only or if they can be added, deleted, or modified.

- • on — Page layout markup is read only and cannot be deleted.

- • off — Page layout markup may be modified.

This option is global. The default setting is on . It does not affect the delete_mark (cut) command.

For more detailed information on the page layout elements and their attributes, see www.arbortext.com/namespace/pagelayout . Refer to the Programmer's Reference for more detailed information about line numbering applications.

## Related Topics

- • set pagelayoutmarkers

- • layout::add function

- • layout::clear function

- • layout::apply function

- • linenum function



---

# set_quicktags

# set quicktags

set quicktags = { on | off}

When set quicktags is set to on , a list of valid tags appears when you press Enter while editing. When set quicktags is set to off , the list of valid tags does not appear when Enter is pressed.

If another action (such as Smart Insert ) is mapped to the Enter key, you can use the Enter key on the numeric keypad.



---

# set_reportinvalidmarkup

# set reportinvalidmarkup

set reportinvalidmarkup= { on | off}

This option controls whether invalid markup is reported as an error during the loading of a file. Even if this is set to off , invalid markup will still be reported when choosing Tools > Check Completeness .

The default is on .

## Related Topics

- • Invalid markup — overview



---

# set_requireattrs

# set requireattrs

set requireattrs= { on | off}

When set requireattrs is set to on and a tag that has required attributes is inserted, the Modify Attributes dialog box for that tag is automatically opened. If you attempt to exit or quit the Modify Attributes dialog box without supplying values for all required attributes, you are asked if you wish to supply required attributes before exiting.

If inserting the tag causes other tags with required attributes to be inserted, you are presented with the Modify Attributes dialog box for those tags as well.



---

# set_revertfocus

# set revertfocus

set revertfocus= { on | off}

This option is used by dialog windows to switch input focus from the dialog to another window, most likely the user instance window that is the parent of the dialog box.

Currently, its only use will be by the insert markup dialog box. If this option is set to “on” and the user selects markup from the dialog, the focus will be switched back to the user instance with the caret at the insertion point. Otherwise, the input focus will remain on the dialog box.



---

# set_rochange

# set rochange

set rochange= { on | off}

If set to on , this command allows you to make changes to a read-only document, although you will only be able to save these changes with the write or save_as command. off is the default.

This command is disabled in the original view of a document that contains change tracking markup.



---

# set_rowrulerunit

# set rowrulerunit

set rowrulerunit= { in | cm | mm | pt | pc | pi}

This command sets the units for the Row Ruler . Available units are:

- • in — inches (default)

- • cm — centimeters

- • mm — millimeters

- • pt — points

- • pc — picas

- • pi — picas

## Related Topics

- • set tablerulers command



---

# set_rtfpreview

# set rtfpreview

set rtfpreview= { on | off}

This option controls whether the resulting RTF document is displayed following a Publish to RTF action instigated by the File > Publish > RTF File menu option. When this option is set to on , Arbortext Editor will display the resulting RTF file in Word (or WordPad if MS Word is not installed). If you set the preference to off , the Publish to RTF dialog box will show the View RTF option unchecked. If you subsequently check the option in the dialog, the RTF document will be displayed automatically following the publish, but because you have specifically set the option to off in your preferences, the value will be unchecked each time the dialog box is opened. When the rtfpreview option is set to off , Arbortext Editor will make no attempt to display the RTF file, which is important if there is no applicable RTF reader available.



---

# set_rtfstylesheet

# set rtfstylesheet

set rtfstylesheet= { name | none}

This command specifies the stylesheet to be used as the default for the Publish > RTF File option on the File menu.

name is the path and file name of a .style or .xsl stylesheet file. If you don't specify an extension for the stylesheet, Arbortext Editor first looks for a .style file, and then a .xsl file.

The stylesheet ID processing instruction must specify rtf as the publishing type.

If you specify only the stylesheet's base name, Arbortext Editor first looks for the file in the document directory, and then looks in the document type directory. If you specify a relative path (other than one that just gives the base name), Arbortext Editor looks for the file using the given path relative to the current working directory.

If you are using Arbortext Publishing Engine for publishing, it must be able to locate the stylesheet. If a document references a stylesheet using a URL, that stylesheet can be found by both Arbortext Editor and Arbortext Publishing Engine . Stylesheets that are available on the Arbortext PE server appear in the Stylesheet selection fields preceded by the notation (pe) .

When you are using Arbortext Publishing Engine , be aware of the following when setting a value for this option:

- • If you try to set the location to a local path for any type of published output, you will get an error that the stylesheet is not the name of a stylesheet on the server. The following example produces an error if Arbortext Publishing Engine publishing is enabled:

- • If you try to set the location to a stylesheet file name only (no path), Arbortext Publishing Engine looks for a stylesheet with a matching name. The following example would succeed if a stylesheet of the same name exists in a location where the Arbortext PE server looks for stylesheets.

If rtfstylesheet is set to none or is not set, Arbortext Editor and Arbortext Publishing Engine use the Editor/Default stylesheet.

Examples

```
set rtfstylesheet=memo2
set rtfstylesheet=~/mydocs/memo/memo2.style
set rtfstylesheet=http://www.some_site.com/examples/techman_web.xsl
```

## Related Topics

- • set stylesheet command

- • Stylesheets overview

- • Displaying your XML document in a browser

- • Configuring stylesheet order in a list

- • Using the Arbortext Publishing Engine for publishing documents

- • Opening, referencing, and saving files



---

# set_saverenames

# set saverenames

set saverenames= { on | off}

When this option is set to on (the default), the save command saves a document by writing a temporary file, deleting the original file, and then renaming the temporary file to the original name. When this option is set to off , save rewrites the original file directly. The default is on to prevent data loss in the case of insufficient disk space. However, the rename strategy may sometimes fail on certain kinds of network file systems. For those situations, set saverenames to off .



---

# set_savewindowconfiguration

# set savewindowconfiguration

set savewindowconfiguration= { yes | no | prompt}

This option determines whether Arbortext Editor saves certain current window and view settings when it exits. This option has a global scope. The settings are:

- • yes — Save the settings.

- • no — Do not save the settings.

- • prompt — Prompt the user to decide whether settings should be saved. This is the default setting.

The size and location of all modeless dialog boxes that have been opened during the current session will be saved.

The set command options saved by this command are the menu, toolbar, split window, and window position settings.

If one of the preceding option values differs between the Edit pane and the Document Map pane, then the value for the current view is used.

## Related topic

- • window_reset_configuration function

- • write_preferences function



---

# set_selectionsvc

# set selectionsvc

set selectionsvc= { on | off}

If set to on (the default), this command allows you to paste between the Edit window and other windows on the workstation. If set to off , Arbortext Editor has a separate paste buffer, the contents of which are unaffected by cutting or copying from other windows.



---

# set_selectscan

# set selectscan

set selectscan= { on | off}

When set to on (the default), the find command highlights the string it locates. Otherwise, the cursor is positioned after the string.



---

# set_sgmlextension

# set sgmlextension

set sgmlextension= ext

This command specifies the extension to use for newly saved SGML files. sgm is the default. The Save As dialog box and save_as command add this extension if the specified file does not already have an extension and the -sgmlextension option is non-null.

Note, a period should not be included as part of the extension.

Examples

```
set sgmlextension=sgm
set sgmlextension="sgml"
```

## Related Topics

- • set asciiextension command

- • set defaultfilter command

- • set htmlextension command

- • set xmlextension command



---

# set_sgmlselection

# set sgmlselection

set sgmlselection= { on | off}

The off option for this command allows you to paste between windows in regular untagged ASCII format. If set to on (the default), the contents are pasted in tagged format. This is necessary if you are pasting tags, entities, or tables from one window to another.



---

# set_showattrs

# set showattrs

set showattrs= { on | off}

When this command is set to on (the default) attributes are listed after the tag name as part of the Edit window tag display.



---

# set_showbreaksfulltags

# set showbreaksfulltags

set showbreaksfulltags= { on | off}

This command enables or disables the display of FOSI specified forced page and column breaks when the tag display is full. The default is off .



---

# set_showbreaksnotags

# set showbreaksnotags

set showbreaksnotags= { on | off}

This command enables or disables the display of FOSI specified forced page and column breaks when the tag display is none. The default is on .



---

# set_showbreakspartialtags

# set showbreakspartialtags

set showbreakspartialtags= { on | off}

This command enables or disables the display of FOSI specified forced page and column breaks when the tag display is partial. The default is off .



---

# set_showcomments

# set showcomments

set showcomments= { on | off}

This command enables or disables the display of comments in the Edit window and the Document Map. If your cursor is in the Edit window and set showcomments is set to off , comment text in the Edit window is hidden and barbell icons represent the comment tags if the tag display mode is full or partial . If the tag display mode is none , no markers appear in the Edit window.

If your cursor is in the Document Map and set showcomments is set to off , the comment icon, label, and text are hidden in the Document Map.

The default setting is on .

## Related Topics

- • Configuring elements to be ignored during a spelling check



---

# set_showconrefs

# set showconrefs

set showconrefs= { on | off}

This command enables or disables the display of content references in the Edit window and the Document Map. If set showconrefs is set to off , referenced content is not displayed in the Edit window. If set showconrefs is set to on , the content of the element is replaced by the resolved value of the content reference attribute, displayed as generated text.

Display of generated text must be enabled to show content reference content.

The default setting is on .

## Related Topics

- • Content reference overview

- • Specifying content reference attribute



---

# set_showcursor

# set showcursor

set showcursor= { on | off}

When this command is set to on , the cursor is visible in the view. The default value is on except for the dir view.



---

# set_showdashedlines

# set showdashedlines

set showdashedlines= { on | off}

If this option is set to on (the default), then the lines between elements in the Document Map are dashed. If set to off , then the lines are solid.



---

# set_showdetail

# set showdetail

set showdetail= { on | off}

If this option is set to on (the default), then detailing is displayed in the current window as set by the detail command. If set to off , then the document is full expanded, regardless of the detailing set for each element.

Note, this command has no effect in the Document Map view.



---

# set_showemptyelement

# set showemptyelement

set showemptyelement= { on | off}

This command allows you to control the gray block with the element name in it when there's an element without any content. If this option is set to on (the default), then an element with no content will be displayed as a gray box containing the start tag name. If the option is set to off , then the empty element box is not displayed.



---

# set_showentities

# set showentities

set showentities= { none | file | text | all}

This command determines whether file and text entities are displayed in the Edit window document. When set to none , no file or text entities are displayed. When set to file or text , the file or text entities are displayed respectively. If set to all , this command displays both types of entities. The default is all .



---

# set_showiconsfulltags

# set showiconsfulltags

set showiconsfulltags= { on | off}

This command enables or disables the display of icons in the Edit pane when the tag display is set to full tags. The icon display is view local scope. The default setting is on .

The command does not affect the display of icons in the Document Map. Also, the display of icons within a table cell depends on the tag display set within the table through the set tabletagdisplay command.

The following icons are affected by this command:

- • File entity icons

- • Product icons

- • Icons set using the oid_set_icon function

## Related Topics

- • set showiconspartialtags

- • set showiconsnotags

- • Showing and hiding tags



---

# set_showiconsnotags

# set showiconsnotags

set showiconsnotags= { on | off}

This command enables or disables the display of icons in the Edit pane when the tag display is set to no tags. The icon display is view local scope. The default setting is off .

The command does not affect the display of icons in the Document Map. Also, the display of icons within a table cell depends on the tag display set within the table through the set tabletagdisplay command.

The following icons are affected by this command:

- • File entity icons

- • Product icons

- • Icons set using the oid_set_icon function

## Related Topics

- • Set option scope

- • set showiconsfulltags

- • set showiconspartialtags

- • Showing and hiding tags



---

# set_showiconspartialtags

# set showiconspartialtags

set showiconspartialtags= { on | off}

This command enables or disables the display of icons in the Edit pane when the tag display is set to partial tags. The icon display is view local scope. The default setting is on .

The command does not affect the display of icons in the Document Map. Also, the display of icons within a table cell depends on the tag display set within the table through the set tabletagdisplay command.

The following icons are affected by this command:

- • File entity icons

- • Product icons

- • Icons set using the oid_set_icon function

## Related Topics

- • Set option scope

- • set showiconsfulltags

- • set showiconsnotags

- • Showing and hiding tags



---

# set_showignorems

# set showignorems

set showignorems= { on | off}

This command enables or disables the display of marked sections with an IGNORE status. If off , IGNORE status sections are hidden. Barbell icons represent hidden marked sections if the tag display is full or partial. If the tag display mode is none, no markers appear. The default is on .



---

# set_showlinks

# set showlinks

set showlinks= { on | off}

This command enables or disables the display of the _link tag pair and _target tag icon. The default is on .



---

# set_showmsgnum

# set showmsgnum

set showmsgnum= { on | off}

If this option is set to on (the default), then error and informational messages displayed in the status line and various dialog boxes are prefixed with a unique message number on the form [Annnnn] . If set to off , then message numbers are not displayed.

This message number may be needed by Arbortext Technical Product Support when reporting error situations, particularly when error messages have been customized at your site to display non-standard messages.



---

# set_showmsstatus

# set showmsstatus

set showmsstatus= { on | off}

If this command is set to on (the default), marked section status keywords are displayed in the _include , _ignore , _cdata , or _rcdata tags used to denote marked sections. If set to off , then only the tag name appears.



---

# set_shownamespaceattrs

# set shownamespaceattrs

set shownamespaceattrs= { on | off}

This command controls the display of namespaced attributes. When set to on (the default), this command displays the attributes of namespaced elements in the Editor view. When set to off , the attributes of namespaced elements are suppressed in the Editor view.

## Related Topics

- • set showunknownattrs

- • set showxmlnsattrs



---

# set_shownamespaceprefix

# set shownamespaceprefix

set shownamespaceprefix= { on | off}

This command enables or disables the display of namespace prefixes in the Edit pane and Document Map. If this option is set to off , all elements are displayed without namespace prefixes.

The option has view scope and the default setting is on .

## Related Topics

- • Set option scope



---

# set_shownewlines

# set shownewlines

set shownewlines= { on | off}

If this command is set to on (the default), a newline character will display in asis sections. If set to off , the newline character will not display.



---

# set_showobjectboundaries

# set showobjectboundaries

set showobjectboundaries= { on | off}

This option determines whether object boundary borders are displayed in the Edit window. The default value for this option is on . This option has view scope.



---

# set_showpastewindow

# set showpastewindow

set showpastewindow= { on | off}

The command determines whether the Invalid Paste Structure dialog box opens when a copy and paste operation from another application to Arbortext Editor fails due to context errors in the converted XML markup. The default is on , meaning that if the markup you are trying to paste is not valid at the paste location, the Invalid Paste Structure dialog box opens. This dialog box enables you to view the markup that Arbortext Editor is trying to paste into the document. The dialog also enables you to copy and paste all or part of that markup into your document.

The Invalid Paste Structure dialog box has a Do not show this window when paste results are invalid check box. When this check box is selected, the showpastewindow preference is set to off and the dialog box no longer appears when pasting converted XML markup would result in context errors. In this case, a message appears on the status bar saying that the paste operation would result in a context error.

Examples:

```
set showpastewindow=on
```

## Related Topics

- • Copying and pasting text from other applications

- • Invalid Paste Structure dialog box



---

# set_showprelimuserules

# set showprelimuserules

set showprelimuserules= { on | off}

This command controls if the preliminary index (non-zero userules) is displayed in the editor view. The on setting displays the preliminary index.

The default is off .

## Related Topics

- • set userules command



---

# set_showprofileshading

# set showprofileshading

set showprofileshading= { on | off}

This command enables or disables profile and inline applicability shading in the Edit windows. The default is off .

Profile shading is configured in the profile configuration file ( .pcf ) for the document type.

Inline applicability shading is presented in a single color. The color is defined with the set inlineapplicabilitycolor option for your application.

## Related Topics

- • Using shading for profiled elements

- • Working with Applicability

- • set inlineapplicabilitycolor



---

# set_showscreenhiddenattrs

# set showscreenhiddenattrs

set showscreenhiddenattrs= { on | off}

This command controls the display of attributes configured in the document type configuration file ( .dcf ) to be hidden in the Edit and Document Map panes. When set to off , Arbortext Editor doesn't display hidden attributes. When set to on , the .dcf file setting is ignored, and Arbortext Editor displays hidden attributes. The default setting is off .

## Related Topics

- • Hiding attributes

- • hidden_tag function

- • Document type configuration files



---

# set_showspaces

# set showspaces

set showspaces= { on | off}

This command controls the appearance of space and tab characters. When showspaces is on , Arbortext Editor displays a character for each space or tab in text content:

- • Spaces: a small dot above the baseline

- • No break spaces: the degree/ring character (°)

- • Tabs: a right arrow (⇒)

The default is off .



---

# set_showunknownattrs

# set showunknownattrs

set showunknownattrs= { on | off}

This command controls whether attributes which were not declared are displayed or suppressed. Such attributes are a form of invalid markup.

The default is on .

## Related Topics

- • Invalid markup — overview

- • set shownamespaceattrs

- • set showxmlnsattrs



---

# set_showxmlnsattrs

# set showxmlnsattrs

set showxmlnsattrs= { on | off}

This command controls whether namespace declaration attributes (XML attributes of the form xmlns and xmlns: prefix , where prefix is any valid XML markup name) are displayed in the Edit and Document Map views. The default is on and the option has view scope.



---

# set_skipautosavecheck

# set skipautosavecheck

set skipautosavecheck= { on | off}

When set skipautosavecheck is set to on , Arbortext Editor does not check for the presence of autosave or crash files when opening a file. Autosave and crash files are still created, if that functionality is enabled, but are not used to open a file.

The default setting is off .



---

# set_skipinlineelements

# set skipinlineelements

set skipinlineelements= { on | off}

The set option and advanced preference skipinlineelements controls whether inline elements are treated as word boundaries when checking spelling. When set to on (the default), the spelling checker will ignore inline element boundaries when evaluating the spelling of words. When set to off , the spelling checker treats each inline element as a word boundary.

The preference has document scope.

The setting of skipinlineelements may be overridden depending on the setting of the .dcf file entry spellCheckingNewWord for the document type. spellCheckingNewWord has the following possible values:

- • yes — An element will always start a new word, regardless of the setting of the skipinlineelements preference.

- • no — An element will not be considered a word boundary, regardless of the setting of the skipinlineelements preference.

- • default — (The default setting.) An element will follow the setting of the skipinlineelements preference.



---

# set_smartinsert

# set smartinsert

set smartinsert= { on | off}

When set smartinsert is set to on , Smart Insert is enabled if it is configured in the document type's .dcf file . When set smartinsert is set to off , Arbortext Editor uses the current cursor location when inserting elements.

The default setting is off . Note that the set quicktags setting can be affected by the setting of set smartinsert .

## Related topic

- • Inserting markup using Smart Insert



---

# set_spellabsoluteaddresses

# set spellabsoluteaddresses

set spellabsoluteaddresses= { on | off}

When this command is set to off , the spell checker ignores absolute URL’s (tokens starting with http:// , https:// , file:// , ftp:// , and mailto: ), absolute file paths (tokens that begin with / , \\ , or X :\ ), and e-mail addresses (tokens that contain a @ and a . ). When set to on , the spell checker will flag those tokens as misspellings. The default is off .



---

# set_spellalphanums

# set spellalphanums

set spellalphanums= { on | off}

When this command is set to on , the spelling checker flags words containing combinations of alphabetic and numeric characters; for example, ten4 or dos2unix. If this option is off , words containing numbers are ignored. The default is off .



---

# set_spellinteractive

# set spellinteractive

set spellinteractive= { on | off}

When this command is set to on , Arbortext Editor automatically checks your document for spelling errors and marks any suspect words with a red wavy underline. The default is on .

## Related Topics

- • Checking spelling

- • Spell checking preferences



---

# set_spellnumerals

# set spellnumerals

set spellnumerals= { on | off}

When this command is set to on , the spell checker flags all Arabic and Roman numerals in the document. The default is off .



---

# set_spellrepeatword

# set spellrepeatword

set spellrepeatword= { on | off}

When this command is set to on , the spell checker flags words occurring twice in succession, such as the the. The default is on .



---

# set_spellsentencecapitalization

# set spellsentencecapitalization

set spellsentencecapitalization= { on | off}

If this command is set to on , the spell checker flags words following a terminal punctuation mark (such as a period) that are not capitalized. The default is off .



---

# set_spellskiptags

# set spellskiptags

set spellskiptags= { on | off}

When this command is set to on , the content in elements defined in the document type's .dcf file is skipped during a spelling check. The default is on .

## Related Topics

- • spellskip_tag function

- • Spell checking preferences

- • Configuring elements to be ignored during a spelling check



---

# set_stricterrors

# set stricterrors

set stricterrors= { on | off}

When set stricterrors is set to on , a reference to an undeclared ACL variable in a package declared with the _STRICT_ global variable will be flagged as an error. Arbortext Editor will terminate the ACL script at the point at which the undeclared variable is referenced. If set to off , a warning message is sent to the Debug Messages window if set debug = 1 . Otherwise, no warning or error is generated.

## Related Topics

- • Predefined variables

- • set traceback



---

# set_stylerconfirmdeletes

# set stylerconfirmdeletes

set stylerconfirmdeletes= { on | off}

When set to on (the default), users are prompted whenever they delete an object such as an element, context, condition, or page set in Arbortext Styler .

This command corresponds to Options > Confirm Deletions in Arbortext Styler .



---

# set_stylercontextformatxsl

# set stylercontextformatxsl

set stylercontextformatxsl= { on | off}

When set to on , Arbortext Styler displays contexts in XSL syntax. When set to off (the default), Arbortext Styler displays contexts in a text format.

For example, if you create a context for title within chapter , the XSL version displays as chapter/title , and the text version displays as title in chapter .

This command corresponds to Options > Show Contexts as XSL in Arbortext Styler .



---

# set_stylerdocelementsonly

# set stylerdocelementsonly

set stylerdocelementsonly= { on | off}

When set to on (the default), Arbortext Styler displays in the Elements list all of the elements currently used in the document. When set to off , Arbortext Styler displays all elements in the stylesheet in the Elements list, which typically corresponds to all elements in the DTD or schema.

Setting this command to on is the equivalent of activating the View > Only Elements in Document menu option in Arbortext Styler .



---

# set_stylerdoctypeelementsonly

# set stylerdoctypeelementsonly

set stylerdoctypeelementsonly= { on | off}

When set to off (the default), Arbortext Styler displays all elements in the stylesheet in the Elements list. When set to on , Arbortext Styler displays in the Elements list the elements from the stylesheet that belong to the current document type.

Setting this command to on is the equivalent of activating the View > Only Elements in Document Type menu option in Arbortext Styler .



---

# set_stylererrorcolor

# set stylererrorcolor

set stylerrrorcolor= { colorname | # rgbspec }

This command determines the font color used in error messages displayed throughout Arbortext Styler . The value is either a named color or an RGB specification preceded by # . The default is red .

Examples (the following are equivalent):

```
set stylererrorcolor=red
set stylererrorcolor=#ff0000
```



---

# set_stylerexplicitfontcolor

# set stylerexplicitfontcolor

set stylerexplicitfontcolor= { colorname | # rgbspec }

This command determines the font color used to display the labels of properties that have been explicitly set in the Arbortext Styler window or dialog boxes. This setting also applies to the color of the property category‘s label when a property from that category is explicitly set. The value is either a named color or an RGB specification preceded by # . The default is blue .

Examples (the following are equivalent):

```
set stylerexplicitfontcolor=red
set stylerexplicitfontcolor=#ff0000
```



---

# set_stylergentexttagfontcolor

# set stylergentexttagfontcolor

set stylergentexttagfontcolor= { colorname | # rgbspec }

This command determines the font color of the generated text (gentext) tag in the Arbortext Styler generated text edit window. The value is either a named color or an RGB specification preceded by # . The default is brown .

The generated text tag also has a background color that is configured using the set stylergentexttagshading setting.

Examples (the following are equivalent):

```
set stylergentexttagfontcolor=red
set stylergentexttagfontcolor=#ff0000
```



---

# set_stylergentexttagshading

# set stylergentexttagshading

set stylergentexttagshading= { colorname | # rgbspec }

This command determines the font shading of the generated text (gentext) tag in the Arbortext Styler generated text edit window. The value is either a named color or an RGB specification preceded by # . The default is yellow .

The generated text tag also has a font color that is configured using the set stylergentexttagfontcolor setting.

Examples (the following are equivalent):

```
set stylergentexttagshading=red
set stylergentexttagshading=#ff0000
```



---

# set_stylerhassourceeditsfontcolor

# set stylerhassourceeditsfontcolor

set stylerhassourceeditsfontcolor= { colorname | # rgbspec }

This command determines the font color of the text confirming the presence of edited source for an element, in the Description tab of the Arbortext Styler window. The value is either a named color or an RGB specification preceded by # . The default is orange .

Note that the setting will not affect the edited source symbols in the list view window, only the heading of the Description tab and the text advising you that source edits exist for the element for the particular output source.

You can set this option as a preference from the Tools > Preferences dialog box. Click the Advanced button and choose stylerhassourceeditsfontcolor .

Examples (the following are equivalent):

```
set stylerhassourceditsfontcolor=red
set stylerhassourceeditsfontcolor=#ff0000
```



---

# set_stylerhtmlversionoverride

# set stylerhtmlversionoverride

set stylerhtmlversionoverride= { html | xhtml | html5 | xhtml5 | no}

This command allows you to specify the version of HTML to be output during a publishing operation, temporarily overriding settings made in a stylesheet’s properties. The default value is no . Using a no value after a previous override action during the same session will revert the HTML version to that specified by the stylesheet.



---

# set_stylerindeterminatefontcolor

# set stylerindeterminatefontcolor

set stylerindeterminatefontcolor= { colorname | # rgbspec }

This command determines the font color used to display the label in the Arbortext Styler window when the value of the field is inherited from multiple sources and the values vary. This may occur, for example, for a Size field when multiple contexts are selected for a title element and the font size varies between contexts. The value is either a named color or an RGB specification preceded by # . The default is orange .

Examples (the following are equivalent):

```
set stylerindeterminatefontcolor=red
set stylerindeterminatefontcolor=#ff0000
```



---

# set_stylerlistsfes

# set stylerlistsfes

set stylerlistsfes= { on | off}

This option is a preference that determines whether the Styler Formatting Elements (SFEs) configured for a stylesheet are displayed along with regular elements in the Elements list in Arbortext Styler . This preference can be set to on or off . A value of on displays SFEs in the list, while setting the preference to off removes them.

You can set this option as a preference from the Tools > Preferences dialog box. Click the Advanced button and choose stylerlistsfes . Select on or off as the choice for the preference.

Setting this command to on is the equivalent of activating the View > Styler Formatting Elements menu option in Arbortext Styler .



---

# set_stylerlistufes

# set stylerlistufes

set stylerlistufes= { on | off}

This option is a preference that determines whether the User Formatting Elements (SFEs) configured for a stylesheet are displayed along with regular elements in the Elements list in Arbortext Styler . This preference can be set to on or off . A value of on displays UFEs in the list, while setting the preference to off removes them.

You can set this option as a preference from the Tools > Preferences dialog box. Click the Advanced button and choose stylerlistufes . Select on or off as the choice for the preference.

Setting this command to on is the equivalent of activating the View > User Formatting Elements menu option in Arbortext Styler .



---

# set_stylernotbasefontcolor

# set stylernotbasefontcolor

set stylernotbasefontcolor= { colorname | # rgbspec }

This command determines the font color used to display the Properties to edit label in the Arbortext Styler window when the value of the field is any value except Base (All Uses) . The value is either a named color or an RGB specification preceded by # . The default is red .

Examples (the following are equivalent):

```
set stylernotbasefontcolor=red
set stylernotbasefontcolor=#ff0000
```



---

# set_stylerresolveconditions

# set stylerresolveconditions

set stylerresolveconditions= { on | off}

When set to on (the default), Arbortext Styler resolves conditions for the contexts selected in the Edit window.

This command corresponds to Options > Resolve Conditions in Arbortext Styler .



---

# set_stylershowduplicatedefs

# set stylershowduplicatedefs

set stylershowduplicatedefs= { on | off}

This option is a preference that determines whether Arbortext Styler displays duplicate element definitions that are contained in both the main stylesheet and associated modules. This preference can be set to on or off . A value of on displays the duplicated definitions in the list, while setting the preference to off removes them.

You can set this option as a preference from the Tools > Preferences dialog box. Click the Advanced button and choose stylershowduplicatedefs . Select on or off as the choice for the preference.

Setting this command to on is the equivalent of activating the View > Show Duplicate Definitions menu option in Arbortext Styler .



---

# set_stylershowunstyled

# set stylershowunstyled

set stylershowunstyled= { on | off}

When set to on (the default), Arbortext Styler highlights missing and unstyled elements in the Edit window, as well as in all Arbortext Styler previews. A missing element is any element that does not have a matching context in the stylesheet.

Missing and unstyled elements are highlighted by displaying the element start and end with a blue font color on a pink background. This option also generates new lines before and after these elements in Arbortext Styler previews.

This command corresponds to Options > Highlight Unstyled Elements in Arbortext Styler .



---

# set_stylersyncelements

# set stylersyncelements

set stylersyncelements= { on | off}

When set to on (the default), placing the cursor inside an element in Arbortext Editor causes that element to be selected in the Arbortext Styler Elements list.

This command corresponds to the Options > Synchronize Elements with Editor menu choice in Arbortext Styler .



---

# set_stylerunstyledfontcolor

# set stylerunstyledfontcolor

set stylerunstyledfontcolor= { colorname | # rgbspec }

This command determines the font color of the element name in the unstyled indicator in any Arbortext Styler preview window when the element has a Style property of unstyled . The value is either a named color or an RGB specification preceded by # . The default is blue .

The unstyled indicator also has a background color that is configured using the set stylerunstyledfontshading setting.

Examples (the following are equivalent):

```
set stylerunstyledfontcolor=red
set stylerunstyledfontcolor=#ff0000
```



---

# set_stylerunstyledfontshading

# set stylerunstyledfontshading

set stylerunstyledfontshading= { colorname | # rgbspec }

This command determines the font shading color of the element name in the unstyled indicator in any Arbortext Styler preview window when the element has a Style property of unstyled . The value is either a named color or an RGB specification preceded by # . The default is red .

The unstyled indicator also has a font color that is configured using the set stylerunstyledfontcolor setting.

Examples (the following are equivalent):

```
set stylerunstyledfontshading=red
set stylerunstyledfontshading=#ff0000
```



---

# set_stylervalnestedpagesetsxslfo

# set stylervalnestedpagesetsxslfo

set stylervalnestedpagesetsxslfo= { on | off}

The default value for this option is off . When set to on , Arbortext Styler requires strict XSL-FO compliance when validating page sets. Arbortext Styler is able to process nested XSL-FO page sets, so they are not reported as validation errors. However, if you plan to export your stylesheet as XSL-FO and use it in another application, nested page sets are not strictly XSL-FO compliant. If you enable this option, Arbortext Styler reports nested XSL-FO page sets as validation errors. This option is disabled if you are using FOSI as your Arbortext Styler print engine.

This command corresponds to the Require XSL-FO Compliance check box in the Arbortext Styler Validate Page Sets dialog box.



---

# set_stylerviewapproottags

# set stylerviewapproottags

set stylerviewapproottags= { on | off}

When set to on , tags in the PTC APP root template of a stylesheet are made available for edit in Arbortext Styler .

PTC APP root template tags display in the Functions list.

The default value is off .

This command corresponds to the Tools > Edit APP Root Template Source menu option in Arbortext Styler .



---

# set_stylesheet

# set stylesheet

set stylesheet= name

This command specifies the stylesheet to be used in place of the default stylesheet for the Editor view.

name is the path and file name of a Arbortext Styler or FOSI stylesheet. If you don't specify an extension for the stylesheet, Arbortext Editor first looks for a .style file, then a .fos file.

If you specify only the stylesheet's base name, Arbortext Editor first looks for the file in the document directory, and then looks in the document type directory. If you specify a relative path (other than one that just gives the base name), Arbortext Editor looks for the file using the given path relative to the current working directory.

Examples

```
set stylesheet=memo2.style
set stylesheet=/mydocs/mem/memo2.fos
set stylesheet=http://www.some_site.com/examples/techman.xsl
```

## Related Topics

- • set printstylesheet command

- • Stylesheet overview

- • Opening, Referencing, and Saving Files



---

# set_stylesheetassociations

# set stylesheetassociations

set stylesheetassociations= { on | off}

When the stylesheetassociations option is set to on , which is the default, the user can specify stylesheet associations, and the stylesheet associations are stored as processing instructions in a document when it is saved. It might be necessary to turn this option off at some sites due to SGML or XML applications that are broken by the presence of stylesheet association processing instructions before the document type declaration.

When the option is set to off , there is no user interface for specifying stylesheet associations, and files that are saved are written without stylesheet association processing instructions, which also removes any pre-existing processing instructions.

If a stylesheet association is specified when Arbortext Editor is using Arbortext Publishing Engine for publishing, only the stylesheet name is saved to the document. If a stylesheet of the same name exists on the Arbortext PE server , it will appear in the stylesheet list of selections for the print and publish dialog boxes with the (pe) notation.

## Related Topics

- • set promptstylesheetassociations command

- • Associating a stylesheet with your document

- • Stylesheet association processing instruction

- • Using the Arbortext Publishing Engine for publishing documents



---

# set_tablecalscolnamerequired

# set tablecalscolnamerequired

set tablecalscolnamerequired= { on | off}

Controls whether new entry tags in a CALS table will have their colname attribute set. The default setting is off .



---

# set_tablecolumnaligncharacter

# set tablecolumnaligncharacter

set tablecolumnaligncharacter= char

Controls the default alignment character ( char ) on the Justification tab of the Table Properties dialog box .

Examples

```
set tablecolumnalignchar="."
set tablecolumnalignchar="-"
```



---

# set_tablecolumnresizable

# set tablecolumnresizable

set tablecolumnresizable= { on | off}

Controls the ability to resize table columns. When set to on (the default), the user interface allows table column widths to change. When set to off , the following user interface changes occur:

- • You cannot drag the column markers in the Column Tool.

- • In the Table Properties dialog box, the Column tab is disabled.

## Related Topics

- • Column Ruler

- • Table Properties dialog box



---

# set_tabledefaultrulethickness

# set tabledefaultrulethickness

set tabledefaultrulethickness= dimen

The set tabledefaultrulethickness command specifies the rule thickness for tables in the current document. However, it has no impact on tables whose markup specifies a rule thickness.

This setting applies to all rules in existing CALS and Arbortext tables. It only applies to outer frame rules in HTML tables. Arbortext Editor also uses the tabledefaultrulethickness value as the default border width in the Insert Table dialog box for HTML tables.

Allowable units of measure are:

- • in — inches (the default)

- • cm — centimeters

- • mm — millimeters

- • pt — points

- • pi or pc — picas

- • px — pixels

The default setting is 1pt (one point).

Examples

```
set tabledefaultrulethickness=25pt
set tabledefaultrulethickness=1pc
```

You can view changes greater than 1pt in the Edit window.

## Related Topics

- • Tables overview

- • Table properties dialog box



---

# set_tableminimumemptyrowheight

# set tableminimumemptyrowheight

set tableminimumemptyrowheight= dimen

This command determines the default published height for empty table rows. The default value is 15 pt . Specify the numeric value and the unit of measure. Allowable units of measure are:

- • in — inches (the default)

- • cm — centimeters

- • mm — millimeters

- • pt — points

- • pi or pc — picas

- • px — pixels

Examples

```
set tableminimumemptyrowheight=10cm
set tableminimumemptyrowheight=350pt
```



---

# set_tableminimumrowheight

# set tableminimumrowheight

set tableminimumrowheight= dimen

This command determines the default published height for table rows with content. The default value is 15 pt . Specify the numeric value and the unit of measure. Allowable units of measure are:

- • in — inches (the default)

- • cm — centimeters

- • mm — millimeters

- • pt — points

- • pi or pc — picas

- • px — pixels

Examples

```
set tableminimumrowheight=10cm
set tableminimumrowheight=350pt
```



---

# set_tablenewrowheightunit

# set tablenewrowheightunit

set tablenewrowheightunit= { in | cm | mm | pt | pc | pi}

This command sets the units for assigning explicit heights to new rows. Available units are:

- • in — inches (the default)

- • cm — centimeters

- • mm — millimeters

- • pt — points

- • pc — picas

- • pi — picas

Examples

```
set tablenewrowheightunit=in
set tablenewrowheightunit=pt
```



---

# set_tablerulers

# set tablerulers

set tablerulers= { on | off}

Controls the display of the Table Rulers. When set to on , the Row Ruler, Column Ruler and Table Icon appear in the edit view. When set to off , these interface items are hidden.

You can set the Window preference for displaying Table Rulers. Go to Tools > Preferences , and, in the Window category, turn on Table Rulers .

You can also set Table Rulers display using the View > Tables > Table Rulers menu command.

## Related Topics

- • Row Ruler

- • Column Ruler

- • Table Icon



---

# set_tablesavecolumnwidthunit

# set tablesavecolumnwidthunit

set tablesavecolumnwidthunit= { * | in | cm | mm | pt | pc | pi | off}

This command sets the units that Arbortext Editor will convert all column widths to when saving documents. This option does not apply to HTML tables. Available settings are:

- • * — proportional

- • in — inches

- • cm — centimeters

- • mm — millimeters

- • pt — points

- • pc — picas

- • pi — picas

- • off — disables column width conversion



---

# set_tabletagdisplay

# set tabletagdisplay

set tabletagdisplay= { none | partial | full | inherit | cycle}

This command changes the tag display for table content where none does not display most tags or icons, partial displays small icons for most tags, full (the default) displays the fully spelled-out tags, inherit automatically follows the setting for set tagdisplay , and cycle moves among the four types of displays in the order full, partial, none, inherit.

Display characteristics for a particular tag pair in a particular mode are set with the tag_display command.



---

# set_tabletags

# set tabletags

set tabletags= { on | off}

Controls the display of tables. When set to off , the tags that define table structure are hidden (regardless of the current tag display) and a graphical representations of tables appear in the edit view. When set to on , this graphical structure is hidden.

If the current tag display ( set tagdisplay command) is set to full or partial , you will see the tags that define a table's structure. If set tabletags is set to on and the current tag display is set to none , only the content of the table will be visible.

## Related Topics

- • set tagdisplay command



---

# set_tabletoolbarautohide

# set tabletoolbarautohide

set tabletoolbarautohide= { on | off}

When set to on , set tabletoolbarautohide automatically hides the Table tool bar whenever the cursor is outside a table. This setting corresponds to the Table Toolbar Only When Table is Active check box of the Window tab of the Tools > Preferences dialog box. The default is off .

## Related Topics

- • set toolbar3 command

- • Window preferences



---

# set_tableuiextensions

# set tableuiextensions

set tableuiextensions= { on | off}

Several forms of table formatting are saved in the document as processing instructions. These processing instructions are not necessarily portable to other authoring and publishing tools. The tableuiextensions option controls whether the user interface will allow an author to apply table formatting that is saved as a processing instruction.

When this option is set to on (the default), all table formatting is available. When set to off , several pieces of the user interface become disabled:

- • The Style , Color , and Width options are not available on the Modify Borders dialog box.

- • The Modify Font dialog box is not available from within the Cell tab of the Table Properties dialog box.

- • For OASIS Exchange tables, the Table tab of the Table Properties dialog box is not available.

- • The Published Output option does not appear on the Row tab of the Table Properties dialog box.

- • For OASIS Exchange and Arbortext tables, you cannot specify a Shading option.

- • For OASIS Exchange tables, you cannot modify the Row Height on the Row tab of the Table Properties dialog box. Similarly, you cannot drag the row height markers on the Row Tool.

- • For HTML tables, you cannot modify individual cell rules in the Modify Borders dialog box.

Note that this command controls the ability to make future changes to table formatting. It will not eliminate existing processing instructions previously added to support formatting changes.

## Related Topics

- • Modifying columns, rows, and cells

- • Adjusting row height

- • Changing the table width

- • Modifying cell font

- • Breaking the table across pages

- • Shading cells



---

# set_tablewidth

# set tablewidth

set tablewidth= dimen

This command determines the default screen display width for tables in the Edit window. The default value is 100% . Specify the numeric valued and the unit of measure. Allowable units of measure are:

- • % — percent

- • in — inches (the default)

- • cm — centimeters

- • mm — millimeters

- • pt — points

- • pi or pc — picas

- • px — pixels

The APTTBLWIDTH environment variable can set the default. The set units option can set the unit of measurement.

Examples

```
set tablewidth=10cm
set tablewidth=350pt
```



---

# set_tablewriteemptycellmarkup

# set tablewriteemptycellmarkup

set tablewriteemptycellmarkup= { on | off}

Arbortext Editor creates table cells which contain <entry> </entry> tag pairs. However, Arbortext Editor can edit tables with tables cells not containing <entry> </entry> tag pairs created by other applications.

When tablewriteemptycellmarkup is set to off , Arbortext Editor omits the empty <entry> </entry> tag pairs when saving such a document. (Certain other circumstances, described in Handling empty table cells , can cause Arbortext Editor to include the tags when saving the document.)

When tablewriteemptycellmarkup is set to on , Arbortext Editor saves the empty entry elements in the document.

The default setting for tablewriteemptycellmarkup is off .



---

# set_tagdisplay

# set tagdisplay

set tagdisplay= { none | partial | full | cycle}

This command changes the tag display where none (the default) does not display most tags or icons, partial displays small icons for most tags, full displays the fully spelled-out tags, and cycle moves among the three types of displays in the order full, partial, none

Display characteristics for a particular tag pair in a particular mode are set with the tag_display command.

## Related Topics

- • set showemptyelement command



---

# set_tagfontcolor

# set tagfontcolor

set tagfontcolor= { colorname | # rgbspec }

This command determines the font color used to display markup icons in the Edit window. The value is either a named color or an RGB specification preceded by # . The default is brown .

You can determine whether Arbortext Editor ignores this setting by using the set usecolorsettings option.

Examples

```
set tagfontcolor=red
set tagfontcolor=#ff0000
```



---

# set_tagfontpercent

# set tagfontpercent

set tagfontpercent= n

This command increases or decreases the size of all tags to the percentage specified. The default value is system dependent. Fonts cannot be displayed at less than 40% of their point size.

n is a number, excluding a percent ( % ) symbol.

## Related Topics

- • set editfontpercent command

- • set fontpercent command

- • set helpfontpercent command



---

# set_tagscan

# set tagscan

set tagscan= { on | off}

The tagscan option allows you to use search strings with the find , caret , and window commands without specifying the -t modifier. off is the default.



---

# set_tagtemplatepath

# set tagtemplatepath

set tagtemplatepath= d1 [: dn ]

This command specifies a list of directories to search for tag templates. Specify each directory separated by a semicolon. A list of multiple directories must be enclosed in quotation marks. The default path is the path specified by APTTAGTPLDIR environment variable , if it exists. If that environment variable is not set, the directory specified by the $home ACL variable is used.

If there is an Arbortext-path \custom\tagtemplates subdirectory at startup, the custom\tagtemplates path is automatically prepended to the tag template path. Putting your tag templates in the custom\tagtemplates subdirectory makes them automatically available, avoiding manual steps to add them to the path.

You can put custom tag templates you want associated with a particular document type into a custom\doctypes\ doctype \tagtemplates directory or in the original location of the document type's doctype \tagtemplates directory.

You can also specify alternate or additional locations for your tag templates directory via the document type’s DCF file. Refer to Specifying an alternate location for a tag templates directory for information.

You can use the append_tagtemplate_path function to update the tag template path.

## Related Topics

- • Using tag templates



---

# set_textentityfontcolor

# set textentityfontcolor

set textentityfontcolor= { inherit | colorname | # rgbspec }

This command determines the font color used to display text entities in the Edit window. If inherit is set, the text entities are displayed the same as the text of the Edit window document. The value is either inherit , or a named color, or an RGB specification preceded by # . The default is inherit .

You can determine whether Arbortext Editor ignores this setting by using the set usecolorsettings option.

Examples

```
set textentityfontcolor=inherit
set textentityfontcolor=red
set textentityfontcolor=#ff0000
```



---

# set_textentitymarkers

# set textentitymarkers

set textentitymarkers= { none | full | partial | default}

This command determines the display of text entity markup icons when text entities are displayed in the Edit window document. When set to any of the following, the setting determines the display regardless of the Edit window document tag display setting:

- • none — No tags or markers are displayed.

- • full — All markup tags and markers are displayed.

- • partial — Only the file entity markers around the file entity are displayed.

When set to default , text entity markup takes on the same setting as the Edit window document tag display. The default is none .



---

# set_toolbar

# set toolbar

set toolbar= { on | off}

The toolbar option turns on or off the display of the Edit (toolbar1), Markup (toolbar2), Table (toolbar3), and Application (toolbar4) tool bars. It is an easy way to show or hide all tool bars without changing the individual setting for each tool bar. The default is on .

## Related Topics

- • set toolbar1 command

- • set toolbar2 command

- • set toolbar3 command

- • set toolbar4 command

- • set toolbar5 command

- • Window preferences



---

# set_toolbar1

# set toolbar1

set toolbar1= { on | off}

The toolbar1 option turns on or off the Edit tool bar. The default is on.

## Related topic

- • set toolbar command



---

# set_toolbar2

# set toolbar2

set toolbar2= { on | off}

The toolbar2 option turns on or off the Markup tool bar. The default is on .

## Related Topics

- • set toolbar command

- • set liteui command



---

# set_toolbar3

# set toolbar3

set toolbar3= { on | off}

The toolbar3 option turns on or off the Table tool bar. The default is on.

## Related Topics

- • Table tool bar

- • set toolbar command

- • set liteui command



---

# set_toolbar4

# set toolbar4

set toolbar4= { on | off}

The toolbar4 option turns on or off the Application tool bar .

## Related topic

- • set toolbar command



---

# set_toolbar5

# set toolbar5

set toolbar5= { on | off}

The toolbar5 option turns on or off toolbar5. Use this command if you have created toolbar5 using XUI.

## Related topic

- • set toolbar command



---

# set_traceback

# set traceback

set traceback= n

The set traceback command allows you to set the number of levels displayed in the function call traceback if a user-defined ACL function aborts with a runtime error. The default is 10 . If you set traceback to 0 (zero), you disable the function call traceback.

Examples

```
set traceback=20
set traceback=6
set traceback=0
```



---

# set_trackcontext

# set trackcontext

set trackcontext= { on | off}

This command enables or disables the display of the element structure containing the cursor in the status bar (for example, memo body para | para). The default is off .



---

# set_undolimit

# set undolimit

set undolimit= n

This command specifies the maximum memory, in bytes, to use for undo buffer space for each open document. The default setting is 500 KB (or 512,000 bytes) of memory. The preference can be adjusted to a number of between 1 and 66536 to allow for more memory to be made available for the undo . If set to 0 , there is no limit other than available virtual memory. Note that if you set this number too low, you will inhibit undo capabilities.  Setting the preference to an excessively high value could affect performance.

The undo limit is based on volume of data deleted. Arbortext Editor holds the deleted data in memory.

The undo buffer is allocated for each document. When a document is closed, its undo history will be discarded and the memory released.

Examples

```
set undolimit=50000
set undolimit=0
```



---

# set_units

# set units

set units= { in | cm | mm | pt | pi | px}

This option specifies the units of measurement used for table width display if the set tablewidth option is not set to a % value. The default is in . The units of measurement are:

- • in — inches

- • cm — centimeters

- • mm — millimeters

- • pt — points

- • pi — picas

- • px — pixels



---

# set_updaterecentdocuments

# set updaterecentdocuments

set updaterecentdocuments= { on | off}

When the this option is on (the default), a file added to the recently used list of files on the File menu is also added to the Windows Start > My Recent Documents list.



---

# set_usecolorsettings

# set usecolorsettings

set usecolorsettings= { on | off}

This option determines whether to use the set fileentityfontcolor , set textentityfontcolor , set gentextfontcolor , and set tagfontcolor options. When set to off , those options are ignored, and the contents of entities, generated text, and tags are drawn with the same font color as surrounding text.

This option has a view scope and defaults to on .



---

# set_useepic43keymappings

# set useepic43keymappings

set useepic43keymappings= { on | off}

The default keyboard mappings used in Epic Editor 4.4 and beyond are different than those used in the 4.3 release. If you prefer the 4.3 version of keyboard mappings, you can turn this option on to restore them.

This option has a global scope and defaults to off . This option takes effect the next time you start Arbortext Editor .

The following table shows the keyboard shortcut for each Arbortext macro (for executing Arbortext Editor actions and menu selections), with the version 4.3 and updated keyboard mappings. If a column is blank it means that there is no shortcut for that command in the corresponding release.



---

# set_user

# set user

set user= user

This option specifies the user ID for the current user. The default value is defined by the system, and may be user-specific if the operating system requires every user to log-in.

If the system provides no default and the option is not set then the first time the user value is needed, a popup will appear to request the user and fullname values. If the popup is dismissed (for example, when running under Arbortext Publishing Engine all pop-ups are dismissed automatically) then a unique session id will be used for user.

The value of user is associated with tracked changes and is put into each change record as the record is created.

For example, if the user's name is Edgar Allan Poe, the user id could be:

```
set user=eap
```



---

# set_usercolor

# set usercolor

set usercolor= { colorname | # rgbspec }

This command allows you to set the user color. The value is either a named color or an RGB specification preceded by # . By default, no color is selected. This set option corresponds to the User Color preference in Tools > Preferences > User Information .

This color can be used to identify the changes you make when change tracking is active. This color identifies you in the Edit window, in print and in published output. If you do not choose a user color, a color will still be assigned to you to identify you in a document. If this setting conflicts with another user’s color, you may be assigned a different color for that document only. This value will not be changed.

Examples (the following are equivalent):

```
set usercolor=red
set usercolor=#ff0000
```



---

# set_userdictpath

# set userdictpath

set userdictpath= d1 [: dn ]

This command searches a list of directories, separated by semicolons, for user-defined dictionaries that are used by the Spell Checker. Specify the directories containing the dictionaries; don't specify individual dictionary names. The default search path is Arbortext-path \lib\proximity\userdict . You can specify the %D or %H symbolic parameters in the path list in the path, %D specifies the default search path.

If there is an Arbortext-path \custom\dictionaries subdirectory at startup, the custom\dictionaries path is automatically prepended to the dictionary path. Putting your custom dictionaries in the custom\dictionaries subdirectory makes them automatically available, avoiding manual steps to add them to the path.

You can use the append_userdict_path function to update the tag template path. You can also specify the user dictionary path in Tools > Preferences > Spelling dialog box.

Example

```
set userdictpath=/users/pat:/company/dicts
set userdictpath="c:\Program Files\Arbortext\editor\dict;c:\Arbortext\mydict"
```

## Related Topics

- • APTDICTPATH environment variable



---

# set_userinput

# set userinput

set userinput= { on | off}

Setting userinput to off blocks user input to the Edit window. If set userinput is set to on (the default), input is not blocked.

## Related Topics

- • disable_windows function



---

# set_userules

# set userules

set userules= { on | off}

When on, values of usetexts with non-zero userules are inserted into "preliminary userule oids" and are processed by userule processing. When off, usetexts with non-zero userules are completely ignored. This saves processing time and memory use. Do not use the off setting when creating final output.

The default is on.

## Related Topics

- • set showprelimuserules command



---

# set_usexsdasdtd

# set usexsdasdtd

set usexsdasdtd= { on | off}

This set option provides a means to migrate a document instance from a DTD to an XML Schema.

If set to on , an instance with a DOCTYPE declaration resolving to a .dtd file will instead be parsed against the XML Schema if there is a .xsd file with the same base name as the .dtd in the document type directory. In this case, the ISO standard character entities will automatically be converted to the equivalent Unicode characters. Character entities that cannot be converted will be flagged as undefined entities because an XML schema cannot declare entities.

The default is off . This option has no effect for SGML document types.



---

# set_validatenamespaces

# set validatenamespaces

set validatenamespaces= { on | off}

When set to on , this option specifies that Arbortext Editor will validate foreign namespaces used in a document and therefore disallow any elements not declared in the document type. When the option is off (the default), any element name with a prefix associated with a foreign namespace is considered valid.



---

# set_validationmode

# set validationmode

set validationmode= { all | dtd | schema}

Specifies how documents in the current session are to be validated.

- • all — The default. Validates documents against their declared DTD or schema. Documents with both a DTD and schema declared will be validated against each document type. The document will be validated against the schema before the DTD.

- • dtd — Validate documents against their declared DTD only.

- • schema — Validate documents against their declared schema only.



---

# set_vertspacefulltags

# set vertspacefulltags

set vertspacefulltags= { on | off}

This command enables or disables the display of vertical space due to FOSI specified pre-space and post-space when the tag display is full . The default is on .



---

# set_vertspacemax

# set vertspacemax

set vertspacemax= dimen

This command determines the maximum space that is displayed before or after a vertical element when the display of vertical space is enabled. Allowable units of measure are: pc, pt, cm, mm, and in . The default is 14.46pt (2 inches).

Example

```
set vertspacemax=1.5in
```



---

# set_vertspacemin

# set vertspacemin

set vertspacemin= dimen

This command determines the minimum space that is displayed before or after a vertical element when the display of vertical space is enabled. Allowable units of measure are: pc, pt, cm, mm, and in . The default is 0pt .

Example

```
set vertspacemin=10pt
```



---

# set_vertspacenotags

# set vertspacenotags

set vertspacenotags= { on | off}

This command enables or disables the display of vertical space when the tag display is set to none . The default is on .



---

# set_vertspacepartialtags

# set vertspacepartialtags

set vertspacepartialtags= { on | off}

This command enables or disables the display of vertical space when the tag display is set to partial . The default is on .



---

# set_vertspacepercent

# set vertspacepercent

set vertspacepercent= n

This command determines the percentage of the vertical space shown in the Edit window. The default is 100 .

n is a number, excluding a percent ( % ) symbol.



---

# set_view

# set view

set view= { edit | docmap | column}

This command determines the view displayed in the Arbortext Editor window. When set to edit , the Edit view is displayed. When set to docmap , the Document Map is displayed. When set to column , the Column view is displayed.

This option has local view scope and is not saved to the user preferences file.

## Related Topics

- • set viewmode command



---

# set_viewchangetracking

# set viewchangetracking

set viewchangetracking= { original | changesapplied | changeshighlighted}



This option specifies the type of change tracking markup to display. It applies to the current Document Map and Edit view pair. The default setting is changesapplied .

- • original — Shows document as if all pending change records have been rejected.

- • changesapplied — Shows document as if all pending change records have been accepted.

- • changeshighlighted — All pending change records are visible.

When this command is set to original , the view is read-only (and will not be affected by changing rochange ).

Example

To view the document without any pending changes displayed:

```
set viewchangetracking=original
```



---

# set_viewmode

# set viewmode

set viewmode= { edit | docmap | column}

This command determines the view displayed in the Arbortext Editor window. When set to edit , only the Edit view is displayed. When set to docmap , the Document Map is displayed in a split view with the Edit view. When set to column , the Column view is displayed in a split view with the Edit view. The position of the split between the two views is determined by the set docmapside option. The percentage of the window allocated to the Document Map or Column view is determined by the set docmappercent option.

This option has local window scope and is saved to the user preferences file.

## Related Topics

- • set view command

- • set docmapside command

- • set docmappercent command



---

# set_webstylesheet

# set webstylesheet

set webstylesheet= { name | none}

This command specifies the stylesheet to be used as the default for the Publish > For Web option on the File menu.

name is the path and file name of a .style or .xsl stylesheet file. If you don't specify an extension for the stylesheet, Arbortext Editor first looks for a .style file, and then a .xsl file.

The stylesheet ID processing instruction must specify web as the publishing type.

If you specify only the stylesheet's base name, Arbortext Editor first looks for the file in the document directory, and then looks in the document type directory. If you specify a relative path (other than one that just gives the base name), Arbortext Editor looks for the file using the given path relative to the current working directory.

If you are using Arbortext Publishing Engine for publishing, it must be able to locate the stylesheet. If a document references a stylesheet using a URL, that stylesheet can be found by both Arbortext Editor and Arbortext Publishing Engine . Stylesheets that are available on the Arbortext PE server appear in the Stylesheet selection fields preceded by the notation (pe) .

When you are using Arbortext Publishing Engine , be aware of the following when setting a value for this option:

- • If you try to set the location to a local path for any type of published output, you will get an error that the stylesheet is not the name of a stylesheet on the server. The following example produces an error if Arbortext Publishing Engine publishing is enabled:

- • If you try to set the location to a stylesheet file name only (no path), Arbortext Publishing Engine looks for a stylesheet with a matching name. The following example would succeed if a stylesheet of the same name exists in a location where the Arbortext PE server looks for stylesheets.

If webstylesheet is set to none or is not set, Arbortext Editor and Arbortext Publishing Engine use the Editor/Default stylesheet.

Examples

```
set webstylesheet=memo2
set webstylesheet=~/mydocs/memo/memo2.style
set webstylesheet=http://www.some_site.com/examples/techman_web.xsl
```

## Related Topics

- • set stylesheet command

- • Stylesheets overview

- • Displaying your XML document in a browser

- • Configuring stylesheet order in a list

- • Using the Arbortext Publishing Engine for publishing documents

- • Opening, referencing, and saving files



---

# set_webzonepolicy

# set webzonepolicy

set webzonepolicy= { on | off}

Determines whether the Microsoft URL security zone policy is used to determine whether a link using the arbortext-editor: protocol is allowed from a web browser. If webzonepolicy is set to on (the default) and a link using the arbortext-editor: protocol is invoked from a web browser, Arbortext Editor first determines the zone of the encoded document path. The link is then allowed or denied according to this policy:

- • Local Machine zone — allow

- • Local Intranet zone — allow

- • CMS zone — allow

- • Trusted Sites zone — allow

- • Internet zone — deny

- • Restricted Sites zone — deny

If the link is denied, then a message is displayed saying that the request has been denied for security purposes. If webzonepolicy is set to off , then no links using the arbortext-editor: protocol are allowed at all and a similar message is displayed.



---

# set_windows

# set windows

set windows= { open | closed}

The windows option closes all open Arbortext Editor windows when set to closed . Setting windows to open (the default) opens them up again.

## Related Topics

- • window_close() built-in function

- • window_open() built-in function



---

# set_windowsscriptdebugger

# set windowsscriptdebugger

set windowsscriptdebugger= { on | off}

The windowsscriptdebugger option controls whether any installed Windows script debugger can be launched.

If windowsscriptdebugger is set to on , any system-installed Windows script debugger will be launched automatically when the active script engine encounters one of the following conditions:

- • A run-time error. (Script syntax errors will not launch the debugger.)

- • A Stop statement in a VBScript.

- • A debugger statement in a JScript.

Do not set this option to on if no debugger is installed.

If windowsscriptdebugger is set to off , no script debugger will be launched. Runtime errors will be reported in message boxes.

The default value of the windowsscriptdebugger option is off .

## Related Topics

- • set javascriptinterpreter



---

# set_wordincludechars

# set wordincludechars

set wordincludechars= chars

Specifies a list of punctuation characters that Arbortext Editor should considered as word-constituent characters for selection. The default value is the null string so underscores and dashes are not considered part of a word selection by default.

Example:

```
set wordincludechars='-_()$'
```



---

# set_wordscan

# set wordscan

set wordscan= { on | off}

When this command is set to on , the find and substitute commands consider whole words only when matching text. For example, the search string the does not find then or there. The default is off .



---

# set_wrapprompt

# set wrapprompt

set wrapprompt= { on | off}

When this command set to on , a prompt message is issued by the find or substitute commands when they reach the end (or beginning) of the document. The default is off .



---

# set_wrapscan

# set wrapscan

set wrapscan= { on | off}

When the wrapscan command is set to on (the default), the find and substitute commands revert to the beginning of the document to continue a search (or to the end for a reverse search).



---

# set_writeabsolutesysid

# set writeabsolutesysid

set writeabsolutesysid= { on | off}

This option determines whether the save and write commands will update the system identifier on the DOCTYPE declaration when writing XML documents. If the option is off (the default), the system ID will not be changed if it is not null. If the original system ID is null, Arbortext Editor writes the base name of the DTD corresponding to the document type. If the option is on , then Arbortext Editor writes an absolute URI for the system ID corresponding to the document type used to load the document (or to the -public option if given). If the -sysid option is used on the write command, then that value is used regardless of the writeabsolutesysid option setting.

The set writeabsolutesysid command also affects the href written for stylesheet associations. If this options is off, the hrefs of existing stylesheet associations are written unchanged, and for new stylesheet associations where the stylesheet is in the same directory as the document or the DTD, a relative URI is written for the href . When this option is on, relative URIs are converted to absolute file:// URI specifications.

## Related Topics

- • write command

- • save command

- • Stylesheet association processing instruction

- • Opening, referencing, and saving files



---

# set_writeaticomment

# set writeaticomment

set writeaticomment= { on | off}

This option instructs Arbortext Editor to write a Arbortext identifying comment as the second line of any saved SGML or XML file. The comment includes the <!DOCTYPE...> declaration for the document type.

If this option is set to off , the comment is suppressed.

The default setting is on .



---

# set_writechangetracking

# set writechangetracking

set writechangetracking= { original | changesapplied | changeshighlighted}



Specifies the write command output:

- • original — Show the document as if all pending change records have been rejected.

- • changesapplied — Shows the document as if all pending change records have been accepted.

- • changeshighlighted — Shows all pending change records.

The default is changeshighlighted .

Example

To set the write output to show the document as if all pending changes have been rejected:

```
set writechangetracking=original
```



---

# set_writecheck

# set writecheck

set writecheck= { on | off}

When this command is set to on (the default), a warning is issued if you try to use the write command to write over an existing file.



---

# set_writeentdecls

# set writeentdecls

set writeentdecls= { rootallchildall | rootallchildref | rootallchildnone | roottreerefchildref | roottreerefchildnone | rootrefchildref}

This option controls which entity declarations are written in the subsets of the root document and its children when these are written by either the save or write commands. (Children include file entities and embedded objects. When the documentation below refers to file entities, the discussion applies to embedded objects as well.)

Generally, this option should be used consistently within an application. It may not be desirable for individuals to have their own settings, or for this to be frequently changed, though some settings have value when used temporarily for clean up purposes.

If it is desired that an entity declaration in the internal subset be preserved when there are no references to that entity anywhere in the document instance, including the internal subset itself (for instance, a parameter entity only referenced from the external subset of the DTD), then writeentdecls must be set to one of the three rootall values.

The following table summarizes the choices. More detailed explanations follow the table.

If you are changing your site from using one of these modes to another, it is recommended that you load all documents and force the writing of all the entities of the document, before continuing with editing. To simplify this process, use the ACL alias save_all_docs . It will cause the root document and all recursively referenced file entities to be saved, whether or not the document/entity is marked as modified.



---

# set_writenobreakattag

# set writenobreakattag

set writenobreakattag= { on | off | default}

This option determines whether line breaks are inserted at element boundaries or before the element close character ( > ) when writing and saving XML documents.

This option has a global scope. The settings are:

- • on — Breaks will not be inserted at element boundaries and before element close characters ( > ).

- • off — (The default.) Breaks may be inserted at element boundaries and before element close characters ( > ).

## Related Topics

- • set outputrecordlength



---

# set_writenonasciichar

# set writenonasciichar

set writenonasciichar= { entref | numref | char}

The set writenonasciichar command controls how Arbortext Editor writes out non-ASCII characters. The options are:

- • entref — Arbortext Editor writes out non-ASCII characters as character entity references. (If a numeric entity reference had been inserted as a character, Arbortext Publishing Engine will write the numeric entity reference as a character.)

- • numref — Arbortext Editor writes out non-ASCII characters as numeric character references.

- • char — Arbortext Editor writes out non-ASCII characters as characters in the target encoding. If Arbortext Editor cannot find the characters in the target encoding, it writes out the non-ASCII characters as numeric character references.

The abbreviation of writenonasciichar is writenonascii .

When used with the set entityinputconvert and set entityoutputconvert commands, the set writenonasciichar also controls how Arbortext Editor writes out character entities.



---

# set_writepi

# set writepi

set writepi= { all | default | touchup | structural | none}

This option determines how the save , write , and save_as commands treat Arbortext Editor processing instructions. This option has a global scope. The settings are:

- • all — Saves Arbortext Editor processing instructions.

- • default — Saves Arbortext Editor processing instructions except for <?Pub _display?> . This is the default setting.

- • touchup — Saves Arbortext Editor processing instructions except for <?Pub _display?> and processing instructions that the editor uses to remember the state of the document display (for example, <?Pub Caret?> ).

- • structural — Saves the same Arbortext Editor processing instructions as the touchup setting except for <?Pub_font?> , <?Pub_newcolumn?> , <?Pub_newline?> , <?Pub_newpage?> and <?Pub_nolinebreak?> .

- • none — Removes Arbortext Editor processing instructions.

If the -pi or -nopi option is specified for the write , save , or save_as commands, then that value is used regardless of the set writepi option setting.

## Related Topics

- • Processing instructions overview

- • save_as command

- • oid_content function

- • selection_markup function



---

# set_writeunixfiles

# set writeunixfiles

set writeunixfiles= { on | off}

By default, the line delimiters written by Arbortext Editor are dictated by the set outputlinebreak command. Setting the writeunixfiles option to on forces Arbortext Editor to write UNIX line endings (line feed). Setting the writeunixfiles option to off (the default) resets the outputlinebreak option to its default value of mswin .

## Related Topics

- • set outputlinebreak command



---

# set_writeunspecifiedattrs

# set writeunspecifiedattrs

set writeunspecifiedattrs= { none | fixed | all}

The set writeunspecifiedattrs command controls the writing of unspecified attributes. An unspecified attribute is any element attribute that does not have a user-defined value. Attributes that have a default value set in the Document Type Definition (DTD) but have not been set using the Arbortext Editor user interface are also considered unspecified.

The default setting is none , which means that Arbortext Editor will not write unspecified attributes when saving a file. When set to fixed , Arbortext Editor writes only the unspecified fixed attributes when saving a file. When set to all , Arbortext Editor writes all unspecified attributes, except for CDATA attributes, when saving a file. Note that the fixed and all settings both significantly increase the size of the written file.

Arbortext recommends that you do not use this command unless you need to write an instance of a file for an application that does not read attributes from a DTD. If you save a document with unspecified attributes and then re-open the document with Arbortext Editor , Arbortext Editor will display the attributes as local modifications.



---

# set_xmlextension

# set xmlextension

set xmlextension= ext

This command specifies the extension to use for newly saved XML files. xml is the default. The Save As dialog box and save_as command add this extension if the specified file does not already have an extension and the -xmlextension option is non-null.

A period should not be included as part of the extension.

Examples

```
set xmlextension=xml
set xmlextension="xml"
```

## Related Topics

- • set asciiextension command

- • set defaultfilter command

- • set htmlextension command

- • set sgmlextension command



---

# set_xmlversion

# set xmlversion

set xmlversion= { 1.0 | 1.1}

This command controls the XML version used when creating and saving an empty document using the ACL function doc_open or the AOM Application interface openDocument() method. The XML version number specified is written on the XML declaration at the start of the empty document when it is saved. If set to 1.1 , it enables support for XML 1.1 characters in names and data. The default is 1.0 to use XML 1.0 rules.

XML 1.1 allows control characters in the range #x1 through #x1F and #x7F through #x9F , most of which are forbidden in XML 1.0. If xmlversion=1.1 , these characters are accepted and written as numeric character references, regardless of the set writenonasciichar setting, to conform to the XML 1.1 specification.

## Related Topics

- • set writenonasciichar command

- • doc_open function