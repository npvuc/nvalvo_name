

---

# custom.xml_File

At the top level of the custom directory is the custom.xml file. Following is the default version of this file:

```
<?xml version="1.0" encoding="UTF-8"?>
<!--Arbortext, Inc., 1988-2009, v.4002-->
<ApplicationConfiguration
xmlns="http://www.arbortext.com/namespace/doctypes/appcfg">
<Information>
<!--The following name will be shown in the New dialog
as the category for all document types in this
custom directory that do not specify a category.-->
<Name>Custom Directory Name</Name>
</Information>
</ApplicationConfiguration>
```

This file is only used when you have a custom document type in the custom\doctypes subdirectory, and you have not designated a category name for the document type in the associated document type configuration ( .dcf ) file’s NewDialog element. In this case, the name in the custom.xml file’s Name element is used as the Category name for the document type(s) in the custom\doctypes subdirectory in the New Document dialog box.



---

# Error_Reporting_for_the_custom\init_Directory

Errors caused by mistakes in custom code in the Arbortext-path \custom\init directory are reported with both the error message and the name of the initialization file causing the error. Note the following:

- • If Arbortext Editor is not running interactively (batch mode), no errors are reported and the errors are not logged.

- • Arbortext Publishing Engine records errors and reports them to its HTTP clients in an HTML error page.

- • ACL, JavaScript, and Java class errors are reported to the Arbortext Editor interface or held by Arbortext Publishing Engine to be sent to HTTP clients making requests.



---

# Related_Topics

- • Using the custom directory for custom applications

- • Description of the application directory structure

- • Startup command files

- • The following set command options and environment variables affect custom path search lists:

For information on creating and implementing custom applications, see the Programmer's Reference and the Customizer's Guide .

If you are using the AOM, refer to the documentation in the Programmer's Reference for Application.getCustomDirectory . Refer to the XUI section of the Customizer's Guide for information on extending the Arbortext Editor Preferences dialog box for your custom application.



---

# Subdirectory_Structure

The following list describes each custom subdirectory and how it's used. Arbortext Editor and Arbortext Publishing Engine look in these directories for any references that use a relative path or have no specified path.

- • classes subdirectory

- • composer subdirectory

- • datamerge subdirectory

- • dialogs subdirectory

- • ditarefs subdirectory

- • dictionaries subdirectory

- • doctypes subdirectory

- • entities subdirectory

- • fonts subdirectory

- • formats subdirectory

- • framesets subdirectory

- • graphics subdirectory

- • importexport subdirectory

- • inputs subdirectory

- • lib subdirectory

- • publishingrules subdirectory

- • pubview subdirectory

- • scripts subdirectory

- • stylermodules subdirectory

- • tagtemplates subdirectory

- • init subdirectory

- • editinit subdirectory