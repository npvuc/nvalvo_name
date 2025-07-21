

---

# Example:_Mappings_Using_Variables

Some example mappings using variables are:

```
map control-s {execute cp $filename $filename.bak; \
save;}
```

This changes the CONTROL+S sequence so that it first makes a backup copy of the previous version of the file with a .bak extension and then saves the current version.

```
map f2 {readvar -prompt \
"Enter story name:" story; exec edit $story;}
```

This is much like the edit command without arguments, but allows a specialized prompt string.

## Related Topics

- • Predefined variables

- • Setting values for variables

- • Using variables

- • The execute command