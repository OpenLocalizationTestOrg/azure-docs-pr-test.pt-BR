---
title: "Conecte-se Arduino tooAzure IoT - lição 2: ferramentas do Azure (Windows) | Microsoft Docs"
description: "Instale o Python e hello Azure interface de linha de comando (CLI do Azure) no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do azure, serviço de nuvem iot, nuvem arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 70dfff14-4be1-468d-9919-e40f4bead308
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9b891224ff3974d9ce5382eb983470d5d41bcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="58510-104">Obtenha as ferramentas do Azure (Windows 7 e superior)</span><span class="sxs-lookup"><span data-stu-id="58510-104">Get Azure tools (Windows 7 and later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="58510-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="58510-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="58510-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="58510-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="58510-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="58510-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="58510-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="58510-108">What you will do</span></span>

<span data-ttu-id="58510-109">Instale o Python e hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="58510-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="58510-110">Se você tiver problemas, procure por soluções em Olá [página de solução](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) para seu quadro Adafruit difusão M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="58510-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="58510-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="58510-111">What you will learn</span></span>
<span data-ttu-id="58510-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="58510-112">In this article, you will learn:</span></span>
* <span data-ttu-id="58510-113">Como tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="58510-113">How tooinstall Python.</span></span>
* <span data-ttu-id="58510-114">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="58510-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="58510-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="58510-115">What you need</span></span>
* <span data-ttu-id="58510-116">Um computador Windows com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="58510-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="58510-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="58510-117">An active Azure subscription.</span></span> <span data-ttu-id="58510-118">Se não tiver uma conta do Azure, crie uma [conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="58510-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="58510-119">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="58510-119">Install Python</span></span>
<span data-ttu-id="58510-120">[Instale o Python](https://www.python.org/downloads/) no seu computador Windows.</span><span class="sxs-lookup"><span data-stu-id="58510-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="58510-121">Você pode instalar o Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="58510-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="58510-122">Esse tutorial se baseia no Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="58510-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="58510-123">Se você já tiver instalado o Python, vá toohello próxima seção e instale Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="58510-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="58510-124">Você também precisa de caminho de saudação tooadd pastas Olá onde python.exe e pip.exe estão instalados toohello sistema `PATH` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="58510-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="58510-125">Por padrão, python.exe é instalado em `C:\Python27` e pip.exe é instalado em `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="58510-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="58510-126">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="58510-126">Install hello Azure CLI</span></span>
<span data-ttu-id="58510-127">Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas para o Azure.</span><span class="sxs-lookup"><span data-stu-id="58510-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="58510-128">Trabalhar diretamente no seu tooprovision de linha de comando e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="58510-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="58510-129">Olá tooinstall CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="58510-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="58510-130">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="58510-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="58510-131">Execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="58510-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="58510-132">Verificar a instalação de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="58510-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="58510-133">Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="58510-133">You see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito][output]

## <a name="summary"></a><span data-ttu-id="58510-135">Resumo</span><span class="sxs-lookup"><span data-stu-id="58510-135">Summary</span></span>
<span data-ttu-id="58510-136">Você instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="58510-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="58510-137">A próxima tarefa toocreate sua identidade de dispositivo e o hub IoT do Azure usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="58510-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58510-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58510-138">Next steps</span></span>
<span data-ttu-id="58510-139">[Criar seu Hub IoT e registrar sua placa Arduino][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="58510-139">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_win.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md