---
title: "Conecte-se framboesa Pi (nó) tooAzure IoT - lição 1: obter ferramentas (Ubuntu) | Microsoft Docs"
description: "Baixe e instale as ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Pi no Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "desenvolvimento de iot, software de iot, software de internet das coisas, instalar o git no ubuntu, execução de gulp, instalar node js no ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="b08ec-104">Obter ferramentas hello (16.04 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="b08ec-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b08ec-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="b08ec-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="b08ec-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="b08ec-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="b08ec-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="b08ec-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="b08ec-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="b08ec-108">What you will do</span></span>
<span data-ttu-id="b08ec-109">Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b08ec-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="b08ec-110">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b08ec-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b08ec-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="b08ec-111">What you will learn</span></span>
<span data-ttu-id="b08ec-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="b08ec-112">In this article, you will learn:</span></span>

* <span data-ttu-id="b08ec-113">Como tooinstall Node. js e Git.</span><span class="sxs-lookup"><span data-stu-id="b08ec-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="b08ec-114">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="b08ec-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="b08ec-115">aplicativo de exemplo Hello para este artigo é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="b08ec-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="b08ec-116">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="b08ec-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="b08ec-117">Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.</span><span class="sxs-lookup"><span data-stu-id="b08ec-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="b08ec-118">versão mínima necessária de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="b08ec-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="b08ec-119">[NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.</span><span class="sxs-lookup"><span data-stu-id="b08ec-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="b08ec-120">Do que você precisa</span><span class="sxs-lookup"><span data-stu-id="b08ec-120">What do you need</span></span>
<span data-ttu-id="b08ec-121">toocomplete essa operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="b08ec-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="b08ec-122">Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="b08ec-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="b08ec-123">Um computador que esteja executando o Ubuntu 16.04 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b08ec-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="b08ec-124">Instale o Git, Node.js e o NPM</span><span class="sxs-lookup"><span data-stu-id="b08ec-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="b08ec-125">Atalho de teclado do uso Olá `Ctrl + Alt + T` tooopen comandos de uma saudação de terminal e execute a seguir:</span><span class="sxs-lookup"><span data-stu-id="b08ec-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="b08ec-126">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="b08ec-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="b08ec-127">Você usa [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooPi de aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="b08ec-127">You use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="b08ec-128">Você também usar Olá [cli de descoberta do dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve informações de rede sobre os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="b08ec-128">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="b08ec-129">Instalar `gulp` e `device-discovery-cli` executando Olá comando no terminal Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b08ec-129">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="b08ec-130">Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento adicional no Ubuntu, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="b08ec-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="b08ec-131">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b08ec-131">Install Visual Studio Code</span></span>
<span data-ttu-id="b08ec-132">[Baixe](https://code.visualstudio.com/docs/setup/linux) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b08ec-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="b08ec-133">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="b08ec-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="b08ec-134">Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="b08ec-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="b08ec-135">Resumo</span><span class="sxs-lookup"><span data-stu-id="b08ec-135">Summary</span></span>
<span data-ttu-id="b08ec-136">Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="b08ec-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="b08ec-137">Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Pi.</span><span class="sxs-lookup"><span data-stu-id="b08ec-137">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b08ec-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b08ec-138">Next steps</span></span>
[<span data-ttu-id="b08ec-139">Criar e implantar o aplicativo de exemplo hello blink</span><span class="sxs-lookup"><span data-stu-id="b08ec-139">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

