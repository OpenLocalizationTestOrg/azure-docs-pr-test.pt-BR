---
title: aaaConfigure um Host do Docker com VirtualBox | Microsoft Docs
description: "Instruções passo a passo tooconfigure padrão Docker instância usando o Docker máquina e VirtualBox"
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
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="06bbe-103">Configurar um host do Docker com o VirtualBox</span><span class="sxs-lookup"><span data-stu-id="06bbe-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="06bbe-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="06bbe-104">Overview</span></span>
<span data-ttu-id="06bbe-105">Este artigo orienta você pela configuração de uma instância de Docker padrão usando a máquina Docker e o VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="06bbe-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="06bbe-106">Se você estiver usando Olá [beta do Docker para Windows](http://beta.docker.com/), essa configuração não é necessária.</span><span class="sxs-lookup"><span data-stu-id="06bbe-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06bbe-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="06bbe-107">Prerequisites</span></span>
<span data-ttu-id="06bbe-108">Olá seguintes ferramentas necessário toobe instalado.</span><span class="sxs-lookup"><span data-stu-id="06bbe-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="06bbe-109">Caixa de Ferramentas do Docker</span><span class="sxs-lookup"><span data-stu-id="06bbe-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="06bbe-110">Configurando o cliente do Docker Olá com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="06bbe-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="06bbe-111">tooconfigure um cliente do Docker, simplesmente abra o Windows PowerShell e realize Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="06bbe-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="06bbe-112">Crie uma instância de host do docker padrão.</span><span class="sxs-lookup"><span data-stu-id="06bbe-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="06bbe-113">Verifique se a instância padrão de saudação está configurado e em execução.</span><span class="sxs-lookup"><span data-stu-id="06bbe-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="06bbe-114">(Você deve ver uma instância chamada “padrão” em execução.</span><span class="sxs-lookup"><span data-stu-id="06bbe-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![saída do docker-machine Is][0]
3. <span data-ttu-id="06bbe-116">Defina o padrão como host atual hello e configure o shell.</span><span class="sxs-lookup"><span data-stu-id="06bbe-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="06bbe-117">Exiba contêineres do Docker active hello.</span><span class="sxs-lookup"><span data-stu-id="06bbe-117">Display hello active Docker containers.</span></span> <span data-ttu-id="06bbe-118">Olá lista deve estar vazia.</span><span class="sxs-lookup"><span data-stu-id="06bbe-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![saída do docker ps][1]

> [!NOTE]
> <span data-ttu-id="06bbe-120">Cada vez que você reinicializa o computador de desenvolvimento, você precisará toorestart seu host do docker local.</span><span class="sxs-lookup"><span data-stu-id="06bbe-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="06bbe-121">toodo, Olá problema comando no prompt de comando a seguir: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="06bbe-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
