---
title: "Connect Raspberry PI (C) tooAzure IoT - lição 1: obter ferramentas (macOS) | Microsoft Docs"
description: "Baixar e instalar ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Pi macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no mac, execução de gulp, instalar node js no mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="3146c-104">Obter ferramentas hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="3146c-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3146c-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="3146c-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="3146c-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="3146c-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="3146c-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="3146c-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="3146c-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="3146c-108">What you will do</span></span>
<span data-ttu-id="3146c-109">Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para seu framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="3146c-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="3146c-110">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3146c-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3146c-111">Embora Olá linguagem da lógica principal Olá de programação C, Node. js ferramentas são usadas em dispositivos de toodiscover de lições Olá e criar e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3146c-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3146c-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="3146c-112">What you will learn</span></span>
<span data-ttu-id="3146c-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="3146c-113">In this article, you will learn:</span></span>

* <span data-ttu-id="3146c-114">Como tooinstall Node. js e Git.</span><span class="sxs-lookup"><span data-stu-id="3146c-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="3146c-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="3146c-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="3146c-116">aplicativo de exemplo Hello para este artigo é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="3146c-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="3146c-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="3146c-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="3146c-118">Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.</span><span class="sxs-lookup"><span data-stu-id="3146c-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="3146c-119">versão mínima necessária de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="3146c-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="3146c-120">[NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.</span><span class="sxs-lookup"><span data-stu-id="3146c-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3146c-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="3146c-121">What you need</span></span>
<span data-ttu-id="3146c-122">toocomplete essa operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="3146c-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="3146c-123">Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="3146c-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="3146c-124">Um Mac que esteja executando o macOS Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3146c-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="3146c-125">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="3146c-125">Install Git and Node.js</span></span>
<span data-ttu-id="3146c-126">tooinstall Git e Node. js, use Olá [Homebrew](http://brew.sh) utilitário de gerenciamento de pacote seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3146c-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="3146c-127">Instale o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="3146c-127">Install Homebrew.</span></span> <span data-ttu-id="3146c-128">Se você já tiver instalado o Homebrew, vá toostep 2.</span><span class="sxs-lookup"><span data-stu-id="3146c-128">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="3146c-129">Pressione `Cmd + Space` e digite `Terminal` tooopen um terminal.</span><span class="sxs-lookup"><span data-stu-id="3146c-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="3146c-130">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3146c-130">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="3146c-131">Instale o Git e Node. js executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3146c-131">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="3146c-132">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="3146c-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="3146c-133">Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooyour de aplicativo de exemplo hello Pi.</span><span class="sxs-lookup"><span data-stu-id="3146c-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Pi.</span></span> <span data-ttu-id="3146c-134">Saudação de uso [cli de descoberta do dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve informações de rede sobre os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="3146c-134">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="3146c-135">Instalar `gulp` e `device-discovery-cli` executando Olá comando no terminal Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3146c-135">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="3146c-136">Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento adicional em macOS, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="3146c-136">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="3146c-137">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3146c-137">Install Visual Studio Code</span></span>
<span data-ttu-id="3146c-138">[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3146c-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="3146c-139">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="3146c-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="3146c-140">Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="3146c-140">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="3146c-141">Resumo</span><span class="sxs-lookup"><span data-stu-id="3146c-141">Summary</span></span>
<span data-ttu-id="3146c-142">Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="3146c-142">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="3146c-143">Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Pi.</span><span class="sxs-lookup"><span data-stu-id="3146c-143">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3146c-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3146c-144">Next steps</span></span>
[<span data-ttu-id="3146c-145">Criar e implantar o aplicativo de intermitência hello</span><span class="sxs-lookup"><span data-stu-id="3146c-145">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

