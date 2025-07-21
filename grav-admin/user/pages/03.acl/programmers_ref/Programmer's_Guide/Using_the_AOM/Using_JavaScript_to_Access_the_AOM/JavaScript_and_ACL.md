

---

# Passing_Arrays_Between_JavaScript_and_ACL

There are two ways to pass arrays between JavaScript and ACL, both involving the conversion of arrays to strings. The first method uses the JavaScript Array.join method to convert the JavaScript array to a string that is passed to the ACL split function.

For example, the JavaScript code

```
var jsArr = [1, 2, 3];
Acl.eval("split('" + jsArr.join() + "', aclArr, ',')");
```

converts the JavaScript array jsArr to the ACL array aclArr .

The second method uses a loop to pass the array, element by element. The Acl.eval call in the example above can be rewritten as:

```
for (var i = 0; i < jsArr.length; i++) {
var ai = i + 1;
Acl.eval("aclArr[" + ai + "] = '" + jsArr[i] + "'");
}
```

This method is slower, but isn't subject to the ACL string token limit of 4096 characters.

Similarly, there are two ways to retrieve an ACL array from JavaScript. The first method uses the ACL join function to concatenate the ACL array into a string that initializes a JavaScript array. For example, you can use the following ACL code to pass the ACL array created above to JavaScript:

```
javascript("var jsArr = [" . join(aclArr) . "]");
```

This method is not limited by the ACL string token limit.

You can also use a loop to retrieve the array, element by element, as shown in the following JavaScript example:

```
var count = parseInt(Acl.eval("count(aclArr)"));
var lowBound = parseInt(Acl.eval("low_bound(aclArr)"));
var jsArr = new Array(count);
for (var i = 0; i < count; i++) {
var ai = lowBound + i;
jsArr[i] = Acl.eval("aclArr[" + ai + "]");
}
```

This method translates the arbitrary array index bounds in an ACL array to the zero-based array index in JavaScript. It also uses the parseInt method to convert the Java string returned by Acl.eval into a JavaScript number.

Associative Arrays

The previous examples concern normal numeric indexed arrays. You can use equivalent techniques to pass associative arrays using for/in loops instead of the for loops as above. The following JavaScript example passes an associative array to ACL:

```
var jsAssoc = {one: 1, two: 2, three: 3};
for (var i in jsAssoc) {
Acl.eval("aclAssoc['" + i + "']='" + jsAssoc[i] + "'");
}
```

You can pass an ACL associative array to JavaScript using the ACL join function or an ACL for/in loop similar to the JavaScript example. The following ACL example shows the join technique to declare a JavaScript array using object literal syntax:

```
javascript("var jsAssoc={" . join(aclAssoc,',',1) . "}")
```