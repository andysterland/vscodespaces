---
author: andster
ms.author: andster
ms.prod: visual-studio-family
ms.technology: visual-studio-codespaces
title: Configuring Windows Instance Types in Codespaces
ms.topic: reference
ms.date: 05/13/2020
---

# Configuring Windows Codespaces

>[!IMPORTANT]
> This document refers to capabilities in the private preview of Visual Studio environments for Codespaces. The Windows instance type and Visual Studio capabilities aren't publicly available and are only available in a private preview. If you're interested in taking part in the preview we'd love for you to [sign up for the private preview of Visual Studio for Codespaces](https://aka.ms/vsfutures-signup).

This document details the capabilities of Windows based Codespace environment for Visual Studio 2019. To get started with the Visual Studio Codespaces take a look at the [Visual Studio Codespaces quick start](../quickstarts/vs.md). We would love to hear you feedback on the customizations (such as applications, features and settings) that you need to be successful using a Windows Codespace environment. If you would like to provide feedback and take part in future customer research please complete this [survey]( https://www.research.net/r/WXGB6N5).

During the private preview Windows instance types for Codespaces will have limited support for customizations via `devcontainer.json`. Specifically the following customizations from `devcontainer.json` are supported:

- VS Code and Web Editor extensions via `extensions`
- VS Code and Web Editor settings via `settings`
- Port forwarding via `forwardPorts` and `appPort`

 More information how to use these properties can be found in the [Configuring Codespaces](configuring.md#codespaces-configuration-reference) documentation.

 The Windows instance types come with a range of already configured components, as listed below. If further customizations are needed you can use the Visual Studio Terminal, which is running PowerShell elevated under the local administrator account. To learn more about the Visual Studio terminal, see the [Visual Studio Terminal announcement blog](https://devblogs.microsoft.com/visualstudio/say-hello-to-the-new-visual-studio-terminal/).

## Installed software

The table below lists the applications and features available in all Windows Codespace environments.

| App                                         | Path Alias | Version            |
|---------------------------------------------|------------|--------------------|
| .NET                                        | N/A        | 4.8                |
| .NET Core Runtime                           | dotnet     | 2.1, 3.1           |
| .NET Core SDK                               | dotnet     | 2.1, 3.1.3, 3.1.4  |
| Azure CLI                                   | az         | 2.5                |
| Chocolatey                                  | choco      | 0.10.15            |
| CMake                                       | cmake      | 3.17               |
| Docker Desktop                              | docker     | 19.03              |
| Git                                         | git        | 2.26               |
| Microsoft build                             | msbuild    | 16.7               |
| Microsoft SQL Server Express Edition 2019   | N/A        | 15.0               |
| Ninja                                       | ninja      | 1.8.2              |
| Node.js                                     | node       | 12.16              |
| NPM                                         | npm        | 6.14               |
| Python                                      | python     | 3.7                |
| VC Package Manager                          | vcpkg      | 2020.02            |
| Windows SDK                                 | N/A        | 10.0.18362         |

The list above is not exhaustive and excludes many tools that Visual Studio installs (e.g. IISExpress). A component may also have a different minor or patch version than the one stated above.

## Microsoft SQL Server

Microsoft SQL Server Express Edition (localdb) is available in the Windows Codespace environment. The current user, which your app and the Visual Studio Terminal run as, has SQL administrator rights to the SQL server. To administer the server you will need to use PowerShell in the Visual Studio Terminal or other command line tools such as `dotnet-ef`. Currently SQL Server Management Studio and other remote administration tools are not available.

### Example connection string

The below is an example of a connection string to connect to the local MS SQL server.

```csharp
"Server=localhost;Integrated Security=true;"
```

## Docker desktop

Docker desktop is installed in all Windows Codespace environment. However, the docker tools for Visual Studio are currently not available in Visual Studio Codespaces.

## Azure CLI

The Azure CLI is installed in all Windows Codespace environments and is available on path as `az`.

### Using Azure resources

If you are using an Azure Active Directory (AAD) identity to authenticate your application against Azure resources, you will need to use first login to Azure from the Visual Studio terminal. To do this use the Azure CLI login command with the device login flow (as shown in the example below). Once logged in your application and terminal session should be able to use that identity.

```powershell
> az login --use-device-code
```

You can learn more on the `az login` command in the Azure CLI [documentation](/cli/azure/reference-index?view=azure-cli-latest#az-login).
