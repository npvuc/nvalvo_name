

---

# ACL_Syntax_Conventions

# ACL Syntax Conventions

These are the conventions used to present ACL command syntax in this document:

- • Command syntax statements appear in boldfaced type when they occur in the text flow.

- • Square brackets ([]) indicate an optional item. The command is still complete if the optional item is left out. For example:

- • A vertical bar (|) separates options when you can choose from several. Here is an example of an ACL command with more than one option:

- • Curly braces ({}) surround choices when they are not optional. You must supply one item from a list that is surrounded by curly braces. Here is an example:

- • Items that appear in italics are tokens that indicate the type of information you must supply at that location. Do not type these tokens verbatim. Here is an example of an ACL command that contains a token.

- • In path names, the term Arbortext-path refers to the directory in which Arbortext Editor is installed at your site. When you see Arbortext-path , replace it with your specific path name.

This table summarizes the command syntax conventions:

You can enter ACL commands at the Arbortext Editor command line. You can also place ACL commands in a separate file that is executed when Arbortext Editor is first started or when a particular document is opened.

## Related Topics

- • Startup command files



---

# Arbortext_Editor_Command_File

# Arbortext Editor Command File

The _main.acl file is the first command file Arbortext Editor reads during startup. This file is located in the \packages subdirectory of Arbortext-path .

Because _main.acl is read early in the Arbortext Editor initialization, before any documents are opened, commands that manipulate menus (for example, menu_add and menu_move ) are not valid in this file. Typically, the _main.acl file is maintained by a system administrator.



---

# Character_Sets_and_Encoding

# Character Sets and Encoding

Arbortext Editor supports the import and export of both 8-bit (for example, ISO-Latin) and multibyte character encodings (for example, Shift-JIS and GB_2312-80). These character encodings are required for input, display, and publishing of the following languages:

- • Japanese

- • Simplified Chinese

- • Traditional Chinese

- • Korean

- • English

- • European (European characters are represented as character entities within Asian-encoded files)

Arbortext Editor supports the following character sets and encoding methods:

- • Adobe-Standard-Encoding

- • ISO-8859-1 through 9

- • ISO-10646-UCS-2

- • EUC-JP

- • Shift-JIS

- • Big5

- • GB_2312-80

- • KSC_5601

- • UTF-8

- • US-ASCII

## Related Topics

- • write command

- • edit command

- • read command

- • save_as command



---

# Displaying_a_Command_History

# Displaying a Command History

At the Arbortext Editor command line, to see a history of commands previously typed, use UP ARROW or DOWN ARROW , or the default keymappings CONTROL-P or CONTROL-N .



---

# Document_Command_Files

# Document Command Files

Arbortext Editor reads the document command files when you open a specific document.

The docname .acl file stores ACL code for a specific document. The docname .js file stores JavaScript code for a specific document.

Commands in the docname .acl and docname .js files override the commands in all previous command files.

You should save the docname .acl and docname .js files in the same directory as the docname document.

## Related Topics

- • Startup command files



---

# Document_Type_Command_Files

# Document Type Command Files

Before Arbortext Editor opens a document, it loads any associated document type command files.

The doctype .acl file stores ACL code used to define the application. The doctype .js file stores JavaScript code to define the application.

For example, in your doctype .acl file you might want to add a document type-specific directory to the graphicspath option using append_graphics_path in the doctype .acl file.

If you open another document of the same document type, Arbortext Editor will not reload the doctype .acl or doctype .js files.

Save the doctype .acl and doctype .js files in your doctypes directory.

## Related Topics

- • Startup command files



---

# Document_Type_Instance_Command_Files

# Document Type Instance Command Files

Arbortext Editor reads document type instance command files each time you open a document incorporating the corresponding document type.

The instance.acl file stores document-specific ACL code. The instance.js file stores document-specific JavaScript code.

For example, if you add a new menu to the instance.acl file associated with the DocBook document type, every time you open a new or existing DocBook document, Arbortext Editor will read the instance.acl file and add the new menu to the document.

This file is located in the document type application directory.

## Related Topics

- • Startup command files



---

# Getting_Online_Help_for_Commands

# Getting Online Help for Commands

Get online help for commands and command functions from the Arbortext Editor online help window. Also get help for commands or a specific command using the Command line.

## Locating online help for a command or command function in the online help

Open the online help Arbortext Command Language (ACL) section. This section contains several section covering commands, functions, callbacks and so on. View the specific topics you're seeking help on.

## Getting online help using the command line

At the Arbortext Editor window command line, enter any of the following commands:

- • For a list of commands:

- • For a specific command:

- • For a list of functions:

- • For an overview of callbacks:

- • For an overview of hooks:



---

# User_Startup_File

# User Startup File

You can create a user startup file to store user-specific key mappings, aliases, or functions. Use the APTRC environment variable to specify your user startup file.

Following is an example of a user startup file.

```
#shows all markup
alias tf set tagdisplay=full;
#hides all markup
alias tn set tagdisplay=none;
#spell-checks selection
alias ck spe -selection;
#insert caption element
map alt+shift+c insert_tag caption;
#insert fig-block element
map alt+shift+f insert_tag figure-block;
#inserts template for corporate indexing
map f4 {insert_tag indexterm;insert_tag indextopic}
```

## Related Topics

- • Startup command files

- • Creating keyboard shortcuts