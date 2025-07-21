

---

# PDF_Element

The <PDF> element specifies the version of the PDF file.

The <PDF> element has no child elements.

The <PDF> element has one attribute, level = 1.3 | 1.4 | 1.5 | 1.6 . The default is 1.4 . PDF versions 1.3, 1.4, 1.5, 1.6, and 1.7 are supported by Adobe Acrobat 4.0, 5.0, 6.0, 7.0, and 8.0 respectively.



---

# PDFX_Element

The <PDFX> element specifies the PDF/X standards series, which provides a consistent and robust subset of PDF which can be used to deliver data suitable for commercial printing. The driver can generate output conforming to the following variations of PDF/X:

- • PDF/X-1 and PDF/X-1a, both defined in ISO 15930-1:2001

- • PDF/X-3 as defined in ISO 15930-3:2002

PDF/X is specified using the <PDFX> tag within the <Compatibility> tag. If you specify <PDFX> , you need to set the enabled attribute of the <Annotations> element to no .

The <PDFX> element has no child elements.