

---

# DefaultFont_Element

The <DefaultFont> element specifies the default font used when creating PDF files. It’s optional and may be used once.

The <DefaultFont> element has one optional child element, <FontName> .

The <DefaultFont> element has no attributes.



---

# EmbedAlways_Element

The <EmbedAlways> element specifies the fonts that are embedded in the PDF file. However, <EmbedNever> takes precedence over <EmbedAlways> .

The <EmbedAlways> element has one child element, <FontName> .

The <EmbedAlways> element has the following attributes and values:



---

# EmbedNever_Element

The <EmbedNever> element specifies the fonts that you do not want embedded in the PDF file. When <EmbedAlways> is specified, <EmbedNever> takes precedence over <EmbedAlways> .

The <EmbedNever> element has one child element, <FontName> .

The <EmbedNever> element has no attributes.



---

# Locations_Element

The <Locations> element can provide additional directories to add to the search path for locating font files such as AFM, PFA, TTF, and so on. It’s optional and can only be used once.

The <Locations> element has one optional child element, <Path> .

The <Locations> element has no attributes.



---

# Map_Element

The <Map> element maps the .tfm file names to fonts that will be embedded in the PDF file. It’s optional and repeatable.

The <Map> element must specify one of the child elements, <FontName> or <FontPath> .

The <Map> element has the following attributes and values:



---

# Simulation_Element

The <Simulation> elements can apply bold or italic simulation to fonts that are not specified in FontName , are not mapped in this configuration file, and do not have the specified font face available. It’s optional and can only be used once.

The <Simulation> element has the optional child elements Bold and Italics .

The <Simulation> element has no attributes.



---

# Substitute_Element

The <Substitute> element specifies a different font for producing the PDF file than was used in the original document. The replacement font must have the same font metrics as the original font. The original font name should be followed by the name of one or more real font names. The first matching replacement font found will be used. Arbortext Editor and Arbortext Publishing Engine use the first replacement font that matches the selection criteria. It’s optional and repeatable.

The <Substitute> element has one child element, <FontName> , which specifies the source and target font mapping. The target <FontName> is required and repeatable.

The <Substitute> element has no attributes.