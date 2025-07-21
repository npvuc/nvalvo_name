

---

# AOM_Interfaces_Specific_to_VBScript

By default, VBScript instances run in a single global context, or namespace, called EpicVBS . The AOM includes VBScript-specific features related to the ScriptContext object:

- • createScriptContext — allows scripts to create and run nested scripts in the global namespace ( EpicVBS ), or in a user-defined context or namespace.

- • getScriptContext — retrieves a reference to any running script context by namespace.

See the descriptions in Application interface and ScriptContext interface for more information.



---

# Sample_VBScript_Code

Sample VBScript code that uses the VBScript AOM interface is included in the Arbortext-path \samples\vbscript directory. The readme.txt file in this directory provides a description of the sample code and instructions for invoking the sample scripts. Examples show how to use the DOM to manipulate the active document and register DOM event handlers. There are two samples, commdlg.vbs and graphic-browser.vbs , which show how to use COM to launch and communicate with Microsoft Word and Microsoft Excel. The VBScript examples are ported from the corresponding JScript samples of the same name.



---

# VBScript_and_ACL

VBScript expressions or scripts can be called from ACL with one of the following ACL primitives:

- • vbscript — Function that evaluates a VBScript expression and returns the result as a string.

- • source — Command that interprets files ending in .vbs as JScript programs to be executed.



---

# VBScript_Error_Handling

VBScript does not support exceptions, so the DOM and AOM exception classes are not available. All exceptions are mapped to the VBScript Err global object. The COM error code values listed in COM Error Handling are available using the Number property of the Err object. The message associated with the exception is available using the Description property. For example:

```
On Error Resume Next
doc.insertBefore doc, doc ' this is invalid
If Err.Number <> 0 Then
Application.alert("Error: " & Err.Number _
& " Description: " & Err.Description)
Err.Clear
End if
```



---

# VBScript_Global_Objects

The Arbortext VBScript implementation provides several global objects available to all VBScript scripts. The Application and Acl objects are instances of the AOM Application and Acl interfaces. Only one object for each interface exists in a Arbortext Editor session.



---

# VBScript_Limitations

Some limitations of the Arbortext VBScript implementation are:

- • VBScript is not case-sensitive.

- • The AOM and DOM constants are not defined in the global context. They must be defined inline in VBScript files to be referenced by variable name.