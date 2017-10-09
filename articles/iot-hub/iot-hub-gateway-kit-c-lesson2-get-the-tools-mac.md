---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 2: obter ferramentas (macOS) | Microsoft Docs"
description: "Instalar as ferramentas no computador Mac, crie um hub IoT e registrar seu dispositivo no hub IoT de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de IoT, software de IoT, serviço de nuvem de IoT, software de Internet das Coisas, CLI do Azure, instalar o Python no Mac, instalar o git no Ubuntu, execução de Gulp, instalar Node.js em Mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a>Obter ferramentas hello (MacOS)
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

- Como tooinstall [Git](https://git-scm.com/) e [Node.js](https://nodejs.org/en/).
  - O Git é um sistema de controle de versão distribuída de software livre. aplicativo de exemplo Hello desta lição é armazenado no Git.
  - O Node.js é um tempo de execução de JavaScript com um avançado ecossistema de pacote.
- Como toouse [NPM](https://www.npmjs.com/) ferramentas de desenvolvimento tooinstall Node. js.
  - versão mínima necessária de saudação do Node. js é 4.5 LTS.
  - NPM é um dos gerenciadores de pacotes de saudação para Node. js.
- Como tooinstall Visual Studio Code.
  - O Visual Studio Code é um editor de código-fonte de plataforma cruzada leve mas poderoso para Windows, Linux e macOS. Ele tem excelente suporte para depuração, controle Git incorporado, realce de sintaxe, preenchimento de código inteligente, trechos de código e também refatoração de código.
- Como tooinstall Python.
  - Python é uma linguagem de programação para fins gerais amplamente utilizada, de alto nível, interpretada e dinâmica.
- Como tooinstall Olá CLI do Azure.
  - Olá CLI do Azure fornece uma experiência de linha de comando em várias plataformas para o Azure. Trabalhar diretamente de uma linha de comando tooprovision e gerenciar recursos.
- Como toouse Olá toocreate CLI do Azure com um hub IoT.

## <a name="what-you-need"></a>O que você precisa

- Um toodownload de conexão de Internet Olá ferramentas e software.
- Um computador Mac que esteja executando o OS X Yosemite (10.10) ou posterior.

## <a name="install-git-and-nodejs"></a>Instalar o Git e o Node.js

tooinstall Git e Node. js, use o utilitário de gerenciamento de pacotes de Homebrew Olá seguindo estas etapas:

1. [Baixar](http://brew.sh/) e instalar o Homebrew. Se você já tiver instalado o Homebrew, vá toostep 2.
   1. Pressione `Cmd + Space` e digite `Terminal` tooopen um terminal.
   2. Execute Olá comando a seguir:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Instale o Git e Node. js executando Olá comando a seguir:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Instalar ferramentas de desenvolvimento do Node.js

Você usa [gulp.js](http://gulpjs.com/) tooautomate implantação e execução de scripts.

gulp tooinstall, execute Olá comando no terminal Olá a seguir:

```bash
npm install -g gulp
```

Se você tiver problemas com a instalação do hello, consulte Olá [guia de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) para problemas de toocommon de soluções.

> [!Note]
> Nó, NPM e Gulp são scripts de automação toorun necessário desenvolvidos no Node. js.

## <a name="install-python"></a>Instalar o Python

Embora o Mac OS X venha com o Python 2.7, recomendamos que você instale o Python por meio do Homebrew. Veja [Instalando Python no Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).

Instale o Python e pip executando Olá comando a seguir:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Instalar Olá CLI do Azure

Olá tooinstall CLI do Azure, siga estas etapas:

1. Execute Olá terminal Olá comandos a seguir:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   instalação de saudação pode levar 5 minutos.

2. Verificar a instalação de saudação executando Olá comando a seguir:
   ```bash
   az iot -h
   ```
   Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.

   ![Verificar a instalação da CLI do Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Instalar o Visual Studio Code

Usar código do Visual Studio posteriormente em arquivos de configuração do hello tooedit tutorial.

[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code.

## <a name="summary"></a>Resumo

Instalar todas as ferramentas de saudação necessárias e software em seu computador Mac. A próxima tarefa é toouse Olá CLI do Azure toocreate um hub IoT e registrar seu dispositivo em seu hub IoT.

## <a name="next-steps"></a>Próximas etapas
[Criar um Hub IoT e registrar o dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)
