

---

# getDefaultParameters_method

Returns the pipeline's default parameters.



---

# getParamDocumentation_method

Returns the documentation DOMString for a parameter. The result is the content of the Documentation child of the Parameter element in the Interface section of the CCF.



---

# getParamEnumerationValues_method

Returns an array of options for an enumeration parameter. Each entry in the list is a DOMString object. The parameter value, as passed to runPipeline(Map) , must match an option. The list is the content of the Value children of the Parameter element in the Interface section of the CCF.



---

# getParamLabel_method

Returns the label DOMString for a parameter. The result is the content of the Label child of the Parameter element in the Interface section of the CCF.



---

# getParamType_method

Returns the type string for a parameter. The result is the type attribute of the Parameter element in the Interface section of the CCF.



---

# isParamRequired_method

Returns the required flag for a parameter. A composer cannot be run unless all required parameters have been given values. The value is the required attribute of this Parameter in the Interface section of the CCF.



---

# runPipeline_method

Runs the pipeline defined by the CCF using the given map of parameter values.