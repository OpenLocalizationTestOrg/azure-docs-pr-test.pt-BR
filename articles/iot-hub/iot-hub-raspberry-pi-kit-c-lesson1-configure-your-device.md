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
# <a name="configure-your-device"></a>Configurar seu dispositivo
## <a name="what-you-will-do"></a>O que você fará
Configurar Pi para uso pela primeira vez e instalar o sistema de operacional Raspbian hello. Raspbian é um sistema operacional livre que é otimizado para Olá hardware framboesa Pi. Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:

* Como tooinstall Raspbian em Pi.
* Como toopower o Pi usando um cabo USB.
* Como tooconnect Pi toohello de rede usando um cabo Ethernet ou uma rede sem fio.
* Como tooadd toohello um LED breadboard e conectá-lo tooPi.

## <a name="what-you-need"></a>O que você precisa
toocomplete essa operação, você precisa Olá seguir partes de seu framboesa Pi 3 Starter Kit:

* Olá framboesa Pi 3 board
* cartão de 16 GB microSD Olá
* Olá 5 volt 2 amp alimentação com cabo micro-6 pés Olá
* breadboard Olá
* Cabos do conector
* Um resistor de 560 Ohm
* Um LED 10 mm difuso
* Olá cabo Ethernet

![Coisas em seu Kit de Início](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Você também precisará de:

* Uma conexão com ou sem fio para tooconnect Pi para.
* Um SD USB adaptador ou mini SD cartão tooburn Olá SO imagem no cartão microSD de saudação.
* Um computador executando o Windows, Mac ou Linux. computador Olá é usado tooinstall Raspbian no cartão microSD de saudação.
* Um toodownload de conexão de Internet Olá ferramentas necessárias e software.

## <a name="install-raspbian-on-hello-microsd-card"></a>Instalar Raspbian no cartão MicroSD de saudação
Prepare um cartão microSD de saudação para a instalação da imagem de Raspbian hello.

1. Baixe o Raspbian.
   1. [Baixar](https://www.raspberrypi.org/downloads/raspbian/) arquivo hello. zip Raspbian Jessie com pixels.
   2. Extrai Olá Raspbian imagem tooa pasta do computador.
2. Instale Raspbian toohello microSD cartão.
   1. [Baixar](https://www.etcher.io) e instale o utilitário de gravador Olá Etcher SD cartão.
   2. Execute Etcher e selecione a imagem de Raspbian de saudação extraído na etapa 1.
   3. Selecione a unidade de cartão microSD hello.
      Observe que Etcher talvez já selecionou unidade correta hello.
   4. Clique em **Flash** tooinstall Raspbian toohello microSD cartão.
   5. Remova o cartão microSD de saudação do seu computador quando a instalação for concluída.
      É cartão de microSD tooremove seguro Olá diretamente porque Etcher automaticamente ejeta ou desmonta cartão microSD de saudação após a conclusão.
   6. Inserir cartão microSD de saudação a Pi.

![Insira o cartão SD de saudação](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Ativar o Pi
Ative o Pi usando cabo USB da micro hello e fonte de alimentação hello.

![Ligar](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> É importante toouse Olá de alimentação no kit de saudação que tenha pelo menos 2A toomake se seu framboesa tem suficiente toowork power corretamente.

## <a name="enable-ssh"></a>Habilitar SSH
A partir do Olá versão de novembro de 2016, Raspbian tem o servidor SSH Olá desabilitado por padrão. Você precisa tooenable-lo manualmente. Você pode consultar toohello [instruções oficiais](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou conectar um monitor e ir muito**Preferências -> Configuração de Pi framboesa** tooenable SSH.

## <a name="connect-raspberry-pi-3-toohello-network"></a>Conectar a rede de toohello framboesa Pi 3
Você pode conectar tooa Pi com fio rede ou tooa sem fio. Certifique-se de Pi é conectado toohello mesmo de rede do computador. Por exemplo, você pode conectar toohello Pi que mesmo opção se o computador está conectado à.

### <a name="connect-tooa-wired-network"></a>Conecte-se tooa de rede com fio
Use Olá Ethernet cabo tooconnect tooyour Pi rede com fio. Olá dois LEDs no Pi ativar se conexão Olá for estabelecida.

![Conectar-se usando um cabo Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Conecte-se a rede sem fio tooa
Siga Olá [instruções](https://www.raspberrypi.org/learning/software-guide/wifi/) da rede sem fio do tooyour de Pi de tooconnect do hello framboesa Pi Foundation. Essas instruções exigem que você toofirst conectar um monitor e um teclado tooPi.

## <a name="connect-hello-led-toopi"></a>Conecte-se tooPi Olá LED
toocomplete essa tarefa, use Olá [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), Olá fios do conector, Olá LED e Olá resistência. Conecte-os toohello [geral de entrada/saída](https://www.raspberrypi.org/documentation/usage/gpio/) portas (GPIO) de Pi.

![Placa universal, LED e Resistor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Conecte-se o lado mais curto de saudação do Olá LED muito**GPIO GND (Pin 6)**.
2. Conecte-se perna mais de saudação do hello LED tooone segmento de resistência Olá.
3. Conecte-se Olá outro segmento de resistência Olá muito**GPIO 4 (7 Pin)**.

Observe que polaridade Olá LED é importante. Essa configuração de polaridade é conhecida como Ativo – Baixo.

![Pinagem](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Parabéns! Você configurou seu Pi com êxito.

## <a name="summary"></a>Resumo
Neste artigo, você aprendeu como tooconfigure Pi instalando Raspbian, rede de tooa Pi conexão, e se conectar a um LED tooPi. Observe que Olá que LED ainda não ativado. Olá próxima tarefa é ferramentas do tooinstall Olá necessárias e software em preparação para a execução de um aplicativo de exemplo no Pi.

![O hardware está pronto](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Próximas etapas
[Obter ferramentas Olá](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

