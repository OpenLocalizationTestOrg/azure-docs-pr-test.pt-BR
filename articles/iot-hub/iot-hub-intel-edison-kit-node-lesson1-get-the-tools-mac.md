---
title: "Conectar o Intel Edison (Nó) ao IoT do Azure - Lição 1: obter ferramentas (macOS)| Microsoft Docs"
description: "Baixe e instale as ferramentas e softwares necessários para o primeiro aplicativo de exemplo do Edison no macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: ferramentas de desenvolvimento arduino, desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no mac, instalar node js no mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="2c440-104">Obter as ferramentas (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="2c440-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2c440-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="2c440-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="2c440-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="2c440-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="2c440-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="2c440-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2c440-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="2c440-108">What you will do</span></span>
<span data-ttu-id="2c440-109">Baixar as ferramentas de desenvolvimento e o software para o primeiro aplicativo de exemplo do Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="2c440-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="2c440-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2c440-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2c440-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="2c440-111">What you will learn</span></span>
<span data-ttu-id="2c440-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="2c440-112">In this article, you will learn:</span></span>

* <span data-ttu-id="2c440-113">Como instalar o Git e o Node.js.</span><span class="sxs-lookup"><span data-stu-id="2c440-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="2c440-114">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="2c440-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="2c440-115">O aplicativo de exemplo para este artigo está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="2c440-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="2c440-116">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="2c440-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="2c440-117">Como usar o NPM (gerenciador de pacotes Node.js) para instalar ferramentas de desenvolvimento adicionais do Node.js.</span><span class="sxs-lookup"><span data-stu-id="2c440-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="2c440-118">A versão mínima necessária do Node.js é a 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="2c440-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="2c440-119">O [NPM](https://www.npmjs.com) é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="2c440-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2c440-120">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="2c440-120">What you need</span></span>
<span data-ttu-id="2c440-121">Para concluir esta operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="2c440-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="2c440-122">Uma conexão com a Internet para baixar as ferramentas de desenvolvimento e o software.</span><span class="sxs-lookup"><span data-stu-id="2c440-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="2c440-123">Um Mac que esteja executando o macOS Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2c440-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="2c440-124">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="2c440-124">Install Git and Node.js</span></span>
<span data-ttu-id="2c440-125">Para instalar o Git e o Node.js, use o utilitário de gerenciamento de pacote [Homebrew](http://brew.sh) seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="2c440-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="2c440-126">Instale o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="2c440-126">Install Homebrew.</span></span> <span data-ttu-id="2c440-127">Se você já tiver instalado o Homebrew, vá para a etapa 2.</span><span class="sxs-lookup"><span data-stu-id="2c440-127">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="2c440-128">Pressione `Cmd + Space` e digite `Terminal` para abrir um terminal.</span><span class="sxs-lookup"><span data-stu-id="2c440-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="2c440-129">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c440-129">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="2c440-130">Instale o Git e o Node.js executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2c440-130">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="2c440-131">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="2c440-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="2c440-132">Use [gulp.js](http://gulpjs.com) para automatizar a implantação do aplicativo de exemplo para o Edison.</span><span class="sxs-lookup"><span data-stu-id="2c440-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="2c440-133">Instale `gulp` executando o seguinte comando no terminal:</span><span class="sxs-lookup"><span data-stu-id="2c440-133">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="2c440-134">Se tiver problemas ao instalar o Node.js e essas ferramentas de desenvolvimento adicionais no macOS, consulte o [guia de solução de problemas][troubleshooting] para ver soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="2c440-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2c440-135">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2c440-135">Install Visual Studio Code</span></span>
<span data-ttu-id="2c440-136">[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2c440-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="2c440-137">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="2c440-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2c440-138">Use este editor posteriormente no tutorial para editar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2c440-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="2c440-139">Resumo</span><span class="sxs-lookup"><span data-stu-id="2c440-139">Summary</span></span>
<span data-ttu-id="2c440-140">Você instalou as ferramentas de desenvolvimento e software necessários para o primeiro aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2c440-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="2c440-141">A tarefa seguinte é criar, implantar e executar o aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="2c440-141">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c440-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c440-142">Next steps</span></span>
<span data-ttu-id="2c440-143">[Criar e implantar o aplicativo de piscar][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="2c440-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
