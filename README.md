# GTM.gs 
GTM Manager lets you work with Google Tag Manager in Google Sheets.

## Quick start
Create new spreadsheet, install add-on.

* paste function GTM_ACCOUNTS_LIST()
* Run 
* Get result

![Quick start GTM Manager](img/start.gif "Quick start GTM Manager")


## Pathes
Most functions parameters are pathes (workspace, tag or folder).
You can find path in GTM page URL:  
https://tagmanager.google.com/#/container/accounts/286472777/containers/22777/workspaces/82/variables/12

where:
* accountPath – accounts/286472777    
* containerPath – accounts/286472777/containers/22777
* workspacePath –  accounts/286472777/containers/22777/workspaces/82
* foldersPath –  accounts/286472777/containers/22777/workspaces/82
* variablePath – accounts/286472777/containers/22777/workspaces/82/variables/12
* tagPath – accounts/123/containers/311/workspaces/4/tags/6
* itemPath – accounts/123/containers/311/workspaces/4/tags(variables,triggers)/6

## Functions
Write functions in sheets cell.

ACCOUNT
* GTM_ACCOUNT_LIST() - List of GTM Accounts
* GTM_CONTAINER_LIST(accountPath) - List of Containers
* GTM_VERSION(workspacePath) - Return GTM Version 

WORKSPACE
* GTM_WORKSPACE_LIST(containerPath) - List of Workspaces
* GTM_WORKSPACE_LIST_ALL() - List of ALL Workspaces
* GTM_WORKSPACE_SET_SHEET()
* GTM_WORKSPACE_GET_SHEET()

FOLDER
* GTM_FOLDER_LIST(workspacePath) - List of folder's pathes and names
* GTM_FOLDER_COPY(workspacePath,to_workspacePath) - Copy GTM folder to new workspace

TAGS
* GTM_TAGS_LIST(workspacePath) - List of Tags in Workspace
* GTM_TAGS_LISTX (workspacePath, arr) - Get list of tags with optional params
* GTM_TAGS_LIST_NOTES(workspacePath) - List of Tags with Notes in Workspace
* GTM_TAGS_ANALYTICS(workspacePath) - List of GA Tags with parameters
* GTM_TAGS_GA4(workspacePath) - List of GA4 Tags with parameters use <code>=QUERY({A:D}, "SELECT Col1, MAX(Col4) WHERE Col1<>'' GROUP BY Col1 PIVOT Col2, Col3 LABEL Col1 'Tag Name'")</code> to pivot it
* GTM_TAG_BY_ID(id, workspacePath) - Return Tag with particular ID
* GTM_TAG_UPDATE_CM(key, val, tagPath) - Update Tag's Custom Metric value
* GTM_TAG_UPDATE_CD(key, val, tagPath) - Update Tag's Custom Dimension value
* GTM_TAG_UPDATE_CG(key, val, tagPath) - Update Tag's Content Group value
* GTM_TAG_RM_CM(key, tagPath) - Remove Tag's Custom Metric value
* GTM_TAG_RM_CD(key, tagPath) - Remove Tag's Custom Dimension value
* GTM_TAG_RM_CG(key, tagPath) - Remove Tag's Content Group value
* GTM_TAG_CD(key, tagPath) - Returns Tag's Custom Dimension value
* GTM_TAG_CM(key, tagPath) - Returns Tag's Custom Metric value
* GTM_TAG_CG(key, tagPath) - Returns Tag's Content Group value
* GTM_TAG_UPDATE_EA(val, tagPath) - Update Tag's GA Event Action value
* GTM_TAG_UPDATE_EL(val, tagPath) - Update Tag's GA Event Label value
* GTM_TAG_UPDATE_EC(val, tagPath) - Update Tag's GA Event Category value
* GTM_TAG_UPDATE_EVENT(key, val, tagPath) - Update GA Tag's Event value
* GTM_TAG_UPDATE_GA4_UP(key, val, tagPath) - Update GA4 Tag's User property
* GTM_TAG_UPDATE_GA4_EP(key, val, tagPath)- Update GA4 Tag's Event parameter

VARIABLES
* GTM_VARIABLES_LIST(workspacePath) - List of Variables in Workspace
* GTM_VARIABLE_CUSTOM_JS_CREATE(name, javaScript, workspacePath) - Create "Custom JavaScript" Variable
* GTM_VARIABLE_JS_CREATE(name, javaScript, workspacePath) - Create "JavaScript" Variable
* GTM_VARIABLE_DL_CREATE(name, value, workspacePath, defaultValue) - Create new Data Layer Variable
* GTM_VARIABLES_CUSTOM_JS_UPDATE(javaScript, variablePath) - Update "Custom JavaScript" Variable
* GTM_VARIABLES_LIST_PARAMS(workspacePath) - List of variables with parameters

TRIGGERS
* GTM_TRIGGERS_LIST(workspacePath) - List of Triggers in Workspace
* GTM_TRIGGERS_LISTX(workspacePath, arr) - Get list of triggers with optional params
* GTM_TAG_TRIGGER_ADD(tagPath, triggerId, isBlockingTrigger) - Add Trigger to Tag
* GTM_TRIGGER_USED(workspacePath, triggerId) - Find Tags with exact Trigger

ITEMS
* GTM_ITEMS_LIST(workspacePath) - List of Tags, Triggers and Variables with Name and Path
* GTM_ITEM_REMOVE(itemPath, notes) - Remove Item from GTM
* GTM_ITEM_REVERT(itemPath, notes) - Revert changes in Item in Workspace
* GTM_ITEM_NAME(itemPath) - Return the Name of exact Item (Variable, Tag, Trigger)
* GTM_ITEM_USED(name, workspacePath) - Find Variables, Tags, Triggers used by exact Item
* GTM_ITEM_USING(name, workspacePath) - Find Variables, Tags, Triggers using with exact Item
* GTM_COPY(itemPath, to_workspacePath) - Copy Item (Variable, Tag, Trigger) to new workspace
* GTM_RENAME(itemPath, name) - Set a new Name for Item (Variable, Tag, Trigger)
* GTM_NOTES_ADD(itemPath, notes) - Add Note to Item (Tag, Trigger or Variable)
* GTM_NOTES_LIST(workspacePath) - List of Tags, Triggers and Variables with Notes
* GTM_LINK(path) - Create Hypertext Link from Path
* GTM_FIND(needle, workspacePath) - Search needle point in Workspace
* GTM_RELATIONS(workspacePath) - Create Relations Map
    
    

## Result
Most functions return pair [path, name]
```=GTM_TAGS_LIST("workspacePath");```
retrurns

| path | name |  
| --- | --- |   
| /path/workspace/tag/32 | Tag name |
| /path/workspace/tag/32 | Tag name |


* GTM_NOTES_LIST(workspacePath) - returns item [name, path, type, notes]  
* GTM_COPY(itemPath, to_workspacePath) - copy item to another workspace
* GTM_FOLDER_COPY(folderPath, to_workspacePath) - copy folder with items to another workspace. Breaks if item name exist at acceptor workspace.
* GTM_RENAME(itemPath, name) - rename item
* GTM_WORKSPACE_LIST_ALL - return all accounts, containers and workspaces
* GTM_TAGS_ANALYTICS - return all analytics tags
* GTM_NOTES_ADD(itemPath, notes) - create/update notes for item

Note
Don't use nested GTM functions:
-GTM_A(GTM_B)-
