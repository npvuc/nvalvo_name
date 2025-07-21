

---

# Using_the_insert_tag_callback_with_tables

It is a common ACL practice to use a custom insert_tag callback function to perform custom tag insertion (above and beyond what Arbortext Editor would do) and then instruct Arbortext Editor to skip the insert that it would have performed by default. When working with tables, such inserts would need to be carefully crafted to adhere to the table model you are using. If the customized insert is not supported by the table model, Arbortext Editor prohibits the insert.

A better solution is to use the insert_tag_after callback when you are within a table.

## Related Topics

- • insert_tag command

- • insert_tag function

- • insert_tag_after callback