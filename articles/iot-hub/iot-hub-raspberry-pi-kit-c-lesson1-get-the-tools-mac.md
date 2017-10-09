---
title: "Connect Raspberry PI (C) tooAzure IoT - lição 1: obter ferramentas (macOS) | Microsoft Docs"
description: "Baixar e instalar ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Pi macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no mac, execução de gulp, instalar node js no mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Obter ferramentas hello (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 ou superior](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>O que você fará
Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para seu framboesa Pi 3. Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Embora Olá linguagem da lógica principal Olá de programação C, Node. js ferramentas são usadas em dispositivos de toodiscover de lições Olá e criar e implantar aplicativos de exemplo.

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
Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooyour de aplicativo de exemplo hello Pi. Saudação de uso [cli de descoberta do dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve informações de rede sobre os dispositivos IoT.

Instalar `gulp` e `device-discovery-cli` executando Olá comando no terminal Olá a seguir:

```bash
sudo npm install -g device-discovery-cli gulp
```

Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento adicional em macOS, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para problemas de toocommon de soluções.

## <a name="install-visual-studio-code"></a>Instalar o Visual Studio Code
[Baixe](https://code.visualstudio.com/docs/setup/osx) e instale o Visual Studio Code. O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS. Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.

## <a name="summary"></a>Resumo
Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello. Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Pi.

## <a name="next-steps"></a>Próximas etapas
[Criar e implantar o aplicativo de intermitência hello](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

