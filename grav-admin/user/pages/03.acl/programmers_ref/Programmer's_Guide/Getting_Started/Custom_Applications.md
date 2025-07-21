

---

# Deploying_Zipped_Customizations

You can deploy not only custom directories, but also application and content management system adapters directories in a compressed zip file. Using a zip file to distribute your customizations has the following advantages:

- • You can host your customizations on a web server.

- • Your customizations will be available to users when they cannot access your network.

- • Network traffic might be reduced.

- • Customizations stored in a compressed zip file are harder to change accidentally than customizations stored in a directory structure.

Note that you cannot use a zip file to distribute a customized installprefs.acl in the custom\lib directory. You can use the APTINSTALLPREFS environment variable to specify the location of a custom installprefs.acl file.

Note also that you cannot include the following font configuration files in the lib subdirectory of a zipped custom directory:

- • charent.cf

- • wcharent.cf

- • wfontsub.cf

- • charmap.cf

These files are processed before a zipped custom directory when Arbortext Editor starts up, so the files cannot be processed when deployed in that way.

## Related Topics

- • Description of the custom directory structure

- • Description of the application directory structure

- • APTCUSTOM — Specifying alternate path to the custom directory

- • Cache directory (.aptcache)

- • APTINSTALLPREFS — Specifying the path name of an alternate installprefs.acl file



---

# Description_of_the_Application_Directory_Structure

The Arbortext-path \application subdirectory supports installing an application into the Arbortext Editor and Arbortext Publishing Engine install trees. Arbortext Editor and the Arbortext Publishing Engine automatically search for subdirectories of the application directory at startup.

Arbortext-path \application must contain a uniquely named subdirectory for each distributed application. Arbortext recommends using the naming pattern for a unique qualified Java class name:

```
com.company-name.application-name
```

Each unique subdirectory of the application directory must also contain an application.xml configuration file which describes various aspects of the application, such as its release version and supported versions of Arbortext products. At startup, Arbortext Editor and the Arbortext Publishing Engine search the application directory for any subdirectories containing an application.xml configuration file. The application.xml file contents provide the criteria to determine whether the application should be loaded. The application directory must be located using a file system; HTTP references are not supported.



---

# Description_of_the_Custom_Directory_Structure

When Arbortext Editor or an Arbortext PE sub-process starts, it can access custom files placed in specific directories. At startup, it automatically looks for compiled Java files ( .class and .jar files), JavaScript, JScript, VBScript, ACL, document type, publishing configuration and other types of files within the Arbortext-path \custom directory structure.

You can have one or more custom directories outside the Arbortext-path install tree. To specify a path list for their locations, set the APTCUSTOM environment variable . The custom directory must be located using a file system; HTTP references are not supported.

At startup, some search paths are automatically prepended with the path to a custom subdirectory. Startup automatically sets some of these search paths using a symbolic variable as a path specification. You can use symbolic parameters to represent a search path in the context of the default search path, the location of the install tree, or the locale.

If a directory supports more than one type of file, the file types are processed in the following order:

- • .acl ( Arbortext Command Language ) files

- • .js (JavaScript or JScript) files

- • .class (Java) files

- • .vbs (VBScript) files

For each file type, its files are processed in alphabetical order by file name.

The Arbortext-path \custom directory is processed at startup. If you add custom applications and document types after startup, they're not recognized during the session. If you're using Arbortext Editor , it needs to be closed and restarted. If you're using Arbortext Publishing Engine , you need to stop and restart the Arbortext Publishing Engine to re-initialize the Arbortext PE sub-processes .



---

# Specifying_the_JavaScript_Interpreter_Engine

Both JavaScript and JScript files have a .js file extension. By default, Arbortext Editor and the Arbortext Publishing Engine interpret .js files as Rhino JavaScript files. You should specify the JavaScript interpreter for a JavaScript or JScript .js file. This is especially important if you have .js files of both types.

We recommend adding a comment line to your script that specifies either the Rhino JavaScript engine (the default) or the Microsoft JScript engine as shown in the following examples. The first line of your .js file must be a comment starting with // .

To specify the Rhino JavaScript interpreter:

```
// type="text/javascript"
```

To specify the Microsoft JScript interpreter:

```
// type="application/jscript"
```

The specification can be enclosed in a script tag. Both of the following examples are a valid specification for JScript:

```
// <script type="application/jscript">
// type="application/jscript"
```

You can also specify the JavaScript interpreter using the ACL set javascriptinterpreter command. You can specify it in an ACL file placed in the Arbortext-path \custom\init directory, where it will be processed at startup. For information on setting the interpreter using ACL, see the online help topic for set javascriptinterpreter .



---

# Using_the_Application_Directory_for_Custom_Applications

The Arbortext-path \application subdirectory provides the means to implement a custom application that uses a special configuration file to determine whether it should be loaded at startup. The application directory uses the same principles of structure as the custom directory.

The Arbortext-path \application directory is processed at startup. If you add a custom application after startup, you must exit and restart Arbortext Editor or stop and restart the Arbortext Publishing Engine to have it recognized. You also have the option to issue the f=init function to re-initialize the Arbortext PE sub-processes . Refer to Configuration Guide for Arbortext Publishing Engine for more information.

Rules for using the application directory are:

- • Your custom application must be contained in a uniquely named subdirectory of the application directory.

- • You must have an application.xml configuration file in the uniquely named subdirectory that sets the conditions for loading the application.

- • The same set of subdirectories supported by the custom directory are supported for the uniquely named subdirectory of the application directory. At startup, the supported directories are automatically detected and used in constructing search paths.

- • Any other subdirectory of the application directory will be ignored at startup. For example, an application\graphics subdirectory with no application.xml file will be ignored during startup.

Arbortext has developed proprietary custom applications that are deployed using the application subdirectory structure. A uniquely named subdirectory contains all the necessary components to run an application within Arbortext Editor as well as the Arbortext Publishing Engine .

The following information will help determine an approach for a custom application.

- • You can have additional subdirectories for your custom application. You are not limited to the subdirectories supported by the custom directory. However, these additional directories are not automatically recognized during the startup process.

- • Processing each unique application's subdirectories follows the same rules for processing custom subdirectories. Recall that the application's subdirectories come after the custom subdirectories in constructing any applicable search paths for the session.

- • If you decide not to use a particular supported subdirectory, you can improve performance by omitting the directory to reduce the length of a search path that would contain it.

- • You can use the APTAPPLICATION environment variable to set the path to one or more application directories.

- • An application should not write data to its own application directory. An application user may not have write permission access to this application directory, for example, any C:\Program Files directories on Windows (the location where Arbortext Editor and the Arbortext Publishing Engine are typically installed).

## Related topics

- • Description of the custom directory structure

- • Description of the application directory structure



---

# Using_the_Custom_Directory_for_Custom_Applications

The Arbortext-path \custom subdirectory structure provides the means to implement custom applications. Where your application should be placed depends on the application purpose and programming language.

If you're implementing custom applications or scripts, the following information will assist you in determining the approach and location for your files:

- • A custom Java program can be placed in custom\init , which supports a .class file that must implement a public static void main (String[] args) method. The method will be called at startup with no arguments (an empty String array). If an error occurs, it's reported interactively for Arbortext Editor or sent to the HTTP client for the Arbortext Publishing Engine .

- • A custom JavaScript, JScript, VBScript, or ACL application can be placed in custom\init or in custom\scripts . If you place your scripts in the custom\scripts directory, you can call them from a script or scripts you place in custom\init (which is processed at startup). Any code that exists outside a function definition in a script from custom\init is executed at startup time. Errors are reported if running interactively, otherwise they're suppressed.

You can create a simple JavaScript example file called simple_init.js . The script should contain the following line:

```
Application.alert("Hello from JavaScript");
```

Put the simple_init.js file in Arbortext-path \custom\init .

When the startup process loads scripts from custom\init , you will see a dialog box showing the Hello from JavaScript message.

## Related Topics

- • Description of the custom directory structure

- • Description of the application directory structure