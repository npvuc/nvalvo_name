

---

# Making_Classes_Available_to_the_Embedded_JVM

The simplest way to make your classes available to Arbortext 's embedded JVM is to put them in the custom\classes directory. Any .class and .jar files in Arbortext-path \custom\classes are automatically added to the Arbortext Editor class path.

You can also use the ACL set javaclasspath command or the ACL append_javaclass_path function to set the list of directories where the embedded JVM can locate your Java classes. The default setting of set javaclasspath includes Arbortext-path \custom\classes .

The javaclasspath option is used only for locating non- Arbortext supplied classes. In addition to aom.jar , several other .jar files are distributed in Arbortext-path \lib\classes and are automatically included as part of the embedded JVM's class path.

Once the JVM has started, changes to the javaclasspath option or to the directories it specifies will not take effect until you exit and start a new session of Arbortext Editor or stop and restart the servlet container for the Arbortext Publishing Engine .



---

# Making_the_AOM_Available_for_Other_Java_Programs

If you are compiling a Java program that uses the AOM, put Arbortext-path \lib\classes\aom.jar in the compiler's -classpath argument.

## Related topic

- • Accessing the Java Console