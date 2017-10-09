---
title: "Connect Raspberry PI (C) tooAzure IoT - lição 1: obter ferramentas (Windows) | Microsoft Docs"
description: "Baixe e instale as ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Pi no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no windows, instalar node js no windows, installar o npm no windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 70ae6d15f9d6af116ff065a79a30d99afc67bffd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="7f3e7-104">Obter ferramentas hello (Windows 7 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="7f3e7-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f3e7-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="7f3e7-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="7f3e7-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="7f3e7-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="7f3e7-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="7f3e7-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="7f3e7-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="7f3e7-108">What you will do</span></span>
<span data-ttu-id="7f3e7-109">Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="7f3e7-110">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7f3e7-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7f3e7-111">Embora Olá linguagem da lógica principal Olá de programação C, Node. js ferramentas são usadas em dispositivos de toodiscover de lições Olá e criar e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7f3e7-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7f3e7-112">What you will learn</span></span>
<span data-ttu-id="7f3e7-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="7f3e7-113">In this article, you will learn:</span></span>

* <span data-ttu-id="7f3e7-114">Como tooinstall Node. js e Git.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="7f3e7-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="7f3e7-116">aplicativo de exemplo Hello para este artigo é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="7f3e7-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="7f3e7-118">Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="7f3e7-119">requisito de versão mínima de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="7f3e7-120">[NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7f3e7-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7f3e7-121">What you need</span></span>

<span data-ttu-id="7f3e7-122">toocomplete essa operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="7f3e7-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="7f3e7-123">Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="7f3e7-124">Um computador que esteja executando o Windows.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="7f3e7-125">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="7f3e7-125">Install Git and Node.js</span></span>

<span data-ttu-id="7f3e7-126">Clicar em links de saudação abaixo toodownload e instale o Git e LTS Node. js para Windows.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="7f3e7-127">Obtenha o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="7f3e7-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="7f3e7-128">Obtenha o Node.js LTS para o Windows</span><span class="sxs-lookup"><span data-stu-id="7f3e7-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="7f3e7-129">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="7f3e7-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="7f3e7-130">Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooPi de aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="7f3e7-131">Saudação de uso [cli de descoberta do dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve informações de rede sobre os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-131">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="7f3e7-132">Inicie um prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="7f3e7-133">Instalar `gulp` e `device-discovery-cli` executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f3e7-133">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="7f3e7-134">Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento Node. js adicionais no seu computador, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="7f3e7-135">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7f3e7-135">Install Visual Studio Code</span></span>

<span data-ttu-id="7f3e7-136">[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="7f3e7-137">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="7f3e7-138">Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="7f3e7-139">Resumo</span><span class="sxs-lookup"><span data-stu-id="7f3e7-139">Summary</span></span>

<span data-ttu-id="7f3e7-140">Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="7f3e7-141">Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Pi.</span><span class="sxs-lookup"><span data-stu-id="7f3e7-141">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f3e7-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f3e7-142">Next steps</span></span>

[<span data-ttu-id="7f3e7-143">Criar e implantar o aplicativo de intermitência hello</span><span class="sxs-lookup"><span data-stu-id="7f3e7-143">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
