---
title: "Olá aaaUsing CLI do Azure no Windows | Microsoft Docs"
description: Usando o hello CLI do Azure no Windows
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
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="2dfc8-103">Usando o hello CLI do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="2dfc8-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="2dfc8-104">Hello Azure Interface de linha de comando (CLI) fornece um ambiente de script para criar e gerenciar recursos do Azure e a linha de comando.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="2dfc8-105">Olá CLI do Azure está disponível para sistemas operacionais Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="2dfc8-106">Entre esses sistemas operacionais, comandos CLI Olá são idênticos, no entanto, sintaxe de script específicas do sistema operacional pode ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="2dfc8-107">Estes documento detalhes Olá maneiras Olá CLI do Azure podem ser instaladas e executadas em Windows e os detalhes de sintáticas considerações para cada.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="2dfc8-108">Para ler a documentação detalhada da CLI do Azure, confira a [Documentação da CLI do Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2dfc8-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="2dfc8-109">Subsistema do Windows para Linux</span><span class="sxs-lookup"><span data-stu-id="2dfc8-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="2dfc8-110">Olá subsistema do Windows para Linux (WSL) fornece um ambiente de Ubuntu Linux no Windows 10 aniversário e edições posteriores.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="2dfc8-111">Quando habilitado, o WSL fornece uma experiência de Bash nativa, que pode ser usada para criar e executar scripts da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="2dfc8-112">Como o WSL fornece uma experiência de Bash nativa, os scripts da CLI do Azure podem ser compartilhados entre o macOS, Linux e Windows sem modificação.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="2dfc8-113">Olá toouse CLI do Azure no WSL, execute o seguinte de hello.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="2dfc8-114">Tarefa</span><span class="sxs-lookup"><span data-stu-id="2dfc8-114">Task</span></span> | <span data-ttu-id="2dfc8-115">Instruções</span><span class="sxs-lookup"><span data-stu-id="2dfc8-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="2dfc8-116">Habilitar WSL</span><span class="sxs-lookup"><span data-stu-id="2dfc8-116">Enable WSL</span></span> | [<span data-ttu-id="2dfc8-117">Como instalar a documentação de WSL</span><span class="sxs-lookup"><span data-stu-id="2dfc8-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="2dfc8-118">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2dfc8-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="2dfc8-119">Instalar Olá CLI em WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="2dfc8-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="2dfc8-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dfc8-120">PowerShell</span></span>

<span data-ttu-id="2dfc8-121">Olá CLI do Azure pode ser executado nativamente no Windows.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="2dfc8-122">Nessa configuração, pacote de CLI do Azure hello está instalado no sistema de operacional do Windows hello e podem ser executados comandos do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="2dfc8-123">Nessa configuração, os scripts e os comandos da CLI do Azure podem ser executados em qualquer versão com suporte do Windows, porém você precisará da sintaxe de script específica da plataforma.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="2dfc8-124">Por isso, scripts não podem ser necessariamente compartilhados entre macOS, Linux e Windows sem modificação.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="2dfc8-125">Olá toouse CLI do Azure no Windows, instale o pacote de saudação usando estas instruções, [instalação Olá CLI em Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="2dfc8-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="2dfc8-126">Imagem de Docker</span><span class="sxs-lookup"><span data-stu-id="2dfc8-126">Docker Image</span></span>

<span data-ttu-id="2dfc8-127">Ao usar o Docker para Windows, uma imagem do Docker pode ser que inclui Olá CLI do Azure iniciada.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="2dfc8-128">Essa imagem se baseia no Linux e inclui uma experiência de bash nativa.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="2dfc8-129">Ao usar o Docker para Windows e imagem de CLI do Azure hello, toobe scripts compartilhados entre macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="2dfc8-130">Olá toouse CLI do Azure no Docker para Windows, garantir que o Docker para Windows está em execução e execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="2dfc8-131">Depois de concluído, um Bash sessão será iniciado ou seja pré-carregados com ferramentas de CLI do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2dfc8-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dfc8-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2dfc8-132">Next Steps</span></span>

[<span data-ttu-id="2dfc8-133">Amostra de CLI para máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="2dfc8-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="2dfc8-134">Amostras de CLI para aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="2dfc8-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="2dfc8-135">Amostras de CLI para Azure SQL</span><span class="sxs-lookup"><span data-stu-id="2dfc8-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
