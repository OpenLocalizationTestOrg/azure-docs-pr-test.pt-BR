---
title: captura de pacote aaaManage com observador de rede do Azure - 1.0 da CLI do Azure | Microsoft Docs
description: "Esta página explica como toomanage Olá recurso de captura de pacote do observador de rede usando o Azure CLI 1.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a>Gerenciar as capturas de pacote com o Observador de Rede do Azure usando a CLI 1.0 do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API REST do Azure](network-watcher-packet-capture-manage-rest.md)

Captura de pacote do Inspetor de rede permite que você toocreate captura sessões tootrack tráfego tooand de uma máquina virtual. Filtros são fornecidos para Olá tooensure de sessão de captura que somente o tráfego de saudação que você deseja capturar. Captura de pacote ajuda anomalias de rede toodiagnose reativo e proativo. Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais. Sendo tooremotely capaz de captura de pacote de gatilho, esse recurso facilita a carga de saudação da execução de uma captura de pacote e manualmente no computador desejado hello, que economiza tempo.

Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.

Este artigo o orienta por Olá diversas tarefas de gerenciamento que estão atualmente disponíveis para captura de pacote.

- [**Iniciar uma captura de pacote**](#start-a-packet-capture)
- [**Parar uma captura de pacote**](#stop-a-packet-capture)
- [**Excluir uma captura de pacote**](#delete-a-packet-capture)
- [**Baixar uma captura de pacote**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Antes de começar

Este artigo pressupõe que você tenha Olá recursos a seguir:

- Uma instância do observador de rede na região Olá deseja toocreate uma captura de pacote
- Uma máquina virtual com o pacote de saudação capturar extensão habilitada.

> [!IMPORTANT]
> Captura de pacote requer um toobe de agente em execução na máquina virtual de saudação. Olá agente é instalado como uma extensão. Para obter instruções sobre extensões de VM, visite [recursos e extensões de máquina Virtual](../virtual-machines/windows/extensions-features.md).

## <a name="install-vm-extension"></a>Instalar a extensão de VM

### <a name="step-1"></a>Etapa 1

Executar Olá `azure vm extension set` agente de captura de pacote do cmdlet tooinstall Olá na máquina de virtual do convidado hello.

Para máquinas virtuais do Windows:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

Para máquinas virtuais Linux:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a>Etapa 2

tooensure que Olá agente estiver instalado, execute Olá `vm extension get` cmdlet e passá-lo a grupo de recursos de saudação e o nome da máquina virtual. Verifique a saudação resultante lista tooensure Olá agente está instalado.

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

saudação de exemplo a seguir é um exemplo de resposta de saudação em execução`azure vm extension get`

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a>Iniciar uma captura de pacotes

Depois de hello a etapas anteriores forem concluídas, agente de captura de pacote de saudação é instalado na máquina virtual de saudação.

### <a name="step-1"></a>Etapa 1

Olá próxima etapa é a instância do tooretrieve Olá observador de rede. Essa variável é passada toohello `network watcher show` cmdlet na etapa 4.

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a>Etapa 2

Recupere uma conta de armazenamento. Esta conta de armazenamento é um arquivo de captura de pacote usado toostore hello.

```azurecli
azure storage account list
```

### <a name="step-3"></a>Etapa 3

Filtros podem ser dados de saudação toolimit usado armazenado por captura de pacote de saudação. Olá exemplo a seguir configura um pacote de captura com vários filtros.  Olá três primeiros filtros coletam tráfego de TCP de saída somente local IP 10.0.0.3 toodestination portas 20, 80 e 443.  filtro de última Olá coleta somente o tráfego UDP.

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Vários filtros podem ser definidos para uma captura de pacote. Se você estiver usando uma estrutura de filtro complexas, é melhor filtros de toouse como um erro de sintaxe de tooavoid de arquivo json. Por exemplo, use o sinalizador de hello "-r" (em vez de "-f") e passar Olá local de um arquivo json que contém a saudação filtros a seguir:

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


Olá, exemplo a seguir é saída de hello esperada da execução de saudação `network watcher packet-capture create` cmdlet.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a>Obter uma captura de pacote

Executando Olá `network watcher packet-capture show` cmdlet, recupera o status de saudação de uma captura de pacote em execução no momento ou foi concluída.

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

Olá, exemplo a seguir é saída Olá Olá `network watcher packet-capture show` cmdlet. Olá exemplo a seguir é após a conclusão da captura de saudação. Olá valor PacketCaptureStatus for interrompido, com um StopReason de TimeExceeded. Esse valor mostra que a captura de pacote de saudação foi bem-sucedida e executou seu tempo.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a>Parar uma captura de pacotes

Executando Olá `network watcher packet-capture stop` cmdlet, se uma sessão de captura está em andamento ele é interrompido.

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Olá cmdlet não retorna resposta quando executado em uma sessão de captura atualmente em execução ou uma sessão existente que já foi interrompido.

## <a name="delete-a-packet-capture"></a>Excluir uma captura de pacotes

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Excluir uma captura de pacote não exclui o arquivo hello na conta de armazenamento hello.

## <a name="download-a-packet-capture"></a>Baixar um pacote de capturas

Depois de concluído, a sessão de captura de pacote hello captura arquivo pode ser carregado tooblob tooa ou armazenamento local arquivo em Olá VM. local de armazenamento de saudação de captura de pacote de saudação é definido no momento da criação da sessão de saudação. Uma ferramenta conveniente tooaccess esses capturar os arquivos salvos tooa conta de armazenamento é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/

Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Próximas etapas

Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)

Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
