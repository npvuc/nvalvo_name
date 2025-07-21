

---

# Adjusting_Java_Memory_Availability

You may be able to improve the performance of Arbortext Import/Export by adjusting the amount of memory that is allocated to Java (which underlies much of Arbortext Import/Export ).

The amount of memory allocated to Java when using Arbortext Import/Export is specified in the file stdexecutorconfig.xml . This file is typically stored in the Arbortext-path \lib\cpix\bin\platform directory. (You can specify an alternate directory for this file using the value of the APTIMPORTCPIX environment variable.)

Use the following steps to adjust the amount of memory allocated to Java.



---

# Importing_Very_Large_Documents

When attempting to import very large documents (such as 50MB+ MIF files that publish as several-hundred-page documents), Arbortext Publishing Engine may report exception errors and fail to import the documents. In these situations, consider trying the following workarounds to successfully import the documents.

- • Break the large document into several smaller documents and import the smaller documents.

- • Raise the maximum size of the Java Virtual Machine (JVM) memory allocation pool by giving a higher value to one of these settings:

Be aware that setting this value to too high of a value will result in a failure to start the Java Virtual Machine. If changing this value results in the document being successfully imported, be sure to reset the javavmmemory value. Having this value unnecessarily high may result in other publishing and importing issues.



---

# Improving_Import_Performance_and_Freeing_Disk_Space

During each import, temporary directories and files are created and stored in the following directory in the Project Directory:

```
\Sample\ExecutionResults
```

Manually delete the contents of this directory over time to increase performance and free disk space. Do not delete the directory if it's still used with an active project.



---

# Known_Export_Limitations

Refer to the Export section of the Arbortext Styler documentation for a listing of Export limitations.



---

# Known_Import_Limitations

Be aware of the following limitations when using Arbortext Import/Export to import documents:

- • Import to SGML is not directly supported by Arbortext Import/Export . To import SGML files, create an XML version of the target document type and use an ACL postimport hook to save as SGML

- • Arbortext Import/Export cannot import graphics as entity references.

- • Processing instructions cannot be directly imported.

- • MIF embedded graphics created using the FrameMaker drawing tools are not imported.

- • In rare circumstances, certain embedded images in MIF files cannot be converted from their original format, instead appearing in the imported file as embedded Microsoft Word documents. The embedded images are identified in the FrameMaker MIF files as "OLE2" images, which is the same OLE compound document format as Microsoft Word files. A possible source for this scenario may occur when the images were originally created in Microsoft Word and then pasted into the FrameMaker document. These embedded images must be recreated in a different format before conversion or be manually recreated after the conversion.

- • Imported documents are not guaranteed to be contextually valid documents.

- • Arbortext Import has no concept of an XML template, which uses Arbortext Editor 's caret location as the starting point. This means any boilerplate data must be encapsulated in one or more MapObjects.

- • Viewing the HTML versions of the source document ( .doc , .rtf , and .mif ) requires Internet Explorer 6.0. Without Internet Explorer 6.0, Arbortext Import and the Arbortext Import Workbench will still operate properly, but the HTML rendering of the source document will not function.

- • Arbortext Import imports RTF versions 1.7 and 1.8 (although specific features of any version may not be mappable or importable). The hundreds of third-party applications that produce RTF may create RTF files with unexpected content. Arbortext Import may not be able to import all of these variations of RTF.

- • Microsoft Word text boxes are not fully supported and may import in unexpected manners due to the nature of their anchor point/XY location relations.

- • Arbortext Import can only process system files. Ensure that permissions are set properly if a database repository is involved in your import process.

- • Arbortext Import does not support importing Hebrew, Arabic, and Thai content.