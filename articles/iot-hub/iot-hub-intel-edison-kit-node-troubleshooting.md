---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 4: solução de problemas | Microsoft Docs"
description: "Página de solução de problemas da experiência Node.js do Intel Edison"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "solução de problemas do arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Solucionar problemas
## <a name="hardware-issues"></a>Problemas de hardware
Para obter informações sobre como resolver problemas comuns no Intel Edison, consulte Olá [página oficial de solução de problemas](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Problemas do pacote de Node.js
### <a name="no-response-during-gulp-tasks"></a>Sem resposta durante as tarefas de gulp
Se você encontrar problemas ao executar tarefas de gulp, você pode adicionar Olá `--verbose` opção de depuração. Tente tooterminate atual gulp tarefas usando `Ctrl + C`, e, em seguida, Olá execução após o comando em suas mensagens de depuração de toosee de janela de console. Você pode ver mensagens de erro detalhadas em sua saída do console. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>Problemas de NPM
Tente tooupdate seu pacote NPM com hello comando a seguir:

```bash
npm install -g npm
```

Se o problema de saudação ainda existe, deixar seus comentários no final deste artigo hello ou criar um problema do GitHub em nosso [repositório de exemplo][sample-repository].

## <a name="remote-debugging"></a>Depuração remota

### <a name="run-hello-sample-application-in-debug-mode"></a>Execute o aplicativo de exemplo hello no modo de depuração

```bash
gulp run --debug
```

Quando o mecanismo de depuração Olá estiver pronto, você deve ser capaz de toosee ```Debugger listening on port 5858``` da saída do console hello.

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a>Configure o dispositivo remoto do código VS tooconnect toohello

Olá abrir **depurar** painel do lado esquerdo de saudação.

Clique em Olá verde **iniciar depuração** botão (F5). Código VS abriria um **Launch** arquivo, que é necessário tooupdate.

Saudação de atualização **Launch** com hello seguindo o conteúdo do arquivo, substitua `[device hostname or IP address]` com o endereço IP do dispositivo real hello ou nome de host.  

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Configuração de depuração remota](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Anexar o aplicativo remoto toohello

Clique em Olá verde **iniciar depuração** (F5) botão e aproveitar a depuração.

Você pode ler [JavaScript no código VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn mais sobre o depurador de saudação.

![Depuração remota interativa](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

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
[Gerenciador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) é executado em sua máquina local do Windows e se conecta tooyour IoT hub no Azure. Ele se comunica com os seguintes Olá [pontos de extremidade de IoT Hub](iot-hub-devguide.md):

- _Gerenciamento de identidade do dispositivo_ tooprovision e gerenciar dispositivos registrados com o hub IoT.
- _Receber o dispositivo para nuvem_ para que você pode monitorar as mensagens enviadas do hub IoT de tooyour de dispositivo.
- _Enviar a nuvem para dispositivo_ para que você pode enviar mensagens tooyour dispositivos do seu hub IoT.

Configurar seu `IoT hub connection string` em toouse essa ferramenta todos os seus recursos.

### <a name="iot-hub-explorer"></a>Gerenciador do Hub IoT
[Hub IoT Explorer](https://github.com/Azure/iothub-explorer) é uma ferramenta CLI em várias plataformas de exemplo toomanage clientes de dispositivos. Você pode usar dispositivos de Olá Olá ferramenta toomanage no registro de identidade hello, monitorar mensagens de dispositivo para nuvem e enviar comandos de nuvem para dispositivo.

tooinstall Olá versão (pré-lançamento) mais recente da ferramenta de Gerenciador de Hub IOT hello, executar Olá comandos em seu ambiente de linha de comando a seguir:

```bash
npm install -g iothub-explorer@latest
```

Você pode usar Olá Olá de tooget obter ajuda adicional sobre todos os comandos do Gerenciador de Hub IOT e seus parâmetros de comando a seguir:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Portal do Azure
Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure. Você também poderá Olá toouse [portal do Azure](../azure-portal-overview.md) toohelp provisionar, gerenciar e depurar seus recursos do Azure.

## <a name="azure-storage-issues"></a>Problemas de Armazenamento do Azure
[Gerenciador de armazenamento do Microsoft Azure (visualização)](http://storageexplorer.com) é um aplicativo autônomo da Microsoft que você pode usar toowork com [armazenamento do Azure](https://azure.microsoft.com/en-us/services/storage/) dados no Linux, Windows e macOS. Usando essa ferramenta, você pode conectar-se a tabela de tooyour e ver dados hello. Você pode usar essa ferramenta tootroubleshoot seus problemas de armazenamento do Azure.

## <a name="next-steps"></a>Próximas etapas
Esta página inclui apenas os problemas mais comuns de saudação do kit de Edison Intel. Você também pode deixar comentários inferior tooreport problemas para solução de problemas.

Voltar muito[começar com Intel Edison (Node. js)](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started