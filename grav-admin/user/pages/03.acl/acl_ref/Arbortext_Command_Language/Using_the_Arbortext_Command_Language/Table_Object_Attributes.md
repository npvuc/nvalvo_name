

---

# Dimensions_in_Attributes

A number of attributes specify dimensions: 3 inches, 2 pixels, etc. Such attribute values are specified as a “unitdim”, a floating-point number followed by a unit (for example, 3.0in , 2.0px ). Valid units are in , pt , pi , px , cm , mm , or % , meaning inches, points, picas, pixels, centimeters, millimeters, or percent.

## Related Topics

- • Shared table attributes

- • Set table attributes

- • Grid table attributes

- • Column table attributes

- • Row table attributes

- • Cell table attributes

- • Rule table attributes

- • tbl_obj_attr_clear

- • tbl_obj_attr_delete

- • tbl_obj_attr_get

- • tbl_obj_attr_set



---

# Mandatory_Attribute_Values

Table object attributes always have a value, even if the value is meaningless. ACL programmers should account for this. For example, if the table markup specifies no row height, Arbortext Editor wants to display the row with the minimum height needed to handle the contents of the cells in the row. Since there's always a value for a row's TARGET_HEIGHT we provide a second attribute, USE_TARGET_HEIGHT , which is zero ( 0 ) or one ( 1 ) to indicate whether the value in TARGET_HEIGHT should be used or ignored.