# Scripting BetterTouchTool using the custom URL Scheme

This is a very recent feature which is only available in **versions greater than 2.430**. 

BetterTouchTool allows to be control via a custom url scheme (btt://).
On this page I'm briefly describing the various functions you can trigger via this URL scheme.

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
* set_persistent_string_variable
* set_string_variable
* set_persistent_number_variable
* set_number_variable


**Note:** Custom URL Schemes can not return values to the calling application/browser. If you need that (e.g. after executing a shell script in BTT), please see the [integrated webserver section](webserver.md)

## Security
BetterTouchTool will ask you the first time you use a btt:// trigger whether you want to allow that. However it doesn't make sense to always continue asking that question as it would destroy the purpose of this.

So to improve security you can define a shared secret which then must be included in all btt:// urls like this: btt://the_function_you_want_to_use/?shared_secret=YourSecret

The shared secret can be defined in the advanced preferences
![shared_secret](media/new/scripting_secret.jpg)


## Available Scripting Interfaces

#### Example Terminal Command (but you can call the URL however you like)

### **trigger_named**

This method will trigger the specified named trigger (which can be configured in the "Other" tab in BetterTouchTool.)

```Bash
open "btt://trigger_named/?trigger_name=TriggerName"
```

### **update_touch_bar_widget**
This method will update the contents of a Touch  Bar Script Widget (identified by its uuid). You can provide a new text to show, a new icon and a new background color.

For the icon you can either provide it directly using the icon_data parameter (must be base64 encoded) or you can provide a file path that points to the new icon (via the icon_path parameter).

You can get the uuid by right-clicking any script widget in BTT.

#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://update_touch_bar_widget/?uuid=CC46E199-B07D-4BF7-AC36-48AAE558540B&text=updatedText&icon_path=/Users/andi/Desktop/test.png&background_color=200,200,100,255"

```

---


### **trigger_action**
This method will trigger any of BetterTouchTool's predefined actions (or any combination of them).

You need to provide a JSON description of the action you want to trigger. The easiest way to get such a JSON description is to right-click the trigger you have configured in BetterTouchTool and choose "Copy JSON". This will copy the complete JSON (including the configuration for the trigger itself), but this action will ignore anything that's not needed. (or you can delete the not needed parts)
#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://trigger_action/?json={ \"BTTPredefinedActionType\" : 153, \"BTTPredefinedActionName\" : \"Move Mouse To Position\", \"BTTMoveMouseToPosition\" : \"{100, 10}\", \"BTTMoveMouseRelative\" : \"6\" }"
```
---


### **execute_assigned_actions_for_trigger**
This method execute all the assigned actions for a given trigger (i.e. gesture, shortcut, drawing etc.) identified by its uuid.

You can get the uuid by right-clicking any configured trigger in BetterTouchTool.

#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://execute_assigned_actions_for_trigger/?uuid=C40D3AE2-2F4E-49B1-A00C-F7E4C3632F07" 

```


---


### **refresh_widget**
This method will execute all scripts assigned to a script widget and update its contents accordingly.

The widget is identified by its uuid, which you can get by right-clicking the widget in BetterTouchTool.

#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://refresh_widget/?uuid=C40D3AE2-2F4E-49B1-A00C-F7E4C3632F07" 

```

---


### **update_trigger**
This method will update the configuration of any trigger you have configured in BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide the uuid of the trigger you want to update (get by right-clicking it in BTT) and a JSON object defining the updates. To know how the JSON object should look like, right-click the trigger in BTT and choose "Copy JSON".


#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://update_trigger/?uuid=0E2F7963-E64C-403A-8591-C3725D4D9ADC&json={\"BTTTouchBarButtonName\" : \"New Name2\",  \"BTTTriggerConfig\" : {\"BTTTouchBarItemIconHeight\" : 30}}"
```

---


### **add_new_trigger**
This method will add a new trigger to BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide a JSON object defining the new trigger. To know how the JSON object should look like, right-click any existing trigger in BTT and choose "Copy JSON".


#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://add_new_trigger/?json={ \"BTTTriggerClass\" : \"BTTTriggerTypeKeyboardShortcut\", \"BTTPredefinedActionType\" : 5, \"BTTPredefinedActionName\" : \"Mission Control\", \"BTTAdditionalConfiguration\" : \"1179658\", \"BTTTriggerOnDown\" : 1, \"BTTEnabled\" : 1, \"BTTShortcutKeyCode\" : 2, \"BTTShortcutModifierKeys\" : 1179648, \"BTTOrder\" : 3 }"
```

---


### **delete_trigger**
This method will delete a trigger from BetterTouchTool.
You need to provide the uuid of the trigger you want to delete (get by right-clicking it in BTT).


#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://delete_trigger/?uuid=0E2F7963-E64C-403A-8591-C3725D4D9ADC"
```


---

### **set_persistent_string_variable**
This allows you to set a variable to a given string that persists over BTT relaunches.

#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://set_persistent_string_variable/?variableName=test&to=12345"
```


---

### **set_string_variable**
This allows you to set a variable to a given string that persists over BTT relaunches.

#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://set_string_variable/?variableName=test&to=12345"
```


---



### **set_persistent_number_variable**
This allows you to set a variable to a given number that persists over BTT relaunches.


#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://set_persistent_number_variable/?variableName=test&to=12345"
```


---

### **set_number_variable**
This allows you to set a variable to a given number for the runtime of BTT.


#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "btt://set_number_variable/?variableName=test&to=12345"
```


---



