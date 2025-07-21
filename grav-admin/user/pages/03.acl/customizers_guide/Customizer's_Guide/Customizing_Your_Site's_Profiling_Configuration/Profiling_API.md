

---

# Profile_Functions

profile_alias ( attr [, doc ])

Returns the alias name for the specified profile attribute.

Returns the number of profile aliases defined in the current (or other) profiling configuration file.

Returns 1 if the specified element can be profiled using the specified profile. Returns 0 if the element cannot be profiled, or if either oid or alias is invalid.

Returns the name of the profile attribute for the specified profile.

Returns the number of profile attributes defined in the configuration file associated with the profiling session.

Returns a document identifier for the current (in-memory) profiling configuration file.

Returns the conflict shading color for the profile for the specified document.

Returns the default value for the specified RADIO_PROFILE.

Returns the default value profilenode for the specified RADIO_PROFILE.

Returns 1 if the specified element can be profiled using the specified profile.

Returns the number of attribute name(s) and value(s) for the specified element that the specified profile can be applied to or not applied to.

Returns the number of elements the specified profile could be applied to or not applied to.

Returns 1 if the specified profile class is a FOLDERED_PROFILE.

Returns 1 if the specified profile class is a RADIO_PROFILE.

Returns 1 if the specified profile class is a STANDARD_PROFILE.

Returns 1 if the specified element would be included if the profile was resolved using the specified logical expression.

Returns the profilenode of type STANDARD_PROFILE, RADIO_PROFILE, or FOLDERED_PROFILE of a profile class.

Returns the number of profilenodes of type STANDARD_PROFILE, RADIO_PROFILE or FOLDERED_PROFILE in the current (or other) profile configuration file.

Returns the shading color of the profile attribute for the specified alias..

Returns an integer identifying the profile type of the specified alias.

Returns 1 if the specified alias is a valid profile.

Returns the allowed value profilenode for the specified value in the profile class identified by the specified alias.

Returns the number of allowed value profilenodes for the profile class identified by the specified alias.

Returns the value separator for the specified profile. The default value is a semicolon.

Returns the number of allowed values for the profile class identified by the specified alias.

Returns the colors for the profile attribute for the specified alias.



---

# Profile_Group_Functions

apply_profile_group ( apply_profile_group_name , arr [, doc ])

Returns the number of profile classes that are included in the specified apply profile group.

Returns 1 if the profile group apply_profile_group_name , is allowed on the element oid .

Returns 1 if the specified profile group is allowed on the specified element.

Returns the number of apply profile groups specified in the profile configuration file.

Returns the profile configuration file markup for the specified set profile group

Returns the number of set profile groups specified in the profile configuration file.

Returns the number of set profile groups, and the profile classes and relationships between profile values for the corresponding resolution group specified in the profiling configuration file.



---

# Profilenode_Functions

profilenode_ancestors ( profilenode , arr )

Returns the number of folders that are ancestors of the node identified by the specified node.

Returns the name of the profile attribute for the specified node.

Returns the number of nodes that are children of the specified node.

Returns the default value for a RADIO_PROFILE node as specified in the profile configuration file.

Returns the default value profilenode for a RADIO_PROFILE node as specified in the profile configuration file.

Returns 1 if the element can be profiled using the profilenode.

Returns the number of attribute name(s) and value(s) for an element that a particular profile could be applied to or not applied to.

Returns the number of elements that a particular profile could be applied to or not applied to.

Returns 1 if the root node of the specified node is a FOLDERED_PROFILE node.

Returns 1 if the root node of the specified node is a RADIO_PROFILE node.

Returns 1 if the root node of the specified node is a STANDARD_PROFILE node.

Returns the profile alias, folder name, or profile value of a profilenode.

Returns the profilenode of the immediate ancestor of the specified node.

Returns the top-level or root node for that profile class.

Returns the shading color for the specified profile node.

Identifies a profilenode's TYPE.

Returns 1 if the specified node is a valid profilenode identifier.

Returns the number of value profilenodes for the specified node.

Returns the value separator corresponding to the specified node. The default value is a semicolon.

Returns the number of allowed values for the specified node.