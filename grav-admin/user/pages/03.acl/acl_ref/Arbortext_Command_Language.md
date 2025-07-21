

---

# Arbortext_Command_Language_Overview

Arbortext Command Language (ACL) is flexible enough for you to perform simple operations and develop complex applications. ACL incorporates many C programming language concepts. A basic knowledge of the C programming language will be helpful, but not necessary. ACL is also similar to awk and perl , so knowledge of these programs can be useful.

The following are some examples of what you can do using ACL:

- • write simple macros that increase user productivity

- • map specific keys to work in specific windows or classes of windows

- • redesign the menu system

- • build and control your own panels and windows

- • change the behavior of many “events” (for example, save, paste, modify tags, etc.) in the application

- • communicate with other applications using the Arbortext Editor Application Programming Interface (API)

- • build your own document management system



---

# Callbacks

# Callback Functions

Callback functions are user-defined functions called during specific events in Arbortext Editor that allow you to customize editing operations. Callback functions provide both a global and a local level of registration or notification to isolate events.

Refer to Callback functions introduction for a detailed introduction to ACL callbacks.



---

# Commands

# alias

alias newcmd { cmd1 | { cmd1 ; [ cmd2 ; …]} | {}}

This command maps cmd1 and any successive commands to the name newcmd . You can then execute the commands by typing newcmd at the Arbortext Editor command line, or by mapping the alias to a specific key on the keyboard.

To alias a command that has parameters (such as substitute ), you must include the parameters when specifying the alias or supply a symbolic parameter (such as $1 ), the value of which is to be supplied when the alias is used.

If you alias newcmd to more than one command, the commands to which it is aliased must be enclosed in curly braces. To define the alias name so that you can make a forward reference to it, use:

```
alias
newcmd
{}
```

The commands in an alias must be separated by a semicolon (;) if they appear on the same line. If each command resides on a separate line, a semicolon is legal but not mandatory. For example, you might define this alias:

```
alias setit { insert_tag figure-block; \
insert_string -sgml "<graphic>"}
```

To use the alias shown in the example above, type setit at the command line. Typing setit sequentially runs the commands defined in the “setit” alias.

Defining an alias in a file (for example, your user startup file) and then using the source command with this file does not actually run the alias. At this point, the system just defines the alias for Arbortext Editor . To actually use the alias shown in the previous example, you must type setit at the Arbortext Editor command line.

To easily access an alias, you can map it to a key on the keyboard. For example, you would enter the following to map the F3 key to the setit alias:

```
map F3 setit
```

Following are some additional examples of the alias command:

```
alias divide split
ali home caret top,first
ali replace sub $*
ali repl replace $*
ali mark_char {mark begin; caret 0,+1; mark;}
ali transpose {
caret 0,-2;
mark_char;
dm;
caret 0,+1;
paste;
}
# The following commands define individual aliases
# to define each of the three varieties of dashes
alias insert_hyphen {
insert_string -sgml "-X";
delete_character;
}
alias insert_ndash {insert_string -sgml "&ndash;"}
alias insert_mdash {insert_string -sgml "&mdash;"}
```

## Related Topics

- • unalias command

- • execute command

- • map command

- • readvar command

- • show variables command

- • Symbolic parameters

- • Command variables



---

# Functions_by_Alphabetical_Listing

# absolute_file_name

absolute_file_name ( filename [, dir ])

This function returns filename converted to an absolute path name. If filename is relative, the function prepends the directory dir if that directory is given; otherwise, the current working directory is used to make filename absolute.

If filename starts with ~ or contains any variable references, the name is expanded by calling expand_file_name . If filename contains the %L symbolic parameter, the name is expanded by calling locale_file_name . Arbortext Editor simplifies file names containing . or .. as components.



---

# Functions_by_Category

# Alias Map Functions



An alias map maps elements, attributes, and attribute values to new names or values. The alias map functions return the alias of the specified function as defined in the DTD.

- • attr_alias function

- • attr_description function

- • attr_real_name function

- • attr_value_alias function

- • attr_value_real_name function

- • tag_alias function

- • tag_description function

- • tag_real_name function



---

# Hooks

# Hook Functions

Hooks are user-defined functions that are called at strategic places by Arbortext Editor so you can customize editing operations. Setting a hook has global effect unless you build in additional user functions to specify a local level.

Refer to Hook functions introduction for a detailed introduction to ACL hooks.



---

# Repository_API

# Introduction to the Repository API

The Repository API allows Arbortext Editor authors to work with virtual documents made up of separate document objects that are stored and controlled independently. This makes it easy for Arbortext Editor users to share and reuse pieces of tagged text (SGML, XML, or HTML) in multiple documents. These individual components can be file entities or externally managed virtual documents. File entities and document objects may be edited directly within their parent document(s).

Stored document objects are accessed via the Repository API. An additional set of Arbortext Command Language (ACL) functions are provided to handle the basics of object manipulation such as browsing, loading, and saving. The Repository API is generalized, and can be applied to a wide variety of document repositories. An Adapter is designed to handle the details of the interface between Arbortext Editor 's Repository API and a specific document repository.



---

# set_Command_Options

# set

set [ -all ] [ -session ] [ -preference ] [ -local ] [ option = value ]

Sets the desired option to the desired value .

The -all , -session , -preference and -local options control the set option scope . These options are mutually exclusive. Use only one at a time.

- • -all — Sets the session scope of the set option and the local scope (if any). All open windows redraw to reflect the update.

- • -session — Sets the session scope for the set option, leaving the local scope unchanged. This option is useful for changing a setting so it affects new windows, but does not change the appearance of currently open windows or the value used when determining what gets written to your preferences file.

- • -preference — Sets the session scope for the set option, leaving the local scope unchanged, and sets the value used when determining what gets written to your preferences file. This option is useful for preparing to call the write_preferences function when updating just an option's preference but not other session-specific values that may have changed.

- • -local — Sets the local scope for the set option, leaving the session scope unchanged. This option is useful for changing the appearance of the current view or document.

Many set options are available in the user interface using the Advanced Preferences dialog box . (Choose Tools > Preferences and then choose the Advanced button.)

The complete list of set command options are available from the online help table of contents by choosing Arbortext Command Language (ACL) > Commands > Commands > set . The command options are also listed alphabetically in the online help index.

## Related Topics

- • option function — Retrieves values used by the set command.

- • option_scope function — Retrieves the scope of a specified option.



---

# Using_the_Arbortext_Command_Language

# Testing and Debugging ACL Scripts

Use the source command to test ACL scripts. For example, if you have several ACL commands in a file called pubcom.acl , you can test the effect of these commands on Arbortext Editor by typing source pubcom.acl at the Arbortext Editor command line. If this file isn't in the current working directory, you will need to enter the path and file name. For example: source test/pubcom.acl

Running the source command actually runs all the commands in the pubcom.acl file as if you had typed them on the command line.

If the file that is sourced contains any syntax or other errors, a message appears explaining the nature of the error. This makes the source command useful for debugging ACL scripts.

## Related Topics

- • source command