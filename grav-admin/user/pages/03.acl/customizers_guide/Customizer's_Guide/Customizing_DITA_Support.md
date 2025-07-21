

---

# Customizing_the_DITA_Resource_Manager

# Customizing the DITA Resource Manager

The Resource Manager dialog box enables you to manage the references inserted into DITA documents. The Resource Manager stores information about its current state in the arbortext.wcf preferences file, so that state can be restored in future sessions. This information is stored in persistent user settings that can be customized to set a desired state at start up using an Arbortext Command Language (ACL) script or Arbortext Object Model (AOM) program. For ACL scripts, you set the preferences with the set_user_property function. For AOM programs, you use the Application.getUserProperties method.

Note that modifying a persistent user property has no effect on currently open Resource Manager dialog boxes. If a preference is modified while the Resource Manager is open, that preference might be overwritten by the dialog box when it closes. It is recommended that you set these preferences in a script or program located in the custom\init directory. That ensures the dialog box is not open at the time the preferences are set. You can also use the dita_reset_rm_state function before specifying your own settings to reset the Resource Manager state and ensure your settings are used. However, this function does remove all of the Resource Manager ’s current state.