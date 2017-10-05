---
title: "Conectar o Raspberry Pi (C) ao IoT do Azure - Lição 1: obter ferramentas (Ubuntu) | Microsoft Docs"
description: "Baixe e instale as ferramentas e software necessários para o primeiro aplicativo de exemplo para o Pi no Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de iot, software de iot, software de internet das coisas, instalar o git no ubuntu, execução de gulp, instalar node js no ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="6af19-104">Obter as ferramentas (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="6af19-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6af19-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="6af19-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="6af19-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6af19-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="6af19-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="6af19-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="6af19-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="6af19-108">What you will do</span></span>
<span data-ttu-id="6af19-109">Baixe as ferramentas de desenvolvimento e o software para o primeiro aplicativo de exemplo para o Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="6af19-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="6af19-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6af19-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6af19-111">Embora a linguagem de programação da lógica principal seja C, as ferramentas Node.js são usadas nas lições para descobrir dispositivos e criar e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6af19-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6af19-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="6af19-112">What you will learn</span></span>
<span data-ttu-id="6af19-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="6af19-113">In this article, you will learn:</span></span>

* <span data-ttu-id="6af19-114">Como instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="6af19-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="6af19-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="6af19-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="6af19-116">O aplicativo de exemplo para este artigo está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="6af19-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="6af19-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="6af19-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="6af19-118">Como usar o NPM (gerenciador de pacotes Node.js) para instalar ferramentas de desenvolvimento adicionais do Node.js.</span><span class="sxs-lookup"><span data-stu-id="6af19-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="6af19-119">A versão mínima necessária do Node.js é a 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="6af19-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="6af19-120">O [NPM](https://www.npmjs.com) é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="6af19-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6af19-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="6af19-121">What you need</span></span>
<span data-ttu-id="6af19-122">Para concluir esta operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="6af19-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="6af19-123">Uma conexão com a Internet para baixar as ferramentas de desenvolvimento e o software.</span><span class="sxs-lookup"><span data-stu-id="6af19-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="6af19-124">Um computador que esteja executando o Ubuntu 16.04 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6af19-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="6af19-125">Instale o Git, Node.js e o NPM</span><span class="sxs-lookup"><span data-stu-id="6af19-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="6af19-126">Use o atalho de teclado `Ctrl + Alt + T` para abrir um terminal e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6af19-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="6af19-127">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="6af19-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="6af19-128">Use [gulp.js](http://gulpjs.com) para automatizar a implantação do aplicativo de exemplo para o Pi.</span><span class="sxs-lookup"><span data-stu-id="6af19-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="6af19-129">Use o [device-discovery-cli](https://github.com/Azure/device-discovery-cli) para recuperar informações de rede sobre os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="6af19-129">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="6af19-130">Instale `gulp` e `device-discovery-cli`, executando o seguinte comando no terminal:</span><span class="sxs-lookup"><span data-stu-id="6af19-130">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="6af19-131">Se você tiver problemas ao instalar o Node.js e essas ferramentas adicionais de desenvolvimento no Ubuntu, consulte o [guia de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="6af19-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="6af19-132">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6af19-132">Install Visual Studio Code</span></span>
<span data-ttu-id="6af19-133">[Baixe](https://code.visualstudio.com/docs/setup/linux) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6af19-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="6af19-134">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="6af19-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="6af19-135">Use este editor posteriormente no tutorial para editar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6af19-135">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="6af19-136">Resumo</span><span class="sxs-lookup"><span data-stu-id="6af19-136">Summary</span></span>
<span data-ttu-id="6af19-137">Você instalou as ferramentas de desenvolvimento e software necessários para o primeiro aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6af19-137">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="6af19-138">A próxima tarefa é criar, implantar e executar o aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="6af19-138">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6af19-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6af19-139">Next steps</span></span>
[<span data-ttu-id="6af19-140">Criar e implantar o aplicativo de intermitência</span><span class="sxs-lookup"><span data-stu-id="6af19-140">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

