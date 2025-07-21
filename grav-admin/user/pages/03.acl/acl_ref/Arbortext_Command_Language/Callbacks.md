

---

# channel_set_callback

# channel_set_callback

channel_set_callback ( ch , funcname [, data ])

This function sets the specified function funcname as a callback to be invoked whenever certain events are detected on the network channel ch . ch is a channel identifier returned by open_connect or open_accept . The optional argument data is evaluated and its value is passed to the specified callback function.

Calling channel_set_callback automatically sets the channel ch to non-blocking mode.

The callback function must be declared as:

```
function
funcname(ch, op[, data])
```

where ch is the channel identifier, data is the user data argument passed to channel_set_callback , and op is the integer specifying the type of notification.

- • 0 — the channel was opened. This notification is actually given when data are first available for reading and allows the callback to initialize its state.

- • 1 — the channel was closed. Note, that if read returns 0 when called on a read (op=2) notification, Arbortext Editor gives a close notification instead of returning 0 from read .

- • 2 — the channel is ready for reading (that is, there is more incoming data).

The callback must call read (or getline if appropriate) on a read notification to read data from channel. The callback cannot be invoked again until after a read is performed. The callback can call read more than once on a single notification, but must be prepared to deal with a partial or incomplete read.

The callback is automatically removed when the channel is closed.

The sample function that follows uses open_connect and channel_set_callback to fetch an HTML document from an HTTP server (well known port 80). For clarity, it does minimal error checking and does not deal with the MIME headers that are normally transmitted preceding the actual document. Unlike the similar example given with open_connect , this uses channel_set_callback to read from channel in a non-blocking manner (that is, the user function ch_notify gets called only when data are available on the channel).

```
function http_async_get(host, path, lclfile) {
local of = open(lclfile, "wb")
if (of < 0) {
message "http_get: couldn't open $lclfile for write"
return 0;
}
local ch = open_connect(host, 80)
if (ch < 0) {
message "http_get: $main::api_error"
return 0;
}
channel_set_callback(ch, "ch_notify", of)
write(ch, "GET " . path . " HTTP/1.0\r\n\r\n")
return ch
}
function ch_notify(ch, what, of)
{
switch (what) {
case 0: # open
# could open the output file here
break;
case 1: #close
close(ch)
close(of)
break;
case 2: # read
local buf, len
len = read(ch, buf, 512)
switch (len) {
case -2: # read would block
return;
case -1: # unexpected error
message "ch_notify: $main::api_error"
# fall through
case 0: # connection was closed
# note, by closing CH here this callback
# gets removed so that we won't get a
# subsequent close notification (1).
close(of)
close(ch)
break
default:
write(of, buf, len)
}
}
}
```

## Related Topics

- • getline built-in function

- • open_accept built-in function

- • open_connect built-in function

- • read built-in function



---

# dlgitem_add_callback

# dlgitem_add_callback

dlgitem_add_callback ( window dlgitem , callback [, "PREPEND" ])

Appends callback to the list of callback functions to be called when the value of dlgitem within window changes. Functions are called in the order that they appear in the list. If successful, the function returns 1 (one).

dlgitem_add_callback has the following parameters:

- • window — The window identifier. If window is invalid, $ERROR is set and 0 is returned.

- • dlgitem — The value of the control's id attribute. If dlgitem does not exist within window, $ERROR is set and 0 is returned.

- • callback — Specifies the actual callback to add. If callback is already on the callback list for the dialog item, the list is reordered to place the callback in the new position. The callback is not added to the list a second time.

- • "PREPEND" — Optional. When specified, the callback is added to the beginning of the list of callback functions.

Three different events are associated with dialog items:

- • ITEM_CHANGED

- • ITEM_FOCUSED

- • ITEM_UNFOCUSED

The callback is called if any of these events occurs. For example, clicking on a button may generate two callbacks, once when the button takes focus, and again when clicked (that is, changed). Therefore, it is a good practice for your callback function to execute only if the desired event has occurred. Otherwise, it should simply return.

Example:

```
$ret = dlgitem_add_callback($win, "TextField",
main::TextFieldCallback);
```

Callback prototype:

```
callback(windowId, dialogItem, eventType, eventSubType, detail)
```

Arguments:

- • windowId — The identifier of the window that contains this dialog item.

- • dialogItem — The value of the dialog item's ID attribute.

- • eventType — One of the following three types.

- • eventSubType — Applies only when eventType is "ITEM_CHANGED" . The following controls have the following eventSubType values:

- • detail — Applies only when eventType is "ITEM_CHANGED" and eventSubType is "CLOSED" . If the combobox dropdown is closed using the ESC key, the value of detail is CANCEL . If the combobox dropdown is closed by other means, detail is an empty string.



---

# dlgitem_remove_callback

# dlgitem_remove_callback

dlgitem_remove_callback ( window , dlgitem , callback )

Removes callback from the list of functions called when the value of dlgitem within window changes value. If window is invalid or dlgitem does not exist within window , or callback is not on the callback list for the dialog item, $ERROR is set and 0 is returned. If successful, the function returns a one ( 1 ).

The window parameter is a window identifier. dlgitem is the value of the control's id attribute. The callback parameter specifies the actual callback to remove.

Example

```
$ret = dlgitem_remove_callback($win, "TextField",
main::TextFieldCallback)
```



---

# doc_add_callback

# doc_add_callback

Appends callbacks to the list of callback functions to be called when a particular document-level event occurs. Two lists of callbacks are maintained for each callback type, one is document specific and the other is global (applies to all documents).

The doc parameter is a document identifier or zero ( 0 ). Using a value of zero adds the callback globally (for all documents). The cbtype parameter is the name of a callback type. The callback parameter specifies the callback function to add. The "PREPEND" flag causes the callback to placed at the beginning rather than the end of the list. Callback functions are called in the order that they appear on the list, global callbacks are called first, followed by document specific callbacks.

If doc is invalid, $ERROR is set and 0 is returned. If successful, the function returns a unique positive document identifier.

Refer to Callback Functions introduction for helpful overview information. Also, refer to the following valid document callback types:



---

# doc_remove_callback

# doc_remove_callback

doc_remove_callback ( doc , cbtype , callback )

Removes callback from the list of functions called when a document-level event occurs. If doc is invalid, or callback is not on the callback list for the document, $ERROR is set and 0 is returned. If successful, the function returns the unique document identifier.

The doc parameter is a document identifier. The cbtype parameter needs to be a valid callback type (valid callbacks are listed under the doc_add_callback function). The callback parameter specifies the actual callback to remove.

Example

```
$ret = doc_remove_callback($doc, "create", \
"main::DocCallback")
```

Refer to Callback Functions introduction for helpful overview information.

## Related Topics

- • doc_add_callback window function



---

# session_add_callback

# session_add_callback

session_add_callback ( cbtype , callback [, "PREPEND" ])

Appends callback to the list of callback functions to be called when desired session-level event occurs. If "PREPEND" is specified, the callback is prepended to the list of callback functions. Functions are called in the order that they appear in the list.

The cbtype parameter needs to be a valid callback type. If cbtype is invalid, the function returns 0 . If it's successful, the function returns 1 .

The callback parameter specifies the actual callback to add. The "PREPEND" flag specifies that the callback should be prepended, not appended.

Refer to Callback Functions introduction for helpful overview information.

Refer to the following valid session callback types.



---

# session_remove_callback

# session_remove_callback

session_remove_callback ( cbtype , callback )

Removes callback from the list of functions called when a session-level event occurs. The callback parameter specifies the callback to remove.

The cbtype parameter needs to be a valid callback type (valid callbacks are listed under the session_add_callback function). If callback is not on the callback list for the session or if cbtype is invalid, the function returns 0 . If it's successful, the function returns 1 .

Example

```
$ret = session_remove_callback("quit", main:: DocCallback)
```

## Related Topics

- • session_add_callback function



---

# timer_add_callback

# timer_add_callback

timer_add_callback ( csecs , callback [, data ])

This function creates an interval timer and returns an identifier for it. csecs is the time interval in centiseconds (hundredths of a second). callback is the name of the function to be called when the interval timer expires. data is an optional user data value that is passed to the callback.

The callback function must be declared as:

```
function
callback
([
data
])
```

and must return either 0 to cancel the timer or 1 to reenable it.

Due to the overhead of executing Arbortext Command Language code, time interval values of less than one-tenth of a second are not recommended.

In the example that follows, the timer_add_callback function displays the current time on the status bar (which is updated once per second for a minute).

```
global nticks=0
function update_clock(win)
{
if (++nticks == 60) {
window_set(win, 'message', '')
return 0; # cancel timer
}
window_set(win, 'message', substr(time_date(), 12, 8))
return 1; # reenable timer
}
timer_add_callback(100, 'update_clock', doc_window())
```



---

# timer_remove_callback

# timer_remove_callback

timer_remove_callback ( id )

This function cancels the interval timer specified by id , which is an identifier returned by a previous call to timer_add_callback . Note that the timer can also be cancelled in the callback function by returning 0 .

## Related Topics

- • timer_add_callback built-in function



---

# userule_add_callback

# userule_add_callback

userule_add_callback ( docid , userule , userule_func )

This function registers userules for document types. userule_add_callback is called when the specified userule(s) and document type(s) need processing. userule_add_callback returns 0 if successful. The function returns -1 on registration failure.

The current registration of ( docid , userule , userule_func ) overrides any existing registration.

- • docid — The document identier of a document using the document type. Setting docid to 0 registers the userule for all document types.

- • userule — The userule number. Setting userule to 0 registers all userules for the document type. Setting userule to a value greater than 2 specifies a particular userule.

- • userule_func — The userule function.

## Related Topics

- • userule_remove_callback function



---

# userule_remove_callback

# userule_remove_callback

userule_remove_callback ( docid , userule , userule_func )

This function unregisters userules for document types. userule_remove_callback returns 0 if successful. The function returns -1 on failure.

- • docid — The document identier of a document using the document type. Setting docid to 0 unregisters the userule for all document types.

- • userule — The userule number. Setting userule to 0 unregisters all userules for the document type. Setting userule to a value greater than 2 specifies a particular userule.

- • userule_func — The userule function.

## Related Topics

- • userule_add_callback function



---

# window_add_callback

# window_add_callback

window_add_callback ( window , cbtype , callback [, "PREPEND" ])

Appends callback to the list of callback functions to be called when the value of a dialog box item within window changes, or when another window-level event occurs. If "PREPEND" is specified, the callback is prepended to the list of callback functions instead. Functions are called in the order that they appear in the list. If window is invalid, $ERROR is set and 0 is returned. If successful, the function returns the unique window identifier.

The window parameter is a window identifier. A valid window identifier must be specified. (A value of 0 specifies “all windows”.) The cbtype parameter needs to be a valid callback type. (Refer to the following list of Valid window callback types .) The callback parameter specifies the actual callback to add. The "PREPEND" flag specifies that the callback should be prepended, not appended.

Refer to window_set and Callback Functions introduction for related information.

Refer to the following valid window callback types.



---

# window_remove_callback

# window_remove_callback

window_remove_callback ( window , cbtype , callback )

Removes callback from the list of functions called when the value of a dialog item within window changes value, or when another window-level event occurs. If window is invalid, or callback is not on the callback list for the window, $ERROR is set and 0 is returned. If successful, the function returns the unique window identifier.

The window parameter is a window identifier. The cbtype parameter needs to be a valid callback type (valid callbacks are listed under the window_add_callback function). The callback parameter specifies the actual callback to remove.

Example

```
$ret = window_remove_callback($win, "create", main:: WindowCallback)
```

## Related Topics

- • window_add_callback function