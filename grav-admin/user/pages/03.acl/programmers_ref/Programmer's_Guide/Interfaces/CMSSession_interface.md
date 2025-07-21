

---

# aclId_attribute

Represent the session ID associated with the CMSSession object. You can use this ID with the Arbortext Command Language (ACL) programming language. If the session is no longer valid, the aclld value is an invalid session ID ( -1 ).



---

# adapter_attribute

Specifies the CMSAdapter object associated with this session.



---

# burstDocument_method

Bursts the specified file system document using this session. If the specified document contains more than one top-level element, it will not be burst.



---

# burstPolicy_attribute

Represents the burst policy of the adapter. The value is one of the CMSBurstPolicy enumerated constants.



---

# burstUserOverride_attribute

Set to true if this session has the user override set to on for bursting-related options such as object names. This setting allows the user to override certain options that would otherwise be completely dictated by the bursting rules. Set to false if it is not. This setting prevents the user from overriding the bursting options.



---

# clearBurstConfig_method

This is a special method for administrators to use while they are developing the burst configuration files. It clears out all of the burst configuration settings you have loaded and reloads the system-wide settings. The document type-specific configurations are loaded as they are needed -- for example, when a document of that document type is burst. This enables new settings to be tested without having to exit Arbortext Editor . This method does not change the folder that Arbortext Editor uses to load burst configuration files.



---

# CMSBurstBoundaryType_enumeration

The CMSBurstBoundaryType enumerated type specifies the available types of bursting that can be configured for any given element. It is used with the getBurstBoundaryType method.

The CMSBurstBoundaryType enumeration has the following constants of type int .



---

# CMSBurstPolicy_enumeration

The CMSBurstPolicy enumerated type specifies when document bursting should occur. It is used with the burstPolicy attribute.

The CMSBurstPolicy enumeration has the following constants of type int .



---

# CMSCreateFlags_enumeration

The CMSCreateFlags enumerated type is used to construct the flags parameter to the createObjectFromSubtree and createNewObject methods by ORing any of the following options.

The CMSCreateFlags enumeration has the following constants of type int .



---

# CMSOperationEnabledType_enumeration

The CMSOperationEnabledType enumerated type is used as the return value of the verifyOperationEnabledInCurrentState method.

The CMSOperationEnabledType enumeration has the following constants of type unsigned short .



---

# CMSSessBurstFlags_enumeration

The CMSSessBurstFlags enumerated type is used to construct the flags parameter to the burstDocument method by ORing any of the following options. The negative flags allow the application developer to override the default session bursting rules.

The CMSSessBurstFlags enumeration has the following constants of type int .



---

# connected_attribute

Set to true if the session is still connected. Set to false if it is not.



---

# createEvent_method

Creates a CMSSession event.



---

# createFolder_method

Creates a new CMS folder object



---

# createNewObject_method

Creates an empty CMS object of the same type as the specified document. If bursting rules are set up, you may use them to supply or override some of the parameter values.



---

# createObjectFromSubtree_method

Creates a new CMS object, assigning content from an in-memory document. If the new object is a folder or an empty document, use null values for the start and end parameters. If bursting rules are setup, you may use them to supply or override some of the parameter values.

After successful completion, the given DOM Nodes will be associated with the new CMS object. However, this does not replace the Nodes with a file entity or XInclude reference and so the association will be lost when the containing document is closed unless some additional action is performed.



---

# currentUser_attribute

Specifies the current CMS user name. This will normally match the loginId parameter to the CMSAdapter.connect() method which established this session.



---

# defaultFolder_attribute

Specifies the Logical ID of the current user's default folder.



---

# disconnect_method

Closes the CMS session. Only the connected attribute can be safely accessed after this method is called.



---

# fullTextSearch_attribute

Indicates whether to index new documents for full-text searching. Not all adapters will implement full text searching.



---

# getAttribute_method

Reads the value of a session attribute. Attributes are identified by name. The attribute names supported by this method will vary with each adapter.



---

# getBurstBoundaryType_method

For the given node , determines the burst boundary type according to the bursting rules associated with this session.



---

# getDefaultCreateInfo_method

Returns the default object creation information that is not specific to any particular document type. This information is defined in the atidefaults configuration file.

The information is returned in a PropertyMap . The following table shows the supported key string values:



---

# getFile_method

Downloads an object from the CMS to a local file and returns the local path name. This method is typically used to retrieve graphic objects.



---

# getFileMappingEntry_method

Checks whether a resolved path name already exists in the CMS. You use this method to avoid creating multiple CMS objects from a single source file -- for example, by loading multiple entity references to one file. Before calling this method, use the objectReuse attribute to determine if this session is managing file mapping entries or not.



---

# getGraphicCreateInfo_method

Returns the default creation information for a new graphic object. This information is defined in the atidefaults configuration file.

The information is returned in a PropertyMap . The following table shows the supported key string values:



---

# getRangeCreateInfo_method

Returns the default creation information for a new object, according to the given start and end Nodes. This information can be defined in a configuration file that is specific to the document type associated with the given Nodes. As a fallback, Arbortext Editor and Arbortext Publishing Engine will use the atidefaults configuration file.

The information is returned in a PropertyMap . The following table shows the supported key string values:



---

# getUserData_method

Retrieves application data from the session. This method enables user interface or application code to retrieve named data that was previously stored by calling the setUserData method.



---

# invokeExtension_method

Invokes an adapter-specific extension function. Some adapters provide functionality beyond the standard CMS API.



---

# logicalIdToPoid_method

Translates a Logical ID to a Persistent Object Identifier (POID). POIDs are used internally by Arbortext Editor and Arbortext Publishing Engine and are not normally used by an application developer.



---

# objectExists_method

Indicates whether an object exists in the CMS. The object is identified by a Logical ID. It is sufficient for this method to ensure that the Logical ID or Persistent Object Identifier (POID) format is correct. To verify the object's actual existence in the CMS, and its accessibility, Application.constructObject must be used.



---

# objectReuse_attribute

Indicates whether the session supports object reuse during bursting by maintaining a Logical ID and filename cache. See the setFileMappingEntry for more details.



---

# poidToLogicalId_method

Translates a Persistent Object Identifier (POID) and version to a Logical ID. POIDs are used internally by Arbortext Editor and Arbortext Publishing Engine and are not normally used by an Application Developer.



---

# putFile_method

Stores a file in the CMS. If the adapter is tracking imported files (see the objectReuse attribute), an entry is created in the persistent lookup table associating the filename with the new Logical ID. See the getFileMappingEntry method for more details.



---

# refreshObjectStatus_method

To improve performance, the internal implementation keeps track of the lock and read-only status of all constructed objects. This method will cause all constructed objects to refresh this information from the adapter. All appropriate views will be updated (if needed) to reflect any change in an object's status.



---

# search_method

Searches the CMS for objects that match the specified search criteria. The criteria string is created by the search dialog. Its format is adapter-specific.



---

# sessionToken_attribute

Specifies an adapter-specific session identifier that can be used to make calls directly into the CMS vendor API.

This attribute might not be supported by all adapters.



---

# setAttribute_method

Sets the value of a session attribute. The attribute names supported by this method will vary with each adapter.



---

# setFileMappingEntry_method

Instructs the adapter to persistently store a path name to a Logical ID association. If a mapping already exists for the path name, it will be replaced with the new Logical ID. Use this method in conjunction with the getFileMappingEntry method to prevent creating multiple CMS objects based on a single file.

The getFileMappingEntry and setFileMappingEntry calls are not atomic. During bursting, a new CMS object is created between the getFileMappingEntry and setFileMappingEntry calls. If multiple processes are performing burst operations, the result might be multiple CMS objects for the same source file. For example, assume process A and process B both call the getFileMappingEntry method at the same time and find that an association does not currently exist. Both processes then create new CMS objects and call the setFileMappingEntry method to create the association. The last setFileMappingEntry call takes precedence, and its CMS object will be reused by subsequent burst operations. The other CMS object continues to exist and be referenced by its XML document.

There is no standard way to tell the adapter to remove a path name to Logical ID mapping.



---

# setOldUserData_method

Can be used to allow some methods and properties in this interface to work with older adapters ("Oracle iFS Adapter" or "Documentum Adapter"). Some older adapters require usage of a "user data" field with certain ACL functions (such as those starting with sess_ or dobj_ ). This allows such functionality of older adapters to be accessed via this AOM interface.

This may be used with the following methods...

- • disconnect()

- • getFile()

- • putFile()

- • createObjectFromSubtree()

- • createNewObject()

- • search()

This stores the given data for use with the next method call which can make use of it. After that method call, the stored data will be automatically erased so it won't affect future calls.



---

# setUserData_method

Stores some application data on the session. Any existing data for the same key is replaced by the new data. This method enables user interface or application code to associate named data with the session, which it can retrieve later by calling the getUserData method. User data only exists in memory, and is not stored between sessions.

Some adapters may support additional arguments to certain methods by having the application call setUserData with a predefined key just before calling the method. The adapter documentation will describe any such additional arguments.



---

# verifyOperationEnabledInCurrentState_method

Indicates whether an operation is allowed in the current state. Some adapters support more than one mode, and different operations may be allowed in each mode. Arbortext Editor does not define what modes or states are possible. Instead, it asks the adapter which operations are enabled in the current state.