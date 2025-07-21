

---

# Characteristics_of_the_ActiveX_Arbortext_Editor

Since the ActiveX version of Arbortext Editor is contained inside of some other window, it has somewhat different functionality than the regular Arbortext Editor window. The ActiveX Arbortext Editor has the following differences from the regular Arbortext Editor :

- • No title bar — Only the window hosting the Arbortext Editor ActiveX control can have a title bar.

- • Does not appear in the Microsoft Windows taskbar — Only the window hosting the Arbortext Editor ActiveX control can appear on the taskbar.

- • Does not appear in the Microsoft Windows ALT+TAB window sequence — Only the window hosting the Arbortext Editor ActiveX control can appear in this sequence.

- • Might not be resizable — The window hosting the Arbortext Editor ActiveX control determines whether the control can be resized.

The ActiveX Arbortext Editor has the following user interface differences from the regular window:

- • The Arbortext Editor menus are available from a toolbar button.

- • The following menu choices (and associated keyboard shortcuts) are not available:

- • The following toolbar buttons are not available:



---

# close_Method

Closes any open document after first prompting to save any changes (if it was modified).

## Related topics

- • Integrating Arbortext Editor with web pages



---

# HRESULT_Return_Values

Each method in the control’s COM interface returns one of the following HRESULT values:

- • S_OK — Operation successful

- • 0x800704C7 — Operation canceled by user

- • E_FAIL — Unexpected failure



---

# open_Method

Opens a resource as a Arbortext Editor document and displays it in the ActiveX embedded Arbortext Editor window. This method first closes the current document (if any) and prompts the user to save it (if modified). Note that at the Save prompt, the user might Cancel the operation. In this case, the current document is left intact and this method returns an error.

If you do not want the user to see a Save prompt, then you can call the close method to close the current document explicitly before calling the open method. Note that you can suppress all informational windows during an open operation by specifying the 0x0020 value for the documentFlags parameter.



---

# show_Method

Opens an existing resource based on its ACL document ID as a Arbortext Editor document and displays it in the ActiveX embedded Arbortext Editor window. In contrast to the open method, the show method enables you to dynamically create an in-memory document that might not have been saved at all and display it in the ActiveX embedded window.

This method first closes the current document (if any) and prompts the user to save it (if modified). Note that at the Save prompt, the user might Cancel the operation. In this case, the current document is left intact and this method returns an error.

If you do not want the user to see a Save prompt, then you can call the close method to close the current document explicitly before calling the show method.



---

# The_EditorControl.dll_Control

The Arbortext Editor ActiveX control is contained in the EditorControl.dll file. The control has the following names when viewed with the Microsoft OLE/COM Object Viewer ( Oleview.exe ) application:

- • Arbortext.EditorControl — The ProgID for the control

- • Arbortext Editor Control — The name in the Object Classes/All Objects group

- • Arbortext Editor Control Type Library — The name in the Type Libraries group

- • IArbortextEditorControl — The name in the Interfaces group

Following is the Interface Definition Language (IDL) definition for the control’s COM interface:

```
interface IArbortextEditorControl : IDispatch{
[id(1), helpstring("Opens a new document after first closing the currently-displayed document (if any).")]
HRESULT open(
[in] BSTR documentPath,
[in,defaultvalue(0)] LONG documentFlags,
[in,defaultvalue(0)] LONG windowFlags,
[in,defaultvalue("")] BSTR xuiPath,
[out, retval] LONG* pWindowId
);
[id(2), helpstring("Displays an already-open document after first closing the currently-displayed document (if any).")]
HRESULT show(
[in] LONG documentId,
[in,defaultvalue(0)] LONG windowFlags,
[in,defaultvalue("")] BSTR xuiPath,
[out, retval] LONG* pWindowId
);
[id(3), helpstring("Closes the currently-displayed document and, by default, prompts to save changes.")]
HRESULT close([in,defaultvalue(0)] LONG flags);
};
```