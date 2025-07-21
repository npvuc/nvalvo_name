

---

# appendChild_method

Appends the component newChild to the end of the list of children. If the newChild is already in the tree, it is first removed.



---

# componentType_attribute

A code representing the type of the underlying object, as defined by ComponentType .



---

# ComponentType_enumeration

The ComponentType enumeration is an integer showing which type of component object this is.

The ComponentType enumeration has the following constants of type unsigned short .



---

# firstChild_attribute

The first child of this component. If there is no such component, this returns null .



---

# insertBefore_method

Inserts the component newChild before the existing child component refChild . If refChild is null , insert newChild at the end of the list of children.



---

# isSameComponent_method

Returns whether this component is the same component as the given one.

This method provides a way to determine whether two Component references returned by the implementation reference the same object. When two Component references are references to the same object, even if through a proxy, the references may be used completely interchangeably, such that all attributes have the same values and calling the same AOM method on either reference always has exactly the same effect.



---

# lastChild_attribute

The last child of this component. If there is no such component, this returns null .



---

# nextSibling_attribute

The next sibling of this component. If there is no such component, this returns null .



---

# ownerWindow_attribute

The Window in which this component resides.



---

# parentComponent_attribute

The parent of this component . If a component has just created and not yet added to the tree, or if it has been removed from the tree, this is null .



---

# previousSibling_attribute

The previous sibling of this component. If there is no such component, this returns null .



---

# removeChild_method

Removes the child component indicated by oldChild from the list of children, and returns it.



---

# replaceChild_method

Replaces the child component oldChild with newChild in the list of children, and return the oldChild component.



---

# text_attribute

The text associated with the component. The values vary according to the component type as follows:

For menu items, you can specify an access key in the label by placing an ampersand ( & ) before the character to be used as the key. For example, to specify F as the access key for "File", you should specify the label as " &File ". The character that follows the ampersand in a label is also known as the mnemonic of the menu item. The label for a menu separator is a dash ( - ).