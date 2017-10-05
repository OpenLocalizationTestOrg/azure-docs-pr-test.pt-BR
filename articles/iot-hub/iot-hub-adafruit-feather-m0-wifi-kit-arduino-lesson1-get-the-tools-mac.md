---
title: "Conecte o Arduino ao IoT do Azure - Lição 1: obter ferramentas (macOS) | Microsoft Docs"
description: "Baixe e instale as ferramentas e software necessários para o primeiro aplicativo de exemplo para o Adafruit Feather M0 WiFi no macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: ferramentas de desenvolvimento arduino, desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no mac, instalar node js no mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a6dc2555367e5fe530b3acde1f1f04ac442fb638
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="833b0-104">Obter as ferramentas (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="833b0-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="833b0-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="833b0-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="833b0-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="833b0-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="833b0-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="833b0-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="833b0-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="833b0-108">What you will do</span></span>

<span data-ttu-id="833b0-109">Baixe as ferramentas de desenvolvimento e o software para o primeiro aplicativo de exemplo para a placa do Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="833b0-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="833b0-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="833b0-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="833b0-111">Embora a linguagem de programação da lógica principal seja o Arduino, ferramentas Node.js são usadas nas lições para compilar e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="833b0-111">Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="833b0-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="833b0-112">What you will learn</span></span>
<span data-ttu-id="833b0-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="833b0-113">In this article, you will learn:</span></span>

* <span data-ttu-id="833b0-114">Como instalar o Git e o Node.js.</span><span class="sxs-lookup"><span data-stu-id="833b0-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="833b0-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="833b0-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="833b0-116">O aplicativo de exemplo para este artigo está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="833b0-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="833b0-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="833b0-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="833b0-118">Como usar o NPM (gerenciador de pacotes Node.js) para instalar ferramentas de desenvolvimento adicionais do Node.js.</span><span class="sxs-lookup"><span data-stu-id="833b0-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="833b0-119">A versão mínima necessária do Node.js é a 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="833b0-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="833b0-120">O [NPM](https://www.npmjs.com) é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="833b0-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="833b0-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="833b0-121">What you need</span></span>
<span data-ttu-id="833b0-122">Para concluir esta operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="833b0-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="833b0-123">Uma conexão com a Internet para baixar as ferramentas de desenvolvimento e o software.</span><span class="sxs-lookup"><span data-stu-id="833b0-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="833b0-124">Um Mac que esteja executando o macOS Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="833b0-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="833b0-125">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="833b0-125">Install Git and Node.js</span></span>
<span data-ttu-id="833b0-126">Para instalar o Git e o Node.js, use o utilitário de gerenciamento de pacote [Homebrew](http://brew.sh) seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="833b0-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="833b0-127">Instale o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="833b0-127">Install Homebrew.</span></span> <span data-ttu-id="833b0-128">Se você já tiver instalado o Homebrew, vá para a etapa 2.</span><span class="sxs-lookup"><span data-stu-id="833b0-128">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="833b0-129">Pressione `Cmd + Space` e digite `Terminal` para abrir um terminal.</span><span class="sxs-lookup"><span data-stu-id="833b0-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="833b0-130">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="833b0-130">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="833b0-131">Instale o Git e o Node.js executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="833b0-131">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="833b0-132">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="833b0-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="833b0-133">Use [gulp.js](http://gulpjs.com) para automatizar a implantação do aplicativo de exemplo para sua placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="833b0-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="833b0-134">Instale `gulp`, `device-discovery-cli` executando o seguinte comando no terminal:</span><span class="sxs-lookup"><span data-stu-id="833b0-134">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="833b0-135">Se tiver problemas ao instalar o Node.js e essas ferramentas de desenvolvimento adicionais no macOS, consulte o [guia de solução de problemas][troubleshooting] para ver soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="833b0-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="833b0-136">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="833b0-136">Install Visual Studio Code</span></span>
<span data-ttu-id="833b0-137">[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="833b0-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="833b0-138">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="833b0-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="833b0-139">Use este editor posteriormente no tutorial para editar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="833b0-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="833b0-140">Resumo</span><span class="sxs-lookup"><span data-stu-id="833b0-140">Summary</span></span>
<span data-ttu-id="833b0-141">Você instalou as ferramentas de desenvolvimento e software necessários para o primeiro aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="833b0-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="833b0-142">A tarefa seguinte é criar, implantar e executar o aplicativo de exemplo na placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="833b0-142">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="833b0-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="833b0-143">Next steps</span></span>
<span data-ttu-id="833b0-144">[Criar e implantar o aplicativo de piscar][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="833b0-144">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md