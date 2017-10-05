---
title: "Conectar o Arduino (C) ao IoT do Azure - Lição 1: configurar dispositivo | Microsoft Docs"
description: Configure o Adafruit Feather M0 WiFi para o primeiro uso.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "configurar arduino, conectar arduino ao pc, configuração arduino, placa arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="fd6c3-104">Configurar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="fd6c3-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fd6c3-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="fd6c3-105">What you will do</span></span>
<span data-ttu-id="fd6c3-106">Configure sua placa Adafruit Feather M0 WiFi Arduino para o primeiro uso montando a placa e ligando-a.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span></span> <span data-ttu-id="fd6c3-107">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="fd6c3-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fd6c3-108">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="fd6c3-108">What you need</span></span>
<span data-ttu-id="fd6c3-109">Para concluir esta operação, você precisará das seguintes partes do seu Kit de início do Adafruit Feather M0 WiFi:</span><span class="sxs-lookup"><span data-stu-id="fd6c3-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="fd6c3-110">A placa Adafruit Feather M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="fd6c3-110">The Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="fd6c3-111">Um cabo USB do tipo Micro B para Tipo A</span><span class="sxs-lookup"><span data-stu-id="fd6c3-111">A Micro B to Type A USB cable</span></span>

![kit][kit]

<span data-ttu-id="fd6c3-113">Você também precisará de:</span><span class="sxs-lookup"><span data-stu-id="fd6c3-113">You also need:</span></span>

* <span data-ttu-id="fd6c3-114">Um computador executando o Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="fd6c3-115">Uma conexão sem fio com a qual a placa Arduino se conectará.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-115">A wireless connection for your Arduino board to connect to.</span></span>
* <span data-ttu-id="fd6c3-116">Uma conexão com a Internet para baixar a ferramenta de configuração.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-116">An Internet connection to download configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fd6c3-117">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="fd6c3-117">What you will learn</span></span>
<span data-ttu-id="fd6c3-118">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="fd6c3-118">In this article, you will learn:</span></span>

* <span data-ttu-id="fd6c3-119">Como montar sua placa Arduino e ligá-la para as lições seguintes.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-119">How to assemble your Arduino board and power it up for the following lessons.</span></span>
* <span data-ttu-id="fd6c3-120">Como adicionar permissões de porta serial no Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-120">How to add serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-to-your-computer"></a><span data-ttu-id="fd6c3-121">Conectar sua placa Arduino ao computador</span><span class="sxs-lookup"><span data-stu-id="fd6c3-121">Connect your Arduino board to your computer</span></span>

1. <span data-ttu-id="fd6c3-122">Conecte o cabo micro USB à porta micro USB superior.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-122">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Porta micro USB superior][top-micro-usb-port]

2. <span data-ttu-id="fd6c3-124">Conecte a outra extremidade do cabo USB ao computador.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-124">Plug the other end of USB cable into your computer.</span></span>

   ![USB do computador][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="fd6c3-126">Adicionar permissões de porta serial no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="fd6c3-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="fd6c3-127">Você pode ignorar esta seção se usar Windows ou macOS.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="fd6c3-128">Para o Ubuntu, você precisa das seguintes etapas para certificar-se de que o usuário normal do Linux tenha as permissões para operar na porta USB da placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span></span>

1. <span data-ttu-id="fd6c3-129">Agora, como usuário normal do terminal:</span><span class="sxs-lookup"><span data-stu-id="fd6c3-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="fd6c3-130">Você verá algo semelhante a:</span><span class="sxs-lookup"><span data-stu-id="fd6c3-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="fd6c3-131">O "0" pode ser um número diferente ou várias entradas podem ser retornadas.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-131">The "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="fd6c3-132">No primeiro caso, os dados de que precisamos são `uucp`, no segundo são `dialout`, que é o proprietário do grupo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span></span>

2. <span data-ttu-id="fd6c3-133">Adicionar usuário ao grupo:</span><span class="sxs-lookup"><span data-stu-id="fd6c3-133">Add user to the to the group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="fd6c3-134">Em que `group-name` são os dados encontrados na primeira etapa e `username` é o nome de usuário do Linux.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="fd6c3-135">Você precisará fazer logoff e fazer logon novamente para que esta alteração entre em vigor e a instalação seja concluída.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-135">You will need to log out and in again for this change to take effect and complete the setup.</span></span>

## <a name="summary"></a><span data-ttu-id="fd6c3-136">Resumo</span><span class="sxs-lookup"><span data-stu-id="fd6c3-136">Summary</span></span>
<span data-ttu-id="fd6c3-137">Neste artigo, você aprendeu como configurar sua placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-137">In this article, you’ve learned how to configure your Arduino board.</span></span> <span data-ttu-id="fd6c3-138">A próxima tarefa é instalar as ferramentas e o software necessários para preparar a execução de um aplicativo de exemplo na placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="fd6c3-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![O hardware está pronto][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="fd6c3-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd6c3-140">Next steps</span></span>
<span data-ttu-id="fd6c3-141">[Obter as ferramentas][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="fd6c3-141">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md