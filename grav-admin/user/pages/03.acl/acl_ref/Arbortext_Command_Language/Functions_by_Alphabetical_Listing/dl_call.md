

---

# Returning_Input_Pointers_as_Results

An entry point called by dl_call should not return one of its parameters as its result if the parameter is, or could be, a pointer to a string. Consider the following ACL code:

```
result = dl_call(do_nothing, "a string")
result = unpack("*a*", result)
```

Assume that the do_nothing DLL entry point is the following:

```
char *do_nothing(char *pChar)
{
return pChar;
}
```

This code will fail if the library containing do_nothing expects 8–bit strings. In this case dl_call will make an 8–bit copy of the parameter a string , and release that memory as soon as the DLL entry point returns. When the call to unpack executes, the pointer returned by the DLL points to the released memory.

One possible way to write the entry point would be the following:

```
char *do_nothing(char *pChar)
{
return strdup(pChar);
}
```

The only caveat to this method is that the DLL will need to release the string memory at some point, perhaps when it is passed to another entry point.

## Related Topics

- • dl_find built-in function

- • pack built-in function

- • unpack built-in function