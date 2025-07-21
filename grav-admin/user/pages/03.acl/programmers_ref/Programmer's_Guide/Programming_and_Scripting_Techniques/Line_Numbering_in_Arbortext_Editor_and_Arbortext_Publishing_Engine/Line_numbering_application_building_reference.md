

---

# Tag_traversal_and_current_tag_conventions

Use the pagelayoutmarkers set option to control the display of the atipl markup, and the protectpagelayout set option to control whether or not it can be modified. The caret command will ignore atipl markup whenever it is not displayed, regardless of these command settings.

oid functions (for example, oid_next and oid_prev ) do not recognize atipl markup whether or not it is displayed in the Edit window. Line numbering applications must be written to handle cases where atipl markup may interfere with tag or oid navigation.

The atipl singleton tags do not affect the balancing of selections, but they must be treated as pairs in other respects by all edit operations. This markup is ignored by the spell checking code, so that word fragments split by these tags are seen as a single word.

Deletion, either forward or backward, will ignore any atipl markup to the left of the cursor if it is not displayed. The deletion operation will fail if the markup is displayed and protected.

In the context of line numbering applications, the current tag is defined as the tag to the left of the cursor. The atipl tags can only be treated as the current tag when they are displayed.



---

# The_atipl_layout_markup

The atipl tag set does not require a separate document type definition; it can be used with all document types. The definitions for these tags are in Arbortext-path \ lib\dtgen\atitag.cf , and the default formatting is defined in FOSI fragment located at Arbortext-path \ lib\atipl-eic.fos .

When the layout::apply function is called, a .layout file is created, using the structures defined in the layout.dtd to specify the composed layout of the document. The atipl singleton tags are then inserted as pairs around the document material that corresponds to the composed output structure they describe. Although atipl tags are singletons, if a particular tag cannot be inserted, its logical mate will not be inserted either. For example, if a <atipl:startcolumn/> tag cannot be inserted, the <atipl:endcolumn/> tag will also not be allowed.

Each start and end tag has a set of generic attributes. Every start tag also has a predefined set of attributes that correspond to the declared attributes of the matching element of the layout.dtd . For more detailed information on the layout.dtd , refer to section The Layout file and document type . The exceptions to this correlation are that the oid and offset attributes are not required, and the <atipl:startfloat/> tag has page, span, and column number attributes.



---

# The_Layout_file_and_document_type

The Layout document type defines the .layout file, which is produced by the Arbortext formatting engine and written to the .aptcache folder when line numbering is applied to a document. The .layout file specifies the structure of the document as it will appear in composed output, and defines where the atipl tags will appear.

The format of the .layout file is defined by the following document type definition. A typical declaration would be structured in this way:

```
<?xml version=1.0?>
<!DOCTYPE layout PUBLIC "-//Arbortext//DTD Layout 1.0//EN"
"layout/layout.dtd">
```



---

# The_line_numbering_namespace

The line numbering namespace and associated markup ( atipl tags) are described on the PTC Inc. namespace web site at: www.arbortext.com/namespace/index-of-arbortext-namespaces.html .