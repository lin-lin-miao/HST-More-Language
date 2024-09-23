# Calculator Plugin

This plugin allows you to extend the application using JavaScript.

## Custom Prompt(), Confirm(), and Alert()

Usage fields: `js/:title=Custom Title/:msg=Custom Message`

Invoke the field: `js/:`, with `/:` as the separator.

Other fields besides `js/:` can be unordered.

If not used, default titles will apply.

## API Calls

Not fully implemented yet, and may change in the future. For additional needs, you can submit an issue at [Issues](https://github.com/lin-lin-miao/HST-More-Language/issues) or contact the author.

### Using Reflection Mechanism

By default, there is no return value.

The reflection class name is: `android`.

Example call:

```javascript
android.Toast(strs);
```

|Function Name|Result|
|--|--|
|Toast(String msg)|Same as app Toast|
|permission(String msg, String value)|Sets plugin permissions; `msg` is the function name, `value` is the setting value|

Available `permission` functions:

- setAppCacheEnabled
- setAppCachePath
- setDatabaseEnabled
- setJavaScriptCanOpenWindowsAutomatically
- setAllowUniversalAccessFromFileURLs

### Using the Prompt() Function

Has a return value.

Example call:

```javascript
prompt("js/:api=i18n/:mes=Calculator")
```

The `api` value is the function name to call.

If there is no `api` value, it acts as a custom input box.

Some APIs may require permissions.

Call values can be unordered.

If the execution fails, `defaultValue` is returned.

|Function Name|Required Parameters|Return Value|Result|
|--|--|--|--|
|i18n|msg=String|String|Translates using the app's loaded translation file|
|name|null|String|Returns plugin name|
|version|null|String|Returns app version|
|path|null|URI|Returns the plugin directory|
|open|msg=Url|boolean|Opens a URL directly with user consent, `true` if agreed, `false` if failed|
|StartStartup|msg=String|String(0/1)|Sets app to run at startup|
|isStartStartup|null|String(0/1)|Checks if the app runs at startup|
|inStartStartup|null|String(0/1)|Checks if it's running at startup|
|exit|null|null|Exits the app|
|CanTrust|msg=String|String(0/1)|Sets permissions contained in the `msg`|
|getCanTrust|null|String|Returns the permissions string|
|readData|path=String|String|Returns saved string|
|writeData|path=String|String(0/1)|Saves a string|
|getChangeCounter|null|String(JSON)|Gets usage data, returns JSON string, requires `UsageSituation` permission|
|up_accountList|null|String(0/1)|Returns the upper-level list, requires `UsageSituation` permission|
|set_accountList|path=String|String(0/1)|Enters sub-directory, requires `UsageSituation` permission|
|getAccountDir|null|String(JSON)|Gets current directory list, requires `UsageSituation` permission|
|getAccount|null|String(JSON)|Gets current account list, requires `UsageSituation` permission|
|change_account|path=String|String(0/1)|Switches accounts in the list, requires `UsageSituation` permission|

#### API Permissions

To obtain permissions:

```javascript
prompt("js/:api=CanTrust/:msg=Permission String")
```

When calling an API, the system will check if the `Permission String` contains the required permissions.

If permissions are lacking, the return will be a String:

```
    android/:api=(Called API)/:noCanTrust=(Missing Permission String)
```