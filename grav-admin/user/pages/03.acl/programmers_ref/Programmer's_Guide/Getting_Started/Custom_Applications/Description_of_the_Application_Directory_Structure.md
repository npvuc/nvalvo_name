

---

# Application_Startup_File

The Arbortext-path \doctypes\appcfg\application.xml file provides a basic template for defining information about the custom application. You can make a copy of doctypes\appcfg\application.xml to use as a template to create the file that will eventually be distributed with the application. The application.xml file must be placed in the application's top level directory, for example:

```
Arbortext-path
\application\com.
company
.
application-package-name
\application.xml
```

In the template application.xml file, you can specify a list of elements that describe the application. If the custom application determines its criteria is not met and the application is not to be loaded, then these values are ignored. The base element for the file is the ApplicationConfiguration element. This element has a required attribute called installType that determines the type of Arbortext Editor installation for which this application is supported. The default value is any meaning the application is supported in both the full and compact installations of Arbortext Editor . The other supported value is full meaning the application is only supported in the full installation of Arbortext Editor .

The following other elements are supported in the application.xml file:

- • Name (required)

- • Description

- • LicenseNumber is only for an application distributed by Arbortext

- • Version (required)

- • Date

- • Copyright

- • Vendor

- • RequiredApplications is for other applications that are required for this application to run correctly. You must enter the qualified name for the application in the qualifiedName attribute and a human-readable name in the name attribute.

- • SupportedProducts

- • SupportedPlatforms

- • GlobalParameters



---

# Related_Topics

For information on creating and implementing custom applications, consult the Programmer's Reference and the Customizer's Guide .

If you are using ACL, refer to the following ACL function descriptions:

- • application_name function

- • get_custom_dir function

- • get_custom_property function

- • get_user_property function

- • set_user_property function

If you are using the AOM, refer to the documentation for Application.getCustomDirectory . Refer to the XUI section of the Customizer's Guide for information on extending the Arbortext Editor Preferences dialog box for your custom application.

The following attributes from the Application interface are also useful:

- • haveWindows

- • initDone

- • isE3

- • customProperties

- • userProperties

- • name



---

# Subdirectory_Structure

A subdirectory of the application directory can be structured the same as the custom directory to take advantage of automatic Arbortext Editor and Arbortext Publishing Engine startup processes. For example, if the uniquely named directory contains graphics or entities directories, those directories are automatically added to the search paths constructed at startup.

An application path could be something like:

```
application\
com.company-name.application-name
```

Refer to the Description of the custom directory structure for the names and descriptions of each supported subdirectory.

When implementing a custom application using the application directory structure, you can add supplemental directories as needed to support your application. However, your application code must be aware of these directories and how to use them.