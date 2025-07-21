

---

# Hiding_Parameter_Values

When inserting a query, query parameters and their values are embedded in the document as part of query result. These parameters are not visible when viewing the document in Arbortext Editor , but they can be viewed when directly viewing the document’s XML source. You may wish to hide these parameter values when they represent sensitive information such as a user name or password.

To hide parameter values when queries are inserted in documents, set the parameter’s <QueryField> hidden attribute value to yes . Doing so will cause the value of the parameter to be replaced by asterisks when inserted in the document in the query result. For example:

```
<QueryField name="p01" hidden="yes" displayType="combo">
<Label>department</Label>
<ListItem>Engineering</ListItem>
<ListItem>Sales and Marketing</ListItem>
<ListItem>Services</ListItem>
</QueryField>
```