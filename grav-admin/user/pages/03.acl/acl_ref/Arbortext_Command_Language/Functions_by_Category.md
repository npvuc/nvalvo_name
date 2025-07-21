

---

# Applicability_Functions

# Applicability Functions



- • registerApplicabilitySyntax function



---

# Application_Management_Functions

# Application Management Functions



- • application_name function

- • doc_clone function

- • doc_dir function

- • get_custom_dir function

- • get_custom_property function

- • get_user_property function

- • set_user_property function



---

# Array,_Variable,_and_Package_Functions

# Array, Variable, and Package Functions



Array, variable, and package functions operate on ACL features (arrays, variables, functions, and packages) or provide information about commands and options.

- • append_catalog_path function

- • append_composer_path function

- • append_dialogs_path function

- • append_dita_path function

- • append_entity_path function

- • append_frameset_path function

- • append_graphics_path function

- • append_javaclass_path function

- • append_load_path function

- • append_newlist_path function

- • append_path function

- • append_tagtemplate_path function

- • append_userdict_path function

- • buffer_empty function

- • caller function

- • caller_file function

- • caller_line function

- • catch function

- • cmd_exists function

- • cmd_key function

- • count function

- • defined function

- • delete function

- • eval (Function) function

- • execute (Function) function

- • graphic_views function

- • high_bound function

- • low_bound function

- • option function

- • package_file function

- • package_name function

- • package (Function) function

- • packages function

- • qsort function

- • require (Function) function

- • throw function

- • varsub function



---

# Buffer_Functions

# Buffer Functions



Buffer functions operate on named paste buffers.

- • buffer_clipboard_contents function

- • buffer_clipboard_formats function

- • buffer_create function

- • buffer_doc function

- • buffer_empty function

- • buffer_is_clipboard function

- • buffer_is_table function

- • insert_buffer function



---

# Byte_String_Functions

# Byte String Functions



Byte string functions operate on byte strings. Byte strings are used to represent binary data as opposed to character strings which represent Unicode strings (two bytes per character).

- • blength function

- • chop function

- • index function

- • length function

- • mblen function

- • mbstoucs function

- • oct function

- • pack function

- • rindex function

- • substr function

- • trim function

- • ucstombs function

- • unpack function



---

# Callback_Functions

# Callback Functions



A callback function is a user-defined function that is called during specific events in Arbortext Editor and allows you to customize editing operations. Callback functions provide both a global and a local level of registration or notification to isolate events, while hooks provide only global effect (unless additional user functions are supplied). For example, you might want a particular function called whenever a specific document is saved or a help window has a quit request.

- • channel_set_callback function

- • dlgitem_add_callback function

- • dlgitem_remove_callback function

- • doc_add_callback function

- • doc_remove_callback function

- • session_add_callback function

- • session_remove_callback function

- • timer_add_callback function

- • timer_remove_callback function

- • userule_add_callback function

- • userule_remove_callback function

- • window_add_callback function

- • window_remove_callback function



---

# Change_Tracking_Functions

# Change Tracking Functions



The change tracking feature in Arbortext Editor tracks text and markup changes made to a baseline document. These functions attempt to accept, reject, locate and collect information from the baseline document.

- • change_tracking_accept_change function

- • change_tracking_accept_selection function

- • change_tracking_find function

- • change_tracking_info function

- • change_tracking_reject_change function

- • change_tracking_reject_selection function

- • change_tracking_user_list function

- • change_tracking_user_properties function

- • doc_has_change_tracking function

- • selection_has_change_tracking function



---

# Channel_Functions

# Channel Functions



The channel functions provide interfaces to the Berkeley socket library, which allows network applications to be written. The open functions return channel identifiers that may also be used with most file identifier functions (for example, read , write , and close ). Several open_ routines return a channel identifier that may be used by subsequent I/O functions. A channel identifier is a small integer file identifier that is returned by open and can be used with the file identifier routines getline , put , close , read , and write . These channel functions allow binary data to be transmitted.

- • open_accept function

- • open_connect function

- • open_listen function

- • pack function

- • read (Function) function

- • unpack function

- • write (Function) function



---

# Column_View_Functions

# Column View Functions



Column view is a Arbortext Editor view specifically designed to support document types that primarily consist of element and attribute content. These functions enable you to operate in column view.

- • columnview_cell_focus function

- • columnview_is_defined function

- • window_get_columnview function

- • window_set_columnview function



---

# COM_Interface_Functions

# COM Interface Functions



These functions support COM (Component Object Model) calls.

- • com_attach function

- • com_call function

- • com_prop_get function

- • com_prop_put function

- • com_release function



---

# Composer_Functions

# Composer Functions



These functions support operations in a log file.

- • composer_log function

- • get_composer_log_contents function

- • get_composer_log_doc function

- • show_composer_log function



---

# Context-Related_Functions

# Context-Related Functions



Context-related functions pertain to the context for a given element in a DTD or at a point within a specific document.

- • content_model function

- • context_full_paths function

- • context_paths function

- • context_string function

- • cut_valid function

- • delete_markup_valid function

- • in_context function

- • in_context_list function

- • oid_expose function

- • oid_paste_valid function

- • oid_show_attr function

- • tag_content function



---

# Custom_Dialog_Box_Functions

# Custom Dialog Box Functions



The Arbortext XUI technology lets an application programmer create, display, manipulate, and modify dialog boxes in real time by writing and modifying XML documents. Refer to the Customizer's Guide for details on working with XUI dialog boxes.



---

# Dialog_Box_Functions

# Dialog Box Functions



Dialog box functions provide dialog boxes for user interaction.

- • color_chooser function

- • file_selector function

- • list_response function

- • panel_popup function

- • response function



---

# Document_Identifier_Functions

# Document Identifier Functions



Most of the Document type functions also take an optional final argument, which is a document ID. Document Identifier functions return or take document identifiers.

- • current_doc function

- • doc_cache_base function

- • doc_cache_dir function

- • doc_clean_cache function

- • doc_clone function

- • doc_close function

- • doc_delete_stylesheet_association function

- • doc_estimate_dfs function

- • doc_formattable function

- • doc_get_stylesheet_association function

- • doc_incomplete function

- • doc_invalidate_graphics function

- • doc_kind function

- • doc_list function

- • doc_name function

- • doc_new_stylesheet_association function

- • doc_num_stylesheet_associations function

- • doc_open function

- • doc_parent function

- • doc_path function

- • doc_read_only function

- • doc_revert function

- • doc_save function

- • doc_set function

- • doc_set_path function

- • doc_set_stylesheet_association function

- • doc_set_translation_locale function

- • doc_set_translation_orig_uri function

- • doc_show function

- • doc_update_display function

- • doc_valid function

- • doc_window function

- • path_doc function

- • save_as_html_file function

- • save_some_docs function



---

# Document_Type_Functions

# Document Type Functions



Document type functions return information about a particular document type. Most functions take an optional final argument. This final argument is a document identifier that determines the document type.

- • base_tag_name function

- • bulleted_list_block_tag_name function

- • bulleted_list_block_tag_name_ns function

- • bulleted_list_item_tag_name function

- • bulleted_list_item_tag_name_ns function

- • catalog_reslove function

- • char_entity_names function

- • content_model function

- • dcf_option function

- • dcf_validate function

- • dcfmodel_element_list function

- • ditaref_resolve function

- • division_heading_tag function

- • division_tag function

- • doc_compose_stylesheets function

- • doc_dtd_not_defined function

- • doc_dtd_not_found function

- • doc_freeform function

- • doc_namecase_sensitive function

- • doc_type function

- • doc_type_dcf_file function

- • doc_type_description function

- • doc_type_dir function

- • doc_type_dita function

- • doc_type_extension function

- • doc_type_file function

- • doc_type_gi function

- • doc_type_language function

- • doc_type_namespace function

- • doc_type_namespaces function

- • doc_type_xml function

- • dtd_decl_path function

- • dtd_tag function

- • entity_tag function

- • file_entity_tag function

- • file_is_graphic function

- • framesets function

- • graphic_attr_name function

- • graphic_entity_attr_name function

- • graphic_entity_names function

- • graphic_entity_tag function

- • graphic_file_attr_name function

- • graphic_format function

- • graphic_information function

- • graphic_relative_path function

- • graphic_tag function

- • graphic_tag_name function

- • hidden_tag function

- • htmldoc function

- • indexproc function

- • insert_graphic_file function

- • ixkey_charent function

- • legal_name function

- • link_idref_attr_name function

- • link_tag function

- • link_tag_name function

- • link_uri_attr_name function

- • marked_section_tag function

- • numbered_list_block_tag_name function

- • numbered_list_block_tag_name_ns function

- • numbered_list_item_tag_name function

- • numbered_list_item_tag_name_ns function

- • oid_content_model function

- • oid_set_graphics_pathname function

- • path_public_ids function

- • procins_tag function

- • public_id function

- • public_id_path function

- • sgml_feature function

- • strcoll function

- • system_id function

- • tag_attr_choices function

- • tag_attr_conref function

- • tag_attr_default function

- • tag_attr_fixed function

- • tag_attr_required function

- • tag_attr_type function

- • tag_attr_value function

- • tag_attrs function

- • tag_content function

- • tag_create function

- • tag_description function

- • tag_display (Function) function

- • tag_diaplay_name function

- • tag_exists function

- • tag_has_attr function

- • tag_has_conref function

- • tag_names function

- • tag_names_ns function

- • tag_real_name function

- • tag_substitutions function

- • text_entity_names function

- • text_entity_tag function

- • text_style_tag_name function

- • text_style_tag_name_ns function

- • uri_resolve function

- • user_tag_names function



---

# Dynamic_Loading_(API)_Functions

# Dynamic Loading (API) Functions



Dynamic loading functions provide a direct interface to the operating system facilities for loading, calling, and unloading functions in dynamically loaded (shared) libraries. In the Windows environment, this includes the following dynamic link library APIs: LoadLibrary , FreeLibrary and GetProcAddress . These functions also allow you to extend ACL by writing DLLs in C or in other programming languages that support DLLs.

- • dl_builtin_addr function

- • dl_call function

- • dl_error function

- • dl_find function

- • dl_load function

- • dl_unload function

- • dom_address function

- • dom_document function

- • dom_free function

- • dom_oid function

- • interpreter_addr function

- • pack function

- • unpack function



---

# Editor_Functions

# Editor Functions



Editor functions query or change the state of a document instance. The OID functions that change the document tree are also found in the “Object identifier (OID) functions” topic.

- • caret_at function

- • caret_in_selection function

- • caret_show function

- • compare_files function

- • current_tag_attr_value function

- • current_tag_name function

- • detail_tag function

- • direction function

- • doc_from_compare function

- • doc_save function

- • doc_word_count function

- • edit_id function

- • edit_new_window function

- • find function

- • forward_char function

- • generate_id function

- • get_default_printer function

- • get_newlist_entry function

- • get_num_printers function

- • goto_oid function

- • graphic_viewer function

- • insert function

- • insert string (Function) function

- • insert_tag (Function) function

- • inside_tag function

- • is_postscript_printer function

- • item_tag function

- • list_tag function

- • looking_at function

- • lookup function

- • lookup_types function

- • lookup_replacements function

- • marking function

- • modified function

- • modify_attr function

- • mouse_at function

- • mouse_in_selection function

- • oid_delete function

- • oid_delete_attr function

- • oid_modify_attr function

- • oid_top_pos function

- • replace function

- • scroll_to_oid function

- • selected function

- • selected_element function

- • selection_anchor function

- • selection_balanced function

- • selection_end function

- • selection_markup function

- • selection_start function

- • spellskip_tag function

- • target_id_attr_name function

- • target_tag function

- • target_tag_name function

- • thesaurus function



---

# Entity_Functions

# Entity Functions



Entity functions provide information about general text entities or external file entities.

- • add_filep_entity function

- • declare_char_entity function

- • declare_file_entity function

- • declare_filep_entity function

- • declare_graphic_entity function

- • declare_notation function

- • declare_text_entity function

- • doc_flatten function

- • entity function

- • entity_doc function

- • entity_exists function

- • entity_expand function

- • entity_first function

- • entity_last function

- • entity_name function

- • entity_notation function

- • entity_parfile function

- • entity_path function

- • entity_pubid function

- • entity_relative_path function

- • entity_resolve function

- • entity_source function

- • entity_sysid function

- • entity_tag function

- • entity_to_unicode function

- • entity_type function

- • file_entity_names function

- • filep_entity_names function

- • graphic_entity_names function

- • insert_filep_entity function

- • modify_file_entity function

- • modify_graphic_entity function

- • modify_text_entity function

- • msp_entity_names function

- • rename_ms_parameter function

- • text_entity_names function

- • undeclare_ms_parameter function

- • unicode_to_entity function



---

# File_Identifier_Functions

# File Identifier Functions



File identifier functions manipulate file identifiers (FIDs) returned by the open function. These functions provide an interface to the C-library standard I/O routines.

- • close function

- • eof function

- • flush function

- • get_preferences_path function

- • getline function

- • open function

- • put function

- • read (Function) function

- • seek function

- • tell function

- • truncate function

- • write (Function) function



---

# File_or_System_Functions

# File or System Functions



File or system functions provide file or system information or are used to manipulate pathnames.

- • absolute_file_name function

- • access function

- • basename function

- • dirname function

- • disable_windows function

- • doc_clean_cache function

- • drop_file_info function

- • expand_file_name function

- • error function

- • errors_suppressed function

- • file_close function

- • file_directory function

- • file_mtime function

- • file_newer function

- • file_public_id function

- • file_size function

- • file_system function

- • filename_to_url function

- • find_file_in_path function

- • getpid function

- • glob function

- • graphic_viewer function

- • http_cache_flush function

- • pwd function

- • system function

- • temp_name function

- • unmask function

- • universal_file_name function

- • url_decode function

- • url_encode function

- • username function



---

# Hook_Functions

# Hook Functions



A hook is a user-defined function that is called at strategic places by Arbortext Editor so you can customize editing operations. Setting a hook has global effect unless you build in additional user functions to specify a local level.

- • adapterstatehook function

- • catalogpathhook function

- • changetrackingaccepthook function

- • changetrackingafterhook function

- • changetrackingrejecthook function

- • chdirhook function

- • compositionframeworkhook function

- • dcfreloadhook function

- • doc_create_hook function

- • editbeforehook function

- • editfilehook function

- • editshowhook function

- • entitydeclconflicthook function

- • entityflattenhook function

- • entitylockhook function

- • formatbeforehook function

- • formatcomplethook function

- • formatcontinuehook function

- • formaterrorhook function

- • formatpagestatushook function

- • graphicpathhook function

- • htmldoccompletehook function

- • htmlfloathook function

- • htmlimginserthook function

- • includeflattenhook function

- • includelockhook function

- • ixkeycharenthook function

- • ixkeymarkuphook function

- • keybaselistchangedhook function

- • keyrefResolveHook function

- • menuloadbeforehook function

- • menuloadhook function

- • newfilehook function

- • parsererrorhook function

- • postexporthook function

- • postimporthook function

- • preexporthook function

- • preferencehook function

- • preimporthook function

- • previewlinkhook function

- • printcompletehook function

- • profiledochook function

- • tblmodelprompthook function

- • untrackedchangehook function

- • userulehook function

- • writetexafterhook function

- • writetexhook function



---

# Import-Export_Functions

# Import/Export Functions



These functions start either an import or export process with the specified parameters.

- • document_export function



---

# Java,_JavaScript,_JScript,_and_VBScript_Functions

# Java, JavaScript, JScript, and VBScript Functions



Java, JavaScript, JScript, and VBScript expressions and scripts can be called, created, read and executed from Arbortext Command Language using the functions listed.

- • append_javaclass_path function

- • java_array_from_acl function

- • java_array_to_acl function

- • java_console function

- • java_constructor function

- • java_constructor_modal function

- • java_delete function

- • java_init function

- • java_instance function

- • java_instance_modal function

- • java_static function

- • java_static_modal function

- • javascript function

- • jscript function

- • js_source function

- • vbscript function



---

# Layout_Functions

# Layout Functions



These functions enable changes to be made to page layout.

- • apply function

- • linenum function

- • oid_find_valid_insert function

- • oid_logical_mate function



---

# Macro_Recorder_Functions

# Macro Recorder Functions



These functions are available for customizing a site’s use of the macro recorder.

- • macro_exists function

- • macro_pause_recording function

- • macro_record function

- • macro_record_cmd function

- • macro_recording function

- • macro_run function

- • macro_running function

- • macro_stop_recording function



---

# Menu_and_Keymap_Functions

# Menu and Keymap Functions



The menu and keymap functions query keymaps or the menu system.

- • key_cmd function

- • keymap_exists function

- • menu_active function

- • menu_checked function

- • menu_cmd function

- • menu_exists function

- • menu_item_array function

- • menu_item_count function

- • menu_popup function

- • undo_menu_description function

- • undo_menu_description_clear function



---

# Message_Localization_Functions

# Message Localization Functions



These functions are used when working with localized message files.

- • agettext function

- • amo_close function

- • amo_open function

- • amo_text function

- • cjk_locale function

- • getlocale function

- • locale_file_name function



---

# Miscellaneous_Functions

# Miscellaneous Functions



These are miscellaneous functions for operating within Arbortext Editor .

- • exit_editor function

- • font_families function

- • function_argc function

- • function_file function

- • function_names function

- • init_done function

- • license function

- • license_info function

- • license_release function

- • terminal_mode function



---

# Notation_Functions

# Notation Functions



Notation functions provide information about notations declared in a document.

- • notation_exists function

- • notation_names function

- • notation_parfile function

- • notation_pubid function

- • notation_source function

- • notation_sysid function



---

# Numeric_Functions

# Numeric Functions



These functions are used when returning numeric character values.

- • chr function

- • dimen_convert function

- • hex function

- • max function

- • min function

- • oct function

- • ord function



---

# Object_Identifier_(OID)_Functions

# Object Identifier (OID) Functions



An OID is a unique identifier that locates an element within the structure of a parsed document instance. The OID also records to which document instance the element belongs. This means you can save an OID in a variable, and then later refer to it in OID functions. It makes no difference what the current document is.

- • doc_first_dobj function

- • doc_next_dobj function

- • goto_oid function

- • oid_asis function

- • oid_attr function

- • oid_attr_list function

- • oid_attr_required function

- • oid_attr_type function

- • oid_backward function

- • oid_caret function

- • oid_caret_offset function

- • oid_caret_pos function

- • oid_check_attr function

- • oid_child function

- • oid_children function

- • oid_content function

- • oid_content_model function

- • oid_context_string function

- • oid_current_tag function

- • oid_declared_tag function

- • oid_delete function

- • oid_delete_attr function

- • oid_detail function

- • oid_detailed function

- • oid_dialog function

- • oid_doc function

- • oid_effective_dita_default_attrs function

- • oid_effective_dita_attr function

- • oid_effective_dita_attrs function

- • oid_empty function

- • oid_encl_include function

- • oid_entity_first function

- • oid_entity_last function

- • oid_entity_lock function

- • oid_expose function

- • oid_find_children function

- • oid_find_child_attrs function

- • oid_find_parent_attrs function

- • oid_find_valid_insert function

- • oid_first function

- • oid_first_tag function

- • oid_forward function

- • oid_gentext function

- • oid_gentext_source function

- • oid_get_icon function

- • oid_graphic_current_view function

- • oid_graphic_format function

- • oid_graphic_pathname function

- • oid_graphic_size function

- • oid_graphic_viewer function

- • oid_has_attr function

- • oid_id_attr_name function

- • oid_in_doc function

- • oid_include_expand function

- • oid_invalid_markup function

- • oid_invalidate_graphic function

- • oid_is_gentext function

- • oid_last function

- • oid_level function

- • oid_logical_mate function

- • oid_modified function

- • oid_modify_attr function

- • oid_mouse_pos function

- • oid_name function

- • oid_namespace_prefix function

- • oid_namespace_prefix_defined function

- • oid_namespace_stack function

- • oid_namesapce_uri function

- • oid_next function

- • oid_null function

- • oid_offset function

- • oid_parent function

- • oid_paste_valid function

- • oid_prev function

- • oid_prompt_attrs function

- • oid_protected function

- • oid_read_only function

- • oid_root function

- • oid_same_doc function

- • oid_select function

- • oid_set_graphic_pathname function

- • oid_set_icon function

- • oid_show_attr function

- • oid_split_tag function

- • oid_tbl_obj_list function

- • oid_top_pos function

- • oid_treeloc function

- • oid_type function

- • oid_unknown function

- • oid_unknown_attr_list function

- • oid_valid function

- • oid_visible_change_tracking function

- • oid_write_graphic function

- • oid_xpath_boolean function

- • oid_xpath_integer function

- • oid_xpath_matches function

- • oid_xpath_nodeset function

- • oid_xpath_string function

- • scroll_to_oid function

- • selected_element function

- • selection_end function

- • selection_start function

- • treeloc_oid function



---

# Profiling_Functions

# Profiling Functions



These functions support profiling and allow for site-specific customizations of Arbortext Editor profiling capabilities.



---

# Schema_Functions

# Schema Functions



These functions validate a document against a schema.

- • ns_schema_validate_batch function

- • schema_validate function

- • schema_validate_batch function



---

# Set_Option_Functions

# Set Option Functions



Set options define how a scope can affect your Arbortext Editor session. These functions either return or set the value of the specified option, which is used to update the current scope.

- • doc_get function

- • doc_set function

- • languages function

- • option_scope function

- • option_type function

- • option_value_max function

- • option_value_min function

- • option_value_units function

- • option_value_validate function

- • option_values function

- • preference function

- • read_preferences function

- • window_reset_configuration function

- • window_set function

- • write_preferences function



---

# String_Functions

# String Functions



A string specifies the text to be inserted at the cursor location.

- • chop function

- • chr function

- • dupl function

- • gsub function

- • hex function

- • index function

- • join (Function) function

- • length function

- • match function

- • match_length function

- • match_result function

- • match_start function

- • oct function

- • ord function

- • reverse function

- • rindex function

- • span function

- • split (Function) function

- • strcoll function

- • sub function

- • substr function

- • tolower function

- • toupper function

- • trim function



---

# Stylesheet_Functions

# Stylesheet Functions



Stylesheets are a collection of style settings that control the appearance of a document. These functions control operations within the stylesheet.

- • clear_stylesheet function

- • fosi_public_id function

- • list_stylesheets function

- • styler function

- • styler_enabled function

- • styler_get_styled_elements function

- • stylesheet function

- • stylesheet_export_fosi function

- • stylesheet_export_xsl function

- • stylesheet_gentext_lang_stats function

- • stylesheet_get_list_dir function

- • stylesheet_get_list_doc function

- • stylesheet_import_xlf function

- • stylesheet_list_add function

- • stylesheet_new function

- • stylesheet_revert function

- • stylesheet_save function

- • stylesheet_saveas function

- • stylesheet_select function



---

# Table_Functions

# Table Functions



Table functions edit tables in the Edit window.

- • go_to_cell function

- • tbl_area_celllist function

- • tbl_caret_col function

- • tbl_caret_row function

- • tbl_dlg_target function

- • tbl_edit_close function

- • tbl_edit_open function

- • tbl_hline_rulelist function

- • tbl_insert function

- • tbl_insert_rows_cols_dlg function

- • tbl_insert_table_dlg function

- • tbl_insertion_valid function

- • tbl_mod_borders_dlg function

- • tbl_mod_cellfont_dlg function

- • tbl_mod_cells_dlg function

- • tbl_mod_table_dlg function

- • tbl_model_celllist function

- • tbl_model_id function

- • tbl_model_list function

- • tbl_model_name function

- • tbl_model_operation function

- • tbl_model_row function

- • tbl_model_support function

- • tbl_model_table_title function

- • tbl_model_tablelist function

- • tbl_model_taglist function

- • tbl_model_wrapperlist function

- • tbl_multicell_border function

- • tbl_multicell_celllist function

- • tbl_multicell_neighborlist function

- • tbl_multicell_size function

- • tbl_multicell_spanner function

- • tbl_selection_clone function

- • tbl_selection_empty function

- • tbl_selection_get function

- • tbl_selection_matchbegin function

- • tbl_selection_matchnext function

- • tbl_selection_nextrectangle function

- • tbl_selection_pasterectangle function

- • tbl_selection_pastetype function

- • tbl_selection_restore function

- • tbl_selection_tmid function

- • tbl_selection_valid function

- • tbl_table_title_delete function

- • tbl_table_titlle_insert function

- • tbline_vline_rulelist function

- • window_cur_table function



---

# Time_Functions

# Time Functions



Time functions return time information or create timers.

- • ctime function

- • elapsed_time function

- • file_mtime function

- • time_date function

- • timer_add_callback function

- • timer_remove_callback function

- • time (Function) function

- • times function



---

# Translation_Functions

# Translation Functions



These functions find, return , and set values of a translated version of a document.

- • doc_is_translation function

- • doc_get_translation_locale function

- • doc_set_translation_locale function

- • doc_get_translation_orig_uri function

- • doc_set_translation_orig_uri function



---

# Window_Functions

# Window Functions



Window functions operate on window identifiers.

- • current_event function

- • current_window function

- • drag_start function

- • drag_stop function

- • event_process function

- • event_stop_process function

- • mouse_set_waiting function

- • window_activate function

- • window_add_recent_documents function

- • window_cascade_all function

- • window_class function

- • window_close function

- • window_count function

- • window_create function

- • window_cur_table function

- • window_destroy function

- • window_doc function

- • window_empty function

- • window_enable function

- • window_get function

- • window_get_columnview function

- • window_id function

- • window_list function

- • window_load_component_file function

- • window_lower function

- • window_mask function

- • window_name function

- • window_open function

- • window_raise function

- • window_redisplay function

- • window_remove_split function

- • window_reset_configuration function

- • window_set function

- • window_set_columnview function

- • window_show function

- • window_split function

- • window_state function

- • window_sync function

- • window_sync_pane function

- • window_sys_close function

- • window_sys_keymenu function

- • window_sys_maximize function

- • window_sys_minimize function

- • window_sys_move function

- • window_sys_restore function

- • window_sys_size function

- • window_table_left_column function

- • window_table_right_column function

- • window_update function

- • window_xid function

- • windows_disabled function



---

# XPath_Functions

# XPath Functions



Placeholder for introductory content.

- • xpath_boolean function

- • xpath_integer function

- • xpath_nodeset function

- • xpath_string function

- • xpath_valid function