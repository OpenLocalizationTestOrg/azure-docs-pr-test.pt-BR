---
title: "Conectar o Intel Edison (Nó) ao IoT do Azure - Lição 1: obter ferramentas (Ubuntu) | Microsoft Docs"
description: "Baixe e instale as ferramentas e softwares necessários para o primeiro aplicativo de exemplo do Edison no Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: ferramentas de desenvolvimento arduino, desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no ubuntu, instalar node js no ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 74c5f06c2b12d140814bfb75125d60b83addf70c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="f5871-104">Obter as ferramentas (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="f5871-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="f5871-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="f5871-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="f5871-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="f5871-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="f5871-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="f5871-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f5871-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="f5871-108">What you will do</span></span>
<span data-ttu-id="f5871-109">Baixar as ferramentas de desenvolvimento e o software para o primeiro aplicativo de exemplo do Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="f5871-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="f5871-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="f5871-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f5871-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="f5871-111">What you will learn</span></span>
<span data-ttu-id="f5871-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="f5871-112">In this article, you will learn:</span></span>

* <span data-ttu-id="f5871-113">Como instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="f5871-113">How to install Git and Node.js</span></span>
  * <span data-ttu-id="f5871-114">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="f5871-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="f5871-115">O aplicativo de exemplo para este artigo está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="f5871-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="f5871-116">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="f5871-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="f5871-117">Como usar o NPM (gerenciador de pacotes Node.js) para instalar ferramentas de desenvolvimento adicionais do Node.js.</span><span class="sxs-lookup"><span data-stu-id="f5871-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="f5871-118">A versão mínima necessária do Node.js é a 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="f5871-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="f5871-119">O [NPM](https://www.npmjs.com) é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="f5871-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f5871-120">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="f5871-120">What you need</span></span>
<span data-ttu-id="f5871-121">Para concluir esta operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="f5871-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="f5871-122">Uma conexão com a Internet para baixar as ferramentas de desenvolvimento e o software.</span><span class="sxs-lookup"><span data-stu-id="f5871-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="f5871-123">Um computador que esteja executando o Ubuntu 16.04 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f5871-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="f5871-124">Instale o Git, Node.js e o NPM</span><span class="sxs-lookup"><span data-stu-id="f5871-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="f5871-125">Use o atalho de teclado `Ctrl + Alt + T` para abrir um terminal e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f5871-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="f5871-126">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="f5871-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="f5871-127">Use [gulp.js](http://gulpjs.com) para automatizar a implantação do aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="f5871-127">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="f5871-128">Instale `gulp` executando o seguinte comando no terminal:</span><span class="sxs-lookup"><span data-stu-id="f5871-128">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="f5871-129">Se você tiver problemas ao instalar o Node.js e essas ferramentas adicionais de desenvolvimento no Ubuntu, consulte o [guia de solução de problemas][troubleshooting] para soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="f5871-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="f5871-130">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f5871-130">Install Visual Studio Code</span></span>
<span data-ttu-id="f5871-131">[Baixe](https://code.visualstudio.com/docs/setup/linux) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f5871-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="f5871-132">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="f5871-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f5871-133">Use este editor posteriormente no tutorial para editar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f5871-133">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="f5871-134">Resumo</span><span class="sxs-lookup"><span data-stu-id="f5871-134">Summary</span></span>
<span data-ttu-id="f5871-135">Você instalou as ferramentas de desenvolvimento e software necessários para o primeiro aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f5871-135">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="f5871-136">A tarefa seguinte é criar, implantar e executar o aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="f5871-136">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5871-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f5871-137">Next steps</span></span>
<span data-ttu-id="f5871-138">[Criar e implantar o aplicativo de exemplo de piscar][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="f5871-138">[Create and deploy the blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
