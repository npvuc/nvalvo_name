

---

# composed_Argument_Options

The composed argument outputs a formatted copy of your document. The following options are valid when the composed argument is valid.

- • panel — Opens the Print Published View dialog box for printing.

- • all , current , page_range , page_list — Control what portion of the document to print:

- • onepass , allpasses , and noformat — Control the formatting process that precedes the print:

- • auto and force — Control how Arbortext Editor decides whether a document instance requires formatting:

- • wait and nowait — Control whether Arbortext Editor should wait for the print to complete (that is, spool) before continuing to execute commands:

- • portrait and landscape — Control the orientation of the output on the paper. If neither is specified, portrait is assumed.

- • collate and nocollate — Controls whether the output is collated. If neither is specified, nocollate is assumed.

- • papersize — Controls the size of the paper on which the document is printed. Specify one of the following options:

- • paperheight and paperwidth — Allow you to specify the height and width of nonstandard paper. Allowable units of measure are: pc , pt , cm , mm , and in .

- • printer — Sends the document to a specific printer if you have more than one printer attached to your system.

- • file — Writes a PostScript version of your document to the specified file.

- • color — Generates color PostScript (requires PostScript level II compatible printer) or monochrome for black and white. Color is the default.

- • copies — Specifies the number of copies to be printed.

- • stylesheet — Specifies a stylesheet for a publishing request to the Arbortext Publishing Engine from Arbortext Editor . You must specify e3: stylesheet-path , where the path is an absolute path to the stylesheet file name. This option is not available if you use panel . The option is ignored if you are not using the Arbortext Publishing Engine for publishing documents .

Following are examples of the print composed command:

```
print composed
print composed current
print composed 3
print composed 2-6
print composed 14-11,9,7-3,1
print composed all copies=4 printer=lw
print composed file=thesis
```

## Related Topics

- • execute command

- • preview command

- • Formatting pass reduction in ACL



---

# editor_Argument_Options

Use the editor argument to print the document as it displays in the Edit view, Document Map, or Column view (whichever has focus). The output will reflect the current display font size and tag display settings.

The following options are valid when the editor argument is valid.

- • panel — Opens the Print Editor View dialog box for printing.

- • all , screen , and selection — Control what portion of the document instance to print:

- • portrait and landscape — Control the orientation of the output on the paper. If neither is specified, portrait is assumed.

- • header and footer — Specify what will print on the top and bottom of the page. The following options are associated with the header and footer arguments:

- • leftmargin and topmargin — Allow you to specify in decimal numbers the indentation from the left or top edge of the paper, respectively, to the point at which the text area is to begin. If you do not specify the unit on the indentation, inches are assumed.

- • printer — Sends the document to a specific printer. If the name includes spaces or special characters, the name must be enclosed with quotes.

- • file — Writes a PostScript version of your document to the specified file.

- • color — Generates color PostScript (requires PostScript level II compatible printer) or monochrome for black and white. Color is the default.

- • copies — Specifies the number of copies to be printed.

Following are examples of the print editor command:

```
print editor all
print editor screen
print editor selection
print editor selection \
header='FORMAT ERROR' footer=datemark \
leftmargin=2
print editor screen header=none \
footer=pageno topmargin=2.5cm
print editor selection printer=lw \
```