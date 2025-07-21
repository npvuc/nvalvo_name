

---

# Associate_a_Program_for_Previewing_RTF_Documents

To preview exported RTF documents from Arbortext Styler , a Windows application must be associated with the .rtf file extension. PTC recommends you associate Microsoft Word 97 (or higher) to the .rtf file extension. Wordpad is delivered with Windows, and will also open RTF files. However, Wordpad may not support all of the features in the RTF file.

Refer to the Microsoft Windows online help for information on associating a file with a program.



---

# Customize_RTF_Style_and_Field_Names

The paragraph styles, character styles, list paragraph styles, and field names available in Arbortext Styler 's RTF property category are defined in two configuration files in the following directory:

```
Arbortext-path
\lib\importexport\lib
```

These files are well-formed, free-form XML files that can used as the basis for custom lists of names. The files are:

- • word-builtin-styles.xml — Specifies the available paragraph, list paragraph, and character style names in the RTF style name and RTF list name lists in the RTF property category and the Paragraph Style for Lists dialog box. By default, the names in the list are the default style names in Word's normal.dot template file.

- • word-fields.xml — Defines the structure of all supported Word fields, along with their instructions, switches, and short descriptions of each field. The specified information is displayed on the Field dialog box available from the RTF property category.

If you wish to customize the list of names available at your site, PTC recommends that you copy these files to the \importexport subdirectory of a custom directory, edit the copies, and set each client workstation to use that custom directory. Arbortext Import/Export will search \importexport (and all paths defined by the importexportpath Advanced Preference) for the first-found instance of word-builtin-styles.xml and word-fields.xml .



---

# Specifying_a_Custom_Template_File

If you want users to use a Word template file other than that shipped with Arbortext Import/Export , create the template file, save the template file from Word in RTF format, and copy the RTF template to the Arbortext Publishing Engine server. From each client workstation, run Arbortext Styler , choose File > Stylesheet Properties , and navigate to the RTF tab. Browse to or enter the path and file name of the RTF template in the Template File field. Users may override this setting by changing or deleting the value in this field.

If no template file is specified, only the Word styles defined in Arbortext-path \lib\importexport\lib\word-builtin-styles.rtf will be used for RTF formatting.

If you wish to include the user-defined style names in the style name lists of the RTF property category, you can create a custom version of word-builtin-styles.xml . To create the desired XML markup for word-builtin-styles.xml , consider using the following VBA macro to extract style names from any Word document or template and create the desired markup for paragraph and character styles. You will then need to extract the list paragraph styles from the <ParagraphStyles> list and add level attribute to indicate nesting level.

```
Sub PrintAllBuiltinStyles()
'
' Loop through the builtin styles
' and print the rtf-fields.xml markup
' to the "Immediate Window"
'
'
Dim aStyle As Style
Dim aStyles As Styles
Set aStyles = ActiveDocument.Styles
Debug.Print "<ParagraphStyles>"
For Each aStyle In aStyles
If aStyle.BuiltIn = True Then
If aStyle.Type = wdStyleTypeParagraph Then
Debug.Print "<StyleName>" + aStyle.NameLocal + "</StyleName>"
End If
End If
Next
Debug.Print "</ParagraphStyles>"
Debug.Print "<CharacterStyles>"
For Each aStyle In aStyles
If aStyle.BuiltIn = True Then
If aStyle.Type = wdStyleTypeCharacter Then
Debug.Print "<StyleName>" + aStyle.NameLocal + "</StyleName>"
End If
End If
Next
Debug.Print "</CharacterStyles>"
End Sub
Sub PrintAllUserDefinedStyles()
'
' Loop through the builtin styles
' and print the rtf-fields.xml markup
' to the "Immediate Window"
'
'
Dim aStyle As Style
Dim aStyles As Styles
Set aStyles = ActiveDocument.Styles
Debug.Print "<ParagraphStyles>"
For Each aStyle In aStyles
If aStyle.BuiltIn = False Then
If aStyle.Type = wdStyleTypeParagraph Then
Debug.Print "<StyleName>" + aStyle.NameLocal + "</StyleName>"
End If
End If
Next
Debug.Print "</ParagraphStyles>"
Debug.Print "<CharacterStyles>"
For Each aStyle In aStyles
If aStyle.BuiltIn = False Then
If aStyle.Type = wdStyleTypeCharacter Then
Debug.Print "<StyleName>" + aStyle.NameLocal + "</StyleName>"
End If
End If
Next
Debug.Print "</CharacterStyles>"
End Sub
```