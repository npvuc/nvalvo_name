

---

# startcolumn_and_endcolumn

```
<!ELEMENT atipl:startcolumn EMPTY>
<!ATTLIST atipl:startcolumn
number NMTOKEN #IMPLIED
%commonattrs; >
<!ELEMENT atipl:endcolumn EMPTY>
<!ATTLIST atipl:endcolumn
%commonattrs; >
```

Columns within a span are indicated by the startcolumn and endcolumn markup. The number attribute indicates the column number. To force a column break, set attr2 to force .



---

# startfloat_and_endfloat

```
<!ELEMENT atipl:startfloat EMPTY>
<!ATTLIST atipl:startfloat
class CDATA #IMPLIED
flid CDATA #IMPLIED
pagetype CDATA #IMPLIED
%commonattrs; >
<!ELEMENT atipl:endfloat EMPTY>
<!ATTLIST atipl:endfloat
%commonattrs; >
```

Floats are parts of a document that do not appear in a set order. Rather, floats appear at the top or bottom of a page, span, or column. The class , flid , and pagetype attributes refer to FOSI concepts associated with every float.



---

# startline_and_endline

```
<!ELEMENT atipl:startline EMPTY>
<!ATTLIST atipl:startline
typemask CDATA "1"
%commonattrs; >
<!ELEMENT atipl:endline EMPTY>
<!ATTLIST atipl:endline
hyphen NMTOKEN #IMPLIED
%commonattrs; >
```

The startline and endline markup indicates the line breaks as defined by the formatting engine. The type of content in a line is indicated by the typemask attribute. The bits that may appear in a typemask indicate whether that content is plain or generated text, and are displayed in the following table:

If a line ends with a hyphen, the character code of the hyphen is added to the hyphen attribute on the end tag.

The margin where the line numbers appear in the printed output is defined by the value of attr2 . Legal values are left or right . The default is right .

The quadding of the number, relative to the page center, is defined by the value of attr3 . This value may be in or out . The default value is out .

The end of a line, where a break is no longer discretionary, may require special treatment. Set attr2 to fill on the end tag to end a line with a filler space that prevents an underfull error.



---

# startpage_and_endpage

```
<!ELEMENT atipl:startpage EMPTY>
<!ATTLIST atipl:startpage
number NMTOKEN #IMPLIED
%commonattrs; >
<!ELEMENT atipl:endpage EMPTY>
<!ATTLIST atipl:endpage
%commonattrs; >
```

The startpage markup indicates the start of a page, as determined by Arbortext Editor 's formatting engine. The number attribute gives the sequential page number.

A folio may be set for the attr1 attribute. It will appear as part of the line number in the format: folio,\-\,lineno .

The type of page break to force is controlled by the attr2 attribute. Valid values are next , verso , and recto . The default is to not force a page break.

The endpage markup specifies the end of a page. If the attr2 attribute is set to the fill , then underfull errors are not reported for this page and the page is not stretched if it is short.



---

# startrow,_endrow,_startentry,_and_endentry

```
<!ELEMENT atipl:startrow EMPTY>
<!ATTLIST atipl:startrow
number NMTOKEN #IMPLIED
%commonattrs; >
<!ELEMENT atipl:endrow EMPTY>
<!ATTLIST atipl:endrow
%commonattrs; >
<!ELEMENT atipl:startentry EMPTY>
<!ATTLIST atipl:startentry
number NMTOKEN #IMPLIED
vspan NMTOKEN #IMPLIED
hspan NMTOKEN #IMPLIED
%commonattrs; >
<!ELEMENT atipl:endentry EMPTY>
<!ATTLIST atipl:endentry
%commonattrs; >
```

The startrow , endrow , startentry , and endentry markup specifies the rows and columns of a table. The number attribute of a row is reset on every page, likewise the number attribute of an entry is reset in every row. The vspan and hspan attributes indicate that an entry is spanning. The former indicates the number of cells spanned vertically, the latter indicates the number spanned horizontally.



---

# startspan_and_endspan

```
<!ELEMENT atipl:startspan EMPTY>
<!ATTLIST atipl:startspan
number NMTOKEN #IMPLIED
columns NMTOKEN #IMPLIED
%commonattrs; >
<!ELEMENT atipl:endspan EMPTY>
<!ATTLIST atipl:endspan
%commonattrs; >
```

The start and end of a spanned column are specified by the startspan and endspan markup. For example, a page that contains two columns of text followed by a page wide table will consist of two spans. The span number, which is reset on every page, is indicated by the attribute number . The number of columns is indicated by columns .



---

# type,_location,_error_and_generic_attributes

```
<!ENTITY % commonattrs
"type (forced|discretionary) "discretionary"
location (inline|display) "inline"
xmlns:atipl CDATA #IMPLIED
error CDATA #IMPLIED
attr1 CDATA #IMPLIED
attr2 CDATA #IMPLIED
attr3 CDATA #IMPLIED
attr4 CDATA #IMPLIED
attr5 CDATA #IMPLIED
attr6 CDATA #IMPLIED
attr7 CDATA #IMPLIED
attr8 CDATA #IMPLIED
attr9 CDATA #IMPLIED" >
```

The type , location and error attributes are used to control the method for generating formatting characteristics for an element and are set during the generation of layout markup. These attributes should not be modified.

The attributes attr1 through attr9 are generic attributes that can be used by the application writer to customize page layout applications. By convention, attr1 is used to display automatically generated text, such as line numbers.