

---

# appsave

# appsave

appsave [ -noprompt ] [ -copydt ] [ -copypacks ] [ -pedata | -pecompare ] [ -dir dir ] [ instance ]

The appsave command saves all the document, stylesheet, and environment information necessary to reproduce a software problem. If you are using the Arbortext Publishing Engine for document publishing, the Arbortext Publishing Engine configuration information that Arbortext Editor is using will also be saved with the rest of the application information. This information helps PTC Technical Support diagnose any problems you may be having.

Included with the saved information will be a directory named \portable_doc . \portable_doc will contain all the files necessary to open a valid version of the current document. portable_doc will contain the following items:

- • A modified copy of the current document at the time the appsave command is executed. If the document is a DITA map, the map will be replaced with a preliminary resolved document (a single monolithic document with no external references). If the document is not a DITA map, its entity references, XML inclusions, and content references will be resolved.

- • A \portable_doc_files subdirectory containing images and other files referenced by the current document. References to these files in the modified current document will be updated to refer to the files in the portable_doc_files directory.

The appsave command parses the top level XSL stylesheet to gather all of the includes and imports and move them to directories under the main XSL stylesheet location. The process recurses into all imports and includes, and the href attributes in each xsl:include and xsl:import are modified according to new relative locations. All absolute paths are changed to relative paths and moved to directories under the main stylesheet. All includes and imports that require network access (such as http , https , and ftp ) are left as is.

The appsave command has the following optional arguments:

- • -noprompt — Suppresses the dialog boxes related to the appsave process.

- • -copydt — Saves your custom DTD if it's installed someplace other than the Arbortext-path \doctypes directory or the Arbortext-path \custom\doctypes directory. Document types found in either of these directories are automatically included.

- • -copypacks — Saves all information and files associated with an installed Arbortext application .

- • -dir dir — Specifies the directory where the information will be saved. If no directory is specified, the default will be appsave\ architecture \ doctypename .

- • instance — Specifies the document instance to use. If no instance is specified, the current document will be used.

- • -pedata — Transmits the current document to Arbortext Publishing Engine , which will open the document and generate an application save from the server. It will include the data requested from the choices for -copydt and -copypacks . The application save will be returned to Arbortext Editor and put into the directory specified by -dir dir .

- • -pecompare — Reports a comparison of the local workstation’s publishing configuration and the Arbortext Publishing Engine server’s configuration. This option is available when you are publishing documents using Arbortext Publishing Engine and you do not specify -pedata .

## Related Topics

- • Contacting PTC Technical Support

- • Using Arbortext Publishing Engine for publishing documents



---

# attribute

# attribute

attribute



This command displays the characteristics of the character or tag before the cursor in the format:

```
caret
line,col
position
n
of
m
on window (
p
%)
character before caret is '
char
'
size font
shown at
screen-display-size
```

The line,col in the caret line represents the position of the cursor in the window: line indicates the screen line number of the current position of the cursor, and col indicates its inset from the left margin. n represents the offset or character position from the beginning of the document to the left of the cursor; m is the total positions in the document. p is the percentage this position represents. char is the character to the left of the cursor. size is the font size at which that character will be typeset, font is the font family to which the character belongs and, screen-display-size is the actual size at which the character is displayed in the Edit pane.

Example

```
att
```



---

# autoload

# autoload

autoload { func() file | alias file }



The autoload command defines the function named func or the alias named alias to be loaded from the file file . The name is defined so that subsequent references are valid, but the file is not read until the function or alias is executed. This permits command packages to be loaded on demand instead of being sourced at start up.

If file is not a path name, that is, does not contain any slashes, the list of directories given in the loadpath option is searched for a file named file . The default command file extension .acl is supplied if necessary.

If the function or alias name is already defined other than by an autoload command, the autoload command does nothing.

Examples

```
autoload version_panel version.acl
autoload sort() /packages/sort.acl
```

## Related Topics

- • Packages

- • require command

- • source command



---

# beep

# beep

beep



This command sounds a beep. Useful for removing a default mapping from a key or signaling an error in an alias or a function.

Example

```
beep
# This replaces the unwanted keymapping "alt+shift+p"
# with a beep; the beep indicates that the key no
# longer performs a useful function.
map alt+shift+p beep
```



---

# break

# break

break

Immediately exits the innermost enclosing while or for loop or case block of a switch statement.

Examples

```
break
# The following alias only works in ascii files
alias goto_line {
caret first,first;
caret 0,+1;
if ($currentline == 2) {caret first,first;}
$lnr = $1;
$n = 1;
while ($n < $lnr) {
caret 0,'(^$)|(^.)' -nows -e;
if ($status != 0) {
execute message "File only has $n lines.";
break;
}
$n++;
}
unsetvar n lnr
}
```

## Related Topics

- • continue command

- • for command

- • switch command

- • while command



---

# caret

# caret

caret { mouse | nextcell | prevcell | nextword | prevword | [ window | nextwindow | prevwindow] [ warp | nowarp] [line,col] [ -c | -noc ] [ -e | -noe ] [ -t | -not ] [ -wrapscan | -nowrapscan ] [ -q | -noq ] [ -screen | -noscreen ] [ -arrow | -noarrow ]}

The caret command is used to change the location of the cursor.

- • caret mouse — Positions the cursor at the current mouse arrow location. Note that if you are mapping a key to caret mouse , it is often desirable to precede the caret command with a clear_mark command . Typically, it is not recommended that you use caret commands in scripts, as the command is affected by the screen position. The absolute form of the caret command is meant to be typed at the command line or mapped to a key.

- • caret nextcell — Applies only when the cursor is in a table cell. This command moves the cursor to the end of the next cell in the current table. If the cursor is in the last cell of a column, it is moved to the first cell in the next row. If the cursor is in the last row and column of the table, it is moved to the first cell in the table.

- • caret prevcell — Applies only when the cursor is in a table cell. This command moves the cursor to the end of the previous cell in the current table. If the cursor is in the first cell of a column, it is moved to the last cell in the previous row. If the cursor is in the first row and column of the table, it is moved to the last cell in the table.

- • caret nextword — Moves the cursor to the beginning of the next word.

- • caret prevword — Moves the cursor to the beginning of the previous word.

- • The window command variable can be any of the following:

- • warp (the default) moves both the cursor and the pointer to the designated window. nowarp moves the cursor without moving the pointer. If click-to-type focus is used, then warp sets the keyboard focus to the specified window instead of moving the pointer.

- • The caret command positions the cursor immediately in front of the character at the specified screen location line,col where line is an integer representing the number of lines down on the screen (this includes blank lines) and col is an integer representing the number of characters and spaces (that is, columns) over from the left margin.

- • The -screen and -noscreen modifiers control whether invisible characters (for example, tags) are skipped when they aren't displayed. The -noscreen modifier specifies that no characters are to be skipped. The -screen modifier specifies that invisible characters should be skipped. If neither -screen or -noscreen are specified, the default is -noscreen . For an example of the -screen modifier, consider the following code fragment:

- • The -arrow and -noarrow modifiers are only used when -screen is set and the Edit window has tag display turned off. Setting -arrow specifies that invisible characters are not skipped (like -noscreen ), however, invisible generated text and the contents of collapsed items are skipped (like -screen ). If neither -arrow nor -noarrow are specified, the default -noarrow is assumed.

- • The remaining modifiers ( c , noc , e , noe , t , not , q , noq , wrapscan , and nowrapscan ) work like the modifiers for the find command.

Examples

```
# position caret at current mouse location
car mouse
car nextcell
car prevwindow
# second line, tenth column
car 2,10
# down two lines, right ten columns
car +2,+10
# this command moves the cursor to the next paragraph
# in the edit window without moving the mouse pointer
car edit nowarp 0,/<para>/ -t
car bottom+1,first
car -2,0
car current-2,current
car bottom,last
car last,last
car begin,current
car current,/ /
car cmd 1,1
car (bottom-top)/2,0
car 0,/apples|oranges/ -e
car 0,/Doctor/ -c
```

## Related Topics

- • Using regular expressions

- • window command



---

# cd

# cd

cd pathname



This command changes the current working directory to the directory specified by pathname . If pathname specifies a drive name only, then the current drive is changed.

Examples

```
cd /docs/book/chap1
cd ..
```



---

# change_entity

# change_entity

change_entity [ -all ] newname



This alias replaces the entity reference before the cursor with a reference to newname . When -all is specified, all occurrences are replaced.

ce is a synonym for change_entity .

Examples

```
ce diag
ce -all ati
```

## Related Topics

- • create_file_entity alias

- • declare_entity alias

- • declare_file_entity alias

- • declare_graphic_entity alias

- • declare_text_entity alias

- • delete_entity alias

- • insert_entity alias

- • insert_graphic_entity alias

- • modify_entity alias

- • modify_file_entities alias

- • modify_graphic_entities alias

- • modify_text_entities alias

- • rename_entity alias

- • undeclare_entity alias



---

# change_tag

# change_tag

change_tag [ [ -all ] newtagname | -panel ]

In the Edit view, this command renames the closest tag, tag pair, or entity reference to the left of the cursor to newtagname . In the Document Map view, this command renames the closest tag, tag pair, or entity reference to the right of the cursor if the cursor is at the start of a line (that is, between the element icon and the element name); you can control this behavior with the set docmapcurrenttag=off option.

Typing change_tag (or simply ct ) at the command line brings up a panel that serves as a palette of all tags in context at the point of the tag being changed. If you have applied an alias map to your document and Tags is the selected Mode , the Elements list will display aliases, rather than real names, for tags that have been assigned an alias. You must direct the panel to perform an action before you can continue working. Specifying -all renames all occurrences of the closest tag left of the cursor to newtagname . If no arguments are given in the ct command, -panel is the default, which causes the Change Tag panel to appear.

ct is a synonym for change_tag .

Examples

```
ct
ct _comment
ct -all ii
```

## Related Topics

- • set docmapcurrenttag command



---

# check_completeness

# check_completeness

check_completeness [ -full ] [output= outspec ]

This command checks whether all the components that are required by the DTD are present. If elements are missing, it provides a listing of problems and supplies missing elements where the fix is unambiguous.

It also checks for ID references for undeclared or multiply-defined IDs. In addition, it checks for mismatches for text IDs, such as saving text to a counter ID. By default, this command checks those parts of a document that have changed since a previous completeness check including file entities. If the -full option is specified, the entire document is validated including any SUBDOC file entities (SUBDOC is a rarely used SGML feature). If a document is saved and exited with its status incomplete, the next completeness check done on the document defaults to -full .

outspec can be any of the following:

- • The name of a file (this can be a complete path name). A right angle bracket ( > ) preceding the file name causes the result of the check_completeness command to be appended to the end of the file.

- • A question mark ( ? ) preceding the output file name. If the file name starts with a question mark, the file name is a variable name whose value is set to the output produced by the command. If the second character is a right angle bracket ( > ), the output is appended to the current value of the variable instead of replacing it.

- • An exclamation point ( ! ) preceding an output specifier. This suppresses the normal prompt to confirm overwriting an existing file.

cc is a synonym for check_completeness .

Examples

```
cc
cc -full
```

## Related Topics

- • doc_incomplete function



---

# clean_cache

# clean_cache

clean_cache [-verbose] [-noexec] [-help] [-size n ] [-time d ] [directory]

The clean_cache alias can be used to manage the auxiliary publishing files stored in the Arbortext Editor cache directory. The algorithm for selecting which directories to remove is based on the time a directory has spent in the cache without being modified. The available arguments are described below:

- • -verbose — Displays information messages while the alias runs.

- • -noexec — Displays a listing of the directories to be removed, but does not actually remove the directories.

- • -help — Displays command syntax.

- • -size n — Reduces the size of the cache to n Kilobytes.

- • -time d — Removes files that have been in the cache (unchanged) for d days or more.

- • directory — Specify the cache directory to clean. If not specified, Arbortext Editor uses the location set by the APTCACHE environment variable. If APTCACHE is not set, Arbortext Editor uses the default location. The default directory is typically C:\Documents and Settings\ username \Local Settings\Application Data\PTC\Arbortext\Editor\.aptcache .

## Related Topics

- • Set option scope

- • doc_clean_cache function

- • Disk space requirements and your cache directory



---

# clear_mark

# clear_mark

clear_mark [ ended | begun | all | noextend]



This command deselects the currently highlighted selection. The ended option (the default) clears the highlighting only if the selection is ended. The begun option clears the highlighting only if the selection has been started, but is not yet ended. The all option clears the highlighting regardless of the selection status. The noextend option clears the selection (as opposed to extending it), even if set extendselection = on .

clm is a synonym for clear_mark .

Examples

```
clm
clm begun
clm all
```

## Related Topics

- • copy_mark command

- • delete_mark command

- • mark command

- • set extendselection command



---

# comment

# comment

comment text



This command causes the command parser to ignore everything from the comment command to the next semicolon ( ;), the next right curly brace (}), or the end of the line—whichever comes first.

The pound sign (#) provides a second type of comment which suppresses everything that follows it on the line.

Comments can be used to annotate a file or to prevent commands from being executed.

com is a synonym for comment .

Examples

```
com The pscr alias prints the screen;
ali pscr print unformatted screen
# This is useful when working on documentation
# map f3 {it italic; is /Arbortext/; caret 0,+1}
alias C_ {comment};
# Uncomment message command when debugging
$d=$docname
$m=$d.".menu"; C_ message "$d/$m"; edit $d/$m
caret 0,/<.*>/; # put caret after next start tag
# The following alias redefines the "save" command
# to be nonoperative:
alias save {comment}
```



---

# compile_doctype

# compile_doctype

compile_doctype [ -nowarn ] [ -noprompt ] [[ -catpath ] [ cat-path ]] [' [-log ] [ log-path ]] [[ -dcl ] [ dcl-path ]] [[ -pubid ] [ public-id ]] [[ -toptag ] [ top-tag ]] [[ doctypeDir ] | dtdPath ] [[ -xml ] | -xml ]

The compile_doctype alias compiles the document type specified by the directory doctypeDir or the DTD file path dtdPath . If no parameters are specified, the Compile Document Type dialog box displays. This command is not supported for the compact installation of Arbortext Editor .

The -nowarn option ignores all warnings encountered during the compilation. By default, all errors and warnings are displayed in a message window.

The -noprompt option prevents display of the dialog box prompting the user to confirm all compilation parameters

The -catpath ' cat-path ' option allows the user to specify the catalog path to use for the compilation. The path entered must be enclosed in single quotes (for example, ' cat-path ' ). If you enter multiple directories in the path, separate each directory with a semicolon ( ; ). By default, the value of option('catalogpath') is used.

The -log log-path option allows users to specify a file path to redirect all messages, errors, and warnings generated during document type compilation. By default, the Arbortext Editor will display messages in the message window.

The -dcl dcl-path option specifies the path to the SGML Declaration for SGML document types. If you do not specify a path, Arbortext Editor will use the appropriate default. You do not need to specify a -dcl dcl-path if you are compiling XML document types. In Arbortext Editor , XML documents are compiled using predefined SGML Declaration values for XML.

The -pubid ' public-id ' option specifies the public ID to use to lookup using the catalog path the SGML Declaration to use in compiling the document type. This is used only if the -dcl option is not provided. You must enclose the ID in single quotes ( ' ) if the public-id option contains any white space.

The -toptag top-tag option specifies the top-level element for the document type DTD that is unwrapped, (no <!DOCTYPE wrapper). If this is not provided and the document type is one of the Arbortext Editor distributed document types (for example, DocBook), then the proper top-level tag is used.

The -sgml | -xml option specifies whether the document type is SGML or XML. If this option is not specified, the value of set compilesgml command determines the type.

## Related Topics

- • Compiling document types overview

- • set compilesgml



---

# continue

# continue

continue



This command starts the next iteration of the innermost nested command, enclosing the while or for loop.

Example

```
continue
```

## Related Topics

- • break command

- • for command

- • while command



---

# copy_file

# copy_file

copy_file { oldfile newfile | file1 [ file2 …] dir }

This command creates the file newfile as a copy of the file oldfile . The destination can be a WebDAV resource provided the target HTTP resource supports WebDAV.

In the second form, copy_file file1 [ file2 ] ... dir , each file name is copied to the specified directory which must already exist. The base name of the destination file corresponds to the original file name. If a source file name is a directory, the directory is recursively copied.

cp is a synonym for copy_file .

Examples

```
cp formlet.sgm /jjs
cp http://www.ptc.com/examples/testfile.xml /dkc
copy_file c:/temp/file.xml http://our_server/webdav/file.xml
cp c:\prj1\publ.sgm c:\prj2\arbortext
cp book.sgm book.acl /book
```

## Related topic

Opening, referencing, and saving files



---

# copy_keymap

# copy_keymap

copy_keymap name newname

This command creates a new keymap named newname as a copy of the keymap name . The keymap called name was created by define_keymap or copy_keymap commands or is a window class name such as edit , cmd , or helpwin . In the latter case, the new keymap will have all the user-level mappings for the specified class.

The new keymap starts out with the same mappings as name but subsequent map commands to name do not affect newname and vice-versa. If name is a prefix keymap, then newname is created as a prefix keymap.

The keymap newname must not be one of the predefined maps system or user or a window class name such as edit , cmd , or helpwin .

ckm is a synonym for copy_keymap .

Examples

```
copy_keymap edit edit2_map
ckm window7 save_map
```

## Related Topics

- • define_keymap command

- • keymap_exists built-in function

- • map command

- • set keymap command

- • undefine_keymap command



---

# copy_mark

# copy_mark

copy_mark [ -append ] [ -noclm ] [ buffername ]

This command copies the currently selected text to the specified paste buffer. If a buffer name is supplied, then that buffer is used. Otherwise the current paste buffer is used. By default, the selection is cleared after the selection is copied. If -append is specified, text is inserted at the end of the buffer rather than completely replacing its contents. If -noclm is specified, the current selection is not cleared.

Change tracking markup is never copied to a buffer on a cut or copy. What is copied is determined by the set viewchangetracking command. If the command is set to show changeshighlighted , then the changesapplied view of the selection is used instead.

cpm is a synonym for copy_mark .

Examples

```
cpm
cpm buf1
cpm -noclm
cpm -append buf1
```

## Related Topics

- • Creating a named paste buffer



---

# count_file_entities

# count_file_entities

count_file_entities

This command will report any file entity names and how many times they appear in the current document.

Examples

```
count_file_entities
```



---

# count_graphic_entities

# count_graphic_entities

count_graphic_entities

This command will report any graphic entity names and how many times they appear in the current document.

Examples

```
count_graphic_entities
```



---

# count_marked_sections

# count_marked_sections

count_marked_sections

This command will report any marked section names and how many times they appear in the current document.

Examples

```
count_marked_sections
```



---

# count_notations

# count_notations

count_notations

This command will report any notation names and how many times they appear in the current document.

Examples

```
count_notations
```



---

# count_text_entities

# count_text_entities

count_text_entities

This command will report any text entity names and how many times they appear in the current document.

Examples

```
count_text_entities
```



---

# create_file_entity

# create_file_entity

create_file_entity [ name [ sysid [ pubid [ type ]]]]

This alias creates a new document of the same type as the document being edited and then inserts, at the cursor, an entity reference to the new document. Any selected (highlighted) text is moved to the new document. If you simply enter create_file_entity with no arguments, you are prompted for an entity name and for the system and public identifiers (which are optional).

name is the file entity name, which is used to construct the reference. If you enter the name of a file entity that has already been declared and there are no conflicts with system and public identifiers for that entity, information from the existing declaration is used. If there are conflicts, you are prompted to resolve them. If the name you supply is unique, this alias constructs a file entity declaration for the new document and adds this declaration to the private markup section of the document instance being edited.

sysid is the system identifier for the file entity, which is also used as the path name for the document instance being created. If no system or public identifier is specified, the entity name is used as the file name, and the file is placed in the current working directory.

pubid is the public identifier for the file entity. An attempt is made to find this identifier in one of the catalog files in the directories identified by the set catalogpath option (typically the doctypes subdirectory of Arbortext-path ). If a mapping for the identifier is found in one of these files, then the path name to which the identifier is mapped is used as path name for the new document.

type is the type of entity. SUBDOC is the only supported option.

cfe is a synonym for create_file_entity .

Examples

```
cfe
cfe list-of-users
cfe users '/sys/usr-list' '-//ATI//ENTITIES User List//EN'
```

## Related Topics

- • change_entity

- • declare_entity

- • declare_file_entity

- • delete_entity

- • insert_entity

- • modify_entity

- • modify_file_entities

- • rename_entity

- • undeclare_entity



---

# create_text_entity

# create_text_entity

create_text_entity [ name [ type ]]

This alias creates a new text entity and then inserts, at the cursor, an entity reference to the new text entity. Any selected text is moved to the new text entity. If you simply enter create_text_entity with no arguments, you are prompted for an entity name.

name is the text entity name, which is used to construct the reference.

type is the optional type of the entity and the only supported option is CDATA ”. This only applies to SGML documents.

cte is a synonym for create_text_entity .

Examples

```
cte
cte product-name
```

## Related Topics

- • change_entity

- • declare_entity

- • declare_text_entity

- • delete_entity

- • insert_entity

- • modify_entity

- • modify_text_entities

- • rename_entity

- • undeclare_entity



---

# declare_entity

# declare_entity

declare_entity [ text [ name [ textstring ]] | file [ name [ sysid [ pubid ]]] | graphic [ name [ notation [ sysid [ pubid ]]]]]

This alias creates either a text, file, or graphic entity reference, as specified, prompting for input as necessary.

For explanations of the arguments, see declare_text_entity , declare_file_entity , and declare_graphic_entity .

de is a synonym for declare_entity .

Examples

```
de
de text atext Arbortext
de file copyright "USER-PATH/project1/copyright"
```

## Related Topics

- • change_entity

- • create_file_entity

- • declare_file_entity

- • declare_graphic_entity

- • declare_text_entity

- • delete_entity

- • insert_entity

- • insert_graphic_entity

- • modify_entity

- • modify_file_entities

- • modify_graphic_entities

- • modify_text_entities

- • rename_entity

- • undeclare_entity



---

# declare_file_entity

# declare_file_entity

declare_file_entity name [ sysid [ pubid [ type ]]]

This alias creates a file entity reference, prompting for input as necessary.

name is the file entity name, which is used to construct the reference. If you enter the name of a file entity that has already been declared and there are no conflicts with system and public identifiers for that entity, information from the existing declaration is used. If there are conflicts, you are prompted to resolve them. If the name you supply is unique, this alias constructs a file entity declaration for the new document and adds this declaration to the private markup section of the document instance being edited.

sysid is the system identifier, or path name, for the file entity.

pubid is the public identifier for the file entity. The identifier must be mapped in one of the catalog files in the directories identified by the set catalogpath option (typically the doctypes subdirectory of Arbortext-path ). When entered from a command file or the command line, the public identifier must be enclosed in quotation marks.

type is the type of entity. SUBDOC is the only supported option.

dfe is a synonym for declare_file_entity .

Examples

```
dfe
dfe ch1 '/doc/startup' '-//ATI//docarch man ch1//EN'
```

## Related Topics

- • change_entity

- • create_file_entity

- • declare_entity

- • delete_entity

- • insert_entity

- • modify_entity

- • modify_file_entities

- • rename_entity

- • undeclare_entity



---

# declare_graphic_entity

# declare_graphic_entity

declare_graphic_entity [ entity [ notation [ sysid [ pubid ]]]]

This alias creates a graphic entity reference, prompting for input as necessary.

notation is an SGML notation for the data type of the graphic.

sysid is the system identifier, or path name, for the graphic entity.

pubid is the public identifier for the graphic entity. The identifier must be mapped in one of the catalog files in the directories identified by set catalogpath option (typically the doctypes directory of Arbortext-path ). When entered from a command file or the command line, the public identifier must be enclosed in quotation marks.

dge is a synonym for declare_graphic_entity .

Examples

```
dge
dge turbogen tif '/ati/graphics/genr.tif'
```

## Related Topics

- • change_entity

- • declare_entity

- • declare_notation

- • delete_entity

- • insert_entity

- • insert_graphic_entity

- • modify_entity

- • modify_graphic_entities

- • rename_entity

- • undeclare_entity



---

# declare_ms_parameter

# declare_ms_parameter

declare_ms_parameter [ parametername [ status ]]

This alias defines a marked section parameter entity name, prompting for input as necessary.

status consists of status keywords and references to other marked section parameters. Status keywords, in order of precedence, are as follows:

- • IGNORE (abbreviated ig )

- • CDATA (abbreviated c )

- • RCDATA (abbreviated r )

- • INCLUDE (abbreviated in )

- • TEMP (abbreviated t )

References to other marked section parameter entities must be prefixed with a percent sign. To enter a status containing multiple keywords or any references to other marked sections, enclose the status string in quotation marks.

dmsp is a synonym for declare_ms_parameter .

Examples

```
dmsp note-to-editor ig
dmsp sgml-code CDATA
dmsp pass3 'ig t'
dmsp irish include
dmsp gaelic '%irish'
```

## Related Topics

- • insert_marked_section command

- • modify_marked_section command

- • modify_ms_parameters command



---

# declare_notation

# declare_notation

declare_notation [ notationname [ sysid [ pubid ]]]

This alias creates a notation declaration, prompting for input as necessary.

sysid is the system identifier, or path name, for the notation. If this string includes spaces or special characters (characters other than letters, digits, and underscores), the whole string needs to be enclosed in quotation marks.

pubid is the public identifier for the notation. To be used by Arbortext Editor , the identifier must be mapped in one of the catalog files in the directories identified by the set catalogpath option (typically the doctypes subdirectory of Arbortext-path ). When entered from a command file or the command line, the public identifier must be enclosed in quotation marks.

dn is a synonym for declare_notation .

Examples

```
dn
dn tex "/ati/help/tex.help"
dn cgm '/iso/cgm' 'ISO 82/4//NOTATION Clear text
encoding//EN'
```

The last example should be entered all on one line.

## Related Topics

- • modify_notation

- • modify_notations

- • rename_notation

- • undeclare_notation



---

# declare_text_entity

# declare_text_entity

declare_text_entity [ name [ textstring [ type ]]]

This alias creates a text entity reference, prompting for input as necessary.

name is the text entity name, which is used to construct the reference.

textstring is the text that replaces the entity reference in the formatted document. If this string includes spaces or special characters (characters other than letters, digits, and underscores), the whole string needs to be enclosed in quotation marks.

type is the type of the entity. CDATA is the only supported option.

dte is a synonym for declare_text_entity .

Examples

```
dte
dte hap HaPPSys
dte sgmled 'SGML Editor'
```

## Related Topics

- • change_entity

- • declare_entity

- • delete_entity

- • insert_entity

- • modify_entity

- • modify_text_entities

- • rename_entity

- • undeclare_entity



---

# define_keymap

# define_keymap

define_keymap [ -prefix ] name



This command creates a new keymap named name that initially has no keys mapped. name has the same syntax as variables names: it must start with a letter and is composed of letters, digits, and underscores. The keymap name must not be one of the predefined maps such as system or user , a window class name such as edit , cmd , helpwin , etc., or a window name as returned by window_name (for example, window4 , window7 , window11 ).

Key and mouse bindings may be assigned to the keymap using the map command. The keymap may be attached to the current window by using the command set keymap= name .

If -prefix is specified, then the keymap is created as a prefix keymap. A prefix keymap differs from a normal keymap in that it is attached to a window by a key press (termed a prefix key) and remains attached to the window only for the next key or button press. This allows a command or command list to be mapped to a sequence of key presses. For example, the key sequence CTRL+X , CTRL+S is mapped to the save command in the example that follows.

dkm is a synonym for define_keymap .

Examples

```
define_keymap -prefix ctrl_x_map
map @ctrl_x_map control-s save
define_keymap emacs
map @emacs control-x set keymap=ctrl_x_map
```

## Related Topics

- • copy_keymap command

- • keymap_exists built-in function

- • map command

- • set keymap command

- • undefine_keymap command

- • cmd_key command



---

# define_tag

# define_tag

define_tag [ newtagname oldtagname ]



This command creates the user-defined tag newtagname as an alias of the tag oldtagname . newtagname can be made up of any combination of letters, numbers, dashes (-), underscores (_), and periods (.). If tag names are not specified, it brings up the Create User-defined Tag dialog box, which prompts for this input.

dft is a synonym for define_tag .

Examples

```
dft invisibleindexterm indexterm
dft editor comment
```



---

# delete_buffer

# delete_buffer

delete_buffer [ -all | buffername ]



This command empties and deletes the specified paste buffer. If -all is specified, it empties and deletes all buffers, including the default buffer. If no buffername is specified, it deletes the contents of the default buffer.

db is a synonym for delete_buffer .

Examples

```
db
db -all
db buf1
```

## Related Topics

- • Creating a named paste buffer



---

# delete_character

# delete_character

delete_character [-f]

This command erases the character before the cursor. If the optional -f argument is set, the command erases the character after the cursor.

dc is a synonym for delete_character .

Example

```
dc
```



---

# delete_entity

# delete_entity

delete_entity

This command deletes the entity reference to the left of the cursor.

dle is a synonym for delete_entity .

Example

```
dle
```



---

# delete_lms

# delete_lms

delete_lms -all

delete_lms -all deletes all local modifications to the tag preceding the cursor (that is, it removes all attributes).

dlm is a synonym for delete_lms .

Examples

```
dlm
dlm -all
```

## Related Topics

- • oid_delete_attr function



---

# delete_mark

# delete_mark

delete_mark [ [ -append ] [ buffername ] | null]

This command deletes the currently selected region. If the deletespaces option is set to on , then delete_mark will also remove a space if the deletion would result in two consecutive spaces. The deleted region is moved to the paste buffer specified. If no buffer name is supplied, the current paste buffer is used (see set paste = buffername ). If the buffername is null , the selection is deleted without being copied to a paste buffer. If the -append option is selected, text is inserted at the end of the buffer rather than completely replacing its contents. This command corresponds to the Delete menu item on the default Edit menu.

dm is a synonym for delete_mark .

Examples

```
dm
dm bufA
dm -append buf2
```

## Related Topics

- • Creating a named paste buffer

- • set deletespaces command



---

# delete_tag

# delete_tag

delete_tag



In the Edit view, this command deletes the tag to the left of the cursor. In the Document Map view, this command deletes the tag to the right of the cursor if the cursor is at the start of a line (that is, between the element icon and the element name); you can control this behavior with the set docmapcurrenttag=off option.

For these purposes, tags are any of the following markup icons: element tag or tag pair, processing instruction, user-defined tag, or entity reference.

dt is a synonym for delete_tag .

Example

```
dt
```

## Related Topics

- • set docmapcurrenttag command



---

# detail

# detail

detail [[ -selection ] | -caret | -mouse | -all ] [ -full | -none | n | tagname | -toggle ]

This command collapses the contents of the specified tag pair to a plus sign with surrounding brackets, [+], or expands the contents of a collapsed structure. Special handling for divisions (such as chapters) causes the division heading text to continue to be displayed when the division is collapsed.

The first set of options determines the region on which the command operates:

- • -selection (the default) indicates the region that is currently selected (or highlighted) if there is a selection; otherwise, the region enclosed by the document tag pair (that is, the entire document). However, -toggle is not a valid option for -selection .

- • -caret indicates the region enclosed by the first tag pair to the left of the cursor.

- • -mouse can indicate one of two regions: the region enclosed by the tag pair to which the pointer is pointing or the region enclosed by the first tag pair to the left of the pointer.

- • -all indicates the region enclosed by the document tag pair (that is, the entire document).

The rest of the options determine how much detail to show:

- • -full expands all collapsed structures in the indicated region so that all detail is shown.

- • -none collapses all structures in the indicated region so that no detail is shown.

- • n allows you to type a number indicating the level of detail to be shown. If the number is entered without a leading + or - sign, detail is shown down to the n th level (relative to the beginning of the region being operated on) and collapsed below that. -n shows n less levels of detail. +n shows n more levels of detail.

- • tagname allows you to specify the type of tag pair to be collapsed. Arbortext Editor determines the nesting level for the first occurrence of the tag tagname , and then collapses everything from that nesting level down.

- • -toggle (the default) is used to alternate between two levels of detail. For -mouse and -caret , it toggles between collapsing and expanding the tag indicated. If less than full detail is currently shown and -all is specified, the current level of detail is remembered, and full detail is shown. If full detail is currently shown, then detail is shown to the last remembered level. -toggle is not a valid option for a selection.

- • -panel displays the detail dialog box to collapse or expand divisions.

Examples

```
det
det -1
det -all
det -selection par
det -all 5
det -selection +1
det -selection -1
det -all -toggle
```



---

# doc_flatten

# doc_flatten

doc_flatten { file | text | all} [undeclare]

This alias replaces the text and/or file entity references with the corresponding entity content. It always works on the entire document. The command should be used with caution, because when the document is saved, all data about the prior existence of entity references is lost. It is good practice to perform a File > Save As after running the doc_flatten alias. The following arguments control the scope of the alias' execution:

- • file — flattens file entities only.

- • text — flattens text entities only.

- • both — flattens both text and file entities.

- • include — flattens XIncludes only.

- • all — flattens all text and file entities as well as XIncludes.

By default, the entity declarations are retained. If the optional parameter undeclare is provided, then the declarations are removed.

## Related Topics

- • doc_flatten function



---

# edit

# edit

edit [ -newwindow | -ok ] [ -readonly ] [ -xml | -untaggedascii ] [ -encoding string ] [ -cc | -nocc ] [ -cd ] [ -stylesheet name ] [ -catalog dir ] [ filename | -last | -current ]

This command replaces the document in the Edit pane with the file specified by filename .

If a filename argument is not specified and the -catalog option does not specify a document entity, edit displays the Open dialog box.

This command has the following options:

- • -newwindow — Specifies that a new window be created to display the new document. If -newwindow is not specified, the new document replaces the current document. -nw is a synonym for -newwindow .

- • -ok — Opens the requested document without prompting you about unsaved changes to the current document or file. Unsaved changes will be lost. This option is ignored if -newwindow is used.

- • -readonly — Opens the requested document as a read-only document.

- • -xml — Specifies that the document to edit is an XML document. When this option is selected, a completeness check will not be performed (that is, -nocc is implied), and specifying -cc will have no effect.

- • -encoding — Determines the encoding of the document, as specified by string ; string must be one of the following strings:

- • -untaggedascii — Opens the requested ASCII document. SGML markup, if any, will not be interpreted. -untagged is a synonym for -untaggedascii .

- • -cc — Specifies that Arbortext Editor perform a completeness check when it opens a Arbortext Editor document. (By default, a completeness check will not be done if the document was saved in Arbortext Editor .) Using this option is recommended when opening documents which were created in Arbortext Editor , but were later edited with another program.

- • -nocc — Specifies that Arbortext Editor not perform a completeness check when opening a document. The document must be fully normalized according to SGML 's reference concrete syntax.

- • -cd — Specifies that Arbortext Editor should change its working directory to the directory containing the file that is opened.

- • -stylesheet — Specifies the stylesheet name be used in place of the default stylesheet for the Edit view. name is the path and file name of a stylesheet file. name can also be the base name of the stylesheet file (the file name without the path). If just the base name is supplied, Arbortext Editor first searches for the file in the document directory, and then the document type directory.

- • -catalog — Specifies the name of the directory dir containing an interchange catalog, which provides the document entity to be edited if no path name is specified. dir is prepended to the current set catalogpath option if not already present. If the interchange catalog specifies a FOSI for the document entity, this FOSI will be used for the Edit view unless the -fosi option is given.

- • -last — Displays the previously edited file.

- • -current — Reloads the current file.

Examples:

```
edit
edit -last -ok
edit -untag mailist
edit -r report
edit -nocc userman
edit -cd C:/test.xml
```

## Related Topics

- • Opening, referencing, and saving files



---

# eval_(Command)

# eval (Command)

eval expression1 [ , expression2 …] [output= outspec ]

This command evaluates each expression and displays the results in the message window.

The output of each expression is separated from the next by the value of the $OFS variable and terminated by the value of the $ORS variable. By default $OFS is a single blank and $ORS is a single newline character. The expressions may be printed to a file or pipe using the output= specifier argument. Refer to show aliases for a complete description of output option. Note that expressions are delimited by a comma. In this case, outspec can be any of the following:

- • The name of a file (this can be a complete path name). A right angle bracket ( > ) preceding the file name causes the result of the eval command to be appended to the end of the file.

- • An asterisk ( * ) indicating the message window. If preceded by a right angle bracket ( >* ), the output is appended to the message window instead of replacing its contents. Additional predefined message windows msgwin2 , msgwin3 , or msgwin4 use the specifier output=*2 , output=*3 , or output=*4 respectively.

- • A question mark ( ? ) preceding the output file name. If the file name starts with a question mark, the file name is a variable name whose value is set to the output produced by the command. If the second character is a right angle bracket ( > ), the output is appended to the current value of the variable instead of replacing it.

- • An exclamation point ( ! ) preceding an output specifier. This suppresses the normal prompt to confirm overwriting an existing file.

Example

```
eval (3 + 4) * 5
```

## Related Topics

- • Command variables

- • eval built-in function

- • Using expressions



---

# execute_(Command)

# execute (Command)

execute [ command | { cmd1 ; [ cmd2 ; …]}]

This command causes the command in the command subwindow to be performed (as does the ENTER key at the command line).

When used with the command option, it defers evaluation of variables until runtime. With the map , alias , and print commands, this means that evaluation is delayed until the action is triggered.

Examples

```
exe cp $filename $filename.bak
execute {cp $filename $filename.bak; save;}
exec print composed printer="\\HP100PS\PS686" file=$print_file
```

## Related Topics

- • Command variables

- • eval function

- • execute function

- • readvar command

- • show variables command

- • Symbolic parameters



---

# exit

# exit

exit

This command closes the current window. If you only have one window open, Arbortext Editor will close saving any changes made to the document.

Examples

```
exit
```



---

# find

# find

find { -panel | [ -b | -f ] [ -select | -noselect ] [ -c | -noc ] [ -word | -noword ] [ -e | -noe ] [ -entityscan | -noentityscan ] [ -markup '<tagname>'|'<entity>' | -t '<tagname>' | -not ] [ -in 'tagname' ] [ -wrapscan | -nowrapscan ] [ -q | -noq ] [ -graphic | -equation | -table | -s ] [ -p ] [ -r ] [ -d ] [/ string /]} [ -alias | -noalias ]

This command searches from the cursor in the specified direction (forward by default) for the first occurrence of the specified string (or the previous search string, if no string is specified). The search ignores generated text. The string you enter must be delimited by one of the standard delimiters.

To replace a string with a different string, use the substitute command .

- • -panel displays the Find/Replace dialog box.

- • -b searches backward.

- • -f (the default) searches forward.

- • -select (the default) highlights and selects the matched string.

- • -noselect positions the cursor at the end of the search string.

- • -c performs a case-sensitive search.

- • -noc (the default) finds a string regardless of how it is capitalized. The set case command sets this parameter for all subsequent searches.

- • -word (or -w ) finds a string only when it matches a whole word.

- • -noword (or -now ) matches strings even when they are part of a larger word

- • -e specifies that the search string is a regular expression. This means that some punctuation characters such as * , \ , and . perform special functions. For example, in find -e /p..t/ , the period . is a placeholder representing any character. The command would find “pret”, “port”, and “part”, as well as the string “p..t”.

- • -noe (the default) specifies that the search string is not a regular expression. The set expressions command sets this parameter for all subsequent searches.

- • -entityscan ( -es ) controls whether or not the find command will search the contents of entities.

- • -noentityscan ( -noes ) will prevent the search from including the contents of entities. For example, the command find -es /script would search for the word “script” and include entities. Setting this option overrides the set entityscan command.

- • -markup ( -m ) indicates that the search string contains one or more tags or entities. Tags are indicated by surrounding angle brackets; an end tag contains a slash. Entities start with an ampersand ( & ) and end in a semicolon ( ; ). For example, to search for the end of an italic tag pair, you might enter find -m '</italic>' . To search for a copyright symbol, you might enter find -m '&copy;' . To search for a comment, you might enter find -m '<_comment>' . (Similar searches would locate processing instructions.)

- • -t works like the -markup option except it does not find entities. This option is provided for backward compatibility; scripts should use the -markup option.

- • -not (the default) indicates the search string does not contain tags. The set tagscan command sets the default value for this parameter for all subsequent searches.

- • -in '< tagname >' searches the text within specified markup by specifying the tag name to search within .

- • -wrapscan (or -ws ) causes the search to wrap to the beginning of the file when the end of the file is reached. -wrapscan is the default.

- • -nowrapscan ( -nows ) prevents the search from wrapping. The set wrapscan command sets the default value for this parameter for all subsequent searches.

- • -q (for “quiet”) suppresses the “string not found” message generated when a search fails. This is useful for putting the find command in command files or aliases.

- • -noq (the default) displays a message when Arbortext Editor cannot find a string that matches the search string.

- • -graphic (or -gr ) searches forward to the next graphic in the document. Search strings are not permitted with the -graphic modifier.

- • -table (or -tab ) searches to the next table in the document. Search strings are not permitted with the -table modifier.

- • -s searches for the next special element (graphic, equation, or table) in the document. Search strings are not permitted with the -s modifier.

- • -p searches to the tag at the end of the current document division (the parent tag). It can be combined with -b to move back to the beginning of a division. Search strings are not permitted with the -p modifier.

- • -r repeats the search in the opposite (reverse) direction. Search strings are not permitted with the -r modifier.

- • -d searches for the mate of the square bracket, curly brace, parenthesis, or double quote directly preceding the cursor; otherwise, it searches for the closest delimiter and positions the cursor next to its mate. Search strings are not permitted with the -d modifier.

- • -alias specifies that the search string can contain element aliases, but not real names, if an alias map has been applied to the document. The default is -noalias .

- • -noalias indicates that the search string cannot contain element aliases, even if an alias map has been applied to the document.

The set case , set expressions , set tagscan , set entityscan , set markupscan and set wrapscan commands can modify the behavior of the find command.

If you use the find command in a script, be sure to use a valid string delimiter for the search string. You must supply either a matching close delimiter or place the string at the end of a line. For instance, find /therefore if it is the end of a line and find /therefore/ are both valid. Using {find /therefore} as part of another command specification isn't valid because the curly brace is a command group delimiter, not a string delimiter. By supplying the closing delimiter / , the command specification {find /therefore/} is now valid.

Examples

```
find -b /and
f -f /and
f /therefore
f -c /Therefore
f -noc /therefore
f -e /gr.y
f -noe /grey/
f -m '</emphasis> hunting'
f -m 'Our Company Name&copy;'
f -not /hunting/
f -p
f -r
f -d
```

When the search text does not contain tags, the -markup option is not specified, or the set markupscan preference is off , then inline tags and processing instructions are ignored when matching text. If a tag starts or ends a line, it is considered a word boundary and also limits a text match. For example, the search text two words would match two <emphasis>words</emphasis> , but would not cross paragraph boundaries to match the following:

```
two</para>
<para>words
```

Elements suppressed by the tag_display command can be recognized and operated on by the find command by setting set hiddentagscan to on .

## Related Topics

- • Using regular expressions

- • substitute command



---

# find_attr_string

# find_attr_string

find_attr_string [ string ]

This alias searches forward from the cursor in the current document for the next occurrence of an attribute value matching string . If you do not supply the argument, a response panel prompts you to do so.

For instance, if you wanted to find a paragraph tag with an id of p100 , you can omit the p and use 100 as the string and the find_attr_string command would still find it. If the attribute exists, the document text moves to show the highlighted tag and the cursor is placed to the right of the tag to facilitate modification.

fas is a synonym for find_attr_string .

Examples

```
find_attr_string 100
fas drw
fas 'diag.tif'
```

## Related Topics

- • find_attr_value command

- • find_id command



---

# find_attr_value

# find_attr_value

find_attr_value [ value ]

This alias scans forward from the cursor in the current document for the next attribute whose value exactly matches value . If you do not supply the argument, a response panel prompts you to do so.

For example, if you have <xrefs idrefs="abc def"> , the command find_attr_value “abc def” would find it. The command find_attr_value “abcdef” would not find it because the attribute values don't match exactly.

Another command you could use in this situation is find_id . find_id abc would find the IDREFS because find_id recognizes attribute values delimited by spaces.

fav is a synonym for find_attr_value .

Examples

```
find_attr_value p100
fav 1
fav "1pc+2pt"
```

## Related Topics

- • find_attr_string command

- • find_id command



---

# find_entity

# find_entity

find_entity entity

This alias searches forward from the cursor in the current document for the first occurrence of the specified entity reference.

fe is a synonym for find_entity .

Examples

```
find_entity bullet
fe ndash
fe alpha
```



---

# find_id

# find_id

find_id [ ID | IDREF ]

This alias scans forward from the cursor in the current document for the next element whose ID or IDREF attribute matches ID or IDREF .

The search can recognize different parts of an ID attribute if they are separated by delimiting spaces. If you do not supply the argument, a response panel prompts you to do so.

For example, if you have <xrefs idrefs="abc def" , the command find_id abc would find it. (Note that the find_attr_value abc command would not find it because the attribute values don't match exactly.)

fid is a synonym for find_id .

Examples

```
find_id abc
fid p100
fid center
```

## Related Topics

- • find_attr_string command

- • find_attr_value command



---

# find_pi

# find_pi

find_pi

This alias searches forward from the cursor in the current document for the next processing instruction, highlights the processing instruction tag, and moves the cursor to the right of the tag to facilitate modification.

fp is a synonym for find_pi .

Examples

```
find_pi
fp
```

## Related Topics

- • find_pi_string command

- • find_pi_value command

- • insert_pi command

- • Modify Processing instruction command

- • Touchup processing instructions

- • Finding processing instructions



---

# find_pi_string

# find_pi_string

find_pi_string [ string ]

This alias scans forward from the cursor in the current document (and wraps around) for the next occurrence of a processing instruction tag having a value matching string . If you do not supply the argument, a response panel prompts you to do so. If the string exists, the processing instruction tag is highlighted and the cursor is placed to the right of the tag to facilitate modification.

find_pi_string is the quickest way to find specific processing instruction tags or names of style options, where string is the tag name or style option.

Suppose you want to find a _kern processing instruction tag with attribute value set to 3pt . Use the following method:

fps is a synonym for find_pi_string .

Examples

```
find_pi_string newpage
fps italic
fps 'hyphen-point'
fps 'Pub _kern'
fps 'Pub _texmac Tex="$\circ$"'
```

## Related Topics

- • find_pi_value command

- • find_pi command

- • insert_pi command

- • Modify Processing instruction command

- • Touchup processing instructions

- • Finding processing instructions



---

# find_pi_value

# find_pi_value

find_pi_value [ value ]

This alias searches forward from the cursor in the current document for the next processing instruction with a value exactly matching value . If you do not supply the argument, a response panel prompts you to do so. If the string exists, the processing instruction tag is highlighted and the cursor is placed to the right of the tag to facilitate modification.

To determine the value for value, you can use the following method. For example, to find a string of 3pt within a _kern processing instruction tag:

- • Insert an example of a processing instruction tag with the same attribute values as the tag you want to find (for example, _kern tag modified to 3pt ). Highlight this tag.

- • At the command line, enter:

- • Press ENTER . An evaluation panel displays the value of the highlighted tag.

- • At the command line, type: fps followed by a space and the result from the eval $selection output (minus the delimiting angle brackets and initial question mark) surrounded by single quotes. For example:

- • Delete the example tag you inserted before pressing ENTER .

Examples

```
find_pi_value 'Pub _newpage'
fpv 'Pub _font Posture="italic"'
fpv 'Pub _hyphen-point'
fpv 'Pub _kern Amount="2pt"'
fpv 'Pub _texmac Tex="$\circ$"'
```

## Related Topics

- • find_pi_string command

- • find_pi command

- • insert_pi command

- • Modify Processing instruction command

- • Touchup processing instructions

- • Finding processing instructions



---

# for

# for

for ( expression1 ; expression2 ; expression3 ) { command-list }

for ( $ variable in $ array ) { command-list }

The first form of this command evaluates expression1 and then executes the listed commands while expression2 is true. At the end of each iteration, executes expression3 . This is equivalent to:

```
expression1
; while (
expression2
) {
command-list
;
expression3
;}
```

The second form of this command executes listed commands with the variable set to each subscript of the array. The subscripts are returned in order (from the lowest to the highest) for a normal array. If the array is associative, the subscripts are returned in arbitrary order. The command list must not contain another for ($variable in $array) statement over the same array.

Examples

```
# Display each of the variables in the
#array "$includes" on std out.
for ($i = 1; $i <= count($includes); $i++) {
eval "[$i], $includes[$i]" output=-;
}
```

```
# This alias creates a list of all valid tags
# in the current document:
tag_names($tags);
$list = " "
for ($i in $tags) {
$list .= delete($tags[$i]) . " "
}
```

## Related Topics

- • If, while, for, switch

- • Functions as expressions and commands

- • Command variables

- • Logical expressions

- • while command



---

# format

# format

format [ continue | onepass | allpasses | layout | quit | stop | help | tokendump | insert string | delete n ] [ force | auto] [ wait | nowait]

Use the format command to control the formatting process. This command is not supported for the compact installation of Arbortext Editor .

The following primary options are available.

- • format continue (the default) resumes or starts formatting. If formatting stopped due to an error, Print Preview will resume with the page containing the error.

- • format onepass makes one pass to reformat the entire document.

- • format allpasses formats the document as many times as is necessary to complete auxiliary entities such as citations, indices, and tables of contents.

- • format layout formats the document in the same way as the allpasses command and creates a layout file in addition to the dvi file.

- • format quit ends document formatting and unloads the formatter. The formatter will be reinitialized and reloaded if formatting is requested again.

- • format stop suspends document formatting; formatting can be resumed later with format continue .

The following commands are valid only when a preview or print job has been stopped by an error. They're useful for debugging formatter errors (as directed by Technical Product Support):

- • format help which requests a help message from the formatter.

- • format tokendump which displays what the formatter was processing when the error occurred.

- • format insert string which sends the specified string to the formatter for interpretation.

- • format delete n which deletes n tokens.

The auto and force options are mutually exclusive and control whether Arbortext Editor decides if formatting is necessary.

- • The (default) auto option lets Arbortext Editor decide whether the document needs to be formatted or not. Arbortext Editor will trigger formatting if the document has not been formatted yet during the current session, or if the previous formatting command left the document in the refmt-needed state, or if the document has been modified since the preceding formatting command. If the document instance is up to date with regard to formatting, then format auto will not reformat the document instance.

- • The force option means to perform at least one formatting pass regardless of whether Arbortext Editor thinks it is necessary.

The wait and nowait options control whether Arbortext Editor should wait for the format to complete before continuing to execute commands.

- • The wait option instructs Arbortext Editor to wait until the format process is complete before continuing with subsequent commands. If formatting fails, your function can return a non-zero error status and retrieve the error message from the variable main::ERROR .

- • The nowait option instructs Arbortext Editor to continue processing and perform the formatting in the background. This is what usually happens when you choose File > Print Preview or File > Print Published .

fmt is a synonym for the format command.

Examples

```
format
fmt cont
fmt onepass
fmt allpasses auto
fmt allpasses force wait
fmt quit
fmt stop
fmt help
fmt tok
fmt ins '\showthe\hsize'
fmt delete 5
```

## Related Topics

- • preview command

- • print command

- • Formatting pass reduction in ACL



---

# global

# global

global var1 [, var2 …]

The global statement (command) declares one or more scalar or array global variables in the current package. It has the same syntax as the local statement. A scalar variable can be given an initial value by assignment using the form var = expr; see the examples that follow. If no initial value is given, the variable is initialized to null.

An array is declared by appending "[]" to the variable name. In this case the array can be a normal or an associative array, depending on context and will grow as necessary. A fixed size normal (that is, non-associative) array may be declared by specifying the size of the array inside the brackets, for example, arr [10]. The size may be an expression, which is evaluated at run time. The size is also the upper bound of the array since the first subscript is 1. To declare a fixed size array with a different minimum subscript, use the form

```
global arr[lb..hb]
```

where lb and hb are expressions giving the low and high bounds of the array. Arbortext Editor will signal a run-time error if you attempt to access elements outside the bounds of a fixed-size array.

Examples

```
global doc_name
global win = -1, doclist[]
global n1 = -5, n2 = n1 + 10
global arr[n1..n2]
```

## Related Topics

- • Arrays and variables

- • local command



---

# help

# help

help [ -2 | -3 | -4 | -msg | -msgwin2 | -msgwin3 | -msgwin4 ] [ -title ' windowtitle '] [ -geometry WxH+X+Y ] [ -tag ] [ -file ] [ -mouse | topic ]

Typing help at the command line, without arguments, opens the Arbortext Editor Help Center and displays its default topic.

Supplying the various options opens the Help Center to a specific topic, opens tag help, or opens other ACL application windows as follows. (Only the -topic option affects Help Center.)

- • The numeric arguments -2 , -3 , -4 , -msg , -msgwin2 , -msgwin3 , and -msgwin4 refer to choices for multiple tag help or ACL application windows. These windows can be used to view multiple help messages at one time. They are also available to application programmers writing their own help.

- • -title lets you override the default window title with a name you supply within quotation marks. If windowtitle is not surrounded by quotation marks, the remainder of the command line is used as the title.

- • -geometry specifies the size and position of the desired help window. It is a string of the form WxH+X+Y , where W is the width, and H is the height of the window in pixels. X and Y specify the position of the window relative to:

- • -tag specifies that topic is the name of an element (tag) in the document type associated with the current document. The -tag option should be given to get help for a tag with the same name as the Arbortext Editor command (for example, index ).

- • -file allows you to specify an alternate Arbortext Editor help file or custom .chm help file. For example, if you want to open the Arbortext Change Page for Defense help file, you would specify:

- • -mouse displays a help message based on the context of the mouse arrow.

- • topic can be command names (for example, help set ), alias names (for example, help find_id ), ACL topics (for example, help functions ) or other terms. If topic is not recognized as a command, alias, or specific topic, the Arbortext Editor Help Center will open with the search results for topic .

hel is a synonym for help .

Examples:

```
help
help find
help declare_graphic_entity
hel -2
hel -msg -title 'Set Commands' set
hel expressions
help operators
hel logical expressions
help operands
help -tag link
```

## Related Topics

- • window_create function



---

# if

# if

if ( condition ) { cmds } [ else if ( condition ) { cmds } …] [ else { cmds }]

This command executes the commands listed only if the given condition is true. else if clauses let you specify alternative commands to be executed when alternate conditions are true. The else clause specifies a course of action to be taken if none of the conditions tested for are true. You may specify any number of else if clauses, but only one else clause.

cmds is a list of one or more commands. The list must be enclosed in curly braces. condition is a logical expression describing the case in which these commands are to be executed.

Examples

```
if ($doctype=="book") {
dft glossword font-change;
ms -global glossword TypeStyle=bold
}
if ( $answer == "yes" ) {
# do something
}
else if ($answer == "no") {
# do something else
}
else {
# try again
}
if (! access($file,"w") {
message "can't write file $file"
}
else {
write -buffer buf1 $file
}
copy_mark
if ($status !=0) {
message "You must select something first”
}
```

## Related Topics

- • If, while, for, switch

- • Functions as expressions and commands

- • Command variables

- • Using expressions

- • Logical expressions

- • while command



---

# insert_accent

# insert_accent

insert_accent accentname

This command places the specified accent on the first item to the left of the cursor if the item is a character. accentname is an entity name. Not all accent names are valid in all document types. The DTD for the document must define the appropriate accent entity as given in the following table.

The entity name may also be used as the accentname argument.

ia is a synonym for insert_accent .

Examples

```
insert_accent acute
ia macron
```



---

# insert_column

# insert_column

insert_column [before]

This command inserts one column after (or before if before is given) the column containing the cursor in the current table cell. This command is not valid if the cursor is not currently in a table cell.

Examples

```
insert_column
insert_column before
```

## Related Topics

- • caret (with nextcell and prevcell arguments)

- • goto_cell built-in function

- • insert built-in function

- • insert_row command



---

# insert_entity

# insert_entity

insert_entity [ name ]

This alias inserts the specified entity reference at the current cursor location, prompting for an entity name if none is supplied. The specified entity name must not be enclosed in quotation marks.

In the Edit view, the cursor is placed after the inserted entity. In the Document Map view, the cursor is placed before the inserted entity; you can control this behavior with the set docmappastecaret=off option.

ie is a synonym for insert_entity .

Examples

```
insert_entity
ie ati
```

## Related Topics

- • change_entity

- • create_file_entity

- • declare_entity

- • declare_file_entity

- • declare_graphic_entity

- • declare_text_entity

- • delete_entity

- • insert_graphic_entity

- • modify_entity

- • modify_file_entities

- • modify_graphic_entities

- • modify_text_entities

- • rename_entity

- • undeclare_entity

- • set docmappastecaret



---

# insert_equation

# insert_equation

insert_equation [ display | inline]



This command begins a new equation of the desired type at the cursor. The default is display .

Examples

```
insert_equation
insert_equ inline
```



---

# insert_graphic

# insert_graphic

insert_graphic [ tagname ]



This command inserts the graphic tag specified by tagname (for this tag) at the cursor. If tagname is not specified, the first, or primary, graphic tag listed in the DCF file is assumed.

If you are using the entity method of graphic support, you may wish to use the insert_graphic_entity command alias instead.

ig is the abbreviation for insert_graphic .

Examples

```
insert_graphic
ig symbol
ig piechart
```



---

# insert_graphic_entity

# insert_graphic_entity

insert_graphic_entity [ name [ tagname ]]

This alias:

- • Inserts the tag specified by tagname for an element identified as a graphic element in the DCF file.

- • Inserts the specified entity name in the first value field, prompting for an entity name if none is supplied.

ige is an abbreviation for insert_graphic_entity .

Examples

```
insert_graphic_entity
ige turbogen
ige caution symbol
```

## Related Topics

- • change_entity

- • declare_entity

- • declare_graphic_entity

- • delete_entity

- • graphic_tag_name

- • insert_entity

- • modify_entity

- • modify_graphic_entities

- • rename_entity

- • undeclare_entity



---

# insert_include

# insert_include

insert_include [ path ] [ parse ]

This alias inserts an XML inclusion to the specified path at the current cursor location, prompting for a path if none is supplied.

The optional parse can be ' xml ' (the default if not supplied) or ' text ', and populates the parse attribute on the include tag itself.

## Related Topics

- • insert_entity



---

# insert_marked_section

# insert_marked_section

insert_marked_section [ status1 [ status2 …]]

This command inserts a marked section around the selected region, if any, with the specified status keywords. Status keywords may be references to declared marked section parameters or may be marked section keywords.

ims is a synonym for insert_marked_section .

Examples

```
insert_marked_section %german
ims %english TEMP
ims %computer INCLUDE CDATA
ims INCLUDE
```

## Related Topics

- • declare_ms_parameter command

- • modify_marked_section command

- • modify_ms_parameters command



---

# insert_pi

# insert_pi

insert_pi [ processinginstruction ]

This alias inserts a processing instruction for non- Arbortext Editor applications, prompting for the processing instruction if none is supplied. In Arbortext Editor , a processing instruction is represented with a _pi markup icon that is locally modified to carry the instruction. Single quotes around a parameter preserve two or more embedded spaces.

Examples

```
insert_pi
insert_pi backslant
insert_pi 'a b'
```

The following command will hide generic processing instructions regardless of the tag display mode: tag_display -none _pi

To insert a Arbortext Editor processing instruction, use the insert_tag command.

## Related Topics

- • find_pi command

- • find_pi_string command

- • find_pi_value command

- • insert_tag command

- • tag_display (command) command

- • Modify Processing instruction command

- • Touchup processing instructions



---

# insert_row

# insert_row

insert_row [before]

This command inserts one row after (or before if before is given) the row containing the cursor in the current table cell. This command is not valid if the cursor is not in a table cell.

Examples

```
insert_row
insert_row [before]
```

## Related Topics

- • caret prevcell command

- • caret nextcell command

- • goto_cell built-in function

- • insert_column command

- • tbl_caret_col built-in function

- • tbl_caret_row built-in function

- • tbl_col_count built-in function

- • tbl_row_count built-in function



---

# insert_string_(Command)

# insert_string (Command)

insert_string [ -pendingdelete | -nopendingdelete ] [ -markup ] [ -buffer buffername | -paste ] [ -append ] / newtext

This command inserts newtext at the current cursor location.

If there is selected text in the document, the command replaces the text according to the current setting of the set pendingdelete command. You can override or force the insert_string command to replace or preserve the current selection with the -pendingdelete and -nopendingdelete options. If -pendingdelete is set, the string replaces any selected text. If -nopendingdelete is set, any selected text is preserved and the inserted text is added to the right of the selected text.

If -markup is specified, the new text is interpreted as an XML (or SGML) string. This allows you to insert markup, diacritics, or special structures such as tables.

The insert_string -markup command will interpret the processing instruction <?Pub Caret> to set the cursor to a specific position within the inserted fragment. For example, after the command: insert_string -markup "<par>abc</par>" is executed, the cursor is placed after the end </par> tag.

However, with the insert_string -markup "<par>ab<?Pub Caret>c</par>" command, the cursor is positioned after the letter b . The <?Pub Caret> processing instruction must come after a character or tag in the markup string. It is ignored if it occurs at the start of the string. To position the cursor before an opening tag, the form <?Pub Caret1> can be used, for example, insert_string -markup "<par><?Pub Caret1>abc</par>" would position the cursor before the starting <par> tag.

If the <?Pub Caret> processing instruction is not included in the string, the cursor is placed per the following rules:

- • If the cursor is in the Edit view, the cursor is placed after the inserted string.

- • If the cursor is in the Document Map view, the cursor is placed before the inserted string; you can control this behavior with the set docmappastecaret=off option.

The -buffer option places newtext in a named paste buffer; -paste puts it in the default paste buffer. The -append option causes the string to be appended to the current contents of the buffer; otherwise, the string replaces whatever is in the buffer.

is is a synonym for insert_string .

Examples:

```
insert_string /Note: /
is -pd /therefore/
is -markup /e&acute;lan/
is -markup "&ndash;"
is -markup "&mdash;"
is -buffer trademarkinfo /Arbortext Architect \
is a trademark of PTC/
```

## Related Topics

- • insert function

- • insert_tag function

- • insert_buffer function

- • Creating a named paste buffer

- • set docmappastecaret command



---

# insert_table

# insert_table

insert_table

The insert_table command opens the Select a Table Model dialog box in which you can choose a table model if the following conditions are true:

- • If your document type supports multiple table models.

- • set prompttablemodels is set to on .

- • The cursor is in a location in which it is valid to insert more than one table model.

Once you have chosen a table model or if your document type only supports one table model, the insert_table command opens the Insert Table dialog box (or the Insert HTML Table dialog box if you selected HTML as the table model). Specify the table configuration options in this dialog box.

Example

```
insert_table
insert_tab
```

## Related Topics

- • set prompttablemodels

- • tblmodelprompthook

- • tbl_model_prompt callback type



---

# insert_tag_(Command)

# insert_tag (Command)

insert_tag { [ -pendingdelete | -nopendingdelete ] tagname | [ -type ] [ -panel ]}



This command inserts the specified tag or tag pair ( tagname ) around the cursor or around currently selected text, if any. Note that paired tags are inserted as a pair.

If typed alone at the command line, insert_tag (or simply it ) brings up the Insert Markup dialog box that provides a list of tags that are valid at the cursor. The panel is context-sensitive meaning the tags in the panel will change as you move the cursor.

If you have applied an alias map to your document and Tags is the selected Mode , the list in the Insert Markup dialog box will display aliases, rather than real names, for tags that have been assigned an alias.

You can keep the Insert Markup dialog box on-screen and use it across editing windows.

Note that paired tags are inserted around a highlighted selection regardless of whether pending delete is on or off. However, if pending delete is on, the default for single (unpaired) tags is to replace highlighted text. If no arguments are given in the it command, then -panel is assumed and simply brings up the Insert Markup dialog box.

For insert_tag -[type] -[panel] , the command specifies the initial markup type to be displayed in the Insert dialog box. Replace -type with one of the following: -dtd (for tags defined in the DTD), -usertags (for user-defined tags), -pi (for processing instructions), -text (for text (general) entities), -file (for file (external) entities), or -ms (for marked section parameter entities).

it is a synonym for insert_tag .

Examples

```
insert_tag
it comment
it -pd tabstop
it -nopd enspace
```

## Related Topics

- • insert_tag function

- • set addrequiredtags command



---

# invoke_processor

# invoke_processor

invoke_processor

This command invokes the table processor. Place the cursor to the right of a table tag to bring up that processor with the invoke_processor command.

Examples

```
invoke_processor
inv
```

## Related Topics

- • link command



---

# join

# join

join

This command joins two adjoining elements of the same type. For this command to work, the cursor must be positioned between the end tag of the first element and the start tag of the second element, or just inside the start tag of the second element. This command also works when more than two adjacent tags of the same type are selected in the Edit view.



---

# js

# js

js JavaScript-expression

This command passes JavaScript-expression to the JavaScript interpreter. The JavaScript expression is passed as a single string argument to the javascript function or the jscript function (depending on the set javascriptinterpreter setting) for evaluation. Unlike other ACL commands, no variable substitution is performed.

If JavaScript returns a non-null defined result, it is displayed in the status line in the Edit pane. The JavaScript expression is evaluated in the global shared scope.

For example,

```
js Application.activeDocument.documentElement.tagName
js print("Hello" + " world!")
js Application.alert("Hello world!")
```

## Related Topics

- • javascript function

- • js_source function

- • jscript function

- • source command

- • set javascriptinterpreter



---

# link

# link

link [ caret | mouse] [ f | b]

link [ -uri uri | -idref idref ] [ -data data ]

This command traverses a link in the Edit view and executes any commands associated with the link. There are two forms of the link command. The first form is associated with link and linkuri callbacks in the doc_add_callback function. The second form is associated with linkto callback in the doc_add_callback function.

For the first form, the tag type determines the action taken. Examples are shown in the following table:

Following is a description of link command parameters for the first form of the command:

- • f (the default) — Traverses forward, establishing a new link to a target.

- • b — Traverses backward to the previous location.

Following is a description of link command parameters for the second form of the command:

- • -uri — Explicitly provides a URI value for the target for the link.

- • -idref — Explicitly provides an IDREF value for the target for the link.

- • -data — A string value that is passed to the linkto callback.

Examples

```
link
link mouse
link b
link -idref help1723
```

## Related Topics

- • doc_add_callback function



---

# load_buffers

# load_buffers

load_buffers [ directory ]



This command loads named paste buffers from the specified directory. If no directory is given, the current document directory is used. Buffers are saved with the save_buffers command.

lb is a synonym for load_buffers .

Examples

```
load_buffers
lb /ati/doc/publ/text
```

## Related Topics

- • Creating a named paste buffer



---

# local

# local

local var1 [, var2 …]



The local statement (command) declares one or more scalar or array variables local to the current block, which ends with the enclosing '}'. It has the same syntax as the global statement.

A scalar variable can be given an initial value by assignment using the form var = expr ; see the examples that follow. If no initial value is given the variable will be initialized to null.

An array is declared by appending "[]" to the variable name. In this case the array can be either a normal or associative array depending on context and will grow as necessary. A fixed size normal (that is, non-associative) array may be declared by specifying the size of the array inside the brackets, for example, arry[10]. The size may be an expression, which is evaluated at run time. The size is also the upper bound of the array since the first subscript is 1. To declare a fixed size array with a different minimum subscript, use the form

local arr [ lb .. hb ]

where lb and hb are expressions giving the low and high bounds of the array. Arbortext Editor will report a run-time error if you attempt to index outside the bounds of a fixed-size array.

It is an error to declare a local variable which was previously defined at the current level. See the following sample function.

The local command is only allowed inside function definitions.

Examples

```
function f(x, src[])
{
local doc, save_doc = current_doc()
local assoc[]; # declare associative array
local dest[count(src)];# declare dest same size as src
local x; # illegal, hides parameter
local m=1
{
local m=2; # ok
local x[]; # ok
}
local m; # illegal, hides previous value
}
```

## Related Topics

- • Arrays and variables

- • global command



---

# lookup

# lookup

lookup [ word ] [output= filename ]



This command displays definition or alternate spellings for the word supplied. Words that contain spaces must be enclosed in quotation marks. If no word is supplied, the definition or spellings displayed are for the word currently selected (or the word nearest the cursor, if there is no selection). Selections can be made from windows other than Arbortext Editor windows, as well. Words are checked against the Proximity/Merriam-Webster Linguibase. Note that the language used for the dictionary is determined by the position of the cursor in the document. You can set a language on individual tags in a document, so that language can vary based on the position of the cursor.

If output is specified, lookup writes the definition of the word to filename . Note that filename can be any of the following:

- • The name of a file (this could be a complete path name).

- • An asterisk ( * ) indicating the message window.

- • A dash ( - ) indicating standard output. (This is normally the window from which you start Arbortext Editor .)

- • A question mark ( ? ) preceding the output file name.

Examples

```
lookup
loo set
loo bicycle
loo "fork over"
```

## Related Topics

- • Supported authoring languages



---

# map

# map

map [ window | all] keyname { cmd1 | { cmd1 ; [ cmd2 ; …]}}

This command assigns command functions to keyboard characters and mouse buttons for the window specified. The value for window , which is a window class name or user-defined keyboard shortcut, can be any of the following:

- • edit , which designates the Edit pane.

- • cmd , which designates the command line.

- • helpwin (also called helpwin1 ), helpwin2 , helpwin3 , helpwin4 , msg (also called msgwin1 ), msgwin2 , msgwin3 , and msgwin4 designate multiple Help windows. Use msgwin for Arbortext Editor messages and output from the show , eval , and similar commands.

- • window name as returned by the window_name function.

- • @ name , which designates the name of a user-defined keyboard shortcut.

If window is a class name, the mapping affects all windows using the specified class keymap, otherwise it changes the mapping in the keymap defined by a previous define_keymap or copy_keymap command.

A list of several window classes can be made by using a plus sign (+) to separate the names. To subtract a window class from a list, use a hyphen (-). The option all is a synonym for edit+cmd . Note that the helpwins and msgwins are not included in the all option. To map a key for all possible window classes, use: map all+textwins . The textwins option is a synonym for helpwins+msgwins . The helpwins option is a synonym for helpwin1+helpwin2+helpwin3+helpwin4 . The msgwins option is the same as msgwin1+msgwin2+msgwin3+msgwin4 .

The default keymap is the one attached to the current window (normally the edit class user keymap).

The value for keyname can be any one of the following:

- • any of the letters a-z or A-Z ,

- • any of the punctuation characters on the keyboard,

- • any of the digits 0-9 ,

- • any of the function keys F1 , F2 , ... F35

- • any of the keypad keys:

- • any of the following name keys.

Commands can also be mapped to the mouse buttons. M1 and M2 designate the left and right mouse buttons on a two-button mouse. On a three-button mouse, M2 is the middle button and M3 is the right button. However, to use a three-button mouse on Windows, you also need to set the environment variable APTMOUSE to equal 3 . Any of the shift or control sequences may be used with any mouse button. In addition, the designation for the mouse button may be prefixed with Up- , Double- , or Triple- where:

- • Up maps a command to the release of the designated mouse button (commands not prefixed by “Up” are executed when the button is first pressed down)

- • Double maps a command to the second click in succession of the designated mouse button

- • Triple maps a command to the third click in succession of the designated mouse button

The map command accepts the abbreviations ctrl for Control , dbl for Double , and trpl for Triple . Note that mouse commands are additive; thus, before a command mapped to the third click of the right mouse button (Triple-M3) is executed, any commands mapped as M3, Up-M3, Double-M3 and Up-M3 would be executed, followed by Triple-M3 and finally Up-M3.

Commands can further be mapped to scroll wheel actions with scrollwheel . You must preface scroll wheel actions with either down or up to indicate whether the action is for scrolling the wheel down or up. For example, down+scrollwheel indicates the mapped command is triggered by scrolling the wheel down.

Examples

```
map BackSpace caret 0,-1
map all f1 caret next
map shift-f2 print unformatted screen \
header=none
map control-shift-alt-q quit ok
map control-d delete_character
map shift-alt-d {caret 0,+1; delete_character;}
map shift-M3 {caret mouse; menu;}
map shift-M1 caret mouse
map @mymap Control-y paste
map Double-M3 help
map all+textwins-cmd shift-UpArrow window -1,0
map all+textwins down+mousewheel ScrollWheelDown
map all+textwins down+mousewheel ScrollWheelDown
map all+textwins up+mousewheel ScrollWheelUp
map edit+textwins control+down+mousewheel ZoomDown
map edit+textwins control+up+mousewheel ZoomUp
```

## Related Topics

- • alias command

- • Command variables

- • execute command

- • menu_add command

- • readvar command

- • show variables command

- • Symbolic parameters

- • unmap command



---

# mark

# mark

mark [ -selection | -noselection ] [ -invert | -noinvert ] [ -word ] [ begin | end]

This command starts or terminates a highlighted selection at respective cursor positions. In cases where neither begin nor end is specified, begin is assumed unless a selection is already started, in which case end is assumed.

In general, -selection (the default) causes Arbortext Editor to claim ownership of the window system PRIMARY selection. The window system selection is not affected if -noselection is specified. However, if end is also given with -selection , then the primary selection is affected only if a non-empty region is marked; if the marked region is empty, then mark -select end clears the marking and the window system PRIMARY selection is unaffected.

The -invert and -noinvert options determine whether selected text can be highlighted on the screen.

The -word option causes the selection to be extended in whole word increments.

Examples

```
mark
mar begin
mar end
# This is the default mapping for the left mouse button
# It enables you to position the caret in
# another window without losing the selection.
map all m1 {clear_mark;caret mouse;mark -noselect begin;}
map all up-m1 {mark -select end;}
mar -noinvert
```



---

# menu

# menu

menu

This command opens a shortcut menu. The location of the cursor within your document determines which shortcut menu opens. For example, if the cursor is within a table, the menu command opens the Table shortcut menu.

Examples

```
menu
men
```



---

# menu_add

# menu_add

menu_add [ -before ] destination label [ -separator | [ -cmd { cmds }] [ -key keyname | -keytext " text "] [ -toggle ' togexpr '] [ -radio ] [ -active " actexpr "]]

This command adds an item to an existing menu where label is the name for the new menu item and destination is a menu path indicating the existing item that the new item should follow.

If destination or label contains spaces or special characters, it must be enclosed in quotes. Please note that underscores, spaces, and periods are not allowed for menu bar labels.

If -before is specified, the new item will appear before the destination item rather than after it.

label specifies the label displayed for the item. If label contains any variable references, for example, "Modify $tagname" , the variable's value is substituted into the label string each time the menu containing the item is posted. Note that the label string label must be enclosed in single quotes to prevent the command parser from expanding the variable reference when the command is parsed.

A mnemonic access key may be specified for the menu item by preceding the desired letter in label with & . To use a literal & in label , use two ampersands, for example, "Save && Exit" .

-cmd { cmds } indicates the commands to be executed when the new menu item is selected. If an item is mapped to more than one command, the commands must be enclosed in curly braces and separated by semicolons.

-key keyname specifies the accelerator key (used for keyboard shortcuts) displayed in the right-hand field of the menu item. To take effect, the accelerator key must be mapped to the command function using the map command; see the map command for a list of valid values for keyname . The keyname is abbreviated to reduce the size of the menu. For example, -key control+Z is displayed as Ctrl+Z .

If no commands are assigned to the menu item with the -cmd option, then the menu item executes whatever is mapped to keyname .

-keytext “ text ” adds the accelerator key text displayed in the right-hand field of the menu item. If “ text ” is none , then no accelerator is shown. The -keytext option is similar to the -key option except that the accelerator text is specified directly by text instead of by a keyname. Since the -keytext option requires more memory, the -key option is preferred. However, -keytext is useful for turning off accelerator text (using none ) and also for menu items mapped to multiple keys, for example, using prefix keymaps, since -key only allows a single key to be specified.

-toggle ' togexpr ' specifies that the menu item is a toggle item (that is, it displays a check mark if set). The string argument togexpr specifies an ACL expression to be evaluated when the menu is posted. If it evaluates to non-zero the menu item will be displayed with a check mark, otherwise, the check mark will be removed.

togexpr can also be surrounded with double quotes.

-radio specifies that the toggle menu item is part of a radio group, that is, it is one a set of mutually exclusive items. All adjacent toggle-type items with the -radio option are considered part of the group. Depending on the window system, a different icon is displayed for radio group items.

-active " actexpr " specifies an expression to be evaluated when the menu is posted that determines whether the menu item is enabled or disabled (grayed-out). If the expression evaluates to non-zero the menu item is selectable, otherwise, the menu item is grayed-out.

-separator specifies that this menu item is a separator line. In this case label should be a null string and no additional options are allowed.

To save menu additions across sessions, you must either write out your changes with the menu_save command (this creates a menu.cf file in the document directory which can be loaded automatically when the document is opened), or you can put your mappings in the docname .acl file for the document.

mad is a synonym for menu_add .

Examples

```
mad .File. "Make all caps" -cmd {tra uc}
mad -before .File.Make_all_caps "Capitalize first" \
-cmd {tra pc}
menu_add .Options. "" -separator
menu_add .Options. "Find &Expressions" \
-toggle 'option("expr")=="on"' \
-cmd {if (option("expr")=="on") {set expr=off;} \
else {set expr=on;}}
```

## Related Topics

- • map command

- • Modifying the default menus

- • Using menu paths

- • menu_add -menu command

- • menu_copy command

- • menu_change command

- • menu_delete command

- • menu_load command

- • menu_move command

- • menu_reset command

- • menu_save command



---

# menu_add_-menu

# menu_add -menu

menu_add -menu [ -before ] destination label

This command adds a menu to the menu bar. label is the name for the new menu and destination is a menu path indicating the existing menu that the new menu will follow. If -before is specified, the new menu will appear before the destination menu rather than after it.

To add a user-defined shortcut menu, you must specify the destination as : (colon) label . You must then add menu items to the shortcut menu, and post it using the menu_popup function .

To add items to your new menu, use the menu_add command without the -menu option.

The following example adds the Test menu to the menu bar after the Tools menu:

```
menu_add -menu .Tools "Test"
```

The abbreviation of menu_add is mad .

The following example adds the Test menu to the menu bar before the Find menu:

```
mad -menu -before .Find "Test"
```

## Related Topics

- • Modifying the default menus

- • Using menu paths

- • menu_add command

- • menu_copy command

- • menu_change command

- • menu_delete command

- • menu_load command

- • menu_move command

- • menu_reset command

- • menu_save command



---

# menu_change

# menu_change

menu_change path [ -label “ name ”] [ -cmd { cmds }] [ -key keyname | -keytext [ “ text ” | none | default]] [ -active [“ actexpr ”] | -inactive ] [ -toggle ' togexpr ']



This command changes an existing menu item. mch is a synonym for menu_change .

- • path is the menu path of the menu item to be changed.

- • -label “ name ” changes the label displayed for the item. If name contains any variable references, for example, -label "Modify $tagname" , the variable reference is substituted into the label string each time the menu containing the item is posted. Note, the label string name must be enclosed in single quotes to prevent the command parser from expanding the variable reference when the command is parsed.

- • -cmd { cmds } changes the command(s) associated with the menu item. The command must be enclosed in curly braces. Multiple commands are separated by semicolons.

- • -key keyname changes the accelerator key text displayed in the right-hand field of the menu item. See map for a list of possible values for keyname . keyname is abbreviated to reduce the size of the menu. For example, -key control-z is displayed as Ctrl+Z .

- • -keytext has three options, -keytext " text " , -keytext none and -keytext default .

- • -active [' actexpr '] specifies an expression to be evaluated when the menu is posted that determines whether the menu item is enabled or disabled (grayed-out). If the expression evaluates to non-zero the menu item is selectable, otherwise, the menu item is unavailable. If actexpr is omitted, the menu item is made active unconditionally.

- • -inactive specifies that the menu item be made insensitive (grayed-out). The item remains unavailable until a subsequent menu_change command enables it with the -active option. If the menu item is enabled using the -active option, it is still subject to be unavailable when posted (according to the context of the cursor). This context-sensitive graying is done only for menu items mapped to simple commands, such as delete_mark , insert_tag , undo . The optional string argument actexpr specifies an expression to be evaluated when the menu is posted. That determines whether the menu item is enabled or disabled (grayed-out). If the expression evaluates to non-zero, the menu item is selectable, otherwise, the menu item is grayed-out.

- • -toggle ' togexpr ' changes the -cmd menu item into a toggle item, which displays a check mark if set. The string argument togexpr specifies an expression to be evaluated when the menu is posted. If it evaluates to non-zero the menu item will be displayed with a check mark, otherwise, the check mark will be removed.

Examples

```
menu_change .File.Print -inactive
mch :EditPopup.Paste -key control-y
mch ".Options.Full Menus" -check
mch ".File.Preview.Current*" -label " to end"
```

## Related Topics

- • Modifying the default menus

- • Using menu paths

- • menu_add command

- • menu_add -menu command

- • menu_copy command

- • menu_delete command

- • menu_load command

- • menu_move command

- • menu_reset command

- • menu_save command

- • map command



---

# menu_copy

# menu_copy

menu_copy item [ -before ] destination

This command copies an item on a menu from one location to another. item is a menu path indicating the item to be copied and destination is a menu path indicating the existing item that the new item should follow. If -before is specified, the new item appears before the destination item rather than after it.

mcp is a synonym for menu_copy .

Examples

```
menu_copy .File.Save .Quick
mcp Insert_Table -before .Quick.Save
```

## Related Topics

- • Modifying the default menus

- • Using menu paths

- • menu_add command

- • menu_add -menu command

- • menu_delete command

- • menu_load command

- • menu_move command

- • menu_reset command

- • menu_save command



---

# menu_delete

# menu_delete

menu_delete item

This command deletes a menu from the menu bar or deletes an item from an existing menu. item is a menu path indicating the menu or item to be deleted.

mdel is a synonym for menu_delete .

Examples

```
menu_delete .Quick.Save
mdel .Quick
```

## Related Topics

- • Modifying the default menus

- • Using menu paths

- • menu_add command

- • menu_add -menu command

- • menu_copy command

- • menu_load command

- • menu_move command

- • menu_reset command

- • menu_save command



---

# menu_load

# menu_load

menu_load [ -d name [ -d name ]] [ -u name [ -u name ]] [ filename ]

A menu.cf file is a menu configuration file created and placed in the directory containing the document file when you use the menu_save command. menu_load loads the specified menu configuration file ( filename ). If no menu file is specified with menu_load , Arbortext Editor determines the menu configuration as follows.

- • The menu.cf file in the directory containing the document file is used.

- • If there is no menu.cf file in the directory containing the document file, then the menu.cf file in the directory specified by the environment variable $APTMENUFILE is loaded.

- • If menu.cf is not found in the path and directory specified by $APTMENUFILE , the default menu configuration file located at Arbortext-path \lib\editmenu.cf is loaded.

Therefore, to reinstate your default menu after loading a custom menu, use menu_load without specifying a menu file.

The -d option with menu_load defines the associated symbol name for the processor used to parse the menu.cf file.

The -u option with menu_load removes the definition of the associated symbol name for the processor used to parse the menu.cf file.

More than one name can be defined (or have its definition removed) by specifying multiple -d (or -u ) options.

Examples

```
menu_load menu.cf
menu_load /mdm/book.men
menu_load -u fullmenus
```

## Related Topics

- • Modifying the default menus

- • Using menu paths

- • menu_add command

- • menu_add -menu command

- • menu_copy command

- • menu_delete command

- • menu_move command

- • menu_reset command

- • menu_save command



---

# menu_move

# menu_move

menu_move item [ -before ] destination

This command moves a menu or an item on a menu from one location to another. item is a menu path indicating the menu or item to be moved and destination is a menu path indicating the existing item that the new menu or item should follow. If -before is specified, the new item appears before the destination item rather than after it.

mmv is a synonym for menu_move .

Examples

```
menu_move .File.New .File.Preview
mmv .File -before .Help
```

## Related Topics

- • Modifying the default menus

- • Using menu paths

- • menu_add command

- • menu_add -menu command

- • menu_copy command

- • menu_delete command

- • menu_load command

- • menu_reset command

- • menu_save command



---

# menu_reset

# menu_reset

menu_reset

This command resets all menus to the state they were when the menus were loaded. That is, if you have changed your current menus using menu_add , menu_delete , menu_move , or another menu modification command, the menu_reset will undo those changes.

Examples

```
menu_reset
```

## Related Topics

- • Modifying the default menus

- • Using menu paths

- • menu_add command

- • menu_add -menu command

- • menu_copy command

- • menu_delete command

- • menu_load command

- • menu_move command

- • menu_save command



---

# menu_save

# menu_save

menu_save [ -all ] [ -buttons ] [ -popups ] [ pathname ]

This command saves your current menu configuration in a file called menu.cf in the directory containing the document or to the path name that you specify. By default, Help and File menus are not saved; the -all option causes these menus to be saved as well.

-buttons specifies that the menus defining the menu bar buttons for the current window are to be saved. This is the default.

-popups specifies that the shortcut menus are to be saved. By default, only user-defined or changed built-in menus are saved. If -all is given, then all shortcut menus are saved.

To save the menu bar menus and the shortcut menus, specify both -buttons and -popups .

Examples

```
menu_save
menu_save -all /ati/doc/master.men
menu_save -all -popups popup.men
```

## Related Topics

- • Modifying the default menus

- • Using menu paths

- • menu_add command

- • menu_add -menu command

- • menu_copy command

- • menu_delete command

- • menu_load command

- • menu_move command

- • menu_reset command



---

# message

# message

message " text " [ " text " …]

This command generates a message window containing the specified text. Either single or double quotes can be used to mark the text. Every set of quotation marks contains a new line of the message. If the message command is read in from a command file, a line break may be introduced by putting a backslash (\) at the end of a line.

If the current window has a message area at the bottom of the window and the message is short enough to fit, it is displayed in the message area instead of a separate window.

Examples

```
message "sending print job to auxiliary printer"
mes "WARNING:" "This report is not yet approved."
mes 'Substitute command successful \
"QAP" changed to "Quality Assurance Program" \
in all cases'
mes "You are currently editing $docname."
```

## Related Topics

- • response function



---

# mkdir

# mkdir

mkdir [ -p ] pathname

This command creates a new directory specified by pathname . If -p is not included, all leading components in pathname must be existing directories, and only the lowest level directory will be created. When the -p option is given, mkdir will create a multiple-level directory structure.

Examples

```
mkdir techman
mkdir ../src
# The following command creates the entire directory structure.
mkdir -p 'c:\newdir\tests\monday'
```



---

# modify_entity

# modify_entity

modify_entity [ name ]

This alias opens a dialog box for any text, file, or graphic entity that has been declared in Arbortext Editor , allowing modification of its definition. If the entity name is not supplied, you are prompted for it.

me is a synonym for modify_entity .

Examples

```
modify_entity
me ati
```

## Related Topics

- • change_entity

- • create_file_entity

- • declare_entity

- • declare_file_entity

- • declare_graphic_entity

- • declare_text_entity

- • delete_entity

- • insert_entity

- • insert_graphic_entity

- • modify_file_entities

- • modify_graphic_entities

- • modify_text_entities

- • rename_entity

- • undeclare_entity



---

# modify_file_entities

# modify_file_entities

modify_file_entities

This alias brings up the file entities panel which displays name, number of uses, and system and public identifiers for all file entities (including those declared in the DTD).

You can use this panel to rename any file entities declared in the private markup section of the document instance, to locate instances of file entity use, and to modify system and public identifiers for entities declared in the private markup section.

mfe is a synonym for modify_file_entities .

Examples

```
modify_file_entities
mfe
```

## Related Topics

- • change_entity

- • create_file_entity

- • declare_entity

- • declare_file_entity

- • delete_entity

- • insert_entity

- • modify_entity

- • rename_entity

- • undeclare_entity



---

# modify_graphic_entities

# modify_graphic_entities

modify_graphic_entities

This alias brings up the graphic entities panel which displays name, number of uses, and system and public identifiers and notations for all graphic entities (including those declared in the DTD).

You can use this panel to rename any graphic entities declared in the private markup section of the document instance, to locate instances of graphic entity use, and to modify system and public identifiers and notations for entities declared in the private markup section.

mge is a synonym for modify_graphic_entities .

Examples

```
modify_graphic_entities
mge
```

## Related Topics

- • change_entity

- • declare_entity

- • declare_graphic_entity

- • delete_entity

- • insert_entity

- • insert_graphic_entity

- • modify_entity

- • rename_entity

- • undeclare_entity



---

# modify_marked_section

# modify_marked_section

modify_marked_section [ status1 [ status2 …]]

This command changes the status of the marked section before the cursor to the status specified, prompting for the new status if necessary. Status keywords may be references to declared marked section parameters or may be marked section keywords.

mms is a synonym for modify_marked_section .

Examples

```
modify_marked_section _ignore
mms %teachers
mms %trainers TEMP
mms %cobol INCLUDE CDATA
```

## Related Topics

- • declare_ms_parameter command

- • insert_marked_section command

- • modify_ms_parameters command



---

# modify_ms_parameters

# modify_ms_parameters

modify_ms_parameters [ parametername1 status1 [ parametername2 status2 …]]

If no parameters are given, this command brings up the Marked Section Parameters panel which displays name, number of uses, and status information for all marked sections declared in the private markup section of the document instance.

Otherwise, it sets parametername1 to status1 , parametername2 to status2 , and so forth. In order for this operation to work, the document must remain in context after all affected marked sections are changed. Otherwise, no changes will be made. Also, the document must be saved before you can apply changes to a marked section.

You can also use this panel to rename marked sections, to locate instances of use, and to modify status information.

mmsp is a synonym for modify_ms_parameters .

Examples

```
modify_ms_parameters
mmsp
```

## Related Topics

- • declare_ms_parameter command

- • insert_marked_section command

- • modify_marked_section command



---

# modify_notation

# modify_notation

modify_notation notationname

This alias allows you to modify the declaration of the specified notation, prompting for a notation name if none is supplied.

mn is a synonym for modify_notation .

Examples

```
modify_notation fax
```

## Related Topics

- • declare_notation

- • modify_notations

- • rename_notation

- • undeclare_notation



---

# modify_notations

# modify_notations

modify_notations

This alias brings up the notations panel which displays the name, number of uses, and system and public identifiers for all notations declared in the private markup section of the document instance. You can also use this panel to rename notations, locate instances of use, and modify system and public identifiers.

mns is a synonym for modify_notations .

Examples

```
modify_notations
mns
```



---

# modify_tag

# modify_tag

modify_tag [ -local [ tagname ] | -global [ tagname ] | -quick | -quickattr ] { [[ attr = value ] …] | [ -inline ] [ -modal ] [ -attr attrname ]}

In the Edit view, this command opens the Modify Attributes dialog box for modifications to either the tag or entity reference immediately before the cursor, or the specified tag or entity reference. In the Document Map view, this command applies to the tag to the right of the cursor if the cursor is at the start of a line (that is, between the element icon and the element name); you can control this behavior with the set docmapcurrenttag=off option.

For tags defined by your DTD, local modifications can be made to SGML /XML attributes. Unless you are modifying a user-defined tag, attributes can only be modified locally. Tags supplied by Arbortext Editor , such as _link , have attributes that can be modified with this command.

If -local is specified (the default), only the current instance of the tag will be affected. Attributes that are set locally override attributes that are set globally.

The -global option is generally able to modify non-DTD markup such as user-defined file and text entities, marked sections, and processing instructions. It cannot modify attributes or elements of a DTD. Where -global is allowed and specified, it modifies every occurrence of the tag in the entire document.

The -quick (or -quickattr ) option will launch the Quick Attribute dialog box , where you can modify a single attribute for the specified element.

The -inline option causes the Column view attribute value cell with focus, if any, to be opened for modification. The command fails silently if the current view is not a Column view or if no cell has focus.

If -modal is specified, the Modify Attributes dialog box is launched as a modal dialog box.

The attr = value option modifies attributes without opening the Modify Attributes dialog box. Up to 50 attr = value pairs can be specified with a single command. You can determine the names of attributes from SGML /XML files.

The attr = value option can be used to set invalid attributes to new values. New invalid attributes cannot be added using this technique.

In a Free-form document type instance, the attr = value option can be used to alter the value of existing attributes and to add new attributes and values. New attribute names must be valid XML names.

If the -attr attrname option is specified, then the keyboard focus for the Modify Attributes dialog box is set to the value field for the specified attribute name. By default, the focus is set to the first attribute field.

mt is a synonym for modify_tag .

Examples

```
modify_tag ID='org-chart'
mt -local
mt -local par ParaType="block"
mt -global -caret
mt -global chaphead OverallTypeSize=18pt \
Underl=true UnderlRuleWidth=width-of-heading
```

## Related Topics

- • tag_exists function

- • tag_has_attr function

- • set docmapcurrenttag command



---

# modify_text_entities

# modify_text_entities

modify_text_entities

This alias brings up the Text Entities dialog box, which displays the name, number of uses, and system and public identifiers for all text entities (including those declared in the DTD).

You can use this dialog box to rename any text entities declared in the private markup section of the document instance, to locate instances of text entity use, and to modify system and public identifiers for entities declared in the private markup section.

mte is a synonym for modify_text_entities .

Examples

```
modify_text_entities
mte
```

## Related Topics

- • change_entity

- • declare_entity

- • declare_text_entity

- • delete_entity

- • insert_entity

- • modify_entity

- • rename_entity

- • undeclare_entity



---

# move_file

# move_file

move_file { oldname newname | file1 [ file2 …] dir }

This command moves the file oldname to newname . This command can be used to rename a file or a document.

The second form of move_file , move_file file1 [ file2 ] ... dir , moves one or more file names (which may also be directories) preserving their original names, into the last directory in the list.

move_file cannot be used to move a directory across file systems. The copy_file and remove_file commands must be used instead.

mv is a synonym for move_file .

Examples

```
move_file drugs.txt /apr3bust
mv /usr/svc/newslet/list.sgm /tecwrite/maillist
mv demo.sgm demo.acl ../article
```



---

# ms_hide

# ms_hide

ms_hide

This alias hides ignored marked sections in a document.

Example

```
ms_hide
```

## Related Topics

- • ms_show alias



---

# ms_show

# ms_show

ms_show

This alias displays ignored marked sections in a document.

Example

```
ms_show
```

## Related Topics

- • ms_hide alias



---

# new

# new

new [ -stylesheet name ] [ -newwindow | -ok ] [ -type doctype ] [ -sample ] [ docname ]

This command replaces the document in the Edit pane with a newly created document.

-stylesheet name specifies the stylesheet to be used in place of the default stylesheet for the Edit view. name is the path and file name of a stylesheet file. name can also be the base name of the stylesheet file (the file name without the path). If just the base name is supplied, Arbortext Editor looks for the file in the document directory, and then the document type directory.

-newwindow specifies that a new window be created to display the new document. If -newwindow is not specified, the new document replaces the current document. -nw is a synonym for -newwindow .

-ok moves you to the requested document without prompting you about unsaved changes to the current document or file (unsaved changes will be lost). This option is not applicable if -newwindow is given.

-type creates a new document of the specified document type. The type can be an initial substring from the list of document types listed in the New Document dialog box. If the name contains blanks, the name must be enclosed in quotes (for example “personal letter”). Any new document type installed as a template is also legal. This option can be combined with the -sample option. If -type is not specified, the New Document dialog box is opened.

-sample specifies that the new document is to contain sample markup.

docname specifies the path name to use when the document is saved. If omitted, the Save As dialog box will prompt for the name when saving.

Examples

```
new -sample book.sgm
new -type memo -nw salesmtg.sgm
```



---

# newline

# newline

newline

This command generates a return.

nl is a synonym for newline .

Examples

```
newline
nl
```



---

# options

# options

options [ [ categoryname ]]

This command brings up the Preferences dialog box from which various options affecting the editing environment can be set. Enter a value for categoryname to automatically bring that category of the dialog box to the foreground. The category names are:

- • Advanced invokes the Advanced Preferences window, for editing set command options

- • Colors corresponds to the Colors category

- • Columns corresponds to the Columns category

- • Compare corresponds to the Compare category

- • DITA corresponds to the DITA category

- • Edit corresponds to the Edit category

- • File corresponds to the File Locations category

- • PE corresponds to the Publishing Engine category

- • Save corresponds to the Save category

- • Spell corresponds to the Spelling category

- • User corresponds to the User Information category

- • View corresponds to the View category

- • Warnings corresponds to the Warnings category

- • Window corresponds to the Window category

Note that all of these options can also be set using the set command.

Examples

```
opt
options Window
Options window
```



---

# outline

# outline

outline [ div | backup]



This command inserts new division tags of the requested type and moves the cursor within those tags when:

- • outline div (the default) starts a new division of the same type after the end of the current division.

- • outline backup moves the cursor past the end tag of the current division so that the next outline div command will start a division one level higher than the current division.

Examples

```
outline
{outline backup; outline div}
```

## Related Topics

- • set indent command



---

# package

# package

package [ packagename ]



This command declares the name of a package when used at the top of a command file. Packages let you declare global variables and functions whose name space is localized to one or more command files.

Example

```
package myapp
```

## Related Topics

- • Packages



---

# paste

# paste

paste [ buffername ] [ -after ]



This command inserts the text from the specified paste buffer at the current cursor location. In the Edit view, the cursor is placed after the pasted region. In the Document Map view, the cursor is placed before the pasted region; you can control this behavior with the set docmappastecaret=off option.

If a buffer name is given, that buffer is used. Otherwise, text is inserted from the current buffer (see set paste= buffername ). Once text is placed in the paste buffer, it can be pasted back any number of times (until it is replaced).

The optional -after flag is used when pasting table objects. If -after is specified, the table object(s) in the paste buffer will be pasted after the cell, row, or column containing the text caret. If -after is omitted, the table object(s) in the paste buffer will be pasted before the cell, row, or column containing the text caret.

Examples

```
paste
pas bufA
pas seealso
pas tablecells -after
```

## Related Topics

- • Creating a named paste buffer

- • set docmappastecaret command

- • set pastepreserve command



---

# preview

# preview

preview [ onepass | allpasses | noformat | noprompt | quit | stop] [ auto | force] [ wait | nowait]

This command formats the current document and displays it in the Print Preview window. The abbreviation pre is a valid substitute for preview .

- • onepass — (The default.) Displays the document in the Print Preview window after performing a single formatting pass. If one pass is not sufficient for final output, then the Arbortext Editor status bar will indicate re-fmt needed and another preview command will trigger another pass.

- • allpasses — Displays the document in the Print Preview window after performing as many formatting passes as necessary for final output. Arbortext Editor performs one pass if there are no page number references in the document, or if the value of the page numbers can be correctly inferred from a previous formatting operation during the current Arbortext Editor session.

- • noformat — Displays the document in the Print Preview window using the existing formatting data file ( .dvi file) for the document (if it exists). Use this option carefully. It is useful if you need draft output for a large document in a hurry and do not want to take the time to reformat minor changes you have made. It could also be used in carefully controlled applications to format in one Arbortext Editor session, and print or preview in another Arbortext Editor without the need to reformat the document.

- • noprompt — Suppresses the Print Preview window. This option is ignored when publishing using Arbortext Publishing Engine .

- • quit — Closes the Print Preview window and continues formatting.

- • stop — Halts document formatting and leaves the Print Preview window open.

- • auto — (The default.) Lets Arbortext Editor decide whether the document needs to be formatted or not before being previewed. Arbortext Editor will trigger formatting if the document has not been formatted yet during the current session, or if the previous formatting command left the document in the refmt-needed state, or if the document has been modified since the preceding formatting command. If the document is up to date with regard to formatting, then preview auto will cause Arbortext Editor to position the Print Preview window to the page containing the cursor.

- • force — Performs at least one formatting pass regardless of whether Arbortext Editor thinks it is necessary.

- • wait — Makes editing unavailable in Arbortext Editor until a preview request completes.

- • nowait — (The default.) Allows editing in Arbortext Editor while a preview request is being processed.

Examples

```
preview (invokes preview onepass auto)
pre onepass
pre onepass force
pre allpasses auto
pre stop
pre quit
```

## Related Topics

- • format command

- • print command

- • Formatting pass reduction in ACL



---

# print

# print

print editor [ panel] [ all | screen | selection] [ portrait | landscape] [ header= { pageno | datemark | none | ' string '}] [ footer= { pageno | datemark | none | ' string '}] [ leftmargin= n ] [ topmargin= n ] [ printer= printer_name ] [ file= path_name ] [ color | monochrome] [ copies= n ]

and

print composed [ panel] [ all | current | page_range | page_list ] [ onepass | allpasses | noformat] [ force | auto] [ wait | nowait] [ portrait | landscape] [ collate | nocollate] [ papersize= { uslegal | usletter | a4 | b5}] [ paperheight= n ] [ paperwidth= n ] [ printer= printer_name ] [ file= path_name ] [ color | monochrome] [ copies= n ] [ stylesheet=e3: n ]

The print command prints the specified portion of the document. There are two main arguments to this command: composed and editor .



---

# quit

# quit

quit [ok]

This command closes the current window. If you only have one window open, this command exits from Arbortext Editor without saving the document. If there are unsaved changes in your document, a panel informs you and asks for permission to exit without saving the changes. You can bypass the panel by typing quit ok .

Examples

```
quit
qui ok
```



---

# read_(Command)

# read (Command)

read [ { -paste | -buffer buffername } [ -append ]] [ -sgml | -untaggedascii | [ -xml ] [ -encoding string ] [ -cc | -nocc ] [ -pendingdelete | -nopendingdelete ] filename

This command inserts the text of the requested file at the point of the cursor.

-paste loads the text of the requested file into either the current or a named paste buffer.

-buffer buffername forces the information that is read to be loaded into the named buffer specified by buffername . If the buffer already exists it will be overwritten, else it is created.

-append adds text to the end of the buffer file rather than replaces the contents of the buffer.

-sgml allows you to read in an SGML document that does not have the SGML header created by the write -sgml command, that is, starting with <!DOCTYPE .

-untaggedascii allows you to read in the named document as ASCII. Tagging, if any, are interpreted as literal text, not Arbortext Editor tags. -untagged is a synonym for -untaggedascii .

-xml reads an XML document into the current document ( SGML or XML). When this option is selected, a completeness check will not be performed (that is, -nocc is implied), and specifying -cc will have no effect.

-encoding determines the encoding of the file being read, as specified by string ; string may be one of the following strings:

-cc forces Arbortext Editor to do a completeness check when it opens a file created with Arbortext Editor . (By default, a completeness check is not done if the file being read in was saved in Arbortext Editor .) This option is recommended when opening documents which were created in Arbortext Editor but were later edited elsewhere and that may no longer be normalized or complete.

-nocc does not allow Arbortext Editor to do a completeness check when reading a document or file. (By default, a completeness check is done after the file is read in.) In this case, the document should be fully normalized.

-pendingdelete replaces any selected text in the document with the file being read.

-nopendingdelete preserves any selected text in the document and places the file being read to the right of the current selection.

filename is the file name and path (if needed).

Examples

```
read mydoc
rea -buffer buf1 wishlist.sgm
rea -sgml /lxr/grants89/proposal.sgm
rea -untag budget.sgm
rea -xml http://www.some_site.com/examples/doc1.xml
```

## Related Topics

- • Opening, referencing, and saving files



---

# readvar

# readvar

readvar [ -help " text "] [ -title " string "] [ [ -prompt " string "] [ -value " string " | -choice " c1 | c2 | c3 … cN " [ -default " string "]] variable1 ] [ [ -prompt " string "] [ -value " string " | -choice " c1 | c2 | c3 … cN " [ -default " string "]] variable2 ] …

The readvar command prompts for the values of the variables named. The information you provide is used to assign values to those variables. (Note that the variable is created if it does not already exist).

The readvar command provides a dialog box that contains OK and CANCEL buttons. If you click on OK , main::status is set to 0 . If you click on CANCEL , main::status is set to 1 .

-help “ text ” specifies that a Help button should be added to the panel and, if pressed, the help text text will display in a Help window.

-title “ string ” specifies a string to be used as the window title for the readvar dialog box.

-prompt identifies a string to be supplied as the text of the prompt. Multiple prompts on the same line are allowed.

-value allows you to specify a string value at the prompt and use it as a default text entry value.

-choice specifies a list of mutually exclusive choices (radio buttons). You can stack the radio buttons vertically on the panel by starting the choice string with | (that is, the first field is empty). If you specify a single item choice list, the choice will appear as a check box instead of a radio button. If the check box is selected, the value is set to a one ( 1 ). If the check box is cleared, the value is set to a zero ( 0 ).

-default allows you to specify a choice string as the default value. It can only be used with the -choice option. Only one of the options -value and -choice may be specified for a given variable name.

variable is a name, which should be supplied without the leading dollar sign. Variable names are limited to 199 characters each.

To establish a mnemonic (hot key) for a particular dialog box item, precede the mnemonic letter with the '&' character in the associated string. Use “&&” anyplace you want a single '&' to show.

You can prompt for up to 20 variables on the same panel.

Examples

```
readvar docname
readvar -prompt '...............' -prompt 'Enter story name:' story
readvar -prompt 'Story:' -value "$docname" story
readvar -prompt 'Enter &name:' name -prompt 'Enter &age:' age
readvar -prompt 'Enter new margins below:' \
-prompt 'Lt marg:' -choice '0.5"|1"|1.5"' l \
-prompt 'Rt marg:' -choice '|same-as-left|0.5"|1"|1.5"' r \
-prompt 'Top margin:' t \
-prompt 'Bottom margin:' b
```

## Related Topics

- • alias command

- • Command variables

- • execute command

- • map command

- • show variables command

- • Symbolic parameters

- • list_response built-in function

- • response built-in function



---

# redisplay

# redisplay

redisplay

The redisplay command redraws the Edit pane with the line containing the cursor centered in the window. The redrawing takes effect immediately. This is useful in command scripts to show an intermediate state. By default, changes to windows made inside command scripts do not show up until the script completes.

red is a synonym for redisplay .

Examples

```
redisplay
red
```



---

# redo

# redo

redo

The redo command reverses the change made by the last undo command. A series of consecutive undos may be reversed by the corresponding number of redos. Redo operations do not get added to the undo buffer.

If you choose Edit > Undo several times and proceed to perform a new (non undo or redo) operation, the forward items in the undo buffer is discarded in favor of the new operation. In this case there would no longer be any operations to redo.

Example

```
redo
```

## Related Topics

- • undo command



---

# remove_file

# remove_file

remove_file [ -r -f ] file1 [ file2 … ]

remove_file deletes the file(s) specified by file1 , file2 , and so on. If a file name specifies a directory, remove_file will delete the directory if it is empty. You can only specify a single file at a time from a WebDAV resource. remove_file will not remove a group of WebDAV resources or a WebDAV collection (folder).

remove_file has the following options:

- • -r — Specifies that remove_file is to recursively delete all files and subdirectories in the specified directories and to delete the named directories themselves.

- • -f — Specifies that remove_file is to delete write-protected files without any warning or prompt.

rm is a synonym for remove_file .

Examples:

```
remove_file myfil
remove_file /usr/draft.xml
remove_file -r -f /usr
remove_file -r -f "$tempfile"
```

If you use a variable name in the command for the file name, place it in double quotes to be sure it's interpreted correctly.

## Related topic

Opening, referencing, and saving files



---

# rename_entity

# rename_entity

rename_entity [ oldname ] [ newname ]

The rename_entity alias renames the entity reference oldname to newname , prompting for input if necessary. This works only for entities declared in the private markup section of the document instance.

re is a synonym for rename_entity .

Examples

```
rename_entity mdr ModReq
re arbortext ARBORTEXT
re address cityzip
```

## Related Topics

- • change_entity

- • create_file_entity

- • declare_entity

- • declare_file_entity

- • declare_graphic_entity

- • declare_text_entity

- • delete_entity

- • insert_entity

- • insert_graphic_entity

- • modify_entity

- • modify_file_entities

- • modify_graphic_entities

- • modify_text_entities

- • undeclare_entity



---

# rename_notation

# rename_notation

rename_notation [ oldname ] [ newname ]

The rename_notation alias renames the notation oldname to newname , prompting for input if necessary. This works only for notations declared in the private markup section of the document instance.

rn is a synonym for rename_notation .

Examples

```
rename_notation CGM cgm
rn Eq equatn
rn TeX tx
```

## Related Topics

- • declare_notation

- • modify_notation

- • modify_notations

- • undeclare_notation



---

# rename_tag

# rename_tag

rename_tag oldtagname newtagname

The rename_tag command renames a tag or entity reference that was defined by the user from oldtagname to newtagname . The tag name can be made up of any combination of letters, numbers, dashes ( - ), underscores ( _ ), and periods ( . ). Entity reference names must start with an ampersand ( & ).

rt is a synonym for rename_tag .

Examples

```
rename_tag comment tech_comment
rt 12-17 12.17.92
rt &address &cityzip
```

## Related Topics

- • declare_entity alias

- • define_tag command

- • rename_entity alias

- • rename_notation alias



---

# repeat

# repeat

repeat [ n ]

The repeat command re-executes the previous command typed at the command line or when used in a script, the preceding command, or command list in the script. If a positive integer argument, n , is specified, the command will be repeated n number of times.

rep is a synonym for repeat .

Examples

```
repeat
rep 5
```



---

# require_(Command)

# require (Command)

require package [ filename ]

The require command loads the package specified by the variable name package from the file specified by filename , if it's not already loaded. If filename is not specified, the list of directories specified in the -loadpath option of the set command is searched for a file named package.acl , where .acl is the standard Arbortext Command Language file name suffix.

If the specified package name is not defined after the file is read, the require command will issue an error message and set main::status to 1 , indicating failure.

The require command has no synonym.

Examples

```
require history
require Tools /ppl/Tools.acl
```

## Related Topics

- • require function

- • set loadpath command

- • source command

- • Opening, referencing, and saving files



---

# save

# save

save [ -pi | -nopi ]

save saves the document that is being edited.

To safeguard against data loss, Arbortext Editor first saves the file to a temporary location; if space is available, the original file is deleted and the temporary file is renamed with the name of the original file.

save has the following options:

- • -pi — Saves Arbortext Editor processing instructions with the document.

- • -nopi — Removes all Arbortext Editor processing instructions (except change tracking processing instructions) and may be useful for exporting the document to another system.

If the save , write or save_as commands do not specify whether to write Arbortext Editor processing instructions, they use the value of the set writepi command.

Examples

```
save
sav
```

You can also use the set writepi command to specify whether the write , save or save_as commands save Arbortext Editor processing instructions.

## Related topic

Opening, referencing, and saving files



---

# save_all_docs

# save_all_docs

save_all_docs [[ -s ]]

This alias saves the current document and any file entities (including nested entities), regardless of whether the entities have been modified. This alias is especially useful after changing the set writeentdecls option for your site.

If -s is specified, the message window showing all saved documents is suppressed.

## Related Topics

- • set writeentdecls command



---

# save_as

# save_as

save_as [ -readonly ] { [ -xml ] | -sgml } [ -pi | -nopi ] [ -encoding string ] [ name ]

save_as copies the current version of the document or file, including any changes you have made since the last save, to the file name (and path if needed) specified by name . The document in the Edit pane will change to the document specified. If name exists, a prompt to confirm its replacement will be displayed. To suppress the prompt, prefix the name with an exclamation point ( ! ). If name is not supplied, the Save As dialog box is displayed.

save_as has the following options:

- • -readonly — Saves the document as read-only.

- • -xml — Saves the document as XML. By default, XML documents are saved as XML documents.

- • -sgml — Saves the document as SGML . By default, SGML documents are saved as SGML documents.

- • -pi — Saves Arbortext Editor processing instructions with the document.

- • -nopi — Removes all Arbortext Editor processing instructions (except change tracking processing instructions) and may be useful for exporting the document to another system.

- • -encoding — Saves the file with the encoding specified by string ; string must be one of the following strings:

Examples

```
save_as
save_as startup.sgm
```

If the save_as , write or save commands do not specify whether to write Arbortext Editor processing instructions, they use the value of the set writepi command.

## Related Topics

- • Opening, referencing, and saving files



---

# save_buffers

# save_buffers

save_buffers [ directory ]

save_buffers saves all paste buffers with names to the directory specified by directory . If no directory is specified, the current document directory is used.

save_buffers saves all buffers named with the set paste command and copy_mark command and appends the suffix: .apb . A buffer name may be truncated to conform to operating system limitations.

Buffers are loaded with the load_buffers command.

sb is a synonym for save_buffers .

Examples

```
save_buffers
sb bookbfps
```

## Related Topics

- • Opening, referencing, and saving files



---

# sh

# sh

sh shell command

This command passes shell command , which is a specified operating system command, to the shell. If the command string contains a semicolon (;) curly braces ({}), a backslash (\) or other special characters, it must be enclosed in quotation marks.

Example

```
sh 'c:\doc\help.com'
```

## Related Topics

- • system function



---

# show_aliases_(show_alias)

# show aliases (show alias)

show aliases [output= filename ]

show alias name [output= filename ]

show aliases displays all the currently defined aliases.

show alias name displays the definition of the alias named name .

If output is specified, this command writes a list of aliases to filename where filename can be any of the following items:

- • The name of a file (this could be a complete path name). A right angle bracket ( > ) preceding the file name causes the list of aliases to be appended to the end of the file. An exclamation point ( ! ) preceding the file name causes the file to be rewritten, if it exists, without the prompt for confirmation.

- • An asterisk ( * ) specifying the message window. If preceded by a right angle bracket ( > ), the output is appended to the message window instead of replacing its contents. Additional predefined message windows msgwin2, msgwin3, or msgwin4 use the specifiers output=*2 , output=*3 , and output=*4 , respectively.

- • A question mark ( ? ) preceding the output file name. If the file name starts with a question mark, the file name is actually a variable name whose value is set to the output produced by the command. If the second character is a right angle bracket ( > ), the output is appended to the current value of the variable instead of replacing it.

- • A dash (-) specifying standard output. (This is typically the window from which you started Arbortext Editor .)

Examples

```
show aliases
sho aliases output=myaliases
sho aliases output=>allaliases
sho alias rename_entity
sho alias find_id output=myalias.txt
```



---

# show_buffers

# show buffers

show buffers [output= filename ]

This command displays a list of all named paste buffers.

If the output option is selected, instead writes a list of named paste buffers to filename where filename can be any of the following:

- • the name of a file (this could be a complete path name). A right angle bracket ( > ) preceding the file name causes the list of aliases to be appended to the end of the file.

- • an asterisk ( * ) indicating the message window. If preceded by a right angle bracket ( >* ), then the output is appended to the message window instead of replacing its contents. Additional predefined message windows msgwin2, msgwin3 , or msgwin4 use the specifier output=*2, output=*3 or output=*4, respectively.

Examples

```
show buffers
sho buffers output=pastebuf.apb
sho buffers output=>pastebuf.apb
```

## Related Topics

- • Creating a named paste buffer



---

# show_characters

# show characters

show characters

This command displays a list of all character entities declared in the DTD with links so that clicking on the entities inserts them in the character entity shortcut menu in the toolbar or in the document if the toolbar is not present.

show chars is a synonym for show characters .

Example

```
show characters
show chars
```



---

# show_cmdkeys

# show cmdkeys

show cmdkeys [output= filename ]

This command displays a list of command aliases and the associated keyboard shortcut for each command bound to a key. Key assignments to complex commands or functions are not included in the list. The output includes only the default user and system keyboard shortcut assignments.

If the output option is selected, this command instead writes a list of mappings to filename where filename can be the name of a file (this could be a complete path name). A right angle bracket ( > ) preceding the file name causes the list of command key assignments to be appended to the end of the file.

Example

```
show cmdkeys
```

## Related Topics

- • cmd_key function

- • show fullkeymap command

- • map command

- • unmap command



---

# show_context

# show context

show context [output= filename ]

This command lists in a display window the tags and other document structures (such as text or equations) currently valid at the cursor.

If the output option is selected, instead writes the list to filename where filename can be the name of a file (this could be a complete path name). A right angle bracket ( > ) preceding the file name causes the list of aliases to be appended to the end of the file.

Examples

```
sho context
sho context output=rules
sho context output=>glblsty
sho context output='>tabify >rules'
```



---

# show_emptyelements

# show emptyelements

show emptyelements

This command invokes the Empty Elements dialog box , which lists all elements in the current document that may contain text, but that are empty.



---

# show_fullkeymap

# show fullkeymap

show fullkeymap [ edit | cmd | helpwins | msgwins | textwins | all] [output= filename ]

This command displays all keymappings (including user-defined and default mappings that have not been remapped) for the Edit pane, command line, help windows, message windows, or all windows. The default is show fullkeymap edit .

A list of several windows classes can be made by using a “plus” sign (+) to separate the names. To subtract a window from a list, use a hyphen (-). The option all displays the keymappings for the first two windows named above (that is, edit+cmd ). The helpwins option refers to multiple Help windows and is shorthand for: helpwin1+helpwin2+helpwin3+helpwin4 . The option msgwins refers to the predefined message windows and is a synonym for msgwin1+msgwin2+ msgwin3+msgwin4 . The option textwins is a synonym for helpwins+msgwins .

If the output option is selected, instead writes a list of mappings to filename where filename can be the name of a file (this could be a complete path name). A right angle bracket (>) preceding the file name causes the list of aliases to be appended to the end of the file.

Examples

```
sho fullkeymap
sho fullkeymap all+text
sho fullkeymap output=/homedir/allkeys
```

## Related Topics

- • map command

- • show keymap command

- • unmap command



---

# show_functions

# show functions

show functions [ package ] [output= filename ]

This command displays a list of all the functions defined in the specified package along with a count of the number of times each function was called in the current session.

- • package — The name of a loaded package or the fully qualified path name of the file defining the functions. If package is not supplied, the current package is used.

- • output — Writes a list of functions to filename where filename can be any of the following values:

Examples:

```
show functions mytools
sho functions c:\acl\functions.acl
```



---

# show_ids

# show ids

show ids [output= filename ]

This command displays the IDs and ID References dialog box that lists all IDs used in ID and IDREF attribute values and locates any errors in their usage. Attribute values given for IDREF must have a matching ID attribute of the same value. File (external) entities are included in the search for ID and IDREF attributes.

The menu item Tools > IDs and ID References is the same as the command show ids . In a file entity Edit pane, selecting IDs and ID References or using the show ids command displays the same ID list as the parent document. You can't check just the IDs of a file entity unless that entity is edited as a separate document by opening a file entity Edit pane from within the document Edit pane.

If the -output option is selected, this command instead writes a list of cross references to filename , where filename can be the name of a file (this could be a complete path name). A right angle bracket ( > ) preceding the file name causes the list of aliases to be appended to the end of the file.

Examples

```
show ids
show ids output=c:\ch3_lou\crosrefs.txt
```



---

# show_keymap

# show keymap

show keymap [ edit | cmd | helpwins | msgwins | textwins | all] [output= filename ]

This command displays any user-defined keymappings for the Arbortext Editor window, command line, help windows, message windows, or all, as specified. show keymap edit is the default. all displays the keymappings for the first two windows named above (that is, edit + cmd ). helpwins refers to multiple help windows (if used) and is shorthand for: helpwin1 + helpwin2 + helpwin3 + helpwin4 . msgwins refers to the predefined message windows and is a synonym for msgwin1 + msgwin2 + msgwin3 + msgwin4 . textwins is a synonym for helpwins + msgwins .

If an output value is specified, the command instead writes a list of mappings to filename where filename can be the name of a file or a complete path and file name. A right angle bracket ( > ) preceding the file name causes the list of aliases to be appended to the end of the file.

Examples

```
sho keymap
sho keymap edit
sho keymap all
sho keymap output=mymaps.txt
sho keymap output=>smaps.txt
```

## Related Topics

- • all current keymappings ( show fullkeymap command)

- • map command

- • unmap command



---

# show_tagnames

# show tagnames

show tagnames [output= filename ]

This command displays all valid tag names for the current document type.

If the output option is selected, instead writes a list of valid tag names to filename where filename can be the name of a file (this could be a complete path name). A right angle bracket ( > ) preceding the file name causes the list of aliases to be appended to the end of the file.

Examples

```
sho tagnames
sho tagnames output=/d1/jkl/publ/booktags.txt
sho tagnames output=>/d3/syst/publtags.txt
```



---

# show_usertags

# show usertags

show usertags [output= filename ]

This command displays user-defined tags.

If the output option is selected, instead writes a list of user-defined tags to filename where filename can be the name of a file (this could be a complete path name). A right angle bracket (>) preceding the file name causes the list of aliases to be appended to the end of the file.

Examples

```
sho usertags
sho usertags output=mytags.txt
sho usertags output=>ourtags.txt
```



---

# show_variables

# show variables

show variables [output= filename ]

This command displays a list of all command variables and their values as defined in the current package. For commands entered at the Edit command line, this is always package main.

If the output option is selected, instead writes a list of variables and their values to filename where filename can be the name of a file (this could be a complete path name). A right angle bracket ( > ) preceding the file name causes the list of aliases to be appended to the end of the file

Examples

```
sho vars
sho vars output=mdkbook.txt
sho vars output=>docsvars.txt
```

## Related Topics

- • alias command

- • Command variables

- • execute command

- • map command

- • readvar command

- • Symbolic parameters



---

# source

# source

source filename

This command reads and executes a list of commands from file filename . Reading of the file terminates if a command has an error or if a return statement is executed.

If the specified file name does not contain any slashes and is not found in the current directory, the source command searches the list of directories specified by the set loadpath command . The extension .acl is appended to the file name if it has no extension. For example, if you have a file called myfuncs.acl in a directory called packages in your home directory, the following will find your file myfuncs.acl :

```
append_load_path("~/packages")
source myfuncs
```

If the file filename ends with the .js extension, then filename is passed to the JavaScript interpreter using the js_source function . The JavaScript program is evaluated in the global scope with the arguments global object set to null.

If the file filename ends with the .vbs extension, the file will be run using the vbscript.dll script engine using COM.

The abbreviation of source is sou .

Examples

```
sou cmd.fil
sou /ati/doc/publ/pubdoc.acl
```

## Related Topics

- • append_load_path function

- • set javascriptinterpreter command

- • Opening, referencing, and saving files

- • Testing and debugging ACL scripts



---

# spell

# spell

spell { [ -entityscan -noentityscan ] [ -selection | -all ] | [ -accept | -ignoreall | -reject | -next | -delete ] word [ word …]}

This command checks the entire document, or the selected text, for spelling errors. The default is to check the current selection if there is one, otherwise, the entire document is checked. Misspelled words are displayed in a window.

Examples

```
spell
spe -selection
spe -all
```

-entityscan (-es) controls whether or not the spell command will include the contents of entities. The counterpart, -noentityscan (-noes) will prevent the search from including the contents of entities. For example, the command spell –es will check the spelling of the document or selection, including all referenced entities. Setting this option overrides the set entityscan command.

The -accept option lets you add a new spelling to the “accepted” word list, saved in the aptspell.xml file. The -reject option lets you add a misspelling to the stop word list, also saved in the aptspell.xml file. Note that these options add words to the aptspell.xml file based on the current authoring language. You can set a language on individual tags in a document, so that language can vary based on the position of the cursor.

The -delete option removes words from the aptspell.xml file.

The -ignoreall option will cause Arbortext Editor to ignore the word for the current session, but not save it in the aptspell.xml file.

The -next option finds the next occurrence of a misspelling when interactive spell checking is enabled.

Arbortext Editor stores the aptspell.xml file in the application data directory. That directory is typically C:\Documents and Settings\ username \Application Data\PTC\Arbortext\Editor .

Elements configured by the tag_display command to not be displayed can be recognized and operated on by the spell command by setting set hiddentagscan to on .

Examples

```
spell -accept Arbortext
spe -reject AM PM ATI
spe -delete a.m.
```

## Related Topics

- • Autocorrection and Spelling Checks

- • Supported authoring languages

- • Creating and accessing a user-defined dictionary

- • Working with your exception dictionary

- • Configuring elements to be ignored during a spelling check



---

# split_(Command)

# split (Command)

split

This command divides the current element at the cursor into two elements. It searches backward for the first unmatched begin tag and inserts its end tag and another begin tag of the same type.

Example

```
split
spl
```



---

# substitute

# substitute



substitute [ -b | -f ] [ -c | -noc ] [ -a ] [ -e | -noe ] [ -wrapscan | -nowrapscan ] [ -q | -noq ] [ -markup ] / oldtext / newtext /

This command searches for oldtext and replaces it with newtext .

- • -a replaces all occurrences of the string oldtext with the string newtext . If -wrapscan is specified, the command replaces all occurrences in the document. If -nowrapscan is specified, the command replaces all occurrences from the current cursor position to the end of the document.

- • -b searches backward.

- • -f (the default) searches forward

- • -c performs a case-sensitive search.

- • -noc (the default) finds a string regardless of how it is capitalized. The set case command sets this parameter for all subsequent searches.

- • -e specifies that the search string is a regular expression. In regular expressions, some punctuation characters (such as * , + , ? , \ , and . ) perform special actions. For example, find -e /p..t/ (where the . is a placeholder representing any character) would match “pret”, “port”, and “part”, as well as the string “p..t”.

- • -noe (the default) specifies the search string is not a regular expression. The set expressions command sets this parameter for all subsequent searches.

- • -wrapscan ( -ws ) (the default) causes the search to wrap to the beginning of the file when the end is reached.

- • -nowrapscan ( -nows ) prevents the search from wrapping. The set wrapscan command sets this parameter for all subsequent searches.

- • -q (for “quiet”) suppresses the “string not found” message generated when a search fails. This is useful when putting the find command in command files or aliases.

- • -noq (the default) displays a message when Arbortext Editor cannot find a string that matches the search string.

- • -markup ( -m ) indicates that the oldtext and newtext strings contain one or more tags or entities. Tags are indicated by surrounding angle brackets; an end tag contains a slash. Entities start with an ampersand ( & ) and end in a semicolon ( ; ).

When performing a case-insensitive substitution ( sub -noc /Never/rarely/ , for example), the replacement is capitalized according to how it was specified, not according to what it replaces (in this example, Never and never would both be replaced with rarely ).

You must supply either a matching close delimiter or place the string at the end of a line. For instance, sub -c /therefore/Therefore if it's the end of a line and sub -c /therefore/Therefore/ are both valid.

Examples

```
substitute /the/THE
substitute -b /here/there
s -f /here/there
s -c /here/there/
s -a /and/AND/
s -a -m /<_newline>//
s -e /Eg...t Wil..n/Myrna Jones/
s '(John)(Smith)'\2,\1' -e
```

## Related Topics

- • Using regular expressions

- • find command



---

# switch

# switch

switch ( expression ) { case constant1 : statements break case constant2 : statements break … default: statements break}

This command selects from a group of statements based on the value of the expression. The form of the statement is similar to that of the switch statement in the C programming language.

When the switch statement is executed, expression is evaluated and then control is transferred to the statement following the case whose constant value matches the expression. If the expression does not match a case value, control is transferred to the statement following the default prefix. If there is no default prefix, then control resumes following the end of the switch .

Case is a clause that delimits a set of alternative statements within a switch statement. The case and default prefixes do not alter flow of control. The break statement may be used to transfer control out of the switch statement.

The case constant may be a string value delimited by single or double quotes, or a regular expression delimited by slashes. For example, this:

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

If the case constants are all integer values or string constants of a single character, a jump table may be used to transfer control to the matched value. This executes considerably faster than a series of if,else if clauses. If the case values are all string values, a binary search is used (for more than three cases). A series of if,else if statements are compiled if the case values are regular expressions or are a mixture of string and integer value.

The body of the switch statement must be enclosed in braces. The case statements do not need to be enclosed in braces.

## Related Topics

- • break command

- • Using expressions



---

# tag_display_(Command)

# tag_display (Command)

tag_display [ -caret | -mouse ] [ -global | -local ] [ -default | -full | -partial | -none | -hide | -icon | -toggle ] [ tagname1 [ tagname2 …]]



This command tailors the Edit pane display of the tags specified.

If no tag name is given, -caret (the default) indicates the first tag to the left of the cursor. -mouse indicates the tag under the mouse arrow, or, if the mouse arrow is not on a tag, the first tag to the left of the arrow.

To change the display of every occurrence of a tag, use the -global option (the default). One or more tag names may be specified, in which case -caret and -mouse have no effect.

To change the display of one particular instance of a tag, use the -local option. (In this case, the tag must be indicated by the cursor or mouse arrow position; any tag name that does not match results in an error message.)

The remaining options change the display as follows:

- • -full — Displays the specified tags in full in all tag display modes.

- • -none — Indicates that the specified tags are not displayed in any tag display mode.

- • -hide — Hides the specified tags and the contents of these tags in any tag display mode.

- • -toggle — (the default) switches between settings as follows:

- • -default — Depends on the changes you are making:

The tag display mode is set with the set tagdisplay command.

Elements configured by the tag_display command to not be displayed can be recognized and operated on by the spell and find commands by setting set hiddentagscan to on .

td is the abbreviation for tag_display .

Examples

```
tag_display -icon indexterm
td -default indexterm
td -mouse
td -icon _ignore
td -local -toggle
td -local -none
td -icon indexterm footnote _comment
td -toggle indexterm
```

## Related Topics

- • set showemptyelement command



---

# time_(Command)

# time (Command)

time [ command | command-list ]

The time command executes the specified command(s) and reports how much real (clock) user and system CPU time has elapsed. (System time is always zero on Arbortext Editor for Windows.) If no argument is given, then time reports the times since Arbortext Editor started.



---

# toggle

# toggle

toggle [ optionname ]

This command changes the value of the Arbortext Editor boolean option specified by optionname . The specified optionname must be a boolean option, having only two values (for example, on/off, 1/0, yes/no, etc.). This command evaluates the current setting and sets the option to its opposite setting.

Example:

```
toggle tabletags
toggle addrequiredtags
```



---

# translate

# translate

translate { uc | lc | mc | pc}

This command converts the case of a highlighted region (or the character before the cursor if no region is selected) in the following manner:

- • translate uc (uppercase) converts every letter in the region to an uppercase or capital letter.

- • translate lc (lowercase) converts every letter in the region to a lowercase letter.

- • translate mc (mixed case) capitalizes the first word of every sentence by converting the first character that follows a period, question mark, or exclamation point to a capital letter if it is a letter.

- • translate pc (proper case) capitalizes the first letter of every word.

Examples

```
translate uc
tra lc
tra mc
tra pc
```



---

# unalias

# unalias

unalias alias

Removes the specified alias from the current list of aliases.

Examples

```
unalias pscr
```

## Related Topics

- • alias command



---

# undeclare_entity

# undeclare_entity

undeclare_entity [ name ]

This alias removes the user-defined entity reference name from the private markup section of the document instance, thus eliminating the entity. If the entity name is not supplied, you are prompted for it.

To use undeclare_entity , you must first remove all references to the entity in the document. If the entity is referenced in the document's paste buffer, you are prompted to clear the paste buffer.

ude is a synonym for undeclare_entity .

Examples

```
undeclare_entity
ude atext
```

## Related Topics

- • change_entity

- • create_file_entity

- • declare_entity

- • declare_file_entity

- • declare_graphic_entity

- • declare_text_entity

- • delete_entity

- • insert_entity

- • insert_graphic_entity

- • modify_entity

- • modify_file_entities

- • modify_graphic_entities

- • modify_text_entities

- • rename_entity



---

# undeclare_notation

# undeclare_notation

undeclare_notation [ notationname ]



This alias removes the user-defined notation notationname from the SGML Declaration in the private markup section of the document instance, thus eliminating the notation. If the notation name is not supplied, you are prompted for it.

udn is a synonym for undeclare_notation .

Examples

```
undeclare_notation
udn
```

## Related Topics

- • declare_notation

- • modify_notation

- • modify_notations

- • rename_notation



---

# undefine_keymap

# undefine_keymap

undefine_keymap name

This command deletes the keymap named name , which was created by define_keymap or copy_keymap . The keymap must not be currently attached to a window. The command will fail if it is. The function keymap_exists may be used to determine if the keymap is in use.

udkm is a synonym for undefine_keymap .

Example

```
undefine_keymap panel_map
```

## Related Topics

- • copy_keymap command

- • define_keymap command

- • keymap_exists built-in function

- • map command

- • set keymap command



---

# undefine_tag

# undefine_tag

undefine_tag tagname

This command undefines the user tag tagname (or entity reference) defined previously by the user.

udft is a synonym for undefine_tag .

Examples

```
undefine_tag indxterm
udft cologo
```

## Related Topics

- • define_tag command



---

# undo

# undo

undo [ boundary | current | clear | mark | unmark | suspend | resume]

With no arguments, this command undoes the most recent change. A redo brings it back.

The options are only useful within ACL scripts. The boundary option causes Arbortext Editor to insert a boundary in the undo history so that a subsequent undo will restore changes up to the current change. Normally, when executing a function or alias mapped to a key or menu item, Arbortext Editor considers all changes made by the script as a single undoable event. The function or alias can use undo boundary to cause the changes to be considered as separately undoable operations.

If current is specified, then this command undoes all changes made by the currently executing function or alias and discards the undo history. This can be used to cancel the effect of a command script, for example, if the script prompts for confirmation and the user cancels the request.

If clear is specified, the undo buffer is cleared. You will not be able to undo any prior operations. Subsequent operations will begin to re-fill the undo buffer.

The mark option inserts a temporary boundary in the undo history that can be removed with the unmark option. This is useful if a script makes changes to the document and then raises a modal dialog to make additional changes. Normally, when a dialog is raised Arbortext Editor inserts a boundary in the undo history. This means the changes made before the dialog was raised would require a separate undo operation to undo. The script can use undo mark and undo unmark to cause the two sets of changes to be combined into a single undo event. See the example below.

If suspend is specified, then any changes made after the command will not be added to the undo history and cannot be undone. Use undo resume to re-enable the undo history. You should use the undo suspend command with care, since it is possible to disable undo history for all further edits to the document if undo resume is not called.

Undo operations are not added to the undo buffer.

Examples

```
und
undo boundary
undo current
```

```
# undo mark/unmark/current example:
if (insert_tag(name)) {
# Tag insertion succeeded, set a temporary boundary and
# raise the modify attributes dialog as a modal dialog
undo mark;
modify_tag -local -modal;
if (main::status != 0) {
undo current;	# User cancelled so back out insert_tag change
} else {
# Dialog succeeded, so remove the temporary undo boundary so
# both operations will become a single undoable event.
undo unmark;
}
}
```

## Related Topics

- • redo command



---

# unmap

# unmap

unmap [window] keyname

This command removes the current user-defined mapping from the specified key. The window argument identifies which window classes are to be affected by unmapping keyname . The keymap attached to the current window is the default.

This command cannot be used to unmap Arbortext Editor 's default key mappings. For example, it is impossible to use the unmap command to make the F1 key do nothing.

The value for window , which is a window class name or user-defined keymap, can be any of the following:

- • edit designates the Edit pane

- • cmd designates the command line

- • helpwin (also called helpwin1 ), helpwin2 , helpwin3 , helpwin4 , msg (also called msgwin1 ), msgwin2 , msgwin3 , and msgwin4 designate multiple Help windows. (Use msgwin for Arbortext Editor messages and output from the show , eval , and similar commands.)

- • window name as returned by the window_name function

- • @ name designates the name of a user-defined keymap.

If window is a class name, the mapping affects all windows using the specified class keymap, otherwise unmap changes the mapping in the keymap defined by a previous define_keymap or copy_keymap command.

A list of several window classes can be made by using a “plus” sign ( + ) to separate the names. To subtract a window class from a list, use a hyphen ( - ). The option all is a synonym for edit+cmd . Note that the helpwins and msgwins are not included in the all option. To map a key for all possible window classes, use: map all+textwins . The textwins option is a synonym for helpwins+msgwins . The helpwins option is shorthand for helpwin1+helpwin2+helpwin3+helpwin4 .

Examples

```
unmap f1
unm cmd backspace
unm helpwin2 Tab
unm edit+cmd f1
unm all+textwins-cmd shift-UpArrow
```

## Related Topics

- • map command



---

# unsetvar

# unsetvar

unsetvar variable1 [ variable2 …]

This command removes any setting for the variable specified. If an array name is specified, all elements are discarded. Individual array elements may be removed using the delete built-in function. Note the absence of the leading dollar sign.

Examples

```
unsetvar docname
unsetvar docname user
```



---

# version

# version

version

Shows the version panel for the version of the software that is being run.

Examples

```
version
ver
```



---

# wait

# wait

wait n

This command delays n seconds before executing the next command.

Example

```
wait 3
```



---

# while

# while

while ( condition ) { cmds }

This command repeats the commands listed as long as the given condition is true.

cmds is a list of one or more commands. The list must be enclosed in curly braces. condition is a logical expression describing the case in which these commands are to be executed.

Examples

```
find -t '
<emphasis>
Editor
</emphasis>
'
while ($status == 0) {
delete_mark; insert_entity ed; find
}
```

## Related Topics

- • If, while, for, switch

- • Functions as expressions and commands

- • Using expressions

- • if command



---

# window

# window

window { pct | / string / | down | up | line , col } [ -c | -noc ] [ -e | -noe ] [ -t | -not ] [ -wrapscan | -nowrapscan ] [ -q | -noq ] -nocaret -wheelup -wheeldown

This command positions the Edit pane so the line specified by the argument is the first line on the screen. The -pct argument specifies a number between 0 and 100 and represents the percentage in the document that should be scrolled to the top of the screen. If 0, the beginning of the document is displayed; if 100, the end is scrolled into view.

If / -string / is specified, the line containing the next occurrence of the specified string (or pattern if -e is also given) is scrolled to the top of the screen. Any of the standard string delimiters may be used in place of “ / ”.

If -down is specified, the document is scrolled so the bottom line on the screen is moved to the top, corresponding to the PAGE DOWN key.

If -up is specified, the document is scrolled so the top line on the screen is moved to the bottom, corresponding to the PAGE UP key.

If -wheeldown is specified, the document is scrolled down the number of lines that correspond to the current setting for the scroll wheel on the pointer device, usually three lines.

If -wheelup is specified, the document is scrolled up the number of lines that correspond to the current setting for the scroll wheel on the pointer device, usually three lines.

If -line,col is specified, the line containing the character at the specified location is scrolled to the first line on the screen. Allowable values for -line and -col are the same as for the caret command. However, only relative line numbers may be specified.

The -nocaret modifier specifies that the cursor position should not be changed even if it is off the screen after the document is scrolled to the new top line.

The other modifiers here work like the modifiers for the find command.

Examples

```
window 50
win 100
win up
win /<section>/ -t
win +2,0
win bottom+1,0
win -2,0
win bottom,0
win (bottom-top)/2,0
```



---

# write_(Command)

# write (Command)

write [ -ct [ original | changesapplied | changeshighlighted]] [ -sgml | -untagged | -xml ] [ -encoding string ] [ -paste | -buffer buffername | -all ] [ -ok ] [ -header | -noheader ] [ -pi | -nopi ] [ -eoc | -noeoc ] [ -nonasciichar [ entref | numref | char]] [ -public pubident ] [ -sysid sysident ] [ -nobreakattag ] [ -flatten [ file | text | both]] filename

The write command saves a version of the document, or a portion of the document, to the file specified by filename .

filename can be any of the following:

- • The name of a file, including path if needed.

- • An asterisk ( * ) indicating the message window. If preceded by a right angle bracket ( >* ), the output is appended to the message window instead of replacing its contents.

The write command has the following options:

- • -ct — Specifies how the document will write changes that have been made with change tracking turned on:

- • -sgml — Writes a version of the document conforming to the SGML standard, ISO 8879. Unless the -noheader option is specified, the standard DOCTYPE header listing any private ENTITY declarations will appear at the top of this version. By default, SGML documents are written as SGML documents.

- • -untagged — Writes a text-only version of the document which contains no tags. No entity expansion or substitution is attempted. write -untagged does not write equations.

- • -xml — Writes the file as an XML document. By default, XML documents are written as XML documents.

- • -encoding — Specifies with string the encoding of the file being written. The setting of this option overrides the encoding declaration in an XML file.

- • -paste — Writes the contents of the current paste buffer to the specified file.

- • -buffer — Writes the contents of the named paste buffer to the specified file.

- • -all — Writes the entire document to the new file name. This is the default option.

- • -ok — Writes the file without prompting you if a file with the same name already exists. The existing file will be overwritten. Alternatively, the file name may be preceded with an exclamation point (!) to suppress the prompt.

- • -header — Specifies that the DOCTYPE header and any private ENTITY declarations that normally appear at the top of a standard DOCTYPE header are maintained.

- • -noheader — Removes the DOCTYPE header and any private ENTITY declarations that normally appear at the top of a standard DOCTYPE header.

- • -pi — Writes processing instructions specific to Arbortext Editor .

- • -nopi — Removes all processing instructions (except change tracking processing instructions) specific to Arbortext Editor .

- • -eoc — Turns on entity conversion, letting you specify how you want Arbortext Editor to write out character entities. This setting overrides the value of the set entityoutputconvert command .

- • -noeoc — Turns off entity conversion, and, if set entityinputconvert is off , Arbortext Editor writes out character entities as they were read in. This option overrides the value of the set entityoutputconvert command .

- • -nonasciichar — Specifies how Arbortext Editor writes out non-ASCII characters. -nonasciichar has the following arguments:

- • -public — Writes the alternate public identifier pubident on the DOCTYPE declaration instead of the original value (if any). pubident is not checked for validity as a minimum literal. If pubident is <none> , then the PUBLIC identifier will be omitted.

- • -sysid — Writes the alternate system identifier sysident on the DOCTYPE declaration instead of the original value if any. For XML files, sysident should be a valid URL (as created by the filename_to_url function). If sysident is <none> , the SYSTEM identifier will be omitted. Using this option overrides the setting of the set writeabsolutesysid command .

- • -nobreakattag — Specifies that breaks not be inserted at element boundaries or before the tag close character (applies to XML documents only). Such breaks may not be properly ignored by web browsers. Avoiding breaks at element boundaries tends to produce many breaks within elements. This may produce a file that is difficult to read when viewed with a text editor. Using this option overrides the setting of the set writenobreakattag command .

- • -flatten — Specifies that Arbortext Editor expand entity references on write, replacing references with the text of the entity type as specified by one of the following arguments:

Examples

```
write -untag -paste cherdoc.txt
write -sgml proposal.xmm
write -buffer bufC oldver.sgm
```

## Related Topics

- • doc_flatten function

- • Opening, referencing, and saving files



---

# xmsgfmt

# xmsgfmt

xmsgfmt [ -o filename .amo] [ file1 .xlf] [ file2 .xlf ...]

xmsgfmt reads XLIFF .xlf files and creates a .amo file that can be used by Arbortext Editor for all error messages it displays.

- • -o filename .amo — The .amo file to be created. If not given, the output is written to file1 .amo

- • file1 .xlf — One or more XLIFF files to be compiled into an .amo file.