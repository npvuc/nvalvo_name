

---

# Accessing_Query_String_Parameters

While the editbeforehook functions are being called, the query strings are available through the following function and methods:

- • ACL: get_custom_property()

- • AOM: Application.getCustomProperties().getString()

After the hook functions have all been called, the query string values are no longer available. To access a query string parameter, you prefix the parameter name with the following value before calling get_custom_property() or Application.getCustomProperties().getString() :

```
com.ptc.arbortext.launcher.temp.
```

For example, to access the workspace parameter in the following example link:

```
arbortext-editor:x-wc%3A%2F%2Ffile%3D1234.xml?workspace=ws1&hosturl=http%3A%2F%2Fpjl%2FWindchill
```

You could use the following ACL code:

```
local value = get_custom_property('com.ptc.arbortext.launcher.temp.workspace');
```

You could also use the following AOM code:

```
String value = Application.getCustomProperties().getString("com.ptc.arbortext.launcher.temp.workspace");
```

If there is no such query parameter, then an empty string is returned for ACL and a null is returned for AOM.

## Related topics

- • Registering and unregistering Arbortext Editor as a COM server

- • set webzonepolicy