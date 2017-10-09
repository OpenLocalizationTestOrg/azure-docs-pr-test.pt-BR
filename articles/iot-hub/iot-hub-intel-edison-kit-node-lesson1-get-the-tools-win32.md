---
title: "Conecte-se Edison Intel (nó) tooAzure IoT - lição 1: obter ferramentas (Windows) | Microsoft Docs"
description: "Baixe e instale as ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Edison no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: ferramentas de desenvolvimento arduino, desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no windows, instalar node js no windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="a22eb-104">Obter ferramentas hello (Windows 7 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="a22eb-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a22eb-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="a22eb-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="a22eb-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="a22eb-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="a22eb-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="a22eb-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a22eb-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="a22eb-108">What you will do</span></span>
<span data-ttu-id="a22eb-109">Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="a22eb-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="a22eb-110">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a22eb-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a22eb-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="a22eb-111">What you will learn</span></span>
<span data-ttu-id="a22eb-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="a22eb-112">In this article, you will learn:</span></span>

* <span data-ttu-id="a22eb-113">Como tooinstall Node. js e Git.</span><span class="sxs-lookup"><span data-stu-id="a22eb-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="a22eb-114">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="a22eb-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a22eb-115">aplicativo de exemplo Hello para este artigo é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="a22eb-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a22eb-116">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="a22eb-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a22eb-117">Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.</span><span class="sxs-lookup"><span data-stu-id="a22eb-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="a22eb-118">requisito de versão mínima de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="a22eb-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a22eb-119">[NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.</span><span class="sxs-lookup"><span data-stu-id="a22eb-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a22eb-120">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="a22eb-120">What you need</span></span>

<span data-ttu-id="a22eb-121">toocomplete essa operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="a22eb-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="a22eb-122">Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="a22eb-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="a22eb-123">Um computador que esteja executando o Windows.</span><span class="sxs-lookup"><span data-stu-id="a22eb-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="a22eb-124">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="a22eb-124">Install Git and Node.js</span></span>

<span data-ttu-id="a22eb-125">Clicar em links de saudação abaixo toodownload e instale o Git e LTS Node. js para Windows.</span><span class="sxs-lookup"><span data-stu-id="a22eb-125">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="a22eb-126">Obtenha o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="a22eb-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="a22eb-127">Obtenha o Node.js LTS para o Windows</span><span class="sxs-lookup"><span data-stu-id="a22eb-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a22eb-128">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="a22eb-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="a22eb-129">Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooEdison de aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="a22eb-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="a22eb-130">Inicie um prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="a22eb-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="a22eb-131">Instalar `gulp` executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a22eb-131">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="a22eb-132">Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento Node. js adicionais no seu computador, consulte Olá [guia de solução de problemas] [ troubleshooting] para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="a22eb-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a22eb-133">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a22eb-133">Install Visual Studio Code</span></span>

<span data-ttu-id="a22eb-134">[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a22eb-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="a22eb-135">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="a22eb-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a22eb-136">Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="a22eb-136">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a22eb-137">Resumo</span><span class="sxs-lookup"><span data-stu-id="a22eb-137">Summary</span></span>

<span data-ttu-id="a22eb-138">Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="a22eb-138">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="a22eb-139">Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Edison.</span><span class="sxs-lookup"><span data-stu-id="a22eb-139">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a22eb-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a22eb-140">Next steps</span></span>

<span data-ttu-id="a22eb-141">[Criar e implantar o aplicativo de intermitência hello][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="a22eb-141">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
