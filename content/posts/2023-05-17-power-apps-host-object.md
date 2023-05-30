---
title: "Power Apps Host Object"
subtitle: Get information about the current host running a Power App
date: 2023-05-17
tags: ["PowerApps"]
---

## The Power Apps Host object

The new *Host* object in Power Apps provides information about the current host running the app.

|![Power Apps Host object.](/img/2023-05-17-power-apps-host-object/power-apps-host-object.png "Power Apps Host object.")|
|-|

The Host object does not have any properties that accept formulas but you can call functions against it to retrieve the following information:

- **BrowserUserAgent**: The complete user agent string that the browser uses to identify itself when running the app

- **OSType**: The name of the operating system where the app is running

- **SessionID**: The Globally Unique Identifier (GUID) that identifies the current session

- **TenantID**: The Globally Unique Identifier (GUID) that specifies the Azure Active Directory (AAD) tenant associated with the presently authenticated user

For example, place the following code into a Text label control Text property...

```
$"Host.BrowserUserAgent: {Host.BrowserUserAgent}

Host.OSType: {Host.OSType}

Host.SessionID: {Host.SessionID}

Host.TenantID: {Host.TenantID}"
```

...to view output similar to the following in the app:

|![Power Apps Host object output.](/img/2023-05-17-power-apps-host-object/power-apps-host-object-output.png "Power Apps Host object output.")|
|-|

## How it can be useful

This information could be useful to know if you're supporting a Power App and an issue is reported.

For example, several users report the same issue with a Power App and, by knowing this information, you determine that the issue occurs only for users using a certain browser version.

This information could be displayed on screen and / or emailed to an app support email address.

## Providing more information to support

To provide even more information to support, consider using the Power Apps [User function](https://learn.microsoft.com/en-us/power-platform/power-fx/reference/function-user) like this...

```
$"User().FullName: {User().FullName}

User().Email: {User().Email}"
```

...to view output similar to the following in the app:

|![Power Apps User function output.](/img/2023-05-17-power-apps-host-object/power-apps-user-function-output.png "Power Apps User function output.")|
|-|

And also the [Office 365 Users connection](https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/connections/connection-office365-users) like this...

```
$"Office365Users.MyProfile().DisplayName: {Office365Users.MyProfile().DisplayName}

Office365Users.MyProfile().JobTitle: {Office365Users.MyProfile().JobTitle}

Office365Users.MyProfile().Department: {Office365Users.MyProfile().Department}"
```

...to view output similar to the following in the app:

|![Power Apps Office 365 Users connection output.](/img/2023-05-17-power-apps-host-object/power-apps-office-365-users-connection-output.png "Power Apps Office 365 Users connection output.")|
|-|

## More information

More info on the Power Apps *Host" object here: https://learn.microsoft.com/en-us/power-platform/power-fx/reference/object-host