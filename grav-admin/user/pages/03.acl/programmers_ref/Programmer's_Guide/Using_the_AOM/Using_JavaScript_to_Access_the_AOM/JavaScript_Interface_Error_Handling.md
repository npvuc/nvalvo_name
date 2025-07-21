

---

# Exception_Handling

JavaScript provides exception handling with try/catch statements. Since JavaScript is implemented using the Java interface, it supports all the DOM and AOM exception classes summarized in Java Interface Exceptions and defined in Interface Overview . Most exception classes define a numeric error code attribute named code and message attribute named message . The symbolic names for the error codes listed with each exception interface description are available for the global exception objects listed in JavaScript Global Objects . For example,

```
try {
node.insertBefore(newNode, refNode);
}
catch (e) {
if (e.code == DOMException.NO_MODIFICATION_ALLOWED_ERR) {
Application.alert("Document is read only");
}
else {
Application.alert("Error: " + e.code +
" Message: " + e.message);
}
}
```