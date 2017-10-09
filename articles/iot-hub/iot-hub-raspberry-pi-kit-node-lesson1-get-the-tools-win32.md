---
title: "Conecte-se framboesa Pi (nó) tooAzure IoT - lição 1: obter ferramentas (Windows) | Microsoft Docs"
description: "Baixe e instale as ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Pi no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: desenvolvimento de iot, software de iot, software de internet das coisas, instalar o git no windows, instalar node js no windows, instalar npm no windows, instalar python no windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ea7f77cc79c70c8c7952b63462b926471fcf71cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="576a7-104">Obter ferramentas hello (Windows 7 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="576a7-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="576a7-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="576a7-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="576a7-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="576a7-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="576a7-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="576a7-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="576a7-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="576a7-108">What you will do</span></span>
<span data-ttu-id="576a7-109">Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="576a7-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="576a7-110">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="576a7-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="576a7-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="576a7-111">What you will learn</span></span>
<span data-ttu-id="576a7-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="576a7-112">In this article, you will learn:</span></span>

* <span data-ttu-id="576a7-113">Como tooinstall Node. js e Git.</span><span class="sxs-lookup"><span data-stu-id="576a7-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="576a7-114">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="576a7-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="576a7-115">aplicativo de exemplo Hello para este artigo é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="576a7-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="576a7-116">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="576a7-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="576a7-117">Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.</span><span class="sxs-lookup"><span data-stu-id="576a7-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="576a7-118">requisito de versão mínima de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="576a7-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="576a7-119">[NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.</span><span class="sxs-lookup"><span data-stu-id="576a7-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="576a7-120">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="576a7-120">What you need</span></span>
<span data-ttu-id="576a7-121">toocomplete essa operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="576a7-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="576a7-122">Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="576a7-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="576a7-123">Um computador que esteja executando o Windows.</span><span class="sxs-lookup"><span data-stu-id="576a7-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="576a7-124">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="576a7-124">Install Git and Node.js</span></span>
<span data-ttu-id="576a7-125">Clique Olá toodownload links a seguir e instale o Git e LTS Node. js para Windows.</span><span class="sxs-lookup"><span data-stu-id="576a7-125">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="576a7-126">Obtenha o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="576a7-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="576a7-127">Obtenha o Node.js LTS para o Windows</span><span class="sxs-lookup"><span data-stu-id="576a7-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="576a7-128">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="576a7-128">Install additional Node.js development tools</span></span>
<span data-ttu-id="576a7-129">Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooPi de aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="576a7-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="576a7-130">Você também usar Olá [cli de descoberta do dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve informações de rede sobre os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="576a7-130">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="576a7-131">Inicie um prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="576a7-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="576a7-132">Instalar `gulp` e `device-discovery-cli` executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="576a7-132">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="576a7-133">Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento Node. js adicionais no seu computador, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="576a7-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="576a7-134">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="576a7-134">Install Visual Studio Code</span></span>
<span data-ttu-id="576a7-135">[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="576a7-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="576a7-136">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="576a7-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="576a7-137">Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="576a7-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="576a7-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="576a7-138">Summary</span></span>
<span data-ttu-id="576a7-139">Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="576a7-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="576a7-140">Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Pi.</span><span class="sxs-lookup"><span data-stu-id="576a7-140">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="576a7-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="576a7-141">Next steps</span></span>
[<span data-ttu-id="576a7-142">Criar e implantar o aplicativo de exemplo hello blink</span><span class="sxs-lookup"><span data-stu-id="576a7-142">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

