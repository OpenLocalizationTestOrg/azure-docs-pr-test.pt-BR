---
title: "Conecte o Arduino ao IoT do Azure - Lição 2: Ferramentas do Azure (Ubuntu) | Microsoft Docs"
description: Instale o Python e a CLI do Azure (Interface de Linha de Comando do Azure) no Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do azure, serviço de nuvem iot, nuvem arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a2f83e59a37abc3f44e770b22ac089b88481a6a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="5f818-104">Obtenha as ferramentas do Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="5f818-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="5f818-105">[Windows 7 ou posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="5f818-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="5f818-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="5f818-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="5f818-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="5f818-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5f818-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="5f818-108">What you will do</span></span>

<span data-ttu-id="5f818-109">Instalar a interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="5f818-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="5f818-110">Se tiver problemas, procure por soluções na [página de solução de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) de sua placa Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="5f818-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5f818-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="5f818-111">What you will learn</span></span>
<span data-ttu-id="5f818-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="5f818-112">In this article, you will learn:</span></span>
* <span data-ttu-id="5f818-113">Como instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f818-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="5f818-114">Como adicionar um subgrupo de IoT da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f818-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5f818-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="5f818-115">What you need</span></span>
* <span data-ttu-id="5f818-116">Um computador Ubuntu com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="5f818-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="5f818-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f818-117">An active Azure subscription.</span></span> <span data-ttu-id="5f818-118">Se você não tiver uma conta, poderá criar uma [conta de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5f818-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="5f818-119">Instalar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5f818-119">Install the Azure CLI</span></span>
<span data-ttu-id="5f818-120">A CLI do Azure fornece uma experiência de linha de comando multiplataforma para o Azure, permitindo que você trabalhe diretamente da linha de comando para provisionar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="5f818-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="5f818-121">Para instalar a CLI do Azure mais recente, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="5f818-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="5f818-122">Execute os seguintes comandos em uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="5f818-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="5f818-123">Pode levar cinco minutos para instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f818-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="5f818-124">Verifique a instalação executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f818-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="5f818-125">Se a instalação for bem-sucedida, você verá a seguinte saída.</span><span class="sxs-lookup"><span data-stu-id="5f818-125">You should see the following output if the installation is successful.</span></span>

![Saída que indica êxito][output]

## <a name="summary"></a><span data-ttu-id="5f818-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="5f818-127">Summary</span></span>
<span data-ttu-id="5f818-128">Você instalou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f818-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="5f818-129">Sua próxima tarefa é criar sua identidade de dispositivo e Hub IoT do Azure usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f818-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f818-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5f818-130">Next steps</span></span>
<span data-ttu-id="5f818-131">[Criar seu Hub IoT e registrar sua placa Arduino][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="5f818-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md