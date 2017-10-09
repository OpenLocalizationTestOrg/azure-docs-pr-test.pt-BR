---
title: "Conecte-se framboesa Pi (nó) tooAzure IoT - lição 2: obter ferramentas (Windows) | Microsoft Docs"
description: "Instale o Python e hello Azure interface de linha de comando (CLI do Azure) no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "serviço de nuvem do iot, cli do azure"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 25b50214322137ea32861fd1131c474e2fc7ebb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Obtenha as ferramentas do Azure (Windows 7 e superior)
> [!div class="op_single_selector"]
> * [Windows 7 e superior](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>O que você fará
Instale o Python e hello Azure interface de linha de comando (CLI do Azure). Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como tooinstall Python.
* Como tooinstall Olá CLI do Azure.

## <a name="what-you-need"></a>O que você precisa
* Um computador Windows com conexão com a Internet.
* Uma assinatura ativa do Azure. Se não tiver uma conta do Azure, crie uma [conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.

## <a name="install-python"></a>Instalar o Python
[Instale o Python](https://www.python.org/downloads/) no seu computador Windows. Você pode instalar o Python 2.7, 3.4 ou 3.5. Esse tutorial se baseia no Python 2.7. Se você já tiver instalado o Python, vá toohello próxima seção e instale Olá CLI do Azure.

Você também precisa de caminho de saudação tooadd pastas Olá onde python.exe e pip.exe estão instalados toohello sistema `PATH` variável de ambiente. Por padrão, python.exe é instalado em `C:\Python27` e pip.exe é instalado em `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Instalar Olá CLI do Azure
Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas para o Azure. Trabalhar diretamente no seu tooprovision de linha de comando e gerenciar recursos.

Olá tooinstall CLI do Azure, siga estas etapas:

1. Abra uma janela de Prompt de comando como administrador.
2. Execute Olá comandos a seguir:

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Verificar a instalação de saudação executando Olá comando a seguir:

   ```bash
   az iot -h
   ```

Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.

![Saída que indica êxito](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Resumo
Você instalou Olá CLI do Azure. A próxima tarefa toocreate sua identidade de dispositivo e o hub IoT do Azure usando Olá CLI do Azure.

## <a name="next-steps"></a>Próximas etapas
[Criar seu Hub IoT e registrar seu Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

