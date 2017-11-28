---
title: "Conectar o Intel Edison (C) ao IoT do Azure - Lição 1: obter ferramentas (Windows)| Microsoft Docs"
description: "Baixe e instale as ferramentas e softwares necessários para o primeiro aplicativo de exemplo do Edison no Windows 7 e em versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: ferramentas de desenvolvimento arduino, desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no windows, instalar node js no windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 7d29a358-544d-4657-a504-5ed9b79c2925
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9d614d17f262b81a75d6128cbc5898dc18ab906
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="7775e-104">Obtenha as ferramentas (Windows 7 ou superior)</span><span class="sxs-lookup"><span data-stu-id="7775e-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="7775e-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="7775e-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="7775e-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="7775e-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="7775e-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="7775e-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7775e-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="7775e-108">What you will do</span></span>
<span data-ttu-id="7775e-109">Baixará as ferramentas de desenvolvimento e o software para o primeiro aplicativo de exemplo do Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="7775e-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="7775e-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="7775e-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="7775e-111">Embora a linguagem de programação da lógica principal seja C, ferramentas Node.js são usadas nas lições para compilar e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7775e-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7775e-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7775e-112">What you will learn</span></span>
<span data-ttu-id="7775e-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="7775e-113">In this article, you will learn:</span></span>

* <span data-ttu-id="7775e-114">Como instalar o Git e o Node.js.</span><span class="sxs-lookup"><span data-stu-id="7775e-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="7775e-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="7775e-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="7775e-116">O aplicativo de exemplo para este artigo está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="7775e-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="7775e-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="7775e-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="7775e-118">Como usar o NPM (gerenciador de pacotes Node.js) para instalar ferramentas de desenvolvimento adicionais do Node.js.</span><span class="sxs-lookup"><span data-stu-id="7775e-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="7775e-119">O requisito mínimo de versão do Node.js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="7775e-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="7775e-120">O [NPM](https://www.npmjs.com) é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="7775e-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7775e-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7775e-121">What you need</span></span>

<span data-ttu-id="7775e-122">Para concluir esta operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="7775e-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="7775e-123">Uma conexão com a Internet para baixar as ferramentas de desenvolvimento e o software.</span><span class="sxs-lookup"><span data-stu-id="7775e-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="7775e-124">Um computador que esteja executando o Windows.</span><span class="sxs-lookup"><span data-stu-id="7775e-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="7775e-125">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="7775e-125">Install Git and Node.js</span></span>

<span data-ttu-id="7775e-126">Clique nos links abaixo para baixar e instalar o Git e o Node.js LTS para Windows.</span><span class="sxs-lookup"><span data-stu-id="7775e-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="7775e-127">Obtenha o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="7775e-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="7775e-128">Obtenha o Node.js LTS para o Windows</span><span class="sxs-lookup"><span data-stu-id="7775e-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="7775e-129">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="7775e-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="7775e-130">Use [gulp.js](http://gulpjs.com) para automatizar a implantação do aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="7775e-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="7775e-131">Inicie um prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="7775e-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="7775e-132">Instale o `gulp` executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7775e-132">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="7775e-133">Se tiver problemas ao instalar o Node.js e essas ferramentas de desenvolvimento adicionais do Node.js no seu computador, consulte o [guia de solução de problemas][troubleshooting] para soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="7775e-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="7775e-134">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7775e-134">Install Visual Studio Code</span></span>

<span data-ttu-id="7775e-135">[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7775e-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="7775e-136">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="7775e-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="7775e-137">Use este editor posteriormente no tutorial para editar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7775e-137">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="7775e-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="7775e-138">Summary</span></span>

<span data-ttu-id="7775e-139">Você instalou as ferramentas de desenvolvimento e software necessários para o primeiro aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7775e-139">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="7775e-140">A tarefa seguinte é criar, implantar e executar o aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="7775e-140">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7775e-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7775e-141">Next steps</span></span>

<span data-ttu-id="7775e-142">[Criar e implantar o aplicativo de piscar][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="7775e-142">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
