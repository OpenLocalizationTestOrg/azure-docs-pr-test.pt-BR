---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 2: obter ferramentas (Windows) | Microsoft Docs"
description: Instale as ferramentas e o software no computador host executando o Windows, crie um Hub IoT e registre seu dispositivo no Hub IoT.
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
ms.openlocfilehash: ecedf5ef89677c73c5d9a3e5250eb9f45f6bad32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="1cecb-104">Obter as ferramentas do Azure (Windows 7 e superior)</span><span class="sxs-lookup"><span data-stu-id="1cecb-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1cecb-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="1cecb-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="1cecb-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="1cecb-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="1cecb-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="1cecb-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="1cecb-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="1cecb-108">What you will do</span></span>

- <span data-ttu-id="1cecb-109">Instalar o Git, Node.js, o Gulp e o Python.</span><span class="sxs-lookup"><span data-stu-id="1cecb-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="1cecb-110">Instalar a interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="1cecb-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="1cecb-111">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1cecb-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1cecb-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="1cecb-112">What you will learn</span></span>

<span data-ttu-id="1cecb-113">Nesta lição, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="1cecb-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="1cecb-114">Como instalar o [Git](https://git-scm.com/) e o [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="1cecb-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="1cecb-115">O Git é um sistema de controle de versão distribuída de software livre.</span><span class="sxs-lookup"><span data-stu-id="1cecb-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="1cecb-116">O aplicativo de exemplo para esta lição está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="1cecb-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="1cecb-117">O Node.js é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="1cecb-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="1cecb-118">Como usar o [NPM](https://www.npmjs.com/) para instalar ferramentas de desenvolvimento do Node.js.</span><span class="sxs-lookup"><span data-stu-id="1cecb-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="1cecb-119">A versão mínima necessária do Node.js é a 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="1cecb-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="1cecb-120">O NPM é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="1cecb-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="1cecb-121">Como instalar o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1cecb-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="1cecb-122">O Visual Studio Code é um editor de código-fonte de plataforma cruzada leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="1cecb-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="1cecb-123">Ele tem excelente suporte para depuração, controle Git incorporado, realce de sintaxe, preenchimento de código inteligente, trechos de código e também refatoração de código.</span><span class="sxs-lookup"><span data-stu-id="1cecb-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="1cecb-124">Como instalar o Python.</span><span class="sxs-lookup"><span data-stu-id="1cecb-124">How to install Python.</span></span>
  - <span data-ttu-id="1cecb-125">Python é uma linguagem de programação para fins gerais amplamente utilizada, de alto nível, interpretada e dinâmica.</span><span class="sxs-lookup"><span data-stu-id="1cecb-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="1cecb-126">Como instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1cecb-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="1cecb-127">A CLI do Azure fornece uma experiência de linha de comando multiplataforma do Azure.</span><span class="sxs-lookup"><span data-stu-id="1cecb-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="1cecb-128">Você trabalha diretamente de uma linha de comando para provisionar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="1cecb-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="1cecb-129">Como usar a CLI do Azure para criar um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1cecb-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1cecb-130">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="1cecb-130">What you need</span></span>

- <span data-ttu-id="1cecb-131">Uma conexão com a Internet para baixar as ferramentas e o software.</span><span class="sxs-lookup"><span data-stu-id="1cecb-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="1cecb-132">Um computador com Windows.</span><span class="sxs-lookup"><span data-stu-id="1cecb-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="1cecb-133">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="1cecb-133">Install Git and Node.js</span></span>

<span data-ttu-id="1cecb-134">Clique nos links a seguir para baixar e instalar o Git e o Node.js LTS para Windows.</span><span class="sxs-lookup"><span data-stu-id="1cecb-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="1cecb-135">Obtenha o Git para Windows</span><span class="sxs-lookup"><span data-stu-id="1cecb-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="1cecb-136">Obtenha o Node.js LTS para o Windows</span><span class="sxs-lookup"><span data-stu-id="1cecb-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="1cecb-137">Instalar ferramentas de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="1cecb-137">Install Node.js development tools</span></span>

<span data-ttu-id="1cecb-138">Você usa o [gulp.js](http://gulpjs.com/) para automatizar a implantação e execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="1cecb-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="1cecb-139">Pressione `Windows + R`, digite `cmd` e pressione `Enter` para abrir uma janela do prompt de comando como administrador e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1cecb-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="1cecb-140">Se você tiver problemas com a instalação, consulte o [guia de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) para obter soluções para problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="1cecb-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="1cecb-141">Nó, NPM e Gulp são necessários para executar os scripts de automação desenvolvidos no Node.js.</span><span class="sxs-lookup"><span data-stu-id="1cecb-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="1cecb-142">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="1cecb-142">Install Python</span></span>

<span data-ttu-id="1cecb-143">Você pode escolher entre Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="1cecb-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="1cecb-144">Neste tutorial, usamos o Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="1cecb-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="1cecb-145">Se você já tiver instalado o Python, vá para a próxima seção.</span><span class="sxs-lookup"><span data-stu-id="1cecb-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="1cecb-146">Obter o Python para Windows</span><span class="sxs-lookup"><span data-stu-id="1cecb-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="1cecb-147">Você também precisa adicionar o caminho das pastas em que Python.exe e pip.exe estão instalados na variável de ambiente `PATH` do sistema.</span><span class="sxs-lookup"><span data-stu-id="1cecb-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="1cecb-148">Por padrão, python.exe é instalado em `C:\Python27` e pip.exe é instalado em `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="1cecb-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="1cecb-149">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1cecb-149">Install the Azure CLI</span></span>

<span data-ttu-id="1cecb-150">Para instalar a CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1cecb-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="1cecb-151">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="1cecb-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="1cecb-152">Instale a CLI do Azure executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="1cecb-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="1cecb-153">A instalação pode levar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="1cecb-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="1cecb-154">Verifique a instalação executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1cecb-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="1cecb-155">Se a instalação for bem-sucedida, você verá a seguinte saída.</span><span class="sxs-lookup"><span data-stu-id="1cecb-155">You should see the following output if the installation is successful.</span></span>

   ![Verificar a instalação da CLI do Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="1cecb-157">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1cecb-157">Install Visual Studio Code</span></span>

<span data-ttu-id="1cecb-158">Use o código do Visual Studio posteriormente no tutorial para editar arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1cecb-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="1cecb-159">[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1cecb-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="1cecb-160">Resumo</span><span class="sxs-lookup"><span data-stu-id="1cecb-160">Summary</span></span>

<span data-ttu-id="1cecb-161">Você instalou todos os softwares e as ferramentas necessárias no computador host.</span><span class="sxs-lookup"><span data-stu-id="1cecb-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="1cecb-162">A próxima tarefa é usar a CLI do Azure para criar um hub IoT e registrar seu dispositivo no seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1cecb-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cecb-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1cecb-163">Next steps</span></span>
[<span data-ttu-id="1cecb-164">Criar um Hub IoT e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="1cecb-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
