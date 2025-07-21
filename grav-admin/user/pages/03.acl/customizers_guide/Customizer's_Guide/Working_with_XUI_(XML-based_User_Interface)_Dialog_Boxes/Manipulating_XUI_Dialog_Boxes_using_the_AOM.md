

---

# Customizing_the_Preferences_Dialog_Box

When Arbortext Editor loads the Preferences dialog box, it scans the dialog search path looking for a file called pref_exts.xml . If any are found, they will be processed in order. Arbortext Editor opens the file, parses it, and adds the new preferences categories to the XUI document which controls the Preferences panel. You can use the pref_exts.xml file to extend the Preferences dialog box for your custom application.

When Arbortext Editor launches, it finds any pref_exts.xml files and adds one or more new items to the list under Category as specified in the file. When the user chooses the new category, its relevant preference settings are displayed adjacent to the right as specified by the designed by the pref_exts.xml file.

The pref_exts.xml file must be placed in a location where Arbortext Editor can locate it at startup, such as the custom\dialogs directory or in a dialogs subdirectory of a custom application running under the application directory. Both of these locations are part of the set dialogspath by default.

A sample Preference Dialog Extension that you can use as a starter for your custom application is in the Arbortext-path \samples\xui\preferences directory. This example uses the custom directory structure and contains several files to be placed within its subdirectories. The pref_exts.xml file contains comments that describe the rules and guidelines for using this capability.