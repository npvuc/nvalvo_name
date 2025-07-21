

---

# With_FOSI

You can generate document properties for the PDF by placing FOSI information anywhere in a document (or in a FOSI that places it anywhere in the document).An example showing the use of atidmd:DocInfo is given below:

```
<atidmd:DocumentMetaData>
<atidmd:DocInfo>
<atidmd:Entry>
<atidmd:Key>Title</atidmd:Key><atidmd:Value>Moby Dick</atidmd:Value>
</atidmd:Entry>
<atidmd:Entry>
<atidmd:Key>Author</atidmd:Key><atidmd:Value>Herman Melville</atidmd:Value>
</atidmd:Entry>
</atidmd:DocInfo>
<atidmd:DocumentMetaData></para>
```