---
title: "aaaAzure métricas comuns de dimensionamento automático do Monitor | Microsoft Docs"
description: "Saiba quais métricas são usadas comumente para fazer o dimensionamento automático dos Serviços de Nuvem, Máquinas Virtuais e Aplicativos Web."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a>Métricas comuns de dimensionamento automático do Azure Monitor
Dimensionamento automático de Monitor do Azure permite que você tooscale Olá número de instâncias em execução para cima ou para baixo, com base nos dados de telemetria (métricas). Este documento descreve as métricas mais comuns que talvez seja preferível toouse. Olá portal do Azure para serviços de nuvem e Farms de servidores, é possível métrica Olá Olá recursos tooscale por. No entanto, também é possível nenhuma métrica de tooscale um recurso diferente por.

Dimensionamento automático de Monitor do Azure se aplica apenas muito[conjuntos de escala de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [serviços de nuvem](https://azure.microsoft.com/services/cloud-services/), e [do serviço de aplicativo - aplicativos Web](https://azure.microsoft.com/services/app-service/web/). Outros serviços do Azure usam métodos de dimensionamento diferentes.

## <a name="compute-metrics-for-resource-manager-based-vms"></a>Computar métricas para VMs com base no Resource Manager
Por padrão, Máquinas Virtuais e Conjuntos de Dimensionamento de Máquinas Virtuais com base no Resource Manager emitem métricas básicas (nível do host). Além disso, quando você configurar a coleta de dados de diagnóstico para uma VM do Azure e VMSS, Olá extensão de diagnóstico do Azure também emite contadores de desempenho do SO convidado (conhecidos como "Métricas do SO convidado").  Você pode usar todas essas métricas em regras de dimensionamento automático.

Você pode usar o hello `Get MetricDefinitions` disponível para o recurso VMSS para métricas de saudação do tooview do PoSH/API/CLI.

Se você estiver usando conjuntos de dimensionamento de VM e não vir uma métrica específica listada, provavelmente ela estará *desabilitada* em sua extensão de diagnóstico.

Se uma determinada métrica não está sendo frequência Olá amostra ou transferidos em que você deseja, é possível atualizar a configuração de diagnóstico de saudação.

Se ambos os casos anteriores for true, examine [tooenable de usar o PowerShell diagnóstico do Azure em uma máquina virtual que executa o Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) sobre tooconfigure PowerShell e atualizar seu tooenable de extensão de diagnóstico de VM do Azure Olá métrica. Esse artigo também inclui um arquivo de configuração de diagnóstico de exemplo.

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a>Métricas de host para VMs Windows e Linux baseadas no Resource Manager
Olá métricas de nível de host a seguir é emitido por padrão para a máquina virtual do Azure e VMSS em instâncias do Windows e Linux. Essas métricas descrevem sua VM do Azure, mas são coletadas do host de VM do Azure hello, em vez de por meio do agente instalado na VM convidada de saudação. Você pode usar essas métricas em regras de dimensionamento automático.

- [Métricas de host para VMs Windows e Linux baseadas no Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [Métricas de host para Conjuntos de Dimensionamento de VMs Windows e Linux baseadas no Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a>Métricas de SO convidado de VMs Windows baseadas no Resource Manager
Quando você cria uma máquina virtual no Azure, diagnóstico está habilitado por meio da extensão de diagnóstico de saudação. extensão de diagnóstico Olá emite um conjunto de métricas obtidas dentro Olá VM. Isso significa que você pode desativar o dimensionamento automático de métricas que não são emitidas por padrão.

Você pode gerar uma lista de métricas de saudação usando Olá comando do PowerShell a seguir.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Você pode criar um alerta para Olá métricas a seguir:

| Nome da métrica | Unidade |
| --- | --- |
| \Processador(_Total)\% Tempo do processador |Porcentagem |
| \Processador(_Total)\% Tempo Privilegiado |Porcentagem |
| \Processador(_Total)\% Tempo de Usuário |Porcentagem |
| \Informações do Processador (_Total)\Frequência do Processador |Contagem |
| \Sistema\Processos |Contagem |
| \Processo(_Total)\Contagem de Thread |Contagem |
| \Processo(_Total)\Contagem de Manipulador |Contagem |
| \Memória\% Bytes Confirmados em Uso |Porcentagem |
| \Memória\Bytes Disponíveis |Bytes |
| \Memória\Bytes Confirmados |Bytes |
| \Memória\Limite de Confirmação |Bytes |
| \Memória\Bytes de Pool Pagináveis |Bytes |
| \Memória\Bytes de Pool Não Pagináveis |Bytes |
| \PhysicalDisk(_Total)\% Tempo de Disco |Porcentagem |
| \PhysicalDisk(_Total)\% Tempo de Leitura de Disco |Porcentagem |
| \PhysicalDisk(_Total)\% Tempo de Gravação de Disco |Porcentagem |
| \Disco físico(_Total)\Transferências do disco/seg |CountPerSecond |
| \PhysicalDisk(_Total)\Leituras de Disco/s |CountPerSecond |
| \PhysicalDisk(_Total)\Gravações de Disco/s |CountPerSecond |
| \PhysicalDisk(_Total)\Bytes de Disco/s |BytesPerSecond |
| \PhysicalDisk(_Total)\Bytes de Leitura de Disco/s |BytesPerSecond |
| \PhysicalDisk(_Total)\Bytes de Gravação de Disco/s |BytesPerSecond |
| \PhysicalDisk(_Total)\Média Tamanho da fila do disco |Contagem |
| \PhysicalDisk(_Total)\Média Tamanho de Fila de Leitura de Disco |Contagem |
| \PhysicalDisk(_Total)\Média Tamanho de Fila de Gravação de Disco |Contagem |
| \LogicalDisk(_Total)\% Espaço Livre |Porcentagem |
| \LogicalDisk(_Total)\Megabytes Livres |Contagem |

### <a name="guest-os-metrics-linux-vms"></a>Métricas de SO convidado de VMs Linux
Quando você cria uma VM no Azure, o diagnóstico é habilitado por padrão usando a extensão de Diagnóstico.

Você pode gerar uma lista de métricas de saudação usando Olá comando do PowerShell a seguir.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 Você pode criar um alerta para Olá métricas a seguir:

| Nome da métrica | Unidade |
| --- | --- |
| \Memory\AvailableMemory |Bytes |
| \Memory\PercentAvailableMemory |Porcentagem |
| \Memory\UsedMemory |Bytes |
| \Memory\PercentUsedMemory |Porcentagem |
| \Memory\PercentUsedByCache |Porcentagem |
| \Memory\PagesPerSec |CountPerSecond |
| \Memory\PagesReadPerSec |CountPerSecond |
| \Memory\PagesWrittenPerSec |CountPerSecond |
| \Memory\AvailableSwap |Bytes |
| \Memory\PercentAvailableSwap |Porcentagem |
| \Memory\UsedSwap |Bytes |
| \Memory\PercentUsedSwap |Porcentagem |
| \Processor\PercentIdleTime |Porcentagem |
| \Processor\PercentUserTime |Porcentagem |
| \Processor\PercentNiceTime |Porcentagem |
| \Processor\PercentPrivilegedTime |Porcentagem |
| \Processor\PercentInterruptTime |Porcentagem |
| \Processor\PercentDPCTime |Porcentagem |
| \Processor\PercentProcessorTime |Porcentagem |
| \Processor\PercentIOWaitTime |Porcentagem |
| \PhysicalDisk\BytesPerSecond |BytesPerSecond |
| \PhysicalDisk\ReadBytesPerSecond |BytesPerSecond |
| \PhysicalDisk\WriteBytesPerSecond |BytesPerSecond |
| \PhysicalDisk\TransfersPerSecond |CountPerSecond |
| \PhysicalDisk\ReadsPerSecond |CountPerSecond |
| \PhysicalDisk\WritesPerSecond |CountPerSecond |
| \PhysicalDisk\AverageReadTime |Segundos |
| \PhysicalDisk\AverageWriteTime |Segundos |
| \PhysicalDisk\AverageTransferTime |Segundos |
| \PhysicalDisk\AverageDiskQueueLength |Contagem |
| \NetworkInterface\BytesTransmitted |Bytes |
| \NetworkInterface\BytesReceived |Bytes |
| \NetworkInterface\PacketsTransmitted |Contagem |
| \NetworkInterface\PacketsReceived |Contagem |
| \NetworkInterface\BytesTotal |Bytes |
| \NetworkInterface\TotalRxErrors |Contagem |
| \NetworkInterface\TotalTxErrors |Contagem |
| \NetworkInterface\TotalCollisions |Contagem |

## <a name="commonly-used-web-server-farm-metrics"></a>Métricas da Web (Farm de servidores) usadas normalmente
Você também pode executar o dimensionamento automático com base nas métricas de servidor da web comuns como Olá comprimento da fila de Http. O nome da métrica é **HttpQueueLength**.  Olá seção listas disponíveis server farm (aplicativos da Web) métricas a seguir.

### <a name="web-apps-metrics"></a>Métricas de aplicativos Web
Você pode gerar uma lista de métricas de aplicativos Web hello usando Olá comando do PowerShell a seguir.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Você pode alertar ou dimensionar com base nessas métricas.

| Nome da métrica | Unidade |
| --- | --- |
| CpuPercentage |Porcentagem |
| MemoryPercentage |Porcentagem |
| DiskQueueLength |Contagem |
| HttpQueueLength |Contagem |
| BytesReceived |Bytes |
| BytesSent |Bytes |

## <a name="commonly-used-storage-metrics"></a>Métricas de armazenamento usadas normalmente
Você pode dimensionar por comprimento de fila de armazenamento, que é o número de saudação de mensagens na fila de armazenamento de saudação. Comprimento da fila de armazenamento é uma métrica especial e limite de saudação é o número de saudação de mensagens por instância. Por exemplo, se houver duas instâncias e limite de saudação é definido too100, dimensionamento ocorre quando a saudação o número total de mensagens na fila de saudação é 200. Que pode ser 100 mensagens por instância, 120 e 80 ou qualquer outra combinação que adiciona too200 ou mais.

Definir essa configuração no hello portal do Azure no hello **configurações** folha. Para conjuntos de escala de VM, você pode atualizar a configuração de dimensionamento automático de saudação toouse de modelo do Gerenciador de recursos de saudação *metricName* como *ApproximateMessageCount* e passar Olá ID da fila de armazenamento hello como  *metricResourceUri*.

Por exemplo, com uma saudação de conta de armazenamento clássico metricTrigger de configuração de AutoEscala inclui:

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

Para uma conta de armazenamento (não-clássico), Olá metricTrigger inclui:

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a>Métricas do Barramento de Serviço usadas frequentemente
Você pode dimensionar por comprimento da fila de barramento de serviço, que é o número de saudação de mensagens na fila do barramento de serviço hello. Comprimento da fila de barramento de serviço é uma métrica especial e limite de saudação é o número de saudação de mensagens por instância. Por exemplo, se houver duas instâncias e limite de saudação é definido too100, dimensionamento ocorre quando a saudação o número total de mensagens na fila de saudação é 200. Que pode ser 100 mensagens por instância, 120 e 80 ou qualquer outra combinação que adiciona too200 ou mais.

Para conjuntos de escala de VM, você pode atualizar a configuração de dimensionamento automático de saudação toouse de modelo do Gerenciador de recursos de saudação *metricName* como *ApproximateMessageCount* e passar Olá ID da fila de armazenamento hello como  *metricResourceUri*.

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> Barramento de serviço, conceito de grupo de recursos de saudação não existe, mas Azure Resource Manager cria um grupo de recursos padrão por região. grupo de recursos de Olá geralmente está no formato de 'Default - ServiceBus-[Região]' hello. Por exemplo, 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast' etc.
>
>
