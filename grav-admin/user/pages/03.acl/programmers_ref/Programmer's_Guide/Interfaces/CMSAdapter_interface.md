

---

# aclId_attribute

Specifies the adapter ID associated with this CMSAdapter object. You can use this ID with the Arbortext Command Language (ACL) programming language such as with the sess_connect() function. However, such usage is discouraged because the appropriate AOM method should be used instead.



---

# connect_method

Establishes a content management system (CMS) session. On success, this session will become the "active" session. See the activeSession attribute of the Application interface for more details.



---

# createEvent_method

Creates a CMS adapter event.



---

# getUserData_method

Retrieves application data from the adapter. This method enables user interface or application code to retrieve named data that was previously stored by calling the setUserData method.



---

# hasFeature_method

Indicates whether this adapter implements a specified feature.



---

# name_attribute

Specifies the human-readable name for this adapter.



---

# qualifiedName_attribute

Specifies the adapter qualified name associated with this adapter. Each adapter is guaranteed to have a unique qualified name.



---

# setOldUserData_method

Can be used to allow the connect method to work with older adapters ("Oracle iFS Adapter" or "Documentum Adapter"). Some older adapters require usage of a "user data" field while connecting.

This stores the given data for use with the next call to the connect method. After that call, the stored data will be automatically erased so it won't affect future calls.



---

# setUserData_method

Stores some application data on the adapter. Any existing data for the same key is replaced by the new data. This method enables user interface or application code to associate named data with the adapter, which it can later retrieve by calling the getUserData method. User data is not saved between Arbortext Editor or Arbortext Publishing Engine sessions.

Some adapters may support additional arguments to certain methods by having the application call setUserData with a predefined key just before calling the method. The adapter documentation will describe any such additional arguments.



---

# valid_attribute

Indicates whether this adapter object is still valid. Some (older) adapters can get unloaded before application exit.