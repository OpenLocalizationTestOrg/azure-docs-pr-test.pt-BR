---
title: "Conectar Raspberry Pi (C) ao IoT do Azure - Lição 2: ferramentas do Azure (Windows) | Microsoft Docs"
description: "Instale o Python e a interface de linha de comando do Azure (CLI do Azure) no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem do iot, cli do azure"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aa96000cb676c088a90f2b3d45c159913185a2e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="be817-104">Obtenha as ferramentas do Azure (Windows 7 e superior)</span><span class="sxs-lookup"><span data-stu-id="be817-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be817-105">Windows 7 e superior</span><span class="sxs-lookup"><span data-stu-id="be817-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="be817-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="be817-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="be817-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="be817-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="be817-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="be817-108">What you will do</span></span>
<span data-ttu-id="be817-109">Instale o Python e a Interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="be817-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="be817-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="be817-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="be817-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="be817-111">What you will learn</span></span>
<span data-ttu-id="be817-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="be817-112">In this article, you will learn:</span></span>
* <span data-ttu-id="be817-113">Como instalar o Python.</span><span class="sxs-lookup"><span data-stu-id="be817-113">How to install Python.</span></span>
* <span data-ttu-id="be817-114">Como instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="be817-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="be817-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="be817-115">What you need</span></span>
* <span data-ttu-id="be817-116">Um computador Windows com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="be817-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="be817-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="be817-117">An active Azure subscription.</span></span> <span data-ttu-id="be817-118">Se não tiver uma conta do Azure, crie uma [conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="be817-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="be817-119">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="be817-119">Install Python</span></span>
<span data-ttu-id="be817-120">[Instale o Python](https://www.python.org/downloads/) no seu computador Windows.</span><span class="sxs-lookup"><span data-stu-id="be817-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="be817-121">Você pode instalar o Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="be817-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="be817-122">Esse tutorial se baseia no Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="be817-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="be817-123">Se você já tiver instalado o Python, vá para a próxima seção e instale a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="be817-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="be817-124">Você também precisa adicionar o caminho das pastas em que python.exe e pip.exe estão instalados na variável de ambiente `PATH` do sistema.</span><span class="sxs-lookup"><span data-stu-id="be817-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="be817-125">Por padrão, python.exe é instalado em `C:\Python27` e pip.exe é instalado em `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="be817-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="be817-126">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="be817-126">Install the Azure CLI</span></span>
<span data-ttu-id="be817-127">A CLI do Azure fornece uma experiência de linha de comando multiplataforma do Azure.</span><span class="sxs-lookup"><span data-stu-id="be817-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="be817-128">Você trabalha diretamente a partir de sua linha de comando para provisionar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="be817-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="be817-129">Para instalar a CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="be817-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="be817-130">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="be817-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="be817-131">Execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="be817-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="be817-132">Verifique a instalação executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="be817-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="be817-133">Você verá a seguinte saída se a instalação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="be817-133">You see the following output if the installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="be817-135">Resumo</span><span class="sxs-lookup"><span data-stu-id="be817-135">Summary</span></span>
<span data-ttu-id="be817-136">Você instalou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="be817-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="be817-137">Sua próxima tarefa é criar sua identidade de dispositivo e Hub IoT do Azure usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="be817-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be817-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be817-138">Next steps</span></span>
[<span data-ttu-id="be817-139">Criar seu Hub IoT e registrar seu Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="be817-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

