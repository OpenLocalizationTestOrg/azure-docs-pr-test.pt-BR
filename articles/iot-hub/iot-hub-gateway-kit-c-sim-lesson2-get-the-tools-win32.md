---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 2: obter ferramentas (Windows) | Microsoft Docs"
description: "Instalar as ferramentas de saudação e software Olá no computador host executando o Windows, crie um hub IoT e registrar seu dispositivo no hub IoT de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de IoT, software de IoT, serviço de nuvem de IoT, software de Internet das Coisas, CLI do Azure, instalar o git no windows, executar gulp, instalar node js no windows, instalar npm no windows, instalar Python no windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="e9dff-104">Obter ferramentas hello (Windows 7 e posterior)</span><span class="sxs-lookup"><span data-stu-id="e9dff-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9dff-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="e9dff-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="e9dff-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e9dff-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="e9dff-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="e9dff-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="e9dff-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="e9dff-108">What you will do</span></span>

- <span data-ttu-id="e9dff-109">Instalar o Git, Node.js, o Gulp e o Python.</span><span class="sxs-lookup"><span data-stu-id="e9dff-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="e9dff-110">Instale hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="e9dff-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="e9dff-111">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e9dff-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e9dff-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="e9dff-112">What you will learn</span></span>

<span data-ttu-id="e9dff-113">Nesta lição, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="e9dff-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="e9dff-114">Como tooinstall [Git](https://git-scm.com/) e [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="e9dff-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="e9dff-115">O Git é um sistema de controle de versão distribuída de software livre.</span><span class="sxs-lookup"><span data-stu-id="e9dff-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="e9dff-116">aplicativo de exemplo Hello desta lição é armazenado no Git.</span><span class="sxs-lookup"><span data-stu-id="e9dff-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="e9dff-117">O Node.js é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="e9dff-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="e9dff-118">Como toouse [NPM](https://www.npmjs.com/) ferramentas de desenvolvimento tooinstall Node. js.</span><span class="sxs-lookup"><span data-stu-id="e9dff-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="e9dff-119">versão mínima necessária de saudação do Node. js é 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="e9dff-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="e9dff-120">NPM é um dos gerenciadores de pacotes de saudação para Node. js.</span><span class="sxs-lookup"><span data-stu-id="e9dff-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="e9dff-121">Como tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e9dff-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="e9dff-122">O Visual Studio Code é um editor de código-fonte de plataforma cruzada leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="e9dff-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e9dff-123">Ele tem excelente suporte para depuração, controle Git incorporado, realce de sintaxe, preenchimento de código inteligente, trechos de código e também refatoração de código.</span><span class="sxs-lookup"><span data-stu-id="e9dff-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="e9dff-124">Como tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="e9dff-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="e9dff-125">Python é uma linguagem de programação para fins gerais amplamente utilizada, de alto nível, interpretada e dinâmica.</span><span class="sxs-lookup"><span data-stu-id="e9dff-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="e9dff-126">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9dff-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="e9dff-127">Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas para o Azure.</span><span class="sxs-lookup"><span data-stu-id="e9dff-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="e9dff-128">Trabalhar diretamente de uma linha de comando tooprovision e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="e9dff-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="e9dff-129">Como toouse Olá toocreate CLI do Azure com um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e9dff-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e9dff-130">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="e9dff-130">What you need</span></span>

- <span data-ttu-id="e9dff-131">Um toodownload de conexão de Internet Olá ferramentas e software.</span><span class="sxs-lookup"><span data-stu-id="e9dff-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="e9dff-132">Um computador com Windows.</span><span class="sxs-lookup"><span data-stu-id="e9dff-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="e9dff-133">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="e9dff-133">Install Git and Node.js</span></span>

<span data-ttu-id="e9dff-134">Clique Olá toodownload links a seguir e instale o Git e LTS Node. js para Windows.</span><span class="sxs-lookup"><span data-stu-id="e9dff-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="e9dff-135">Obtenha o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="e9dff-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="e9dff-136">Obtenha o Node.js LTS para o Windows</span><span class="sxs-lookup"><span data-stu-id="e9dff-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="e9dff-137">Instalar ferramentas de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="e9dff-137">Install Node.js development tools</span></span>

<span data-ttu-id="e9dff-138">Você usa [gulp.js](http://gulpjs.com/) tooautomate implantação e execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="e9dff-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="e9dff-139">Pressione `Windows + R`, tipo `cmd` e pressione `Enter` tooopen uma janela de Prompt de comando, e, em seguida, Olá executar comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9dff-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="e9dff-140">Se você tiver problemas com a instalação do hello, consulte Olá [guia de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="e9dff-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="e9dff-141">Nó, NPM e Gulp são scripts de automação toorun necessário desenvolvidos no Node. js.</span><span class="sxs-lookup"><span data-stu-id="e9dff-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="e9dff-142">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="e9dff-142">Install Python</span></span>

<span data-ttu-id="e9dff-143">Você pode escolher entre Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="e9dff-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="e9dff-144">Neste tutorial, usamos o Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="e9dff-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="e9dff-145">Se você já tiver instalado o python, vá toohello próxima seção.</span><span class="sxs-lookup"><span data-stu-id="e9dff-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="e9dff-146">Obter o Python para Windows</span><span class="sxs-lookup"><span data-stu-id="e9dff-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="e9dff-147">Você também precisa de caminho de saudação tooadd pastas Olá onde Python.exe e pip.exe estão instalados toohello sistema `PATH` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="e9dff-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="e9dff-148">Por padrão, python.exe é instalado em `C:\Python27` e pip.exe é instalado em `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="e9dff-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="e9dff-149">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e9dff-149">Install hello Azure CLI</span></span>

<span data-ttu-id="e9dff-150">Olá tooinstall CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e9dff-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="e9dff-151">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="e9dff-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="e9dff-152">Instale Olá CLI do Azure executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9dff-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="e9dff-153">instalação de saudação pode levar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e9dff-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="e9dff-154">Verificar a instalação de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9dff-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="e9dff-155">Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e9dff-155">You should see hello following output if hello installation is successful.</span></span>

   ![Verificar a instalação da CLI do Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="e9dff-157">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e9dff-157">Install Visual Studio Code</span></span>

<span data-ttu-id="e9dff-158">Usar código do Visual Studio posteriormente em arquivos de configuração do hello tooedit tutorial.</span><span class="sxs-lookup"><span data-stu-id="e9dff-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="e9dff-159">[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e9dff-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="e9dff-160">Resumo</span><span class="sxs-lookup"><span data-stu-id="e9dff-160">Summary</span></span>

<span data-ttu-id="e9dff-161">Instalar todas as ferramentas de saudação necessárias e software no computador host.</span><span class="sxs-lookup"><span data-stu-id="e9dff-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="e9dff-162">A próxima tarefa é toouse Olá CLI do Azure toocreate um hub IoT e registrar seu dispositivo em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e9dff-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9dff-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9dff-163">Next steps</span></span>
[<span data-ttu-id="e9dff-164">Criar um Hub IoT e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="e9dff-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
