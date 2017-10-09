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
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a><span data-ttu-id="a4a18-103">Implantar um host remoto Docker ASP.NET contêiner tooa</span><span class="sxs-lookup"><span data-stu-id="a4a18-103">Deploy an ASP.NET container tooa remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="a4a18-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a4a18-104">Overview</span></span>
<span data-ttu-id="a4a18-105">Docker é um mecanismo de contêiner leve, semelhante em alguma máquina virtual de tooa maneiras que você pode usar toohost aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="a4a18-105">Docker is a lightweight container engine, similar in some ways tooa virtual machine, which you can use toohost applications and services.</span></span>
<span data-ttu-id="a4a18-106">Este tutorial orienta você pelas usando Olá [Visual Studio Tools para Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extensão toodeploy um host do ASP.NET Core aplicativo tooa Docker no Azure usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4a18-106">This tutorial walks you through using hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy an ASP.NET Core app tooa Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4a18-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a4a18-107">Prerequisites</span></span>
<span data-ttu-id="a4a18-108">a seguir Olá é necessário toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="a4a18-108">hello following is required toocomplete this tutorial:</span></span>

* <span data-ttu-id="a4a18-109">Crie uma VM do Host do Docker do Azure conforme descrito em [como toouse docker-máquina com o Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a4a18-109">Create an Azure Docker Host VM as described in [How toouse docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="a4a18-110">Instalar a versão mais recente de saudação do [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="a4a18-110">Install hello latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="a4a18-111">Baixar Olá [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="a4a18-111">Download hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="a4a18-112">Instalar o [Docker para Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="a4a18-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="a4a18-113">1. Criar um aplicativo Web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a4a18-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="a4a18-114">Olá etapas a seguir orientam você na criação de um aplicativo ASP.NET Core básico que será usado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a4a18-114">hello following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="a4a18-115">2. Adicionar suporte ao Docker</span><span class="sxs-lookup"><span data-stu-id="a4a18-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a><span data-ttu-id="a4a18-116">3. Use Olá DockerTask.ps1 Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4a18-116">3. Use hello DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="a4a18-117">Abra um diretório do PowerShell prompt toohello raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="a4a18-117">Open a PowerShell prompt toohello root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="a4a18-118">Validar o host remoto hello está em execução.</span><span class="sxs-lookup"><span data-stu-id="a4a18-118">Validate hello remote host is running.</span></span> <span data-ttu-id="a4a18-119">Você deve ver o estado = Em execução</span><span class="sxs-lookup"><span data-stu-id="a4a18-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="a4a18-120">Usando o aplicativo hello compilação Olá - parâmetro de compilação</span><span class="sxs-lookup"><span data-stu-id="a4a18-120">Build hello app using hello -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="a4a18-121">Executar o aplicativo hello, usando Olá - parâmetro de execução</span><span class="sxs-lookup"><span data-stu-id="a4a18-121">Run hello app, using hello -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="a4a18-122">Após a conclusão do docker, verá resultados semelhantes toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="a4a18-122">Once docker completes, you should see results similar toohello following:</span></span>
   
   ![Exibir aplicativo][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
