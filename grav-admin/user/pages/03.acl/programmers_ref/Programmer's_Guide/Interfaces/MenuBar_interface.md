

---

# find_method

Finds the menu item associated with the menu path specified by menuPath . A menu path is a way of indicating the exact location of the menu item in the menu bar hierarchy. This item can be either an item on a menu or the menu itself.

Menu path syntax is similar to path name syntax, with periods separating the components instead of slashes. The leading parts of a menu path correspond to a menu name, the trailing part matches a menu item. For example, .File.New refers to the item New on the File menu. Menu paths need not specify the trailing ellipsis on a menu item, for example, .File.Open and .File.Open... refer to the same menu item.

A menu path is considered absolute if it starts with a period ( . ). The name following the period must be the name of one of the top-level menus on the menu bar (for example, .File , .Edit , .Tools ). If a menu path does not start with a period, the entire hierarchy for the menu bar is searched for the first occurrence of the item. The search starts with the first menu on the left and progresses down through every item on a menu before moving on to the next menu to the right.

The syntax of a menu path allows specifications of a menu item by position and also by name. If a component of a menu path begins with # and is followed by one or more digits, it specifies a numeric position. For example, the menu path .File.#3 specifies the third item in the File menu. Numeric positions may be specified in any component. For example, .View.#5.#3 is the same as .View.Tools.Table (assuming the default menu configuration). Blank or separator lines within the menu count as items.

Menu item labels may contain ACL variable references. If a menu label contains any variable references (for example, Modify $tagname ), the variable reference is substituted into the label string each time the menu containing the item is posted.

The find method recognizes the following special characters when matching a menu path against the menu hierarchy: