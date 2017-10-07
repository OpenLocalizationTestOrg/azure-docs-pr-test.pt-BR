---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 2: obter ferramentas (Windows) | Microsoft Docs"
description: "Instalar as ferramentas de saudação e software Olá no computador host executando o Windows, crie um hub IoT e registrar seu dispositivo no hub IoT de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desenvolvimento de IoT, software de IoT, serviço de nuvem de IoT, software de Internet das Coisas, CLI do Azure, instalar o git no windows, executar gulp, instalar node js no windows, instalar npm no windows, instalar Python no windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3b30b60a0115413394992061a88dde4cd442ac19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a>Obter ferramentas hello (Windows 7 e posterior)
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
- Um computador com Windows.

## <a name="install-git-and-nodejs"></a>Instalar o Git e o Node.js

Clique Olá toodownload links a seguir e instale o Git e LTS Node. js para Windows.

- [Obtenha o Git para Windows](https://git-scm.com/download/win/)
- [Obtenha o Node.js LTS para o Windows](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Instalar ferramentas de desenvolvimento do Node.js

Você usa [gulp.js](http://gulpjs.com/) tooautomate implantação e execução de scripts.

Pressione `Windows + R`, tipo `cmd` e pressione `Enter` tooopen uma janela de Prompt de comando, e, em seguida, Olá executar comando a seguir:

```cmd
npm install -g gulp
```

Se você tiver problemas com a instalação do hello, consulte Olá [guia de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) para problemas de toocommon de soluções.

> [!Note]
> Nó, NPM e Gulp são scripts de automação toorun necessário desenvolvidos no Node. js.

## <a name="install-python"></a>Instalar o Python

Você pode escolher entre Python 2.7, 3.4 ou 3.5. Neste tutorial, usamos o Python 2.7. Se você já tiver instalado o python, vá toohello próxima seção.

[Obter o Python para Windows](https://www.python.org/downloads/)

Você também precisa de caminho de saudação tooadd pastas Olá onde Python.exe e pip.exe estão instalados toohello sistema `PATH` variável de ambiente. Por padrão, python.exe é instalado em `C:\Python27` e pip.exe é instalado em `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Instalar Olá CLI do Azure

Olá tooinstall CLI do Azure, siga estas etapas:

1. Abra uma janela de Prompt de comando como administrador.

2. Instale Olá CLI do Azure executando Olá comandos a seguir:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   instalação de saudação pode levar 5 minutos.

3. Verificar a instalação de saudação executando Olá comando a seguir:

   ```cmd
   az iot -h
   ```

   Você verá a seguinte Olá saída se a instalação de saudação foi bem-sucedida.

   ![Verificar a instalação da CLI do Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Instalar o Visual Studio Code

Usar código do Visual Studio posteriormente em arquivos de configuração do hello tooedit tutorial.

[Baixe](https://code.visualstudio.com/docs/setup/windows) e instale o Visual Studio Code.

## <a name="summary"></a>Resumo

Instalar todas as ferramentas de saudação necessárias e software no computador host. A próxima tarefa é toouse Olá CLI do Azure toocreate um hub IoT e registrar seu dispositivo em seu hub IoT.

## <a name="next-steps"></a>Próximas etapas
[Criar um Hub IoT e registrar seu dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)
