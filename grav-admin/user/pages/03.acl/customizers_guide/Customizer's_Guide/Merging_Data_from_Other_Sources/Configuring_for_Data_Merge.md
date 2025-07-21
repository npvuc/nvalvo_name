

---

# The_.dcf_File

To merge data, the document type's .dcf file must contain a <DataMerge> element specifying the base name of the file containing the query definitions and whether they are enabled. In the following example, the query definitions are stored in the file example1.dmf and are made available to authors:

```
<DataMerge>
<DataSource enabled="yes" name="example1"/>
</DataMerge>
```



---

# The_Data_Merge_Configuration_File_(The_.dmf_File)

The .dmf file defines queries and their components. The file is an XML file based on the supplied datamerge.dtd document type. Queries must be defined in the .dmf file before authors can add merged data to their documents. Arbortext Editor first searches the current document type directory for a .dmf file, then searches Arbortext-path \custom\datamerge .

The following sample example1.dmf file provides a sample content query that retrieves employee information from a database and returns the result as a table. The query takes three parameters: username and password for connecting to the database, and department for the specific department employee information. In the example code, the referenced resources in the <Resource> element are provided as part of Arbortext Editor .

```
<DataMerge>
<Resource>
&msAccessSource;
&tableModelTransformer;
</Resource>
<!-- **** QUERY: "Select Employees" **** -->
<Query name = "Employee_Query" queryType="table">
<Label>Select Employees</Label>
<Interface>
<Documentation>
Interface section contains query parameters to be shown in
the insert query dialog box. This query defines one parameter
which is shown as a combo box in the query dialog box.
</Documentation>
<QueryField name="p01" displayType="combo">
<Label>department</Label>
<ListItem>Engineering</ListItem>
<ListItem>Sales and Marketing</ListItem>
<ListItem>Services</ListItem>
</QueryField>
</Interface>
<SourceRef name="QuerySource" nameref="MS_Access_Source">
<Documentation>
This is a source filter that retrieve data from an MS Access
database using jdbc-odbc bridge. The SQL statement contains a
parameter "department".
</Documentation>
<ParameterRef name = "p_statement" nameref="sqlStatement" >
<Value>select name, phone, email from employees where department = ?</Value>
</ParameterRef>
<!-- SQL Parameters -->
<ParameterGroupRef name = "queryParameters" nameref="sqlParameters" >
<Documentation>
This parameter defines the values to be passed into SQL statement.
</Documentation>
<ParameterRef name = "department" datatype="string" >
<Documentation>
The value of this parameter refers to the value specified in insert query dialog box
(department).
</Documentation>
<QueryFieldRef nameref="p01"/>
</ParameterRef>
</ParameterGroupRef>
<!-- SQL Parameters -->
<ParameterGroupRef name = "p_connect" nameref="connectionProperties" >
<Documentation>
Connection string for connecting to an Access database file. An DSN need
to be setup in Windows Control Panel ODBC Administration. In this example,
the name for the DSN is "employees".
</Documentation>
<ParameterRef name = "p_url" nameref = "url">
<Value>jdbc:odbc:employees</Value>
</ParameterRef>
</ParameterGroupRef>
</SourceRef>
<TransformerRef name="QueryTransformer" nameref="TableModelTransformer">
<Documentation>
Table model transformer transforms the query result into an Arbortext table model.
</Documentation>
<ParameterRef nameref="tableModel">
<Documentation>
The table model to use.
</Documentation>
<Value>OASIS Exchange</Value>
</ParameterRef>
<ParameterRef nameref="wrapperTag">
<Documentation>
The wrapper tag for the table model.
</Documentation>
<Value>table</Value>
</ParameterRef>
</TransformerRef>
</Query>
</DataMerge>
```

After inserting the query, the following markup is added to the document at the insertion point:

```
<atidm:query xmlns:atidm="http://www.arbortext.com/namespace/DataMerge"
queryKey="example1:Employee_Query"
queryName="Select Employees(department)"
queryType="table"
timestamp="1079992813593"
updateOnOpen="yes"
updateOnCompose="yes"
updateManually="yes"
p01="Engineering">
<table> .... </table>
```