

---

# Line_Numbering_Limitations

- • Line numbers cannot be added to lines that consist entirely of generated text (for example, a table of contents or index).

- • FOSI stylesheets must be used. Line numbering is not supported with XSL-FO stylesheets.

- • The same FOSI must be used to apply and view the line numbers.

- • Performance on large documents will be slow and memory intensive.

- • Changes made outside of Arbortext Editor or Arbortext Publishing Engine may corrupt line and page markers.

- • Change tracking records must be either accepted or rejected before line numbering is applied.

- • Line numbers can only be displayed on the left side of the Edit window. However, line numbers can be set to appear on either side of a composed print document.

- • There is no support for languages without spaces between words (for example, Chinese, Japanese, and Korean).

- • Line numbering is only intended to work with XML documents.

- • Line numbering is not supported when using composition pipeline formatting (for example, line numbers cannot be applied to profiled documents).

- • Line numbering cannot be applied to documents that contain file entities that are referenced multiple times in a single document. Unexpected behavior may result.

- • Rules and leaders are ignored. Adjacent line breaks may not be marked up correctly.

The following limitations apply to the sample application, but are not necessarily limitations of the Arbortext Editor line numbering capability

- • Only single column output is supported.

- • Tables are accommodated, but not algroups .

- • Vertical spanning of cells is not supported.

- • Only top justified text in tables is supported.

Contact PTC Inc. consulting services for help developing your customized line numbering application.



---

# Line_Numbering_Namespace

The line numbering namespace and associated markup ( atipl tags) are described on the PTC Arbortext namespace web site at http://www.arbortext.com/namespace/index-of-arbortext-namespaces.html .



---

# Line_Numbering_Sample_Application

A sample line numbering application can be found in the samples\linenumbering folder in your installation directory. Use the following procedure to view an example of line numbering using this sample application. You'll need to have either Arbortext Styler or Print Composer installed and licensed to perform the following procedure:

## To Apply Line Numbers to a Sample Document: