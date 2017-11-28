---
title: "Connect Intel Edison (C) tooAzure IoT - lição 2: ferramentas do Azure (macOS) | Microsoft Docs"
description: Instale o Python e a CLI do Azure (Interface de Linha de Comando do Azure) no macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "cli do azure, serviço de nuvem iot, nuvem arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0dfc9ff90e879d5fd03040016ac71a9fe4f4a744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="fb869-104">Obtenha as ferramentas do Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="fb869-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="fb869-105">[Windows 7 e posterior][windows]</span><span class="sxs-lookup"><span data-stu-id="fb869-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="fb869-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="fb869-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="fb869-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="fb869-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="fb869-108">O que você fará</span><span class="sxs-lookup"><span data-stu-id="fb869-108">What you will do</span></span>
<span data-ttu-id="fb869-109">Instale hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="fb869-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="fb869-110">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="fb869-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fb869-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="fb869-111">What you will learn</span></span>
<span data-ttu-id="fb869-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="fb869-112">In this article, you will learn:</span></span>
* <span data-ttu-id="fb869-113">Como tooinstall CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb869-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="fb869-114">Como tooadd um subgrupo de IoT de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb869-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fb869-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="fb869-115">What you need</span></span>
* <span data-ttu-id="fb869-116">Um Mac com conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="fb869-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="fb869-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb869-117">An active Azure subscription.</span></span> <span data-ttu-id="fb869-118">Se não tiver uma conta do Azure, você pode [criar uma conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="fb869-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="fb869-119">Instalar o Python</span><span class="sxs-lookup"><span data-stu-id="fb869-119">Install Python</span></span>
<span data-ttu-id="fb869-120">Embora macOS vem com Python 2.7 imediato saudação, recomendamos que você instale Python por meio de Homebrew.</span><span class="sxs-lookup"><span data-stu-id="fb869-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="fb869-121">Consulte [Instalando Python no macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="fb869-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="fb869-122">Instale o Python e pip executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb869-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="fb869-123">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="fb869-123">Install hello Azure CLI</span></span>
<span data-ttu-id="fb869-124">Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas para o Azure.</span><span class="sxs-lookup"><span data-stu-id="fb869-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="fb869-125">Trabalhar diretamente no seu tooprovision de linha de comando e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="fb869-125">You work directly from your command line tooprovision and manage resources.</span></span> 

<span data-ttu-id="fb869-126">tooinstall hello mais recente CLI do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="fb869-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="fb869-127">Olá executar comandos em uma janela de terminal a seguir.</span><span class="sxs-lookup"><span data-stu-id="fb869-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="fb869-128">Pode levar cinco minutos tooinstall Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb869-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="fb869-129">Verificar a instalação de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb869-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="fb869-130">Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="fb869-130">You should see hello following output if hello installation is successful.</span></span>

![Saída que indica êxito](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="fb869-132">Resumo</span><span class="sxs-lookup"><span data-stu-id="fb869-132">Summary</span></span>
<span data-ttu-id="fb869-133">Você instalou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb869-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="fb869-134">A próxima tarefa é toocreate sua identidade de dispositivo e o hub IoT do Azure usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb869-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb869-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb869-135">Next steps</span></span>
<span data-ttu-id="fb869-136">[Criar seu Hub IoT e registrar o Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="fb869-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
