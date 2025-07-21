

---

# Using_ACL_with_the_AOM

# Using ACL with the AOM

You can access the Arbortext Object Model (AOM) from the Arbortext Command Language (ACL). Because the AOM does not currently provide all the functionality available from ACL, an AOM program may need to call ACL functions for certain types of customizations. There are several ACL functions that interface with Java, JavaScript, JScript, VBScript, and COM, which are documented in the Arbortext Command Language Reference . Each section in this guide that covers a specific programming or scripting language notes any language-specific binding issues.



---

# Using_COM_to_Access_the_AOM

# Using COM to Access the AOM

Arbortext Editor includes a Component Object Model (COM) binding to the AOM. Using this binding, developers on Windows platforms can write programs that use COM to access the AOM or DOM functions supported in Arbortext Editor .

COM should be installed on all Windows systems that are running Arbortext Editor . It is unlikely that your Windows systems will not have COM already installed on them.

When acting as a COM server, Arbortext Editor registers an Epic.Application COM class which implements the _Application N interface (for example, _Application6 — consult the type library for the correct interface version), an Epic.Acl COM class which implements the IAcl3 interface, a number of DOM xxx classes which implement their respective IDOM xxx interfaces, and many other xxx classes that implement their respective I xxx AOM interfaces.

If you are trying to use COM among different machines, you will need to install DCOM (Distributed Component Object Model). Extensive information on both COM and DCOM is available from the Microsoft Developers Network (MSDN) web site at msdn.microsoft.com .

The Arbortext Editor COM interface to the DOM portion of AOM uses the COM binding defined by Microsoft with changes for DOM Level 2 and Arbortext extensions. However, Microsoft has made several significant extensions to the DOM that are not supported by Arbortext . The definition of the COM classes and methods that Arbortext Editor exports is contained in the type library that is part of the Arbortext-path \bin\editor.exe binary. Developers can use a variety of tools to inspect this type library.

The type library defines multiple versions of many interfaces. When an interface is extended for a given Arbortext Editor or Arbortext Publishing Engine release, a new version of the interface is defined with the version number incremented. For example, the _Application3 interface was introduced with Epic Editor and E3 4.3.

Arbortext Editor or an Arbortext PE sub-process does not need to be running for it to be available to COM. If Arbortext Editor or an Arbortext PE sub-process is not running when a call is made to the Arbortext Editor COM server, it will automatically load and run in the background while servicing the COM call. If a user then uses the Windows user interface to start a Arbortext Editor session, the invisible instance that was running exclusively as a COM server automatically becomes visible and available to the user.



---

# Using_Java_to_Access_the_AOM

# Using Java to Access the AOM

Arbortext Editor and Arbortext Publishing Engine include a Java binding to the AOM. Using this binding, software developers can use the Java programming language to write applications for Arbortext Editor or the Arbortext Publishing Engine .

Arbortext Editor and the Arbortext Publishing Engine implement the Java interface using the Java Native Interface (JNI). The JNI allows Java code that runs within an embedded Java Virtual Machine (JVM) to operate with applications and libraries written in other languages such as C++. In Arbortext Editor and the Arbortext Publishing Engine , the JNI interacts specifically with the AOM.

Arbortext Editor or an Arbortext PE sub-process creates only one instance of the JVM per session and initializes it the first time a Java method is executed. The -js startup option may be specified when launching Arbortext Editor to cause the JVM to be initialized on startup. You can also start the JVM using the java_init ACL function. The JVM is unloaded when you end the current Arbortext Editor or Arbortext PE sub-process session.

There are several ACL functions of the form java_ xxx that allow ACL programs to call a Java static method, a Java instance method, or a Java constructor, and otherwise interact with Java programs. These ACL functions are explained in Java and ACL .



---

# Using_JavaScript_to_Access_the_AOM

# Using JavaScript to Access the AOM

Arbortext Editor and the Arbortext Publishing Engine include a JavaScript binding to the AOM. Using this binding, software developers can use the JavaScript programming language to write applications for Arbortext Editor and the Arbortext Publishing Engine .

Arbortext uses the Rhino open-source Java implementation from The Mozilla Organization as its JavaScript interpreter. This version of Rhino supports the JavaScript language version 1.5 and is compliant with the European Computer Manufacturers Association (ECMA) standard described in ECMA-262 Edition 3 ( www.mozilla.org/js/language/E262-3.pdf ).

Arbortext Editor uses the Rhino interpreter unmodified, distributed as Arbortext-path \lib\classes\js.jar . For more information about Rhino, see the Rhino: JavaScript for Java web page at www.mozilla.org/rhino . The source code for the interpreter is available at the Mozilla site at www.mozilla.org/rhino/download.html .

The Arbortext Object Model (AOM) interface for JavaScript is implemented on top of the Java AOM interface classes using a feature called LiveConnect. Refer to Calling Java from JavaScript for details.



---

# Using_JScript_to_Access_the_AOM

# Using JScript to Access the AOM

Arbortext Editor and the Arbortext Publishing Engine include a JScript binding to the AOM. Using this binding, software developers can use the JScript programming language to write applications for Arbortext Editor and the Arbortext Publishing Engine .

Arbortext uses Microsoft Windows Script (or ActiveScript) as the JScript interpreter. This script engine is represented primarily by the system files jscript.dll and scrrun.dll which are typically installed by Microsoft Windows, Internet Explorer, and the Windows Script Host upgrades available from the Microsoft Developers Network (MSDN). Arbortext recommends Windows Script Version 5.6, which is free from the Microsoft web site at: msdn.microsoft.com/library/default.asp?url=/library/en-us/script56/html/letintro.asp .

The AOM interface and the DOM interface for JScript are implemented using the PTC Arbortext COM interface. Access to external COM servers is implemented through standard COM interfaces used by the Microsoft script engines.



---

# Using_VBScript_to_Access_the_AOM

# Using VBScript to Access the AOM

Arbortext Editor and the Arbortext Publishing Engine include a VBScript binding to the AOM. Using this binding, software developers can use the VBScript programming language to write applications for Arbortext Editor and the Arbortext Publishing Engine .

Arbortext uses Microsoft Windows Script (or ActiveScript) as the VBScript interpreter. This script engine is represented primarily by the system files vbscript.dll and scrrun.dll which are typically installed by Microsoft Windows, Internet Explorer, and the Windows Script Host upgrades available on the Microsoft Developers Network (MSDN). Arbortext recommends the most recent version of Windows Script, Version 5.6, which is free from the Microsoft web site at: msdn.microsoft.com/library/default.asp?url=/library/en-us/script56/html/letintro.asp .

The AOM interface and the DOM interface for VBScript is implemented via Arbortext 's COM interface. Access to external COM servers is implemented through standard COM interfaces used by the Microsoft script engines.