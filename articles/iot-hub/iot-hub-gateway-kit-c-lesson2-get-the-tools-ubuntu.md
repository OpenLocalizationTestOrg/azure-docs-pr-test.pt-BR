---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 2: obter ferramentas (Ubuntu) | Microsoft Docs"
description: Instale as ferramentas e o software no computador host executando o Ubuntu, crie um Hub IoT e registrar seu dispositivo no Hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de iot, software de iot, serviço de nuvem de IoT, software de Internet das coisas, CLI do Azure, instalar o git no ubuntu, execução de gulp, instalar node js no ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 234b60e1f8eaff52ce07f54d4d12de2421cc1a52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="632e9-104">Obter as ferramentas (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="632e9-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="632e9-105">Windows 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="632e9-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="632e9-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="632e9-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="632e9-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="632e9-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="632e9-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="632e9-108">What you will do</span></span>

- <span data-ttu-id="632e9-109">Instalar o Git, Node.js, o Gulp e o Python.</span><span class="sxs-lookup"><span data-stu-id="632e9-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="632e9-110">Instalar a interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="632e9-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="632e9-111">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="632e9-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="632e9-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="632e9-112">What you will learn</span></span>

<span data-ttu-id="632e9-113">Nesta lição, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="632e9-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="632e9-114">Como instalar o Git e o Node.js.</span><span class="sxs-lookup"><span data-stu-id="632e9-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="632e9-115">O Git é um sistema de controle de versão distribuída de software livre.</span><span class="sxs-lookup"><span data-stu-id="632e9-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="632e9-116">O aplicativo de exemplo para esta lição está armazenado em Git.</span><span class="sxs-lookup"><span data-stu-id="632e9-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="632e9-117">O Node.js é um tempo de execução de JavaScript com um avançado ecossistema de pacote.</span><span class="sxs-lookup"><span data-stu-id="632e9-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="632e9-118">Como usar o NPM para instalar ferramentas de desenvolvimento do Node.js.</span><span class="sxs-lookup"><span data-stu-id="632e9-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="632e9-119">A versão mínima necessária do Node.js é a 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="632e9-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="632e9-120">O NPM é um dos gerenciadores de pacote para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="632e9-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="632e9-121">Como instalar o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="632e9-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="632e9-122">O Visual Studio Code é um editor de código-fonte de plataforma cruzada leve mas poderoso para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="632e9-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="632e9-123">Ele tem excelente suporte para depuração, controle Git incorporado, realce de sintaxe, preenchimento de código inteligente, trechos de código e também refatoração de código.</span><span class="sxs-lookup"><span data-stu-id="632e9-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="632e9-124">Como instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="632e9-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="632e9-125">A CLI do Azure fornece uma experiência de linha de comando multiplataforma do Azure.</span><span class="sxs-lookup"><span data-stu-id="632e9-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="632e9-126">Você trabalha diretamente de uma linha de comando para provisionar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="632e9-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="632e9-127">Como usar a CLI do Azure para criar um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="632e9-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="632e9-128">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="632e9-128">What you need</span></span>

- <span data-ttu-id="632e9-129">Uma conexão com a Internet para baixar as ferramentas e o software.</span><span class="sxs-lookup"><span data-stu-id="632e9-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="632e9-130">Um computador que esteja executando o Ubuntu 16.04 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="632e9-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="632e9-131">Instalar o Git e o Node.js</span><span class="sxs-lookup"><span data-stu-id="632e9-131">Install Git and Node.js</span></span>

<span data-ttu-id="632e9-132">Para instalar o Git e Node.js, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="632e9-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="632e9-133">Pressione `Ctrl + Alt + T` para abrir um terminal.</span><span class="sxs-lookup"><span data-stu-id="632e9-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="632e9-134">Execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="632e9-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="632e9-135">Instalar ferramentas de desenvolvimento do Node.js</span><span class="sxs-lookup"><span data-stu-id="632e9-135">Install Node.js development tools</span></span>

<span data-ttu-id="632e9-136">Você usa o [gulp.js](http://gulpjs.com/) para automatizar a implantação e execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="632e9-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="632e9-137">Para instalar o gulp, execute o seguinte comando no terminal:</span><span class="sxs-lookup"><span data-stu-id="632e9-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="632e9-138">Se você tiver problemas com a instalação, consulte o [guia de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) para obter soluções para problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="632e9-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="632e9-139">Nó, NPM e Gulp são necessários para executar os scripts de automação desenvolvidos no Node.js.</span><span class="sxs-lookup"><span data-stu-id="632e9-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="632e9-140">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="632e9-140">Install the Azure CLI</span></span>

<span data-ttu-id="632e9-141">Para instalar a CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="632e9-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="632e9-142">Execute os seguintes comandos no terminal:</span><span class="sxs-lookup"><span data-stu-id="632e9-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="632e9-143">A instalação pode levar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="632e9-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="632e9-144">Verifique a instalação executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="632e9-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="632e9-145">Se a instalação for bem-sucedida, você verá a seguinte saída.</span><span class="sxs-lookup"><span data-stu-id="632e9-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="632e9-146">![Verificar a instalação da CLI do Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="632e9-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="632e9-147">Instalar o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="632e9-147">Install Visual Studio Code</span></span>

<span data-ttu-id="632e9-148">Use o código do Visual Studio posteriormente no tutorial para editar arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="632e9-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="632e9-149">[Baixe](https://code.visualstudio.com/docs/setup/linux) e instale o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="632e9-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="632e9-150">Resumo</span><span class="sxs-lookup"><span data-stu-id="632e9-150">Summary</span></span>

<span data-ttu-id="632e9-151">Você instalou todos os softwares e as ferramentas necessárias no computador host.</span><span class="sxs-lookup"><span data-stu-id="632e9-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="632e9-152">A próxima tarefa é usar a CLI do Azure para criar um hub IoT e registrar seu dispositivo no seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="632e9-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="632e9-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="632e9-153">Next steps</span></span>
[<span data-ttu-id="632e9-154">Criar um Hub IoT e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="632e9-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
