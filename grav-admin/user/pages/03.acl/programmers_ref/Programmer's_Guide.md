

---

# AOM_set_Options_Overview

This appendix describes the options that can be passedas the name parameter to the getOption and setOption methods of the followinginterfaces:

- • Application

- • ADocument

- • View

- • Window

The entire set of options that can be passed is listed in the Arbortext Command Language Reference .The Arbortext Command Language Reference is available in the Arbortext Editor Help Center. Search the HelpCenter for any option by name, or refer to the Help Center index forall options beginning with the term “ set ”.

Options must be of the proper scope for the interface to bepassed with a method. That is, only document scope option names canbe passed with ADocument.setOption ,only window scope option names can be passed with Window.setOption , and so on. The scope of each option is stated at the beginningof each option's description.

Following each option name, the allowed values are listed.

- • Italics represent variable values. For example,

- • Curley braces represent a fixed set of possible values.For example,

Option values are returned as strings by the getOption() methods.

Refer to the Arbortext Command Language Reference for a complete list of options.