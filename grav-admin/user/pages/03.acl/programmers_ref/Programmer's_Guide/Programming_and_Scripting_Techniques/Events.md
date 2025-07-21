

---

# Application-Dependent_Features

The DOM Level 2 Events specification defines the DOMFocusIn , DOMFocusOut , and DOMActivate user interface events, but does not define when they will occur. The specification also allows implementation-dependent treatment of the DOMSubtreeModified mutation event. The following table describes when these events occur in Arbortext Editor and the Arbortext Publishing Engine :

Refer to Event Types for a description of each event type.



---

# Event_Handlers

Event handlers are registered in a binding-specific manner. The following sections illustrate the techniques used to implement the EventListener interface for each language binding supported by Arbortext Editor and the Arbortext Publishing Engine .

The example (repeated in each binding) shows how to register a mouse click handler (of the MouseEvents event module) for the active document. The handler prints a line to the message window showing the element hierarchy in the following form each time the mouse is clicked within the document:

```
(book(chapter(para
```



---

# Event_Interfaces

The following tables summarize the DOM Event Model interfaces and the AOM extended event interfaces supported by Arbortext Editor and the Arbortext Publishing Engine .



---

# Event_Modules_and_Domains

The DOM Level 2 Events specification allows an application to support multiple modules of events. Arbortext Editor and the Arbortext Publishing Engine support all of the DOM Level 2 event modules except HTMLEvents . In addition, Arbortext Editor and the Arbortext Publishing Engine add several application-specific event modules and further divide the event modules into the following event domains: CMSObject , CMSSession , CMSAdapter , Document , and Window .

The Document domain includes those events created by the createEvent method of the DocumentEvent interface and used by the EventTarget interface as implemented by the Node interface and its subclasses. The Document domain includes the DOM Level 2 Event modules UIEvents , MouseEvents , and MutationEvents , as well as the Arbortext -specific AEditEvent module. The AEditEvent module defines several event types used to notify programmers of important document operations that are not covered by DOM events.

The Window domain includes those events created by the createEvent method of the Window interface and used by the EventTarget interface as implemented by the Component interface and its subclasses. The Window domain includes the WindowEvents , MenuEvents and ControlEvents modules.

The CMSSession domain includes those events associated with CMS sessions. The target of all events in this domain is a CMSSession . The events in this domain bubble in the following order:

An EventListener may be established on any of these targets.

The CMSObject domain includes those events associated with CMS objects. The target of all events in this domain is a CMSObject . The events in this domain bubble in the following order:

An EventListener may be established on any of these targets.

The CMSAdapter domain includes those events associated with CMS adapters. The target of all events in this domain is a CMSAdapter . The events in this domain bubble in the following order:

An EventListener may be established on both of these targets.

The AEvent interface is the Arbortext extension to the W3C Event interface which adds two attributes to determine the domain and module of the event:

- • domain — returns a constant identifying the event domain

- • moduleType — returns a constant identifying the event module

The following event modules are supported. The module name listed is the feature string to pass as the eventType parameter to the appropriate createEvent method.

Events associated with user interaction with a mouse or keyboard.

Domain: Document

Events associated with mouse input devices.

Domain: Document

Events associated with actions that modify the structure of the document.

Domain: Document

Events associated with high level editing operations.

Domain: Document

Events associated with changes in the state of Window objects.

Domain: Window

Events associated with MenuItem objects.

Domain: Window

Events associated with XUI control objects. These are not currently exposed through the AOM.

Domain: Window

Events associated with CMS objects.

Domain: CMSObject

Events associated with construct operations for existing CMS objects.

Domain: CMSSession

Events associated with creating new CMS objects.

Domain: CMSSession

Events associated with file-related CMS session operations.

Domain: CMSSession

Events associated with burst-related CMS session operations.

Domain: CMSSession

Events associated with CMS session disconnection operations.

Domain: CMSSession

Events associated with CMS adapter connection operations.

Domain: CMSAdapter

Events associated with CMS adapter disconnection operations.

Domain: CMSAdapter



---

# Event_Types

The following sections define the event types supported by each event module and include information about event bubbling, event cancellation, and specific context information for each event type.

The descriptions of the W3C modules ( UIEvent , MouseEvent , and MutationEvent ) in the following sections are taken from the Document Object Model (DOM) Level 2 Events Specification ( www.w3.org/TR/DOM-Level-2-Events ).



---

# Notes_and_Limitations

The following notes and limitations apply to the Arbortext Editor and the Arbortext Publishing Engine implementations of events:

- • Be aware that DOM mutation events trigger after the document is loaded and something happens to change the document, not as the document is being read in by Arbortext Editor or the Arbortext Publishing Engine .

- • HTML-specific features in the W3C DOM Events specification are not implemented.

- • No mutation events are currently fired for undo or redo operations. Instead the AOMUndo event type is dispatched.

- • SGML-specific document structures such as ignored marked sections are not supported by the Arbortext Editor and the Arbortext Publishing Engine DOM implementation.