---
title: Windows Containers on Windows Server
description: Container deployment quick start
keywords: docker, containers
author: enderb-ms
ms.date: 09/26/2016
ms.topic: article
ms.prod: windows-containers
ms.service: windows-containers
ms.assetid: e3b2a4dc-9082-4de3-9c95-5d516c03482b
---

# Windows Containers on Windows Server

This exercise walks through basic deployment and use of the Windows container feature on Windows Server 2016. During this exercise, you install the container role and deploy a simple Windows Server container. Before starting this quick start, familiarize yourself with basic container concepts and terminology. You can find this information in the [Quick Start Introduction](./index.md).

This quick start is specific to Windows Server containers on Windows Server 2016. Additional quick start documentation, including containers in Windows 10, are found in the table of contents on the left hand side of this page.

**Prerequisites:**

One computer system (physical or virtual) running Windows Server 2016. If you are using Windows Server 2016 TP5, please update to [Window Server 2016 Evaluation](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 ). 

> Critical updates are needed in order for the Windows Container feature to function. Please install all updates before working through this tutorial.

If you would like to deploy on Azure, this [template](https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-tools/containers-azure-template) makes it easy.<br/>
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2FVirtualization-Documentation%2Fmaster%2Fwindows-server-container-tools%2Fcontainers-azure-template%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>


## 1. Install Docker

To install Docker we'll use the [OneGet provider PowerShell module](https://github.com/oneget/oneget). The provider enables the containers feature on your machine. You also install Docker which requires a reboot. Docker is required in order to work with Windows containers. It consists of the Docker Engine and the Docker client.

Open an elevated PowerShell session and run the following commands.

First install the OneGet PowerShell module.

```none
Install-Module -Name DockerMsftProvider -Repository PSGallery -Force
```

Next you use OneGet to install the latest version of Docker.
```none
Install-Package -Name docker -ProviderName DockerMsftProvider
```

When PowerShell asks you whether to trust the package source 'DockerDefault', type A to continue the installation. When the installation is complete, reboot the computer.

```none
Restart-Computer -Force
```

## 2. Install Windows Updates

Ensure your Windows Server system is up-to-date by running:

```none
sconfig
```

This shows a text-based configuration menu, where you can choose option 6 to Download and Install Updates:

```none
===============================================================================
                         Server Configuration
===============================================================================

1) Domain/Workgroup:                    Workgroup:  WORKGROUP
2) Computer Name:                       WIN-HEFDK4V68M5
3) Add Local Administrator
4) Configure Remote Management          Enabled

5) Windows Update Settings:             DownloadOnly
6) Download and Install Updates
7) Remote Desktop:                      Disabled
...
```

When prompted, choose option A to download all updates.

## 3. Deploy Your First Container

For this exercise, you download a pre-created .NET sample image from the Docker Hub registry and deploy a simple container running a .Net Hello World application.  

Use `docker run` to deploy the .Net container. This will also download the container image which may take a few minutes.

```console
docker run microsoft/dotnet-samples:dotnetapp-nanoserver
```

The container starts, prints the hello world message, and then exits.

```console
         Dotnet-bot: Welcome to using .NET Core!
    __________________
                      \
                       \
                          ....
                          ....'
                           ....
                        ..........
                    .............'..'..
                 ................'..'.....
               .......'..........'..'..'....
              ........'..........'..'..'.....
             .'....'..'..........'..'.......'.
             .'..................'...   ......
             .  ......'.........         .....
             .                           ......
            ..    .            ..        ......
           ....       .                 .......
           ......  .......          ............
            ................  ......................
            ........................'................
           ......................'..'......    .......
        .........................'..'.....       .......
     ........    ..'.............'..'....      ..........
   ..'..'...      ...............'.......      ..........
  ...'......     ...... ..........  ......         .......
 ...........   .......              ........        ......
.......        '...'.'.              '.'.'.'         ....
.......       .....'..               ..'.....
   ..       ..........               ..'........
          ............               ..............
         .............               '..............
        ...........'..              .'.'............
       ...............              .'.'.............
      .............'..               ..'..'...........
      ...............                 .'..............
       .........                        ..............
        .....


**Environment**
Platform: .NET Core 1.0
OS: Microsoft Windows 10.0.14393
```

For in depth information on the Docker Run command, see [Docker Run Reference on Docker.com]( https://docs.docker.com/engine/reference/run/).

## Next Steps

[Container Images on Windows Server](./quick-start-images.md)

[Windows Containers on Windows 10](./quick-start-windows-10.md)
