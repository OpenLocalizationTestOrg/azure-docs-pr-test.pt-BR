---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 2: obter ferramentas (Ubuntu) | Microsoft Docs"
description: "Instalar as ferramentas de saudação e software Olá no computador host executando o Ubuntu, crie um hub IoT e registrar seu dispositivo no hub IoT de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de iot, software de iot, serviço de nuvem de IoT, software de Internet das coisas, CLI do Azure, instalar o git no ubuntu, execução de gulp, instalar node js no ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Obter ferramentas hello (16.04 Ubuntu)
> [!div class="op_single_selector"]
> * [Windows 7 ou superior](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>O que você fará

- Instalar o Git, Node.js, o Gulp e o Python.
- Instale hello Azure interface de linha de comando (CLI do Azure). 

Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).
## <a name="what-you-will-learn"></a>O que você aprenderá

Nesta lição, você aprenderá:

- Como tooinstall Node. js e Git.
  - O Git é um sistema de controle de versão distribuída de software livre. aplicativo de exemplo Hello desta lição é armazenado no Git.
  - O Node.js é um tempo de execução de JavaScript com um avançado ecossistema de pacote.
- Como ferramentas de desenvolvimento toouse NPM tooinstall Node. js.
  - versão mínima necessária de saudação do Node. js é 4.5 LTS.
  - NPM é um dos gerenciadores de pacotes de saudação para Node. js.
- Como tooinstall Visual Studio Code.
  - O Visual Studio Code é um editor de código-fonte de plataforma cruzada leve mas poderoso para Windows, Linux e macOS. Ele tem excelente suporte para depuração, controle Git incorporado, realce de sintaxe, preenchimento de código inteligente, trechos de código e também refatoração de código.
- Como tooinstall Olá CLI do Azure
  - Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas para o Azure. Trabalhar diretamente de uma linha de comando tooprovision e gerenciar recursos.
- Como toouse Olá toocreate CLI do Azure com um hub IoT.

## <a name="what-you-need"></a>O que você precisa

- Um toodownload de conexão de Internet Olá ferramentas e software.
- Um computador que esteja executando o Ubuntu 16.04 ou posterior.

## <a name="install-git-and-nodejs"></a>Instalar o Git e o Node.js

tooinstall Git e Node. js, siga estas etapas:

1. Pressione `Ctrl + Alt + T` tooopen um terminal.
2. Execute Olá comandos a seguir:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Instalar ferramentas de desenvolvimento do Node.js

Você usa [gulp.js](http://gulpjs.com/) tooautomate implantação e execução de scripts.

gulp tooinstall, execute Olá comando no terminal Olá a seguir:

```bash
sudo npm install -g gulp
```

Se você tiver problemas com a instalação do hello, consulte Olá [guia de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) para problemas de toocommon de soluções.

> [!Note]
> Nó, NPM e Gulp são scripts de automação toorun necessário desenvolvidos no Node. js.

## <a name="install-hello-azure-cli"></a>Instalar Olá CLI do Azure

Olá tooinstall CLI do Azure, siga estas etapas:

1. Execute Olá terminal Olá comandos a seguir:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   instalação de saudação pode levar 5 minutos.

2. Verificar a instalação de saudação executando Olá comando a seguir:

   ```bash
   az iot -h
   ```
Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.
![Verificar a instalação da CLI do Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Instalar o Visual Studio Code

Usar código do Visual Studio posteriormente em arquivos de configuração do hello tooedit tutorial.

[Baixe](https://code.visualstudio.com/docs/setup/linux) e instale o Visual Studio Code.

## <a name="summary"></a>Resumo

Instalar todas as ferramentas de saudação necessárias e software no computador host. A próxima tarefa é toouse Olá CLI do Azure toocreate um hub IoT e registrar seu dispositivo em seu hub IoT.

## <a name="next-steps"></a>Próximas etapas
[Criar um Hub IoT e registrar seu dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)
