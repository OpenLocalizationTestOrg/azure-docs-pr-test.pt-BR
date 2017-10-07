---
title: "Conecte-se framboesa Pi (nó) tooAzure IoT - lição 2: obter ferramentas (Ubuntu) | Microsoft Docs"
description: Instale o Python e hello Azure interface de linha de comando (CLI do Azure) no Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "serviço de nuvem do iot, cli do azure"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2f98923a-5274-4220-87d4-77ac8beb4d0f
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0adf91bef41f502e1333fdcc75cfb2fe912364c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="eaf91-104">Obtenha as ferramentas do Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="eaf91-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eaf91-105">Windows 7 e superior</span><span class="sxs-lookup"><span data-stu-id="eaf91-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="eaf91-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="eaf91-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="eaf91-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="eaf91-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="eaf91-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="eaf91-108">What you will do</span></span>
<span data-ttu-id="eaf91-109">Instale hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="eaf91-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="eaf91-110">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="eaf91-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eaf91-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="eaf91-111">What you will learn</span></span>
<span data-ttu-id="eaf91-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="eaf91-112">In this article, you will learn:</span></span>
* <span data-ttu-id="eaf91-113">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf91-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="eaf91-114">Como tooadd um subgrupo de IoT de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf91-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eaf91-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="eaf91-115">What you need</span></span>
* <span data-ttu-id="eaf91-116">Um computador Ubuntu com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="eaf91-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="eaf91-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf91-117">An active Azure subscription.</span></span> <span data-ttu-id="eaf91-118">Se você não tiver uma conta, poderá criar uma [conta de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="eaf91-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="eaf91-119">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="eaf91-119">Install hello Azure CLI</span></span>
<span data-ttu-id="eaf91-120">Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas do Azure, permitindo que você toowork diretamente do seu tooprovision de linha de comando e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="eaf91-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command-line tooprovision and manage resources.</span></span>

<span data-ttu-id="eaf91-121">tooinstall hello mais recente CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="eaf91-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="eaf91-122">Olá executar comandos em uma janela de terminal a seguir.</span><span class="sxs-lookup"><span data-stu-id="eaf91-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="eaf91-123">Pode levar cinco minutos tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf91-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="eaf91-124">Verificar a instalação de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="eaf91-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="eaf91-125">Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="eaf91-125">You should see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="eaf91-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="eaf91-127">Summary</span></span>
<span data-ttu-id="eaf91-128">Você instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf91-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="eaf91-129">A próxima tarefa é toocreate Olá seu hub IoT do Azure e a identidade do dispositivo usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf91-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eaf91-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eaf91-130">Next steps</span></span>
[<span data-ttu-id="eaf91-131">Criar seu Hub IoT e registrar seu Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="eaf91-131">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

