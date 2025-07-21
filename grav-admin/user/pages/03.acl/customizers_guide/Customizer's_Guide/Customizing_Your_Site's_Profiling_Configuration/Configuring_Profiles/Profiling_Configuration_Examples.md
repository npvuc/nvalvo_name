

---

# Nesting_Profiles

Profile classes can contain folders containing more folders and profiles. Using such a structure provides a categorization of related profiles. In this example, several Windows platforms are categorized in a parent Windows folder.

Example of nested profiles in the Apply Profiles dialog box.

This profiling configuration is created with the following markup:

```
<Profile attribute="os" alias="Operating System">
<ProfileFolder name="Windows">
<Allowed value="Windows XP"/>
<Allowed value="Windows 2000"/>
<Allowed value="Windows Server 2003"/>
</ProfileFolder>
<Allowed value="Unix"/>
</Profile>
```



---

# Restricting_Profiles_to_or_from_Specific_Elements

By restricting profiling to only certain elements, you can ensure that information is always included or included in only certain circumstances. In this example, if the toc element has a role attribute set to the value required , the element cannot be profiled by the users level of expertise. This ensures that the Table of Contents is always included when the document is published. If the user attempts to profile a toc element with its role attribute set to the value required , the profiles will be unavailable:

Example of restricted profile values.

This profiling configuration is created with the following markup:

```
<Profile attribute="userlevel" alias="User Level">
<NotProfileElement element="toc">
<AttributeTest name="role" value="required"/>
</NotProfileElement>
<RadioChoice>
<Allowed value="Novice"/>
<Allowed value="Typical"/>
<Allowed value="Expert"/>
</RadioChoice>
</Profile>
```



---

# Using_Logical_Expressions_when_Configuring_Profiles

Set profile groups define a collection of individual profiles an author can choose at publishing time in a single step. When creating set profile groups, you can use logical expressions to specify publishing that is dependant on profile value relationships. When using logical expressions, ensure that the names assigned to the SetProfileGroup elements clearly communicate to the user the profiles that will be published.

In this example, different user levels are grouped. Elements profiled for all of the user levels represented by the selected group will be published.

Example of set profile groups.

This profiling configuration is created with the following markup:

```
<SetProfileGroup name="Novice and Typical User Levels">
<LogicalExpression>
<LogicalGroup operator="OR">
<ProfileRef alias="User Level" value="Novice"/>
<ProfileRef alias="User Level" value="Typical"/>
</LogicalGroup>
</LogicalExpression>
</SetProfileGroup>
<SetProfileGroup name="Expert and Typical User Levels">
<LogicalExpression>
<LogicalGroup operator="OR">
<ProfileRef alias="User Level" value="Expert"/>
<ProfileRef alias="User Level" value="Typical"/>
</LogicalGroup>
</LogicalExpression>
</SetProfileGroup>
<SetProfileGroup name="Typical Windows Customer">
<LogicalExpression>
<LogicalGroup operator="AND">
<ProfileRef alias="User Level" value="Typical"/>
<LogicalGroup operator="OR">
<ProfileRef alias="Operating System" value="Windows XP"/>
<ProfileRef alias="Operating System" value="Windows 2000"/>
<ProfileRef alias="Operating System" value="Windows Server 2003"/>
</LogicalGroup>
<ProfileRef alias="Security Level" value="Customer"/>
</LogicalGroup>
</LogicalExpression>
</SetProfileGroup>
```