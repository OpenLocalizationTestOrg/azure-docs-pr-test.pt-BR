---
title: "Conectar o Raspberry Pi (C) ao IoT do Azure - Lição 1: obter ferramentas (macOS) | Microsoft Docs"
description: "Baixe e instale as ferramentas e software necessários para o primeiro aplicativo de exemplo para o Pi no macOS."
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
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="b7421-104">Obter as ferramentas (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="b7421-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7421-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="b7421-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="b7421-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="b7421-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="b7421-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="b7421-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="b7421-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="b7421-108">What you will do</span></span>
<span data-ttu-id="b7421-109">Baixe as ferramentas de desenvolvimento e o software para o primeiro aplicativo de exemplo para o Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b7421-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="b7421-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b7421-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b7421-111">Embora a linguagem de programação da lógica principal seja C, as ferramentas Node.js são usadas nas lições para descobrir dispositivos e criar e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b7421-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b7421-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="b7421-112">What you will learn</span></span>
<span data-ttu-id="b7421-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="b7421-113">In this article, you will learn:</span></span>

* <span data-ttu-id="b7421-114">Como instalar o Git e o Node.js.</span><span class="sxs-lookup"><span data-stu-id="b7421-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="b7421-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="b7421-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="b7421-116">O aplicativo de exemplo para este artigo está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="b7421-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="b7421-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="b7421-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="b7421-118">Como usar o NPM (gerenciador de pacotes Node.js) para instalar ferramentas de desenvolvimento adicionais do Node.js.</span><span class="sxs-lookup"><span data-stu-id="b7421-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="b7421-119">A versão mínima necessária do Node.js é a 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="b7421-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="b7421-120">O [NPM](https://www.npmjs.com) é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="b7421-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b7421-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="b7421-121">What you need</span></span>
<span data-ttu-id="b7421-122">Para concluir esta operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="b7421-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="b7421-123">Uma conexão com a Internet para baixar as ferramentas de desenvolvimento e o software.</span><span class="sxs-lookup"><span data-stu-id="b7421-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="b7421-124">Um Mac que esteja executando o macOS Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b7421-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="b7421-125">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="b7421-125">Install Git and Node.js</span></span>
<span data-ttu-id="b7421-126">Para instalar o Git e o Node.js, use o utilitário de gerenciamento de pacote [Homebrew](http://brew.sh) seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="b7421-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="b7421-127">Instale o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="b7421-127">Install Homebrew.</span></span> <span data-ttu-id="b7421-128">Se você já tiver instalado o Homebrew, vá para a etapa 2.</span><span class="sxs-lookup"><span data-stu-id="b7421-128">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="b7421-129">Pressione `Cmd + Space` e digite `Terminal` para abrir um terminal.</span><span class="sxs-lookup"><span data-stu-id="b7421-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="b7421-130">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7421-130">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="b7421-131">Instale o Git e o Node.js executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b7421-131">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="b7421-132">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="b7421-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="b7421-133">Use [gulp.js](http://gulpjs.com) para automatizar a implantação do aplicativo de exemplo para o Pi.</span><span class="sxs-lookup"><span data-stu-id="b7421-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Pi.</span></span> <span data-ttu-id="b7421-134">Use o [device-discovery-cli](https://github.com/Azure/device-discovery-cli) para recuperar informações de rede sobre os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="b7421-134">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="b7421-135">Instale `gulp` e `device-discovery-cli`, executando o seguinte comando no terminal:</span><span class="sxs-lookup"><span data-stu-id="b7421-135">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="b7421-136">Se você tiver problemas ao instalar o Node.js e essas ferramentas adicionais de desenvolvimento no macOS, consulte o [guia de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="b7421-136">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="b7421-137">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b7421-137">Install Visual Studio Code</span></span>
<span data-ttu-id="b7421-138">[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b7421-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="b7421-139">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="b7421-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="b7421-140">Use este editor posteriormente no tutorial para editar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b7421-140">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="b7421-141">Resumo</span><span class="sxs-lookup"><span data-stu-id="b7421-141">Summary</span></span>
<span data-ttu-id="b7421-142">Você instalou as ferramentas de desenvolvimento e software necessários para o primeiro aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b7421-142">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="b7421-143">A próxima tarefa é criar, implantar e executar o aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="b7421-143">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7421-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7421-144">Next steps</span></span>
[<span data-ttu-id="b7421-145">Criar e implantar o aplicativo de intermitência</span><span class="sxs-lookup"><span data-stu-id="b7421-145">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

