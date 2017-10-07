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
# <a name="configure-your-device"></a>Configurar seu dispositivo
## <a name="what-you-will-do"></a>O que você fará
Configure seu quadro Adafruit difusão M0 WiFi Arduino para uso pela primeira vez com a montagem de quadro hello, ligar. Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>O que você precisa
toocomplete essa operação, você precisa Olá partes a seguir para o Adafruit difusão M0 WiFi Starter Kit:

* Olá Adafruit difusão M0 WiFi board
* Um tooType Micro B um cabo

![kit][kit]

Você também precisará de:

* Um computador executando o Windows, Mac ou Linux.
* Uma conexão sem fio para seu tooconnect de quadro Arduino para.
* Uma ferramenta de configuração de toodownload de conexão de Internet.

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:

* Como tooassemble sua placa Arduino e power-a para Olá seguintes lições.
* Como as permissões de porta serial tooadd no Ubuntu.

## <a name="connect-your-arduino-board-tooyour-computer"></a>Conectar o computador de tooyour Arduino board

1. Conecte cabo micro Olá Olá superior micro porta.

   ![Porta micro USB superior][top-micro-usb-port]

2. Plug Olá outra extremidade do cabo USB em seu computador.

   ![USB do computador][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Adicionar permissões de porta serial no Ubuntu

Você pode ignorar esta seção se usar Windows ou macOS. Para Ubuntu, você precisa Olá etapas toomake se usuário do linux normal de saudação tem Olá permissões toooperate na porta USB Olá seu quadro Arduino a seguir.

1. Agora, como usuário normal do terminal:

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   Você verá algo semelhante a:

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   Olá "0" pode ser um número diferente ou várias entradas poderá ser retornadas. Dados de caso de saudação primeiro Olá precisamos é `uucp`, Olá segundo é `dialout`, que é o proprietário do grupo de saudação do arquivo hello.

2. Adicione usuário toohello toohello grupo:

   ```bash
   sudo usermod -a -G group-name username
   ```

   Onde `group-name` dados Olá encontrada na primeira etapa de Olá, e `username` é o nome de usuário do linux.

3. Será necessário toolog sair e entrar novamente para essa alteração tootake efeito e instalação Olá concluída.

## <a name="summary"></a>Resumo
Neste artigo, você aprendeu como tooconfigure seu quadro Arduino. Olá próxima tarefa é o software em preparação para a execução de um aplicativo de exemplo em seu quadro Arduino e ferramentas necessárias do tooinstall hello.

![O hardware está pronto][hardware-is-ready]

## <a name="next-steps"></a>Próximas etapas
[Obter ferramentas Olá][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md