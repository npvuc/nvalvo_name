

---

# Processing_Query_Strings

The arbortext-editor protocol enable you to add an optional query string to the URI. Following is an example of a URI with the query string:

```
arbortext-editor:x-wc%3A%2F%2Ffile%3D1234.xml?workspace=ws1&hosturl=http%3A%2F%2Fpjl%2FWindchill
```

In this example, there are two query parameters: workspace and hosturl . Their decoded values are ws1 and http://pjl/Windchill .

These query string parameters enable the link to specify potentially useful metadata about the link. This metadata can be accessed inside of an ACL editbeforehook hook function. When one of these links are selected in a web browser, all of the functions in the editbeforehook are called before the document is actually opened. This gives the hook function a chance to do any special processing before the document opens.

For example, following is an HTML link containing some query strings that opens an Arbortext Editor session:

```
<a href="arbortext-editor:http%3A%2F%2Fserver%2Fpath%2Ffile.xml?hint1=food&hint2=M%26Ms">
click here
</a>
```

This links opens the http://server/path/file.xml document and includes the hints food and M&Ms as query strings. Assume the following hook code is sourced:

```
package metadata;
function my_edit_before_hook(path)
{
local hint1 = get_custom_property('com.ptc.arbortext.launcher.temp.hint1');
local hint2 = get_custom_property('com.ptc.arbortext.launcher.temp.hint2');
response("Path=$path\n\nhint1=$hint1\n\nhint2=$hint2");
# returning -1 will cancel the edit
}
add_hook('editbeforehook', package_name().'::my_edit_before_hook');
```

In this case, when the link is selected in the web browser, the response dialog box displays both the decoded http path to the file and the hint1 and hint2 metadata that was in the original HTML link.



---

# The_arbortext-editor_Protocol

You use the arbortext-editor protocol to launch a Arbortext Editor session for a document from a link on a web page. In this case, the usual Arbortext Editor window is used to open the document, so Arbortext Editor must be installed or otherwise available on the local system. In general, when a web browser processes a link with an unknown protocol the browser checks the local system to see whether there is an application registered to handle the protocol. When Arbortext Editor is registered as a COM server on a Microsoft Windows system, part of that process associates Arbortext Editor with the arbortext-editor protocol.

For security reasons, most web browsers usually prompt the user before initially launching the associated program for a given protocol URI. Since Arbortext Editor is registered as the associated program for the arbortext-editor protocol, a browser generally displays a dialog box warning the user that this link will launch an application on their system and asking for confirmation before proceeding. Such dialog boxes generally have an option to not show the warning again for this protocol. If Arbortext Editor is not installed on the system, or is not registered for some reason, most browsers will display an error message saying that the protocol is not associated with an installed program.

Following is an example of an HTML link that would open Arbortext Editor for a document named sample.xml :

```
<a href="arbortext-editor:http%3A%2F%2Fdocserver%2Fwebdav%2Fsample.xml">
Sample document
</a>
```

Note that if the link appears as an attribute value in HTML markup, then it is subject to the normal encoding rules of those attribute values. In particular, if the link contains the & character (such as if there is a query string with more than one parameter), then this must be encoded as &amp; . For example, the following link:

```
arbortext-editor:http%3A%2F%2Fdocserver%2Fwebdav%2Fsample.xml?color=blue&priority=high
```

should appear inside of an HTML link as follows:

```
<a href="arbortext-editor:http%3A%2F%2Fdocserver%2Fwebdav%2Fsample.xml?color=blue&amp;priority=high">
Sample document
</a>
```



---

# The_Protocol_Syntax

Following is the syntax for the arbortext-editor protocol presented in the RFC format defined in RFC 4395 by the Internet Assigned Numbers Authority (IANA) :

```
arbortexturi = scheme ":" resource [ "?" query] [ "#" anchor]
scheme = "arbortext-editor" | "arbortext-editor-embed"
query = query-pair *["&" query-pair]
query-pair = key "=" value
resource = utf8 url encoded resource
key = utf8 url encoded query component
value = utf8 url encoded query component
anchor = utf8 url encoded resource
```

In the syntax, resource must be the encoded full path to a document that can be opened with Arbortext Editor .

utf8 url encoded resource refers to the standard rules for encoding a resource referenced from a URI. The following rules apply in this case:

- • The alphanumeric characters "a" through "z", "A" through "Z" and "0" through "9" remain the same.

- • The special characters " . ", " - ", " * " and " _ " remain the same.

- • The space character is converted into "%20".

- • All other characters are first converted into one or more bytes using UTF-8, and then each byte is represented by the character string "% xy ", where xy is the two-digit hexadecimal representation of the byte.

For example, the string The string ü@foo-bar would get converted to The%20string%20%C3%BC%40foo-bar , because in UTF-8 the character ü is encoded as two bytes C3 (hex) and BC (hex), and the character @ is encoded as %40 and spaces are encoded as %20 .

utf8 url encoded query component refers to the optional query string, which must be encoded according to the application/x-www-form-urlencoded mime type (defined in the W3C HTML 4.01 Specification ). The basic encoding rules are the same in this case, but space characters are represented by a plus sign ( + ).

Following are some examples of legal uses of the protocol:



---

# The_Security_Zone_Policy

By default, whether a document is opened by an arbortext-editor protocol link is determined by the Microsoft URL security zone policy. When a link using the protocol is invoked from a web browser, Arbortext Editor first determines the zone of the encoded resource path. The link is then allowed or denied according to this policy:

- • Local Machine zone — allow

- • Local Intranet zone — allow

- • CMS zone — allow

- • Trusted Sites zone — allow

- • Internet zone — deny

- • Restricted Sites zone — deny

If the link is denied, then a message is displayed saying that the request has been denied for security purposes. The use of URL security zones is controlled by the webzonepolicy preference.