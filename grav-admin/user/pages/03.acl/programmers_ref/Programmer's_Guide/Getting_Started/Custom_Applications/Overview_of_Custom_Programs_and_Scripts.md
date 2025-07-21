

---

# The_Application_Directory_Structure

The Arbortext-path \application subdirectory can contain custom applications as well as application software distributed by Arbortext . The application directory must have one or more uniquely named subdirectories, each containing a specific configuration file, application.xml , that conforms to a specific format. At startup, the application directory is searched for subdirectories and the presence of a valid application.xml file. In the uniquely named subdirectory, all subdirectories of the custom directory are supported. The custom application in a application then uses these subdirectories in the same way as the custom directory structure. You can also have additional subdirectories needed to support the implementation of this type of custom application. Implementing your custom application using this approach takes advantage of the startup sequence, supports delivering a completely self-contained custom application, and offers the option of setting the conditions for whether the application should be loaded. The application directory is also explained in this chapter.



---

# The_Custom_Directory_Structure

The Arbortext-path \custom directory has a subdirectory structure designed to hold your custom programs and scripts and make them automatically available during the session. At startup, these subdirectories are searched for Java, JavaScript, JScript, VBScript, ACL, and composer configuration files. You can also provide custom document types, entities, fonts, graphics, and native shared libraries and DLLs. The supported file types are automatically accessed if they reside in the appropriate subdirectory. Implementing your custom files using this approach takes advantage of the startup sequence to automatically locate your custom files. The Arbortext-path \custom directory and its subdirectories are explained in detail in this chapter.