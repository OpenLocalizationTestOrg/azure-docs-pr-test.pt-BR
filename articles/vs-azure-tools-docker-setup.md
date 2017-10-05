---
title: Configurar um host do Docker com o VirtualBox | Microsoft Docs
description: "Instruções passo a passo para configurar uma instância de Docker padrão usando a máquina Docker e o VirtualBox"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: e9465afb560a73d74f853c19094b3ee75b8c470c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="4994b-103">Configurar um host do Docker com o VirtualBox</span><span class="sxs-lookup"><span data-stu-id="4994b-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="4994b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4994b-104">Overview</span></span>
<span data-ttu-id="4994b-105">Este artigo orienta você pela configuração de uma instância de Docker padrão usando a máquina Docker e o VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="4994b-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="4994b-106">Se você estiver usando o [Docker para Windows beta](http://beta.docker.com/), essa configuração não é necessária.</span><span class="sxs-lookup"><span data-stu-id="4994b-106">If you’re using the [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4994b-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4994b-107">Prerequisites</span></span>
<span data-ttu-id="4994b-108">As ferramentas a seguir precisam ser instaladas.</span><span class="sxs-lookup"><span data-stu-id="4994b-108">The following tools need to be installed.</span></span>

* [<span data-ttu-id="4994b-109">Caixa de Ferramentas do Docker</span><span class="sxs-lookup"><span data-stu-id="4994b-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-the-docker-client-with-windows-powershell"></a><span data-ttu-id="4994b-110">Configurando o cliente Docker com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4994b-110">Configuring the Docker client with Windows PowerShell</span></span>
<span data-ttu-id="4994b-111">Para configurar um cliente Docker, apenas abra o Windows PowerShell e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4994b-111">To configure a Docker client, simply open Windows PowerShell, and perform the following steps:</span></span>

1. <span data-ttu-id="4994b-112">Crie uma instância de host do docker padrão.</span><span class="sxs-lookup"><span data-stu-id="4994b-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="4994b-113">Verifique se a instância padrão está configurada e em execução.</span><span class="sxs-lookup"><span data-stu-id="4994b-113">Verify the default instance is configured and running.</span></span> <span data-ttu-id="4994b-114">(Você deve ver uma instância chamada “padrão” em execução.</span><span class="sxs-lookup"><span data-stu-id="4994b-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![saída do docker-machine Is][0]
3. <span data-ttu-id="4994b-116">Defina o padrão como o host atual e configure seu shell.</span><span class="sxs-lookup"><span data-stu-id="4994b-116">Set default as the current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="4994b-117">Exiba os contêineres do Docker ativo.</span><span class="sxs-lookup"><span data-stu-id="4994b-117">Display the active Docker containers.</span></span> <span data-ttu-id="4994b-118">A lista deve estar vazia.</span><span class="sxs-lookup"><span data-stu-id="4994b-118">The list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![saída do docker ps][1]

> [!NOTE]
> <span data-ttu-id="4994b-120">Sempre que você reinicializar o computador de desenvolvimento, precisará reiniciar o host do Docker local.</span><span class="sxs-lookup"><span data-stu-id="4994b-120">Each time you reboot your development machine, you’ll need to restart your local docker host.</span></span>
> <span data-ttu-id="4994b-121">Para fazer isso, envie o seguinte comando em um prompt de comando: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="4994b-121">To do this, issue the following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
