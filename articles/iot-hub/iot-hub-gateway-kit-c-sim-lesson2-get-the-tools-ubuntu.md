---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 2: obter ferramentas (Ubuntu) | Microsoft Docs"
description: "Instalar as ferramentas de saudação e software Olá no computador host executando o Ubuntu, crie um hub IoT e registrar seu dispositivo no hub IoT de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de iot, software de iot, serviço de nuvem de IoT, software de Internet das coisas, CLI do Azure, instalar o git no ubuntu, execução de gulp, instalar node js no ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 38c4d5d9cceec47758f0641cc26b631a7b19d37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="aa274-104">Obter ferramentas hello (16.04 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="aa274-104">Get hello tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa274-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="aa274-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="aa274-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="aa274-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="aa274-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="aa274-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="aa274-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="aa274-108">What you will do</span></span>

- <span data-ttu-id="aa274-109">Instalar o Git, Node.js, o Gulp e o Python.</span><span class="sxs-lookup"><span data-stu-id="aa274-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="aa274-110">Instale hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="aa274-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="aa274-111">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="aa274-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="aa274-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="aa274-112">What you will learn</span></span>

<span data-ttu-id="aa274-113">Nesta lição, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="aa274-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="aa274-114">Como tooinstall Node. js e Git.</span><span class="sxs-lookup"><span data-stu-id="aa274-114">How tooinstall Git and Node.js.</span></span>
  - <span data-ttu-id="aa274-115">O Git é um sistema de controle de versão distribuída de software livre.</span><span class="sxs-lookup"><span data-stu-id="aa274-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="aa274-116">aplicativo de exemplo Hello desta lição é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="aa274-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="aa274-117">O Node.js é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="aa274-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="aa274-118">Como ferramentas de desenvolvimento toouse NPM tooinstall Node. js.</span><span class="sxs-lookup"><span data-stu-id="aa274-118">How toouse NPM tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="aa274-119">versão mínima necessária de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="aa274-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="aa274-120">NPM é um dos gerenciadores de pacotes de saudação para Node. js.</span><span class="sxs-lookup"><span data-stu-id="aa274-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="aa274-121">Como tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="aa274-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="aa274-122">O Visual Studio Code é um editor de código-fonte de plataforma cruzada leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="aa274-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="aa274-123">Ele tem excelente suporte para depuração, controle Git incorporado, realce de sintaxe, preenchimento de código inteligente, trechos de código e também refatoração de código.</span><span class="sxs-lookup"><span data-stu-id="aa274-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="aa274-124">Como tooinstall Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="aa274-124">How tooinstall hello Azure CLI</span></span>
  - <span data-ttu-id="aa274-125">Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas para o Azure.</span><span class="sxs-lookup"><span data-stu-id="aa274-125">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="aa274-126">Trabalhar diretamente de uma linha de comando tooprovision e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="aa274-126">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="aa274-127">Como toouse Olá toocreate CLI do Azure com um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aa274-127">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aa274-128">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="aa274-128">What you need</span></span>

- <span data-ttu-id="aa274-129">Um toodownload de conexão de Internet Olá ferramentas e software.</span><span class="sxs-lookup"><span data-stu-id="aa274-129">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="aa274-130">Um computador que esteja executando o Ubuntu 16.04 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="aa274-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="aa274-131">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="aa274-131">Install Git and Node.js</span></span>

<span data-ttu-id="aa274-132">tooinstall Git e Node. js, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="aa274-132">tooinstall Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="aa274-133">Pressione `Ctrl + Alt + T` tooopen um terminal.</span><span class="sxs-lookup"><span data-stu-id="aa274-133">Press `Ctrl + Alt + T` tooopen a terminal.</span></span>
2. <span data-ttu-id="aa274-134">Execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa274-134">Run hello following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="aa274-135">Instalar ferramentas de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="aa274-135">Install Node.js development tools</span></span>

<span data-ttu-id="aa274-136">Você usa [gulp.js](http://gulpjs.com/) tooautomate implantação e execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="aa274-136">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="aa274-137">gulp tooinstall, execute Olá comando no terminal Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa274-137">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="aa274-138">Se você tiver problemas com a instalação do hello, consulte Olá [guia de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="aa274-138">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="aa274-139">Nó, NPM e Gulp são scripts de automação toorun necessário desenvolvidos no Node. js.</span><span class="sxs-lookup"><span data-stu-id="aa274-139">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="aa274-140">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="aa274-140">Install hello Azure CLI</span></span>

<span data-ttu-id="aa274-141">Olá tooinstall CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="aa274-141">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="aa274-142">Execute Olá terminal Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa274-142">Run hello following commands in hello terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="aa274-143">instalação de saudação pode levar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="aa274-143">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="aa274-144">Verificar a instalação de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa274-144">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="aa274-145">Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="aa274-145">You should see hello following output if hello installation is successful.</span></span>
<span data-ttu-id="aa274-146">![Verificar a instalação da CLI do Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="aa274-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="aa274-147">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="aa274-147">Install Visual Studio Code</span></span>

<span data-ttu-id="aa274-148">Usar código do Visual Studio posteriormente em arquivos de configuração do hello tooedit tutorial.</span><span class="sxs-lookup"><span data-stu-id="aa274-148">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="aa274-149">[Baixe](https://code.visualstudio.com/docs/setup/linux) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="aa274-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="aa274-150">Resumo</span><span class="sxs-lookup"><span data-stu-id="aa274-150">Summary</span></span>

<span data-ttu-id="aa274-151">Instalar todas as ferramentas de saudação necessárias e software no computador host.</span><span class="sxs-lookup"><span data-stu-id="aa274-151">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="aa274-152">A próxima tarefa é toouse Olá CLI do Azure toocreate um hub IoT e registrar seu dispositivo em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aa274-152">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa274-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa274-153">Next steps</span></span>
[<span data-ttu-id="aa274-154">Criar um Hub IoT e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="aa274-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
