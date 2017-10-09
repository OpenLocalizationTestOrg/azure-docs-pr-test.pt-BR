---
title: "Conecte-se framboesa Pi (nó) tooAzure IoT - lição 1: obter ferramentas (Ubuntu) | Microsoft Docs"
description: "Baixe e instale as ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Pi no Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "desenvolvimento de iot, software de iot, software de internet das coisas, instalar o git no ubuntu, execução de gulp, instalar node js no ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Obter ferramentas hello (16.04 Ubuntu)

> [!div class="op_single_selector"]
> * [Windows 7 ou superior](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a>O que você fará
Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para framboesa Pi 3. Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:

* Como tooinstall Node. js e Git.
  * [Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído. aplicativo de exemplo Hello para este artigo é armazenado no Git.
  * O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.
* Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.
  * versão mínima necessária de saudação do Node. js é 4.5 LTS.
  * [NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.

## <a name="what-do-you-need"></a>Do que você precisa
toocomplete essa operação, você precisará de:

* Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.
* Um computador que esteja executando o Ubuntu 16.04 ou posterior.

## <a name="install-git-nodejs-and-npm"></a>Instale o Git, Node.js e o NPM
Atalho de teclado do uso Olá `Ctrl + Alt + T` tooopen comandos de uma saudação de terminal e execute a seguir:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Instalar ferramentas adicionais de desenvolvimento do Node.js
Você usa [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooPi de aplicativo de exemplo hello. Você também usar Olá [cli de descoberta do dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve informações de rede sobre os dispositivos IoT.

Instalar `gulp` e `device-discovery-cli` executando Olá comando no terminal Olá a seguir:

```bash
sudo npm install -g device-discovery-cli gulp
```

Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento adicional no Ubuntu, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para problemas de toocommon de soluções.

## <a name="install-visual-studio-code"></a>Instalar o Visual Studio Code
[Baixe](https://code.visualstudio.com/docs/setup/linux) e instale o Visual Studio Code. O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS. Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.

## <a name="summary"></a>Resumo
Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello. Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Pi.

## <a name="next-steps"></a>Próximas etapas
[Criar e implantar o aplicativo de exemplo hello blink](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

