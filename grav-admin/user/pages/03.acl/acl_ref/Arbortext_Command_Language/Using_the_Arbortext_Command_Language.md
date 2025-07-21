

---

# A_Further_Modification

# A Further Modification

You may want to add another if/else command to the commands shown in the Test the location of a document example. Using the pwd command to print the working directory slows things down a little bit. In some cases, the value of the variable $dirname is already the complete path. You can speed things up in some cases by checking to see whether the value of $dirname is already a complete path and if it is, using it as the value for $workingdir:

```
if (substr($dirname,1,1)=='\') {
$workingdir=$dirname;
} else { $workingdir= `pwd`;}
if (index($wd,'conf')!=0 && $doctype==memo) {
modify_tag -global document \
scilevel=secret;}
```

$dirname is a predefined Arbortext Editor variable. Its value is the name of the current document directory. The initial if/else command uses the substr function to find out whether the directory name begins with a backslash (\). If the name does begin with a backslash, the value of $dirname is a complete path, in which case it can be used as the value for $workingdir. If the name does not begin with a slash, the status of the index function will be 0, the initial if condition will not be true, and the else clause is invoked, calling pwd to get the complete path.



---

# ACL_Coding_for_Better_Generated_Text_Performance

# ACL Coding for Better Generated Text Performance

For a series of complex editing operations the ACL developer should consider temporarily disabling generated text updates before performing the operations and then restoring the previous generated text state when finished. This will maximize performance if gentext is set to on and gentextautoupdate is set to something other than none , as the gentext will only be updated once when all editing operations are complete, instead of incrementally after each edit.

```
function complex_edit() {
local previous_gentext_state = option('gentextautoupdate');
set gentextautoupdate=none;
[...two or more really complex editing functions here...]
set gentextautoupdate=$previous_gentext_state;}
```



---

# ACL_Functions_Defined

# ACL Functions Defined

Functions are different than commands because they return a value that can be assigned to a variable. A function takes arguments that are specified in parentheses directly following the function name. Here is the syntax for a function:

```
$value =
functionname
(
argument1
,
argument2
, . . .)
```

Assigning the value to a variable is not mandatory.



---

# ACL_Syntax_Conventions_for_Quotation_Marks

# ACL Syntax Conventions for Quotation Marks

Either double ( " ) or single ( ' ) quotes can be used to delimit strings.

When a variable occurs within double quotes, its value is substituted. For example,

When a variable occurs in a string delimited by single quotes, it is treated as a literal string. For example,

If a dollar sign ( $ ) is directly followed by characters, the sequence is treated as a variable string. To treat the sequence as a literal string, use two consecutive dollar signs. For example,

Also note that backslash ( \ ) sequences are recognized in double-quoted strings but not in single-quoted strings. In the following example, the backslash ( \ ) and double quotes ( “ ) are used to create a newline character that is assigned to the variable $n1 .

```
$n1="\n"
```

The next example is a string of the two characters `\' and `n':

```
$n1=`\n'
```



---

# Addition,_Subtraction,_String_Concatenation

# Addition, Subtraction, String Concatenation

The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Arbortext_Editor_Command_Aliases

# Arbortext Editor Command Aliases

For help on a built-in command alias, double-click on an alias name:



---

# Array,_Variable,_and_Package_Functions

# Array, Variable, and Package Functions

Array, variable, and package functions operate on ACL features (arrays, variables, functions, and packages) or provide information about commands and options.



---

# Array_Membership

# Array Membership



The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Arrays_and_Variables

# Arrays and Variables

An array is a special type of variable because it can contain more than one value. An array consists of an array name and an index. The index identifies the element of the array that is addressed.

Arbortext Editor provides two types of one-dimensional arrays:

You do not have to declare arrays or array elements or how many elements are in an array. When used in expressions, arrays are created when referenced in a manner similar to scalar variables. For example, as long as you have not already defined the scalar variable $a , then $a[1] = 'one' creates the array $a and assigns the string " one " to element 1 .

Associative arrays are much like normal arrays except that subscripts are actually strings called keys. For example, $aa["one"] = 1 assigns the value 1 to the element with the key " one ". A null subscript of an associative array is equivalent to a key of " 0 ".

You can iterate over all the keys in an associative array using the for statement:

```
for (
key
in
array
)
```

For example, the following commands iterate over the two elements of the associative array price:

```
$price["candy"] = 45
$price["pop"] = $price["candy"] + 5
for ($junk in $price) {
$price[$junk] += 10;
}
```

A normal array is implemented internally using an array which dynamically expands if necessary as elements are added to it. An associative array is implemented using a hash table so lookups are fast regardless of the array size, but not as fast as a normal array. An associative array also usually requires more memory since each element has a fixed overhead due to the hash table.

Since the syntax for both normal and associative arrays is the same, Arbortext Editor decides which kind of array to use based on the subscript. If the subscript is an integer, a normal array is assumed. An associative array is used if the subscript is a string. If the array subscripts are all small integers but then a string subscript is used, Arbortext Editor will convert the array into an associative array. For example, with

```
arr[1] = 1
arr[2] = 2
arr["three"] = 3
```

the array arr starts off as a normal array but when the third assignment is executed, the array gets converted into an associative array. Arbortext Editor will also convert a normal array into an associative array if the array becomes sparse, that is, the majority of the elements are undefined. For example, with

```
arr[1] = 1
arr[2] = 2
arr[100000] = 100000
```

after the third statement, the array would become an associative array since considerably less memory would be needed to represent it. If you use integer subscripts with an associative array, it is more efficient to use a string subscript as the first reference. For example, preceding both examples above with

```
arr[" "] = " "
```

would avoid the conversion into an associative array.

When used in an expression, the subscript of an array may be an expression. The resulting value is used to access the array element. However, when used in variable substitution, the subscript may only be an integer constant (or string if an associative array), or a scalar variable. For example, the following command will not parse:

```
caret $pos[$i+1]
```

because $i+1 is an expression. This command can be rewritten, however, as

```
$i++;
caret $pos[$i]
```

Although you don't have to declare a global array variable, you can use the global statement to define it as follows:

```
global arr[]
```

The array arr can be either type of array, its subscripts determine whether it is a normal or associative array. The global statement can also be used to declare a fixed size normal array. For example:

```
global arr[10]
```

declares an array with 10 elements, indexed from 1 to 10. In this case, if you attempt to use a subscript not in this range, Arbortext Editor will issue an error message. You can specify a different starting subscript by using the notation global arr [lb ..hb] . For example:

```
global arr[-5..5]
```

defines an array with the lower bound -5 and higher bound 5 . If you know the size of an array, it is more efficient to declare it as a fixed array of that size instead of letting the array dynamically expand. Most of the built-in functions that return arrays return fixed-size arrays.

The local statement can be used to declare local array variables and has the same syntax as global . The low_bound and high_bound built-in function return the bounds of a fixed-size array. The count built-in function returns the number of elements actually in use in either a normal or associative array.

The unsetvar command can be used to undefine an array, discarding its elements. For example:

```
unsetvar arr
```

deletes array $arr . Note that no leading dollar sign is used on the unsetvar command.

To delete an array element, use the delete built-in function. For example:

```
delete($arr[$i])
```

Deleting an element releases the memory for it and marks it undefined, both for normal and associative arrays. The built-in function count will return one less after the deletion. For a dynamic (non-fixed size) normal array, if you delete the first element of the array, the low_bound function will return the next valid index. If you delete the last element, high_bound will return the previous index.

The delete function may also be used to undefine an array, as in:

```
delete($arr)
```

## Related Topics

- • Using expressions

- • Array membership expression

- • char_entity_names function

- • count function

- • delete function

- • join function

- • split function

- • tag_names function

- • user_tag_names function



---

# Assignment

# Assignment

It is important to note that the order in which items appear in this table are arbitrary. All operators have equal precedence to ACL.

The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Back-quotes

# Back-quotes

Information can be processed by either Arbortext Editor , using ACL, or it can be passed to the operating system shell for processing. Various features of Arbortext Editor allow you to pass information between the shell and Arbortext Editor .

The back-quotes (opening single quotes) perform a function similar to the sh command. Any command placed in back-quotes (` `) is also executed in a Bourne subshell. The difference is that the command returns what would normally be piped to standard output (as the sh command does). Therefore the result of the command has to be assigned to a variable. For example to evaluate the user name the following command can be applied:

```
$username =`whoami`message "$username"
```

As a second example, the following command extracts the current date from the system and assigns it to a variable:

```
$today=`date '+%y-%m-%d' `
```

This sequence runs the command date '+%y-%m-%d' in the UNIX shell and assigns the result to the variable $today . The value for this variable might be something like "93-08-25" .

Like the shell, runs of white space in the output (such as blanks, tabs, newlines, and so on) are replaced with a single blank character.



---

# Bitwise_Negation

# Bitwise Negation



The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Bitwise_“and”

# Bitwise “and”

The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Bitwise_“or”

# Bitwise “or”

The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Bitwise_“xor”

# Bitwise “xor”

The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# break_and_continue

# break and continue

The break and continue commands are useful in if , while , and for loops. The break command is typically used in combination with a condition. If a break command is executed in a loop, it immediately forces the loop to be broken off.

In the following example, the while loop is broken off when a noname tag occurs to the left of the string Peter. In that case, the while loop is broken off, the replacement does not take place, and the search terminates.

```
find "Peter"
while ($status == 0) {
if ($tagname == "noname") {
message "noname tag encountered!";
break
}
delete_mark
insert_string "John"
find "Peter"
}
```

The continue command also breaks off the execution of the loop but does not exit it. It causes the rest of the statements in the current cycle of the loop to be skipped and forces the loop to start at the beginning of the next cycle.

In the following example, the break is replaced by a continue . As in the above example, if the string Peter is preceded by a noname tag, it is not replaced. However, unlike the previous example the loop continues its search. It cycles between continue and while , since that status is still true, thus it is not broken off.

```
find "Peter"
while ($status == 0)
{
if ($tagname == "noname")
{
message "noname tag encountered!"
continue
}
delete_mark
insert_string "John"
find "Peter"
}
```

The break command can also be used within a switch statement to transfer control after the end of the switch body. For example:

```
switch (str) {
case |x|:
if (str == "x1") {
break
}
case |y|:
message "$str starts with y"
break
}
```



---

# Buffer_Functions

# Buffer Functions

Buffer functions operate on named paste buffers.



---

# Built-in_Functions,_Callbacks,_and_Hooks

# Built-in Functions, Callbacks, and Hooks

Built-in functions, callbacks, and hooks are built into Arbortext Editor and may be used in expressions.

Use either of the following methods to display the help for a specific command:

- • At the Command line, enter the command help commandname , where commandname is the name of the desired command, function, callback, or hook.

- • In the Help Center, search for the name of the command, function, callback, or hook to view any topics mentioning the term.



---

# Byte_String_Functions

# Byte String Functions

Byte string functions operate on byte strings. Byte strings are used to represent binary data as opposed to character strings which represent Unicode strings (two bytes per character).



---

# Callback_Functions_Introduction

# Callback Functions Introduction

A callback function is a user-defined function that is called during specific events in Arbortext Editor and allows you to customize editing operations. Callback functions provide both a global and a local level of registration or notification to isolate events, while hooks provide only global effect (unless additional user functions are supplied). For example, you might want a particular function called whenever a specific document is saved or a help window has a quit request.

At the session level, there are two basic callback functions. The session_add_callback function adds a specified function as a callback that's invoked whenever the Arbortext Editor session occurs. The session_remove_callback function removes the function as a callback for session monitoring.

At the window level, there are also two callback functions. The window_add_callback function adds a specified function as a callback to that is invoked whenever the specified action occurs in the specified window or in any window if win is 0. The window_remove_callback function removes the function as a callback.

At the document level, there are two basic callback functions. The doc_add_callback function adds a specified function as a callback that is invoked whenever the specified action occurs in the specified document, or in any document if doc is 0. The doc_remove_callback function removes the function as a callback.

At the dialog item level, there are two basic callback functions. The dlgitem_add_callback function adds a specified function as a callback that is invoked whenever the specified action occurs at the specified dialog item. The dlgitem_remove_callback function removes the function as a callback.

You can also invoke callbacks after a specified amount of time. The timer_add_callback function adds a specified function as a callback that is invoked after a specified interval. The timer_remove_callback function removes the function as a callback.

The basic structure of a callback is (document-level callbacks are used for these examples):

```
doc_add_callback (
doc
,
cbtype
,
funcname
)
```

The function specified by funcname is a callback that is invoked whenever the type of action specified by cbtype occurs in document ID doc .

doc is either a valid document ID, or 0. If doc is 0, the callback applies to all documents.

cbtype is a string and must be a callback.

funcname should be a fully-qualified function name with no argument list. As examples of valid and invalid names for funcname :

In the next example, the function mycallback is removed as a callback of type cbtype on the document doc .

```
doc_remove_callback(
doc
,
cbtype
,
mycallback
)
```

An example of a function that is notified whenever a cut is requested on docs 5, 7 or 10:

```
package mycallbacks
function cut_callback( doc, op )
{
if ( op == 1 )
{
# no reason not to proceed
return 0
}
else if ( op == 2 )
{
# this is where processing occurs
# we want to block the user from
# cutting anywhere inside <para> tags in this doc
if ( inside_tag('para', doc) )
{
response( 'Can\'t cut inside <para> tags.' )
return -1
}
else
{
return 0
}
}
}
...
doc_add_callback( 5, 'cut', 'mycallbacks::cut_callback' )
doc_add_callback( 7, 'cut', 'mycallbacks::cut_callback' )
doc_add_callback( 10, 'cut', 'mycallbacks::cut_callback')
```

Whether or not a callback function is called with any parameters depends on the particular function. It is an error to assign a callback function when its parameters do not match (although this is not detected until the function is called).

Callback functions that take op as their last argument are called twice in succession. The first call ( op=1 ) checks for approval to act. A return value of 0 means continue execution. A return value of -1 from any callback means stop the operation without calling any more callbacks that may be registered, do not make any op=2 callback calls, and skip basic Arbortext Editor processing. The second call ( op=2 ) performs the action unless the operation has been stopped earlier. A return value of 0 allows basic Arbortext Editor processing after all callbacks have been called. A return code of -1 from any callback prevents basic Arbortext Editor processing.

## Related Topics

- • channel_set_callback function

- • dlgitem_add_callback function

- • dlgitem_remove_callback function

- • doc_add_callback function

- • doc_remove_callback function

- • session_add_callback function

- • session_remove_callback function

- • timer_add_callback function

- • timer_remove_callback function

- • window_add_callback function

- • window_remove_callback function



---

# Cell_Table_Attributes

# Cell Table Attributes

In addition to the attributes listed in the Shared table attributes help topic, the following attributes are supported on cell table objects.

## Related Topics

- • Table object attributes overview

- • Shared table attributes

- • Set table attributes

- • Grid table attributes

- • Column table attributes

- • Row table attributes

- • Rule table attributes



---

# Channel_Functions

# Channel Functions

The channel functions provide interfaces to the Berkeley socket library, which allows network applications to be written. The open functions return channel identifiers that may also be used with most file identifier functions (for example, read , write , and close ).

Several open_ routines return a channel identifier that may be used by subsequent I/O functions. A channel identifier is a small integer file identifier that is returned by open and can be used with the file identifier routines getline , put , close , read , and write . These channel functions allow binary data to be transmitted.



---

# Column_Table_Attributes

# Column Table Attributes

In addition to the attributes listed in the Shared table attributes help topic, the following attributes are supported on column table objects.

## Related Topics

- • Table object attributes overview

- • Shared table attributes

- • Set table attributes

- • Grid table attributes

- • Row table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_get

- • tbl_obj_attr_set



---

# Command_Variables

# Command Variables

Arbortext Editor provides command variables in a manner similar to the UNIX shells. Command variables are used to specify a string whose exact value may not be known at the time. For example, suppose you want to make a command that tells you the current line number. You can't specify this value exactly because the current line number varies with the position of the cursor. To solve this problem, use a variable to indicate the cursor location.

Some variables are created within Arbortext Editor , while others are created outside Arbortext Editor as environment variables.

## Related Topics

- • Creating your own variables

- • Predefined variables

- • Setting values for variables

- • Using variables

- • The execute command



---

# Conditional_Expression

# Conditional Expression

The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Context-Related_Functions

# Context-Related Functions

Context-related functions pertain to the context for a given element in a DTD or at a point within a specific document.



---

# Creating_a_Named_Current_Buffer

# Creating a Named Current Buffer

If you want to create a named paste buffer to be the current paste buffer (the buffer that stores, and is replaced with each Cut and Copy ), use the command set paste= buffername . The current paste buffer is also the buffer used by the copy_mark , paste , delete_mark , read , and write commands when no paste buffer name is specified.



---

# Creating_a_Named_Paste_Buffer

# Creating a Named Paste Buffer



To write a text passage to a named buffer, use one of these commands:

- •

- •

- •

Buffer names are case-sensitive within the Arbortext Command Language . Thus, you can create one buffer named bills and another named Bills.

To insert the contents of a named paste buffer, use the command paste buffername . In this example, enter the following at the Arbortext Editor command line:

```
paste warntext
```



---

# Creating_and_Manipulating_Windows

# Creating and Manipulating Windows

An unlimited number of application-defined windows may be created using the function window_create . The class (or type) of the window is specified as the first argument to window_create . It may be one of the strings: “edit,” “msg,” “msgwin1 ” through “msgwin4,” “help,” “helpwin1 ” through “helpwin4,” or “list.”

The class determines the default geometry and whether a document tree is associated with the window. If the class is list , then a list selection dialog is created. Otherwise, the window displays a document tree and has a class-specific keymap associated with it. For document class windows (all except list class), the second argument to window_create is a bit mask of flags that controls whether a menu bar is created for the window, whether a vertical scrollbar is created, whether a message area is provided at the bottom of the window, and for edit class windows, whether a Command window is supplied below the Edit subwindow.

The third argument to window_create is a document identifier obtained from a previous call to doc_open or if -1, then a scratch document (doctype ascii for edit classes, or the built-in help document type for other classes) is created and attached to the window. (The associated document tree may be changed later by calling doc_show .) Since doc_open supports arbitrary document types, windows created using window_create may display different arbitrary document types, and in fact, for edit classes, full interactive context checking is enabled. There is a slight performance slowdown when switching between document types, since the parser does not support simultaneous parsing of disparate document types. Internally, the parser is reinitialized when switching between document types, which typically takes one second or so.

The window names edit and cmd do not specify unique windows. These are window classes and when used on commands like caret refer to a window relative to the current document's window, or on the map command refer to a window class map. For example, caret edit issued from a command window keymapping, moves the focus to the corresponding Edit window. If issued from outside an edit or cmd -class window, it will give focus to the last edit class window having focus. The window names msg, msgwin [1-4], help, and helpwin [1-4] refer to the built-in fixed windows (for backward compatibility). These names, when used on commands like caret , or as a window argument to the various window_ xxx functions like window_close , always refer to the built-in windows and never to window of that class created by window_create . A window ID must be used to refer to such windows created by window_create .

There are several window manipulation functions, which are listed in the Window manipulation functions table.

- • Example of edit window function

- • Example of list response panel

- • window_class built-in function

- • window_get built-in function

- • window_id built-in function

- • window_name built-in function



---

# Creating_Buffers_that_Contain_Files

# Creating Buffers that Contain Files

Existing ASCII files or SGML files, such as Arbortext Editor documents or portions of them, can become the text of a paste buffer. To do this, use the read -buffer command. You can then use a paste command to put this file in your document.

To create a paste buffer named cprt that contains the text of an existing SGML file called copyright , enter the following command at the command line:

```
read -buffer cprt -SGML copyright
```

To paste the contents into the document, position the cursor where you want the text to appear and at the command line, enter:

```
paste cprt
```

To create a paste buffer named pl that contains the text of an ASCII file called partslist , enter the following at the command line:

```
read -buffer pl -untag partslist
```

To paste the contents into the document, position the cursor where you want the text to appear and at the command line, enter:

```
paste pl
```

ASCII files may require tagging when inserted into an SGML document.



---

# Creating_your_Own_Variables

# Creating your Own Variables

You can use the readvar command, or an assignment statement (of the format $ varname=expression ) to define your own variables. In addition, many functions will set variables.



---

# DDE_Support

# DDE Support

Arbortext Editor users can use Dynamic Data Exchange (DDE) to execute ACL commands and functions within a Arbortext Editor session. This DDE support is intended for integrators who wish to interface other Windows applications with Arbortext Editor .



---

# Decrement

# Decrement



The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Deleting_Named_Paste_Buffers

# Deleting Named Paste Buffers



To delete an unsaved named buffer during the current editing session, use the delete_buffer command. Otherwise, unsaved named buffers are deleted when you exit Arbortext Editor .

Examples

To remove a named paste buffer, partno , which contains a particular equipment part number that you know you won't need again in this editing session, enter the following command on the Arbortext Editor command line:

```
delete_buffer partno
```

In this way, you are free to create another paste buffer named partno with a different equipment part number.

To delete all unsaved buffers, at the command line, enter:

```
delete_buffer -all
```



---

# Dialog_Box_Functions

# Dialog Box Functions

Dialog box functions provide dialog boxes for user interaction.



---

# Document_Identifier_Functions

# Document Identifier Functions

Most of the Document type functions also take an optional final argument, which is a document ID. Document Identifier functions return or take document identifiers.



---

# Document_Type_Functions

# Document Type Functions

Document type functions return information about a particular document type. Most functions take an optional final argument. This final argument is a document identifier that determines the document type.



---

# Dynamic_Loading_(API)_Functions

# Dynamic Loading (API) Functions

Dynamic loading functions provide a direct interface to the operating system facilities for loading, calling, and unloading functions in dynamically loaded (shared) libraries. In the Windows environment, this includes the following dynamic link library APIs: LoadLibrary , FreeLibrary and GetProcAddress . These functions also allow you to extend ACL by writing DLLs in C or in other programming languages that support DLLs.



---

# Editor_Functions

# Editor Functions

Editor functions query or change the state of a document instance. The OID functions that change the document tree are also found in the “Object identifier (OID) functions” topic.



---

# Entity_Functions

# Entity Functions

Entity functions provide information about general text entities or external file entities.



---

# Example:_Determine_a_File's_Write_Status

# Example: Determine a File's Write Status

The following if command, which would presumably be embedded in a procedure that defined the variable $file , uses the access built-in function to determine the write status of a file:

```
if ( access($file, "w" ) ) {
message "can't write file $file"
}
```



---

# Example:_Edit_Window_Function

# Example: Edit Window Function

Here is an example of a function that could be used to edit another document in a new window. This function is defined in the system _main.acl file. (Note: flags equals the sum of bits set.)

```
function edit_new_window(file, flags=0x3f, geom="") {
# if no special args, use builtin command
if (flags&0x3f == 0x3f && geom == "") {
edit -newwindow $file
return}
# open a new doc tree
local doc = doc_open(file);
if (doc < 0) {
# error message already displayed by doc_open
return}
# see if already in window; if so just expose it
local win = doc_window(doc);
if (win > 0) {
doc_close(doc);
# decrement reference count
window_open(win);
# uniconify maybe
window_raise(win);
return}
# make an edit class window for it with
# edit-style initialization flags |= 0x140
win = window_create("edit", flags, doc, geom);
if (win < 0) { message "Couldn't create
window to edit: $file";
# couldn't make a window so unload document
doc_close(doc);
return}
# make this doc be the current one for
# the set command
current_doc(doc)
# convert tagged tables to pictures according
# to global setting
if (option("tabletags") == "off") {
set tabletags=off}
window_show(win, 1);
# map the window now}
```



---

# Example:_List_Response_Panel

# Example: List Response Panel

You can create any number of non-blocking list response panels using window_create . The window_set function is used to change various attributes of the panel, for example:

- • the list of items to display

- • the label at the top of the panel

- • the default input item

- • the function to call when a button is pressed

- • the labels displayed on the buttons

The scrolling list may be set from an array or appended one item at a time. The callback function has complete control over the behavior of the window when a button is pressed. For example, it can choose to unmap the window (for reuse), destroy it, or display a message and leave the window up.

Here is an example.

```
function list_callback(win, but, seln, pos)
{
if (but == 3)
{
# HELP
window_set(win, "message", "Pick any number");
}
else if (but == 2)
{
# APPLY: leave panel up
# ... do something here with $seln
}
else if (but == 1)
{
# OK
# take down window, but don't destroy it for reuse
window_show(win, 0);
# ... do something here with $seln}
else
{
# else 0 (CANCEL) or -1 (window manager quit)
window_destroy(win);
}
return 0;
}
function pickanum()
{
local w, X[]
# make an array of items
split("one two three four", X)
w = window_create("list")
window_set(w, "items", X, "default", X[2], \
"title", "Pick a Number", \
"callback", "list_callback")
window_show(w, 1);
return w;
}
```



---

# Example:_Substituting_Tags

# Example: Substituting Tags

Currently, you cannot use the substitute command to insert, delete, or change tags. The following series of commands (which would be put in a file and called with the source command) gets around this restriction by interactively inserting a tag pair around every occurrence of the phrase selected. By substituting change_tag or delete_tag for insert_tag in the command sequence that follows, you could design a similar procedure which would delete or change tags in the highlighted phrase.

```
set sgmlselection=off
$phrase=$selection
set sgmlselection=on wrapscan=off
if ($tagname != "") {
if (substr($tagname,1,1) == '/') {
$TAG=substr($tagname,2,length($tagname)-1);
}
else {
$TAG=$tagname
}
} else {
$TAG='NO_TAGS'
}
if ( "$TAG" == "NO_TAGS" ) {
message "No tags allowed in ascii file"
} else if ("$phrase" && "$TAG") {
find -sel "$phrase";
while ($status == 0) {
$ack=response("Change?", "Yes", "No", "Cancel")
if ($status != 0 || $ack == 3) { break;}
if ($ack == 1) {
break;
}
if ($ack == 1) {
insert_tag $TAG}
}
find
}
} else {
message "You must select something first"
}
unsetvar TAG phrase
```

For example, if you want to put emphasis tags around almost every occurrence of “ Arbortext Editor ” in your document, find the first occurrence of the phrase in your document and put emphasis tags around it. Then select the entire phrase (including the emphasis tags) and source the file containing the commands listed above. Arbortext Editor then finds each occurrence of the phrase and prompts you to insert the tag pair. To insert the tag, click on the Yes button on the prompt panel. To skip the phrase (for example, if the occurrence were already tagged), click on the No button. To get out of the search-and-tag operation (abort the loop), click on the Cancel button.

This command script could also be written as a user-defined function.



---

# Example:_Tailoring_Dash_Insertion

# Example: Tailoring Dash Insertion

Arbortext Editor cycles through three different types of dashes (- or hyphen, – or en dash, and — or em dash) when you press the - key. The following commands change the order of this cycling.

```
# Here we define individual aliases to insert each
# kind of dash:
#
alias insert_hyphen
{
insert_string -sgml "-X";
delete_character;
}
alias insert_ndash {insert_string -sgml "&ndash;"}
alias insert_mdash {insert_string -sgml "&mdash;"}
#
# Here we define what dash type should be inserted
# for each case. To change the order, only these
# aliases need to be swapped:
#
alias insert_dash_after_non_dash insert_hyphen
alias insert_dash_after_hyphen insert_ndash
alias insert_dash_after_ndash insert_mdash
alias insert_dash_after_mdash insert_hyphen
#
# Insert the appropriate dash depending on what's
# already there.
#
alias insert_dash
{
# assume pending delete, so if there is a selection,
# delete it before inserting the dash
if ( selected() > 0 )
{delete_mark;}
# now select the character before the cursor
clear_mark;
mark begin;
caret 0,-1;
mark end;
# figure out what dash to insert based on the previous
# character, since sgmlselection may be set on or off,
# we need to test two cases where the SGML and ASCII
# versions are different.
if ( $selection == "-" ) # type one dash
{
delete_mark;
insert_dash_after_hyphen;
}
else if ( $selection == "&ndash;" || \
$selection == "––" ) # type two dashes
{
delete_mark;
insert_dash_after_ndash;
}
else if ( $selection == "&mdash;" || \
$selection == "–––" ) # type three dashes
{
delete_mark;
insert_dash_after_mdash;
}
else
{
clear_mark;
caret 0,+1;
insert_dash_after_non_dash;
}
};
#
# Finally, we map the hyphen/dash/minus key to our
# insert_dash alias.
map edit - insert_dash;
```

If you were operating in an environment when pending delete was disabled, you would want to remove the lines that deleted a selected region.



---

# Example:_Test_a_Document_Type

# Example: Test a Document Type

The following command notifies you if the document you are editing is a plain ASCII file rather than an SGML document:

```
if ($doctype=="ascii") {
message "Notice: The file you are editing \
is not an SGML document. You can still use \
Arbortext Editor to edit this file but \
you cannot enter tags.";}
```

The logical expression $doctype=="ascii" tests the value of the variable $doctype . If the value of this variable is ascii (that is to say, if you are editing an ASCII document), Arbortext Editor prints the warning message expressed by the message command.

You could put this in the document docname .acl file, but then you would not get the message if you switched documents with the edit command. To get around this, you could put the above if/else command in a command file called asciiwri.acl . Then put the following commands in your docname .acl file:

```
source asciiwri.acl
alias pub {edit $1; source asciiwri.acl;}
```

If you use the pub command to switch files instead of the edit command, you are notified if you have switched to an ASCII file.



---

# Example:_Test_the_Location_of_a_Document

# Example: Test the Location of a Document

These commands modify the running headers for any memo documents in a particular directory:

```
$workingdir=`pwd`
if (index($workingdir,'conf')!=0 && \
$doctype=="memo") {modify_tag -global document \
scilevel=secret;}
```

pwd is used to print the complete path for the working directory. The path is then used as the value of the newly defined variable $workingdir . Statements of the format $ xxx = are used to assign values to variables or to create variables and assign them values. The name of the variable appears to the left of the = sign and the value of variable appears to the right. pwd is a command that prints the complete path for the working directory. You can pass commands from Arbortext Editor to the operating system by enclosing them in left quotes.

The condition for this if command consists of a complex expression made of two smaller expressions.

The first of the smaller expressions:

```
index($workingdir,'conf')!=0
```

uses the index function to test whether the path for the working directory includes the string “ conf ” for confidential (presumably, any memos in the directory conf or a subdirectory of that directory should have the special header). The != (NOT) operator compares the result of the index function with 0 . If the value is not 0 (that is, the string “ confidential ” appears in the path) then the first expression is true. If it is 0 , the expression is false.

The second of the smaller expressions:

```
$doctype==”memo”
```

tests to see whether the value of the variable $doctype is “ memo ”. In this case, if the value is 0 (the value for $doctype was “ memo ”), the expression is true. If the value is not 0 , the test is false.

Finally, the AND operator, && , compares the results of the two tests. For the Arbortext Editor modify_tag command to be executed, both expressions must be true. (The modify_tag command changes the security level, or “ scilevel ”, to “ secret ”) If the document is not a memo or is not in the directory conf , the security level is not affected.



---

# Example_of_Named_Paste_Buffers

# Example of Named Paste Buffers

Suppose you have a Arbortext Editor document that contains a list of unsorted addresses and you want to create two new separate sections—one for people in Maine and the other for people in Wisconsin. You could create two simple keymappings to help you with your task. The first keymapping, F5 , would delete the highlighted address and add it to a paste buffer containing the addresses of people who live in Maine (ME). The second, F6 would add them to a buffer for people who live in Wisconsin (WI):

```
map f5 {delete_mark -append ME}
map f6 {delete_mark -append WI}
```

After you go through the mailing list collecting the addresses for Maine and Wisconsin, paste in the sorted address lists by entering at the command line:

```
paste ME
```

and

```
paste WI
```



---

# Expression_Operator_Precedence

# Expression Operator Precedence

Expressions are built using the following operators, which are listed in increasing order of precedence (grouping operators have highest precedence; assignment operators have lowest). Within each table, the operators have equal precedence.



- • Assignment operators

- • Conditional expression operator

- • Conditional Logical “or” operator

- • Logical “and” operator

- • Array membership operator

- • Bitwise “or” operator

- • Bitwise “xor” operator

- • Bitwise “and” operator

- • Relational operator

- • Shift operators

- • Addition, subtraction, and string concatenation operators

- • Multiplication, division, and remainder operators

- • Unary minus operator

- • Logical negation operator

- • Bitwise negation operator

- • Increment operator

- • Decrement operator

- • Grouping operator



---

# File_Identifier_Functions

# File Identifier Functions

File identifier functions manipulate file identifiers (FIDs) returned by the open function. These functions provide an interface to the C-library standard I/O routines.



---

# File_or_System_Functions

# File or System Functions

File or system functions provide file or system information or are used to manipulate pathnames.



---

# Formatting_Pass_Reduction_in_ACL

# Formatting Pass Reduction in ACL

The term "pass reduction" refers to minimizing the number of formatting passes Arbortext Editor takes when formatting a document instance for preview or printing. Without pass reduction, documents that refer to page numbers or page locators (for example, in a table of contents, in cross references, or having the final page number in the header or footer), will require two passes the first time they are formatted during an editing session. With pass reduction, many documents can be formatted satisfactorily with one pass. This approximately halves the time required for formatting, at the risk of some loss in typesetting precision in the form of extra white space adjacent to page numbers.

The basic mechanism for pass reduction is a process where the resolved page locators are overlaid in space reserved for them during the initial pass. Whether or not there is visible extra space, and whether it degrades a document's appearance depends on the FOSI, and the document instance.

Arbortext Editor provides users with access to pass reduction controls with two preferences. For ACL scripting purposes, these preferences are available in the form of two set commands.

The set commands are set overlaypagenumbers set overlayunderflowtolerance .

The set overlaypagenumbers command enables/disables pass reduction (the default is enabled). The set overlayunderflowtolerance command sets the amount of disparity to accept when a final page variable value is smaller than the space it is overlaid in. Arbortext Editor never accepts an overlay if the new value is larger than the space it is overlaid on (the default is one character).

The related environment variable, APTNOOVERLAYPAGENUMBERS , is provided for customers who absolutely do not want page number overlaying to be done, they can totally disable overlaying by setting the environment variable APTNOOVERLAYPAGENUMBERS to Yes .

The paragraphs below explain how these settings interact with formatting command options. First some terms need to be explained:

- • overlaying fails means that it is impossible to overlay page numbers because the change in a page variable affects the structure of the formatted output, not just a character string. This is the case when

- • overlaying was poor means:

- • overlaying works well means neither of the above conditions was true

- • formatting command means any of the preview , format , or print composed commands.

If pass reduction is enabled, and you execute a formatting command with the onepass option, the Arbortext Editor formatter makes one pass, and at the end of the pass overlays page numbers so that the output will show resolved page numbers. If overlaying fails or is poor, then the document will be marked as refmt-needed and the next formatting command the user enters will cause another formatting pass, and the correct values will be plugged in without being overlaid. If overlaying works well, then the document will not be marked as refmt-needed . If desired, the user could force an additional formatting pass using the force option with the formatting command in order to obtain a non-overlaid result.

If pass reduction is enabled, and you execute a formatting command with the allpasses option, the Arbortext Editor formatter first makes one pass and at the end of the pass overlays page numbers. If overlaying fails or is poor, then the formatter automatically does another pass. If overlaying works well, then the single pass suffices. Again, if desired, the user could force an additional formatting pass using the force option with the formatting command in order to obtain a non-overlaid result.

If pass reduction is disabled, and you execute a formatting command with the onepass option, then the Arbortext Editor formatter makes one pass, and at the end of the pass, if there are any page numbers that are incorrect, it overlays page numbers so that the output will show resolved page numbers. That part is the same as if pass reduction is enabled. What is different is that the document will be marked as refmt-needed if any page number overlaying was done, regardless of whether the overlaying worked well.

If pass reduction is disabled, and you execute a formatting command with the allpasses option, the Arbortext Editor formatter makes one pass, and at the end of the pass, if there are any page numbers that are incorrect, a second pass is automatically initiated.

A compromise for users who want highest publishing quality but want the speed of overlaying would be to specify the underflow tolerance as 0 . Then overlaying will be attempted, but will only be accepted for final output if the number of characters matches exactly. How often this happens will depend on the work habits of your authors.

## Related Topics

- • print command

- • preview command

- • format command

- • set overlaypagenumbers command

- • set overlayunderflowtolerance command

- • APTNOOVERLAYPAGENUMBERS environment variable



---

# Functions_as_Expressions_and_Commands

# Functions as Expressions and Commands

Except as otherwise noted, all arguments may be expressions. Also, the ACL parser recognizes function calls in the context of a command. This means that, in addition to using a variable assignment or logical expression to call a function (such as $n = split("a b c", $arr, " ") , you can type a command that contains a function call at the command line. Here is an example:

```
split("a b c", $arr, " ")
```

When you call a function in this manner, the value returned by the function is discarded.

## Related Topics

- • Using expressions

- • Logical expressions

- • Expression operator precedence

- • Operands



---

# Grid_Table_Attributes

# Grid Table Attributes

In addition to the attributes listed in the Shared table attributes help topic, the following attributes are supported on grid table objects.

## Related Topics

- • Table object attributes overview

- • Shared table attributes

- • Set table attributes

- • Column table attributes

- • Row table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_get

- • tbl_obj_attr_set



---

# Grouping

# Grouping



The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Hook_Functions_Introduction

# Hook Functions Introduction

A hook is a user-defined function that is called at strategic places by Arbortext Editor so you can customize editing operations. Setting a hook has global effect unless you build in additional user functions to specify a local level.

The built-in functions add_hook and remove_hook are convenience routines that enable and disable hook functions. The add_hook function has the form:

```
add_hook(
hookname
,
funcname
[,
prepend
])
```

where hookname is the name of the hook set option, funcname is a string specifying the name of the user-defined function to call, and prepend is an optional flag which if non-zero specifies the function should be added to the head of the hook function list. add_hook will not add funcname if it is already present in the list. The remove_hook function has the form:

```
remove_hook(
hookname
,
funcname
)
```

where the parameters hookname and funcname are the same as for add_hook .

Whether or not a hook function is called with any parameters depends on the particular hook. It is an error to assign a hook function with mismatched parameters (although this is not detected until the hook function is called). Some hook functions must return a result. For hooks that do return a result, -1 is generally a special return value. This value means the edit operation was completed by the callback, no additional callbacks are needed, and Arbortext Editor need not continue processing the command.

A hook function may change the associated set option (by using add_hook or remove_hook ), although the change will not take effect until all functions on the current hook list have been called. However, any hook may still return a value of -1 to abort the processing of the remaining hooks.

When a hook function is called, the hook is suspended so that the function will not be reentered if it executes a command or function that would result in the hook function being called again.



---

# if,_while,_for,_switch

# if, while, for, switch

The Command Language has four commands available to conditionalize execution of commands to a specific condition. These commands are if , while , for , and switch .

The if statement has the following structure:

```
if (
condition
) {
commands
} else {
commands
}
```

If the condition defined by condition is true (that is, not equal to 0 (zero)), then the first group of commands is executed. If the condition is false (that is, equal to 0), then the second group of commands (defined by the else statement) is executed. The else statement in this command is optional.

In the following example, a find command is executed. The if statement checks the $status variable to evaluate if the find was successful. If the condition $status == 0 (that is, if the find was successful, and thus the status variable is equal to 0), then the string is replaced, otherwise a message is issued indicating that the string was not found.

```
find "Peter"
if ($status == 0) {
delete_mark
insert_string "John"
} else {
message "Peter not found!"
}
```

The while command described below is a loop statement that relates repeated execution of a group of commands to a specific condition.

```
while (
condition
) {
commands
}
```

The commands defined by commands are repeatedly executed until condition becomes false (that is, equal to 0 (zero)).

In the next example, the find and replace commands are repeatedly executed until the find command is unsuccessful, which sets the status variable to something other than 0 (zero). The result is that every occurrence of the string in a document is replaced, rather than only the first one, as in the previous example.

```
find "Peter"
while ($status == 0) {
delete_mark
insert_string "John"
find "Peter"
}
```

The for command can also execute a group of commands repeatedly. There are two ways to use the command.

In the following example, for is used to execute a group of commands for every element in an array. If $array is an array variable with five elements, then commands is executed five times (for each element in this array). Each time, $index has the current value of the array index.

```
for ($index in $array) {
commands
}
```

The second way to use the for command is to relate its execution to a counter. In the following example, $count is set to a start value of 1 . The commands are executed while $count is less than 5 . After every cycle the counter is incremented by 1 . This means that the commands are executed exactly four times.

```
for ($count=1; $count<5; $count+=1)
{
commands
}
```

Note that at the exit of the for loop the value of $count is equal to 5 .

The syntax of the second use of for is just like in C language:

```
for (
expression1
;
expression2
;
expression3
)
{
commands
}
```

where each expression is optional. This form is equivalent to:

```
expression1
while (
expression2
) {
commands
expression3;
}
```

The switch command selects from a group of statements based on the value of the expression. The form of the statement is similar to that of the C programming language. It has the following syntax:

```
switch (
expression
)
{
case
constant1
:
statements
break
case
constant2
:
statements
break
…
default:
statements
break
}
```

The body of the switch statement must be enclosed in braces. The case statements do not need to be enclosed in braces.

The case and default prefixes do not alter flow of control. The break statement may be used to transfer control out of the switch statement.

Unlike C, the case constant value does not only need to be an integer. The constant may be a string value delimited by single or double quotes, or a regular expression delimited by slashes. For example, this:

```
switch (x) {
case 1:
message "x is 1"
break
case "one":
message "x is 'one'"
break
case /this|that/:
message "x contains 'this' or 'that'"
break
}
```

is equivalent to this:

```
if (x == 1) {
message "x is 1"
} else if (x == "one") {
message "x is 'one'"
} else if (match(x, "this|that")) {
message "x contains 'this' or 'that'"
}
```

Since the match function is used to evaluate a case prefix that specifies a regular expression, the statements following the case may use the match functions match_result , match_start , and match_length to extract parts of the matched expression.

If the case constants are all integer values or string constants of a single character, a jump table may be used to transfer control to the matched value. This executes considerably faster than a series of if, else if clauses. If the case values are all string values, a binary search is used (for more than three cases). A series of if, else if statements are compiled if the case values are regular expressions or are a mixture of string and integer value.

The case constant label allows for variable substitution. For example:

```
readIncompete=-2
readError=-1
readEOF=0
switch (read(ch, buf, 512)) {
case $readIncomplete:
...
case $readError:
...
case $readEOF:
...
default:
...
}
```



---

# Increment

# Increment



The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Inserting_the_Text_of_a_Named_Paste_Buffer

# Inserting the Text of a Named Paste Buffer



The paste command allows you to insert text from a temporary or permanent (saved and loaded) named buffer at the cursor.

If warntext is a paste buffer you made in this editing session, to insert its text, enter the following command at the command line:

```
paste warntext
```

If warntext is a paste buffer you made in a previous editing session of this document, and you saved it with the save_buffers command to the document subdirectory, then to insert its text, enter this at the command line:

```
load_buffers
```

press ENTER and then enter this at the command line:

```
paste warntext
```

The text of warntext appears at the cursor.



---

# list_response

# list_response

The list_response function presents the user with a number of choices in a scrolling list panel. The list is passed as an array variable. For example, to create a list with four choices, enter on the Arbortext Editor command line:

```
split("red green blue black", $a)
$choice=list_response($a, "Choose a Color")
```



---

# Listing_Paste_Buffers

# Listing Paste Buffers



To list the named paste buffers in the current editing session, use the command show buffers [output= filename ] .

To see a panel of the current named buffers, at the command line, enter:

```
sho buffers
```

or, to make a file of the names in the current directory, enter:

```
sho buffers output=buffers.txt
```



---

# Loading_Saved_Buffers

# Loading Saved Buffers

To load named paste buffers saved in a previous editing session, use the load_buffers command. You may specify a directory from which to load.

If the named paste buffers are in the directory with the document, enter the following command on the Arbortext Editor command line:

```
load_buffers
```

If the named paste buffers are in another directory, you must specify the path and file name.



---

# Logical_Expressions

# Logical Expressions

Logical expressions are those using the operators ! (for logical negation), && (the “and” operator), or || (the “or” operator). In logical expressions, a string that is not the null string or “ 0 ” (zero) is evaluated as true. The result of a logical operator is 1 for true and 0 for false. Short circuit expression evaluation is done for the “and” and “or” operators. This means that with the “and” operator ( && ), evaluation ceases as soon as a false is found, for the expression must be false. Likewise, with the “or” operator ( || ), evaluation ceases as soon as a true is found, for the expression must be true.

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Expression operator precedence

- • Operands



---

# Logical_Negation

# Logical Negation



The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Logical_“and”

# Logical “and”



The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Logical_“or”

# Logical “or”



The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Manipulation_of_Selections

# Manipulation of Selections

Three commands can manipulate a selected region.

- • copy_mark — causes the selected region to be copied into the paste buffer.

- • clear_mark — deselects a selected region.

- • delete_mark — cuts the selected region and puts it into the paste buffer.

Usually, the delete_mark command is performed only when the region has balanced tag pairs. Unbalanced regions are allowed, however, if tags can be inserted such that the document remains in context.

Failure of any of these commands causes the $status variable to be set to 1 .



---

# Marking

# Marking

Use the mark command to mark a string in the document (this string may include tags) for further processing. Marking (or highlighting) is a way to select, evaluate, or remove certain parts of a document. The mark begin command initiates a selection, starting highlighting at the cursor. The mark end command terminates the highlighting and causes the region to be selected. This region ranges from the place where the cursor was (where mark begin was executed) to the place where the mark end is issued. At this point, the variable $selection is equal to the content of this region and can thus be evaluated.

In the following example, the cursor is first moved to the top of the document. Then it is placed after the first chaphead it encounters and the beginning of the selection is marked. Then the cursor is placed before the end tag (note the –1 value to place it before the end tag rather than after it). Then the end is marked. The content of the chaphead tag pair is then assigned to the variable $title .

```
caret first,first
caret 0,"<chaphead>" -t
mark begin
caret 0,"</chaphead>"-1 -t
mark end
$title = $selection
```



---

# Menu_and_Keymap_Functions

# Menu and Keymap Functions

The menu and keymap functions query keymaps or the menu system.



---

# Menu_Paths

# Menu Paths

A menu path is a way of indicating the exact location of an item in the menu system. (This item can be either an item on a menu, or the menu itself.)

Menu paths look like directory paths, except periods are used to separate the components instead of slashes. The leading parts of a menu path correspond to a menu name, the trailing part matches a menu item. For example, .File.New refers to the item New on the File menu.

A menu path is considered absolute if it starts with a period ( . ). The name following the period must be the name of one of the top level menus on the menu bar. (For example, .File , .Edit , .Tools .) If a menu path does not start with a period, the entire menu bar hierarchy for the current window is searched for the first occurrence of the item starting with the first menu on the left and progressing down through every item on a menu before moving on to the next menu to the right.

You can use the menu path to specify a destination (as with the menu_add and menu_move commands). If a dot appears at the end of a menu path, it indicates the last item on the last menu named. For example, menu_add .File.New. 'Create Invoice' specifies that the new item Create Invoice would be added at the end of the New submenu of the File menu, but menu_add .File.New 'Copy Document' would cause the new item Copy Document to be added to the File menu after the item New .

When matching a menu path against a menu item, the mnemonic key character & is ignored in both strings. For example, " .File.New " will match the " &File ” menu. Also, it is not necessary to specify a trailing ellipsis (" ... ") or mnemonic of the form "( &X )" on the target menu item. The menu path " .File.Open " will match the " Open... " menu item of the " File " menu. Similarly, " .File.Exit " will match the " File " menu item " Exit(&Q) ". The trailing mnemonic ( &X ) is often used with Asian localized menus.

The syntax of a menu path allows specifications of a menu item by position and also by name. If a component of a menu path begins with # and is followed by one or more digits, then this specifies a numeric position. For example, the menu path .File.#3 specifies the third item in the File menu. Numeric positions may be specified in any component. For example, .File.#1.#2 is the same as .File.New.Sample , assuming the default menu configuration. The first non-title item is referenced by #1 . The menu title, if any, may be specified by using #0 . Blank or separator lines within the menu count as items. The function menu_item_count may be used to obtain the number of items in a menu.

Menu item labels may contain variable references. If a menu label contains any variable references, for example, Modify $tagname , the variable reference is substituted into the label string each time the menu containing the item is posted.

## Related Topics

- • Modifying the default menus

- • Special characters in menu paths

- • Shortcut menus



---

# Modifying_the_Default_Menus

# Modifying the Default Menus

With Arbortext Editor , it is possible to modify the default menus for an entire installation, for a particular document, for a particular user or group of users, or for a particular document. You may want to modify the order in which some items appear on the Arbortext Editor menus, delete menu commands, add custom functions to existing menus, or add new menus to the menu bar. It is also possible to replace the entire existing menu structure. You can also include shortcut menus for any window.

A single menu configuration file is used for all document types because there are no document-type specific items in the default menus. Arbortext Editor loads the file editmenu.cf from the lib subdirectory of Arbortext-path . A different default editmenu.cf file may be loaded by setting the environment variable APTMENUFILE to the path name of the menu configuration file.

The commands menu_add , menu_change , menu_delete , menu_copy , and menu_move let you customize the menus. The menu_reset command restores the menus to their default states. The menu_save and menu_load commands create and load a menu configuration file, which can be used to store your customized menus. (You need to maintain the correct path names to the menu configuration file if you move the document type to a new directory.)

For specific information on each command, click on the name of the command listed below:

The type of menu customization determines which customization file it should be included in.

To modify the default menus for a particular document type, place the commands to modify or load menus in the document type instance command file .

For a document, place the commands to modify or load menus in the document command file in the directory containing the document docname file.

To replace the default menu configuration file for all of the document types, set the environment variable $APTMENUFILE to the path name of the new menu configuration file.

To replace the default menu configuration file for a particular document type, use the menu_load command to load a menu configuration file, typically named menu.cf .

Arbortext Editor reads the document type command files ( doctype .acl and doctype .js ) and then the document type instance command files ( instance.acl and instance.js ) in the document type directory if they exist, before reading document command files ( docname .acl and docname .js ). The document type instance command files are read when the document type is loaded and whenever documents are switched. This allows document type-specific changes to the menus using the menu_add , menu_delete and menu_change commands, or another configuration file to be read using menu_load .

Because the document type instance command file is read each time you open a document of the same document type, any menu modification commands should be conditionalized using tests. For example:

```
if (!menu_exists(".MyMenu")) {
menu_add -menu . ".MyMenu"
menu_add ".MyMenu." "Some item" -cmd {some_command;}
}
```

## Related Topics

- • Menu paths

- • Special characters in menu paths

- • Shortcut menus



---

# Multiplication,_Division,_Remainder

# Multiplication, Division, Remainder

The order in which items appear in this table are arbitrary. All operators have equal precedence to ACL.

The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Notation_Functions

# Notation Functions

Notation functions provide information about notations declared in a document.



---

# Object_Identifier_(OID)_Functions

# Object Identifier (OID) Functions

In addition to strings and integers, there is another data type in ACL called an object identifier (OID).

An OID is a unique identifier that locates an element within the structure of a parsed document instance. The OID also records to which document instance the element belongs. This means you can save an OID in a variable, and then later refer to it in OID functions. It makes no difference what the current document is.

An OID is assigned to each start tag when it is parsed or inserted into the document instance. An OID is valid for the duration of an editing session or until the associated object is deleted, for example, by a cut operation.

Not all SGML markup within Arbortext Editor are given OIDs. In particular, character entity references represented by internal tag names starting with & , and the _include and exclude internal tags used to represent included marked sections, are not assigned OIDs because they are not part of the element structure. End tags are not assigned OIDs because the OID for the start tag is sufficient to locate the end of the structure.

File and text entity tags do have object identifiers. That is, OID functions such as oid_next and oid_child return OIDs for file and text entity tags. These entity objects appear as elements with no content, and oid_empty always returns the value of 1 .

To descend into an entity, the oid_entity_first function may be used to return the top-level element contained within the entity. For external file entities, the OID returned will be in a different document tree. If oid is the OID of a file entity, oid_doc( oid ) != oid_doc(oid_entity_first( oid )) For text entities, the OID returned is in the same tree. Related functions are entity_first , entity_doc , and entity_name .

When the viewchangetracking option is set to all the oid-walking functions will “see” and be able to return change tracking markup. Under any other circumstances they will not. It is acceptable to pass a change tracking markup oid to an oid function no matter what the view setting.

There are several functions that operate on OIDs to permit efficient navigation and interrogation of the document structure. In addition, the logical operators == and != may be used to compare two OIDs for equality. The logical operators < , <= , > , and >= test the ordering of two OIDs. For example, oid1 < oid2 is true if oid1 occurs before oid2 in the document instance. The relational operators do not test structural relationships; the oid_level function can be used for testing if one OID contains another.

The only other operator that permits OIDs as operands is the assignment operator. It is incorrect to use an OID with any other operator (for example, + ) or to compare an OID with a number or string.



---

# Operands

# Operands

Operands for expressions are any of the following:

Leading white space in a string is ignored in cases where the string is interpreted as a number.

Arbortext Editor uses the dot (.) as a concatenation operator, which allows you to use built-in functions, such as substr , to build strings. This means that for a document named Ch2 , an operand such as ${ docname }.bak would be interpreted as Ch2bak , and not as Ch2.bak . In cases where this is not desired, you must use quotation marks to indicate that the dot is to be taken literally (for example, "${ docname }.bak" ).

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Expression operator precedence

- • Logical expressions



---

# Packages

# Packages

Packages let you declare global variables and functions whose name space is localized to one or more command files. You declare a package using the package command at the beginning of a file. Here is an example:

```
package myapp
```

This package defines a new symbol table in which all global variables and functions in the remainder of the file are placed. You can refer to variables and functions in other packages by adding them to the package name with two colons (::). Here are some examples:

```
main::selection, history::set_cmd_line(), myapp::myvar
```

Predefined variables such as doctype , status , selection , etc., are defined in the package main . If you want to reference these predefined variables and functions inside a new package, the new package must be preceded by the main package, such as:

```
main::status
```

In packages other than main , it's not necessary for a dollar sign ($) to precede a variable term inside an expression.

All function names defined in a package are local to the package. It is possible, however, to "export" the function name to the main package (or another package) by using a package prefix on the function definition. Here is an example:

```
function main::fac(n) { ...}
```

The example shown above puts the function name fac into the main package, but any variables in the function body are still local to the current package.

The package declaration may also be used within a function definition to switch the current package. The scope of the package declaration is the same as the local command. That is, the previous package is restored when the end of the block is reached, which is indicated by a right curly bracket (}), or another package command is executed. Here is an example:

```
package myapp
status=0
function f(x)
{
# refers to myapp::status
status = 1;
{
package main
# refers to main::status
status = 0;
}
# refers to myapp::status
status = 2;
}
```

If you're in a package other than main , and that package calls out functions (including built-in functions) defined in main , it's not necessary to precede those functions with the main package prefix. When a function call without a package prefix is compiled, the parser looks up the name of the function in the active function list. If the function name isn't found, the parser tries to determine if the function is a user-defined or built-in function in the main package.

Unlike package main , a reference to an undefined variable does not refer to an environment variable of the same name. For example, in the main package, $PATH normally refers to the path environment variable. In any other package, $PATH refers to a package local variable.

The name space for aliases is not affected by packages. Aliases are always compiled as if they had been defined in the main package. Like the local command, the package command is not valid in an alias. To refer to variables (and functions) that aren't in the main package, you must use the package name prefix within an alias.

Built-in Arbortext Editor commands may also be prefixed with the main:: qualifier. This allows you to define an alias that unambiguously refers to a primitive command. Here is an example:

```
alias myquit {
# do something
main::quit; # really quit
}
```

Without the prefix, the reference to quit might actually invoke some alias of quit.

The package function can be used to change the current package to a package previously specified by the package command.



---

# Predefined_Variables

# Predefined Variables

Some variables are predefined by Arbortext Editor . This following is a list of predefined variables and what they represent. All of these variables are automatically maintained by Arbortext Editor .

- • $ENV — An associative array in the main package defining the current environment. For example, to refer to the environment variable APTCATPATH in any package, use main::ENV["APTCATPATH"] . In the main package, $APTCATPATH can be used directly, although this use is not encouraged since it is not clear whether you are referring to a Arbortext Editor or system environment variable.

- • $ERROR — The syntax or run-time error message for the last command executed. It is set to the null string before any command or expression (including those from the execute and eval built-in functions) is compiled.

- • $ERRORS — The array that holds the last few errors that were stored in $ERROR . The number of stored errors is determined by the value of $ERRORS_SIZE . An entry can added to this array either by an error in a function or command (such as doc_open ) or by any ACL command or function which explicitly assigns a value to $ERROR .

- • $ERRORS_SIZE — Controls how many errors are stored in $ERRORS . If a new entry to $ERRORS exceeds the limit of $ERRORS_SIZE , the oldest entry is removed. The default is 10.

- • $is_compact_install — Determines if the version of Arbortext Editor running is the compact installation. If Arbortext Editor is the compact installation, returns any value other than zero. If Arbortext Editor is the full installation, returns zero.

- • $is_e3 — Determines if the Arbortext Publishing Engine is running in server-mode (no user interface) and, if true, returns any value other than zero.

- • $is_e3_interactive — Determines if the Arbortext Publishing Engine is running in Arbortext Publishing Engine Interactive mode (has user interface) and, if true, returns any value other than zero. Used with $is_e3 , as in the following example, to determine the mode in which the Arbortext Publishing Engine is running:

- • $OFS — The output field separator used by eval command to separate expressions. The default value is a single blank.

- • $ORS — The output record separator used by eval command to terminate an expression list. The default value is a single newline.

- • $PCS — The separator that separates parts of a path. It is a read-only variable equal to “ \ ”.

- • $PLS — The path list separator, that is, the character that separates path names in a list of path names. It is a read-only variable equal to “ ; ”.

- • $RESPONSES — The array that holds the last few responses that were stored in $RESPONSE . The number of stored responses is determined by the value of $RESPONSES_SIZE . An entry can be added to this array either by a response from the response function, the message command or by any ACL command or function which explicitly assigns a value to $RESPONSE .

- • $RESPONSES_SIZE — Controls how many responses are stored in $RESPONSES . If a new entry to $RESPONSES exceeds the limit of $RESPONSES_SIZE , the oldest entry is removed. The default is 0 for Arbortext Editor and 10 for the Arbortext Publishing Engine .

- • $OFS — The output field separator used by eval command to separate expressions. The default value is a single blank.

- • $SYMTAB — An associative array giving the symbol table for global variables in the current package. SYMTAB[ expr] is equivalent to the variable named by the result of expr , for example, SYMTAB["x"] is a synonym for the variable x . Note, one way to test for the existence of a variable "var" is to use the expression (var in SYMTAB) . This is equivalent to defined(var) . SYMTAB is the only predefined variable which exists in all packages. All other predefined variables are only in the main package.

- • $appdata — The path name of the application data directory. This is the same value as returned by the get_appdata_dir function called with no arguments. $appdata is a read-only variable.

- • $aptpath — A read-only variable which specifies the location of the directory that contains the program files needed to run the software.

- • $arch — A read-only variable that specifies the architecture of the host running the software.

- • $comproot — The installation directory used for publishing. If Arbortext Publishing Engine is being used for publishing, this is the path name on the Arbortext Publishing Engine server. Otherwise, the value is the same as the value of $aptpath . $comproot is a read-only variable.

- • $currentcolumn — The number of the column where the cursor is positioned. This variable is valid only if the current document is displayed in a window. This is a read-only variable.

- • $currentline — The number of the line where the cursor is positioned. This variable is valid only if the current document is displayed in a window. This is a read-only variable.

- • $dirname — The directory name of the current document if it is attached to an edit class window, or the document attached to the Edit window that last had focus.

- • $dirselect — The name of the currently selected file name in the directory display (if no file name is selected, its value is null). This is a read-only variable.

- • $docname — The name of the current document if it is attached to an edit class window, or the document attached to the Edit window that last had focus. It is the name without any leading path name components. For example: /jdoe/mydoc.sgm becomes mydoc.sgm .

- • $filename — The path name of the file being edited including any leading path name components and the file name. It refers to the current document if it is attached to an edit class window, or the document attached to the Edit window that last had focus.

- • $home — A read-only variable that holds the value of the user's home directory. $home defaults to the value of the HOME environment variable. Otherwise, $home uses the home directory as specified by the operating system. If no home directory can be determined, $home is set to the Arbortext Editor startup directory.

- • $progname — The full name of the program being executed, for example, Arbortext Editor .

- • $selection — A string representing the selected region in the current window (if no selection exists in that window, its value is null). If sgmlselection=on , the string includes any SGML codes. Otherwise, tags and other SGML are not included in the string. This is a read-only variable.

- • $sh_status — The exit status of the process executed by the last sh command or backquote expression.

- • $status — A number representing the status of the last command executed: 0 means successful completion. 1 means failure. 2 (which only applies to conditional commands) indicates a syntax error.

- • $system — A string specifying the type of system on which Arbortext Editor is running. $system is a read-only variable.

- • $tagname — The name of the tag to the left of the cursor in the Edit view (in ASCII documents its value is null). End tags start with slash (/). Angle brackets are not included in the value. This is a read-only variable.

- • $topline — The vertical position in the document of the line at the top of the window. This variable is valid only if the current document is displayed in a window. This is a read-only variable.

- • $version_build — The current build number of Arbortext Editor . This is a read-only variable.

- • $version_date — The date of the current version of Arbortext Editor . This is a read-only variable.

- • $version_date_code — The current software date code. For example, “M020”. This is a read-only variable.

- • $version_number — The current version number of the software. This is a read-only variable.

- • $version_release — The current software release number. For example, “5.4”. This is a read-only variable.

- • $winsys — A string specifying the type of windows system for which this version of Arbortext Editor was created. (For example, " Windows ".) $winsys is a read-only variable.

- • $wintype — A string specifying the internal windows system implementation type for which this version of Arbortext Editor was created. (For example, " MFC " or " Galaxy ".) $wintype is a read-only variable.

- • _STRICT_ — A variable that controls how variables are declared in ACL packages. If you declare the _STRICT_ variable at the top of your package file, all variables must be explicitly declared. The default behavior is for variables to automatically declare themselves the first time they are referenced.

Arbortext Editor also recognizes environment variables. The associative array $ENV is the preferred way to access environment variables. However, for variable references used in the main package, if Arbortext Editor cannot find a variable of the name you supply, and an operating system environment variable of the same name exists, its value is used.

Use the command show variables or show vars to display a list of the variables defined in the main package.

## Related Topics

- • Creating your own variables

- • Environment variables

- • Using expressions

- • Setting values for variables

- • show variables command

- • set stricterrors

- • eval (command)

- • Using variables

- • The execute command

- • Variable names



---

# readvar_and_response

# readvar and response

The readvar command and response functions can be used to prompt the user for input. readvar brings up a window with one or more entry fields in which text or values can be entered. The -value option enables the application programmer to present the user with a default value. If the user clicks on OK without entering a value, the default value is used.

The following two examples include a readvar with one entry field with a default value of "Mr.X" and a readvar with three entry fields.

```
readvar -prompt "Enter your name:" -value "Mr.X" name
readvar -prompt "Height:" -choice '5.5|8.5|11' h
-prompt "Width" -choice '8|11|16' w
-prompt "Depth" d
```

The first command prompts the user with only one entry field in which to enter his or her name. In the second example, there are entry fields with choice boxes for the height and width, and an entry box for the depth.

The response function creates a number of buttons in a special window, and returns a value indicating which button was clicked. The value of the button correlates to its place in the argument.

For example, the user is given three choices in the following example:

```
$choice=response("Are you ready?","yes","no","maybe")
```

When a user clicks on yes in the window, $choice is set to 1 . Clicking no sets $choice to 2 . Clicking maybe sets $choice to 3 .



---

# Relational

# Relational

It is important to note that the order in which items appear in this table are arbitrary. All operators have equal precedence to ACL.

The relational operators ( < , > , <= , >= , == , and != ) use arithmetic comparisons if both operands are numerals; otherwise, string comparisons are used. White space may delimit operators, but it is not required.

The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Row_Table_Attributes

# Row Table Attributes

In addition to the attributes listed in the Shared table attributes help topic, the following attributes are supported on row table objects.

## Related Topics

- • Table object attributes overview

- • Shared table attributes

- • Set table attributes

- • Grid table attributes

- • Column table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_get

- • tbl_obj_attr_set



---

# Rule_Table_Attributes

# Rule Table Attributes

In addition to the attributes listed in the Shared table attributes help topic, the following attribute is supported on rule table objects.

## Related Topics

- • Table object attributes overview

- • Shared table attributes

- • Set table attributes

- • Grid table attributes

- • Column table attributes

- • Row table attributes

- • Cell table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_get

- • tbl_obj_attr_set



---

# Set_Option_Scope

# Set Option Scope

Each set option has a scope which defines how it can affect your Arbortext Editor session. Set options use the following scope definitions:

- • Session — Almost all set options have a session scope. The session scope encompasses all the views in all the windows of the current Arbortext Editor session. The catalogpath and graphicspath set options are examples of set options that have a session scope, but no local scope; such options are said to be “global” options.

- • Preference — Not all set options are saved in the preference file. If a set option is a preference, then it is used to create the first edit window when Arbortext Editor is started. Changing the local or session scope of a set option does not change its preference setting. Use the write_preferences function to set preferences.

- • Local — Some set options have a local scope, meaning that the set option is controllable locally, without changing the session setting. The local scopes are:



---

# Set_Table_Attributes

# Set Table Attributes

In addition to the attributes listed in the Shared table attributes help topic, the following attributes are supported on set table objects.

## Related Topics

- • Table object attributes overview

- • Shared table attributes

- • Grid table attributes

- • Column table attributes

- • Row table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_get

- • tbl_obj_attr_set



---

# Setting_Values_for_Variables

# Setting Values for Variables

An assignment statement of the format $ varname = expression (where expression represents the new value for the variable) can be used to create a new variable and assign a value to it. You can also use this form of assignment statement to change the value of an existing variable. The expression must be terminated by the end of the command line or a semicolon (;). The assignment statement can be typed at the Arbortext Editor command line or entered in a command file (such as your docname .acl file). The new value will be recognized for the current editing session.

To change the value of an existing variable, you can:

- • use an assignment statement to give the variable a new value

- • reassign the value of the variable using an assignment operator (a subclass of expression operators)

- • use the increment (++) or decrement (– –) operator

For example, you might use one of the following assignment statements to change the value of a variable:

```
$i++
$n += 5
```

The command unsetvar and the delete function allow you to “undo” the definition of a variable.

Note that the variables $currentline , $dirselect , $selection , $tagname , and $topline are read-only, and their values may not be changed.

## Related Topics

- • Creating your own variables

- • Predefined variables

- • Using variables

- • The execute command



---

# Shared_Table_Attributes

# Shared Table Attributes

The following attributes are supported on all table objects (sets, grids, columns, rows, cells, and rules).

## Related Topics

- • Table object attributes overview

- • Set table attributes

- • Grid table attributes

- • Column table attributes

- • Row table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_get

- • tbl_obj_attr_set



---

# Shift_Operators

# Shift Operators

It is important to note that the order in which items appear in this table are arbitrary. All operators have equal precedence to ACL.

The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# Shortcut_Menus

# Shortcut Menus

You can create custom shortcut (popup) menus.

A shortcut menu is specified by using a colon as the first character of the menu path instead of a period.

To define a shortcut menu, specify : as the destination argument on the menu_add command. For example, this defines an abbreviated Edit menu, which could be posted in the Command window:

```
menu_add -menu : cmd -title "Command"
menu_add :cmd. Cut -cmd {delete_mark;} -key control-x
menu_add :cmd. Copy -cmd {copy_mark;} -key control-c
menu_add :cmd. Paste -cmd {paste;} -key control-g
menu_add :cmd. Delete -cmd {delete_mark null;}
```

The menu_load command may also be used to define shortcut menus. A shortcut menu is defined in the same way as a button menu, except the top-level definition for the shortcut menu is written using PopupMenu instead of Menu . A shortcut menu may not be referenced inside a Buttons section of the menu.cf file.

A user-defined shortcut menu is posted using the menu_popup function. The menu command posts the built-in menu for the current window. You need to map a key combination or mouse button to the function so users can access the menu. For example:

```
map m2 menu_popup("cmd")
```

where cmd is the name of a shortcut menu previously defined by a menu_load or menu_add command (as shown in the example above). The mapping could also be to a function that decides to post one of several shortcut menus based on the current position of the cursor or mouse.

A shortcut menu may be posted in any window. However, for performance reasons, it is often better to define a separate shortcut menu for each window. If a menu is posted in a different window than where it was last displayed, the window system objects in the previous window have to be destroyed and recreated in the new window.

The names of the built-in menus for the various window classes are shown in the table.

## Related Topics

- • Modifying the default menus

- • Menu paths

- • Special characters in menu paths



---

# show_commands

# show commands

Use the show command to display information about an option . The syntax for the show command is show option .

Following is a list of supported options for the show command:



---

# Size_Limits_for_ACL_Variables

# Size Limits for ACL Variables

There is no size limit for a string-valued variable. However, the command parser limits the size of any command argument or string token to 4095 characters. For example, if both $b and $c are 2500 characters long, then the following example creates a variable that is 5000 characters:

```
$a = $b . $c
```

The variable $a shown above is too long to be substituted into a command at the Arbortext Editor command line. Therefore, typing the following would result in a parser error:

```
find "$a"
```

This variable could, however, be used in an expression or function call. Here is an example:

```
$d=substr($a,1500)
insert($a)
```

The show variables command gives you a listing of all defined variables and their values.



---

# Special_Characters_in_Menu_Paths

# Special Characters in Menu Paths

A number of special characters can be used in the menu path to specify patterns, providing a compact way of expressing complex menu names.

As with regular expressions, most special characters can be preceded by a back slash (\) when you do not want them to be treated as special characters.

The special characters are listed below:

## Related Topics

- • Modifying the default menus

- • Menu paths

- • Shortcut menus



---

# Storing_a_Buffer_from_One_Session_to_the_Next

# Storing a Buffer from One Session to the Next

To save the contents of the named paste buffers from the current session for use in future editing sessions, use the save_buffers command or options on the write command: -paste or -buffer buffername . Otherwise, named paste buffers created during an editing session are removed when you exit Arbortext Editor .

The save_buffers command creates a buffername .apb file for each named buffer and puts these files in the specified directory. By default, the files are placed in the directory containing the document.

In this example, you created the named buffers pl and warningtext in this editing session and you want to save them for future use. At the command line, enter: save_buffers . This creates the files pl.apb and warningtext.apb in the user directory.

As another example, you want to save named paste buffers for a specific document type in a separate directory called nambufs . At the command line, enter:

```
save_buffers nambufs
```



---

# String_Concatenation

# String Concatenation

Use a dot (.) as the concatenation operator to merge two strings into one string. You can also use a dot to concatenate a combination of string variables.

The following example shows how dot concatenation is used to set the value of $filename to datafile.txt .

```
$textfile="datafile"
$extension=".txt"
$filename=$textfile . $extension
```

The following example shows how to use the dot operator to concatenate a combination of strings and string variables:

```
$firstname="John"
$lastname="Smith"
$myname="My name is " . $firstname ." " . $lastname . "."
```

In the example above, the value of $myname is My name is John Smith .



---

# Symbolic_Parameters

# Symbolic Parameters

A symbolic parameter is a variable, such as $1 or $2 , whose value is defined by the context within which it is used. Symbolic parameters can be used to define arguments for aliases. For example, a generic alias can be used to replace a specific string in a document by a different string. If the alias is used more than once for different replacement strings, the following alias using symbolic parameters would be a solution.

```
alias replace_string {
find $1
delete_mark
insert_string $2
}
```

When the command replace_string "Peter" "John" is run, the alias uses the first argument ( "Peter" ) in the find command and the second argument ( "John" ) in the insert_string command. The result would be that the first occurrence of the string Peter after the cursor (in the document) would be replaced by the string John .

Arbortext Editor allows you to supply parameters to the alias command. This means that you can define an alias, leaving a slot for information you will supply when you type the new command. This “slot” is indicated by the notation $1 , $2 , $3 , and so on, where $1 is the location where the first piece of information encountered is to be supplied, $2 is the location for the second piece of information, and so forth.

For example, if you have a tendency to type open at the command line as the command to open a different document, you can define the alias:

```
alias open edit $1
```

To move to the document ProposalA , you can type either edit ProposalA or open ProposalA at the command line.



---

# Table_Functions

# Table Functions

Table functions edit tables in the Edit window.



---

# Table_Object_Attributes

# Table Object Attributes

Attribute values are initially derived from table markup. Values may be manipulated by the following ACL functions:

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_get

- • tbl_obj_attr_set

Some values are numbers, some values are strings. String values are case insensitive.



---

# The_execute_Command

# The execute Command



For most commands, variables are substituted when Arbortext Editor compiles commands into an internal representation rather than when the command is executed. (The exceptions are the execute and eval commands, the if/else and for/while conditional commands, function calls, and variable assignment where variables are substituted when the command is executed.) This can pose problems with the map , alias , and print commands unless you used the execute command to defer evaluation of any variables until the action is triggered.

## Related Topics

- • Creating your own variables

- • Predefined variables

- • Setting values for variables

- • Symbolic parameters



---

# The_message_Command

# The message Command

The message command is useful for displaying specific information to the user. Running the command displays it on the status bar or, if the message cannot fit on the status bar, it will be displayed in a dialog box.

The message command is asynchronous. This means that when a message command is issued in a script, it does not wait for the user to click Dismiss before executing the rest of the script. The script continues execution regardless of the action of the user on this message.

The message command does not return any value or signal and is therefore not useful for dialog purposes.



---

# The_sh_Command

# The sh Command

Information can be processed by either Arbortext Editor , using ACL, or it can be passed to the operating system shell for processing. Various features of Arbortext Editor allow you to pass information between the shell and Arbortext Editor .

The sh command passes the given command(s) to the system shell.

The following example displays the Windows Character Map window which allows you to insert extended characters not found on all keyboards:

```
sh charmap &
```

Use the ampersand (&) when launching any program that displays a window. The ampersand allows Arbortext Editor to continue processing while the window is displayed.

sh runs the commands in a new shell. This means that you cannot use the command to set environment variables in the login shell ( cmd.exe ).

When running a single command, quotes around it are allowed but not necessary.

```
sh ls -lag
sh 'ls -lag'
sh "ls -lag"
```

When running multiple commands, or commands that contain curly braces ({}), quotes are necessary and the commands must be delimited by semicolons (;) For example:

```
sh 'cd c:\temp;dir *.xml'
```

Note that single quotes inhibit variable substitution. When a variable is to be substituted, use double quotes. For example:

```
sh "cd %HOME%;del *.tmp"
```



---

# Time_Functions

# Time Functions

Time functions return time information or create timers.



---

# Unary_Minus

# Unary Minus



The following operators are numeric and require numeric operands:

```
+, -, *, /, &, ^, |, <<, >>, %, ~, ++, and ––
```

## Related Topics

- • Functions as expressions and commands

- • Using expressions

- • Logical expressions

- • Operands



---

# User-Defined_Functions

# User-Defined Functions

You can define your own functions using this form:

```
function
name
(
parameter-list
)
{
commands
}
```

parameter-list can contain up to 50 scalar and array variables that are separated by commas. You declare an array variable by appending brackets ([]) to the variable name.

When a function is called, scalar variables are passed by value, and array arguments are passed by reference. You can force a scalar variable to be passed by reference by adding an ampersand (&) to the variable name. Take this function as an example:

```
function f(a, &b, c[]) {}
```

In the example above, the scalar variable "a" is passed by value. The scalar variable "b" and the array variable "c" are passed by reference.

As is the case in C++, you can give trailing arguments default values. Here is an example:

```
function f(n, m=10) {}
```

This example declares a function that may be called with one or two arguments. If only one argument is passed, the value of "m" is 10. The default value is an expression that's evaluated at the time of the call. Any variables that are referenced are in the scope of the caller.

The names specified in parameter-list are local to the function. All other variables are global. You can introduce additional local variables by using the local command, as shown in this example:

```
local x, y=10, z[]
```

This example declares scalar variables x and y and array variable z to be local to the current block, which ends with a right bracket (]). Scalar variables can be given initial values. In the example above, y has a value of 10 . The local command is an executable command, so default values are evaluated each time the command is executed. This also means it's not efficient to use local commands inside loops that are executed many times.

In the C programming language, you can declare a local variable that's already defined at the current level. You cannot do this in ACL. The following example illustrates this point:

```
function f(x)
{
# illegal, hides parameter
local x;
local m=1
{
# ok
local m=2;
# ok
local x[];
}
# illegal, hides previous value
local m;
}
```

In ACL, the local command is only allowed inside function definitions.

A function may return a value if the return command, which takes an expression as an optional argument, is used with the function. For example, function fac(n) { return n > 1 ? n * fac(n-1) : 1} is the most common factorial function. If no value is given for the return command, or the function fails to execute a return command, the result of the function is undefined. It's an error to refer to the result of the function in this case.

A function definition must appear at the outermost scope level. That is, you can't define a function inside a function, an alias, or a block. However, it is possible to define a function dynamically using the built-in execute function.

Functions must be defined before they are called. The function command defines the function name after the name argument is parsed. This allows recursive functions to be declared. You can declare a forward reference using this form:

```
function
name
() {}
```

Unlike aliases, the text of the function is not kept in memory, so there is no limit on the size of the function body.

Within a function definition, a variable term in an expression need not start with a dollar sign ($). Here is an example:

```
function backup_and_save()
{
local bakfile = filename. ".bak"
copy_file $filename $bakfile
save
}
```

However, the dollar sign is still needed to introduce variable substitution in commands that do not take expressions. The dollar sign is also required in double-quoted strings within expressions.

Also, unlike aliases, you don't have to add execute to commands in which variable substitution is done at parse time. In the example above, an implicit execute is added to the copy_file command, so the values of the variables are not used until run-time.



---

# Using_Conditional_Logic

# Using Conditional Logic

The Command Language has four commands available to conditionalize execution of commands to a specific condition. These commands are if , while , for , and switch .

The if , while , for , and switch commands do not change the $status variable (a predefined Arbortext Editor variable), unless a syntax error results during evaluation of the logical expression describing the conditions in which the commands are to be executed ( expr in the syntax statement above). In this case, $status is set to 2 and the statement is aborted.

If you are typing an if , while , for , and switch command at the command line, the entire command must appear on one line. However, if the command is read from a command file, the block of commands may extend across multiple lines. Line breaks can occur at command boundaries or, for a conditional command like if , while , for , and switch at the start of the command block, that is, before or after the left brace ({). If you need to break the line in the middle of a command, put a backslash at the end of the line preceding the break.

## Related Topics

- • Break and continue

- • Using looping and conditionals



---

# Using_Expressions

# Using Expressions

Expressions are used by the if/else , for/while , switch , and eval commands. Expressions are also used in function calls and in assigning variables.

For commands with expressions, evaluation of variables within the expression is deferred until the command is executed. With other commands, variables are substituted when the command is compiled, unless the execute command is used to defer evaluation.

## Related Topics

- • Functions as expressions and commands

- • Expression operator precedence

- • Logical expressions

- • Operands



---

# Using_Looping_and_Conditionals

# Using Looping and Conditionals

Until you become familiar with the syntax and power of logical expressions and variables, you may find it difficult to write if/else , while , and for commands.

The Looping and Conditionals help book contains examples of if/else, while, and for commands. By examining these examples, you will get a sense of how expressions and variables are used to build these commands.

Start by looking over the syntax statements for the if/else , while , and for commands. Then view the online help for variables and expressions . Finally, work through the examples in the Looping and Conditionals help.



---

# Using_Named_Buffers

# Using Named Buffers

Ordinarily, each time you copy or cut text, you replace the contents of the default paste buffer with the text you just copied or cut. Named paste buffers provide a way to save and retrieve paste buffers that contain text passages that you expect to reuse multiple times.



---

# Using_Regular_Expressions

# Using Regular Expressions

Regular expressions are used to construct simple to complex search criteria, as described in the following sections. Regular expressions are supported by the find , substitute , caret , and window ACL commands as well as the match , sub and gsub ACL functions.

There are two ways to use regular expressions in commands. The first is to specify the -e option as part of your command (see the syntax for the individual command for more information). The second is to use the command set expressions = on .

Regular expressions are normally delimited by the / character when used in commands, although you may use any standard command string delimiters. When used as string terms in functions such as match , they must be delimited with the standard string term delimiters " or ' . The rules for strings in double quotes apply before the regular expression is parsed: backslash sequences, such as \n (newline) and \t (tab), are replaced by the corresponding character and variable substitution is performed.



---

# Using_the_Interface_and_Dialog_Tools

# Using the Interface and Dialog Tools

The message and readvar commands and the response and list_response functions give the applications program a way to prompt for input from the user. You can also create non-blocking list selection dialog boxes using the window_create function.



---

# Using_Variables

# Using Variables



To use a variable, supply it in the command at the point at which you wish its value to be used. For example, suppose you want to know which line of a document the cursor is positioned in. You can't supply the line number explicitly without counting all the lines in the file, but you can use a command containing the variable $currentline to determine this value:

```
message "line: $currentline"
```

Entering this command at the command line displays the line number on the status bar.



---

# Variable_Assignment_and_Relation

# Variable Assignment and Relation

By default variable does not need a special declaration. It is declared when you assign a value to it.

There are three types of variables in ACL: integer, string, and character. Each variable type is preceded by a dollar sign ($).

Below is an example of each variable type:

ACL allows variable assignments that are similar to those used in the C programming language. For example:

Note that “/” is a division operator that uses integer arithmetic. This means that if $a==5 , the result of $a/3 is 1, not 1.6667.

The percent sign (%) is an operator that outputs the remainder of division arithmetic; thus, if $a==5 , the result of $a%3 is 2 .

ACL also allows abbreviated notation for increment operations. Here are some examples:



---

# Variable_Names

# Variable Names

A variable is a “word” in a command that begins with a dollar sign ($) and a letter (such as $a), or a dollar sign and an underscore (such as $_). Variable names can be up to 100 characters long, not including the dollar sign ($). Examples of variable names are $docname and $_currentline .

Although a variable must start with a letter or underscore (_), the remainder of the name can consist of letters, digits, and underscores. Uppercase and lowercase letters are distinct; that is, $ABC and $abc are different variables.



---

# Window_Manipulation_Functions

# Window Manipulation Functions

Refer the topics in the Window functions section of the online help, beginning with the topic current_event , for a listing of the available window manipulation functions. Also refer to the following examples:

- • Example of edit window function

- • Example of list response panel