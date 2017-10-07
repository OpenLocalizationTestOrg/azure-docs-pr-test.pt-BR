---
title: "Connect Arduino (C) tooAzure IoT - lição 1: Configurar dispositivo | Microsoft Docs"
description: Configure o Adafruit Feather M0 WiFi para o primeiro uso.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configurado, conecte-se arduino toopc, arduino de instalação, arduino board"
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
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="d294b-104">Configurar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="d294b-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d294b-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="d294b-105">What you will do</span></span>
<span data-ttu-id="d294b-106">Configure seu quadro Adafruit difusão M0 WiFi Arduino para uso pela primeira vez com a montagem de quadro hello, ligar.</span><span class="sxs-lookup"><span data-stu-id="d294b-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="d294b-107">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d294b-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d294b-108">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="d294b-108">What you need</span></span>
<span data-ttu-id="d294b-109">toocomplete essa operação, você precisa Olá partes a seguir para o Adafruit difusão M0 WiFi Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="d294b-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="d294b-110">Olá Adafruit difusão M0 WiFi board</span><span class="sxs-lookup"><span data-stu-id="d294b-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="d294b-111">Um tooType Micro B um cabo</span><span class="sxs-lookup"><span data-stu-id="d294b-111">A Micro B tooType A USB cable</span></span>

![kit][kit]

<span data-ttu-id="d294b-113">Você também precisará de:</span><span class="sxs-lookup"><span data-stu-id="d294b-113">You also need:</span></span>

* <span data-ttu-id="d294b-114">Um computador executando o Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="d294b-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="d294b-115">Uma conexão sem fio para seu tooconnect de quadro Arduino para.</span><span class="sxs-lookup"><span data-stu-id="d294b-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="d294b-116">Uma ferramenta de configuração de toodownload de conexão de Internet.</span><span class="sxs-lookup"><span data-stu-id="d294b-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d294b-117">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="d294b-117">What you will learn</span></span>
<span data-ttu-id="d294b-118">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="d294b-118">In this article, you will learn:</span></span>

* <span data-ttu-id="d294b-119">Como tooassemble sua placa Arduino e power-a para Olá seguintes lições.</span><span class="sxs-lookup"><span data-stu-id="d294b-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="d294b-120">Como as permissões de porta serial tooadd no Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d294b-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="d294b-121">Conectar o computador de tooyour Arduino board</span><span class="sxs-lookup"><span data-stu-id="d294b-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="d294b-122">Conecte cabo micro Olá Olá superior micro porta.</span><span class="sxs-lookup"><span data-stu-id="d294b-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Porta micro USB superior][top-micro-usb-port]

2. <span data-ttu-id="d294b-124">Plug Olá outra extremidade do cabo USB em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d294b-124">Plug hello other end of USB cable into your computer.</span></span>

   ![USB do computador][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="d294b-126">Adicionar permissões de porta serial no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d294b-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="d294b-127">Você pode ignorar esta seção se usar Windows ou macOS.</span><span class="sxs-lookup"><span data-stu-id="d294b-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="d294b-128">Para Ubuntu, você precisa Olá etapas toomake se usuário do linux normal de saudação tem Olá permissões toooperate na porta USB Olá seu quadro Arduino a seguir.</span><span class="sxs-lookup"><span data-stu-id="d294b-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="d294b-129">Agora, como usuário normal do terminal:</span><span class="sxs-lookup"><span data-stu-id="d294b-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="d294b-130">Você verá algo semelhante a:</span><span class="sxs-lookup"><span data-stu-id="d294b-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="d294b-131">Olá "0" pode ser um número diferente ou várias entradas poderá ser retornadas.</span><span class="sxs-lookup"><span data-stu-id="d294b-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="d294b-132">Dados de caso de saudação primeiro Olá precisamos é `uucp`, Olá segundo é `dialout`, que é o proprietário do grupo de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="d294b-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="d294b-133">Adicione usuário toohello toohello grupo:</span><span class="sxs-lookup"><span data-stu-id="d294b-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="d294b-134">Onde `group-name` dados Olá encontrada na primeira etapa de Olá, e `username` é o nome de usuário do linux.</span><span class="sxs-lookup"><span data-stu-id="d294b-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="d294b-135">Será necessário toolog sair e entrar novamente para essa alteração tootake efeito e instalação Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="d294b-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="d294b-136">Resumo</span><span class="sxs-lookup"><span data-stu-id="d294b-136">Summary</span></span>
<span data-ttu-id="d294b-137">Neste artigo, você aprendeu como tooconfigure seu quadro Arduino.</span><span class="sxs-lookup"><span data-stu-id="d294b-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="d294b-138">Olá próxima tarefa é o software em preparação para a execução de um aplicativo de exemplo em seu quadro Arduino e ferramentas necessárias do tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="d294b-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![O hardware está pronto][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="d294b-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d294b-140">Next steps</span></span>
<span data-ttu-id="d294b-141">[Obter ferramentas Olá][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="d294b-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md