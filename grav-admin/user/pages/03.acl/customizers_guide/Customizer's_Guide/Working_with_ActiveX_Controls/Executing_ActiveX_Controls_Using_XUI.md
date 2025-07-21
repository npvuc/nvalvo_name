

---

# Example:_Embedded_Calendar_Control

This example uses XUI technology to embed the Microsoft Calendar control in a document based on the Arbortext XML DocBook (axdocbook) DTD and displayed in Arbortext Editor . When the user selects a date, the date is added as the content of the document's <date> element. Using the Calendar control for entering the date eliminates the possibility of the user mis-typing the date. The Calendar control also provides a well-known user interface for working with dates.



---

# Example:_Previewing_Word_and_Excel_Documents

This example demonstrates how ActiveX dialog boxes can be implemented at a script level. In this scenario, users need to be able to preview Word and Excel documents from within Arbortext Editor . Because this type of functionality is not document type specific, the file could be activated from a custom Arbortext Editor menu item.

The following file supports this example and is available at the following location:

```
Arbortext-path
\samples\activex\commdlg.xml
```

This example launches the Microsoft Common Dialog control, an ActiveX version of the standard File Open dialog box. The script launches Microsoft Excel or Word depending on the user's selection on the File Open dialog box. The only ActiveX piece of the implementation is the File Open dialog box. Launching of Word and Excel uses standard ACL COM functions.

```
<!--ArborText, Inc., 1988-2003, v.4002-->
<!DOCTYPE window PUBLIC "-//Arbortext//DTD XUI XML 1.0//EN"
"xui.dtd">
<window orient="horizontal" focus="opendlg" modal="false"
xmlns:ev="http://www.w3c.org/2001/xml-events">
<activex id="opendlg" progid="MSComDlg.CommonDialog"></activex>
<script type="application/x-vbscript"
ev:event="windowload"
ev:propagate="continue">
' Set flags
OpenDlg.Flags = cdlOFNHideReadOnly
' Set filters
OpenDlg.Filter = "Excel Files(*.xls)|*.xls|" & _
"Word Documents (*.doc)|*.doc|CSV Files(*.csv)|*.csv|Text Files" & _
"(*.txt)|*.txt|All Files (*.*)|*.*|"
' Specify default filter
OpenDlg.FilterIndex = 1
' Display the Open dialog box
opendlg.ShowOpen
index = OpenDlg.FilterIndex
filename = OpenDlg.filename
Application.ActiveWindow.Close()
if(filename <> "") then
' Let's launch Excel or Word as COM servers
' (Not to be confused with the ActiveX control from which
' we selected a file name.)
if(index = 1 or index = 3) then ' if .xls or .csv
' Open file in Excel
Dim hExcel 'handle to the Excel app
Dim hWorkbooks 'handle to Excel Workbooks object
set hExcel = CreateObject("Excel.Application")
hExcel.Visible = -1
set hWorkbooks = hExcel.Workbooks
hWorkbooks.Open(filename)
else ' for all other file types....
'Open file in MS Word
Dim hWord 'handle to the Word app
Dim hWordDocs
set hWord = CreateObject("Word.Application")
hWord.Visible = -1
set hWordDocs = hWord.Documents
hWordDocs.Open(filename)
end if
end if
</script>
</window>
```