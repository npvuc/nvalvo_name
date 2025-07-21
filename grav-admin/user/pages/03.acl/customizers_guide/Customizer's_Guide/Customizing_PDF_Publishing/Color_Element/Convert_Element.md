

---

# CMYK_Element

The <CMYK> element specifies the eight digit hexadecimal representation of a color based on eight bits each of cyan, magenta, yellow, and black.

The <CMYK> element has no child elements.

The <CMYK> element has no attributes.



---

# Grayscale_Element

The <Grayscale> element specifies the three digit hexadecimal representation of grayscale based on twelve bit grayscale value.

The <Grayscale> element has no child elements.

The <Grayscale> element has no attributes.



---

# Model_Element

The <Model> element transforms any color from the source color model to the target color model. It’s optional and repeatable.

The <Model> element has no child elements.

The <Model> element has the following attributes:



---

# RGB_Element

The <RGB> element specifies the six digit hexadecimal representation of a color based on eight bits each of red, green, and blue.

The <RGB> element has no child elements.

The <RGB> element has no attributes.



---

# Spot_Element

The <Spot> element specifies the mapping of one specified color to another specified color. It’s optional and repeatable.

The <Spot> element specifies the mapping using the child elements <CMYK> , <Grayscale> , or <RGB> . Specify the mapping by using the form source,target . The source color will be replaced with the target color.

The <Spot> element has no attributes.