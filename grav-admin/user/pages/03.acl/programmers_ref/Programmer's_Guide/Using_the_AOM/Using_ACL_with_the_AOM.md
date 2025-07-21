

---

# Using_the_Acl_Interface

The AOM provides the Acl interface with methods to evaluate an ACL expression ( Acl.eval ) or execute an ACL command ( Acl.execute ). Both methods take a string object as an argument. This means that any AOM object passed to ACL must be converted to a string. Likewise, an ACL type returned by Acl.eval is converted to a string to pass to the AOM.

The expression passed to Acl.eval and the command passed to Acl.execute are evaluated in the ACL package context of the originating ACL function that invoked the AOM method, for example, javascript or js_source for JavaScript or a java_ type function for Java. For document type and document JavaScript and VBScript customization files automatically executed by Arbortext Editor or the Arbortext PE sub-process , this is the main package. If the string passed to Acl.eval or Acl.execute starts with a function call with a package prefix, then the package declaring the function is used.