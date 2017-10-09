---
title: "aaaAzure agregação de eventos do serviço de malha com o diagnóstico do Azure Linux | Microsoft Docs"
description: "Saiba mais sobre a agregação e coleta de eventos utilizando o LAD para monitoramento e diagnóstico de clusters do Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Coleta e agregação de eventos utilizando o Diagnóstico do Linux Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Quando você estiver executando um cluster do Service Fabric do Azure, é logs de Olá de toocollect uma boa ideia de todos os nós de saudação em um local central. Ter Olá logs em um local central ajuda a analisar e solucionar problemas no seu cluster, ou em aplicativos de saudação e serviços em execução no cluster.

Tooupload uma forma e coletar logs é toouse Olá Linux do Azure Diagnostics (LAD) extensão, carrega logs tooAzure armazenamento e também tem Olá opção toosend logs tooAzure Application Insights ou Hubs de eventos. Você também pode usar um processo externo tooread Olá de eventos do armazenamento e colocá-los em um produto de plataforma de análise, como [análise de logs do OMS](../log-analytics/log-analytics-service-fabric.md) ou outra solução de análise de log.

## <a name="log-and-event-sources"></a>Origem do evento e log

### <a name="service-fabric-platform-events"></a>Eventos de plataforma do Service Fabric
O Service Fabric emite alguns logs prontos para uso via [LTTng](http://lttng.org), incluindo eventos operacionais ou eventos de tempo de execução. Esses logs são armazenados no local Olá Olá Gerenciador de recursos de cluster modelo especifica. tooget ou definir detalhes da conta de armazenamento hello, procure a marca Olá **AzureTableWinFabETWQueryable** e procure **StoreConnectionString**.

### <a name="application-events"></a>Eventos de aplicativo
 Eventos emitidos pelo código de seus serviços e aplicativos, conforme especificado por você durante a instrumentação do software. Você pode usar qualquer solução de log que grave arquivos de log baseados em texto, por exemplo, LTTng. Para obter mais informações, consulte a documentação de LTTng de saudação no rastreamento do aplicativo.

[Monitora e diagnostica serviços em uma configuração de desenvolvimento de computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Implantar a extensão de diagnóstico Olá
Olá primeira etapa na coleta de logs é extensão de diagnóstico Olá toodeploy em cada uma das VMs Olá no cluster do Service Fabric hello. Olá extensão de diagnóstico coleta logs em cada VM e os carrega toohello conta de armazenamento que você especificar. etapas de saudação variam com base em se você usar Olá portal do Azure ou o Gerenciador de recursos do Azure.

Definir toodeploy Olá diagnóstico extensão toohello VMs no cluster hello como parte da criação do cluster, **diagnóstico** muito**em**. Depois de criar o cluster hello, você não pode alterar essa configuração usando o portal de saudação.

Em seguida, configurar arquivos de saudação do Linux Azure Diagnostics (LAD) toocollect e colocá-los em sua conta de armazenamento. Esse processo é explicado como cenário 3 ("carregar seus próprios arquivos de log") no artigo Olá [LAD usando toomonitor e diagnosticar VMs do Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). A seguir obtém esse processo que você acessar toohello rastreamentos. Você pode carregar o Visualizador de tooa Olá rastreamentos de sua escolha.

Você também pode implantar a extensão de diagnóstico hello usando o Gerenciador de recursos do Azure. Olá processo é semelhante para o Windows e Linux e está documentado para clusters do Windows no [como toocollect registra com o Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).

Você também pode usar o Operations Management Suite, conforme descrito em [Análise de Log do Operations Management Suite com o Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Depois de concluir essa configuração, Olá LAD agent monitora Olá arquivos de log especificado. Sempre que uma nova linha é acrescentado toohello arquivo, ele cria uma entrada de syslog que é enviada toohello de armazenamento que você especificou.

## <a name="next-steps"></a>Próximas etapas

toounderstand mais detalhadamente os eventos que você deve examinar durante a solução de problemas, consulte [LTTng documentação](http://lttng.org/docs) e [LAD usando](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
