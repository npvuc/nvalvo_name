

---

# Allowed_Element

## Synopsis

Mixed content model:

```
Allowed
Empty
```

Attributes:

```
value CDATA #REQUIRED
```

## Description

The <Allowed> element specifies the only allowed value for a profile.

The element has no child elements.

The <Allowed> element has the following attribute:

- • value = CDATA



---

# ApplyProfileGroup_Element

## Synopsis

Mixed content model:

```
ApplyProfileGroup
(ProfileRef)+
```

Attributes:

```
name CDATA #REQUIRED
```

## Description

The <ApplyProfileGroup> element specifies a named apply profile group.

The element can have the following child element:

<ProfileRef>

The <ApplyProfileGroup> element has the following attribute:

- • name = CDATA



---

# AttributeTest_Element

## Synopsis

Mixed content model:

```
AttributeTest
EMPTY
```

Attributes:

```
name CDATA #REQUIRED
value CDATA #IMPLIED
```

## Description

The <AttributeTest> element specifies whether an attribute test must be performed.

The element has no child elements.

The <AttributeTest> element has the following attributes:

- • name = CDATA

- • value = CDATA



---

# LogicalExpression_Element

## Synopsis

Mixed content model:

```
LogicalExpression
(LogicalGroup | LogicalNOT)
```

Attributes:

```
None
```

## Description

The <LogicalExpression> element specifies a logical expression to use in a set profile group.

The element can have the following child elements:

<LogicalGroup> , <LogicalNOT>

The <LogicalExpression> element has no attributes.



---

# LogicalGroup_Element

## Synopsis

Mixed content model:

```
LogicalGroup
((ProfileRef | LogicalGroup | LogicalNOT),
(ProfileRef | LogicalGroup | LogicalNOT)+)
```

Attributes:

```
operator (AND | OR | XOR | EQUAL) #REQUIRED
```

## Description

The <SetProfileGroup> element defines a logical expression group

The element can have the following child elements:

<ProfileRef> , <LogicalGroup> , <LogicalNOT>

The <LogicalGroup> element has the following attribute:

- • operator = AND | OR | XOR | EQUAL



---

# LogicalNOT_Element

## Synopsis

Mixed content model:

```
LogicalNOT
(ProfileRef| LogicalGroup)
```

Attributes:

```
None
```

## Description

The <LogicalNOT> element specifies logical negation of an expression. That is, for value A, the expression is true if A is false and the expression false if A is true.

The element can have the following child elements:

<ProfileRef> , <LogicalGroup>

The <LogicalNOT> element has no attributes.



---

# NotProfileElement_Element

## Synopsis

Mixed content model:

```
NotProfileElement
(AttributeTest*)
```

Attributes:

```
element NMTOKEN #REQUIRED
```

## Description

The <NotProfileElement> element defines the elements to be restricted from having a particular profile.

The element can have the following child element:

<AttributeTest>

The <NotProfileElement> element has the following attribute:

- • element = NMTOKEN



---

# Profile_Element

## Synopsis

Mixed content model:

```
Profile
((ProfileElement* | NotProfileElement*),
((ProfileFolder | Allowed)+ | RadioChoice))
```

Attributes:

```
attribute NMTOKEN #REQUIRED
alias CDATA #REQUIRED
valueSeparator CDATA ";"
```

## Description

The <Profile> element defines the profiles that are available to apply to an element.

The element can have the following child elements:

<ProfileElement> , <NotProfileElement> , <ProfileFolder>

The <Profile> element has the following attributes:

- • attribute = NMTOKEN

- • alias = CDATA

- • valueSeparator = CDATA



---

# ProfileClasses_Element

## Synopsis

Mixed content model:

```
ProfileClasses
((Profile+, ApplyProfileGroup*, SetProfileGroup*))
```

Attributes:

```
none
```

## Description

The <ProfileClasses> element defines the profiles that are available to apply to an element.

The element can have the following child elements:

<Profile> , <ApplyProfileGroup> , <SetProfileGroup>

The <ProfileClasses> element has no attributes.

- • authorModifiable = true | false



---

# ProfileElement_Element

## Synopsis

Mixed content model:

```
ProfileElement
(AttributeTest*)
```

Attributes:

```
element NMTOKEN #REQUIRED
```

## Description

The <ProfileElement> element defines the elements to which the profile is restricted.

The element can have the following child element:

<AttributeTest>

The <ProfileElement> element has the following attribute:

- • element = NMTOKEN



---

# ProfileFolder_Element

## Synopsis

Mixed content model:

```
ProfileFolder
(ProfileFolder+ | Allowed+)
```

Attributes:

```
name CDATA #REQUIRED
```

## Description

The <ProfileFolder> element specifies the folder structure of a hierarchical (foldered) profile. Folders can contain folders.

The element can have the following child elements:

<ProfileFolder> , <Allowed>

The <ProfileFolder> element has the following attribute:

- • name = CDATA



---

# ProfileRef_Element

## Synopsis

Mixed content model:

```
ProfileRef
Empty
```

Attributes:

```
alias CDATA #REQUIRED
value CDATA #REQUIRED
```

## Description

The <ProfileRef> element specifies the profile to use in a group.

The element has no child elements.

The <ProfileRef> element has the following attributes:

- • alias = CDATA

- • value = CDATA



---

# Profiles_Element

## Synopsis

Mixed content model:

```
Profiles
(ProfileClasses+)
```

Attributes:

```
none
```

## Description

The <Profiles> element is a the top-level element of the .pcf file.

The element can have the following child element:

<ProfileClasses>

The <Profiles> element has no attributes.



---

# RadioChoice_Element

## Synopsis

Mixed content model:

```
RadioChoice
(Allowed*)
```

Attributes:

```
None
```

## Description

The <RadioChoice> element specifies that a profile can only accept one value from a give list of values.

The element can have the following child element:

<Allowed>

The <RadioChoice> element has no attributes.



---

# SetProfileGroup_Element

## Synopsis

Mixed content model:

```
SetProfileGroup
(ProfileRef | LogicalExpression)
```

Attributes:

```
name CDATA #REQUIRED
```

## Description

The <SetProfileGroup> element specifies a combination of profile settings to be used during publishing or resolution.

The element can have the following child elements:

<ProfileRef> , <LogicalExpression>

The <SetProfileGroup> element has the following attribute:

- • name = CDATA