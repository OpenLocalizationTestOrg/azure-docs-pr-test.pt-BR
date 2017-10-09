---
title: "Connect Intel Edison (C) tooAzure IoT - lição 2: ferramentas do Azure (Ubuntu) | Microsoft Docs"
description: Instale o Python e a CLI do Azure (Interface de Linha de Comando do Azure) no Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do azure, serviço de nuvem iot, nuvem arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 2463cb8e-5758-4d72-af98-62520d41f2f7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a7691c13d43aa6dfff24adf2b470728d5266713e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="0324e-104">Obtenha as ferramentas do Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="0324e-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0324e-105">[Windows 7 e posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="0324e-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="0324e-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="0324e-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="0324e-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="0324e-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="0324e-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="0324e-108">What you will do</span></span>
<span data-ttu-id="0324e-109">Instale hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="0324e-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="0324e-110">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="0324e-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0324e-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="0324e-111">What you will learn</span></span>
<span data-ttu-id="0324e-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="0324e-112">In this article, you will learn:</span></span>
* <span data-ttu-id="0324e-113">Como tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0324e-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="0324e-114">Como tooadd um subgrupo de IoT de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0324e-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0324e-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="0324e-115">What you need</span></span>
* <span data-ttu-id="0324e-116">Um computador Ubuntu com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="0324e-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="0324e-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="0324e-117">An active Azure subscription.</span></span> <span data-ttu-id="0324e-118">Se você não tiver uma conta, poderá criar uma [conta de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0324e-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="0324e-119">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0324e-119">Install hello Azure CLI</span></span>
<span data-ttu-id="0324e-120">Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas do Azure, permitindo que você toowork diretamente do seu tooprovision de linha de comando e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="0324e-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="0324e-121">tooinstall hello mais recente CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="0324e-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="0324e-122">Olá executar comandos em uma janela de terminal a seguir.</span><span class="sxs-lookup"><span data-stu-id="0324e-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="0324e-123">Pode levar cinco minutos tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0324e-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="0324e-124">Verificar a instalação de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0324e-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="0324e-125">Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="0324e-125">You should see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="0324e-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="0324e-127">Summary</span></span>
<span data-ttu-id="0324e-128">Você instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0324e-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="0324e-129">A próxima tarefa é toocreate Olá seu hub IoT do Azure e a identidade do dispositivo usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0324e-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0324e-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0324e-130">Next steps</span></span>
<span data-ttu-id="0324e-131">[Criar seu Hub IoT e registrar o Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="0324e-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
