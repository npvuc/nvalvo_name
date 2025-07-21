

---

# Acl_interface

# Acl interface

The Acl interface represents the ACL ( Arbortext Command Language ) interpreter. It allows the AOM programmer to request that a string be executed as an ACL command or evaluated as an ACL function. The Acl interface also provides methods for converting from ACL OIDs to DOM nodes and from ACL document identifiers to DOM Document nodes.



---

# ActivexEvent_interface

# ActivexEvent interface

The ActivexEvent interface provides specific contextual information associated with Activex events.



---

# ADocument_interface

# ADocument interface

The Arbortext extension to the W3C DOM Document interface.



---

# ADocumentEntityEvent_interface

# ADocumentEntityEvent interface

The ADocumentEntityEvent interface provides specific contextual information associated with the ADocumentEntityEvent extension. Use these event types to notify programmers about important document operations related to entities that are not covered by DOM events.



---

# ADocumentEvent_interface

# ADocumentEvent interface

The ADocumentEvent interface provides specific contextual information associated with the ADocumentEvent extension. Use these event types to notify programmers about important document operations that are not covered by DOM events.



---

# ADocumentType_interface

# ADocumentType interface

Arbortext extensions to the W3C DOM DocumentType interface



---

# AEditEvent_interface

# AEditEvent interface

The AEditEvent interface provides specific contextual information associated with the EditEvent extension. These event types are used to notify programmers of important document operations that are not covered by DOM events.



---

# AElement_interface

# AElement interface

The Arbortext extension to the W3C DOM Element interface.



---

# AEvent_interface

# AEvent interface

The Arbortext extension to the W3C DOM Event interface. This interface adds the moduleType attribute to Event , giving the source of the event.



---

# ANode_interface

# ANode interface

The Arbortext extension to the W3C DOM Node interface.



---

# AOMException_exception

# AOMException exception

Some AOM operations may throw an AOMException as specified in their method descriptions. Unlike DOMException and other exception interfaces, AOMException provides an error message string in the message field instead of a numeric code.

Objects that implement the AOMException interface include the following property:



---

# AOMObject_interface

# AOMObject interface

The Arbortext AOMObject interface is implemented by all AOM and DOM classes.



---

# Application_interface

# Application interface

The Application interface provides access to Arbortext Editor and Arbortext Publishing Engine global functionality. (That is, features that are not associated with any document, document type, or document component.) It is implemented as a singleton: there is only one Application object instantiation in existence.



---

# ApplicationEvent_interface

# ApplicationEvent interface

The ApplicationEvent interface provides specific contextual information associated with the ApplicationEvent .



---

# ARange_interface

# ARange interface

The Arbortext extension to the W3C DOM Range interface.

ARange adds four read-only attributes ( startOID , startPos , endOID , endPos ) that give the start and end points of the Range as strings that may be spliced into ACL commands. Note that ACL represents a point as an OID/POS pair.

Arbortext Editor (and Arbortext Publishing Engine ) and the DOM represent ranges differently. Therefore, the individual components of a DOM range endpoint (attributes startNode , startOffset ) and an Arbortext endpoint (attributes startOID , startPos ) may differ. That is, the OID indicated by startOID will not necessarily be the starting OID for the node indicated by startNode , and the integer value startOffset will not necessarily be equal to the integer value startPos . Nor will there necessarily be equivalences between endNode and endOID or endOffset and endPos .

PTC only guarantees that the point in the document represented by the pair ( startNode , startOffset ) will be the same point as that indicated by the pair ( startOID , startPos ) and that the point represented by the pair ( endNode , endOffset ) will be the same point as that represented by the pair ( endOID , endPos ).

The DOM allows the endpoint of a range to be within a processing instruction; Arbortext products do not. If a DOM (node, offset) pair is located within a processing instruction, the corresponding (OID, pos) pair will indicate the point just before the start of the processing instruction (if the [node, offset] is the start of the range) or just after the end of the processing instruction (if the [node, offset] is the end of the range).



---

# CMSAdapter_interface

# CMSAdapter interface

Represents an installed content management system (CMS) adapter.



---

# CMSAdapterConnectEvent_interface

# CMSAdapterConnectEvent interface

The CMSAdapterConnectEvent interface provides specific contextual information associated with the CMSAdapterConnectEvent extension. These event types notify programmers of events related to logging onto a CMS.



---

# CMSAdapterDisconnectEvent_interface

# CMSAdapterDisconnectEvent interface

The CMSAdapterDisconnectEvent interface provides specific contextual information associated with the CMSAdapterDisconnectEvent extension. These event types notify programmers of events related to logging off a CMS session.



---

# CMSBrowseItem_interface

# CMSBrowseItem interface

The CMSBrowseItem interface contains information returned from CMSBrowseIterator.getNext() . CMSBrowseItem objects are static and do not reflect changes made after the iterator was created.



---

# CMSBrowseIterator_interface

# CMSBrowseIterator interface

For searching and browsing functions, the adapter returns this iterator over the sequence of results. A CMSBrowseIterator object is a static view of the browsing results. It does not reflect any changes made to the content management system (CMS) after the iterator was created.



---

# CMSException_exception

# CMSException exception

Defines the exception thrown by the methods and properties in the Arbortext Object Model (AOM) that work with content management systems (CMS). CMSException objects contain an error code, an error message, and an optional detailed message.

The code field stores one of the CMSExceptionCode constants to indicate the error condition. Arbortext defines the error codes.

The message field contains a human-readable description of the error. These messages should be localized.

The detail field contains an in-depth description of the error that may be written to a log. The description could be something like a Java stack trace or a detailed error description provided by the CMS. Detailed error descriptions do not need to be localized.

Objects that implement the CMSException interface include the following properties:



---

# CMSObject_interface

# CMSObject interface

The CMSObject interface represents a reference to a content management system (CMS) object. If a document references the same child object twice then there will be two different references to that same child CMS object. Each reference will have its own distinct CMSObject object that can have different properties from the other. For example, the start and end properties would be different for each.



---

# CMSObjectEvent_interface

# CMSObjectEvent interface

The CMSObjectEvent interface provides specific contextual information associated with the CMSObjectEvent extension. These event types notify programmers of important CMS object operations.



---

# CMSObjectList_interface

# CMSObjectList interface

The CMSObjectList interface provides fast, random access to a collection of CMSObject s. Do not confuse this with CMSBrowseIterator which provides sequential access to CMSBrowseItem s and is used when there are possibly high-latency calls being made into the CMS.



---

# CMSSession_interface

# CMSSession interface

The CMSSession interface represents a content management system (CMS) session.



---

# CMSSessionBurstDocumentEvent_interface

# CMSSessionBurstDocumentEvent interface

The CMSSessionBurstDocumentEvent interface provides specific contextual information associated with the CMSSessionBurstDocument extension. These event types notify programmers of events related to document bursting and the resultant objects created in the repository.



---

# CMSSessionConstructEvent_interface

# CMSSessionConstructEvent interface

The CMSSessionConstructEvent interface provides specific contextual information associated with the CMSSessionConstructEvent extension. These event types notify programmers of operations that construct in-memory representations of repository objects.



---

# CMSSessionCreateEvent_interface

# CMSSessionCreateEvent interface

The CMSSessionCreateEvent interface provides specific contextual information associated with the CMSSessionCreateEvent extension. These event types notify programmers of events related to creating new CMS objects in the repository.



---

# CMSSessionDisconnectEvent_interface

# CMSSessionDisconnectEvent interface

The CMSSessionDisconnectEvent interface provides specific contextual information associated with the CMSSessionDisconnectEvent extension. These event types notify programmers of events related to logging off a CMS session.



---

# CMSSessionFileEvent_interface

# CMSSessionFileEvent interface

The CMSSessionFileEvent interface provides specific contextual information associated with the CMSSessionFileEvent extension. These event types notify programmers of events related to managing non-textual document objects in the repository.



---

# Component_interface

# Component interface

The Component interface is the base interface for all window components.



---

# Composer_interface

# Composer interface

The Composer interface represents a composition pipeline defined by a Composer Configuration File (CCF). The CCF is an XML document corresponding to the Arbortext Composer DTD.



---

# ControlEvent_interface

# ControlEvent interface

The ControlEvent interface provides specific contextual information associated with Control events.



---

# Dialog_interface

# Dialog interface

The Dialog interface extends the Window interface. It represents a XUI dialog and has the single attribute dialogView .



---

# Interface_Overview

# Interface Overview

The AOM supports most of the DOM interfaces developed by the W3C, several Arbortext extensions to the DOM interfaces, and many additional Arbortext interfaces for features that are not part of the DOM. Refer to Introduction to the Document Object Model (DOM) for a list of supported DOM specifications.

The interface descriptions use the DOM conventions in presenting a language-neutral definition of the list of constants (enumerations), attributes (properties), and methods implemented for each interface. For some language bindings, the enumeration (constant) names are available as global typedef s (for example, COM C++), as static final constants (Java, JavaScript), or only available as numeric values (JScript and VBScript, currently). Attributes (or properties) in some language bindings are translated to set Xxx and set Xxx methods. For example, the Application.activeDocument attribute is obtained by calling the Application.getActiveDocument() method in Java. Read-only attributes, as noted in the Access table entry of each attribute description, only have a get Xxx method in these language bindings. (Refer to the Index terms “attributes”, “enumerations”, and “methods” for alphabetical listings of each, respectively.)

The descriptions of the W3C interfaces in the following chapters are taken from their respective W3C specifications. Each description provides a reference to its W3C specification.

In the W3C interface descriptions, the DOMString type is a string of 16-bit Unicode characters, the same as the String type in the other interface descriptions. Throughout the documentation consider references to HTML or XML to also include SGML.

Square braces ( [ ] ) denote optional trailing parameters which may be omitted in most script bindings. Also, the AOM provides method overloads in the Java binding so that optional parameters may be omitted.

The AOM supports the following interfaces:

The AOM supports the following Arbortext PE Application interfaces:



---

# MenuBar_interface

# MenuBar interface

The MenuBar interface represents a menu bar.



---

# MenuEvent_interface

# MenuEvent interface

The MenuEvent interface provides specific contextual information associated with Menu events.



---

# MenuItem_interface

# MenuItem interface

The MenuItem interface represents a menu item.



---

# PropertyMap_interface

# PropertyMap interface

The PropertyMap interface provides the abstraction of a collection of typed objects associated with string keys.

The items in the PropertyMap are accessible by a string key. The keys attribute is provided to iterate over all entries in the map.

A PropertyMap object can be created using the Application.createPropertyMap factory method. Some AOM methods return PropertyMap objects.



---

# ScriptContext_interface

# ScriptContext interface

The ScriptContext interface provides methods to load and run scripts using the Microsoft Windows Scripting engine in separate contexts.

This interface is only available in the COM binding of the AOM.



---

# StringList_interface

# StringList interface

The StringList interface provides the abstraction of an ordered collection of DOMString s, without defining or constraining how this collection is implemented.

The items in the StringList are accessible by an integral index, starting from 0.

Some AOM methods return StringList objects. A StringList object can be created using the Application.createStringList factory method. For example,

```
var list = Application.createStringList(10);
```

creates a new StringList object with 10 elements, all null. The length attribute will return 10 in this case. To create an array where length returns the number of non-null entries, create the StringList with size 0 and add elements using the append method. For example,

```
var list = Application.createStringList(0);
list.append("one");
list.append("two");
list.append("three");
```

The length attribute would return 3 in this case.



---

# TableCell_interface

# TableCell interface

Represents a single cell in a table. May be part of a spanned TableMulticell , but represents a single cell in that multicell if so.



---

# TableColumn_interface

# TableColumn interface

Represents either a column of cells. Every cell is part of exactly one TableColumn .



---

# TableException_exception

# TableException exception

Defines the exceptions used by the Table AOM methods.

Objects that implement the TableException interface include the following property:



---

# TableGrid_interface

# TableGrid interface

Represents a table grid which is a rectangular array of cells. All rows and all columns are the same length.



---

# TableMulticell_interface

# TableMulticell interface

Represents a rectangular array of spanned cells in a table. The majority of the behavior of a TableMulticell is inherited from TableRectangle .



---

# TableObject_interface

# TableObject interface

Base class for all table objects.



---

# TableObjectStore_interface

# TableObjectStore interface

A TableObjectStore contains a collection of TableObject s all from the same document. Elements can be added in any order (objects are sorted into row-major order as they are added) and retrieved through iteration.



---

# TableRectangle_interface

# TableRectangle interface

Represents a rectangle of cells.



---

# TableRow_interface

# TableRow interface

Represents a row of cells. Every cell is part of exactly one TableRow .



---

# TableRule_interface

# TableRule interface

Represents a rule. A rule is the line between two cells.



---

# TableSet_interface

# TableSet interface

A TableSet is a collection of one or more TableGrid s, each of which is a rectangular array of TableCell s



---

# TableTilePlex_interface

# TableTilePlex interface

A TableTilePlex is used to represent a table selection. It may contain either a collection of TableRectangle objects or a collection of TableRule objects or both. All of the contents of any one tileplex must be in the same document and must be managed by the same table model.



---

# ToolBarEvent_interface

# ToolBarEvent interface

The ToolBarEvent interface provides specific contextual information associated with ToolBar events.



---

# View_interface

# View interface

The View interface is a subclass of AbstractView , representing a view of an associated Document . (An edit view of a document is represented as a View object.) An Editor frame Window can contain two View s. If a UIEvent is raised for a window, an event listener can use the view attribute of the UIEvent to obtain an object that implements the View interface (not just the AbstractView ).



---

# W3C_AbstractView_interface

# W3C AbstractView interface

The AbstractView interface is defined in the W3C Document Object Model (DOM) Level 2 Views Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Views-20001113 .)

A base interface that all views shall derive from.



---

# W3C_Attr_interface

# W3C Attr interface

The Attr interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The Attr interface represents an attribute in an Element object. Typically the allowable values for the attribute are defined in a document type definition.

Attr objects inherit the Node interface, but since they are not actually child nodes of the element they describe, the DOM does not consider them part of the document tree. Thus, the Node attributes parentNode , previousSibling , and nextSibling have a null value for Attr objects. The DOM takes the view that attributes are properties of elements rather than having a separate identity from the elements they are associated with; this should make it more efficient to implement such features as default attributes associated with all elements of a given type. Furthermore, Attr nodes may not be immediate children of a DocumentFragment . However, they can be associated with Element nodes contained within a DocumentFragment . In short, users and implementors of the DOM need to be aware that Attr nodes have some things in common with other objects inheriting the Node interface, but they also are quite distinct.

The attribute's effective value is determined as follows: if this attribute has been explicitly assigned any value, that value is the attribute's effective value; otherwise, if there is a declaration for this attribute, and that declaration includes a default value, then that default value is the attribute's effective value; otherwise, the attribute does not exist on this element in the structure model until it has been explicitly added. Note that the nodeValue attribute on the Attr instance can also be used to retrieve the string version of the attribute's value(s).

In XML, where the value of an attribute can contain entity references, the child nodes of the Attr node may be either Text or EntityReference nodes (when these are in use; see the description of EntityReference for discussion). Because the DOM Core is not aware of attribute types, it treats all attribute values as simple strings, even if the DTD or schema declares them as having tokenized types.



---

# W3C_CDATASection_interface

# W3C CDATASection interface

The CDATASection interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

CDATA sections are used to escape blocks of text containing characters that would otherwise be regarded as markup. The only delimiter that is recognized in a CDATA section is the "]]>" string that ends the CDATA section. CDATA sections cannot be nested. Their primary purpose is for including material such as XML fragments, without needing to escape all the delimiters.

The DOMString attribute of the Text node holds the text that is contained by the CDATA section. Note that this may contain characters that need to be escaped outside of CDATA sections and that, depending on the character encoding ("charset") chosen for serialization, it may be impossible to write out some characters as part of a CDATA section.

The CDATASection interface inherits from the CharacterData interface through the Text interface. Adjacent CDATASection nodes are not merged by use of the normalize method of the Node interface.



---

# W3C_CharacterData_interface

# W3C CharacterData interface

The CharacterData interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The CharacterData interface extends Node with a set of attributes and methods for accessing character data in the DOM. For clarity this set is defined here rather than on each object that uses these attributes and methods. No DOM objects correspond directly to CharacterData , though Text and others do inherit the interface from it. All offsets in this interface start from 0 .

As explained in the DOMString interface, text strings in the DOM are represented in UTF-16, i.e. as a sequence of 16-bit units. In the following, the term 16-bit units is used whenever necessary to indicate that indexing on CharacterData is done in 16-bit units.



---

# W3C_CharacterDataEditVAL_interface

# W3C CharacterDataEditVAL interface

The CharacterDataEditVAL interface is defined in the W3C Document Object Model (DOM) Level 3 Validation Specification. (Refer to http://www.w3.org/TR/DOM-Level-3-Val .)

This interface extends the NodeEditVAL interface with additional methods for document editing. An object implementing this interface must also implement CharacterData interface. When validating CharacterData nodes, the NodeEditVAL.nodeValidity operation must find the nearest parent node in order to do this; if no parent node is found, VAL_UNKNOWN is returned. In addition, when VAL_INCOMPLETE is passed in as an argument to the NodeEditVAL.nodeValidity operation to operate on such nodes, the operation considers all the text and not just some of it.



---

# W3C_Comment_interface

# W3C Comment interface

The Comment interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

This interface inherits from CharacterData and represents the content of a comment, i.e., all the characters between the starting ' <!-- ' and ending ' --> '. Note that this is the definition of a comment in XML, and, in practice, HTML, although some HTML tools may implement the full SGML comment structure.



---

# W3C_Document_interface

# W3C Document interface

The Document interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The Document interface represents the entire HTML or XML document. Conceptually, it is the root of the document tree, and provides the primary access to the document's data.

Since elements, text nodes, comments, processing instructions, etc. cannot exist outside the context of a Document , the Document interface also contains the factory methods needed to create these objects. The Node objects created have a ownerDocument attribute which associates them with the Document within whose context they were created.



---

# W3C_DocumentEditVAL_interface

# W3C DocumentEditVAL interface

The DocumentEditVAL interface is defined in the W3C Document Object Model (DOM) Level 3 Validation Specification. (Refer to http://www.w3.org/TR/DOM-Level-3-Val .)

This interface extends the NodeEditVAL interface with additional methods for document editing. An object implementing this interface must also implement the Document interface.



---

# W3C_DocumentEvent_interface

# W3C DocumentEvent interface

The DocumentEvent interface is defined in the W3C Document Object Model (DOM) Level 2 Events Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113 .)

The DocumentEvent interface provides a mechanism by which the user can create an Event of a type supported by the implementation. It is expected that the DocumentEvent interface will be implemented on the same object which implements the Document interface in an implementation which supports the Event model.



---

# W3C_DocumentFragment_interface

# W3C DocumentFragment interface

The DocumentFragment interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

DocumentFragment is a "lightweight" or "minimal" Document object. It is very common to want to be able to extract a portion of a document's tree or to create a new fragment of a document. Imagine implementing a user command like cut or rearranging a document by moving fragments around. It is desirable to have an object which can hold such fragments and it is quite natural to use a Node for this purpose. While it is true that a Document object could fulfill this role, a Document object can potentially be a heavyweight object, depending on the underlying implementation. What is really needed for this is a very lightweight object. DocumentFragment is such an object.

Furthermore, various operations -- such as inserting nodes as children of another Node -- may take DocumentFragment objects as arguments; this results in all the child nodes of the DocumentFragment being moved to the child list of this node.

The children of a DocumentFragment node are zero or more nodes representing the tops of any sub-trees defining the structure of the document. DocumentFragment nodes do not need to be well-formed XML documents (although they do need to follow the rules imposed upon well-formed XML parsed entities, which can have multiple top nodes). For example, a DocumentFragment might have only one child and that child node could be a Text node. Such a structure model represents neither an HTML document nor a well-formed XML document.

When a DocumentFragment is inserted into a Document (or indeed any other Node that may take children) the children of the DocumentFragment and not the DocumentFragment itself are inserted into the Node . This makes the DocumentFragment very useful when the user wishes to create nodes that are siblings; the DocumentFragment acts as the parent of these nodes so that the user can use the standard methods from the Node interface, such as insertBefore and appendChild .



---

# W3C_DocumentRange_interface

# W3C DocumentRange interface

The DocumentRange interface is defined in the W3C Document Object Model (DOM) Level 2 Traversal and Range Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Traversal-Range-20001113 .)



---

# W3C_DocumentType_interface

# W3C DocumentType interface

The DocumentType interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

Each Document has a doctype attribute whose value is either null or a DocumentType object. The DocumentType interface in the DOM Core provides an interface to the list of entities that are defined for the document, and little else because the effect of namespaces and the various XML schema efforts on DTD representation are not clearly understood as of this writing.

The DOM Level 2 doesn't support editing DocumentType nodes.



---

# W3C_DocumentView_interface

# W3C DocumentView interface

The DocumentView interface is defined in the W3C Document Object Model (DOM) Level 2 Views Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Views-20001113 .)

The DocumentView interface is implemented by Document objects in DOM implementations supporting DOM Views. It provides an attribute to retrieve the default view of a document.



---

# W3C_DOMConfiguration_interface

# W3C DOMConfiguration interface

The DOMConfiguration interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The DOMConfiguration interface represents the configuration of a document and maintains a table of recognized parameters. Using the configuration, it is possible to change Document.normalizeDocument() behavior, such as replacing the CDATASection nodes with Text nodes or specifying the type of the schema that must be used when the validation of the Document is requested. DOMConfiguration objects are also used in [ DOM Level 3 Load and Save ] in the DOMParser and DOMSerializer interfaces.

The parameter names used by the DOMConfiguration object are defined throughout the DOM Level 3 specifications. Names are case-insensitive. To avoid possible conflicts, as a convention, names referring to parameters defined outside the DOM specification should be made unique. Because parameters are exposed as properties in the , names are recommended to follow the section 5.16 Identifiers of [ Unicode ] with the addition of the character '-' (HYPHEN-MINUS) but it is not enforced by the DOM implementation. DOM Level 3 Core Implementations are required to recognize all parameters defined in this specification. Some parameter values may also be required to be supported by the implementation. Refer to the definition of the parameter to know if a value must be supported or not.

The following list of parameters defined in the DOM:

The resolution of the system identifiers associated with entities is done using Document.documentURI . However, when the feature "LS" defined in [ DOM Level 3 Load and Save ] is supported by the DOM implementation, the parameter "resource-resolver" can also be used on DOMConfiguration objects attached to Document nodes. If this parameter is set, Document.normalizeDocument() will invoke the resource resolver instead of using Document.documentURI .



---

# W3C_DOMException_exception

# W3C DOMException exception

The DOMException interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

DOM operations only raise exceptions in "exceptional" circumstances, i.e., when an operation is impossible to perform (either for logical reasons, because data is lost, or because the implementation has become unstable). In general, DOM methods return specific error values in ordinary processing situations, such as out-of-bound errors when using NodeList .

Implementations should raise other exceptions under other circumstances. For example, implementations should raise an implementation-dependent exception if a null argument is passed when null was not expected.

Some languages and object systems do not support the concept of exceptions. For such systems, error conditions may be indicated using native error reporting mechanisms. For some bindings, for example, methods may return error codes similar to those listed in the corresponding method descriptions.

Objects that implement the DOMException interface include the following property:



---

# W3C_DOMImplementation_interface

# W3C DOMImplementation interface

The DOMImplementation interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The DOMImplementation interface provides a number of methods for performing operations that are independent of any particular instance of the document object model.



---

# W3C_DOMStringList_interface

# W3C DOMStringList interface

The DOMStringList interface is defined in the W3C Document Object Model (DOM) Level 3 Core Specification. (Refer to http://www.w3.org/TR/DOM-Level-3-Core .)

The DOMStringList interface provides the abstraction of an ordered collection of DOMString values, without defining or constraining how this collection is implemented. The items in the DOMStringList are accessible via an integral index, starting from 0.



---

# W3C_Element_interface

# W3C Element interface

The Element interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The Element interface represents an element in an HTML or XML document. Elements may have attributes associated with them; since the Element interface inherits from Node , the generic Node interface attribute attributes may be used to retrieve the set of all attributes for an element. There are methods on the Element interface to retrieve either an Attr object by name or an attribute value by name. In XML, where an attribute value may contain entity references, an Attr object should be retrieved to examine the possibly fairly complex sub-tree representing the attribute value. On the other hand, in HTML, where all attributes have simple string values, methods to directly access an attribute value can safely be used as a convenience.



---

# W3C_ElementEditVAL_interface

# W3C ElementEditVAL interface

The ElementEditVAL interface is defined in the W3C Document Object Model (DOM) Level 3 Validation Specification. (Refer to http://www.w3.org/TR/DOM-Level-3-Val .)

This interface extends the NodeEditVAL interface with additional methods for guided document editing. An object implementing this interface must also implement the Element interface.

This interface also has attributes that are a NameList of elements or attributes which can appear in the specified context. Some schema languages, i.e., W3C XML schema, define wildcards which provide for validation of attribute and element information items dependent on their namespace names but independent of their local names.

To expose wildcards, the NameList returns the values that represent the namespace constraint:

- • {namespaceURI, name} is {null, ##any} if any;

- • {namespaceURI, name} is {namespace_a, ##other} if not and a namespace name (namespace_a);

- • {namespaceURI, name} is {null, ##other} if not and absent;

- • Pairs of {namespaceURI, name} with values {a_namespaceURI | null, null} if a set whose members are either namespace names or absent.



---

# W3C_Entity_interface

# W3C Entity interface

The Entity interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

This interface represents an entity, either parsed or unparsed, in an XML document. Note that this models the entity itself not the entity declaration. Entity declaration modeling has been left for a later Level of the DOM specification.

The nodeName attribute that is inherited from Node contains the name of the entity.

An XML processor may choose to completely expand entities before the structure model is passed to the DOM; in this case there will be no EntityReference nodes in the document tree.

XML does not mandate that a non-validating XML processor read and process entity declarations made in the external subset or declared in external parameter entities. This means that parsed entities declared in the external subset need not be expanded by some classes of applications, and that the replacement value of the entity may not be available. When the replacement value is available, the corresponding Entity node's child list represents the structure of that replacement text. Otherwise, the child list is empty.

The DOM Level 2 does not support editing Entity nodes; if a user wants to make changes to the contents of an Entity , every related EntityReference node has to be replaced in the structure model by a clone of the Entity 's contents, and then the desired changes must be made to each of those clones instead. Entity nodes and all their descendants are readonly.

An Entity node does not have any parent.



---

# W3C_EntityReference_interface

# W3C EntityReference interface

The EntityReference interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

EntityReference objects may be inserted into the structure model when an entity reference is in the source document, or when the user wishes to insert an entity reference. Note that character references and references to predefined entities are considered to be expanded by the HTML or XML processor so that characters are represented by their Unicode equivalent rather than by an entity reference. Moreover, the XML processor may completely expand references to entities while building the structure model, instead of providing EntityReference objects. If it does provide such objects, then for a given EntityReference node, it may be that there is no Entity node representing the referenced entity. If such an Entity exists, then the subtree of the EntityReference node is in general a copy of the Entity node subtree. However, this may not be true when an entity contains an unbound namespace prefix. In such a case, because the namespace prefix resolution depends on where the entity reference is, the descendants of the EntityReference node may be bound to different namespace URIs.

As for Entity nodes, EntityReference nodes and all their descendants are readonly.



---

# W3C_Event_interface

# W3C Event interface

The Event interface is defined in the W3C Document Object Model (DOM) Level 2 Events Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113 .)

The Event interface is used to provide contextual information about an event to the handler processing the event. An object which implements the Event interface is generally passed as the first parameter to an event handler. More specific context information is passed to event handlers by deriving additional interfaces from Event which contain information directly relating to the type of event they accompany. These derived interfaces are also implemented by the object passed to the event listener.



---

# W3C_EventException_exception

# W3C EventException exception

The EventException interface is defined in the W3C Document Object Model (DOM) Level 2 Events Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113 .)

Event operations may throw an EventException as specified in their method descriptions.

Objects that implement the EventException interface include the following property:



---

# W3C_EventListener_interface

# W3C EventListener interface

The EventListener interface is defined in the W3C Document Object Model (DOM) Level 2 Events Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113 .)

The EventListener interface is the primary method for handling events. Users implement the EventListener interface and register their listener on an EventTarget using the AddEventListener method. The users should also remove their EventListener from its EventTarget after they have completed using the listener.

When a Node is copied using the cloneNode method the EventListener s attached to the source Node are not attached to the copied Node . If the user wishes the same EventListener s to be added to the newly created copy the user must add them manually.



---

# W3C_EventTarget_interface

# W3C EventTarget interface

The EventTarget interface is defined in the W3C Document Object Model (DOM) Level 2 Events Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113 .)

The EventTarget interface is implemented by all Nodes in an implementation which supports the DOM Event Model. Therefore, this interface can be obtained by using binding-specific casting methods on an instance of the Node interface. The interface allows registration and removal of EventListeners on an EventTarget and dispatch of events to that EventTarget .



---

# W3C_ExceptionVAL_exception

# W3C ExceptionVAL exception

The ExceptionVAL interface is defined in the W3C Document Object Model (DOM) Level 3 Validation Specification. (Refer to http://www.w3.org/TR/DOM-Level-3-Val .)

Some Validation operations may throw an ExceptionVAL as described in their descriptions.

Objects that implement the ExceptionVAL interface include the following property:



---

# W3C_MouseEvent_interface

# W3C MouseEvent interface

The MouseEvent interface is defined in the W3C Document Object Model (DOM) Level 2 Events Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113 .)

The MouseEvent interface provides specific contextual information associated with Mouse events.

The detail attribute inherited from UIEvent indicates the number of times a mouse button has been pressed and released over the same screen location during a user action. The attribute value is 1 when the user begins this action and increments by 1 for each full sequence of pressing and releasing. If the user moves the mouse between the mousedown and mouseup the value will be set to 0, indicating that no click is occurring.

In the case of nested elements mouse events are always targeted at the most deeply nested element. Ancestors of the targeted element may use bubbling to obtain notification of mouse events which occur within its descendent elements.



---

# W3C_MutationEvent_interface

# W3C MutationEvent interface

The MutationEvent interface is defined in the W3C Document Object Model (DOM) Level 2 Events Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113 .)

The MutationEvent interface provides specific contextual information associated with Mutation events.



---

# W3C_NamedNodeMap_interface

# W3C NamedNodeMap interface

The NamedNodeMap interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

Objects implementing the NamedNodeMap interface are used to represent collections of nodes that can be accessed by name. Note that NamedNodeMap does not inherit from NodeList ; NamedNodeMaps are not maintained in any particular order. Objects contained in an object implementing NamedNodeMap may also be accessed by an ordinal index, but this is simply to allow convenient enumeration of the contents of a NamedNodeMap , and does not imply that the DOM specifies an order to these Nodes.

NamedNodeMap objects in the DOM are live.



---

# W3C_NameList_interface

# W3C NameList interface

The NameList interface is defined in the W3C Document Object Model (DOM) Level 3 Core Specification. (Refer to http://www.w3.org/TR/DOM-Level-3-Core .)

The NameList interface provides the abstraction of an ordered collection of parallel pairs of name and namespace values (which could be null values), without defining or constraining how this collection is implemented. The items in the NameList are accessible via an integral index, starting from 0.



---

# W3C_Node_interface

# W3C Node interface

The Node interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The Node interface is the primary datatype for the entire Document Object Model. It represents a single node in the document tree. While all objects implementing the Node interface expose methods for dealing with children, not all objects implementing the Node interface may have children. For example, Text nodes may not have children, and adding children to such nodes results in a DOMException being raised.

The attributes nodeName , nodeValue and attributes are included as a mechanism to get at node information without casting down to the specific derived interface. In cases where there is no obvious mapping of these attributes for a specific nodeType (e.g., nodeValue for an Element or attributes for a Comment ), this returns null . Note that the specialized interfaces may contain additional and more convenient mechanisms to get and set the relevant information.

The values of nodeName , nodeValue , and attributes vary according to the node type as follows:



---

# W3C_NodeEditVAL_interface

# W3C NodeEditVAL interface

The NodeEditVAL interface is defined in the W3C Document Object Model (DOM) Level 3 Validation Specification. (Refer to http://www.w3.org/TR/DOM-Level-3-Val .)

This interface is similar to the [ DOM Level 3 Core ] Node interface, with methods for guided document editing.



---

# W3C_NodeList_interface

# W3C NodeList interface

The NodeList interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The NodeList interface provides the abstraction of an ordered collection of nodes, without defining or constraining how this collection is implemented. NodeList objects in the DOM are live.

The items in the NodeList are accessible via an integral index, starting from 0.



---

# W3C_Notation_interface

# W3C Notation interface

The Notation interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

This interface represents a notation declared in the DTD. A notation either declares, by name, the format of an unparsed entity (see section 4.7 of the XML 1.0 specification [ XML 1.0 ]), or is used for formal declaration of processing instruction targets (see section 2.6 of the XML 1.0 specification [ XML 1.0 ]). The nodeName attribute inherited from Node is set to the declared name of the notation.

The DOM Level 1 does not support editing Notation nodes; they are therefore readonly.

A Notation node does not have any parent.



---

# W3C_ProcessingInstruction_interface

# W3C ProcessingInstruction interface

The ProcessingInstruction interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The ProcessingInstruction interface represents a " processing instruction", used in XML as a way to keep processor-specific information in the text of the document.



---

# W3C_Range_interface

# W3C Range interface

The Range interface is defined in the W3C Document Object Model (DOM) Level 2 Traversal and Range Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Traversal-Range-20001113 .)



---

# W3C_RangeException_exception

# W3C RangeException exception

The RangeException interface is defined in the W3C Document Object Model (DOM) Level 2 Traversal and Range Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Traversal-Range-20001113 .)

Range operations may throw a RangeException as specified in their method descriptions.

Objects that implement the RangeException interface include the following property:



---

# W3C_Text_interface

# W3C Text interface

The Text interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The Text interface inherits from CharacterData and represents the textual content (termed character data in XML) of an Element or Attr . If there is no markup inside an element's content, the text is contained in a single object implementing the Text interface that is the only child of the element. If there is markup, it is parsed into the information items (elements, comments, etc.) and Text nodes that form the list of children of the element.

When a document is first made available via the DOM, there is only one Text node for each block of text. Users may create adjacent Text nodes that represent the contents of a given element without any intervening markup, but should be aware that there is no way to represent the separations between these nodes in XML or HTML, so they will not (in general) persist between DOM editing sessions. The normalize() method on Node merges any such adjacent Text objects into a single node for each block of text.



---

# W3C_TypeInfo_interface

# W3C TypeInfo interface

The TypeInfo interface is defined in the W3C Document Object Model (DOM) Level 2 Core Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113 .)

The TypeInfo interface represent a type referenced from Element or Attr nodes, specified in the schemas associated with the document. The type is a pair of a namespace URI and name properties, and depends on the document's schema.

If the document's schema is an XML DTD [ XML 1.0 ], the values are computed as follows:

- • If this type is referenced from an Attr node, typeNamespace is null and typeName represents the [attribute type] property in the [ XML Information Set ]. If there is no declaration for the attribute, typeName is null .

- • If this type is referenced from an Element node, the typeNamespace and typeName are null .

If the document's schema is an XML Schema [ XML Schema Part 1 ], the values are computed as follows using the post-schema-validation infoset contributions (also called PSVI contributions):

- • If the [validity] property exists AND is "invalid" or "notKnown": the {target namespace} and {name} properties of the declared type if available, otherwise null .

- • If the [validity] property exists and is "valid":



---

# W3C_UIEvent_interface

# W3C UIEvent interface

The UIEvent interface is defined in the W3C Document Object Model (DOM) Level 2 Events Specification. (Refer to http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113 .)

The UIEvent interface provides specific contextual information associated with User Interface events.



---

# Window_interface

# Window interface

The Window interface represents a top level window frame which is created by Editor.



---

# WindowEvent_interface

# WindowEvent interface

The WindowEvent interface provides specific contextual information associated with Window events.



---

# WindowException_exception

# WindowException exception

Window operations may throw a WindowException as specified in their method descriptions.

Objects that implement the WindowException interface include the following property: