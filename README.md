# GTM.gs 
GTM gs lets you work with Google Tag Manager in Google Sheets.

## Quick start
To get table with all accounts, containers and workspaces
1. Write formula ```=GTM_WORKSPACE_LIST_ALL```
2. Click in spreadsheet navigation:
Add-ons > GTM.gs > RunAllFormulas

Item - Tag, Variable or Trigger.

We write functions in sheets cell. Most functions parameters are pathes (workspace, tag or folder).
You can find path in GTM URL:  
https://tagmanager.google.com/#/container/accounts/286472777/containers/22777/workspaces/82/variables/12
where:
* account path – accounts/286472777    
* container path – accounts/286472777/containers/22777
* workspace path –  accounts/286472777/containers/22777/workspaces/82
* variable path – accounts/286472777/containers/22777/workspaces/82/variables/12

Most functions return pair [path, name]
```=GTM_TAGS_LIST(workspacePath);```
retrurns
| path | name |  
| --- | --- |   
| /path/workspace/tag/32 | Tag name |
| /path/workspace/tag/32 | Tag name |

## Functions
LIST
* GTM_ACCOUNT_LIST
* * GTM_CONTAINER_LIST(accountPath)
* * * GTM_WORKSPACE_LIST(containerPath)
* * * * GTM_TAGS_LIST(workspacePath)
* * * * GTM_VARIABLES_LIST(workspacePath)
* * * * GTM_TRIGGERS_LIST(workspacePath)
* * * * GTM_FOLDER_LIST(workspacePath)
* * * * GTM_ITEMS_LIST(workspacePath) 

GTM_NOTES_LIST(workspacePath) - returns item [name, path, type, notes]

GTM_COPY(itemPath, to_workspacePath) - copy item to another workspace
GTM_FOLDER_COPY(folderPath, to_workspacePath) - copy foleder with items to another workspace. Breaks if item name exist at acceptor workspace.

GTM_RENAME(itemPath, name) - rename item


GTM_WORKSPACE_LIST_ALL - return all accounts, containers and workspaces
GTM_TAGS_ANALYTICS - return all analytics tags

GTM_NOTES_ADD(itemPath, notes) - create/update notes for item

