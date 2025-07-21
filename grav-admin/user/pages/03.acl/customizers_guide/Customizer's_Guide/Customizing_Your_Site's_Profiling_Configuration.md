

---

# .pcf_(Profile_Configuration_File)

# .pcf (Profile Configuration File)

A profile configuration file ( .pcf ) is an XML document specifying profile values that can be applied to any elements (or a limited number of elements) in a document type. A document type's .dcf file specifies the .pcf file to use for the document type's profiling configuration. Several document types can use the same .pcf file for their profiling configurations.

A .pcf file has the following structure:

- • A top-level <Profiles> element contains all of the <ProfileClasses> elements in the configuration file.

- • <ProfileClasses> elements define the profile classes of related individual profiles and groups of individual profiles for applying at editing time and setting at publishing time. <ProfileClasses> elements contain the <Profile> , <ApplyProfileGroup> , and <SetProfileGroup> elements.

- • <Profile> elements define individual profiles that authors can apply to elements at editing time and select to produce profiled output. With the <Profile> element, you can specify:

- • <ApplyProfileGroup> elements specify groupings of individual profiles the author can apply to elements at editing time.

- • <SetProfileGroup> elements specify groupings of individual profiles the author can set at publishing time. Individual profiles can be included and excluded using logical expressions.



---

# Configuring_Profiles

# Configuring Profiles

This section covers the profile configuration process and provides examples of profile configurations.



---

# Profiling_API

# Profiling API

Profiles are organized into folders and sub-folders containing one or more profile values. You can visualize the resulting structure as a tree of information, with each profile (along with its folders, sub-folders, and allowed values) being a branch of the tree. Each folder, sub-folder, or value is considered to be a node (or profilenode ) on the tree. The profile tree is a hierarchical structure containing profilenode objects and branches that link the different profilenode s with each other. Each branch has a top-level root node with sub-folder nodes (if any) and value nodes that represent the leaves of the tree.

The profiling API consists of ACL functions that walk a profile tree and traverse the profilenodes to determine the following information:

- • The different properties of each profilenode . (For example, to determine the type of node the profilenode is.

- • Relative location information about the profilenode such as the node's ancestors, children, and so on.

A profilenode can be one of the following types:

- • STANDARD_PROFILE, RADIO_PROFILE or FOLDERED_PROFILE — The type assigned to the top-level (root) profilenode .

- • PROFILE_FOLDER

- • ALLOWED_VALUE

The following elements in a profile configuration file are assigned a profilenode value as defined in the following table:

The following ACL functions support profiling and allow for site-specific customizations of Arbortext Editor profiling capabilities. Refer to the Arbortext Editor online help for detailed descriptions of each function.



---

# Profiling_DTD_Element_Reference

# Profiling DTD Element Reference

The location of the profiling document type definition is Arbortext-path \doctypes\profiling\profiling.dtd .



---

# Profiling_Overview

# Profiling Overview

Profiling is a means to provide specific content for a selected audience or for a specific application. Using profiling, authors can include all document variations in one file, and use profiles to control what elements appear in published versions of a document. By comparing the selected audience with each element's audience profile, Arbortext Editor strips out irrelevant content and assembles a custom publication.

Individual profiles specify that content can have one or more than one profile of a particular class. Classes may contain standard and unique profiles.

- • Standard individual profiles apply one or more profiles in a class to an element.

- • Unique individual profiles apply one and only one profile in a class to an element.

Two types of profile groups exist. Apply profile groups specify a collection of individual profiles defined as a named profile group an author can apply to an element in a single step. Set profile groups specify a collection of individual profiles an author can choose at publishing time in a single step.

Authors apply profile values to elements at editing time by setting certain element attributes to specific values as defined in profile configuration ( .pcf ) files. Individual document types reference the .pcf file containing the profiling definitions defined for the document type. Multiple document types can reference a single .pcf file.

You can configure colored shading to differentiate between profile, profile groups, or individual values. Refer to Using shading for profiled elements for further information.