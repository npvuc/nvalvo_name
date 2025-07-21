

---

# rootallchildall

The rootallchildall setting causes all entity declarations to be written in the root document's subset, and in the subset of all its children. This produces valid SGML in that the root document contains declarations for all entities of the document tree, and additionally writes all entity declarations in a special comment subset at the front of file entities. That can be useful if the file entities are edited standalone (that is, edited directly instead of being edited by being opened from the parent document) and if access to all the entities declared in the entire document tree is necessary during this standalone editing. With this setting, if an entity declaration is present in one file entity's subset, every file of that document tree that is saved will include the entity declaration.

The main drawback of this method is the larger size of fragments both when stored, and in memory. Another drawback is slower performance when performing operations such as deleting entity declarations.

While this setting most closely approximates pre-8.0 behavior, these drawbacks generally make it undesirable for sites where large documents are published of many file entities or objects.



---

# rootallchildnone

The rootallchildnone setting, causes all entity declarations to be written in the root document's subset only, and no entity declarations to be written in file entity subsets. This produces valid SGML in that the root document contains declarations for all entities of the document tree. This is a good method when it is not necessary to edit entities standalone.

It may also be desirable if it is acceptable that all entity references are unrecognized when editing file entities standalone. The entity references will be preserved, but they will be treated as character entities, which may or may not invalidate the document structure, causing context errors. If you know that in your application it will not cause errors, then it might be a useful setting for you.



---

# rootallchildref

The rootallchildref setting, causes all entity declarations to be written in the root document's subset, and declarations for entities referenced immediately with a child to be written in the subset of each child. This produces valid SGML in that the root document contains declarations for all entities of the document tree, and additionally writes all entity declarations currently referenced by a file entity in a special comment subset at the front of the file entity. That can be useful if the file entities are edited standalone (that is, edited directly instead of being edited by being opened from the parent document).

This setting balances the need for standalone entity editing with the need for smaller entities. If it is not necessary to be able to access all entities while editing standalone, the smaller entity size, both when stored and in memory, makes this setting preferable to rootallchildall .

This option is the default.



---

# rootrefchildref

The rootrefchildref setting causes all files (objects) of the document tree to be written with only the declarations referenced immediately within that file. If an entity is referenced only from a file entity, not from the root document, this option produces invalid SGML in that the root document will not have declarations for all the entities referenced in the document tree. Such documents will produce SGML parsing errors if read with the check completeness ( -cc ) option.

## Related Topics

- • save_all_docs alias



---

# roottreerefchildnone

The roottreerefchildnone setting, causes entity declarations referenced anywhere in the document tree (that is, in the root doc or its children) to be written in the root document's subset, and no entity declarations to be written in childrens' subsets. This produces valid SGML in that the root document contains declarations for all entities referenced in the document tree.

This option has all the benefits/considerations of rootallchildnone and additionally purges the root document of declarations to unreferenced entities. It takes longer to save documents with this setting, so its primary value may be to periodically “clean” your documents.



---

# roottreerefchildref

The roottreerefchildref setting, causes entity declarations referenced anywhere in the document tree (that is, in the root document or its children) to be written in the root document's subset, and declarations for entities referenced immediately with a child to be written in the subset of each child. This produces valid SGML in that the root document contains declarations for all entities referenced in the document tree, and additionally writes all entity declarations currently referenced by a file entity in a special comment subset at the front of the file entity.

This option has all the benefits of rootallchildref and additionally purges the root document of declarations to unreferenced entities. It takes longer to save documents with this setting, so its primary value may be to periodically “clean” your documents.