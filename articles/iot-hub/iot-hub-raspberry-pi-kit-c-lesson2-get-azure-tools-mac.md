---
title: "Connect Raspberry PI (C) tooAzure IoT - lição 2: ferramentas do Azure (macOS) | Microsoft Docs"
description: Instale o Python e a CLI do Azure (Interface de Linha de Comando do Azure) no macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem do iot, cli do azure"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Obtenha as ferramentas do Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 e superior](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>O que você fará
Instale hello Azure interface de linha de comando (CLI do Azure). Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como tooinstall CLI do Azure.
* Como tooadd um subgrupo de IoT de saudação CLI do Azure.

## <a name="what-you-need"></a>O que você precisa
* Um Mac com conexão com a Internet.
* Uma assinatura ativa do Azure. Se não tiver uma conta do Azure, você pode [criar uma conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.

## <a name="install-python"></a>Instalar o Python
Embora macOS vem com Python 2.7 imediato saudação, recomendamos que você instale Python por meio de Homebrew. Consulte [Instalando Python no macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).

Instale o Python e pip executando Olá comando a seguir:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Instalar Olá CLI do Azure
Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas para o Azure. Trabalhar diretamente no seu tooprovision de linha de comando e gerenciar recursos. 

tooinstall hello mais recente CLI do Azure, siga estas etapas:

1. Olá executar comandos em uma janela de terminal a seguir. Pode levar cinco minutos tooinstall Olá CLI do Azure.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Verificar a instalação de saudação executando Olá comando a seguir:

   ```bash
   az iot -h
   ```

Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Resumo
Você instalou Olá CLI do Azure. A próxima tarefa é toocreate sua identidade de dispositivo e o hub IoT do Azure usando Olá CLI do Azure.

## <a name="next-steps"></a>Próximas etapas
[Criar seu Hub IoT e registrar seu Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

