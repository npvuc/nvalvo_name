

---

# acl_attribute

The Acl global object.



---

# activeDocument_attribute

A DOM Document that represents the Arbortext Editor or Arbortext Publishing Engine active or current document . If the user interface is active, this is the document that has the focus.



---

# activeSession_attribute

Represents the active CMSSession (if any).



---

# activeWindow_attribute

A Window object that represents the Arbortext Editor active window. If the user interface is not active, returns null .



---

# adapterQNames_attribute

A list of adapter qualified names for all registered adapters that are available to the application. These values are suitable for use with the Application.getAdapter() method.



---

# alert_method

Displays an alert dialog box with the specified message.



---

# confirm_method

Displays a modal confirmation dialog box with the specified message.



---

# constructObject_method

Create a new CMSObject for the object referenced by logicalId.



---

# createComposer_method

Creates a Composer object for the given ccfPath .



---

# createDialogFromDocument_method

Creates a dynamic dialog box according to the content of a document.



---

# createDialogFromFile_method

Creates a dynamic dialog box according to the content of an XML file.



---

# createEvent_method

Creates an event of type ApplicationEvent .



---

# createPropertyMap_method

Creates an empty PropertyMap object that is an unordered collection of name-value pairs.



---

# createScriptContext_method

Creates a ScriptContext object that may be used to load, compile, and execute scripts using the Microsoft Windows Script engine. This method is only available in the COM binding of the Application interface.



---

# createStringList_method

Creates an empty StringList object that is an ordered collection of DOMString s.



---

# createTableObjectStore_method

Creates an empty TableObjectStore object that is a collection of TableObject s.



---

# createTableTilePlex_method

Creates an empty TableTilePlex object which can represent a table selection in a document.



---

# createWindow_method

Creates a window of the specified windowClass with optional components given by flags . The window created is not initially displayed. Use the Window.show() method to make the window appear.



---

# customProperties_attribute

Returns a PropertyMap object containing custom properties for an application. This object is initialized from the application-specific global parameters specified in an application's application.xml file.



---

# documents_attribute

A DOM NodeList which contains all documents currently opened by Arbortext Editor or Arbortext Publishing Engine . The NodeList will be updated as documents are opened and closed.



---

# domImplementation_attribute

The DOMImplementation object. This is the same value that is returned by a DOM Document object's implementation attribute.



---

# error_method

Sounds a beep and displays the error message specified by message in the status bar of the active window if possible, otherwise in a separate dialog. The message is also assigned to the ERROR predefined ACL variable

The error method is used by Arbortext Editor to display most error messages.



---

# event_attribute

An Event object which stores the context of the current event. This attribute can only be obtained from within an event listener.



---

# getAdapter_method

Returns the requested adapter if available.



---

# getCustomDirectory_method

Returns the installation directory for a specified application. If name is omitted or the null string, then the default custom directory is returned, either the first value of the APTCUSTOM environment variable if set or else the custom subdirectory in the product installation directory.

If name is a number, then this specifies the 0-based index into the list of custom directories. This allows an iterator to enumerate the list of custom directories by calling this method in a loop, incrementing the index until a null string is returned.

If name is a negative integer, then the list is traversed in reverse. "-1" returns the last custom directory, "-2" the second to last custom directory and so on.



---

# getLocale_method

Returns the requested locale string.



---

# getLocalizedMessage_method

Returns the localized version of the specified message from the default message catalog file.



---

# getOption_method

Returns the value of the Arbortext set option, in global scope.



---

# getOptionScope_method

Returns the scope of the Arbortext set option.



---

# getScriptContext_method

Returns an IDispatch pointer to a ScriptContext object for the running script specified by the name parameter. This method is only available in the COM binding of the Application interface.



---

# haveWindows_attribute

Returns true if the application is running in windows-mode. Returns false if running as an Arbortext Publishing Engine server or in one-shot command mode ( -c specified as a startup option).



---

# initDone_attribute

Returns true if the product has completed initialization.



---

# isE3_attribute

Returns true if the product is running Arbortext Publishing Engine , either server or interactive mode. Server mode can be determined by also testing the haveWindows attribute.



---

# lastErrorDetail_attribute

Represents the detail field of the last exception thrown by the AOM. If the exception had no detail field then this will be an empty string. The current value is available only until the next AOM exception is thrown.

This is only available in the COM binding of the Application interface because other bindings have direct access to the exception's detail field.



---

# LoadFlags_enumeration

The LoadFlags enumerated type is used to construct the flags parameter to the openDocument method by ORing any of the following options:

The LoadFlags enumeration has the following constants of type int .



---

# logicalIdExists_method

Tests the existence of Logical IDs associated with any active CMS session as well as for file-system and http/https resources.



---

# logicalIdToSession_method

If the specified path is the correct Logical ID format for a connected CMS, this returns the CMSSession object associated with that session.



---

# messageBox_method

Displays a message box with the text message and optional title title . The flags parameter determines what predefined buttons and icons display in the message box, and is formed by ORing the flags from the following groups of flag bits.

Specify one of the following flags to indicate the buttons that will display in the message box:

- • 0x00 — Display OK button only. This is the default.

- • 0x01 — Display OK and Cancel buttons.

- • 0x02 — Display Abort, Retry, and Ignore buttons.

- • 0x03 — Display Yes, No, and Cancel buttons.

- • 0x04 — Display Yes and No buttons.

- • 0x05 — Display Retry and Cancel buttons.

Specify one of the following flags to indicate the icon to display in the message box. If you do not specify one of these flags, an icon does not display.

- • 0x10 — Display the Error (Stop) icon. This icon is typically used with the Abort, Retry, and Ignore buttons

- • 0x20 — Display the Question icon. This icon is typically used with the Yes and No buttons.

- • 0x30 — Display the Warning icon.

- • 0x40 — Display the Information icon.

Specify one of the following flags to indicate the default button:

- • 0x000 — The first button is the default. This is the default if no other default button flag is specified.

- • 0x100 — The second button is the default.

- • 0x200 — The third button is the default.

If the dialog box has a Cancel or Ignore button, the function returns 3 if the Cancel or Ignore button or ESC key was pressed, or if the dialog box was closed from the Close system menu or Close button. If the dialog box does not have a Cancel or Ignore button and is closed with the ESC key or by the Close system menu or Close button, the function returns 2 if the dialog has only Yes and No buttons. If the dialog box only has an OK button, it returns a 1 .



---

# MessageBoxFlags_enumeration

The MessageBoxFlags enumerated type is used to construct the flags parameter to the messageBox method by ORing any of the following options:

The MessageBoxFlags enumeration has the following constants of type int .



---

# name_attribute

Specifies the name of the Arbortext product, for example, "Arbortext Editor" . This string is not localized. The localized version of the string can be obtained by calling getLocalizedMessage on the result.



---

# openDocument_method

Reads an XML or SGML file and creates a new Document object that may be used to navigate the document's content. The method may also be used to create an empty document if path is null , similar to the createDocument method of the DOMImplementation interface.

The pubid and sysid arguments specify the document type for the document if path is omitted or null , if the associated file does not specify a DOCTYPE declaration, or if bit OPEN_FORCEDT is included in flags . The pubid and sysid arguments are ignored if path specifies an SGML file that starts with a DOCTYPE declaration, if OPEN_FORCEDT is not specified, or if path specifies a binary document file. If the document type is not specified, is "ascii" , or cannot be determined the document is opened in untagged mode.



---

# optionNames_attribute

A StringList containing the names of all Arbortext set options, excluding ACL hook names.



---

# OptionScope_enumeration

The OptionScope enumerated type is the return type of the getOptionScope method, and has the following values:

The OptionScope enumeration has the following constants of type unsigned short .



---

# path_attribute

specifies the location of the directory that contains the program files needed to run the software.



---

# print_method

Outputs a string to the message window. If the user interface is not open on Windows, the message is discarded. In Arbortext Publishing Engine on Windows, the message is sent to the trace window if it is open, otherwise it is discarded.



---

# prompt_method

Displays a modal dialog box with the specified message prompt , a text input field, and OK and Cancel buttons.



---

# quit_method

Terminates the application with the exit status status . The parameter code determines if the user is prompted for unsaved changes or not and has one of the values:

- • 0 — prompt about any unsaved changes.

- • 1 — save all modified documents without prompting.

- • 2 — do not prompt about unsaved changes and quit without saving modified documents.



---

# registerIOAdapter_method

Called during startup by the adapter to register itself with Arbortext Editor . This call should be the last thing done in the initialization/loading code for the adapter. An adapter cannot be unregistered once it has been registered.



---

# run_method

Runs the macro or alias named name . The name is first looked up as a macro using the active document macro scope. If no such macro is found in any scope, then name is looked up as a command alias.



---

# setOption_method

Sets the value of the Arbortext set option, in global scope. If name specifies a Document - or View -scoped option, setting the value does not affect any existing documents or views, only newly created objects.



---

# userProperties_attribute

Returns a PropertyMap object containing user properties (preferences) that override custom properties set for an application. This object is initialized from the user property section of the epic.wcf preferences file. Changes made to the userProperties object are saved back to the preferences file on exit.