---
title: "Conecte o Arduino ao IoT do Azure - Lição 1: obter ferramentas (Windows) | Microsoft Docs"
description: "Baixe e instale as ferramentas e software necessários para o primeiro aplicativo de exemplo para o Adafruit Feather M0 WiFi no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: ferramentas de desenvolvimento arduino, desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no windows, instalar node js no windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9cfb8cd2-eafb-4ba2-b23e-d94e114ff3a6
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d27c016c4a74e31455e676b3c3070a8e262b21f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="0c97a-104">Obtenha as ferramentas (Windows 7 ou superior)</span><span class="sxs-lookup"><span data-stu-id="0c97a-104">Get the tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="0c97a-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="0c97a-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="0c97a-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="0c97a-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="0c97a-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="0c97a-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="0c97a-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="0c97a-108">What you will do</span></span>

<span data-ttu-id="0c97a-109">Baixe as ferramentas de desenvolvimento e o software para o primeiro aplicativo de exemplo para a placa do Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="0c97a-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="0c97a-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="0c97a-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="0c97a-111">Embora a linguagem de programação da lógica principal seja o Arduino, ferramentas Node.js são usadas nas lições para compilar e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0c97a-111">Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0c97a-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="0c97a-112">What you will learn</span></span>
<span data-ttu-id="0c97a-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="0c97a-113">In this article, you will learn:</span></span>

* <span data-ttu-id="0c97a-114">Como instalar o Git e o Node.js.</span><span class="sxs-lookup"><span data-stu-id="0c97a-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="0c97a-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="0c97a-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="0c97a-116">O aplicativo de exemplo para este artigo está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="0c97a-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="0c97a-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="0c97a-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="0c97a-118">Como usar o NPM (gerenciador de pacotes Node.js) para instalar ferramentas de desenvolvimento adicionais do Node.js.</span><span class="sxs-lookup"><span data-stu-id="0c97a-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="0c97a-119">O requisito mínimo de versão do Node.js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="0c97a-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="0c97a-120">O [NPM](https://www.npmjs.com) é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="0c97a-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0c97a-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="0c97a-121">What you need</span></span>

<span data-ttu-id="0c97a-122">Para concluir esta operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="0c97a-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="0c97a-123">Uma conexão com a Internet para baixar as ferramentas de desenvolvimento e o software.</span><span class="sxs-lookup"><span data-stu-id="0c97a-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="0c97a-124">Um computador que esteja executando o Windows.</span><span class="sxs-lookup"><span data-stu-id="0c97a-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="0c97a-125">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="0c97a-125">Install Git and Node.js</span></span>

<span data-ttu-id="0c97a-126">Clique nos links abaixo para baixar e instalar o Git e o Node.js LTS para Windows.</span><span class="sxs-lookup"><span data-stu-id="0c97a-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="0c97a-127">Obtenha o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="0c97a-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="0c97a-128">Obtenha o Node.js LTS para o Windows</span><span class="sxs-lookup"><span data-stu-id="0c97a-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="0c97a-129">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="0c97a-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="0c97a-130">Use [gulp.js](http://gulpjs.com) para automatizar a implantação do aplicativo de exemplo para sua placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="0c97a-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="0c97a-131">Inicie um prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="0c97a-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="0c97a-132">Instale `gulp`, `device-discovery-cli` executando o seguinte comando no terminal:</span><span class="sxs-lookup"><span data-stu-id="0c97a-132">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
npm install -g gulp device-discovery-cli
```

<span data-ttu-id="0c97a-133">Se tiver problemas ao instalar o Node.js e essas ferramentas de desenvolvimento adicionais do Node.js no seu computador, consulte o [guia de solução de problemas][troubleshooting] para soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="0c97a-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="0c97a-134">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0c97a-134">Install Visual Studio Code</span></span>

<span data-ttu-id="0c97a-135">[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0c97a-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="0c97a-136">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="0c97a-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="0c97a-137">Use este editor posteriormente no tutorial para editar o código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0c97a-137">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="0c97a-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="0c97a-138">Summary</span></span>

<span data-ttu-id="0c97a-139">Você instalou as ferramentas de desenvolvimento e software necessários para o primeiro aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0c97a-139">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="0c97a-140">A tarefa seguinte é criar, implantar e executar o aplicativo de exemplo na placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="0c97a-140">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c97a-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c97a-141">Next steps</span></span>

<span data-ttu-id="0c97a-142">[Criar e implantar o aplicativo de exemplo de piscar][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="0c97a-142">[Create and deploy the blink sample application][create-and-deploy-the-blink-sample-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md