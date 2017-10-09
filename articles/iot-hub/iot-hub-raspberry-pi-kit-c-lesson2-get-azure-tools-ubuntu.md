---
title: "Connect Raspberry PI (C) tooAzure IoT - lição 2: ferramentas do Azure (Ubuntu) | Microsoft Docs"
description: Instale o Python e a CLI do Azure (Interface de Linha de Comando do Azure) no Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem do iot, cli do azure"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a03512f2-fabe-40c5-8505-b93eef8e5bec
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1af4848f9fe0508e362c15b36eec8a35aea9ac5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Obtenha as ferramentas do Azure (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 e superior](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>O que você fará
Instale hello Azure interface de linha de comando (CLI do Azure). Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

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

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>Resumo
Você instalou Olá CLI do Azure. A próxima tarefa é toocreate Olá seu hub IoT do Azure e a identidade do dispositivo usando a CLI do Azure.

## <a name="next-steps"></a>Próximas etapas
[Criar seu Hub IoT e registrar seu Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

