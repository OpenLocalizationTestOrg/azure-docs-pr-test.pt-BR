---
title: "Conecte-se framboesa Pi (nó) tooAzure IoT - lição 1: obter ferramentas (macOS) | Microsoft Docs"
description: "Baixar e instalar ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Pi macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "desenvolvimento de iot, software de iot, software de internet das coisas, instalar python no mac, instalar o git no mac, execução de gulp, instalar node js no mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 382b066cb7ece7ffdeb22b162b725727b22e5fac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="11b84-104">Obter ferramentas hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="11b84-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11b84-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="11b84-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="11b84-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="11b84-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="11b84-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="11b84-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="11b84-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="11b84-108">What you will do</span></span>
<span data-ttu-id="11b84-109">Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para seu framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="11b84-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="11b84-110">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="11b84-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="11b84-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="11b84-111">What you will learn</span></span>
<span data-ttu-id="11b84-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="11b84-112">In this article, you will learn:</span></span>

* <span data-ttu-id="11b84-113">Como tooinstall Node. js e Git.</span><span class="sxs-lookup"><span data-stu-id="11b84-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="11b84-114">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="11b84-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="11b84-115">aplicativo de exemplo Hello para este artigo é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="11b84-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="11b84-116">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="11b84-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="11b84-117">Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.</span><span class="sxs-lookup"><span data-stu-id="11b84-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="11b84-118">versão mínima necessária de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="11b84-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="11b84-119">[NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.</span><span class="sxs-lookup"><span data-stu-id="11b84-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="11b84-120">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="11b84-120">What you need</span></span>
<span data-ttu-id="11b84-121">toocomplete essa operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="11b84-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="11b84-122">Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="11b84-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="11b84-123">Um Mac que esteja executando o macOS Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="11b84-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="11b84-124">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="11b84-124">Install Git and Node.js</span></span>
<span data-ttu-id="11b84-125">tooinstall Git e Node. js, use Olá [Homebrew](http://brew.sh) utilitário de gerenciamento de pacote seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="11b84-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="11b84-126">Instale o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="11b84-126">Install Homebrew.</span></span> <span data-ttu-id="11b84-127">Se você já tiver instalado o Homebrew, vá toostep 2.</span><span class="sxs-lookup"><span data-stu-id="11b84-127">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="11b84-128">Pressione `Cmd + Space` e digite `Terminal` tooopen um terminal.</span><span class="sxs-lookup"><span data-stu-id="11b84-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="11b84-129">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="11b84-129">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="11b84-130">Instale o Git e Node. js executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="11b84-130">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="11b84-131">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="11b84-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="11b84-132">Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooPi de aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="11b84-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="11b84-133">Saudação de uso [cli de descoberta do dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve informações de rede sobre os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="11b84-133">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="11b84-134">Instalar `gulp` e `device-discovery-cli` executando Olá comando no terminal Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="11b84-134">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="11b84-135">Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento adicional em macOS, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="11b84-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="11b84-136">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="11b84-136">Install Visual Studio Code</span></span>
<span data-ttu-id="11b84-137">[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="11b84-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="11b84-138">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="11b84-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="11b84-139">Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="11b84-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="11b84-140">Resumo</span><span class="sxs-lookup"><span data-stu-id="11b84-140">Summary</span></span>
<span data-ttu-id="11b84-141">Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="11b84-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="11b84-142">Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Pi.</span><span class="sxs-lookup"><span data-stu-id="11b84-142">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11b84-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11b84-143">Next steps</span></span>
[<span data-ttu-id="11b84-144">Criar e implantar o aplicativo de exemplo hello blink</span><span class="sxs-lookup"><span data-stu-id="11b84-144">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

