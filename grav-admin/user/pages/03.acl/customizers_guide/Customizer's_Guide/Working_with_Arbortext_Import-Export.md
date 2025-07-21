

---

# Configuring_for_Exporting

# Configuring for Exporting

Arbortext Import/Export uses Arbortext Styler to export XML documents to RTF. To install and configure Arbortext Import/Export for Export stylesheet development and deployment, perform the following steps:

Arbortext Import/Export exports documents as RTF version 1.7 documents. Visit www.microsoft.com for a copy of the Rich Text Format (RTF) Specification Version 1.7.



---

# Configuring_for_Importing

# Configuring for Importing

Configure client workstations for importing files in the following manners as appropriate.



---

# Troubleshooting

# Troubleshooting

If you receive the following error message:

```
Failed to load conversion bridge DLL
```

.NET Framework v2.0.50727 or v3.0 may not be installed. Download an updated .NET Framework from www.microsoft.com .

If you receive the same error message with return code 30 and a path starting with \\ , this indicates that the executable is on a network drive. This configuration is not supported due to .Net library restrictions.



---

# Using_Arbortext_Import-Export_in_Batch_Mode

# Using Arbortext Import/Export in Batch Mode

You can use Arbortext Import/Export to import and export documents in an unattended, or batch, fashion. From the Arbortext Editor command line or an ACL script, use the following ACL functions when importing and exporting documents in batch mode.

document_export ([ inFile [, outFile [, styleSheet [, logFile [, nFlags ]]]]])