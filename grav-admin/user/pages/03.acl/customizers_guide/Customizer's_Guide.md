

---

# Custom_Applications

# Overview of Custom Programs and Scripts

The Arbortext Editor and Arbortext Publishing Engine installations have directory structures within them where you can place your custom scripts and programs. The custom and the application directories are described in the following sections.



---

# Customizing_Copying_and_Pasting_from_Other_Applications

# Customizing Copying and Pasting from Other Applications

On the Windows platform, Arbortext Editor enables you to copy content from other applications and paste the content into your document using matching markup from your document type. You can copy content from Microsoft Word, Adobe FrameMaker, web browsers, text editors, and other applications and paste that content into your document. Arbortext Editor uses technology to map the content from the other application to the markup appropriate for your document. For example, assume you are authoring a DITA document and copy a bullet list in a Microsoft Word document. When you paste that list into your DITA document, it will be pasted with the appropriate ul and li tags.

This chapter provides an overview of this feature and its limitations. It tells you how to disable the feature and how to modify the supported clipboard source types. It also tells you how to implement the feature for custom document types, and how to customize the Paste Special dialog box.



---

# Customizing_DITA_Support

# Customizing DITA support

Arbortext Editor provides a specialized user interface for editing DITA (Darwin Information Typing Architecture) maps and topics. You can customize parts of that interface to meet the needs of your site.



---

# Customizing_Help

# Customizing Tag Help

Tag help is the help that appears when you place the mouse pointer over a tag in your document and press SHIFT + F1 or Help . Tag help describes the elements declared in the document type that is being used.



---

# Customizing_PDF_Publishing

# PDF Publishing Overview

There are several ways in which you can create PDF files with Arbortext Editor and Arbortext Styler or Arbortext Publishing Engine :

- • With the PTC APP publishing engine, you can publish PDF directly from an XML file or generate from intermediate PostScript source.

- • With the FOSI publishing engine, you can publish PDF directly from an XML file.

See Publishing Engine Overview , Choosing PDF Configuration Options , and Print and PDF Configuration Files for an explanation of print engines and PDF configuration files.



---

# Customizing_Publishing_Rules

# Customizing Publishing Rules

See Publishing Rules Overview and its related topics in the Arbortext Editor or Arbortext Publishing Engine Interactive online help for general information about creating, using, and managing publishing rules. You will need to be familiar with how publishing rules work to better understand this documentation.



---

# Customizing_Your_Site's_Profiling_Configuration

# Customizing Your Site's Profiling Configuration

Profiling sections of documents let you designate that certain sections contain information targeted at a specific audience or contain information that only applies when a particular set of circumstances exists. This chapter describes how to configure profiling specific to your site’s needs.



---

# Merging_Data_from_Other_Sources





---

# Working_with_ActiveX_Controls

# Overview

Microsoft ActiveX controls are Windows-only objects that combine features of COM servers, COM Automation, COM Event interfaces, and ActiveScript hosting. ActiveX controls are self-contained applets or controls which expose their functionality to third-party programmers through COM. Arbortext Editor lets you configure, launch, and use these COM controls to extend Arbortext Editor with tools from a variety of software vendors or through using those controls you create yourself. You can also run Arbortext Editor itself in an ActiveX control.

Using ActiveX controls provide the following benefits:

- • Less programming — When using existing controls, developers need only be concerned with writing scripts that handle the communication of data between their XML and the controls. They do not need to design the user interface, develop the user interface, or design the API or properties that hold the data entered by the user.

- • Enhanced end-user productivity — Create specialized user interfaces for particular types of documents.

- • Simplified complex tagging operations — Create boilerplate sections of documents, set sections to be read-only, create tagging with desired attributes or elements completed, or otherwise control the end-users' interaction with documents.

For details on creating and using ActiveX controls in general, refer to the ActiveX Controls section of Microsoft's MSDN Library. ( http://msdn.microsoft.com/library/ ) and numerous other locations on the World Wide Web. The remainder of this chapter covers configuring and launching ActiveX controls with Arbortext Editor and running Arbortext Editor in an ActiveX control.



---

# Working_with_Arbortext_Import-Export





---

# Working_with_XUI_(XML-based_User_Interface)_Dialog_Boxes

# XUI Overview

The Arbortext XUI (XML-based User Interface) technology lets an application programmer create, display, manipulate, and modify dialog boxes in real time by writing and modifying XML documents. All aspects of a dialog box, including controls, layout, and event listeners, can be stored in a single XUI XML document. The document type for XUI XML documents is Arbortext-path \doctypes\xui\xui.dtd . The Arbortext XUI technology is influenced by the Mozilla XML User Interface Language (XUL) and its ongoing development ( www.mozilla.org/projects/xul/xul.html ).

Each control in a XUI dialog box is associated with an element in an XML document. For example, to add a check box control to the dialog box, insert a checkbox element in to the XUI document. A control’s properties are represented by the attributes of the element. For example, the label attribute of the checkbox element specifies the label of the check box control in the dialog box. The checked attribute of the element represents the current status of the check box control.

The layout of XUI dialog boxes is automatically managed by PTC Arbortext Editor . The type of the layout and the properties of the layout are specified in the XUI XML document by inserting layout related elements and attributes. XUI layout algorithms arrange layout by considering the size of each control and ensuring that the dialog box is displayed in a balanced manner after resizing.

PTC Arbortext Editor makes use of W3C XML Events to monitor the activities in the dialog box. The W3C XML Events specification can be found at www.w3.org/TR/2001/WD-xml-events-20011026 . Event listening scripts can be inserted in the XUI XML document as the content of an element representing an event listener.

A set of AOM interfaces manipulate XUI dialog boxes. For example, the Window interface represents the frame window of the XUI dialog box. You can use the hide method to hide the dialog box, the setTitle method to set the window’s title, and so on. Refer to Manipulating XUI Dialog Boxes using the AOM for more details.

XUI dialog boxes can be displayed as standard dialog boxes (overlaying an application or document), and they can be displayed embedded in a document in the Edit pane in Arbortext Editor . Refer to Embedding XUI Dialog Box Controls in a Document for details on displaying XUI dialog boxes within documents. Standard dialog boxes with docking enabled can be dragged into a Arbortext Editor edit window and docked on one edge of the edit window. Dialog boxes with docking enabled can contain all controls that are allowed in a standard dialog box except for toolbars and menubars.