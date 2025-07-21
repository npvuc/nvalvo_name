

---

# PDF_Configuration_Files_for_FOSI

The distributed configuration files are:

- • Arbortext-path \lib\standard.pdfcf

- • Arbortext-path \lib\screen.pdfcf

- • Arbortext-path \lib\print.pdfcf

- • Arbortext-path \lib\smallfile.pdfcf

You can create a custom PDF configuration file ( custom-file-name .pdfcf ) and put it in Arbortext-path \custom\lib , where it will be automatically accessible when Arbortext Editor or Arbortext Publishing Engine starts. You can also put a set pdfconfigfile statement in a custom ACL file placed in Arbortext-path \custom\init\ custom-file-name .acl , where it will be loaded at start time.

The structure and content of the .pdfcf PDF configuration file is explained in PDF DTD Element Usage (FOSI) and the sections that follow it.



---

# PDF_Configuration_Files_for_PTC_APP

The distributed configuration files are:

- • Arbortext-path \app\standard.appcf

- • Arbortext-path \app\postscript.appcf

You can save a custom version of files if you wish to tailor your own PDF publishing process/output. Open the file in Arbortext Editor (without a stylesheet), make changes, then save the custom file, with the same file extension, in any of these locations:

- • Publishing PDF from Arbortext Editor or Arbortext Styler — you can browse for a custom file, or locate it in the APTCUSTOM \app directory where PTC APP will find it

- • Publishing PDF via Arbortext Publishing Engine — a custom file must be located on the PE server, in any of these locations:

Custom .appcf files must contain a single Print and a single Format element, although these do not require child elements to be valid.

See PDF Configuration File for the APP Engine (.appcf) and Print and PDF Configuration Files for PTC ALD Publishing for information about custom configuration files.