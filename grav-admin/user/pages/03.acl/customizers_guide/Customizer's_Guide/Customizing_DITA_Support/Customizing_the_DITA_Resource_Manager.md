

---

# Customing_the_Default_Look_in_Location

You can customize the default location for the Resource Manager Look in option using preferences. Note that the setting of the Synchronize Location Across Tabs menu choice and associated set ditasynctab command also affects the Look in location. If tab synchronization is turned on, then any location you set at start up only applies until the user navigates to a different location in the Resource Manager browser.

You can use the following preferences to set the Look in location for specific tabs:

- • com.arbortext.dita.lastAccessDirForLinkXrefPane — Link/Xref tab

- • com.arbortext.dita.lastAccessDirForImagePane — Image tab

- • com.arbortext.dita.lastAccessDirForTopicContentReferencePane — Conref tab on the Resource Manager for DITA topics

- • com.arbortext.dita.lastAccessDirForMapContentReferencePane — Insert Conref dialog box for DITA maps.

- • com.arbortext.dita.lastAccessDirForKeyDefPane — Key Definition tab

- • com.arbortext.dita.lastAccessDirForTopicsPane — Topic tab

- • com.arbortext.dita.lastAccessDirForXincludePane — Inclusion dialog box

For example, you could use the following ACL code to set the default Look in location for the Link/Xref tab to C:\demo :

```
set_user_property(\
"com.arbortext.dita.lastAccessDirForLinkXrefPane", \
"C:\\demo");
```



---

# Customizing_the_displayed_Resource_Manager_tabs

You can customize the tabs that appear in the docked version of the Resource Manager using the following persistent user preference:

com.arbortext.dita.rm.( doctype ).tabs=( tab1 ),( tab2 ),( tab3 ),...

For the doctype token, you can specify either a specific document type base name (for example, ditabase or bookmap ), or you can use map to specify all DITA map specializations and topic to specify all topic specializations.

For the tab token, you can specify one of the following values:

If no preferences are specified, the following default values are used:

For example, you could use the following ACL code to remove the Content Reference tab from the docked Resource Manager dialog box for DITA topics and replace it with the Inclusion tab:

```
set_user_property(\
'com.arbortext.dita.rm.topic.tabs', \
'link_xref_tab,image_tab,xinclude_tab');
```

You could use the following ACL code to remove the Key Definition tab and add the Image tab for DITA BookMaps:

```
set_user_property(\
'com.arbortext.dita.rm.bookmap.tabs', \
'topic_tab,new_topic_tab,keydef_tab,image_tab');
```



---

# Customizing_the_Tags_Displayed_in_the_Insert_Option

You can customize the tags displayed in the Resource Manager Insert option using the following persistent user preference:

com.arbortext.dita.rm.( doctype ).[( tab ).]hiddenTags

For the optional doctype token, you can specify a specific document type base name (for example, ditabase or bookmap ). If omitted, the preference applies for all document types that do not have an explicit preference value set.

For the optional tab token, you can specify the same values as those used to set the default tabs. If omitted, the preference applies for all tabs.

The value of the preference is a list of tag names, separated by commas. As the cursor moves around the document, the Resource Manager scans this list until it finds the tags that are legal at the current location and displays only those tags in the Insert option.

For example, you could use the following ACL code to just display topicset or topicsetref tags in Insert option for DITA BookMaps:

```
set_user_property(\
"com.arbortext.dita.rm.bookmap.hiddenTags", \
"topicset,topicsetref")
```

## Related topics

- • DITA authoring overview

- • Resource Manager overview

- • Preferences file

- • set_user_property function

- • dita_doc_show_rm_tab function

- • dita_show_rm_tab function

- • dita_reset_rm_state function



---

# Customizing_the_Tags_Selected_in_the_Insert_Option

You can customize the tags selected in the Resource Manager Insert option using the following persistent user preference:

com.arbortext.dita.rm.( doctype ).[( tab ).]preferredTags

For the optional doctype token, you can specify a specific document type base name (for example, ditabase or bookmap ). If omitted, the preference applies for all document types that do not have an explicit preference value set.

For the optional tab token, you can specify the same values as those used to set the default tabs. If omitted, the preference applies for all tabs.

The value of the preference is a list of tag names, separated by commas. As the cursor moves around the document, the Resource Manager scans this list until it finds a tag that is legal at the current location and make that the default selection in the Insert option.

For example, you could use the following ACL code to automatically select the chapter or topicref tags in the Topic tab Insert option for DITA BookMaps:

```
set_user_property(\
"com.arbortext.dita.rm.bookmap.topic_tab.preferredTags", \
"chapter,topicref")
```

The part tag still appears in the option, but is never selected automatically.



---

# Customizing_the_Type_of_Files_to_Display_in_the_Show_and_Type_Options

You can customize the type of files displayed in the Resource Manager Show and Type options using the following persistent user preference:

com.arbortext.dita.rm.[( doctype ).]( tab ).( filter )

For the optional doctype token, you can specify a specific document type base name (for example, ditabase or bookmap ). If omitted, the preference applies for all document types that do not have an explicit preference value set.

For the tab token, you can specify the same values as those used to set the default tabs.

For the filter token, you specify the option you want to customize. You can use either showFilter or typeFilter .

The value of the preference is a string identifying the file filter. In general, the following naming rules are used for filters:

- • When the filter is for elements based on a class, the value is that base class — for example, topic/topic for All Topics .

- • When the filter is the same as a file extension or tag name, the name is the named thing in lower case — for example, pdf , html , fig , or section .

- • Otherwise, the name is the same as the English label for the filter in lower case with spaces replaced by underscore ( _ ) characters.

You can use the following values for Show option filters:

You can use the following values for Type option filters:

For example, you could use the following ACL code to set the default Type option value to PDF for all tabs and document types:

```
set_user_property(\
"com.arbortext.dita.rm.typeFilter", \
"pdf");
```

You could use the following ACL code to set the default Type option value to Topic or Map on the Topic tab for DITA BookMaps:

```
set_user_property(\
"com.arbortext.dita.rm.bookmap.topic_tab.typeFilter", \
"topic_or_map")
```

You could use the following ACL code to set the default Show option value to All topics on the Link/Xref tab for all Learning and Training topics:

```
set_user_property(\
"com.arbortext.dita.rm.learningDitabase.link_xref_tab.showFilter", \
"topic/topic")
```