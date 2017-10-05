---
title: "Conectar o Intel Edison (Nó) ao IoT do Azure - Lição 2: ferramentas do Azure (Ubuntu) | Microsoft Docs"
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
ms.openlocfilehash: 65248e14d0ea05a44efe76e66e1ef519285982b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="5e45e-104">Obtenha as ferramentas do Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="5e45e-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5e45e-105">[Windows 7 e posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="5e45e-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="5e45e-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="5e45e-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="5e45e-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="5e45e-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5e45e-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="5e45e-108">What you will do</span></span>
<span data-ttu-id="5e45e-109">Instalar a interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="5e45e-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="5e45e-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5e45e-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e45e-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="5e45e-111">What you will learn</span></span>
<span data-ttu-id="5e45e-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="5e45e-112">In this article, you will learn:</span></span>
* <span data-ttu-id="5e45e-113">Como instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e45e-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="5e45e-114">Como adicionar um subgrupo de IoT da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e45e-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e45e-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="5e45e-115">What you need</span></span>
* <span data-ttu-id="5e45e-116">Um computador Ubuntu com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="5e45e-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="5e45e-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e45e-117">An active Azure subscription.</span></span> <span data-ttu-id="5e45e-118">Se você não tiver uma conta, poderá criar uma [conta de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5e45e-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="5e45e-119">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5e45e-119">Install the Azure CLI</span></span>
<span data-ttu-id="5e45e-120">A CLI do Azure fornece uma experiência de linha de comando multiplataforma para o Azure, permitindo que você trabalhe diretamente da linha de comando para provisionar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="5e45e-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="5e45e-121">Para instalar a CLI do Azure mais recente, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="5e45e-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="5e45e-122">Execute os seguintes comandos em uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="5e45e-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="5e45e-123">Pode levar cinco minutos para instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e45e-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="5e45e-124">Verifique a instalação executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5e45e-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="5e45e-125">Se a instalação for bem-sucedida, você verá a seguinte saída.</span><span class="sxs-lookup"><span data-stu-id="5e45e-125">You should see the following output if the installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="5e45e-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="5e45e-127">Summary</span></span>
<span data-ttu-id="5e45e-128">Você instalou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e45e-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="5e45e-129">Sua próxima tarefa é criar sua identidade de dispositivo e Hub IoT do Azure usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e45e-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e45e-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e45e-130">Next steps</span></span>
<span data-ttu-id="5e45e-131">[Criar seu Hub IoT e registrar o Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="5e45e-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
