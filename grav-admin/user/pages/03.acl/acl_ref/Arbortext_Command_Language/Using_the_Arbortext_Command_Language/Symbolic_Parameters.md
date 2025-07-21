

---

# $"*_Symbolic_Parameter

The $”* symbolic parameter indicates that all arguments to the alias should be concatenated and then quoted as a single string term to replace the parameter. The quoting follows the same rules as for $"n .



---

# $"n_Symbolic_Parameter

The $" n parameter refers to the n th positional parameter in the alias invocation, quoted as necessary to form a valid string term for expressions. This is most useful for providing an alias wrapper for a user-defined or built-in function. For example,

```
function xyz(s) { eval "xyz:", s output=>*;}
alias xyz { xyz($"1);}
```

allows the alias to be invoked as any of the following:

```
xyz test
xyz "test two"
xyz 'test 3'
```

Since aliases use the older convention of doubling string delimiters instead of the C-style backslash escape (that is, \" ), you must double the delimiter to get an embedded quote. For example,

```
xyz "embedded ""quote"
```

would expand to

```
xyz("embedded \"quote")
```



---

# $#_Symbolic_Parameter

The $# substitutes the number of arguments specified on the alias invocation. For example, if you entered the following alias:

```
alias argc {eval $#, "arguments";}
argc a b c
```

and executed the following command:

```
argc a b c
```

you would generate the following output:

```
3 arguments
```



---

# $*_Symbolic_Parameter

$* means substitute all the parameters supplied to the alias and $0 refers to the alias name. For example, the command:

```
alias screendump print editor screen $*
```

defines a command to do a screen dump (print the screen contents) and (because of the $* ) allows users to specify print options with the screendump command. For example, you could print the screen contents by typing:

```
screendump
```

The following command would print the screen contents, but it would add page numbers to the header and a date stamp to the footer:

```
screendump header=pageno footer=datemark
```

You can also use symbolic parameters to substitute part of an option. For example, to define a command that opens (for editing) a document in the directory /user/xxx , issue the command:

```
alias homedir edit /user/xxx/$1
```

If you were editing a document in a different directory and issued the command homedir todo , your document would be replaced with the document todo from directory /user/xxx .

To simplify things even more, you can shorten the name of your new command from homedir to hd by typing:

```
alias hd homedir $*
```

To edit todo , enter hd todo .

The $0 symbolic parameter will substitute the alias name within the alias invocation itself. For example:

```
alias testecho response("You just ran the $0 function.")
```

Running the testecho alias would generate the following response:

```
You just ran the testecho function.
```