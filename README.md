# lazy-jack-vscode
# Vscode viewWelcome

```
    "viewsWelcome": [
      {
        "view": "fast-repo-gui",
        "contents": "Open github Repository \n[Open](command:command_open_github_repo)\n[Actions](command:command_open_github_actions)\n[Wiki](command:command_open_github_wiki)\nOpen local sourcetree\n[Open](command:command_open_sourcetree_local_repo)"
      }
    ],
```
* 每個按鍵要會發出一個命令
* 設定命令行為
    ``` typescript
    export function registerFastGithubCmd(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand(command_open_github_repo, async () => {
        openGitHubBrowserAction(context, "repo");
    }));
    context.subscriptions.push(vscode.commands.registerCommand(command_open_github_actions, async () => {
        openGitHubBrowserAction(context, "actions");
    }));
    context.subscriptions.push(vscode.commands.registerCommand(command_open_github_wiki, async () => {
        openGitHubBrowserAction(context, "wiki");
    }));
    context.subscriptions.push(vscode.commands.registerCommand(command_open_sourcetree_local_repo, async () => {
        terminal_util.runTerminal("open -a SourceTree ./")
    }));
    }

    ```

# Vscode sideBar
  * package.json
    * activitybar 為左側欄位
    * views 點選後工作區會顯示的內容
    * 一個view可以有多個tree
    * 注意viewsContainers的id要與views的id相同
    * 每個 activitybarId會對應一個 dataProviderId 
        * [Utils/BaseTreeDataProvider](/packages//lazy_jack_vscode_utils/README.md#sidebar)
  
  ```
    {
        "name": "name",
        "contributes": {
            "viewsContainers": {
                "activitybar": [
                    {
                    "id": "activitybarId",
                    "title": "name",
                    "icon": "images/icon.png"
                    }
                ]
            },
            "views": {
                "activitybarId": [
                    {
                    "id": "dataProviderId",
                    "name": "name",
                    }
                ]
            }
        }  
      
    }

    ```