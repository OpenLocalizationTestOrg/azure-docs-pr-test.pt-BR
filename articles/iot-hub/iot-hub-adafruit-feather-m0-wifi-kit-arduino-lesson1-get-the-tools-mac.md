---
title: "Conecte-se Arduino tooAzure IoT - lição 1: obter ferramentas (macOS) | Microsoft Docs"
description: "Baixe e instale as ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Adafruit difusão M0 WiFi em macOS."
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
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="dcef0-104">Obter ferramentas hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="dcef0-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="dcef0-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="dcef0-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="dcef0-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="dcef0-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="dcef0-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="dcef0-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="dcef0-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="dcef0-108">What you will do</span></span>

<span data-ttu-id="dcef0-109">Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para a sua placa Adafruit difusão M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="dcef0-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="dcef0-110">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="dcef0-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="dcef0-111">Embora Arduino Olá linguagem da lógica principal Olá de programação, ferramentas Node.js são usadas em Olá lições toobuild e implantar aplicativos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="dcef0-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="dcef0-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="dcef0-112">What you will learn</span></span>
<span data-ttu-id="dcef0-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="dcef0-113">In this article, you will learn:</span></span>

* <span data-ttu-id="dcef0-114">Como tooinstall Node. js e Git.</span><span class="sxs-lookup"><span data-stu-id="dcef0-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="dcef0-115">[Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído.</span><span class="sxs-lookup"><span data-stu-id="dcef0-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="dcef0-116">aplicativo de exemplo Hello para este artigo é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="dcef0-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="dcef0-117">O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="dcef0-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="dcef0-118">Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.</span><span class="sxs-lookup"><span data-stu-id="dcef0-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="dcef0-119">versão mínima necessária de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="dcef0-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="dcef0-120">[NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.</span><span class="sxs-lookup"><span data-stu-id="dcef0-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="dcef0-121">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="dcef0-121">What you need</span></span>
<span data-ttu-id="dcef0-122">toocomplete essa operação, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="dcef0-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="dcef0-123">Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.</span><span class="sxs-lookup"><span data-stu-id="dcef0-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="dcef0-124">Um Mac que esteja executando o macOS Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="dcef0-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="dcef0-125">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="dcef0-125">Install Git and Node.js</span></span>
<span data-ttu-id="dcef0-126">tooinstall Git e Node. js, use Olá [Homebrew](http://brew.sh) utilitário de gerenciamento de pacote seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="dcef0-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="dcef0-127">Instale o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="dcef0-127">Install Homebrew.</span></span> <span data-ttu-id="dcef0-128">Se você já tiver instalado o Homebrew, vá toostep 2.</span><span class="sxs-lookup"><span data-stu-id="dcef0-128">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="dcef0-129">Pressione `Cmd + Space` e digite `Terminal` tooopen um terminal.</span><span class="sxs-lookup"><span data-stu-id="dcef0-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="dcef0-130">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcef0-130">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="dcef0-131">Instale o Git e Node. js executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcef0-131">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="dcef0-132">Instalar ferramentas adicionais de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="dcef0-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="dcef0-133">Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação de tooyour de aplicativo de exemplo hello Arduino quadro.</span><span class="sxs-lookup"><span data-stu-id="dcef0-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="dcef0-134">Instalar `gulp`, `device-discovery-cli` executando Olá comando no terminal Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcef0-134">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="dcef0-135">Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento adicional em macOS, consulte Olá [guia de solução de problemas] [ troubleshooting] para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="dcef0-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="dcef0-136">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dcef0-136">Install Visual Studio Code</span></span>
<span data-ttu-id="dcef0-137">[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dcef0-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="dcef0-138">O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="dcef0-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="dcef0-139">Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="dcef0-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="dcef0-140">Resumo</span><span class="sxs-lookup"><span data-stu-id="dcef0-140">Summary</span></span>
<span data-ttu-id="dcef0-141">Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="dcef0-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="dcef0-142">Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em seu quadro Arduino.</span><span class="sxs-lookup"><span data-stu-id="dcef0-142">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcef0-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dcef0-143">Next steps</span></span>
<span data-ttu-id="dcef0-144">[Criar e implantar o aplicativo de intermitência hello][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="dcef0-144">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md