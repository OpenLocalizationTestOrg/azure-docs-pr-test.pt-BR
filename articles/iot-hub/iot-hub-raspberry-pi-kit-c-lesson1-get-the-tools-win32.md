---
title: "Connect Raspberry PI (C) tooAzure IoT - lição 1: obter ferramentas (Windows) | Microsoft Docs"
description: "Baixe e instale as ferramentas necessárias hello e software para o primeiro aplicativo de exemplo hello para Pi no Windows 7 e versões posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: desenvolvimento de iot, software de iot, software de Internet das coisas, instalar o git no windows, instalar node js no windows, installar o npm no windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 70ae6d15f9d6af116ff065a79a30d99afc67bffd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>Obter ferramentas hello (Windows 7 ou posterior)

> [!div class="op_single_selector"]
> * [Windows 7 ou superior](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>O que você fará
Baixe ferramentas de desenvolvimento hello e software Olá Olá primeiro aplicativo de exemplo para framboesa Pi 3. Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Embora Olá linguagem da lógica principal Olá de programação C, Node. js ferramentas são usadas em dispositivos de toodiscover de lições Olá e criar e implantar aplicativos de exemplo.

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:

* Como tooinstall Node. js e Git.
  * [Git](https://git-scm.com) é um software livre de sistema de controle de versão distribuído. aplicativo de exemplo Hello para este artigo é armazenado no Git.
  * O [Node.js](https://nodejs.org/en/) é um tempo de execução de JavaScript com um avançado ecossistema de pacote.
* Como ferramentas de desenvolvimento do toouse NPM tooinstall adicionais Node. js.
  * requisito de versão mínima de saudação do Node. js é 4.5 LTS.
  * [NPM](https://www.npmjs.com) é uma saudação gerenciadores de pacotes para Node. js.

## <a name="what-you-need"></a>O que você precisa

toocomplete essa operação, você precisará de:

* Um toodownload de conexão de Internet Olá ferramentas de desenvolvimento e Olá software.
* Um computador que esteja executando o Windows.

## <a name="install-git-and-nodejs"></a>Instalar o Git e o Node.js

Clicar em links de saudação abaixo toodownload e instale o Git e LTS Node. js para Windows.

* [Obtenha o Git para Windows](https://git-scm.com/download/win/)
* [Obtenha o Node.js LTS para o Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Instalar ferramentas adicionais de desenvolvimento do Node.js

Use [gulp.js](http://gulpjs.com) tooautomate implantação de saudação do tooPi de aplicativo de exemplo hello. Saudação de uso [cli de descoberta do dispositivo](https://github.com/Azure/device-discovery-cli) tooretrieve informações de rede sobre os dispositivos IoT.

Inicie um prompt de comando como administrador. Instalar `gulp` e `device-discovery-cli` executando Olá comando a seguir:

```bash
npm install -g device-discovery-cli gulp
```

Se você tiver problemas ao instalar o Node. js e essas ferramentas de desenvolvimento Node. js adicionais no seu computador, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para problemas de toocommon de soluções.

## <a name="install-visual-studio-code"></a>Instalar o Visual Studio Code

[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code. O Visual Studio Code é um editor de código-fonte leve mas poderoso para Windows, Linux e macOS. Você pode usar este editor posteriormente no código de exemplo hello tooedit tutorial hello.

## <a name="summary"></a>Resumo

Você instalou as ferramentas de desenvolvimento de saudação necessárias e software para o primeiro aplicativo de exemplo hello. Olá próxima tarefa é toocreate, implantar e executar o aplicativo de exemplo hello em Pi.

## <a name="next-steps"></a>Próximas etapas

[Criar e implantar o aplicativo de intermitência hello](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
