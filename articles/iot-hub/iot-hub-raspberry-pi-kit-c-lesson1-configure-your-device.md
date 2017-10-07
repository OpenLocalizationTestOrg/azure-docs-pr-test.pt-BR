---
title: "Connect Raspberry PI (C) tooAzure IoT - lição 1: Configurar dispositivo | Microsoft Docs"
description: "Configure framboesa Pi 3 para uso pela primeira vez e instale Olá OS Raspbian, um sistema operacional livre que é otimizado para Olá hardware framboesa Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspbian de instalação, download raspbian, como tooinstall raspbian, raspbian framboesa, a instalação pi instalação raspbian, framboesa pi instalar sistema operacional, framboesa pi sd cartão instalar, framboesa pi connect, conectividade de pi pi, framboesa tooraspberry de se conectar"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="293eb-104">Configurar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="293eb-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="293eb-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="293eb-105">What you will do</span></span>
<span data-ttu-id="293eb-106">Configurar Pi para uso pela primeira vez e instalar o sistema de operacional Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="293eb-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="293eb-107">Raspbian é um sistema operacional livre que é otimizado para Olá hardware framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="293eb-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="293eb-108">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="293eb-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="293eb-109">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="293eb-109">What you will learn</span></span>
<span data-ttu-id="293eb-110">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="293eb-110">In this article, you will learn:</span></span>

* <span data-ttu-id="293eb-111">Como tooinstall Raspbian em Pi.</span><span class="sxs-lookup"><span data-stu-id="293eb-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="293eb-112">Como toopower o Pi usando um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="293eb-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="293eb-113">Como tooconnect Pi toohello de rede usando um cabo Ethernet ou uma rede sem fio.</span><span class="sxs-lookup"><span data-stu-id="293eb-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="293eb-114">Como tooadd toohello um LED breadboard e conectá-lo tooPi.</span><span class="sxs-lookup"><span data-stu-id="293eb-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="293eb-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="293eb-115">What you need</span></span>
<span data-ttu-id="293eb-116">toocomplete essa operação, você precisa Olá seguir partes de seu framboesa Pi 3 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="293eb-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="293eb-117">Olá framboesa Pi 3 board</span><span class="sxs-lookup"><span data-stu-id="293eb-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="293eb-118">cartão de 16 GB microSD Olá</span><span class="sxs-lookup"><span data-stu-id="293eb-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="293eb-119">Olá 5 volt 2 amp alimentação com cabo micro-6 pés Olá</span><span class="sxs-lookup"><span data-stu-id="293eb-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="293eb-120">breadboard Olá</span><span class="sxs-lookup"><span data-stu-id="293eb-120">hello breadboard</span></span>
* <span data-ttu-id="293eb-121">Cabos do conector</span><span class="sxs-lookup"><span data-stu-id="293eb-121">Connector wires</span></span>
* <span data-ttu-id="293eb-122">Um resistor de 560 Ohm</span><span class="sxs-lookup"><span data-stu-id="293eb-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="293eb-123">Um LED 10 mm difuso</span><span class="sxs-lookup"><span data-stu-id="293eb-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="293eb-124">Olá cabo Ethernet</span><span class="sxs-lookup"><span data-stu-id="293eb-124">hello Ethernet cable</span></span>

![Coisas em seu Kit de Início](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="293eb-126">Você também precisará de:</span><span class="sxs-lookup"><span data-stu-id="293eb-126">You also need:</span></span>

* <span data-ttu-id="293eb-127">Uma conexão com ou sem fio para tooconnect Pi para.</span><span class="sxs-lookup"><span data-stu-id="293eb-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="293eb-128">Um SD USB adaptador ou mini SD cartão tooburn Olá SO imagem no cartão microSD de saudação.</span><span class="sxs-lookup"><span data-stu-id="293eb-128">A USB-SD adapter or mini-SD card tooburn hello OS image onto hello microSD card.</span></span>
* <span data-ttu-id="293eb-129">Um computador executando o Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="293eb-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="293eb-130">computador Olá é usado tooinstall Raspbian no cartão microSD de saudação.</span><span class="sxs-lookup"><span data-stu-id="293eb-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="293eb-131">Um toodownload de conexão de Internet Olá ferramentas necessárias e software.</span><span class="sxs-lookup"><span data-stu-id="293eb-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="293eb-132">Instalar Raspbian no cartão MicroSD de saudação</span><span class="sxs-lookup"><span data-stu-id="293eb-132">Install Raspbian on hello MicroSD card</span></span>
<span data-ttu-id="293eb-133">Prepare um cartão microSD de saudação para a instalação da imagem de Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="293eb-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="293eb-134">Baixe o Raspbian.</span><span class="sxs-lookup"><span data-stu-id="293eb-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="293eb-135">[Baixar](https://www.raspberrypi.org/downloads/raspbian/) arquivo hello. zip Raspbian Jessie com pixels.</span><span class="sxs-lookup"><span data-stu-id="293eb-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="293eb-136">Extrai Olá Raspbian imagem tooa pasta do computador.</span><span class="sxs-lookup"><span data-stu-id="293eb-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="293eb-137">Instale Raspbian toohello microSD cartão.</span><span class="sxs-lookup"><span data-stu-id="293eb-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="293eb-138">[Baixar](https://www.etcher.io) e instale o utilitário de gravador Olá Etcher SD cartão.</span><span class="sxs-lookup"><span data-stu-id="293eb-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="293eb-139">Execute Etcher e selecione a imagem de Raspbian de saudação extraído na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="293eb-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="293eb-140">Selecione a unidade de cartão microSD hello.</span><span class="sxs-lookup"><span data-stu-id="293eb-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="293eb-141">Observe que Etcher talvez já selecionou unidade correta hello.</span><span class="sxs-lookup"><span data-stu-id="293eb-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="293eb-142">Clique em **Flash** tooinstall Raspbian toohello microSD cartão.</span><span class="sxs-lookup"><span data-stu-id="293eb-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="293eb-143">Remova o cartão microSD de saudação do seu computador quando a instalação for concluída.</span><span class="sxs-lookup"><span data-stu-id="293eb-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="293eb-144">É cartão de microSD tooremove seguro Olá diretamente porque Etcher automaticamente ejeta ou desmonta cartão microSD de saudação após a conclusão.</span><span class="sxs-lookup"><span data-stu-id="293eb-144">It is safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="293eb-145">Inserir cartão microSD de saudação a Pi.</span><span class="sxs-lookup"><span data-stu-id="293eb-145">Insert hello microSD card into your Pi.</span></span>

![Insira o cartão SD de saudação](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="293eb-147">Ativar o Pi</span><span class="sxs-lookup"><span data-stu-id="293eb-147">Turn on Pi</span></span>
<span data-ttu-id="293eb-148">Ative o Pi usando cabo USB da micro hello e fonte de alimentação hello.</span><span class="sxs-lookup"><span data-stu-id="293eb-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![Ligar](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="293eb-150">É importante toouse Olá de alimentação no kit de saudação que tenha pelo menos 2A toomake se seu framboesa tem suficiente toowork power corretamente.</span><span class="sxs-lookup"><span data-stu-id="293eb-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="293eb-151">Habilitar SSH</span><span class="sxs-lookup"><span data-stu-id="293eb-151">Enable SSH</span></span>
<span data-ttu-id="293eb-152">A partir do Olá versão de novembro de 2016, Raspbian tem o servidor SSH Olá desabilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="293eb-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="293eb-153">Você precisa tooenable-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="293eb-153">You need tooenable it manually.</span></span> <span data-ttu-id="293eb-154">Você pode consultar toohello [instruções oficiais](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou conectar um monitor e ir muito**Preferências -> Configuração de Pi framboesa** tooenable SSH.</span><span class="sxs-lookup"><span data-stu-id="293eb-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="293eb-155">Conectar a rede de toohello framboesa Pi 3</span><span class="sxs-lookup"><span data-stu-id="293eb-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="293eb-156">Você pode conectar tooa Pi com fio rede ou tooa sem fio.</span><span class="sxs-lookup"><span data-stu-id="293eb-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="293eb-157">Certifique-se de Pi é conectado toohello mesmo de rede do computador.</span><span class="sxs-lookup"><span data-stu-id="293eb-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="293eb-158">Por exemplo, você pode conectar toohello Pi que mesmo opção se o computador está conectado à.</span><span class="sxs-lookup"><span data-stu-id="293eb-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="293eb-159">Conecte-se tooa de rede com fio</span><span class="sxs-lookup"><span data-stu-id="293eb-159">Connect tooa wired network</span></span>
<span data-ttu-id="293eb-160">Use Olá Ethernet cabo tooconnect tooyour Pi rede com fio.</span><span class="sxs-lookup"><span data-stu-id="293eb-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="293eb-161">Olá dois LEDs no Pi ativar se conexão Olá for estabelecida.</span><span class="sxs-lookup"><span data-stu-id="293eb-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![Conectar-se usando um cabo Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="293eb-163">Conecte-se a rede sem fio tooa</span><span class="sxs-lookup"><span data-stu-id="293eb-163">Connect tooa wireless network</span></span>
<span data-ttu-id="293eb-164">Siga Olá [instruções](https://www.raspberrypi.org/learning/software-guide/wifi/) da rede sem fio do tooyour de Pi de tooconnect do hello framboesa Pi Foundation.</span><span class="sxs-lookup"><span data-stu-id="293eb-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="293eb-165">Essas instruções exigem que você toofirst conectar um monitor e um teclado tooPi.</span><span class="sxs-lookup"><span data-stu-id="293eb-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="293eb-166">Conecte-se tooPi Olá LED</span><span class="sxs-lookup"><span data-stu-id="293eb-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="293eb-167">toocomplete essa tarefa, use Olá [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), Olá fios do conector, Olá LED e Olá resistência.</span><span class="sxs-lookup"><span data-stu-id="293eb-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="293eb-168">Conecte-os toohello [geral de entrada/saída](https://www.raspberrypi.org/documentation/usage/gpio/) portas (GPIO) de Pi.</span><span class="sxs-lookup"><span data-stu-id="293eb-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Placa universal, LED e Resistor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="293eb-170">Conecte-se o lado mais curto de saudação do Olá LED muito**GPIO GND (Pin 6)**.</span><span class="sxs-lookup"><span data-stu-id="293eb-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="293eb-171">Conecte-se perna mais de saudação do hello LED tooone segmento de resistência Olá.</span><span class="sxs-lookup"><span data-stu-id="293eb-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="293eb-172">Conecte-se Olá outro segmento de resistência Olá muito**GPIO 4 (7 Pin)**.</span><span class="sxs-lookup"><span data-stu-id="293eb-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="293eb-173">Observe que polaridade Olá LED é importante.</span><span class="sxs-lookup"><span data-stu-id="293eb-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="293eb-174">Essa configuração de polaridade é conhecida como Ativo – Baixo.</span><span class="sxs-lookup"><span data-stu-id="293eb-174">This polarity setting is commonly known as Active Low.</span></span>

![Pinagem](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="293eb-176">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="293eb-176">Congratulations!</span></span> <span data-ttu-id="293eb-177">Você configurou seu Pi com êxito.</span><span class="sxs-lookup"><span data-stu-id="293eb-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="293eb-178">Resumo</span><span class="sxs-lookup"><span data-stu-id="293eb-178">Summary</span></span>
<span data-ttu-id="293eb-179">Neste artigo, você aprendeu como tooconfigure Pi instalando Raspbian, rede de tooa Pi conexão, e se conectar a um LED tooPi.</span><span class="sxs-lookup"><span data-stu-id="293eb-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="293eb-180">Observe que Olá que LED ainda não ativado.</span><span class="sxs-lookup"><span data-stu-id="293eb-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="293eb-181">Olá próxima tarefa é ferramentas do tooinstall Olá necessárias e software em preparação para a execução de um aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="293eb-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![O hardware está pronto](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="293eb-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="293eb-183">Next steps</span></span>
[<span data-ttu-id="293eb-184">Obter ferramentas Olá</span><span class="sxs-lookup"><span data-stu-id="293eb-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

