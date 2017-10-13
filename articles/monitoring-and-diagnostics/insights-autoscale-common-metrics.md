---
title: "Métricas comuns de dimensionamento automático do Azure Monitor | Microsoft Docs"
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
ms.openlocfilehash: 240a230d09680672ccd5316470a87d047fab9fd1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a>Métricas comuns de dimensionamento automático do Azure Monitor
O dimensionamento automático do Azure Monitor permite que você aumente ou reduza número de instâncias em execução com base nos dados de telemetria (métricas). Este documento descreve as métricas mais comuns que você pode querer usar. No Portal do Azure para Serviços de Nuvem e Farms de Servidores, você pode escolher a métrica do recurso segundo a qual o dimensionamento será feito. No entanto, também é possível escolher qualquer métrica de um recurso diferente e fazer o dimensionamento com base nela.

O dimensionamento automático do Azure Monitor aplica-se somente aos [Conjuntos de Dimensionamento da Máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Serviços de Nuvem](https://azure.microsoft.com/services/cloud-services/) e [Serviço de Aplicativo - Aplicativos Web](https://azure.microsoft.com/services/app-service/web/). Outros serviços do Azure usam métodos de dimensionamento diferentes.

## <a name="compute-metrics-for-resource-manager-based-vms"></a>Computar métricas para VMs com base no Resource Manager
Por padrão, Máquinas Virtuais e Conjuntos de Dimensionamento de Máquinas Virtuais com base no Resource Manager emitem métricas básicas (nível do host). Além disso, ao configurar a coleta de dados de diagnóstico para uma VM do Azure e VMSS, a extensão de diagnóstico do Azure também emite contadores de desempenho do SO convidado (conhecidos geralmente como “Métricas do SO convidado”).  Você pode usar todas essas métricas em regras de dimensionamento automático.

Você pode usar o PoSH/API/CLI `Get MetricDefinitions` para exibir as métricas disponíveis para o recurso de VMSS.

Se você estiver usando conjuntos de dimensionamento de VM e não vir uma métrica específica listada, provavelmente ela estará *desabilitada* em sua extensão de diagnóstico.

Se uma determinada métrica não estiver sendo amostrada ou transferida com a frequência que você deseja, você poderá atualizar a configuração de diagnóstico.

Se qualquer um dos casos acima for verdadeiro, consulte [Usar o PowerShell para habilitar o Diagnóstico do Azure em uma máquina virtual que executa o Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) sobre o PowerShell para configurar e atualizar sua extensão de diagnóstico de VM do Azure para habilitar a métrica. Esse artigo também inclui um arquivo de configuração de diagnóstico de exemplo.

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a>Métricas de host para VMs Windows e Linux baseadas no Resource Manager
As seguintes métricas de nível de host são emitidas por padrão para a VM do Azure e VMSS em instâncias do Windows e Linux. Essas métricas descrevem sua VM do Azure, mas são coletadas do host de VM do Azure em vez de por meio do agente instalado na VM convidada. Você pode usar essas métricas em regras de dimensionamento automático.

- [Métricas de host para VMs Windows e Linux baseadas no Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [Métricas de host para Conjuntos de Dimensionamento de VMs Windows e Linux baseadas no Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a>Métricas de SO convidado de VMs Windows baseadas no Resource Manager
Quando você cria uma VM no Azure, o diagnóstico é habilitado usando a extensão de Diagnóstico. A extensão de diagnóstico emite um conjunto de métricas extraído de dentro da VM. Isso significa que você pode desativar o dimensionamento automático de métricas que não são emitidas por padrão.

Você pode gerar uma lista das métricas usando o seguinte comando do PowerShell.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Você pode criar um alerta para as métricas a seguir:

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

Você pode gerar uma lista das métricas usando o seguinte comando do PowerShell.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 Você pode criar um alerta para as métricas a seguir:

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
Você também pode realizar a autoescala com base em métricas comuns do servidor Web, como o comprimento da fila Http. O nome da métrica é **HttpQueueLength**.  A seção a seguir lista as métricas de farm de servidores (aplicativos Web) disponíveis.

### <a name="web-apps-metrics"></a>Métricas de aplicativos Web
Você pode gerar uma lista das métricas de aplicativos Web usando o seguinte comando do PowerShell.

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
Você pode dimensionar segundo o comprimento da fila de armazenamento, que é o número de mensagens na fila de armazenamento. O comprimento da fila de armazenamento é uma métrica especial e o limite aplicado será o número de mensagens por instância. Por exemplo se houver duas instâncias e o limite for definido como 100, ocorrerá um dimensionado quando o número total de mensagens na fila for 200. Podendo ser 100 mensagens por instância, 120, 80 ou qualquer outra combinação totalizando até 200 ou mais.

Defina essas configurações na folha **Configurações** do Portal do Azure. Para Conjuntos de Dimensionamento de VMs, você pode atualizar a configuração de Dimensionamento Automático no modelo do Resource Manager para utilizar *metricName* como *ApproximateMessageCount* e passar a ID da fila de armazenamento como *metricResourceUri*.

Por exemplo, com uma Conta de Armazenamento Clássico, a configuração de dimensionamento automático metricTrigger incluiria:

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

Para uma conta de armazenamento (não clássica), o metricTrigger incluiria:

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a>Métricas do Barramento de Serviço usadas frequentemente
Você pode dimensionar segundo o comprimento da fila do Barramento de Serviço, que é o número de mensagens na fila do Barramento de Serviço. O comprimento da fila de Barramento de Serviço é uma métrica especial e o limite aplicado será o número de mensagens por instância. Por exemplo se houver duas instâncias e o limite for definido como 100, ocorrerá um dimensionado quando o número total de mensagens na fila for 200. Podendo ser 100 mensagens por instância, 120, 80 ou qualquer outra combinação totalizando até 200 ou mais.

Para Conjuntos de Dimensionamento de VMs, você pode atualizar a configuração de Dimensionamento Automático no modelo do Resource Manager para utilizar *metricName* como *ApproximateMessageCount* e passar a ID da fila de armazenamento como *metricResourceUri*.

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> Para o Barramento de Serviço, o conceito de grupo de recursos não existe, mas o Azure Resource Manager cria um grupo de recursos padrão por região. O grupo de recursos geralmente está no formato 'Default - ServiceBus-[região]'. Por exemplo, 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast' etc.
>
>
