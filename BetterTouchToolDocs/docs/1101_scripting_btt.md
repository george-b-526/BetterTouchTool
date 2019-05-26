# Scripting BTT

Starting with BetterTouchTool 2.430 it supports three methods of basic scripting:


* [Via Apple Script](apple_script.md)
* [Via the custom btt:// URL Scheme](custom_url_scheme.md)
* [Via an integrated webserver](webserver.md)

Additionally if you use BetterTouchTool's Floating Web View, you can also trigger all of the methods using Java Script: [Trigger from Floating Web View](floating_menu_javascript.md)


All of these methods support the same functions:
* trigger_named
* update_touch_bar_widget
* trigger_action
* execute_assigned_actions_for_trigger
* refresh_widget
* update_trigger
* add_new_trigger 
* delete_trigger
* trigger_named
* trigger_named_async_without_response
* get_dock_badge_for
* get_active_touch_bar_group
* is_true_tone_enabled
* get_location
* set_persistent_string_variable
* set_string_variable
* set_persistent_number_variable
* set_number_variable
* get_number_variable
* get_string_variable
