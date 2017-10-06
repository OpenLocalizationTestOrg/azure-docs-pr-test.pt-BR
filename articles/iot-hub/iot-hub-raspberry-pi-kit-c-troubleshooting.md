---
title: Connect Raspberry PI (C) tooAzure IoT - solucionar | Microsoft Docs
description: "Página de solução de problemas para experiência Raspberry Pi Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: problemas de iot, problemas internet das coisas
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Solucionar problemas
## <a name="hardware-issues"></a>Problemas de hardware
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>aplicativo Hello também será executado, mas Olá LED estiver piscando não
Esse problema é sempre conectividade de circuito de hardware toohello relacionados. Use Olá etapas tooidentify problemas a seguir.

1. Verifique que você escolheu Olá correto **GPIO** em seu quadro. Olá duas portas devem ser **GPIO GND (Pin 6)** e **GPIO 04 (7 Pin)**.
2. Verifique se polaridade de saudação do seu LED está correta. trecho mais Olá deve indicar Olá **positivo**, pin do nó.
3. Saudação de uso **3.3 v fixar** e **GND Pin** em framboesa Pi 3. Trate Pi como Olá corrente. Verifique que Olá LED funciona bem.

![Especificação do LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Outros problemas de hardware
Para obter informações sobre como resolver problemas comuns de framboesa Pi 3, consulte Olá [página oficial de solução de problemas](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Problemas do pacote de Node.js
### <a name="no-response-during-gulp-tasks"></a>Sem resposta durante as tarefas de gulp
Se você encontrar problemas ao executar tarefas de gulp, você pode adicionar Olá `--verbose` opção de depuração. Tente tooterminate atual gulp tarefas usando `Ctrl + C`, e, em seguida, Olá execução após o comando em suas mensagens de depuração de toosee de janela de console. Você pode ver mensagens de erro detalhadas em sua saída do console. 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemas de descoberta de dispositivo
Para obter ajuda na solução de problemas comuns com hello `devdisco` de comando, verifique Olá [Leiame](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>Problemas de NPM
Tente tooupdate seu pacote NPM com hello comando a seguir:

```bash
npm install -g npm
```

Se o problema de saudação ainda existe, deixar seus comentários no final deste artigo hello ou criar um problema do GitHub em nosso [repositório de exemplo](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)

## <a name="remote-debugging"></a>Depuração remota

O suporte à depuração remota estará disponível em breve na Extensão C/C++ do Visual Studio Code.

Por enquanto, você pode usar GDB por meio do seu terminal SSH favorito:

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a>Problemas da CLI do Azure
Hello Azure interface de linha de comando (CLI do Azure) é uma compilação de visualização. Procure a solução em Olá [guia de instalação de visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluções. Tente tooupgrade cli do Azure toolatest versão quando comandos não funcionam conforme o esperado.

Se você encontrar quaisquer erros com a ferramenta hello, arquivo um [problema](https://github.com/Azure/azure-cli/issues) em Olá **problemas** seção do repositório do GitHub hello.

Para ajudar a solucionar problemas comuns, consulte Olá [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).

Se você atender a "Não foi possível localizar uma versão que satisfaz o requisito de hello", por favor, comando a seguir de execução Olá versão de toolastest pip tooupgrade.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemas de instalação do Python
### <a name="legacy-installation-issues-macos"></a>Problemas de instalação herdada (macOS)
Ao instalar o **pip**, um erro de permissão será lançado quando houver pacotes mais antigos instalados com permissões **su**. Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada. Alguns **pip** pacotes de uma instalação anterior foram criados pela raiz, que faz com que o erro de permissão de saudação. Olá solução é tooremove esses pacotes instalados pela raiz. Use essa tarefa de saudação toocomplete as etapas a seguir:

1. Acesse: /usr/local/lib/python2.7/site-packages
2. Listar pacotes criados por raiz: `ls -l | grep root`
3. Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`
4. Reinstale o Python.

## <a name="azure-iot-hub-issues"></a>Problemas do Hub IoT do Azure
Se você tiver configurado com êxito o hub IoT do Azure com `azure-cli`, e você precisa de uma ferramenta toomanage Olá os dispositivos que estão se conectando tooyour IoT hub, tente Olá ferramentas a seguir:

### <a name="device-explorer"></a>Gerenciador de Dispositivos
[Gerenciador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) é executado em sua máquina local do Windows e se conecta tooyour IoT hub no Azure. Ele se comunica com os seguintes Olá [pontos de extremidade de IoT Hub](iot-hub-devguide.md):

* *Gerenciamento de identidade do dispositivo* tooprovision e gerenciar dispositivos registrados com o hub IoT.
* *Receber o dispositivo para nuvem* para que você pode monitorar as mensagens enviadas do hub IoT de tooyour de dispositivo.
* *Enviar a nuvem para dispositivo* para que você pode enviar mensagens tooyour dispositivos do seu hub IoT.

Configurar seu `IoT hub connection string` em toouse essa ferramenta todos os seus recursos.

### <a name="iot-hub-explorer"></a>Gerenciador do Hub IoT
[Hub IoT Explorer](https://github.com/Azure/iothub-explorer) é uma ferramenta CLI em várias plataformas de exemplo toomanage clientes de dispositivos. Você pode usar dispositivos de Olá Olá ferramenta toomanage no registro de identidade hello, monitorar mensagens de dispositivo para nuvem e enviar comandos de nuvem para dispositivo.

tooinstall Olá versão (pré-lançamento) mais recente da ferramenta de Gerenciador de Hub IOT hello, executar Olá comandos em seu ambiente de linha de comando a seguir:

```
npm install -g iothub-explorer@latest
```

Você pode usar Olá Olá de tooget obter ajuda adicional sobre todos os comandos do Gerenciador de Hub IOT e seus parâmetros de comando a seguir:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Portal do Azure
Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure. Você também poderá Olá toouse [portal do Azure](../azure-portal-overview.md) toohelp provisionar, gerenciar e depurar seus recursos do Azure.

## <a name="azure-storage-issues"></a>Problemas de Armazenamento do Azure
[Gerenciador de armazenamento do Microsoft Azure (visualização)](http://storageexplorer.com) é um aplicativo autônomo da Microsoft que você pode usar toowork com dados de armazenamento do Azure no Linux, Windows e macOS. Usando essa ferramenta, você pode conectar-se a tabela de tooyour e ver dados hello. Você pode usar essa ferramenta tootroubleshoot seus problemas de armazenamento do Azure.
