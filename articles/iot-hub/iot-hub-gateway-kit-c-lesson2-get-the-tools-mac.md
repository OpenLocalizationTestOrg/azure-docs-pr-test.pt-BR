---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 2: obter ferramentas (macOS) | Microsoft Docs"
description: Instalar as ferramentas no computador Mac, criar um Hub IoT e registrar seu dispositivo no Hub IoT.
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
ms.openlocfilehash: 07bc5f2cf6542273c334371b77520c674c5d2f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="321e6-104">Obter as ferramentas (MacOS)</span><span class="sxs-lookup"><span data-stu-id="321e6-104">Get the tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="321e6-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="321e6-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="321e6-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="321e6-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="321e6-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="321e6-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="321e6-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="321e6-108">What you will do</span></span>

- <span data-ttu-id="321e6-109">Instalar o Git, Node.js, o Gulp e o Python.</span><span class="sxs-lookup"><span data-stu-id="321e6-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="321e6-110">Instalar a interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="321e6-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="321e6-111">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="321e6-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="321e6-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="321e6-112">What you will learn</span></span>

<span data-ttu-id="321e6-113">Nesta lição, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="321e6-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="321e6-114">Como instalar o [Git](https://git-scm.com/) e o [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="321e6-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="321e6-115">O Git é um sistema de controle de versão distribuída de software livre.</span><span class="sxs-lookup"><span data-stu-id="321e6-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="321e6-116">O aplicativo de exemplo para esta lição está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="321e6-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="321e6-117">O Node.js é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="321e6-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="321e6-118">Como usar o [NPM](https://www.npmjs.com/) para instalar ferramentas de desenvolvimento do Node.js.</span><span class="sxs-lookup"><span data-stu-id="321e6-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="321e6-119">A versão mínima necessária do Node.js é a 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="321e6-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="321e6-120">O NPM é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="321e6-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="321e6-121">Como instalar o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="321e6-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="321e6-122">O Visual Studio Code é um editor de código-fonte de plataforma cruzada leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="321e6-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="321e6-123">Ele tem excelente suporte para depuração, controle Git incorporado, realce de sintaxe, preenchimento de código inteligente, trechos de código e também refatoração de código.</span><span class="sxs-lookup"><span data-stu-id="321e6-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="321e6-124">Como instalar o Python.</span><span class="sxs-lookup"><span data-stu-id="321e6-124">How to install Python.</span></span>
  - <span data-ttu-id="321e6-125">Python é uma linguagem de programação para fins gerais amplamente utilizada, de alto nível, interpretada e dinâmica.</span><span class="sxs-lookup"><span data-stu-id="321e6-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="321e6-126">Como instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="321e6-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="321e6-127">A CLI do Azure fornece uma experiência de linha de comando multiplataforma do Azure.</span><span class="sxs-lookup"><span data-stu-id="321e6-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="321e6-128">Você trabalha diretamente de uma linha de comando para provisionar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="321e6-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="321e6-129">Como usar a CLI do Azure para criar um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="321e6-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="321e6-130">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="321e6-130">What you need</span></span>

- <span data-ttu-id="321e6-131">Uma conexão com a Internet para baixar as ferramentas e o software.</span><span class="sxs-lookup"><span data-stu-id="321e6-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="321e6-132">Um computador Mac que esteja executando o OS X Yosemite (10.10) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="321e6-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="321e6-133">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="321e6-133">Install Git and Node.js</span></span>

<span data-ttu-id="321e6-134">Para instalar o Git e o Node.js, use o utilitário de gerenciamento de pacote Homebrew seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="321e6-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="321e6-135">[Baixar](http://brew.sh/) e instalar o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="321e6-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="321e6-136">Se você já tiver instalado o Homebrew, vá para a etapa 2.</span><span class="sxs-lookup"><span data-stu-id="321e6-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="321e6-137">Pressione `Cmd + Space` e digite `Terminal` para abrir um terminal.</span><span class="sxs-lookup"><span data-stu-id="321e6-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="321e6-138">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="321e6-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="321e6-139">Instale o Git e o Node.js executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="321e6-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="321e6-140">Instalar ferramentas de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="321e6-140">Install Node.js development tools</span></span>

<span data-ttu-id="321e6-141">Você usa o [gulp.js](http://gulpjs.com/) para automatizar a implantação e execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="321e6-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="321e6-142">Para instalar o gulp, execute o seguinte comando no terminal:</span><span class="sxs-lookup"><span data-stu-id="321e6-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="321e6-143">Se você tiver problemas com a instalação, consulte o [guia de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) para obter soluções para problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="321e6-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="321e6-144">Nó, NPM e Gulp são necessários para executar os scripts de automação desenvolvidos no Node.js.</span><span class="sxs-lookup"><span data-stu-id="321e6-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="321e6-145">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="321e6-145">Install Python</span></span>

<span data-ttu-id="321e6-146">Embora o Mac OS X venha com o Python 2.7, recomendamos que você instale o Python por meio do Homebrew.</span><span class="sxs-lookup"><span data-stu-id="321e6-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="321e6-147">Veja [Instalando Python no Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="321e6-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="321e6-148">Instale o Python e o pip executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="321e6-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="321e6-149">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="321e6-149">Install the Azure CLI</span></span>

<span data-ttu-id="321e6-150">Para instalar a CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="321e6-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="321e6-151">Execute os seguintes comandos no terminal:</span><span class="sxs-lookup"><span data-stu-id="321e6-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="321e6-152">A instalação pode levar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="321e6-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="321e6-153">Verifique a instalação executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="321e6-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="321e6-154">Se a instalação for bem-sucedida, você verá a seguinte saída.</span><span class="sxs-lookup"><span data-stu-id="321e6-154">You should see the following output if the installation is successful.</span></span>

   ![Verificar a instalação da CLI do Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="321e6-156">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="321e6-156">Install Visual Studio Code</span></span>

<span data-ttu-id="321e6-157">Use o código do Visual Studio posteriormente no tutorial para editar arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="321e6-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="321e6-158">[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="321e6-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="321e6-159">Resumo</span><span class="sxs-lookup"><span data-stu-id="321e6-159">Summary</span></span>

<span data-ttu-id="321e6-160">Você instalou todos os softwares e as ferramentas necessárias no computador Mac.</span><span class="sxs-lookup"><span data-stu-id="321e6-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="321e6-161">A próxima tarefa é usar a CLI do Azure para criar um hub IoT e registrar seu dispositivo no seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="321e6-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="321e6-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="321e6-162">Next steps</span></span>
[<span data-ttu-id="321e6-163">Criar um Hub IoT e registrar o dispositivo</span><span class="sxs-lookup"><span data-stu-id="321e6-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
