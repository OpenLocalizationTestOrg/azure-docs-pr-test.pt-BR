---
title: "Conecte-se Arduino tooAzure IoT - lição 2: ferramentas do Azure (Ubuntu) | Microsoft Docs"
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
ms.openlocfilehash: 7eb9c891a6340fee018894883583022d740ecb6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Obtenha as ferramentas do Azure (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 ou posterior][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>O que você fará

Instale hello Azure interface de linha de comando (CLI do Azure). Se você tiver problemas, procure por soluções em Olá [página de solução](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) para seu quadro Adafruit difusão M0 WiFi Arduino.

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como tooinstall Olá CLI do Azure.
* Como tooadd um subgrupo de IoT de saudação CLI do Azure.

## <a name="what-you-need"></a>O que você precisa
* Um computador Ubuntu com conexão com a Internet.
* Uma assinatura ativa do Azure. Se você não tiver uma conta, poderá criar uma [conta de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.

## <a name="install-hello-azure-cli"></a>Instalar Olá CLI do Azure
Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas do Azure, permitindo que você toowork diretamente do seu tooprovision de linha de comando e gerenciar recursos.

tooinstall hello mais recente CLI do Azure, siga estas etapas:

1. Olá executar comandos em uma janela de terminal a seguir. Pode levar cinco minutos tooinstall Olá CLI do Azure.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Verificar a instalação de saudação executando Olá comando a seguir:

   ```bash
   az iot -h
   ```

Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.

![Saída que indica êxito][output]

## <a name="summary"></a>Resumo
Você instalou Olá CLI do Azure. A próxima tarefa é toocreate Olá seu hub IoT do Azure e a identidade do dispositivo usando a CLI do Azure.

## <a name="next-steps"></a>Próximas etapas
[Criar seu Hub IoT e registrar sua placa Arduino][create-your-iot-hub-and-register-your-arduino-board]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md