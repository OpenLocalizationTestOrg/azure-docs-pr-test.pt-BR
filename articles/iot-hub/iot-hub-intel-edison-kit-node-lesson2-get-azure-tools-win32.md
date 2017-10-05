---
title: "Conectar o Intel Edison (Nó) ao IoT do Azure - Lição 2: ferramentas do Azure (Windows) | Microsoft Docs"
description: "Instale o Python e a interface de linha de comando do Azure (CLI do Azure) no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do azure, serviço de nuvem iot, nuvem arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 60631b54-6d2e-4e8a-88bf-7c2f8e7e1f29
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7257fe98fa1075456de620ca46b4e10c34e06574
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="e9559-104">Obtenha as ferramentas do Azure (Windows 7 e superior)</span><span class="sxs-lookup"><span data-stu-id="e9559-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e9559-105">[Windows 7 e posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="e9559-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="e9559-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="e9559-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="e9559-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="e9559-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e9559-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="e9559-108">What you will do</span></span>
<span data-ttu-id="e9559-109">Instale o Python e a Interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="e9559-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="e9559-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e9559-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e9559-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="e9559-111">What you will learn</span></span>
<span data-ttu-id="e9559-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="e9559-112">In this article, you will learn:</span></span>
* <span data-ttu-id="e9559-113">Como instalar o Python.</span><span class="sxs-lookup"><span data-stu-id="e9559-113">How to install Python.</span></span>
* <span data-ttu-id="e9559-114">Como instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9559-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e9559-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="e9559-115">What you need</span></span>
* <span data-ttu-id="e9559-116">Um computador Windows com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="e9559-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="e9559-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9559-117">An active Azure subscription.</span></span> <span data-ttu-id="e9559-118">Se não tiver uma conta do Azure, crie uma [conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e9559-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="e9559-119">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="e9559-119">Install Python</span></span>
<span data-ttu-id="e9559-120">[Instale o Python](https://www.python.org/downloads/) no seu computador Windows.</span><span class="sxs-lookup"><span data-stu-id="e9559-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="e9559-121">Você pode instalar o Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="e9559-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="e9559-122">Esse tutorial se baseia no Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="e9559-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="e9559-123">Se você já tiver instalado o Python, vá para a próxima seção e instale a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9559-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="e9559-124">Você também precisa adicionar o caminho das pastas em que python.exe e pip.exe estão instalados na variável de ambiente `PATH` do sistema.</span><span class="sxs-lookup"><span data-stu-id="e9559-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="e9559-125">Por padrão, python.exe é instalado em `C:\Python27` e pip.exe é instalado em `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="e9559-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="e9559-126">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e9559-126">Install the Azure CLI</span></span>
<span data-ttu-id="e9559-127">A CLI do Azure fornece uma experiência de linha de comando multiplataforma do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9559-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="e9559-128">Você trabalha diretamente a partir de sua linha de comando para provisionar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="e9559-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="e9559-129">Para instalar a CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e9559-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="e9559-130">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="e9559-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="e9559-131">Execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="e9559-131">Run the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="e9559-132">Verifique a instalação executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9559-132">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="e9559-133">Você verá a seguinte saída se a instalação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e9559-133">You see the following output if the installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="e9559-135">Resumo</span><span class="sxs-lookup"><span data-stu-id="e9559-135">Summary</span></span>
<span data-ttu-id="e9559-136">Você instalou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9559-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="e9559-137">Sua próxima tarefa é criar sua identidade de dispositivo e Hub IoT do Azure usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9559-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9559-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9559-138">Next steps</span></span>
<span data-ttu-id="e9559-139">[Criar seu Hub IoT e registrar o Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="e9559-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
