

---

# drop_file

Function prototype:

```
function
funcname
(
path
,
num
,
count
,
flags
)
```

drop_file is called when a drop operation involving one or more files is performed. The default action can be prevented by returning -1 from this callback. For example, if the callback opens or inserts the file(s).

Arguments:

- • path is the path name of the file being dropped.

- • num is the index number of the file being dropped, starting with 1 .

- • count is the number of files being dropped by the operation.

- • flags is bit mask giving information about the drop operation defined below.

If more than one file is being dropped, the callback is called multiple times with the num parameter increased incrementally on each call, until count calls have been made. If the callback returns -1 on any call during a multiple-file drop, then the file associated with that callback is not processed and the next file is called.

The flags parameter may have any of the following bits set:

- • 0x0001 - the SHIFT key is pressed.

- • 0x0002 - the CTRL key is pressed.

- • 0x0004 - the path specifies a graphic file.

- • 0x0008 - the ALT key is pressed.

By default, the CTRL key modifier determines whether a file is opened or inserted. A graphic file (indicated by bit 0x0004 being set) is always inserted.



---

# drop_file_over

Function prototype:

```
function
funcname
(
op
,
count
,
flags
)
```

drop_file_over is called to receive more information on the progress of a drag and drop operation and to provide feedback that will cause different mouse pointers, and possibly a drop cursor, to be displayed or not. The callback might be called multiple times (possibly hundreds of times) for a single drag and drop operation as the mouse pointer moves over the window, so should be written as efficiently as possible.

The drop file operation ends with either a call to the drop_file callback or a final call to the drop_file_over callback indicating that the drag and drop operation has been cancelled or is no longer over the Arbortext Editor window. If multiple drop_file_over callbacks are registered, the first callback that does not return -1 determines what action will be taken. Any remaining callbacks will not be called until the mouse moves.

Arguments:

- • op is an operation code that has the following possible values:

- • count is the number of files being dropped by the operation.

- • flags is a bit mask giving the following information about the drop operation:

The function returns one of the following codes:

- • -1 — Indicates processing should continue.

- • 0 — Indicates that the request is not allowed at this point.

- • 1 — Indicates that the request is allowed and will result in a file open operation that is independent of the mouse position at the time of the drop.

- • 2 — Indicates that a drop at this point will result in an insertion and that a drop insertion cursor should be drawn to show the point of insertion.

## Related Topics

- • drop_file_info function



---

# quit

Function prototype:

```
function
funcname
(
code
,
system
)
```

This quit callback is passed the argument code , which indicates how the application is being exited.

Arguments

- • funcname is the name for the user-defined function called to be invoked whenever the editing session is terminated. This is invoked before any of the built-in save checking is done. If the quit callback returns a value of -1 , no further callbacks will be called and the quit will be canceled. All other returned values are ignored. If the callback is already on the callback list for the session, the list is shuffled to place the callback into the desired position. The callback is not added to the list a second time.

- • code is one of the following values:

- • system is one of the following values:

## Related Topics

- • session_remove_callback function

- • exit command

- • quit command