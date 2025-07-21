

---

# Accessing_the_Java_Console

The Java Console displays everything that a Java program writes to the Java System.out PrintStream and output from the JavaScript print() function. The Java Console also displays the JVM version number and vendor.

For example, if a Java method executes:

```
System.out.println("Hello");
```

then Hello displays on the Java Console (if it is open).

If the Java Console is closed, output will be discarded.

There are two ways you can access the Java Console:

- • Choose Tools > Java Console .

- • Use the java_console ACL function, which can also specify the size of the window.



---

# Accessing_the_Java_Console

The Java Console displays everything that a Java program writes to the Java System.out PrintStream and output from the JavaScript Print() function. The Java Console also displays the JVM version number and vendor.

For example, if you use the java_static function to run a Java method and that Java method executes:

```
System.out.println("Hello");
```

then Hello displays on the Java Console (if the Java Console is open).

If the Java Console is closed, output will be discarded.

There are two ways in which you can access the Java Console:

- • Choose Tools > Administrative Tools > Java Console .

- • Use the java_console function . You can also use this function to specify the size of the window.



---

# AOM_Packages

Arbortext Editor and the Arbortext Publishing Engine ship with Java classes for using the AOM from the Java programming language. The supplied Java classes are stored in a Java archive file Arbortext-path \lib\classes\aom.jar and are intended for developer use. The AOM and DOM Java classes and interfaces are stored in the following packages:

All the methods in the Application class and the Acl class are class methods. Therefore you will never need an instance of the Application or an Acl object.

Your Java program should import the required AOM and DOM packages. For example, if you are writing a DOM event handler you would need to import at least the following packages:

```
import com.arbortext.epic.*;
import org.w3c.dom.*;
import org.w3c.dom.events.*;
```

See Overview for details on using events with the AOM.



---

# Compiling_Your_AOM_Java_Program

When compiling a Java program that uses the AOM, you must put Arbortext-path \lib\classes\aom.jar in the compiler's -classpath argument. For example:

```
javac -classpath "C:\Program Files\Arbortext\editor\lib\classes\aom.jar" MyClass.java
```

The compiled program can only be run within PTC Arbortext ’s Java environment. Java programs running in a JVM outside of Arbortext Editor cannot use the AOM classes.



---

# Debugging_Java_Applications

Arbortext Publishing Engine requires you to obtain a JRE from Oracle (www.java.com) and install it. Arbortext supports the Java Platform Debugger Architecture (JPDA, see http://java.sun.com/products/jpda/ ),any JPDA compliant Java debugger can hook into Arbortext .

JDB can also be used to debug a Java program using two methods: the socket method and the shared memory method.

Before using JDB, ensure you have Oracle JDK version 11 or later installed on your workstation. Java debugging related DLLs and shared libraries must be accessible by the debugger. The PATH environment variable must include the bin directory of the JDK.

Compile your Java programs with the -g flag (for debugging).



---

# Java_Access_to_DOM_Extensions

The AOM's extensions to DOM are represented by companion interfaces that start with the letter A , for example, ANode is the extension to the W3C Node interface, ADocument is the extension to the Document interface, and so on.

In Java, these interfaces can be obtained from their related objects by using the casting methods. For instance:

```
Document doc = Application.getActiveDocument();
Range r = ((ADocument)doc).getInsertionPoint();
```



---

# Java_and_ACL

To call a Java method from ACL, use one of the following java_ type functions.

- • java_constructor — Calls a Java constructor.

- • java_constructor_modal — Calls a Java constructor in a new thread.

- • java_delete — Deletes a Java object created by java_constructor , java_instance , or java_static .

- • java_instance — Calls a Java instance method.

- • java_instance_modal — Calls a Java instance method in a new thread.

- • java_static — Calls a Java static method.

- • java_static_modal — Calls a Java static method in a new thread.

- • java_init — Tests if the JVM is running and optionally initializes it.

The flow of control in the Java interface usually starts with the execution of a java_ type ACL function. Arbortext Editor or the Arbortext PE sub-process starts its embedded Java Virtual Machine (JVM) at startup, making the distributed Java classes and user Java classes available. Java .class files placed in the custom\init directory are automatically executed without the need for the java_ type functions.

The Java programming language supports method overloading, so several methods in a class may have the same name with different arguments. When searching for the method to invoke, Arbortext Editor or the Arbortext PE sub-process will use the first method it finds that has the correct name and correct number of arguments.

The java_ type functions use Java reflection methods to analyze the called Java class or method before calling it, converting the arguments in the java_ type function to the data types used by the called Java code. If you include ACL variables and function calls within your arguments, Arbortext Editor or the Arbortext PE sub-process will perform the necessary variable substitution and pass the result to the called Java code. All arguments passed are considered read-only to the called Java code; the called Java code will not change the value of any of the passed arguments.

Argument values that originate in ACL and are passed to a class or method can only be converted to a void, a Java string, or one of the supported primitive data type. The supported primitive data types are:

- • int

- • short

- • long

- • float

- • double

- • char

- • byte

Argument values that originate as returned data from a previous call to a java_ type function can be passed back to a Java class or method. For example, a called Java method may return a Java structure. This returned object would be placed within the specified ACL return variable name. While this Java structure could not be used directly within ACL, you could pass it to another Java class or method by calling a java_ type function and supplying the return variable name as an input argument.



---

# Java_Interface_Exceptions

Several AOM and DOM methods will raise an exception if an error occurs. The following tables summarize the DOM and AOM exception classes:

In the Arbortext Editor Java interface, all DOM and AOM exceptions are subclasses of java.lang.RuntimeException and inherit the getMessage method from the java.lang.Throwable interface. The getMessage method can be used to retrieve an error message associated with the exception.

Most DOM and AOM exception classes define a code field that can be accessed to determine the numeric error code associated with the exception (the exception is the AOMException class). Symbolic names for the error codes listed with each exception interface description in Interface Overview are available as class constants. For example, the following checks for a specific DOM error code ( NO_MODIFICATION_ALLOWED_ERR ):

```
try {
node.insertBefore(newNode, refNode);
}
catch (DOMException e) {
if (e.code == DOMException.NO_MODIFICATION_ALLOWED_ERR) {
// document is read only
}
}
```

If your Java program does not catch an exception, its execution will be aborted and an error message will be displayed.



---

# Java_Virtual_Machine_(JVM)_Management

By default at startup, Arbortext Editor detects and loads an installed Java Virtual Machine (JVM). You can also load the detected JVM using the java_init function. The JVM instance is dedicated to running Java code started from within Arbortext Editor . Arbortext Editor creates only one instance of the JVM per session. The JVM is unloaded when you end the current Arbortext Editor session.

If you choose to load another JVM, specify it with the set javavmpath ACL command, or APTJAVAVMPATH environment variable.

You can use the set javavmmemory ACL command to set the maximum size of the memory allocation pool before the JVM starts.

By default, Arbortext Editor uses the JVM in the Java Runtime Environment (JRE) included in the Arbortext Editor installation. The JRE is located in the Arbortext-path \bin\jre directory. You can see the current JVM version included with Arbortext Editor by choosing Tools > Administrative Tools > Java Console to open the Arbortext Java Console .



---

# Making_Classes_Available_to_the_Embedded_JVM

You can use the set javaclasspath command or the append_javaclass_path function to set the list of directories where the embedded JVM can locate your Java classes. The default setting of set javaclasspath is empty. Regardless of whether set javaclasspath is set, the embedded JVM searches the distributed Java classes in Arbortext-path \lib\classes\aom.jar . The aom.jar file holds com.arbortext.epic , which contains the Arbortext Editor distributed Java classes that implement the AOM and DOM.

Any .class and .jar files in Arbortext-path \custom\classes are automatically added to the Arbortext Editor class path.

Subsequent changes to specify external Java class directories do not affect the running JVM until you exit Arbortext Editor and start a new session. Be sure to set the path to your directory before making your first Java function call.



---

# Sample_Java_Code

Sample Java code for the Java interface is included in the Arbortext-path \samples\java directory. The README file in this directory provides a description of the sample code and how to invoke the sample methods. Note that you must compile the sample Java code before you can use it.



---

# Using_an_IDE_to_create_Your_AOM_Java_Program

There are a number of Java-based Integrated Development Environments (IDE) that can be used to create AOM Java programs. The IDE must be able to find the AOM JAR file. Using Oracle's J/Developer version 3.2.2 as an example, follows these instructions:

Refer to the documentation for your IDE for instructions on a class path.