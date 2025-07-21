

---

# Annotations_Element

The <Annotations> element controls the display f bookmarks, links, and other features in the PDF file. It’s optional and may be used once.

The <Annotations> element has no child elements.

The <Annotations> element has the following attributes:



---

# Compatibility_Element

The <Compatibility> element specifies the type of PDF file that is produced. It’s optional and may be used once.

The <Compatibility> element may have either a <PDF> or <PDFX> child element.

The <Compatibility> element has no attributes.



---

# Compression_Element

The <Compression> element specifies the type and level of compression. It’s optional and may be used once.

The <Compression> element has no child elements.

The <Compression> element has the following attributes:



---

# Cropmarks_Element

The <Cropmarks> element specifies the characteristics of crop marks and whether they appear in the PDF output. It’s optional and may be used once.

The <Cropmarks> element has no child elements.

The <Cropmarks> element has the following attributes:



---

# Docinfo_Element

The <Docinfo> element specifies document properties in the PDF being created. It’s optional and may be used once.

The <Docinfo> element has one required child element, <Entry> , which specifies the document property names and their values.

The <Docinfo> element has no attributes.



---

# Images_Element

The <Images> element specifies how graphics are handled in the PDF file. It’s optional and may be used once.

The <Images> element has one optional child element, <DownSample> .

The <Images> element has two attributes:



---

# Merge_Element

The <Merge> element allows inserting existing PDFs into the PDF being created. It’s optional and may be used once.

The <Merge> element has one required child element, <Insert> , which specifies the insertion instructions.

The <Merge> element has no attributes.



---

# Open_Element

The <Open> element controls the characteristics of the PDF file when it is opened. It’s optional and may be used once.

The <Open> element has no child elements.

The <Open> element has the following attributes:

Use the following guidelines:

- • Setting pageLayout = default ignores the other settings.

- • For a single page non-scrolling view, use pageLayout = single and continuous = no (ignores facing ).

- • For a single page scrolling view, use pageLayout = single and continuous = yes (ignores facing ).

- • For a two page scrolling view that starts with first page on the left side, use pageLayout = twoup , continuous = yes , and facing = no .

- • For a two page scrolling view that starts with first page on the right side and then continues with facing pages, use pageLayout = twoup , continuous = yes , and facing = yes .

- • For a two page non-scrolling view that starts with the first page on the left side, use pageLayout = twoup , continuous = no , and facing = no .

- • For a two page non-scrolling view that starts with the first page on the right side and then continues with facing pages, use pageLayout = twoup , continuous = no , and facing = yes .



---

# Security_Element

The <Security> element limits access to the PDF file. It’s optional and may be used once.

The <Security> element has no child elements.

The <Security> element has the following attributes and values:

For detailed information about attribute inter-dependencies see Adobe documentation.