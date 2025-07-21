

---

# Copy_and_Paste_Overview

# Copy and Paste Overview

When you copy text to the Microsoft Windows clipboard, certain applications copy more than just text to the system clipboard. For example, most Microsoft applications put the following formats on the clipboard for a copy operation:

- • RTF markup (Rich Text Format)

- • HTML markup

- • Unicode text

- • ANSI text

Adobe FrameMaker puts FrameMaker Interchange Format (MIF) on the clipboard during a copy operation, as well as RTF markup and Unicode and ANSI text.

Using Arbortext Import/Export technology, Arbortext Editor can automatically map content on the clipboard to tagging appropriate for the document type of the document where the content is being pasted. Arbortext Editor generates a basic map template based on the following information:

- • The source type of the copied text on the clipboard

- • The document type of the document currently being edited in Arbortext Editor where the text is being pasted

- • The document type configuration file ( .dcf ) associated with the document type

- • The Arbortext Styler stylesheet ( .style ) associated with the document type

Support for copying and pasting from other applications has been added to the .dcf files for the following document types distributed with Arbortext Editor :

- • ATI XML DocBook V4.0 ( axdocbook )

- • Arbortext Article ( asdocbook )

- • The DITA Topic and Concept document types

- • The Technical Information Application topic document types

- • HTML

In most cases, copying and pasting works for both XML and SGML document types because Arbortext Editor has automatic features to handle XML-specific markup in a manner compatible with SGML markup.

While Arbortext Editor automatically creates Import MapTemplate files for these document types, you can use Arbortext Import to create custom maps for your site. For example, your site might use custom Microsoft Word style names site that need to be defined in the MapTemplate, or you might want to define additional inline elements for a paste operation besides the emphasis elements.

If you have an custom document type, you can also configure your document type to intelligently paste content from other applications into Arbortext Editor .

## Related topics

- • Copying and pasting text from other applications

- • Document type configuration files



---

# Customizing_the_Paste_Special_Dialog_Box

# Customizing the Paste Special Dialog Box

Besides the automatic copy and paste support, you can control how content from other applications is pasted into a document through the Paste Special dialog box. After you have copied content from another application, you can select Edit > Paste Special to open the dialog box and select how you want the content to be pasted into your document.

By default, the Paste Special dialog box enables you to paste clipboard content in the following formats:

- • bullet list

- • numbered list

- • paragraphs

- • table (from tabular text)

- • table with no title

- • table with title

- • text

- • title

- • web link

You can customize this dialog box to change the supported document formats, change the format to a different MapObject, or add support for elements in your custom document type. The supported document formats are configured in the following file: Arbortext-path \lib\locale\en\pasteAsList.xlf . Put your customized pasteAsList.xlf file in custom\lib\locale\en (or in your locale specific subdirectory).

The pasteAsList.xlf file uses the XML Localization Interchange File Format (XLIFF) document type. See www.oasis-open.org/committees/xliff/documents/xliff-specification.htm for more information about XLIFF. The XLIFF document type specifies sets of source and target tags, where the source tag contains the string to be translated and the target tag contains the string to be displayed in the dialog box.

Following is the markup from pasteAsList.xlf for the bullet list document format type:

```
<trans-unit id="1" resname="bullet_list">
<source>bullet list</source>
<target>bullet list</target>
</trans-unit>
```

Note the resname="bullet_list" part of this markup. That is a reference to one or more MapObjects in the common-base.std base MapTemplate file. These MapObjects are used to convert the content on the clipboard into the document format specified by the selection in the Paste Special dialog box and take precedence over the ones used for the regular copying and pasting operations in that case.

The MapObject in common-base.std that uses the bullet_list reference must use an EVAL_XPATH Input Rule which is triggered by the following XPath expression:

```
//TEXTXMLSTREAM/HEAD/XYZDOCUMENTMETATAGS/XYZMETA[@name="STDSourceFileName"]
[@value="bullet_list.aticp:source_type"]
```

This Input Rule can be expressed as “Match this MapObject if the source file name (an abstract name created from the resname attribute value) is equal to bullet_list.rtf or bullet_list.mif or bullet_list.htm ” and so forth. Any MapObjects with Input Rules that match if the user has chosen the bullet list item in the Paste Special dialog box will perform the special conversions defined by those rules.

You can use Arbortext Editor to edit the pasteAsList.xlf file to add or remove document formats and to change the strings displayed in the Paste Special dialog box. You can use Arbortext Import to modify the MapObjects referenced in common-base.std (or any other MapTemplate) from pasteAsList.xlf or to add new MapObjects for new document formats.

Note that the MapObject priority as described in Arbortext Import online help is important to Paste Special customization. MapObjects in common-base.std have higher priority values, which means they have lower priority in the top-down MapObject selection process in the final generated map. A very specific MapObject such as those used for Paste Special might never be selected if that MapObject is located below more generic MapObjects that could match the selection first. Be sure to place Paste Special MapObjects near the top of your custom MapTemplate file.

Following are some examples of Paste Special customizations:

- • Develop a Paste Special MapObject for a paragraph to convert a simple paragraph to a document type specific footnote element.

- • Develop a new Paste Special MapObject to convert numbered lists into steps and substeps elements in the DITA Task document type, instead of the default behavior of converting numbered lists in the clipboard source into numbered lists in the document type markup.

- • Develop a new Paste Special MapObject to convert Microsoft Word or Adobe FrameMaker index terms into document type specific index term markup.

## Related topics

- • Copying and pasting text from other applications

- • Using Paste Special

- • Paste Special dialog box

- • Configuring and Using Arbortext Import/Export



---

# Disabling_Copy_and_Paste

# Disabling Copy and Paste

If you do not want Arbortext Editor to convert content from other applications into markup, then you can disable this feature. In this case, copy and paste from other applications will function as that operation did before Arbortext Editor release 5.4. That is, pasted content will be a stream of text without any tagging.

Following are some reasons you might want to revert to the earlier way Arbortext Editor did copy and paste operations from other applications:

- • Many applications that want to preserve text formatting in clipboard content use RTF to store that content. This might cause unexpected results in the converted markup.

- • This feature is dependent on a certain release of the Java Virtual Machine (JVM) and third-party Java classes. Changes in the .jar files in your install tree or in a custom\classes directory might adversely affect the copy and paste feature requiring you to disable it.

- • If you have existing customizations that process HTML or RTF clipboard content or if you have a customization using the buffer_clipboard_contents function, then you might want to retain that customization instead of using the new copy and paste feature.

- • If you use a right-to-left language then you might want disable this feature, as Arbortext Import/Export does not reliably support language directionality.

Follow these steps to disable copy and paste:

Note that you can also use the set pastesource command to disable copy and paste by setting the value of the command to an empty or null string, for example: set pastesource="" .

## Related topics

- • Copying and pasting text from other applications

- • set pastesource

- • buffer_clipboard_contents



---

# Implementing_Copy_and_Paste_for_a_Custom_Document_Type

# Implementing Copy and Paste for a Custom Document Type

You can implement the copying and pasting from other applications feature for custom document types. However, to get the best results you must be sure to provide the configuration information in your document type that Arbortext Editor requires to be able to correctly convert the source clipboard data into your document type’s markup.

Some of this information is in the document type itself, such as the supported table models. Also, some information is in the associated Arbortext Styler .style file. However, most of the required information is in the associated document type configuration ( .dcf ) file. You will get the best results from this feature by ensuring that this information is configured in your .dcf file. The following table summarizes the required .dcf file settings and provides example markup from the axdocbook.dcf file.

Arbortext Editor will use the information in your document type and the associated .dcf and .style files to build the automatically generated MapTemplate files for your document type and the relevant clipboard source formats. If you make a change to the .dcf file, then the automatically generated files are regenerated in the next copy and paste operation using the document type. If a .style file is associated with the document type, the information in the .style file for graphics, links, and link targets takes precedence over related .dcf information. All other information that controls copy and paste is collected from the .dcf file.

You might also want to customize the base MapTemplate files or the Paste Special dialog box for your custom document type. However, note that a MapTemplate file specific to a source type and document type (such as rtf-task.std for a DITA Task document) can be modified in the MapTemplate Editor without regard to the .dcf file information. Remember that the automatically generated MapTemplate files will be populated by placeholder element names rather than actual element names. You can modify the default MapTemplate files as desired using Arbortext Import , or even create custom MapTemplate files for copy and paste from scratch using the MapTemplate Editor. As long as you follow the file naming convention and put the customized MapTemplate file in a custom\lib folder, that file will control the conversion process.

## Related topics

- • Copying and pasting text from other applications

- • Document type configuration files



---

# Limitations

# Limitations

The copying and pasting from other applications feature has the following limitations:

- • This feature only supports pasting into the Arbortext Editor Edit pane or Arbortext Styler Generated Text Editor.

- • This feature does not affect copying and pasting markup between two Arbortext Editor windows.

- • Because Arbortext Import/Export does not currently support text directionality, this feature does not support directionality.

- • The quality of the pasted markup depends primarily on the structure and clarity of the source documents. In the case of Microsoft Word and Adobe Framemaker documents, using paragraph styles is important to successful and efficient conversion. If all paragraphs in the source document use the same style name, even though the formatting may create the illusion of division titles, it is not possible to automatically determine the desired markup. If the source document uses unique style names to represent division titles at various nested levels, then the paste results will be more automatic. Well-styled source documents can significantly reduce the time spent for manual cleanup.

- • The quality of the pasted markup also depends on how well the document type elements have been defined in the document type configuration ( .dcf ) file, and to some extent the .style file.

- • Support for inline styles (bold, italic, and so forth) requires an element that is unique to that purpose, such as emphasis with attributes, or b (for bold). Multiple, simultaneous inline styles, such as bold-italic, assumes the nested element model like axdocbook .  By default, the feature can handle all combinations of bold, italic, and underline.  More sophisticated conversion requires a custom MapTemplate.

- • While images can be copied and pasted from Microsoft Word, those images that have been constructed from a loose collection of drawing objects cannot be pasted directly as an image because it is not a single image.

- • Adobe FrameMaker does not include image information in the clipboard data, so images cannot be copied and pasted from FrameMaker.

- • If you select and copy a table from Adobe FrameMaker 7.2 or earlier, the table structure is not copied to the clipboard. However if you copy a sibling paragraph with the table (the paragraph before or the paragraph after), the table structure is converted correctly. This is a limitation of FrameMaker versions prior to 8.0.

- • If you select and copy a table that contains another nested table and attempt to paste that table into a Arbortext XML DocBook document, a DITA document, or a document of another document type that requires that a table be enclosed in paragraph tags, the Invalid Paste Structure dialog box opens. Arbortext Editor does not enclose a nested table in paragraph tags in this case.

## Related topics

- • Copying and pasting text from other applications



---

# Modifying_the_Source_Types_Used_for_Copy_and_Paste

# Modifying the Source Types Used for Copy and Paste

In addition to disabling copy and paste, you can also control the clipboard formats Arbortext Editor uses to convert the copied content to markup. Following are some reasons you might want to control the clipboard formats:

- • Adobe FrameMaker puts both MIF and RTF content on the clipboard during a copy operation. You might want to remove the MIF format so that RTF is used for converted markup.

- • Many applications put both HTML and RTF content on the clipboard during a copy operation. You might want to disable one or the other of these formats for a particular application because you get better results from a specific format.

- • You might want to disable all of the formats except for text, but still enable users to use Edit > Paste Special and the Paste Special dialog box to provide some control over the results of a paste operation.

Follow these steps to control the source types used for copy and paste:

Note that you can also use the set pastesource command to set the clipboard formats supported for copy and paste.

## Related topics

- • Copying and pasting text from other applications

- • Using Paste Special

- • set pastesource



---

# Using_Arbortext_Import_to_Customize_the_MapTemplate_Files

# Using Arbortext Import to Customize the MapTemplate Files

You can use the Arbortext Import MapTemplate Editor included in Arbortext Architect to modify the automatically generated MapTemplate files that Arbortext Editor produces for a copy and paste operation. Following are some reasons you might want to modify the default templates:

- • Modify the division title MapObjects to match custom heading style names instead of Microsoft Words default “Heading n ” style names.

- • Modify the behavior of the default ID/IDREF handling from Microsoft Word bookmarks or Adobe FrameMaker cross-reference markers.

- • Add new MapObjects to convert inline character styles to elements

- • Add new MapObjects to convert formatted text to both elements and attributes

- • Modify the default MapObjects to handle user-defined list paragraph styles, list styles, or tables styles

- • Add map debug comments to troubleshoot copy and paste conversion issues

- • Add new MapObjects to work with custom Paste Special operations

## The automatically generated MapTemplate files

The first time that you copy and paste content from another application into Arbortext Editor , a MapTemplate file for the pasted clipboard content and the document type into which the content is pasted is automatically created. These files are stored in the Arbortext Editor cache directory ( .aptcache ). The cache directory is typically located at C:\Documents and Settings\ username \Application Data\PTC\Arbortext\Editor\.aptcache . The MapTemplate files are stored in a subdirectory of .aptcache named maptemplates .

The MapTemplate files are named source_type - doctype_name .std. For example, a MapTemplate file for the RTF source type and the axdocbook document type would be named rtf-axdocbook.std . A file for the HTML source type and the DITA topic document type would be named html-topic.std .

You can modify these automatically generated files in the MapTemplate Editor as required for your site. Put the modified files in either the Arbortext-path \custom\lib directory or in a custom\lib directory referenced through the APTCUSTOM environment variable. Your customized MapTemplate file will override the automatically generated file for the source type and document type combination implied by its file name.

The automatically generated MapTemplate files are regenerated every time you start a new Arbortext Editor session and paste for the first time with a given source type and document type combination. If you modify a document type’s .dcf file or perform a Arbortext Editor preview operation in Arbortext Styler , the MapTemplate files in .aptcache\maptemplates are marked as outdated and are regenerated as if you have started a new Arbortext Editor session. MapTemplate files in a custom\lib directory are not affected by Arbortext Editor operations and can only be disabled by renaming the file or deleting the MapTemplate from the file system.

## The base MapTemplate files

The automatically generated MapTemplate files are created from a set of base MapTemplate files. These files are stored in the Arbortext-path \lib\cpix\lib directory. The following base MapTemplate files are in this directory:

Base MapTemplate files

- • common-base.std — The common file used for all automatically generated maps.

- • htm—base.std — The file used for HTML content.

- • mif—base.std — The file used for MIF content.

- • rtf—base.std — The file used for RTF content.

- • txt—base.std — The file used for text content.

- • html-table.std — The file used for HTML tables.

- • oasis-table.std — The file used for OASIS Exchange tables.

The base MapTemplate files contain placeholder values for the document type element names. For example, the element used for paragraphs in a document type has the placeholder aticp:primary_paragraph in the Output Rules defined in the base MapTemplate file. This placeholder is replaced in the automatically generated MapTemplate file by the paragraph element defined in the .dcf file for the document type used for the generated file. Other elements are similarly added to the file based on information in the document type’s .dcf and .style files.

Following are the placeholder values for different document elements in the base MapTemplate files, including example markup from the axdocbook.dcf file that matches the placeholders for that document type.

As with the automatically generated MapTemplate files, you can modify a copy of the base files in the MapTemplate Editor as required for your site. Put the modified files in either the Arbortext-path \custom\lib directory or in a custom\lib directory referenced through the APTCUSTOM environment variable. Your customized MapTemplate file will override the base file.

Following are some examples of how you might modify the base MapTemplate files:

- • To expand the functionality of one of the base MapTemplate files, insert the appropriate placeholder name in place of actual document type dependent element names. Your base MapTemplate file will affect all document types. For example, if your Microsoft Word documents use special style names for division titles, you might add new MapObjects or modify the Input Rules of existing MapObjects. These MapObjects in a base MapTemplate file can include placeholder names for division elements and their title in the Output Steps of the MapObject’s Output Rules.

- • The base table MapTemplate files produce hard-coded element names rather than placeholder names, because these names are typical of the table models supported by Arbortext Editor . If your document type uses namespaced elements for one or more of the supported table models, you can modify the Output Rules of the base table MapTemplate and the change will affect all source types and document types at your site.

- • Because default styles are less common in Adobe FrameMaker, custom MapTemplate files can provide better support for both divisions and their titles and numbered and bulleted lists.

## Customizing the MapTemplate files

You can customize the MapTemplate files in the following ways:

- • The base MapTemplate files themselves

- • Custom overrides to the base files

- • The automatically generated MapTemplate files

- • Custom overrides to the automatically generated files

The best practice for customizing the MapTemplate files is to use the custom override files. This enables you to just change the specific parts of the base and automatically generated files that you need to modify. Note that this feature only recognizes the map objects found in a custom map template. It ignores the metadata in a map template, such as the drivers, driver options, and pre- and post-processing options. Those settings are defined in the rtf-base.std , mif-base.std , htm-base.std , and txt-base.std files.

The following sample files are available in the Arbortext-path \samples\copypaste directory:

- • common-base-custom.std — Shows how to customize the default pasting behavior by having bold text in other applications converted to a processing instruction.

- • rtf-task-custom.std — Shows how to use the Paste Special dialog box to paste numbered lists as steps and substeps in a DITA task.

- • pasteAsList.xlf — Used with the rtf-task-custom.std sample file to show the changes to the Paste Special dialog box.

- • rtf-topic-custom.std — Shows how to paste footnotes and index terms from Microsoft Word to a DITA topic.

- • rtf-axdocbook.std and pasteaslist.xlf — Shows how to paste footnotes and index terms from Microsoft Word to an XML DocBook document.

A readme.txt file in the directory describes how to implement the sample files.

## Manually generating the MapTemplate files

You can use the create_copypaste_map function to manually generate a MapTemplate file for a given source type and document type. The function returns the same MapTemplate file as the one automatically created by Arbortext Editor .

This function has the following syntax:

This function generates a basic MapTemplate file for the given clipboard source type and document type. It has the following parameters:

- • source_type — Specifies the type of clipboard data. The following values are supported:

- • path — The full path to the generated MapTemplate file.

- • doc — Optional. The identifier of the document for which the associated document type should be used for the MapTemplate file.

The function returns 0 on success or one of the following error codes on failure:

## Related topics

- • Copying and pasting text from other applications

- • Configuring and Using Arbortext Import/Export

- • Document type configuration files

- • Cache directory (.aptcache)

- • set pastesource

- • Using Paste Special