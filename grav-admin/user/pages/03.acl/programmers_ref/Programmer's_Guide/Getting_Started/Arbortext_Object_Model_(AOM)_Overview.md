

---

# Introduction_to_the_Arbortext_Object_Model_(AOM)

The AOM provides object-oriented programming access to Arbortext Editor and Arbortext Publishing Engine . The AOM supports the W3C DOM (Document Object Model) Core and Validation interfaces with extensions, and provides many additional interfaces for Arbortext -specific features that are not part of the DOM. The Arbortext extensions to the DOM use a naming convention where A (for Arbortext ) is prepended to the DOM interface name; for example, the Arbortext extension for the DOM Node interface is ANode .

The AOM supports bindings to Java, COM (Component Object Model), and C++. The AOM also provides scripting access to its interfaces using JavaScript, JScript, VBScript, and the ACL ( Arbortext Command Language ).

The following diagram shows the relationship between Arbortext Editor and Arbortext Publishing Engine , the DOM and AOM interfaces, and programs or scripts accessing the DOM and AOM.

Java programs and JavaScript communicate with the DOM and AOM interfaces using the Java Binding. COM C++ programs, VBScript, and JScript communicate with the DOM and AOM interfaces using the COM Binding. C++ Programs communicate with the DOM and AOM interfaces using the C++ Binding. The DOM and AOM interfaces communicate with Arbortext Editor and the Arbortext Publishing Engine .



---

# Introduction_to_the_Document_Object_Model_(DOM)

The Document Object Model (DOM) is a standards-compliant interface for examining and modifying an XML or SGML document. The DOM Level 2 specification is a recommendation of the Worldwide Web Consortium (W3C) comprised of several parts. Arbortext products implement the DOM Level 2 features as described in the following W3C specifications:

- • Document Object Model (DOM) Level 2 Core Specification (http://www.w3.org/TR/DOM-Level-2-Core)

- • Document Object Model (DOM) Level 2 Views Specification (http://www.w3.org/TR/DOM-Level-2-Views)

- • Document Object Model (DOM) Level 2 Events Specification (http://www.w3.org/TR/DOM-Level-2-Events)

- • Document Object Model (DOM) Level 2 Traversal and Range Specification (http://www.w3.org/TR/DOM-Level-2-Traversal-Range), range only

Arbortext also implements the W3C Recommendation Document Object Model (DOM) Level 3 Validation Specification dated 27 January 2004. ( http://www.w3.org/TR/2004/REC-DOM-Level-3-Val-20040127/ ) The validation interfaces are implemented for both XML and SGML documents. (The DOM Level 3 Core interface DOMConfiguration is not implemented in this release.)



---

# Using_the_DOM_Support_in_AOM

Some considerations and limitations for using DOM through the AOM can help you determine your approach.