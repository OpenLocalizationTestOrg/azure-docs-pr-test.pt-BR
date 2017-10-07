---
title: captura de pacote aaaManage com observador de rede do Azure - 2.0 do CLI do Azure | Microsoft Docs
description: "Esta página explica como toomanage Olá recurso de captura de pacote do observador de rede usando o Azure CLI 2.0"
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
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a>Gerenciar as capturas de pacote com o Observador de Rede do Azure usando a CLI 2.0 do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API REST do Azure](network-watcher-packet-capture-manage-rest.md)

Captura de pacote do Inspetor de rede permite que você toocreate captura sessões tootrack tráfego tooand de uma máquina virtual. Filtros são fornecidos para Olá tooensure de sessão de captura que somente o tráfego de saudação que você deseja capturar. Captura de pacote ajuda anomalias de rede toodiagnose reativo e proativo. Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais. Sendo tooremotely capaz de captura de pacote de gatilho, esse recurso facilita a carga de saudação da execução de uma captura de pacote e manualmente no computador desejado hello, que economiza tempo.

Este artigo usa nossa próxima geração CLI para o modelo de implantação de gerenciamento de recursos do hello, 2.0 do CLI do Azure, que está disponível para Windows, Mac e Linux.

Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

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

Executar Olá `az vm extension set` agente de captura de pacote do cmdlet tooinstall Olá na máquina de virtual do convidado hello.

Para máquinas virtuais do Windows:

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

Para máquinas virtuais Linux:

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a>Etapa 2

tooensure que Olá agente estiver instalado, execute Olá `vm extension get` cmdlet e passá-lo a grupo de recursos de saudação e o nome da máquina virtual. Verifique a saudação resultante lista tooensure Olá agente está instalado.

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

saudação de exemplo a seguir é um exemplo de resposta de saudação em execução`az vm extension show`

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a>Iniciar uma captura de pacotes

Depois de hello a etapas anteriores forem concluídas, agente de captura de pacote de saudação é instalado na máquina virtual de saudação.

### <a name="step-1"></a>Etapa 1

Olá próxima etapa é a instância do tooretrieve Olá observador de rede. Nome da seção de saudação observador de rede é passado toohello `az network watcher show` cmdlet na etapa 4.

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a>Etapa 2

Recupere uma conta de armazenamento. Esta conta de armazenamento é um arquivo de captura de pacote usado toostore hello.

```azurecli
azure storage account list
```

### <a name="step-3"></a>Etapa 3

Filtros podem ser dados de saudação toolimit usado armazenado por captura de pacote de saudação. Olá exemplo a seguir configura um pacote de captura com vários filtros.  Olá três primeiros filtros coletam tráfego de TCP de saída somente local IP 10.0.0.3 toodestination portas 20, 80 e 443.  filtro de última Olá coleta somente o tráfego UDP.

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Olá, exemplo a seguir é saída de hello esperada da execução de saudação `az network watcher packet-capture create` cmdlet.

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a>Obter uma captura de pacote

Executando Olá `az network watcher packet-capture show` cmdlet, recupera o status de saudação de uma captura de pacote em execução no momento ou foi concluída.

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

Olá, exemplo a seguir é saída Olá Olá `az network watcher packet-capture show` cmdlet. Olá exemplo a seguir é após a conclusão da captura de saudação. Olá valor PacketCaptureStatus for interrompido, com um StopReason de TimeExceeded. Esse valor mostra que a captura de pacote de saudação foi bem-sucedida e executou seu tempo.

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a>Parar uma captura de pacotes

Executando Olá `az network watcher packet-capture stop` cmdlet, se uma sessão de captura está em andamento ele é interrompido.

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> Olá cmdlet não retorna resposta quando executado em uma sessão de captura atualmente em execução ou uma sessão existente que já foi interrompido.

## <a name="delete-a-packet-capture"></a>Excluir uma captura de pacotes

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
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
