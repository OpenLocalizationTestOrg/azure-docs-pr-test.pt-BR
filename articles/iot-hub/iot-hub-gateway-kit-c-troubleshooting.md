---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Solução de problemas | Microsoft Docs"
description: "Página de solução de problemas de gateway NUC Intel"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: problemas de iot, problemas internet das coisas
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed6812c60412afb615012e3d694051d009b149a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Solucionar problemas

## <a name="hardware-issues"></a>Problemas de hardware

### <a name="ti-sensortag-cannot-be-connected"></a>SensorTag de TI não pode ser conectado

problemas de conectividade de SensorTag tootroubleshoot, use Olá [SensorTag aplicativo](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).

### <a name="have-an-issue-with-intel-nuc"></a>Problemas com o NUC da Intel

tootroubleshoot problemas de inicialização, consulte muito[solução de problemas de inicialização não Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).

tootroubleshoot problemas do sistema operacional, consulte muito[solução de problemas de sistema operacional Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).

tootroubleshoot outros problemas, consulte muito[códigos de piscar e avisar para Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).

## <a name="nodejs-package-issues"></a>Problemas do pacote de Node.js

### <a name="no-response-during-gulp-tasks"></a>Sem resposta durante as tarefas de gulp

Se você encontrar problemas em vez de tarefas em execução, você pode adicionar Olá `--verbose` opção de depuração. Tente tooterminate atual gulp tarefas usando `Ctrl + C`, e, em seguida, Olá execução após o comando em suas mensagens de depuração de toosee de janela de console. Você pode ver mensagens de erro detalhadas em sua saída do console.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemas de descoberta de dispositivo

Para obter ajuda na solução de problemas comuns com hello `discover-sensortag` de comando, verifique Olá [página wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).

### <a name="npm-issues"></a>problemas de npm

Tente tooupdate seu pacote npm executando Olá comando a seguir:

```bash
npm install -g npm
```

Se o problema de saudação ainda existe, deixar seus comentários no final deste artigo hello ou criar um problema do GitHub em nosso [repositório de exemplo](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).

## <a name="remote-debugging"></a>Depuração Remota
> As instruções abaixo se destinam à depuração dos scripts node.js usados neste tutorial.
### <a name="run-hello-sample-application-in-debug-mode"></a>Execute o aplicativo de exemplo hello no modo de depuração

Execute o aplicativo de exemplo hello no modo de depuração por meio de saudação comando a seguir:

```bash
gulp run --debug
```

Quando o mecanismo de depuração Olá estiver pronto, você deverá ver `Debugger listening on port 5858` na saída do console hello.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Configure o dispositivo remoto do Visual Studio Code tooconnect toohello

1. Olá abrir **depurar** painel no lado esquerdo de saudação.
2. Clique em Olá verde **iniciar depuração** botão (F5). O Visual Studio Code abre um arquivo `launch.json`.
3. Saudação de atualização `launch.json` arquivo com hello conteúdo a seguir. Substituir `[device hostname or IP address]` com o nome de host ou endereço IP de dispositivo real do hello.

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Configuração de Depuração Remota](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Anexar o aplicativo remoto toohello

Clique em Olá verde **iniciar depuração** (F5) botão toostart depuração.

Leitura [JavaScript no código VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn mais sobre o depurador de saudação.

![Depurar o Exemplo de BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Problemas da CLI do Azure

Hello Azure interface de linha de comando (CLI do Azure) é uma compilação de visualização. soluções de tooseek, você pode usar o hello [guia de instalação de visualização](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Se você encontrar quaisquer erros com a ferramenta hello, arquivo um [problema](https://github.com/Azure/azure-cli/issues) em Olá **problemas** seção do repositório do GitHub hello.

Para obter ajuda na solução de problemas comuns, consulte Olá [Leiame](https://github.com/Azure/azure-cli/blob/master/README.rst).

Se você atender a "Não foi possível localizar uma versão que satisfaz o requisito de hello", por favor, comando a seguir de execução Olá versão de toolastest pip tooupgrade.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemas de instalação do Python

### <a name="legacy-installation-issues-macos"></a>Problemas de instalação herdada (macOS)

Ao instalar o pip, um erro de permissão será lançado quando houver pacotes herdados instalados com permissões **su**. Essa situação ocorre porque a instalação anterior do Python usando brew (macOS) não está completamente desinstalada. Alguns pacotes de pip de uma instalação anterior foram criados pela raiz, que faz com que o erro de permissão de saudação. Olá solução é tooremove esses pacotes instalados pela raiz. Use essa tarefa de saudação toocomplete as etapas a seguir:

1. Vá muito`/usr/local/lib/python2.7/site-packages`
2. Listar pacotes criados por raiz: `ls -l | grep root`
3. Desinstalar pacotes da etapa 2: `sudo rm -rf {package name}`
4. Reinstale o Python.

## <a name="azure-iot-hub-issues"></a>Problemas do Hub IoT do Azure

Se você tiver configurado com êxito o hub IoT do Azure com hello CLI do Azure, e você precisa de uma ferramenta toomanage Olá os dispositivos que estão se conectando tooyour IoT hub, tente Olá ferramentas a seguir.

### <a name="device-explorer"></a>Gerenciador de Dispositivos

[Gerenciador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) é executado em sua máquina local do Windows e se conecta tooyour IoT hub no Azure. Ele se comunica com os seguintes Olá [pontos de extremidade de IoT Hub](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- Tooprovision de gerenciamento de identidade do dispositivo e gerenciar dispositivos registrados com o hub IoT.
- Receba o dispositivo na nuvem para que você pode monitorar as mensagens enviadas do hub IoT de tooyour de dispositivo.
- Envie nuvem para dispositivo para que você pode enviar mensagens tooyour dispositivos do seu hub IoT.

Configure todos os seus recursos de sua cadeia de conexão de hub IoT dentro toouse essa ferramenta.

### <a name="iothub-explorer"></a>iothub-explorer

[Gerenciador de Hub IOT](https://github.com/Azure/iothub-explorer) é uma ferramenta CLI em várias plataformas de exemplo toomanage clientes de dispositivos. Você pode usar dispositivos de Olá Olá ferramenta toomanage no registro de identidade hello, monitorar mensagens de dispositivo para nuvem e enviar comandos de nuvem para dispositivo.

tooinstall Olá versão mais recente (pré-lançamento) da ferramenta de Gerenciador de Hub IOT hello, executar Olá comando a seguir:

```bash
npm install -g iothub-explorer@latest
```

tooget obter ajuda adicional sobre todos os Olá comandos do Gerenciador de Hub IOT e seus parâmetros, execute Olá comando a seguir:

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>Olá portal do Azure

Uma experiência completa de CLI ajuda você a criar e gerenciar todos os recursos do Azure. Você também poderá Olá toouse [portal do Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provisionar, gerenciar e depurar seus recursos do Azure.

## <a name="azure-storage-issues"></a>Problemas de Armazenamento do Azure

[Gerenciador de armazenamento do Microsoft Azure (visualização)](http://storageexplorer.com/) é um aplicativo autônomo da Microsoft que você pode usar toowork com dados de armazenamento do Azure no Linux, Windows e macOS. Usando essa ferramenta, você pode conectar-se a tabela de tooyour e ver dados hello. Você pode usar essa ferramenta tootroubleshoot seus problemas de armazenamento do Azure.
