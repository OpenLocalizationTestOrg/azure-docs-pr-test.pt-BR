---
title: "Conecte o Raspberry Pi (Nó) ao IoT do Azure - Lição 1: obter ferramentas (Ubuntu) | Microsoft Docs"
description: "Baixe e instale as ferramentas e software necessários para o primeiro aplicativo de exemplo para o Pi no Ubuntu."
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
ms.openlocfilehash: de583be0cdce058c83091f421376812e8013d76e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="af70d-104">Obter as ferramentas (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="af70d-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="af70d-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="af70d-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="af70d-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="af70d-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="af70d-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="af70d-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="af70d-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="af70d-108">What you will do</span></span>
<span data-ttu-id="af70d-109">Baixe as ferramentas de desenvolvimento e o software para o primeiro aplicativo de exemplo para o Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="af70d-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="af70d-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="af70d-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="af70d-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="af70d-111">What you will learn</span></span>
<span data-ttu-id="af70d-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="af70d-112">In this article, you will learn:</span></span>

* <span data-ttu-id="af70d-113">Como instalar o Git e o Node.js.</span><span class="sxs-lookup"><span data-stu-id="af70d-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="af70d-114">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="af70d-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="af70d-115">O aplicativo de exemplo para este artigo está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="af70d-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="af70d-116">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="af70d-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="af70d-117">Como usar o NPM (gerenciador de pacotes Node.js) para instalar ferramentas de desenvolvimento adicionais do Node.js.</span><span class="sxs-lookup"><span data-stu-id="af70d-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="af70d-118">A versão mínima necessária do Node.js é a 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="af70d-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="af70d-119">O [NPM](https://www.npmjs.com) é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="af70d-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="af70d-120">Do que você precisa</span><span class="sxs-lookup"><span data-stu-id="af70d-120">What do you need</span></span>
<span data-ttu-id="af70d-121">Para concluir esta operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="af70d-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="af70d-122">Uma conexão com a Internet para baixar as ferramentas de desenvolvimento e o software.</span><span class="sxs-lookup"><span data-stu-id="af70d-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="af70d-123">Um computador que esteja executando o Ubuntu 16.04 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="af70d-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="af70d-124">Instale o Git, Node.js e o NPM</span><span class="sxs-lookup"><span data-stu-id="af70d-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="af70d-125">Use o atalho de teclado `Ctrl + Alt + T` para abrir um terminal e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="af70d-125">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="af70d-126">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="af70d-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="af70d-127">Você usa o [gulp.js](http://gulpjs.com) para automatizar a implantação do aplicativo de exemplo para o Pi.</span><span class="sxs-lookup"><span data-stu-id="af70d-127">You use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="af70d-128">E também usa o [device-discovery-cli](https://github.com/Azure/device-discovery-cli) para recuperar informações de rede sobre os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="af70d-128">You also use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="af70d-129">Instale `gulp` e `device-discovery-cli`, executando o seguinte comando no terminal:</span><span class="sxs-lookup"><span data-stu-id="af70d-129">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="af70d-130">Se você tiver problemas ao instalar o Node.js e essas ferramentas adicionais de desenvolvimento no Ubuntu, consulte o [guia de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="af70d-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="af70d-131">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="af70d-131">Install Visual Studio Code</span></span>
<span data-ttu-id="af70d-132">[Baixe](https://code.visualstudio.com/docs/setup/linux) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="af70d-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="af70d-133">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="af70d-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="af70d-134">Use este editor posteriormente no tutorial para editar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="af70d-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="af70d-135">Resumo</span><span class="sxs-lookup"><span data-stu-id="af70d-135">Summary</span></span>
<span data-ttu-id="af70d-136">Você instalou as ferramentas de desenvolvimento e software necessários para o primeiro aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="af70d-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="af70d-137">A próxima tarefa é criar, implantar e executar o aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="af70d-137">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af70d-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af70d-138">Next steps</span></span>
[<span data-ttu-id="af70d-139">Criar e implantar o aplicativo de exemplo intermitente</span><span class="sxs-lookup"><span data-stu-id="af70d-139">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

