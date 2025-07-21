

---

# create_Callback_Type

create is invoked whenever a window is created either by a call to the window_create function or a call internally by Arbortext Editor to create a window.



---

# destroy_Callback_Type

destroy is called whenever a window is deleted. The global destroy hook is called after any local destroyCallback function is set on the window.



---

# notify_Callback_Type

notify is used when you add a callback to a XUI window. It has the following form:

```
callback
(
win
dlgitem
event
data
appdata
)
```

Where:

- • win — The identifier of the window to be removed.

- • dlgitem — The value of the control's id attribute.

- • event — The type of event. It can be one of the following strings:

- • data — User data value that is passed to the callback.

- • appdata — Specifies a value for later reference.



---

# quit_Callback_Type

quit is called when a window is dismissed.

Example

```
function
funcname
(
win
,
code
, op=2)
```

The window identifier, win , can be obtained by calling window_id . The argument code is passed, indicating how the application is being exited.

Arguments

- • win is the identifier of the window to be removed.

- • code is one of the following values:

- • op is the function callback operation. Callbacks are called twice in succession with op specifying the stage of callback operation.

## Related Topics

- • exit command

- • quit command