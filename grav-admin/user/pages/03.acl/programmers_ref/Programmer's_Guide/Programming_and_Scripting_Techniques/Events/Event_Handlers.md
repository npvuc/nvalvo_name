

---

# COM_C++

Much of the COM C++ example was generated automatically using the Insert > New ATL Object menu in the Microsoft Visual C++ IDE followed by Implement Interface on the CListener class added by New ATL Object . This was edited so both the raw methods and the method wrappers were created by the #import statement.

The listener class declaration is:

```
#ifndef __LISTENER_H_
#define __LISTENER_H_
#include "resource.h" // main symbols
#import "epic.exe" raw_native_types, no_namespace, named_guids
class ATL_NO_VTABLE CListener :
public CComObjectRootEx<CComSingleThreadModel>,
public IDispatchImpl<IDOMEventListener,
&IID_IDOMEventListener, &LIBID_Epic>
{
public:
CListener()
{
}
DECLARE_NO_REGISTRY()
DECLARE_PROTECT_FINAL_CONSTRUCT()
BEGIN_COM_MAP(CListener)
COM_INTERFACE_ENTRY(IDispatch)
COM_INTERFACE_ENTRY(IDOMEventListener)
END_COM_MAP()
public:
STDMETHOD(raw_handleEvent)(IDOMEvent * evt);
};
#endif //__LISTENER_H_
```

The listener implementation class is:

```
#include "stdafx.h"
#include "Listener.h"
#include <string>
typedef std::basic_string< unsigned short > DOMString;
STDMETHODIMP CListener::raw_handleEvent( IDOMEvent *rawEvent)
{
IDOMEventPtr pEvent = rawEvent;
IDOMNode3Ptr pNode = pEvent->target;
DOMString context;
while (pNode)
{
if (pNode->nodeType == NODE_ELEMENT)
{
context.insert(0, pNode->nodeName);
context.insert(0, L"(");
}
pNode = pNode->parentNode;
}
_Application3Ptr pEpic(__uuidof(Application));
context += L"\n";
pEpic->Print(_variant_t(context.c_str()));
pEvent->stopPropagation();
return S_OK;
}
```

The method that creates and attaches the listener is:

```
void AttachListener()
{
CListener *pListener = new CComObject<CListener>;
IDOMEventListenerPtr pIntfc;
if (pListener)
{
pListener->QueryInterface(IID_IDOMEventListener,
(void **) &pIntfc);
_Application3Ptr pEpic(__uuidof(Application));
IDOMEventTargetPtr pDocTarget;
pDocTarget = pEpic->ActiveDocument;
pDocTarget->addEventListener(_bstr_t("click"), pIntfc, true);
}
}
```



---

# Java

In Java, it is necessary to cast the Document object to call the addEventListener method of the EventTarget interface. Also, note the event listener parameter is specified using an anonymous inner class.

```
Document doc = Application.getActiveDocument();
((EventTarget)doc).addEventListener("click",
new EventListener() {
public void handleEvent(Event event) {
Node node = (Node)event.getTarget();
String context = "";
while (node != null) {
if (node.getNodeType() == Node.ELEMENT_NODE) {
context = "(" + node.getNodeName() + context;
}
node = node.getParentNode();
}
Application.print(context + "\n");
event.stopPropagation();
}
}, true);
```



---

# JavaScript

JavaScript uses the LiveConnect feature to connect to Java to create the DOM EventListener object to pass to addEventListener . The handler object associated with the EventListener is declared using object literal syntax.

```
function clickEvent(event)
{
var node = event.target;
var context = "";
while (node != null) {
if (node.nodeType == node.ELEMENT_NODE) {
context = "(" + node.nodeName + context;
}
node = node.parentNode;
}
Application.print(context + "\n");
event.stopPropagation();
}
var doc = Application.activeDocument;
// define an object with the required handleEvent method
var o = { handleEvent: clickEvent};
var listener = Packages.org.w3c.dom.events.EventListener(o);
doc.addEventListener("click", listener, true);
```



---

# JScript

In JScript, the EventListener interface is implemented by declaring a constructor of the same name. Note, that because of the way JScript works, the interface constants like Node.ELEMENT_NODE are not available. Otherwise, the clickEvent function is the same as the in the JavaScript example. The main difference is in how the listener object is created.

```
function EventListener( )
{
this.handleEvent = clickEvent;
}
function clickEvent(event)
{
var node = event.target;
var context = "";
while (node != null) {
if (node.nodeType == 1 /*ELEMENT_NODE*/) {
context = "(" + node.nodeName + context;
}
node = node.parentNode;
}
Application.print(context + "\n");
event.stopPropagation();
}
var doc = Application.activeDocument;
var listener = new EventListener();
doc.addEventListener("click", listener, true);
```



---

# VBScript

In VBScript, the event handler is declared as a class:

```
Class EventListener
Public Function handleEvent(ByVal evt)
Dim node
set node = evt.target
Dim context
context = ""
While Not node Is Nothing
If node.nodeType = 1 Then
context = "(" & node.nodeName & context
End If
Set node = node.parentNode
Wend
Application.print(context)
Application.print()
evt.stopPropagation()
handleEvent = 0
End Function
End Class
Dim doc
set doc = Application.activeDocument
Dim listener
set listener = new EventListener
doc.addEventListener "click", listener, true
```



---

# Visual_Basic

In Visual Basic, the event handler is created as a listener class with the following code. Note that Print is a reserved method name in Visual Basic, so the Application.Print method is not available; the VB Debug.Print method is used instead.

```
Option Explicit
Implements IDOMEventListener
Private Sub IDOMEventListener_handleEvent _
(ByVal evt As IDOMEvent)
Dim node As IDOMNode3
Set node = evt.target
Dim context As String
context = ""
While Not node Is Nothing
If node.nodeType = NODE_ELEMENT Then
context = "(" & node.nodeName & context
End If
Set node = node.parentNode
Wend
Debug.Print context
evt.stopPropagation
End Sub
```

Then a Visual Basic form must be created with this code included to register the event listener:

```
Option Explicit
Dim myListener As IDOMEventListener
Dim app As Epic.Application
Dim activeDoc As DOMDocument
Dim target As IDOMEventTarget
Private Sub Form_Load()
Set myListener = New Listener
Set app = New Epic.Application
Set activeDoc = app.ActiveDocument
Set target = activeDoc
target.addEventListener "click", myListener, False
End Sub
```