

---

# Creating_Tag_Help_for_a_New_Document_Type

Use the following steps for creating tag help for a new document type.



---

# Location_of_Tag_Help_Files

Tag help files are stored in a \help subdirectory of a document type's directory in Arbortext-path \doctypes . Arbortext-path is the directory where Arbortext Editor is installed. The doctypes directory in Arbortext-path in turn contains directories for the individual distributed document types. Each of those directories has a \help subdirectory.

As an illustration, if Arbortext Editor resides in the directory c:\Program Files\ PTC Arbortext \Editor , tag help for a document type would reside in c:\Program Files\ PTC Arbortext \Editor\doctypes\ dtddir \help , where dtddir is the name of the directory containing a particular document type.

More specifically, if your document type is a customized document type installed in the directory c:\apps\doctypes\mydoc , the document type’s tag help files will be stored in c:\apps\doctypes\mydoc\help .



---

# Tag_Help_File_Types

To create and modify help for element tags using Arbortext Editor , create and save the text for each tag in a separate file, typically using the same document type as that which the help supports. If the document type does not easily support text elements, PTC recommends using a document type such as XHTML.

For example, create help files supporting the memo SGML document type using the memo SGML document type. Create help files supporting the ATI XML DocBook document type using the ATI XML DocBook document type.