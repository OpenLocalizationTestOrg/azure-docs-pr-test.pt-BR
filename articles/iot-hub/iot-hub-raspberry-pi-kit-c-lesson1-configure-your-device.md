---
title: "Conectar o Raspberry Pi (C) ao IoT do Azure - Lição 1: configurar dispositivo | Microsoft Docs"
description: Configure seu Raspberry Pi 3 para o primeiro uso e instale o SO Raspbian, um sistema operacional gratuito e otimizado para o hardware Raspberry Pi.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "instalação raspbian, download raspbian, como instalar raspbian, configuração raspbian, instalação raspbian raspberry pi, raspberry pi instalar so, instalação de placa sd raspberry pi, conexão raspberry pi, conectar-se ao raspberry pi, conectividade raspberry pi"
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
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="c0ef7-104">Configurar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="c0ef7-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c0ef7-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="c0ef7-105">What you will do</span></span>
<span data-ttu-id="c0ef7-106">Configurar o Pi para uso pela primeira vez e instalar o sistema operacional Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="c0ef7-107">Raspbian é um sistema operacional gratuito e otimizado para o hardware Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="c0ef7-108">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c0ef7-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c0ef7-109">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c0ef7-109">What you will learn</span></span>
<span data-ttu-id="c0ef7-110">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="c0ef7-110">In this article, you will learn:</span></span>

* <span data-ttu-id="c0ef7-111">Como instalar o Raspbian no Pi.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="c0ef7-112">Como ligar o Pi usando um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="c0ef7-113">Como conectar o Pi à rede usando um cabo Ethernet ou rede sem fio.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="c0ef7-114">Como adicionar um LED à placa universal e conectá-lo ao Pi.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c0ef7-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="c0ef7-115">What you need</span></span>
<span data-ttu-id="c0ef7-116">Para concluir esta operação, você precisará das seguintes partes do seu Kit de Início do Raspberry Pi 3:</span><span class="sxs-lookup"><span data-stu-id="c0ef7-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="c0ef7-117">A placa do Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="c0ef7-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="c0ef7-118">O cartão microSD de 16GB</span><span class="sxs-lookup"><span data-stu-id="c0ef7-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="c0ef7-119">A fonte de alimentação 2A de 5V com o cabo micro USB de 1,80 metros</span><span class="sxs-lookup"><span data-stu-id="c0ef7-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="c0ef7-120">A placa universal</span><span class="sxs-lookup"><span data-stu-id="c0ef7-120">The breadboard</span></span>
* <span data-ttu-id="c0ef7-121">Cabos do conector</span><span class="sxs-lookup"><span data-stu-id="c0ef7-121">Connector wires</span></span>
* <span data-ttu-id="c0ef7-122">Um resistor de 560 Ohm</span><span class="sxs-lookup"><span data-stu-id="c0ef7-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="c0ef7-123">Um LED 10 mm difuso</span><span class="sxs-lookup"><span data-stu-id="c0ef7-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="c0ef7-124">O cabo Ethernet</span><span class="sxs-lookup"><span data-stu-id="c0ef7-124">The Ethernet cable</span></span>

![Coisas em seu Kit de Início](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="c0ef7-126">Você também precisará de:</span><span class="sxs-lookup"><span data-stu-id="c0ef7-126">You also need:</span></span>

* <span data-ttu-id="c0ef7-127">Uma conexão com ou sem fio para que o Pi seja conectado.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="c0ef7-128">Um adaptador USB-SD ou cartão Mini-SD para gravar a imagem do sistema operacional no cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="c0ef7-129">Um computador executando o Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="c0ef7-130">O computador é usado para instalar o Raspbian no cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="c0ef7-131">Uma conexão com a Internet para baixar as ferramentas e o software necessários.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="c0ef7-132">Instalar o Raspbian no cartão MicroSD</span><span class="sxs-lookup"><span data-stu-id="c0ef7-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="c0ef7-133">Preparar o cartão microSD para instalação da imagem do Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="c0ef7-134">Baixe o Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="c0ef7-135">[Baixe](https://www.raspberrypi.org/downloads/raspbian/) o arquivo zip do Raspbian Jessie com Pixel.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="c0ef7-136">Extraia a imagem do Raspbian em uma pasta no computador.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="c0ef7-137">Instale o Raspbian no cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="c0ef7-138">[Baixe](https://www.etcher.io) e instale o utilitário gravador de cartão SD Etcher.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="c0ef7-139">Execute o Etcher e selecione a imagem do Raspbian extraída na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="c0ef7-140">Selecione a unidade de cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="c0ef7-141">Observação que o Etcher talvez já tenha selecionado a unidade correta.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="c0ef7-142">Clique em **Flash** para instalar o Raspbian no cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="c0ef7-143">Remova o cartão microSD do computador após a conclusão.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="c0ef7-144">É seguro remover o cartão microSD diretamente porque o Etcher ejeta ou desmonta automaticamente o cartão microSD após a conclusão.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="c0ef7-145">Insira o cartão microSD no seu Pi.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-145">Insert the microSD card into your Pi.</span></span>

![Insira o cartão SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="c0ef7-147">Ativar o Pi</span><span class="sxs-lookup"><span data-stu-id="c0ef7-147">Turn on Pi</span></span>
<span data-ttu-id="c0ef7-148">Ligue o Pi usando o cabo micro USB e a fonte de alimentação.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Ligar](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="c0ef7-150">É importante usar uma fonte de alimentação do kit que tenha pelo menos 2A para confirmar que o Raspberry será alimentado com capacidade suficiente para funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="c0ef7-151">Habilitar SSH</span><span class="sxs-lookup"><span data-stu-id="c0ef7-151">Enable SSH</span></span>
<span data-ttu-id="c0ef7-152">Da versão de novembro de 2016 em diante, o Raspbian tem o servidor SSH desabilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="c0ef7-153">Você precisa habilitá-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-153">You need to enable it manually.</span></span> <span data-ttu-id="c0ef7-154">Você pode consultar as [instruções oficiais](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou conectar um monitor e ir para **Preferências-> Configuração do Raspberry Pi** para habilitar o SSH.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="c0ef7-155">Conectar o Raspberry Pi 3 à rede</span><span class="sxs-lookup"><span data-stu-id="c0ef7-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="c0ef7-156">Você pode conectar o Pi a uma rede com ou sem fio.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="c0ef7-157">Verifique se o Pi está conectado à mesma rede que o computador.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="c0ef7-158">Por exemplo, você pode conectar o Pi no mesmo comutador que o computador está conectado.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="c0ef7-159">Conectar a uma rede com fio</span><span class="sxs-lookup"><span data-stu-id="c0ef7-159">Connect to a wired network</span></span>
<span data-ttu-id="c0ef7-160">Use o cabo Ethernet para conectar o Pi à sua rede com fio.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="c0ef7-161">Os dois LEDs no Pi serão ligados se a conexão for estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Conectar-se usando um cabo Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="c0ef7-163">Conectar a uma rede sem fio</span><span class="sxs-lookup"><span data-stu-id="c0ef7-163">Connect to a wireless network</span></span>
<span data-ttu-id="c0ef7-164">Siga as [instruções](https://www.raspberrypi.org/learning/software-guide/wifi/) do Raspberry Pi Foundation para conectar o Pi à sua rede sem fio.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="c0ef7-165">Essas instruções exigem que você primeiro conecte um monitor e um teclado ao Pi.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="c0ef7-166">Conectar o LED ao Pi</span><span class="sxs-lookup"><span data-stu-id="c0ef7-166">Connect the LED to Pi</span></span>
<span data-ttu-id="c0ef7-167">Para concluir essa tarefa, use a [placa universal](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), os cabos do conector, o LED e o resistor.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="c0ef7-168">Conecte-os às portas [GPIO](https://www.raspberrypi.org/documentation/usage/gpio/) (entrada/saída de uso geral) do seu Pi.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Placa universal, LED e Resistor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="c0ef7-170">Conecte o segmento mais curto do LED no **GPIO GND (Pino 6)**.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="c0ef7-171">Conecte o segmento mais longo do LED em um segmento do resistor.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="c0ef7-172">Conecte o outro segmento do resistor no **GPIO 4 (Pino 7)**.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="c0ef7-173">Observe que a polaridade do LED é importante.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="c0ef7-174">Essa configuração de polaridade é conhecida como Ativo – Baixo.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-174">This polarity setting is commonly known as Active Low.</span></span>

![Pinagem](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="c0ef7-176">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="c0ef7-176">Congratulations!</span></span> <span data-ttu-id="c0ef7-177">Você configurou seu Pi com êxito.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="c0ef7-178">Resumo</span><span class="sxs-lookup"><span data-stu-id="c0ef7-178">Summary</span></span>
<span data-ttu-id="c0ef7-179">Neste artigo, você aprendeu como configurar o Pi ao instalar o Raspbian, a conectar o Pi a uma rede e a conectar um LED ao Pi.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="c0ef7-180">Observe que o LED ainda não está aceso.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="c0ef7-181">Na próxima tarefa, você instalará as ferramentas e o software necessários para preparar a execução de um aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="c0ef7-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![O hardware está pronto](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="c0ef7-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c0ef7-183">Next steps</span></span>
[<span data-ttu-id="c0ef7-184">Obter as ferramentas</span><span class="sxs-lookup"><span data-stu-id="c0ef7-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

