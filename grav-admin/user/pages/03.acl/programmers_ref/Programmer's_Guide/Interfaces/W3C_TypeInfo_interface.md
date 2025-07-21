

---

# DerivationMethods_enumeration

These are the available values for the derivationMethod parameter used by the method TypeInfo.isDerivedFrom() . It is a set of possible types of derivation, and the values represent bit positions. If a bit in the derivationMethod parameter is set to 1 , the corresponding type of derivation will be taken into account when evaluating the derivation between the reference type definition and the other type definition. When using the isDerivedFrom method, combining all of them in the derivationMethod parameter is equivalent to invoking the method for each of them separately and combining the results with the OR boolean function. This specification only defines the type of derivation for XML Schema.

In addition to the types of derivation listed below, please note that:

- • any type derives from xsd:anyType .

- • any simple type derives from xsd:anySimpleType by restriction.

- • any complex type does not derive from xsd:anySimpleType by restriction.

The DerivationMethods enumeration has the following constants of type unsigned short .



---

# isDerivedFrom_method

This method returns if there is a derivation between the reference type definition, i.e. the TypeInfo on which the method is being called, and the other type definition, i.e. the one passed as parameters.



---

# typeName_attribute

The name of a type declared for the associated element or attribute, or null if unknown. Implementations may also use null to represent XML Schema anonymous types.



---

# typeNamespace_attribute

The namespace of the type declared for the associated element or attribute or null if the element does not have declaration or if no namespace information is available. Implementations may also use null to represent XML Schema anonymous types.