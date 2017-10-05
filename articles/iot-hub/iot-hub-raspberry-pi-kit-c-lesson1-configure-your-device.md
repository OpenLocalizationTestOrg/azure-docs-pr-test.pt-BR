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
# <a name="configure-your-device"></a>Configurar seu dispositivo
## <a name="what-you-will-do"></a>O que você fará
Configurar o Pi para uso pela primeira vez e instalar o sistema operacional Raspbian. Raspbian é um sistema operacional gratuito e otimizado para o hardware Raspberry Pi. Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:

* Como instalar o Raspbian no Pi.
* Como ligar o Pi usando um cabo USB.
* Como conectar o Pi à rede usando um cabo Ethernet ou rede sem fio.
* Como adicionar um LED à placa universal e conectá-lo ao Pi.

## <a name="what-you-need"></a>O que você precisa
Para concluir esta operação, você precisará das seguintes partes do seu Kit de Início do Raspberry Pi 3:

* A placa do Raspberry Pi 3
* O cartão microSD de 16GB
* A fonte de alimentação 2A de 5V com o cabo micro USB de 1,80 metros
* A placa universal
* Cabos do conector
* Um resistor de 560 Ohm
* Um LED 10 mm difuso
* O cabo Ethernet

![Coisas em seu Kit de Início](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Você também precisará de:

* Uma conexão com ou sem fio para que o Pi seja conectado.
* Um adaptador USB-SD ou cartão Mini-SD para gravar a imagem do sistema operacional no cartão microSD.
* Um computador executando o Windows, Mac ou Linux. O computador é usado para instalar o Raspbian no cartão microSD.
* Uma conexão com a Internet para baixar as ferramentas e o software necessários.

## <a name="install-raspbian-on-the-microsd-card"></a>Instalar o Raspbian no cartão MicroSD
Preparar o cartão microSD para instalação da imagem do Raspbian.

1. Baixe o Raspbian.
   1. [Baixe](https://www.raspberrypi.org/downloads/raspbian/) o arquivo zip do Raspbian Jessie com Pixel.
   2. Extraia a imagem do Raspbian em uma pasta no computador.
2. Instale o Raspbian no cartão microSD.
   1. [Baixe](https://www.etcher.io) e instale o utilitário gravador de cartão SD Etcher.
   2. Execute o Etcher e selecione a imagem do Raspbian extraída na etapa 1.
   3. Selecione a unidade de cartão microSD.
      Observação que o Etcher talvez já tenha selecionado a unidade correta.
   4. Clique em **Flash** para instalar o Raspbian no cartão microSD.
   5. Remova o cartão microSD do computador após a conclusão.
      É seguro remover o cartão microSD diretamente porque o Etcher ejeta ou desmonta automaticamente o cartão microSD após a conclusão.
   6. Insira o cartão microSD no seu Pi.

![Insira o cartão SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Ativar o Pi
Ligue o Pi usando o cabo micro USB e a fonte de alimentação.

![Ligar](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> É importante usar uma fonte de alimentação do kit que tenha pelo menos 2A para confirmar que o Raspberry será alimentado com capacidade suficiente para funcionar corretamente.

## <a name="enable-ssh"></a>Habilitar SSH
Da versão de novembro de 2016 em diante, o Raspbian tem o servidor SSH desabilitado por padrão. Você precisa habilitá-lo manualmente. Você pode consultar as [instruções oficiais](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou conectar um monitor e ir para **Preferências-> Configuração do Raspberry Pi** para habilitar o SSH.

## <a name="connect-raspberry-pi-3-to-the-network"></a>Conectar o Raspberry Pi 3 à rede
Você pode conectar o Pi a uma rede com ou sem fio. Verifique se o Pi está conectado à mesma rede que o computador. Por exemplo, você pode conectar o Pi no mesmo comutador que o computador está conectado.

### <a name="connect-to-a-wired-network"></a>Conectar a uma rede com fio
Use o cabo Ethernet para conectar o Pi à sua rede com fio. Os dois LEDs no Pi serão ligados se a conexão for estabelecida.

![Conectar-se usando um cabo Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a>Conectar a uma rede sem fio
Siga as [instruções](https://www.raspberrypi.org/learning/software-guide/wifi/) do Raspberry Pi Foundation para conectar o Pi à sua rede sem fio. Essas instruções exigem que você primeiro conecte um monitor e um teclado ao Pi.

## <a name="connect-the-led-to-pi"></a>Conectar o LED ao Pi
Para concluir essa tarefa, use a [placa universal](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), os cabos do conector, o LED e o resistor. Conecte-os às portas [GPIO](https://www.raspberrypi.org/documentation/usage/gpio/) (entrada/saída de uso geral) do seu Pi.

![Placa universal, LED e Resistor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Conecte o segmento mais curto do LED no **GPIO GND (Pino 6)**.
2. Conecte o segmento mais longo do LED em um segmento do resistor.
3. Conecte o outro segmento do resistor no **GPIO 4 (Pino 7)**.

Observe que a polaridade do LED é importante. Essa configuração de polaridade é conhecida como Ativo – Baixo.

![Pinagem](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Parabéns! Você configurou seu Pi com êxito.

## <a name="summary"></a>Resumo
Neste artigo, você aprendeu como configurar o Pi ao instalar o Raspbian, a conectar o Pi a uma rede e a conectar um LED ao Pi. Observe que o LED ainda não está aceso. Na próxima tarefa, você instalará as ferramentas e o software necessários para preparar a execução de um aplicativo de exemplo no Pi.

![O hardware está pronto](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Próximas etapas
[Obter as ferramentas](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

