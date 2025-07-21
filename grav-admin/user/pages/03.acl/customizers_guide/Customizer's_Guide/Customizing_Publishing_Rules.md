

---

# Adding_a_Publishing_Rule_Parameter

# Adding a Publishing Rule Parameter

Any publishing parameter can be set using the Advanced tab for the publishing rule. This example uses a publishing rule from the sample publishing rules file located at:

Arbortext-path \samples\publishingrules\sample.prcf

You will need to put it into a supported publishing rules directory accessible to your system, either your home directory or a custom\publishingrules directory, so that Arbortext Editor can find it automatically. If you are not sure of the location of your home directory, you can choose Help > Session and find Home directory in the list.

The following example shows how to add the rule.generateLog publishing rule parameter to the Advanced tab for a sample publishing rule.



---

# Adding_a_Publishing_Rule_Set_Parameter

# Adding a Publishing Rule Set Parameter

This example uses the publishing rule set from the sample publishing rules file located at:

Arbortext-path \samples\publishingrules\sample.prcf

You will need to put it into a supported publishing rules directory accessible to your system, either your home directory or a custom\publishingrules directory, so that Arbortext Editor can find it automatically. If you are not sure of the location of your home directory, you can choose Help > Session and find Home directory in the list.

The following example shows how to add the absoluteManifestPaths rule set parameter to the Advanced tab for the sample publishing rule set.



---

# Arbortext_Publishing_Engine_Document_Conversion

# Arbortext Publishing Engine Document Conversion

If you are using a client application and the f=convert function to send publishing requests to the Arbortext PE server , you can control the rule set parameters to be used during publishing on the Arbortext PE server . To use the rule set parameters as defined in the rule file, specify use-ruleset-parameters= yes on the HTTP f=convert request.

If you specify use-ruleset-parameters= yes , then Arbortext Publishing Engine will use the parameter values specified in the rule set definition in the rule file. If a parameter required for publishing processing is not specified in the rule file, the default value will be used.

If you specify use-ruleset-parameters= no (the default), then Arbortext Publishing Engine will ignore all rule set parameters in a rule file for f=convert requests, and it will use all default values for rule set parameters.

For more information on using f=convert , see the Arbortext Publishing Engine Document Conversion chapter of the Programmer's Guide to Arbortext Publishing Engine .



---

# Overriding_Rule_Parameters

# Overriding Rule Parameters

A rule set can override a rule parameter by specifying a parameter with the following syntax:

```
override:
file
:
rule
:
parameter
=
override-value
```

- • file (optional)

- • rule

- • parameter

- • override-value

A rule set can override the same parameter for every rule it contains by specifying a rule set parameter:

```
override:all:
parameter
=
override-value
```

- • parameter

- • override-value

For example, override:all could specify the debug parameter for every rule in the rule set by setting override-all:debug to the value 1 .



---

# Publishing_Rule_Output

# Publishing Rule Output

The output of a publishing rule consists of the requested published document, referenced content, and optional logs. The output can include the following:

- • The published output as specified by the publishing rule, which is one of the following, depending on the type of publishing operation:

- • an optional rule log that is placed in the same directory as the published output for the rule. It contains information about the publishing process, including the part of the Event Log that describes the execution of the publishing rule. The log name will be the same as the rule's output file name (including file extension) or directory name with an appended .rulelog.xml extension.



---

# Publishing_Rule_Output_Files

# Publishing Rule Output Files



---

# Publishing_Rule_Parameters

# Publishing Rule Parameters

Publishing rule parameters are stored in the rule’s definition in its rule file. The publishing rule parameters control the names of output files or directories and whether to generate log files for the publishing rule. Rule parameter values may contain several variables, defined as follows:

- • %n is the publishing rule name

- • %u is a discretionary sequential numbering applied by a rule set processor to ensure a directory name is unique. %u is an empty string when a rule runs alone.

- • %s is the period with file extension for a published output file (whether or not it’s accompanied by a directory of referenced content), as specified by the rule’s rule.outputSuffix parameter value. If the rule produces a directory, %s is the empty string.

When a rule executes, the publishing rule processor substitutes the appropriate value for these variables in each rule parameter. To specify a literal % in your parameter value, use %% .



---

# Publishing_Rule_Set_Parameters

# Publishing Rule Set Parameters

Rule set parameters are stored in the rule set's definition in its rule file. The publishing rule set parameters control how paths are handled, directory naming conventions for multiple rules, and generating logs and manifest files. Rule set parameter values may contain several variables, defined as follows:

- • %n is the publishing rule name

- • %u is a discretionary sequential numbering applied by a rule set processor to ensure a directory name is unique. %u is an empty string when a rule runs alone.

- • %s is the period with file extension for a published output file (whether or not it’s accompanied by a directory of referenced content), as specified by the rule’s rule.outputSuffix parameter value. If the rule produces a directory, %s is the empty string.

When a rule set is executed, the publishing rule processor substitutes the appropriate value for these variables in each rule set parameter. To specify a literal % in your parameter value, use %% .



---

# Rule_and_Rule_Set_Error_Handling

# Rule and Rule Set Error Handling

Error handling for rules and rule sets:

- • Any rule parameter covered in the preceding documentation that has an invalid value will be logged in the rule log as a Warning message. Publishing processing will use the parameter's default value instead.

- • Any rule parameter that is not recognized by the rule processor will be ignored, presuming the intent is to pass it on to the publishing framework.

- • Any rule set parameter covered in the preceding documentation that has an invalid value will be logged in the manifest as a Warning message. Publishing rule processing will use the default value instead.

- • Any rule set parameter not covered in the preceding documentation (not recognized by the rule processor) will be logged in the rule set manifest (if one is generated) as a Warning message.