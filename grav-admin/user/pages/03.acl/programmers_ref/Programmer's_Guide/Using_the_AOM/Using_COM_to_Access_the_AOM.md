

---

# Accessing_COM_Using_JScript_or_VBScript

You can access the AOM in JScript and VBScript using the COM interface. The Arbortext Editor Application and Acl objects are exposed to the script automatically as global objects when using the built-in script interpreters.

You can access external third-party COM objects using the JScript ActiveXObject object or the VBScript CreateObject and GetObject functions. Microsoft Excel is an example of a COM server which can be accessed from Arbortext Editor . For example, to launch Microsoft Excel using JScript, use the following statement:

```
var xl = new ActiveXObject("Excel.Application");
```

To launch it using VBScript, use:

```
Dim xl
set xl = CreateObject("Excel.Application")
```

Both examples provide access to Excel's Application object, which is different from the Arbortext Editor Application object. (If you were running a script outside the built-in interpreter, for example, using Excel VBA, you would need to create an instance of the Arbortext Editor Application object using Epic.Application .)

Extensive documentation on JScript and VBScript is available from the Microsoft Developers Network (MSDN) web site at msdn.microsoft.com . Search for the topic “Windows Script”. Documentation on how to use a COM server, such as Excel, is provided by the software vendor. In the case of Microsoft Office products, the VBA (Visual Basic for Applications) documentation is the primary source of information on the COM objects exposed in each Microsoft Office application.



---

# COM_Error_Handling

All of the Arbortext Editor COM interfaces support the ErrorInfo COM interface and use it to pass error messages to the client if the called method fails. All supplied methods return an HRESULT which indicates success or failure and the general nature of the failure. Developers can use standard COM practices to retrieve error codes and error messages.

The DOM specification indicates that several methods will raise an exception upon certain types of failure. This is also the case for several AOM methods. Since the COM interface doesn't support exceptions, these failures will be turned into HRESULT return values. The specific value returned for a given exception can be found in the type library for the Arbortext-path \bin\editor.exe binary. They're also presented in the tables that follow. The general rule is that these exceptions will be returned as DOM_E_ YYY _ERR for the DOMException , EventException and RangeException errors, TABLE_E_ YYY _ERR for TableException errors, WINDOW_E_ YYY _ERR for WindowException errors, and EXECUTE_E_ YYY for AclException errors.

The following tables list the COM error codes and values for each range of errors. See the exception interface definitions in Interface Overview for the exception codes and their meanings.

JScript maps the COM errors to the Error object, and VBScript maps the COM errors to the Err object. See JScript Exception Handling and VBScript Error Handling for details.



---

# COM_Objects_and_ACL

You can use ACL ( Arbortext Command Language ) to call most COM (Component Object Model) objects which export the IDispatch interface and which include a type library.

You can use this functionality, for example, to invoke an application or DLL written in Visual Basic. Such an external application can, in turn, invoke Arbortext Editor or an Arbortext PE sub-process using its COM interface to access or change a document. Keep in mind that calling COM objects from VBScript or JScript scripts is more straightforward than calling COM objects from ACL (refer to Accessing COM Using JScript or VBScript ).

ACL includes a set of functions to support COM calls: com_attach , com_call , com_prop_get , com_prop_put , and com_release .

Use the com_attach function to attach to a COM object and return a handle that can be used to invoke the object. After a successful com_attach , you can use the object handle to make calls to com_call , com_prop_get , or com_prop_set to invoke a method or get or set a property in a COM interface. Use the com_release function to release an object attached by com_attach or one returned by another interface. These functions are documented in the Arbortext Command Language Reference .

Arbortext Editor and the Arbortext PE sub-process use the type library associated with a COM interface to determine the type of each argument and the return value of a method or property invoked using an ACL function. This makes it possible, for example, to pass ACL variables to COM methods that expect parameters passed by reference and have the COM object return results to ACL by changing the value of the variable.

Arbortext Editor and Arbortext Publishing Engine have some restrictions and limitations in their support for calling COM interfaces, many of which are inherent to ACL:

- • Named arguments are not supported.

- • Arguments can be omitted only at the end of the argument list

- • You cannot pass an ACL array to a COM interface as an array. You can pass a member of an ACL array as an individual argument.

- • A called COM interface function can't return an array and have it converted into an ACL array.

- • You cannot use the other information in a type library (such as enum definitions) in ACL.

- • There is no implicit support for the implied Value , _NewEnum , or Evalute methods and properties even though it may be possible to call them explicitly.



---

# Registering_and_Unregistering_Arbortext_Editor_as_a_COM_Server

When you install Arbortext Editor , the setup program automatically registers PTC Arbortext Editor as a COM server. The uninstall program will unregister Arbortext Editor as a COM server.

Starting with release 5.4, Arbortext Editor also automatically checks at startup to see whether the application is registered as a COM server. If Arbortext Editor finds that it is not registered as a COM server, it performs a COM registration for Arbortext Editor itself and all of its installed components as part of the startup process. This check can be disabled with the APTNOCOMCHECK environment variable. If the automatic registration fails for some reason (usually because the user does not have administrator privileges), Arbortext Editor still opens but displays an error message first saying that this version is no longer configured correctly. In this case, some Arbortext Editor components might not be available. You can keep Arbortext Editor from opening in this case with the APTFAILIFNOCOM environment variable.

If you run a version of Arbortext Editor earlier than 5.4 on the same system with your current version, you might encounter problems with the earlier version’s COM registration due to the new automatic COM registration. You can obtain a utility called register.bat from PTC Technical Support that will correctly register releases of Arbortext Editor prior to 5.4. For more information, search the Technical Support knowledge base for TPI 144503.

You can manually register or unregister a PTC Arbortext Editor installation at any time by running Arbortext Editor with the -RegServer , -UnregServer , or -UnregAnyServer startup command options. In the examples that follow, the first path to the editor.exe binary is for 64-bit installations, and the second path is for 32-bit installations.

```
Arbortext-path
\bin\x86\editor.exe -RegServer
Arbortext-path
\bin\x86\editor.exe -RegServer
```

```
Arbortext-path
\bin\x64\editor.exe -RegServer
Arbortext-path
\bin\x86\editor.exe -RegServer
```

Registers a specific Arbortext Editor installation as a COM server.

```
Arbortext-path
\bin\x86\editor.exe -UnregServer
Arbortext-path
\bin\x86\editor.exe -UnregServer
```

```
Arbortext-path
\bin\x64\editor.exe -UnregServer
Arbortext-path
\bin\x86\editor.exe -UnregServer
```

Unregisters a specific Arbortext Editor installation as a COM server. Note that the -UnregServer option will not remove the editor.exe COM server entry in the registry, unless the Arbortext Editor installation you are running matches the Arbortext Editor installation listed as the current editor.exe COM server.

```
Arbortext-path
\bin\x86\editor.exe -UnregAnyServer
Arbortext-path
\bin\x86\editor.exe -UnregAnyServer
```

```
Arbortext-path
\bin\x64\editor.exe -UnregAnyServer
Arbortext-path
\bin\x86\editor.exe -UnregAnyServer
```

Unregisters any version of Arbortext Editor on the system as a COM server, not just the installation for which you are using the option.

## Related topics

- • Using the Acl interface

- • Startup command syntax

- • APTNOCOMCHECK — Do not perform a COM check and automatic registration on startup

- • APTFAILIFNOCOM — Silently fail when COM check and automatic registration fails on startup



---

# Sample_COM_Code

Sample Visual Basic and Visual C++ code that uses the COM interface is included in the Arbortext-path \samples\com directory. The Readme file in this directory provides details on the samples.