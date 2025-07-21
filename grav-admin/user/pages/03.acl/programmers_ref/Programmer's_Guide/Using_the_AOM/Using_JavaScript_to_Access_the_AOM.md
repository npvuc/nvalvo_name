

---

# Calling_Java_from_JavaScript

The Mozilla Rhino JavaScript interpreter bundled with Arbortext Editor provides a mechanism called LiveConnect that lets you use Java classes and methods from JavaScript. The Arbortext Object Model (AOM) classes are written in Java and made available in JavaScript by LiveConnect.

LiveConnect manages the Java to JavaScript communication, including conversion of data types. JavaScript: The Definitive Guide, written by David Flanagan and published by O'Reilly, discusses this subject. There are some limitations with LiveConnect and the AOM, as noted in JavaScript Limitations .

Rhino also supports defining new JavaScript classes by writing Java code that extends the org.mozilla.javascript.ScriptableObject class. The JavaScript function defineClass makes such classes available to JavaScript. Refer to the Rhino documentation at the Mozilla web page ( www.mozilla.org/rhino/doc.html ) for details.

With LiveConnect, Java packages are represented in JavaScript by the JavaPackage class. You can access the Java classes provided with the JVM embedded in Arbortext Editor , plus those found in the Java class path (as specified by the javaclasspath parameter of the setOption method, described in AOM set Options Overview ) from the top-level JavaPackage object Packages . This includes the standard Java system classes (for example, Packages.java.lang.System ) and the packages provided by Arbortext (for example, Packages.com.arbortext.epic , Packages.org.w3c.dom ), and the JavaScript interpreter ( Packages.org.mozilla.javascript ). As a convenience, the classes in the java package can be referred to directly without the Packages qualifier, for example, java.lang.System and java.lang.awt.Frame .

The global object Application is a shortcut for the Packages.com.arbortext.epic.Application JavaClass. Similarly, the global object Acl is a shortcut for the Packages.com.arbortext.epic.Acl JavaClass.

The following JavaScript example uses the standard Java AWT classes to create and display a dialog box.

```
function hello()
{
var f = new java.awt.Frame("Hello World");
var ta = new java.awt.TextArea("hello, world", 100, 200);
f.add("Center", ta);
f.pack();
f.show();
}
hello();
```

A more complicated example with event handling is included with the Arbortext distribution. Refer to Sample JavaScript Code for details.



---

# JavaScript_and_ACL

JavaScript expressions or scripts can be called from ACL with one of the following ACL primitives:

- • javascript — Function that evaluates a JavaScript expression and returns the result as a string.

- • js_source — Function that reads and executes a file containing a JavaScript program.

- • js — Command that evaluates a JavaScript expression and displays the result.

- • source — Command that interprets files ending in .js as JavaScript programs to be executed when set javascriptinterpreter is set to rhino .

The flow of control in the JavaScript interface usually starts with the execution of one of these ACL functions or commands, with the exception of customization files ending in .js . Arbortext Editor and the Arbortext PE sub-process automatically load and execute JavaScript programs from the doctype .js , instance .js , and document .js files following the same rules as doctype .acl , instance .acl , and docname .acl files.

The JavaScript interpreter starts the first time Arbortext Editor or the Arbortext PE sub-process executes one of these ACL functions or commands or reads a .js customization file. Arbortext Editor and the Arbortext PE sub-process will also start the Java Virtual Machine, if necessary. You may also specify the -jvm and -js startup command options to start Java and JavaScript, respectively, when Arbortext Editor is opened.

Unlike the Java interface, only string arguments are passed from ACL to JavaScript. So any ACL argument value passed to js_source is converted to a string. ACL arrays must be converted to some form of delimited string (for example, as an array literal) or passed element by element to JavaScript expressions. Refer to Passing Arrays Between JavaScript and ACL for more details.

JavaScript objects may not be returned directly to ACL. If the result of a JavaScript expression passed to javascript is an object, the toString method is invoked on the object and that value is returned by javascript .



---

# JavaScript_Global_Objects

The Arbortext JavaScript implementation provides several global objects available to all JavaScript scripts. The Application and Acl objects are instances of the AOM Application and Acl interfaces. Only one object for each interface exists in a Arbortext Editor or Arbortext PE sub-process session.



---

# JavaScript_Interface_Error_Handling

When executing JavaScript programs, Arbortext Editor displays error messages if there are problems when starting the JavaScript interpreter, in the embedded Java Virtual Machine (JVM), or if the JavaScript interpreter reports an exception. If the JavaScript interpreter reports an exception, Arbortext Editor displays a message such as “The Java method name has thrown an exception.” If you use the ACL function javascript to invoke the JavaScript interpreter, name is eval ; if you use the ACL function js_source , name is source .

The JavaScript exception message is sent to the Java Console if it is open; otherwise, it is discarded. When developing JavaScript applications, choose Tools > Java Console to open the Java Console and view exception messages.

For JavaScript code executed by reading a .js file, the JavaScript exception report includes a traceback showing the file name and line number of each function active at the time of the error. The traceback also lists Java methods for the JavaScript interpreter, which can be ignored.



---

# JavaScript_Language_Extensions

The Arbortext Editor JavaScript implementation includes a few non-standard extensions, modeled on similar features provided by the Rhino Shell. The Rhino Shell is a standalone utility from Mozilla that runs JavaScript programs.



---

# JavaScript_Limitations

The following lists some limitations of the Arbortext Editor JavaScript implementation.

- • The Mozilla Rhino JavaScript interpreter does not support the netscape.javascript.JSObject class as part of LiveConnect. It uses a different mechanism for accessing JavaScript objects from Java. See Requirements and Limitations at the Mozilla web page developer.mozilla.org/en-US/docs/Web for additional limitations of the interpreter, and the Mozilla web page developer.mozilla.org/en-US/docs/Web/Tutorials for a description of using JavaScript objects from Java.

- • Strings returned by AOM/DOM methods are Java String objects and not JavaScript String objects. While Java String objects share many of the same methods as JavaScript String objects (for example, charAt , substring , toLowerCase ) and can be used in string contexts, they are not equivalent. In particular, Java String has no length property; use the length() method instead. Also, Java String is not automatically converted to a number when used in a numeric context. To explicitly convert a Java String to a number when appropriate, use the parseInt or parseFloat function.



---

# Sample_JavaScript_Code

Sample JavaScript code that uses the JavaScript AOM interface is included in the Arbortext-path \samples\javascript directory. The readme.txt file in this directory provides a description of the sample code and how to invoke the sample scripts. The samples include examples of using the DOM to manipulate the active document, registering DOM Event handlers, using Java AWT classes, and transferring arrays between JavaScript and ACL.

There is a sample from the Mozilla Rhino distribution that implements a JavaScript File class in Java and an example script, jsdoc.js , that uses the defineClass JavaScript extension to define the File class.

Refer to Rhino Examples at the Mozilla web page ( www.mozilla.org/rhino/examples.html ) for additional sample JavaScript scripts.



---

# Specifying_the_Interpreter_for_.js_Files



Arbortext Editor supports two JavaScript interpreters. You should specify which interpreter to use to process your .js files. You can include a special comment as the first line of the file. If the first line of the .js file using either form specified in the following examples, then the Rhino JavaScript interpreter will be used.

```
// type="text/javascript"
```

or

```
// <script type="text/javascript">
```

You can also specify the interpreter with the ACL set javascriptinterpreter command. However, we recommend using the commenting technique as it ensures proper handling of your .js files regardless of the javascriptinterpreter setting.