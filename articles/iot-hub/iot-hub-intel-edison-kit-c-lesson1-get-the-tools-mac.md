---
title: "Connect Intel Edison (C) tooAzure IoT - lição 1: obter ferramentas (macOS) | Microsoft Docs"
description: "Baixe e instale as ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Edison em macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: ferramentas de desenvolvimento arduino, desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no mac, instalar node js no mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 3f764f2e-25fa-4dde-9e8d-d278453fccfd
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a53331b0dce73c3dd51de91f07df86e28cbb6b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="7ddc4-104">Obter ferramentas hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="7ddc4-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="7ddc4-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="7ddc4-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="7ddc4-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="7ddc4-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="7ddc4-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="7ddc4-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7ddc4-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="7ddc4-108">What you will do</span></span>
<span data-ttu-id="7ddc4-109">Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para seu Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="7ddc4-110">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="7ddc4-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="7ddc4-111">Embora Olá linguagem da lógica principal Olá de programação C, Node. js ferramentas são usadas em Olá lições toobuild e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7ddc4-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7ddc4-112">What you will learn</span></span>
<span data-ttu-id="7ddc4-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="7ddc4-113">In this article, you will learn:</span></span>

* <span data-ttu-id="7ddc4-114">Como tooinstall Node. js e Git.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="7ddc4-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="7ddc4-116">aplicativo de exemplo Hello para este artigo é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="7ddc4-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="7ddc4-118">Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="7ddc4-119">versão mínima necessária de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="7ddc4-120">[NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7ddc4-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7ddc4-121">What you need</span></span>
<span data-ttu-id="7ddc4-122">toocomplete essa operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="7ddc4-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="7ddc4-123">Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="7ddc4-124">Um Mac que esteja executando o macOS Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="7ddc4-125">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="7ddc4-125">Install Git and Node.js</span></span>
<span data-ttu-id="7ddc4-126">tooinstall Git e Node. js, use Olá [Homebrew](http://brew.sh) utilitário de gerenciamento de pacote seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="7ddc4-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="7ddc4-127">Instale o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-127">Install Homebrew.</span></span> <span data-ttu-id="7ddc4-128">Se você já tiver instalado o Homebrew, vá toostep 2.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-128">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="7ddc4-129">Pressione `Cmd + Space` e digite `Terminal` tooopen um terminal.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="7ddc4-130">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ddc4-130">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="7ddc4-131">Instale o Git e Node. js executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ddc4-131">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="7ddc4-132">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="7ddc4-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="7ddc4-133">Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooyour de aplicativo de exemplo hello Edison.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Edison.</span></span>

<span data-ttu-id="7ddc4-134">Instalar `gulp` executando Olá comando no terminal Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ddc4-134">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="7ddc4-135">Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento adicional em macOS, consulte Olá [guia de solução de problemas] [ troubleshooting] para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="7ddc4-136">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7ddc4-136">Install Visual Studio Code</span></span>
<span data-ttu-id="7ddc4-137">[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="7ddc4-138">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="7ddc4-139">Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="7ddc4-140">Resumo</span><span class="sxs-lookup"><span data-stu-id="7ddc4-140">Summary</span></span>
<span data-ttu-id="7ddc4-141">Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="7ddc4-142">Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Edison.</span><span class="sxs-lookup"><span data-stu-id="7ddc4-142">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ddc4-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ddc4-143">Next steps</span></span>
<span data-ttu-id="7ddc4-144">[Criar e implantar o aplicativo de intermitência hello][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="7ddc4-144">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
