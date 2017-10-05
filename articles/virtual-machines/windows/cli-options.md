---
title: "Utilização da CLI do Azure no Windows | Microsoft Docs"
description: "Utilização da CLI do Azure no Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: be02ad0d7752cb08f092deeb5a86dcd126403237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-on-windows"></a><span data-ttu-id="e163a-103">Utilização da CLI do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="e163a-103">Using the Azure CLI on Windows</span></span>

<span data-ttu-id="e163a-104">A Interface de linha de comando (CLI) do Azure fornece um ambiente de script e linha de comando para criar e gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e163a-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="e163a-105">A CLI do Azure está disponível para os sistemas operacionais macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="e163a-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="e163a-106">Entre esses sistemas operacionais, os comandos da CLI são idênticos, mas a sintaxe de script específica do sistema operacional pode ser diferente.</span><span class="sxs-lookup"><span data-stu-id="e163a-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="e163a-107">Este documento explica em detalhes como a CLI do Azure pode ser instalada e executada no Windows e fornece considerações minuciosas acerca da sintaxe de cada um.</span><span class="sxs-lookup"><span data-stu-id="e163a-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="e163a-108">Para ler a documentação detalhada da CLI do Azure, confira a [Documentação da CLI do Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e163a-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="e163a-109">Subsistema do Windows para Linux</span><span class="sxs-lookup"><span data-stu-id="e163a-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="e163a-110">O WSL (subsistema do Windows para Linux) fornece um ambiente Ubuntu Linux na edição de aniversário do Windows 10 e edições posteriores.</span><span class="sxs-lookup"><span data-stu-id="e163a-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="e163a-111">Quando habilitado, o WSL fornece uma experiência de Bash nativa, que pode ser usada para criar e executar scripts da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e163a-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="e163a-112">Como o WSL fornece uma experiência de Bash nativa, os scripts da CLI do Azure podem ser compartilhados entre o macOS, Linux e Windows sem modificação.</span><span class="sxs-lookup"><span data-stu-id="e163a-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="e163a-113">Siga as seguintes etapas para usar a CLI do Azure em WSL.</span><span class="sxs-lookup"><span data-stu-id="e163a-113">To use the Azure CLI in WSL, complete the following.</span></span>

|<span data-ttu-id="e163a-114">Tarefa</span><span class="sxs-lookup"><span data-stu-id="e163a-114">Task</span></span> | <span data-ttu-id="e163a-115">Instruções</span><span class="sxs-lookup"><span data-stu-id="e163a-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="e163a-116">Habilitar WSL</span><span class="sxs-lookup"><span data-stu-id="e163a-116">Enable WSL</span></span> | [<span data-ttu-id="e163a-117">Como instalar a documentação de WSL</span><span class="sxs-lookup"><span data-stu-id="e163a-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="e163a-118">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e163a-118">Install the Azure CLI</span></span> |[<span data-ttu-id="e163a-119">Como instalar a CLI no WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="e163a-119">Install the CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="e163a-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e163a-120">PowerShell</span></span>

<span data-ttu-id="e163a-121">A CLI do Azure pode ser executada nativamente no Windows.</span><span class="sxs-lookup"><span data-stu-id="e163a-121">The Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="e163a-122">Nessa configuração, o pacote da CLI do Azure é instalado no sistema operacional Windows e os comandos podem ser executados a partir do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e163a-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="e163a-123">Nessa configuração, os scripts e os comandos da CLI do Azure podem ser executados em qualquer versão com suporte do Windows, porém você precisará da sintaxe de script específica da plataforma.</span><span class="sxs-lookup"><span data-stu-id="e163a-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="e163a-124">Por isso, scripts não podem ser necessariamente compartilhados entre macOS, Linux e Windows sem modificação.</span><span class="sxs-lookup"><span data-stu-id="e163a-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="e163a-125">Siga essas instruções para usar a CLI do Azure no Windows: [Como instalar a CLI no Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="e163a-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="e163a-126">Imagem de Docker</span><span class="sxs-lookup"><span data-stu-id="e163a-126">Docker Image</span></span>

<span data-ttu-id="e163a-127">Ao usar o Docker para Windows, uma imagem de Docker, que inclui a CLI do Azure, pode ser iniciada.</span><span class="sxs-lookup"><span data-stu-id="e163a-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span></span> <span data-ttu-id="e163a-128">Essa imagem se baseia no Linux e inclui uma experiência de bash nativa.</span><span class="sxs-lookup"><span data-stu-id="e163a-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="e163a-129">Ao usar o Docker para Windows e a imagem da CLI do Azure, os scripts são compartilhados entre o macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="e163a-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="e163a-130">Para usar a CLI do Azure no Docker para Windows, confira se o Docker para Windows está em execução e execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="e163a-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="e163a-131">Depois de concluído, uma sessão Bash pré-carregada com as ferramentas da CLI do Azure será iniciada.</span><span class="sxs-lookup"><span data-stu-id="e163a-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e163a-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e163a-132">Next Steps</span></span>

[<span data-ttu-id="e163a-133">Amostra de CLI para máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="e163a-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="e163a-134">Amostras de CLI para aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="e163a-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="e163a-135">Amostras de CLI para Azure SQL</span><span class="sxs-lookup"><span data-stu-id="e163a-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
