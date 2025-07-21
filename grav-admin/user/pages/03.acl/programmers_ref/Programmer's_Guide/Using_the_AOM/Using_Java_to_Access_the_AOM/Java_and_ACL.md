

---

# Passing_Arrays_Between_Java_and_ACL

Some ACL functions accept or return array data. Java programs that call these ACL functions will require additional coding to transfer the array data across the interface.

For example, if a Java program needs a list of the available tag names in a document, it can use the Acl.eval Java method to call the tag_names ACL function. This ACL function returns an integer for the total number of available tag names to the Java method, but it stores the array of tag names in an ACL array. To retrieve this data and make it available to the Java program, further calls to the Acl.eval method would be necessary. Consider the sample code that follows:

```
// This method fills a Java String array with the data
// from an ACL array
private String[] convertAclArray(String aclArrayName, \
int aclArraySize) {
String[] result = new String[aclArraySize];
for (int i = 0; i < aclArraySize; i++) {
// The first element of a Java array has index 0 but the first
// element of an ACL array has index 1
result[i] = Acl.eval(aclArrayName + "[" + String.valueOf(i+1)
+ "]");
}
return result;
}
.
.
.
try {
total = Acl.eval("tag_names($arr)");
} catch (AclException e) {
// Maybe the $arr has been defined and it is not an array
g.drawString(e.getMessage() , 20, 60);
return;
}
String[] names = convertAclArray("$arr", Integer.parseInt(total));
.
.
.
```

Similarly, data in Java arrays need to be transferred to an ACL array before that data can be used by an ACL function.

The java_array_from_acl and java_array_to_acl ACL functions can also be used to convert certain types of arrays between ACL and Java. See the online help for details.