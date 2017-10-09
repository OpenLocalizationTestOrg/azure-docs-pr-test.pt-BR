---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 2: obter ferramentas (macOS) | Microsoft Docs"
description: "Instalar as ferramentas no computador Mac, crie um hub IoT e registrar seu dispositivo no hub IoT de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de IoT, software de IoT, serviço de nuvem de IoT, software de Internet das Coisas, CLI do Azure, instalar o Python no Mac, instalar o git no Ubuntu, execução de Gulp, instalar Node.js em Mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="1adb4-104">Obter ferramentas hello (MacOS)</span><span class="sxs-lookup"><span data-stu-id="1adb4-104">Get hello tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1adb4-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="1adb4-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="1adb4-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="1adb4-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="1adb4-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="1adb4-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="1adb4-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="1adb4-108">What you will do</span></span>

- <span data-ttu-id="1adb4-109">Instalar o Git, Node.js, o Gulp e o Python.</span><span class="sxs-lookup"><span data-stu-id="1adb4-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="1adb4-110">Instale hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="1adb4-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="1adb4-111">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1adb4-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1adb4-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="1adb4-112">What you will learn</span></span>

<span data-ttu-id="1adb4-113">Nesta lição, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="1adb4-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="1adb4-114">Como tooinstall [Git](https://git-scm.com/) e [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="1adb4-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="1adb4-115">O Git é um sistema de controle de versão distribuída de software livre.</span><span class="sxs-lookup"><span data-stu-id="1adb4-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="1adb4-116">aplicativo de exemplo Hello desta lição é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="1adb4-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="1adb4-117">O Node.js é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="1adb4-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="1adb4-118">Como toouse [NPM](https://www.npmjs.com/) ferramentas de desenvolvimento tooinstall Node. js.</span><span class="sxs-lookup"><span data-stu-id="1adb4-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="1adb4-119">versão mínima necessária de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="1adb4-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="1adb4-120">NPM é um dos gerenciadores de pacotes de saudação para Node. js.</span><span class="sxs-lookup"><span data-stu-id="1adb4-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="1adb4-121">Como tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1adb4-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="1adb4-122">O Visual Studio Code é um editor de código-fonte de plataforma cruzada leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="1adb4-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="1adb4-123">Ele tem excelente suporte para depuração, controle Git incorporado, realce de sintaxe, preenchimento de código inteligente, trechos de código e também refatoração de código.</span><span class="sxs-lookup"><span data-stu-id="1adb4-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="1adb4-124">Como tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="1adb4-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="1adb4-125">Python é uma linguagem de programação para fins gerais amplamente utilizada, de alto nível, interpretada e dinâmica.</span><span class="sxs-lookup"><span data-stu-id="1adb4-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="1adb4-126">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1adb4-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="1adb4-127">Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas para o Azure.</span><span class="sxs-lookup"><span data-stu-id="1adb4-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="1adb4-128">Trabalhar diretamente de uma linha de comando tooprovision e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="1adb4-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="1adb4-129">Como toouse Olá toocreate CLI do Azure com um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1adb4-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1adb4-130">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="1adb4-130">What you need</span></span>

- <span data-ttu-id="1adb4-131">Um toodownload de conexão de Internet Olá ferramentas e software.</span><span class="sxs-lookup"><span data-stu-id="1adb4-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="1adb4-132">Um computador Mac que esteja executando o OS X Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1adb4-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="1adb4-133">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="1adb4-133">Install Git and Node.js</span></span>

<span data-ttu-id="1adb4-134">tooinstall Git e Node. js, use o utilitário de gerenciamento de pacotes de Homebrew Olá seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1adb4-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="1adb4-135">[Baixar](http://brew.sh/) e instalar o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="1adb4-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="1adb4-136">Se você já tiver instalado o Homebrew, vá toostep 2.</span><span class="sxs-lookup"><span data-stu-id="1adb4-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="1adb4-137">Pressione `Cmd + Space` e digite `Terminal` tooopen um terminal.</span><span class="sxs-lookup"><span data-stu-id="1adb4-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="1adb4-138">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1adb4-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="1adb4-139">Instale o Git e Node. js executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1adb4-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="1adb4-140">Instalar ferramentas de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="1adb4-140">Install Node.js development tools</span></span>

<span data-ttu-id="1adb4-141">Você usa [gulp.js](http://gulpjs.com/) tooautomate implantação e execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="1adb4-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="1adb4-142">gulp tooinstall, execute Olá comando no terminal Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1adb4-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="1adb4-143">Se você tiver problemas com a instalação do hello, consulte Olá [guia de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="1adb4-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="1adb4-144">Nó, NPM e Gulp são scripts de automação toorun necessário desenvolvidos no Node. js.</span><span class="sxs-lookup"><span data-stu-id="1adb4-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="1adb4-145">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="1adb4-145">Install Python</span></span>

<span data-ttu-id="1adb4-146">Embora o Mac OS X venha com o Python 2.7, recomendamos que você instale o Python por meio do Homebrew.</span><span class="sxs-lookup"><span data-stu-id="1adb4-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="1adb4-147">Veja [Instalando Python no Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="1adb4-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="1adb4-148">Instale o Python e pip executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1adb4-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="1adb4-149">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1adb4-149">Install hello Azure CLI</span></span>

<span data-ttu-id="1adb4-150">Olá tooinstall CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1adb4-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="1adb4-151">Execute Olá terminal Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1adb4-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="1adb4-152">instalação de saudação pode levar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="1adb4-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="1adb4-153">Verificar a instalação de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1adb4-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="1adb4-154">Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="1adb4-154">You should see hello following output if hello installation is successful.</span></span>

   ![Verificar a instalação da CLI do Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="1adb4-156">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1adb4-156">Install Visual Studio Code</span></span>

<span data-ttu-id="1adb4-157">Usar código do Visual Studio posteriormente em arquivos de configuração do hello tooedit tutorial.</span><span class="sxs-lookup"><span data-stu-id="1adb4-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="1adb4-158">[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1adb4-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="1adb4-159">Resumo</span><span class="sxs-lookup"><span data-stu-id="1adb4-159">Summary</span></span>

<span data-ttu-id="1adb4-160">Instalar todas as ferramentas de saudação necessárias e software em seu computador Mac.</span><span class="sxs-lookup"><span data-stu-id="1adb4-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="1adb4-161">A próxima tarefa é toouse Olá CLI do Azure toocreate um hub IoT e registrar seu dispositivo em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1adb4-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1adb4-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1adb4-162">Next steps</span></span>
[<span data-ttu-id="1adb4-163">Criar um Hub IoT e registrar o dispositivo</span><span class="sxs-lookup"><span data-stu-id="1adb4-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
