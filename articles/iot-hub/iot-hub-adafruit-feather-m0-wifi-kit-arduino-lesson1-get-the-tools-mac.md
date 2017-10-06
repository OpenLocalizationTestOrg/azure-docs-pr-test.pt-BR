---
title: "Conecte-se Arduino tooAzure IoT - lição 1: obter ferramentas (macOS) | Microsoft Docs"
description: "Baixe e instale as ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Adafruit difusão M0 WiFi em macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: ferramentas de desenvolvimento arduino, desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no mac, instalar node js no mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Obter ferramentas hello (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 ou posterior][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>O que você fará

Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para a sua placa Adafruit difusão M0 WiFi Arduino. 

Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

> [!NOTE]
> Embora Arduino Olá linguagem da lógica principal Olá de programação, ferramentas Node.js são usadas em Olá lições toobuild e implantar aplicativos de exemplo.

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:

* Como tooinstall Node. js e Git.
  * [Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído. aplicativo de exemplo Hello para este artigo é armazenado no Git.
  * O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.
* Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.
  * versão mínima necessária de saudação do Node. js é 4.5 LTS.
  * [NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.

## <a name="what-you-need"></a>O que você precisa
toocomplete essa operação, você precisará de:
* Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.
* Um Mac que esteja executando o macOS Yosemite (10.10) ou posterior.

## <a name="install-git-and-nodejs"></a>Instalar o Git e o Node.js
tooinstall Git e Node. js, use Olá [Homebrew](http://brew.sh) utilitário de gerenciamento de pacote seguindo estas etapas:

1. Instale o Homebrew. Se você já tiver instalado o Homebrew, vá toostep 2.

   1. Pressione `Cmd + Space` e digite `Terminal` tooopen um terminal.
   2. Execute Olá comando a seguir:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Instale o Git e Node. js executando Olá comando a seguir:

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Instalar ferramentas adicionais de desenvolvimento do Node.js
Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação de tooyour de aplicativo de exemplo hello Arduino quadro.

Instalar `gulp`, `device-discovery-cli` executando Olá comando no terminal Olá a seguir:

```bash
sudo npm install -g gulp device-discovery-cli
```

Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento adicional em macOS, consulte Olá [guia de solução de problemas] [ troubleshooting] para problemas de toocommon de soluções.

## <a name="install-visual-studio-code"></a>Instalar o Visual Studio Code
[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code. O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS. Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.

## <a name="summary"></a>Resumo
Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello. Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em seu quadro Arduino.

## <a name="next-steps"></a>Próximas etapas
[Criar e implantar o aplicativo de intermitência hello][create-and-deploy-the-blink-application]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md