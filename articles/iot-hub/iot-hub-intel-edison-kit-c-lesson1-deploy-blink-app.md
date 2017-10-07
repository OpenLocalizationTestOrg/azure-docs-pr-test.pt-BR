---
title: "Connect Intel Edison (C) tooAzure IoT - lição 1: implantar o aplicativo | Microsoft Docs"
description: "Clonar um aplicativo de exemplo C de saudação do GitHub e execute gulp toodeploy tooyour esse aplicativo placa Edison Intel. Este aplicativo de exemplo pisca Olá LED conectado toohello placa a cada dois segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projetos led arduino, piscar led arduino, código piscar led arduino, programa de piscar arduino, exemplo de piscar arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Criar e implantar o aplicativo de intermitência hello
## <a name="what-you-will-do"></a>O que você fará
Clonar o aplicativo de exemplo C de saudação do GitHub e usar Olá gulp ferramenta toodeploy Olá exemplo aplicativo tooIntel Edison. aplicativo de exemplo Hello pisca Olá LED conectado toohello placa a cada dois segundos. Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

## <a name="what-you-will-learn"></a>O que você aprenderá
* Como toodeploy e execução Olá aplicativo de exemplo no Edison.

## <a name="what-you-need"></a>O que você precisa
Você deve ter concluído Olá seguintes operações com êxito:

* [Configurar seu dispositivo][configure-your-device]
* [Obter ferramentas Olá][get-the-tools]

## <a name="open-hello-sample-application"></a>Aplicativo de exemplo hello aberto
Olá tooopen aplicativo de exemplo, siga estas etapas:

1. Clone o repositório de exemplo de saudação do GitHub executando Olá comando a seguir:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

arquivo Olá Olá `app` subpasta é o arquivo de origem da chave de saudação que contém Olá código toocontrol Olá LED.

### <a name="install-application-dependencies"></a>Instalar dependências de aplicativos
Instale bibliotecas de saudação e outros módulos, que é necessário para o aplicativo de exemplo hello executando Olá comando a seguir:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurar conexão do dispositivo Olá
tooconfigure Olá conexão do dispositivo, siga estas etapas:

1. Gere arquivo de configuração de dispositivo de saudação executando Olá comando a seguir:

   ```bash
   gulp init
   ```

   arquivo de configuração de saudação `config-edison.json` contém credenciais do usuário Olá use toolog em tooEdison. vazamento de saudação tooavoid de credenciais de usuário, o arquivo de configuração Olá é gerado na subpasta Olá `.iot-hub-getting-started` da pasta base do hello em seu computador.

2. Abra o arquivo de configuração de dispositivo de saudação no código do Visual Studio executando Olá comando a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Substitua o espaço reservado de saudação `[device hostname or IP address]` e `[device password]` com endereço IP de saudação e senha marcados para baixo na lição anterior.

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Parabéns! Você criou com êxito o primeiro aplicativo de exemplo hello para Edison.

## <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a>Instalar o hello Azure IoT Hub SDK Edison
Instale hello Azure IoT Hub SDK em Edison executando Olá comando a seguir:

```bash
gulp install-tools
```

Essa tarefa pode levar um longo tempo toocomplete, dependendo de sua conexão de rede. Ela precisa toobe executada apenas uma vez para um Edison.

### <a name="deploy-and-run-hello-sample-app"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello executando Olá comando a seguir:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Verifique se Olá aplicativo funciona
aplicativo de exemplo Hello encerra automaticamente após Olá LED pisca para 20 vezes. Se você não vir Olá LED piscando, consulte Olá [guia de solução de problemas] [ troubleshooting] para problemas de toocommon de soluções.

![LED piscando][led-blinking]

## <a name="summary"></a>Resumo
Instalar Olá necessárias ferramentas toowork com Edison e implantado uma saudação do exemplo aplicativo tooEdison tooblink LED. Você pode criar, implantar e executar outro aplicativo de exemplo que se conecta Edison tooAzure toosend de IoT Hub e receber mensagens.

## <a name="next-steps"></a>Próximas etapas
[Obter Olá ferramentas do Azure][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
