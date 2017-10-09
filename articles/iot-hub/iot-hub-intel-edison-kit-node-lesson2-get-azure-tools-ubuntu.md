---
title: "Conecte-se Edison Intel (nó) tooAzure IoT - lição 2: ferramentas do Azure (Ubuntu) | Microsoft Docs"
description: Instale o Python e a CLI do Azure (Interface de Linha de Comando do Azure) no Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do azure, serviço de nuvem iot, nuvem arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 6dcb34bf-54a3-4af0-ba89-95d5cfafceff
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca2996b779a4d3cde833c5f2824d19ec46241bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="7093b-104">Obtenha as ferramentas do Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="7093b-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="7093b-105">[Windows 7 e posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="7093b-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="7093b-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="7093b-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="7093b-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="7093b-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7093b-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="7093b-108">What you will do</span></span>
<span data-ttu-id="7093b-109">Instale hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="7093b-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="7093b-110">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="7093b-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7093b-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7093b-111">What you will learn</span></span>
<span data-ttu-id="7093b-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="7093b-112">In this article, you will learn:</span></span>
* <span data-ttu-id="7093b-113">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7093b-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="7093b-114">Como tooadd um subgrupo de IoT de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7093b-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7093b-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7093b-115">What you need</span></span>
* <span data-ttu-id="7093b-116">Um computador Ubuntu com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="7093b-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="7093b-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7093b-117">An active Azure subscription.</span></span> <span data-ttu-id="7093b-118">Se você não tiver uma conta, poderá criar uma [conta de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="7093b-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="7093b-119">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7093b-119">Install hello Azure CLI</span></span>
<span data-ttu-id="7093b-120">Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas do Azure, permitindo que você toowork diretamente do seu tooprovision de linha de comando e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="7093b-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="7093b-121">tooinstall hello mais recente CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="7093b-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="7093b-122">Olá executar comandos em uma janela de terminal a seguir.</span><span class="sxs-lookup"><span data-stu-id="7093b-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="7093b-123">Pode levar cinco minutos tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7093b-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="7093b-124">Verificar a instalação de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7093b-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="7093b-125">Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="7093b-125">You should see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="7093b-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="7093b-127">Summary</span></span>
<span data-ttu-id="7093b-128">Você instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7093b-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="7093b-129">A próxima tarefa é toocreate Olá seu hub IoT do Azure e a identidade do dispositivo usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7093b-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7093b-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7093b-130">Next steps</span></span>
<span data-ttu-id="7093b-131">[Criar seu Hub IoT e registrar o Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="7093b-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
