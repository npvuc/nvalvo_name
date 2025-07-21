

---

# applyOverlay_attribute

Specifies whether the CMS browser should apply its default icon overlay logic (the corresponding value is 1.) Overlay icons represent an object's lock status. A 0 value indicates that the display icon is a composite icon that includes a lock status icon. This attribute is optional. The default is 1. A 0 value is ignored when no displayIcon is provided.



---

# CMSItemType_enumeration

The CMSItemType enumerated type indicates the type of object. Some values may be combined with others, as specified below.

The CMSItemType enumeration has the following constants of type int .



---

# CMSLockStatus_enumeration

The CMSLockStatus enumerated type indicates the lock status of an object.

The CMSLockStatus enumeration has the following constants of type int .



---

# displayIcon_attribute

Specifies the graphic icon used to represent this object instance in the Editor's CMS browser. The value is a relative pathname, and the standard search path is used. This attribute is optional and may contain an empty string.



---

# fullPath_attribute

Specifies the adapter-specific full path name of the CMS object. This attribute is optional and may contain an empty string.



---

# itemType_attribute

Contains a bit mask of the CMSItemType constants.



---

# lockStatus_attribute

Contains one of the CMSLockStatus constants.



---

# logicalId_attribute

Specifies the object's Logical ID.



---

# name_attribute

Specifies the human-readable object name.



---

# revision_attribute

Specifies the object's content management system (CMS) version identifier. This attribute is optional and may contain an empty string.