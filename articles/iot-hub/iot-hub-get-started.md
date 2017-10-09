---
title: "IoT Hub do Azure - começar a conectar-se a nuvem do IoT dispositivos toohello | Microsoft Docs"
description: Saiba como tooconnect seus quadros IoT e starter kits tooAzure IoT Hub. Seus dispositivos podem enviar telemetria tooIoT Hub e IoT Hub podem monitorar e gerenciar seus dispositivos.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: tutorial do hub iot do azure
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a>Tutoriais de introdução ao Hub IoT do Azure

Você pode usar o Azure IoT Hub hello Azure IoT soluções de dispositivos e SDKs toobuild Internet das coisas (IoT):

* IoT Hub do Azure é um serviço totalmente gerenciado na nuvem de saudação que se conecta com segurança, monitora e gerencia os dispositivos IoT. Use Olá SDKs do Azure IoT dispositivo tooimplement seus dispositivos IoT.
* Use um gateway IoT em cenários de IoT mais complexos. Por exemplo, em que você precisa tooconsider fatores como dispositivos herdados, os custos de largura de banda, as políticas de segurança e privacidade ou processamento de dados de borda. Nesses cenários, você deve usar Azure IoT borda tooimplement um gateway que se conecta o hub de IoT tooyour dispositivos.

## <a name="what-hello-tutorials-cover"></a>O que abordam os tutoriais de saudação

Estes tutoriais apresentam tooAzure IoT Hub e o dispositivo Olá SDKs. tutoriais de saudação abordam recursos comuns de IoT cenários toodemonstrate saudação do IoT Hub. Olá tutoriais também ilustram como toocombine IoT Hub com outros Azure serviços e as ferramentas toobuild mais poderosas soluções de IoT. Tutoriais de saudação, você pode escolher toouse os dispositivos IoT reais ou simulados. Além disso, você pode aprender como toouse um hub IoT gateway tooenable dispositivos tooconnect tooyour.

## <a name="set-up-your-device"></a>Configurar seu dispositivo

Conecte-se uma IoT dispositivo ou gateway tooAzure IoT Hub. Você pode escolher um tooget do dispositivo físico ou simulada iniciado:

| Dispositivo IoT                       | Linguagem de programação |
|----------------------------------|----------------------|
| Raspberry Pi                     | [Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]  |
| Kit de Desenvolvimento da IoT                       | [Arduino no VSCode][DevKit]     |
| Intel Edison                     | [Node.js][Ed_Nd], [C][Ed_C]    |
| Adafruit Feather HUZZAH ESP8266  | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 Thing Dev       | [Arduino][Th_Ard]              |
| Adafruit Feather M0              | [Arduino][M0_Ard]              |
| Dispositivo simulado no computador           | [.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth] |
| Simulador de dispositivo online         | [Raspberry Pi (Node.js)][Ol_Sim] |

Além disso, você pode usar um hub IoT borda gateway tooenable dispositivos tooconnect tooyour IoT:

| Dispositivos de gateway               | Linguagem de programação | Plataforma         |
|------------------------------|----------------------|------------------|
| Intel NUC (modelo DE3815TYKE) | C                    | [Wind River Linux][NUC_Lnx] |
| Gateway simulado            | C                    | [Linux][Sim_Lnx], [Windows][Sim_Win] |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
