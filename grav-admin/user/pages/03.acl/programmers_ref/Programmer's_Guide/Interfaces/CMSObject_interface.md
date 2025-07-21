

---

# aclId_attribute

Specifies the dobj ID equivalent to this CMSObject object. You can use this ID with the Arbortext Command Language (ACL) programming language. If this object is no longer valid, the attribute value will be 0 (an invalid dobj ID).

Each access returns a new dobj ID. The caller is responsible for calling the ACL dobj_close() function on each returned valid ID. Calling dobj_close() does not affect the original CMSObject or the IDs returned previously.



---

# allReferences_attribute

Returns a collection of all active object references to the same associated CMS object version.

Each CMSObject represents a specific reference (or usage) of a CMS object. If a CMS object references (through File Entity or XInclude) the same child object twice in different parts of the document content, then each reference would have its own CMSObject object. Use the allReferences attribute to write application code that iterates over all open references to this CMS object. Note that the class attribute of each reference may be different.

This attribute can return object references from multiple distinct documents.



---

# burst_method

Bursts the checked out object. The bursting process follows the established defaults and specific rules for the associated document type. If the object contains sibling (that is, more than one) top-level elements, it is not burst.



---

# cancelCheckout_method

Unlocks the object in the CMS without updating it. The adapter can optionally return the previous version of the object.



---

# checkin_method

Checks the object in to the CMS. To properly update the revised object in the CMS, you must save the object before calling this method.



---

# checkout_method

Locks the CMS object for modification. If the CMS_LOCK_FORCE flag is set and the object is locked by another user, the object will be forcibly unlocked if the caller has that right.

The exact semantics of this method are adapter-specific. For example, if a CMS does not support versioning then this may simply "lock" the object to prevent other users from editing it.



---

# CMSBurstFlags_enumeration

The CMSBurstFlags enumerated type is used to construct the flags parameter to the burst method by ORing any of the following options.

The CMSBurstFlags enumeration has the following constants of type int .



---

# CMSLockFlags_enumeration

The CMSLockFlags enumerated type is used to construct the flags parameter to the checkout method by ORing any of the following options.

The CMSLockFlags enumeration has the following constants of type int .



---

# CMSObjectClassType_enumeration

The CMSObjectClassType enumerated type is used with the objectClass read-only attribute.

The CMSObjectClassType enumeration has the following constants of type int .



---

# CMSObjectLockStatusType_enumeration

The CMSObjectLockStatusType enumerated type is used with the lockStatus read-only attribute.

The CMSObjectLockStatusType enumeration has the following constants of type int .



---

# cmsObjectType_attribute

Specifies the name of the CMS object type.



---

# cmsPathName_attribute

Specifies the path name of object in the CMS. If the object exists in multiple folders, any one of the folder paths could be returned.



---

# CMSSaveFlags_enumeration

The CMSSaveFlags enumerated type is used to construct the flags parameter to the save method by ORing any of the following options.

The CMSSaveFlags enumeration has the following constants of type int .



---

# comment_attribute

Specifies the check in or check out comment for the object.

There is currently no standard way of setting the comment for an object. This must be handled in an adapter-specific way.



---

# contentType_attribute

Specifies the type of the object's content.

For non-graphics, this may be one of the following values:

- • xml

- • sgml

- • html

- • text

- • ascii

For graphics and non-markup documents, this will be a file extension ("bmp", "gif", "jpg", "svg", "doc", etc.).



---

# createEvent_method

Creates an event of type CMSObjectEvent .



---

# creationDate_attribute

Specifies the object's creation date in an adapter-specific human-readable form.



---

# deleteObject_method

Deletes the object from the CMS. All versions of the object will be deleted. After calling this method, you can no longer use this CMSObject object.

If the CMS supports referential integrity, this will fail if any of the deleted object versions are referenced as children of other objects.



---

# enclosingObject_attribute

Specifies the object reference that encloses this particular CMS object reference. If this is a top level object, the value is null .

For example, if the user inserts reference to a "chapter" object into a checked out "book" object (via File Entity or XInclude) then the enclosingObject for the "chapter" object reference would be the containing "book" object.



---

# encoding_attribute

Specifies the character encoding of the object's content.

For most adapters, this attribute would only be available if the object was currently loaded.



---

# end_attribute

Specifies the last DOM Node associated with the object reference. You can reference a given CMS object in multiple places in either a single document or multiple documents. See allReferences for more details.

This may be null if this object reference is not currently associated with any DOM Nodes. For example, this could represent a folder object or an object whose content has not yet been loaded into a document.



---

# fullTextIndexed_attribute

Indicates whether the document is marked for full text indexing.



---

# getAttribute_method

Reads the value of an attribute. Attributes are identified by name. If the attribute has more than one value, an index is used to identify which value to return.

To get the values of multiple attributes, use the getAttributes method.



---

# getAttributes_method

Gets the values for a list of attributes. Attributes with a single value are stored as String entries in the returned PropertyMap . Attributes with multiple values are stored as StringList entries.



---

# getChildren_method

Retrieves the contents of a folder or the children of a document object.



---

# getParents_method

Returns an iterator over the set of documents that reference this object.



---

# getUserData_method

Retrieves application data from the object. This method enables user interface or application code to retrieve named data that was previously stored by calling the setUserData method.



---

# getVersions_method

Returns an iterator over all versions of the object.



---

# hasChildRefs_attribute

Specifies whether non-folder objects have any child object references.

A true value suggests that the getChildren method can safely be called to enumerate the children.



---

# instanceDoctypeName_attribute

Specifies the object's instance document type name. If the object's content contains a document type declaration such as...

<!DOCTYPE book PUBLIC "-//Arbortext//DTD DocBook XML V4.0//EN" "axdocbook.dtd">

then this attribute would represent the string book . Note that this value has nothing to do with the DTD or Schema associated with this object.

Some XML instances do not contain a document type declaration and so this value would be an empty string.

For most adapters, this attribute would only be available if the object was currently loaded.



---

# invokeExtension_method

Invokes an adapter-specific extension function. Some adapters provide functionality beyond the standard CMS API.



---

# isFolder_attribute

Indicates whether the object is a folder or folder subtype.



---

# isLatestVersion_attribute

Indicates whether this version is the most recent version of the object on a particular CMS branch.



---

# isVirtualDocContainer_attribute

Indicates whether the object contains references to child objects which are virtual document objects. Objects that reference all of their children using file entities, XIncludes, and graphic tags are not virtual document containers.



---

# lockable_attribute

Indicates whether the current user can attempt to lock the object. For example, if another user has the object checked out, this attribute should be false .

A true value is not a guarantee that a checkout will succeed since, for example, another user could have checked this out in the mean time.



---

# lockOwner_attribute

Specifies the CMS user name that currently holds the lock. Returns an empty string if the object is not locked.



---

# lockStatus_attribute

Specifies the lock status of this CMS object. The value is one of the CMSObjectLockStatusType enumerated constants.



---

# lockStatusDisplay_attribute

Specifies a human-readable string describing the lock status. For example, the value of this attribute could be "locked", "unlocked", and so forth. The returned string can be displayed in the user interface and should be localized.



---

# logicalId_attribute

Specifies the Logical ID of the object used for external binding. A Logical ID identifies a class of objects, any one of which may be selected at any given time. For example, a Logical ID can identify a specific version of a specific CMS object (fixed reference) or the current version (floating reference). Logical IDs are valid across sessions, and are stored inside structured documents. At any time, you can translate a Logical ID into a POID that identifies a specific version of a specific object.



---

# modificationDate_attribute

Specifies the object's last modification date in an adapter-specific human-readable form.



---

# modified_attribute

Will be true if the object's content has been modified in memory and has not yet been saved.



---

# move_method

Moves the object to a new folder in the CMS.



---

# name_attribute

Specifies the name of object. This is normally a human-readable name and is used primarily for display purposes.



---

# objectClass_attribute

Specifies the class of the CMS object. The value is one of the CMSObjectClassType enumerated constants.



---

# permission_attribute

Specifies the permissions associated with the object in a human-readable string. The format of the string is adapter-specific and is for display purposes only.



---

# poid_attribute

Specifies the Persistent Object Identifier (POID) associated with the object. This is different from a Logical ID, which can represent different versions of an object over time. For example, the Logical ID could represent the "LATEST" version of the object. The POID always references the same version of the object. An application programmer seldom needs to use a POID. Instead, they should mainly use the logicalId attribute.



---

# publicId_attribute

Specifies the Public ID of the object's DTD or Schema.

For most adapters, this attribute would only be available if the object was currently loaded.



---

# readOnly_attribute

Indicates whether the object's content is read-only. Note that this is independent of whether the current user has this object checked out because some adapter's may allow for such a combination.



---

# releaseReference_method

Releases this reference to the underlying repository object. After this call, most methods on this object will throw a CMSException with a code value of INVALID_CMSOBJECT_ERR . However, the valid attribute is always safe to access and will return false in this case.



---

# save_method

Saves a CMS object without checking it in (interim save). The object remains checked out.

Some adapters may support the saving of attributes for objects which are not checked out. See the CMS_SAVE_OBJECT_ATTR enumerated constant.



---

# session_attribute

Specifies the CMSSession object associated with this object.



---

# setAttribute_method

Sets the value of an attribute. Attributes are identified by name.

To set the values of multiple attributes, use the setAttributes method.



---

# setAttributes_method

Sets the values for a list of attributes. The calling function passes a PropertyMap containing entries for each of the attributes to be set. Attributes with a single value are stored as String entries in the PropertyMap . Attributes with multiple values are stored as StringList entries.



---

# setOldUserData_method

This method can be used to allow some properties and methods in this interface to work with older adapters ("Oracle iFS Adapter" or "Documentum Adapter"). Some older adapters require usage of a "user data" field with certain ACL functions (such as those starting with sess_ or dobj_ ). This allows such functionality of older adapters to be accessed via this AOM interface.

This may be used with the following methods:

- • getChildren()

- • getParents()

- • getVersions()

- • save()

- • checkout()

- • checkin()

- • cancelCheckout()

- • deleteObject()

- • move()

This stores the given data for use with the next method call which can make use of it. After that method call, the stored data will be automatically erased so it won't affect future calls.



---

# setUserData_method

Stores some application data on the object. Any existing data for the same key is replaced by the new data. This method enables user interface or application code to associate named data with the object, that it can later retrieve by calling the getUserData method. User data only exists in memory and is not stored persistently.

Some adapters may support additional arguments to certain methods by having the application call setUserData with a predefined key just before calling the method. The adapter documentation will describe any such additional arguments.



---

# size_attribute

Specifies the size of the object content in bytes. This is optional and some adapters may choose to not implement it.



---

# start_attribute

Specifies the first DOM Node associated with the object reference. You can reference a given CMS object in multiple places in either a single document or multiple documents. See the allReferences attribute for more details.

This may be null if this object reference is not currently associated with any DOM Nodes. For example, this could represent a folder object or an object whose content has not yet been loaded into a document.



---

# systemId_attribute

Specifies the System ID of the object's DTD or Schema.

For most adapters, this attribute would only be available if the object was currently loaded.



---

# tagName_attribute

Specifies the tag name for the top-level element in the object. The value is blank for objects with unstructured content.



---

# valid_attribute

Indicates whether this still represents a valid object reference. For example, if the associated session has been disconnected then this object reference is considered invalid.



---

# version_attribute

Specifies the CMS version ID of the object in an adapter-specific format. This is for display purposes only.