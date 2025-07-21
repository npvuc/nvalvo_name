

---

# AOM_Interfaces_Specific_to_JScript

By default, JScript instances run in a single global context, or namespace, called EpicJS . The AOM includes JScript-specific features related to the ScriptContext interface:

- • createScriptContext —allows scripts to create and run nested scripts in the global namespace ( EpicJS ) or in a user-defined context or namespace.

- • getScriptContext —retrieves a reference to any running script context by namespace.

See the descriptions in Application interface and ScriptContext interface for more information.



---

# JScript_Exception_Handling

JScript provides exception handling with try/catch statements. JScript is implemented using the COM interface, so it does not support the DOM and AOM exception classes. All exceptions are mapped to the JScript Error global object. The COM error code values listed in COM Error Handling are available using the number property of the Error object. The message associated with the exception is available using the description property. For example:

```
try {
doc.insertBefore(doc, doc); // this is invalid
}
catch(e) {
Application.alert("Error: " + (e.number&0xffff) +
" Description: " + e.description);
}
```



---

# JScript_Global_Objects

The Arbortext JScript implementation provides several global objects available to all JScript scripts. The Application and Acl objects are instances of the AOM Application and Acl interfaces. Only one object for each interface exists in a Arbortext Editor session.



---

# JScript_Limitations

Some limitations of the Arbortext JScript implementation are:

- • JScript is not case-sensitive. Rhino JavaScript is case-sensitive. AOM and DOM compatiblity between JScript and JavaScript files requires the script author to comply with the capitalization of methods and attributes described in this guide.

- • The AOM and DOM constants are not defined in the global context. They must be defined inline in JScript files to be referenced by variable name.



---

# JScript_with_ACL

JScript expressions or scripts can be called from ACL with one of the following ACL primitives:

- • jscript — Function that evaluates a JScript expression and returns the result as a string.

- • js — Command that evaluates a JScript expression and displays the result.

- • source — Command that interprets files ending in .js as JavaScript programs to be executed when set javascriptinterpreter is set to jscript .

The flow of control in the JScript interface usually starts with the execution of one of these ACL functions or commands, with the exception of customization files ending in .js . Arbortext Editor and the Arbortext PE sub-process automatically load and execute JScript programs from the doctype .js , instance .js , and document .js files following the same rules as doctype .acl , instance .acl , and docname .acl files.

The JScript interpreter starts the first time Arbortext Editor or the Arbortext PE sub-process executes one of these ACL functions or commands or reads a .js customization file. Arbortext Editor and the Arbortext PE sub-process will also start the Java Virtual Machine, if necessary. You may also specify the -jvm and -js startup command options to start JScript when Arbortext Editor is opened.

Unlike the Java interface, only string arguments are passed from ACL to JScript. ACL arrays must be converted to some form of delimited string (for example, as an array literal) or passed element by element to JScript expressions. Refer to Passing Arrays Between JavaScript and ACL for more details.

JScript objects may not be returned directly to ACL. If the result of a JScript expression passed to javascript is an object, the toString method is invoked on the object and that value is returned by javascript .



---

# Sample_JScript_Code

Sample JScript code that uses the JScript AOM interface is included in the Arbortext-path \samples\jscript directory. The readme.txt file in this directory provides a description of the sample code and instructions for invoking the sample scripts. Examples show how to use the DOM to manipulate the active document, register DOM Event handlers, and transfer arrays between JScript and ACL. The JScript examples are ported from the corresponding Rhino JavaScript samples of the same name.



---

# Specifying_the_Interpreter_for_.js_Files

Arbortext Editor supports two JavaScript interpreters on Windows. You should specify which interpreter to use to process your .js files. You can include a special comment as the first line of the file. If the first line of the .js file contains a comment using either form specified in the following examples, then the Microsoft JScript interpreter will be used.

```
// application="text/jscript"
```

or

```
// <script application="text/jscript">
```

You can also specify the interpreter with the ACL set javascriptinterpreter command. However, we recommend using the commenting technique as it ensures proper handling of your .js files regardless of the javascriptinterpreter setting.