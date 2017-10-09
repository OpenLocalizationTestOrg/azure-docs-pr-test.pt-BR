---
title: "aaaDeploy um host remoto Docker ASP.NET Core Linux Docker contêiner tooa | Microsoft Docs"
description: "Saiba como toouse Visual Studio Tools para Docker toodeploy um núcleo de ASP.NET web contêiner de Docker tooa de aplicativo em execução em uma VM Linux do Host do Docker do Azure"
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a>Implantar um host remoto Docker ASP.NET contêiner tooa
## <a name="overview"></a>Visão geral
Docker é um mecanismo de contêiner leve, semelhante em alguma máquina virtual de tooa maneiras que você pode usar toohost aplicativos e serviços.
Este tutorial orienta você pelas usando Olá [Visual Studio Tools para Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extensão toodeploy um host do ASP.NET Core aplicativo tooa Docker no Azure usando o PowerShell.

## <a name="prerequisites"></a>Pré-requisitos
a seguir Olá é necessário toocomplete este tutorial:

* Crie uma VM do Host do Docker do Azure conforme descrito em [como toouse docker-máquina com o Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Instalar a versão mais recente de saudação do [Visual Studio](https://www.visualstudio.com/downloads/)
* Baixar Olá [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)
* Instalar o [Docker para Windows](https://docs.docker.com/docker-for-windows/install/)

## <a name="1-create-an-aspnet-core-web-app"></a>1. Criar um aplicativo Web ASP.NET Core
Olá etapas a seguir orientam você na criação de um aplicativo ASP.NET Core básico que será usado neste tutorial.

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Adicionar suporte ao Docker
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a>3. Use Olá DockerTask.ps1 Script do PowerShell
1. Abra um diretório do PowerShell prompt toohello raiz do projeto. 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. Validar o host remoto hello está em execução. Você deve ver o estado = Em execução 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. Usando o aplicativo hello compilação Olá - parâmetro de compilação
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. Executar o aplicativo hello, usando Olá - parâmetro de execução
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   Após a conclusão do docker, verá resultados semelhantes toohello seguinte:
   
   ![Exibir aplicativo][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
