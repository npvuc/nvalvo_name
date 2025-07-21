

---

# addNamedItem_method

Adds a script object or COM object to the script context's variable namespace. This method makes a given script's methods available to other script instances. Such availability is important when binding events to child controls in an ActiveX component, such as to buttons residing on an HTML form launched within the Microsoft WebBrowser control. Because event binding is name-based, this method gives much greater flexibility than would normally be available from the script host.



---

# addTypeLib_method

Adds a type library to the script context. This makes the constants defined in the library available to scripts in the context.



---

# addTypeLibFlags_enumeration

Bits defined in the flags parameter to AddTypeLib .

The addTypeLibFlags enumeration has the following constants of type unsigned short .



---

# loadScriptFile_method

Loads, compiles, and runs the specified script file.



---

# loadScriptText_method

Compiles and evaluates the script expression and returns the result as a string.



---

# scriptType_enumeration

Passed as the value of the scriptType parameter to loadScriptText .

The scriptType enumeration has the following constants of type unsigned short .



---

# terminate_method

Terminates and unloads the Microsoft Windows Script engine instance associated with this object. It gives the user the means to close a given script engine instance.