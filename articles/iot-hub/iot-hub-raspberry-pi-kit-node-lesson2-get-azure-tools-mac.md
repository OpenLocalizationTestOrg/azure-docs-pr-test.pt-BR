---
title: "Conecte o Raspberry Pi (Nó) ao IoT do Azure - Lição 2: Obter ferramentas (Ubuntu) | Microsoft Docs"
description: Instale o Python e a interface de linha de comando do Azure (CLI do Azure) no macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "serviço de nuvem do iot, cli do azure"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 1814b703-2d81-45db-aff0-eb338c97f120
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 12a8c5b20724e747f3799960a0bd39b82d7fa6b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="bfaf6-104">Obtenha as ferramentas do Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="bfaf6-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfaf6-105">Windows 7 e superior</span><span class="sxs-lookup"><span data-stu-id="bfaf6-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="bfaf6-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="bfaf6-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="bfaf6-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="bfaf6-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="bfaf6-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="bfaf6-108">What you will do</span></span>
<span data-ttu-id="bfaf6-109">Instalar a interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="bfaf6-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="bfaf6-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bfaf6-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bfaf6-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="bfaf6-111">What you will learn</span></span>
<span data-ttu-id="bfaf6-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="bfaf6-112">In this article, you will learn:</span></span>
* <span data-ttu-id="bfaf6-113">Como instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="bfaf6-114">Como adicionar um subgrupo de IoT da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bfaf6-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="bfaf6-115">What you need</span></span>
* <span data-ttu-id="bfaf6-116">Um Mac com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="bfaf6-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-117">An active Azure subscription.</span></span> <span data-ttu-id="bfaf6-118">Se não tiver uma conta do Azure, você pode [criar uma conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="bfaf6-119">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="bfaf6-119">Install Python</span></span>
<span data-ttu-id="bfaf6-120">Embora o macOS venha com o Python 2.7 integrado, recomendamos que você instale o Python por meio do Homebrew.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="bfaf6-121">Consulte [Instalando Python no macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="bfaf6-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="bfaf6-122">Instale o Python e o pip executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bfaf6-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="bfaf6-123">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bfaf6-123">Install the Azure CLI</span></span>
<span data-ttu-id="bfaf6-124">A CLI do Azure fornece uma experiência de linha de comando multiplataforma do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="bfaf6-125">Você trabalha diretamente da linha de comando para provisionar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-125">You work directly from your command-line to provision and manage resources.</span></span> 

<span data-ttu-id="bfaf6-126">Para instalar a CLI do Azure mais recente, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="bfaf6-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="bfaf6-127">Execute os seguintes comandos em uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="bfaf6-128">Pode levar cinco minutos para instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="bfaf6-129">Verifique a instalação executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfaf6-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="bfaf6-130">Se a instalação for bem-sucedida, você verá a seguinte saída.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-130">You should see the following output if the installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="bfaf6-132">Resumo</span><span class="sxs-lookup"><span data-stu-id="bfaf6-132">Summary</span></span>
<span data-ttu-id="bfaf6-133">Você instalou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="bfaf6-134">Sua próxima tarefa é criar sua identidade de dispositivo e Hub IoT do Azure usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfaf6-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfaf6-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bfaf6-135">Next steps</span></span>
[<span data-ttu-id="bfaf6-136">Criar seu Hub IoT e registrar seu Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="bfaf6-136">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

