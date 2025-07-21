

---

# Publishing_Rule_Set_Output

The output of a publishing rule set is a directory containing:

- • a set of subdirectories, one for each publishing rule. Each subdirectory contains the publishing rule output according to type of operation, as described in the previous section.

- • a manifest file can be placed in the rule sets’s top level output directory. The rule set manifest.xml contains identifying information about the rule set itself, then lists each publishing rule in the rule set. For each rule, the manifest will list the rule's name, location, type and other static information. It will also list the path to the rule's output directory or output file, whether output for the rule succeeded, and how many errors and warnings were written to the Event Log (which is included in the rule log) while the rule was executing.