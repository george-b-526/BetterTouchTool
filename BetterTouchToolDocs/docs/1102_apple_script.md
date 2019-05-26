# Scripting BetterTouchTool using Apple Script

BetterTouchTool has a small but powerful Apple Script interface which will be described here.

The available scripting interfaces are:
* trigger_named
* trigger_named_async_without_response
* update_touch_bar_widget
* trigger_action
* execute_assigned_actions_for_trigger
* refresh_widget
* update_trigger
* add_new_trigger 
* delete_trigger
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


## Security
In general every application that is allowed to execute Apple Script could trigger these scripting functions. If you do not want this, you can define a shared secret which then must be included in all calls as "shared_secret" parameter.

The shared secret can be defined in the advanced preferences
![shared_secret](media/new/scripting_secret.jpg)

## Available Scripting Interfaces

### **trigger_named**
This method will trigger the specified named trigger (which can be configured in the "Other" tab in BetterTouchTool.)

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

trigger_named "TriggerName" 

end tell
```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.trigger_named("TriggerName");
```
---


### **trigger_named_async_without_response**
This method will trigger the specified named trigger (which can be configured in the "Other" tab in BetterTouchTool.).
In contrast to the trigger_named it does not wait for a result - **this should always be used if you do not need a response**.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

trigger_named_async_without_response "TriggerName" 

end tell
```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.trigger_named_async_without_response("TriggerName");
```
---



### **update_touch_bar_widget**
This method will update the contents of a Touch  Bar Script Widget (identified by its uuid). You can provide a new text to show, a new icon and a new background color.

For the icon you can either provide it directly using the icon_data parameter (must be base64 encoded) or you can provide a file path (via the icon_path parameter) that points to the new icon.

You can get the uuid by right-clicking any script widget in BTT.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

update_touch_bar_widget "9990CE09-9820-4D67-9C52-8BABAB263056" text "newButtonText" icon_path "~/Desktop/005-ShoppingBasket@2x.png" background_color "255,100,100,255"

end tell
```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.update_touch_bar_widget("9990CE09-9820-4D67-9C52-8BABAB263056", 
{
	text: "hi there!",
	icon_path: "/Users/andi/Desktop/test.png",
	background_color: "200,100,100,255"	
});
```
---


### **trigger_action**
This method will trigger any of BetterTouchTool's predefined actions (or any combination of them).

You need to provide a JSON description of the action you want to trigger. The easiest way to get such a JSON description is to right-click the trigger you have configured in BetterTouchTool and choose "Copy JSON". This will copy the complete JSON (including the configuration for the trigger itself), but this action will ignore anything that's not needed. (or you can delete the not needed parts)
#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

	trigger_action "{\"BTTPredefinedActionType\":100}"

end tell

```
#### Java Script for Automation Example:
Hint: don't forget to use JSON.stringify() before passing the actionDefinition object.
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');
var actionDefinition = {
  "BTTPredefinedActionType" : 153, 
  "BTTPredefinedActionName" : "Move Mouse To Position", 
  "BTTMoveMouseToPosition" : "{10, 10}", 
  "BTTMoveMouseRelative" : "6"
};


BetterTouchTool.trigger_action(JSON.stringify(actionDefinition));

```

---


### **execute_assigned_actions_for_trigger**
This method execute all the assigned actions for a given trigger (i.e. gesture, shortcut, drawing etc.) identified by its uuid.

You can get the uuid by right-clicking any configured trigger in BetterTouchTool.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"
	execute_assigned_actions_for_trigger "2F34005D-4537-464D-94E9-A7F42DA39DF1"
end tell

```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.execute_assigned_actions_for_trigger("2F34005D-4537-464D-94E9-A7F42DA39DF1");

```

---


### **refresh_widget**
This method will execute all scripts assigned to a script widget and update its contents accordingly.

The widget is identified by its uuid, which you can get by right-clicking the widget in BetterTouchTool.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"
	refresh_widget "2F34005D-4537-464D-94E9-A7F42DA39DF1"
end tell

```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.refresh_widget("2F34005D-4537-464D-94E9-A7F42DA39DF1");

```

---


### **update_trigger**
This method will update the configuration of any trigger you have configured in BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide the uuid of the trigger you want to update (get by right-clicking it in BTT) and a JSON object defining the updates. To know how the JSON object should look like, right-click the trigger in BTT and choose "Copy JSON".

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

update_trigger "2F34005D-4537-464D-94E9-A7F42DA39DF1" json "{\"BTTTouchBarButtonName\" : \"New Name\",  \"BTTTouchBarItemIconHeight\" : 25}"

end tell


```
#### Java Script for Automation Example:
Hint: don't forget to use JSON.stringify() before passing the actionDefinition object.
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');
var updateDefinition = {
	"BTTTouchBarButtonName" : "New Name",
	"BTTTouchBarItemIconHeight" : 25
}
BetterTouchTool.update_trigger("2F34005D-4537-464D-94E9-A7F42DA39DF1", {json: JSON.stringify(updateDefinition)});

```

---


### **add_new_trigger**
This method will add a new trigger to BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide a JSON object defining the new trigger. To know how the JSON object should look like, right-click any existing trigger in BTT and choose "Copy JSON".

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

add_new_trigger "{ \"BTTTriggerClass\" : \"BTTTriggerTypeKeyboardShortcut\", \"BTTPredefinedActionType\" : 5, \"BTTPredefinedActionName\" : \"Mission Control\", \"BTTAdditionalConfiguration\" : \"1179658\", \"BTTTriggerOnDown\" : 1, \"BTTEnabled\" : 1, \"BTTShortcutKeyCode\" : 2, \"BTTShortcutModifierKeys\" : 1179648, \"BTTOrder\" : 3 }"

end tell

```
#### Java Script for Automation Example:
Hint: don't forget to use JSON.stringify() before passing the actionDefinition object.
```JavaScript

// this will add a new keyboard shortcut to BTT.
var BetterTouchTool = Application('BetterTouchTool');

var newTriggerDefinition = {
  "BTTTriggerClass" : "BTTTriggerTypeKeyboardShortcut",
  "BTTPredefinedActionType" : 5,
  "BTTPredefinedActionName" : "Mission Control",
  "BTTAdditionalConfiguration" : "1179648",
  "BTTTriggerOnDown" : 1,
  "BTTEnabled" : 1,
  "BTTShortcutKeyCode" : 2,
  "BTTShortcutModifierKeys" : 1179648,
  "BTTOrder" : 3
}

BetterTouchTool.add_new_trigger(JSON.stringify(newTriggerDefinition))

```




### **delete_trigger**
This method will delete a trigger from BetterTouchTool.
You need to provide the uuid of the trigger you want to delete (get by right-clicking it in BTT).

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

delete_trigger "2F34005D-4537-464D-94E9-A7F42DA39DF1"

end tell


```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.delete_trigger("2F34005D-4537-464D-94E9-A7F42DA39DF1");

```

---


### **set_persistent_string_variable**
This allows you to set a variable to a given string that persists over BTT relaunches.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

    set_persistent_string_variable "variableName" to "this is a test value"

end tell


```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.set_persistent_string_variable("variableName", {to: "this is a test value"});

```

---

### **set_string_variable**
This allows you to set a variable to a given string that persists over BTT relaunches.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

    set_string_variable "variableName" to "this is a test value"

end tell


```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.set_string_variable("variableName", {to: "this is a test value"});

```

---


### **set_persistent_number_variable**
This allows you to set a variable to a given string that persists over BTT relaunches.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

    set_persistent_number_variable "variableName" to 12345

end tell


```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.set_persistent_number_variable("variableName", {to: 1345});

```

---


### **set_number_variable**
This allows you to set a variable to a given string that persists over BTT relaunches.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

    set_number_variable "variableName" to 12345

end tell


```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.set_number_variable("variableName", {to: 1345});

```

---

### **get_number_variable**
This allows you to retrieve the contents of a number variable with the given name

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

    return get_number_variable "variableName"

end tell


```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.get_number_variable("variableName");

```

---

### **get_string_variable**
This allows you to retrieve the contents of a string variable with the given name

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

    return get_string_variable "variableName"

end tell


```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.get_string_variable("variableName");

```

---


### **get_dock_badge_for**
This method will efficiently get the current Dock badge for a specific application. Running this function multiple times will return the previously cached value until the specified update_interval has been reached. 

When an update interval is provided, BTT will internally refresh the badges for all apps every x seconds. In this case consecutive "get_dock_badge_for" function calls are basically free, as they will just return the last cached value. This is the recommended way to do it, and the update_interval should not be too small.

If you need to refresh the cache immediately for some reason, you can leave the update_interval function out. Then BTT will immediately refresh all the dock badges and return the latest value.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

	get_dock_badge_for "Calendar" update_interval 5

end tell


```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.get_dock_badge_for("Calendar", {'update_interval': 5});

```

---
