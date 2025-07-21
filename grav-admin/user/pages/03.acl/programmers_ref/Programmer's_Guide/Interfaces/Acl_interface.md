

---

# DOMDocument_method

Returns the DOM Document object corresponding to an Arbortext document ID. The desired document must be open in Arbortext Editor or Arbortext Publishing Engine before calling this method, but the document does not need to be visible in a window. Developers can obtain the document identifier they need by using the Eval method to call an ACL function such as current_doc .



---

# DOMOID_method

Returns the DOM Node associated with the supplied ACL object identifier oid .

This method is useful for creating a DOM node object from a portion of a document instead of the entire document. The desired document must be open in Arbortext Editor or Arbortext Publishing Engine before calling this method. The object identifier oid can be obtained by using the Eval method to call an ACL function such as oid_caret .



---

# Eval_method

Evaluates a string as an ACL expression and returns the result of the evaluation as a string. The string to evaluate must contain an expression. For example:

```
2+2
```

or

```
tbl_oid_cell(oid_caret(),oid_caret_pos())
```

Variable substitution in the expression string occurs on the ACL side of the AOM interface, not on the client side. You can include ACL variables in the expression string. However, do not include variables native to the client program.



---

# Execute_method

Executes a string as an ACL command. The return value varies depending on the interface.

Variable substitution in the expression string occurs on the ACL side of the AOM interface and not on the client side. You can include ACL variables in the expression string. However, do not include variables native to the client program.



---

# GetCMSObject_method

Returns a CMSObject object equivalent to the given ACL dobj id.



---

# GetCMSSession_method

Returns the CMSSession object associated with the given ACL session id.

This does not support the default (file-system) session id value of 0 .



---

# GetVar_method

Returns the value of an ACL scalar variable as a string.



---

# GetWindow_method

Returns the AOM Window object corresponding to an Arbortext window ID. Developers can obtain the window identifier they need by using the Eval method to call an ACL function such as current_window .



---

# SetVar_method

Sets the value of an ACL scalar variable to the specified string.