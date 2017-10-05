---
title: "Conectar o Raspberry Pi (C) ao IoT do Azure - Lição 1: obter ferramentas (Windows) | Microsoft Docs"
description: "Baixe e instale as ferramentas e software necessários para o primeiro aplicativo de exemplo para o Pi no Windows 7 e versões posteriores."
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
ms.openlocfilehash: 0e58975f4411f97223b2c4374bdd746fe6628c42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="7cabc-104">Obtenha as ferramentas (Windows 7 ou superior)</span><span class="sxs-lookup"><span data-stu-id="7cabc-104">Get the tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7cabc-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="7cabc-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="7cabc-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="7cabc-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="7cabc-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="7cabc-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="7cabc-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="7cabc-108">What you will do</span></span>
<span data-ttu-id="7cabc-109">Baixe as ferramentas de desenvolvimento e o software para o primeiro aplicativo de exemplo para o Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="7cabc-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="7cabc-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7cabc-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7cabc-111">Embora a linguagem de programação da lógica principal seja C, as ferramentas Node.js são usadas nas lições para descobrir dispositivos e criar e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7cabc-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7cabc-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7cabc-112">What you will learn</span></span>
<span data-ttu-id="7cabc-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="7cabc-113">In this article, you will learn:</span></span>

* <span data-ttu-id="7cabc-114">Como instalar o Git e o Node.js.</span><span class="sxs-lookup"><span data-stu-id="7cabc-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="7cabc-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="7cabc-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="7cabc-116">O aplicativo de exemplo para este artigo está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="7cabc-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="7cabc-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="7cabc-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="7cabc-118">Como usar o NPM (gerenciador de pacotes Node.js) para instalar ferramentas de desenvolvimento adicionais do Node.js.</span><span class="sxs-lookup"><span data-stu-id="7cabc-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="7cabc-119">O requisito mínimo de versão do Node.js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="7cabc-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="7cabc-120">O [NPM](https://www.npmjs.com) é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="7cabc-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7cabc-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7cabc-121">What you need</span></span>

<span data-ttu-id="7cabc-122">Para concluir esta operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="7cabc-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="7cabc-123">Uma conexão com a Internet para baixar as ferramentas de desenvolvimento e o software.</span><span class="sxs-lookup"><span data-stu-id="7cabc-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="7cabc-124">Um computador que esteja executando o Windows.</span><span class="sxs-lookup"><span data-stu-id="7cabc-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="7cabc-125">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="7cabc-125">Install Git and Node.js</span></span>

<span data-ttu-id="7cabc-126">Clique nos links abaixo para baixar e instalar o Git e o Node.js LTS para Windows.</span><span class="sxs-lookup"><span data-stu-id="7cabc-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="7cabc-127">Obtenha o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="7cabc-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="7cabc-128">Obtenha o Node.js LTS para o Windows</span><span class="sxs-lookup"><span data-stu-id="7cabc-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="7cabc-129">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="7cabc-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="7cabc-130">Use [gulp.js](http://gulpjs.com) para automatizar a implantação do aplicativo de exemplo para o Pi.</span><span class="sxs-lookup"><span data-stu-id="7cabc-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="7cabc-131">Use o [device-discovery-cli](https://github.com/Azure/device-discovery-cli) para recuperar informações de rede sobre os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="7cabc-131">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="7cabc-132">Inicie um prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="7cabc-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="7cabc-133">Instale `gulp` e `device-discovery-cli` executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7cabc-133">Install `gulp` and `device-discovery-cli` by running the following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="7cabc-134">Se você tiver problemas ao instalar o Node.js e essas ferramentas adicionais de desenvolvimento do Node.js no seu computador, consulte o [guia de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="7cabc-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="7cabc-135">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7cabc-135">Install Visual Studio Code</span></span>

<span data-ttu-id="7cabc-136">[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7cabc-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="7cabc-137">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="7cabc-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="7cabc-138">Use este editor posteriormente no tutorial para editar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7cabc-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="7cabc-139">Resumo</span><span class="sxs-lookup"><span data-stu-id="7cabc-139">Summary</span></span>

<span data-ttu-id="7cabc-140">Você instalou as ferramentas de desenvolvimento e software necessários para o primeiro aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7cabc-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="7cabc-141">A próxima tarefa é criar, implantar e executar o aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="7cabc-141">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cabc-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7cabc-142">Next steps</span></span>

[<span data-ttu-id="7cabc-143">Criar e implantar o aplicativo de intermitência</span><span class="sxs-lookup"><span data-stu-id="7cabc-143">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
