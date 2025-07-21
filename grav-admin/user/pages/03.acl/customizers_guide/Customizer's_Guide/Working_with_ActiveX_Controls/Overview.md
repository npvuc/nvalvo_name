

---

# Arbortext_Editor_and_ActiveX_Controls

ActiveX controls can be implemented with Arbortext Editor in two ways:

- • In a separate XUI file specifying the operation of the control. Refer to the description of the activex element in the Working with XUI (XML-based User Interface) dialog boxes chapter of the Customizer's Guide .

- • Defined and called directly from the .dcf file. The control is still launched in a generated XUI dialog box. Refer to Executing ActiveX Controls Using the .dcf File to Bind to an Element Directly .

Keep the following items in mind when working with ActiveX controls and Arbortext Editor .

- • Using ActiveX controls with Arbortext Editor is supported on Windows platforms. Refer to the Installation Guide for Arbortext Editor, Arbortext Styler, and Arbortext Architect for a detailed list of requirements for working with ActiveX controls.

- • Rhino JavaScript does not support ActiveX controls in Arbortext Editor .

- • ActiveX controls are third-party tools. Many free controls are available to Windows users, as are many commercially licensed controls. Licensing and obtaining proper documentation for these third-party products is your responsibility. No claims are made as to the reliability or fitness of a third-party control or its compatibility with Arbortext Editor .



---

# Related_AOM_Interfaces

Working with ActiveX controls makes use of the following AOM interfaces. (Refer to the Programmer's Reference for details on all AOM interfaces.)



---

# Running_Scripts

When working with ActiveX controls, keep the following items in mind:

- • To call an ActiveScript from another ActiveScript, use the Application.createScriptContext and ScriptContext.loadScriptFile methods. Do not use the ACL source command from within a JScript or VBScript file as in:

- • Any session-level scripts placed in Arbortext-path \custom\init or any directory defined by the APTCUSTOM environment variable will be executed automatically when Arbortext Editor starts.

- • Any document type level scripts (such as Arbortext-path \custom\doctypes\axdocbook\axdocbook.js ) will be run automatically the first time a document of the named document type is opened or created. The doctype .* file is not run on subsequent openings of files of the same document type.

- • Any document-level scripts (such as Arbortext-path \custom\doctypes\axdocbook\instance.js ) will be run automatically each time a document of the named document type is opened or created.

- • Any instance-specific scripts (such as filename .vbs where filename is the same root name as that of the document) will be run each time a specific document of that name is opened or created.