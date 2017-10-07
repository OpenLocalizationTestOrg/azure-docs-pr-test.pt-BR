---
title: "aaaCollect logs usando o diagnóstico do Azure Linux | Microsoft Docs"
description: "Este artigo descreve como tooset o diagnóstico do Azure toocollect logs de um cluster do Service Fabric Linux em execução no Azure."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Coletar logs usando o Diagnóstico do Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Quando você estiver executando um cluster do Service Fabric do Azure, é logs de Olá de toocollect uma boa ideia de todos os nós de saudação em um local central. Tendo Olá logs em um local central torna fácil tooanalyze e solucionar problemas, independentemente de estarem em seus serviços, seu aplicativo ou o próprio cluster hello. Tooupload uma forma e coletar logs é a extensão de diagnóstico do Azure Olá toouse, quais carregamentos logs tooAzure armazenamento, informações de aplicativo do Azure ou Hubs de eventos do Azure. Você também pode ler eventos de saudação do armazenamento ou Hubs de eventos e colocá-los em um produto, como [análise de Log](../log-analytics/log-analytics-service-fabric.md) ou outra solução de análise de log. O [Application Insights do Azure](https://azure.microsoft.com/services/application-insights/) apresenta um serviço abrangente interno de pesquisa e análise de logs.

## <a name="log-sources-that-you-might-want-toocollect"></a>Fontes de log que convém toocollect
* **Logs do Service Fabric**: emitido de plataforma Olá via [LTTng](http://lttng.org) e carregados tooyour conta de armazenamento. Logs podem ser eventos operacionais ou eventos de tempo de execução que Olá plataforma emite. Esses logs são armazenados no local de saudação manifesto do cluster que Olá especifica. (detalhes de conta de armazenamento do tooget Olá, procure a marca Olá **AzureTableWinFabETWQueryable** e procure **StoreConnectionString**.)
* **Eventos do aplicativo:** eventos emitidos do seu código de serviço. Você pode usar qualquer solução de log que grave arquivos de log baseados em texto, por exemplo, LTTng. Para obter mais informações, consulte a documentação de LTTng de saudação no rastreamento do aplicativo.  

## <a name="deploy-hello-diagnostics-extension"></a>Implantar a extensão de diagnóstico Olá
Olá primeira etapa na coleta de logs é extensão de diagnóstico Olá toodeploy em cada uma das VMs Olá no cluster do Service Fabric hello. Olá extensão de diagnóstico coleta logs em cada VM e os carrega toohello conta de armazenamento que você especificar. etapas de saudação variam com base em se você usar Olá portal do Azure ou o Gerenciador de recursos do Azure.

Definir toodeploy Olá diagnóstico extensão toohello VMs no cluster hello como parte da criação do cluster, **diagnóstico** muito**em**. Depois de criar o cluster hello, você não pode alterar essa configuração usando o portal de saudação.

Em seguida, configurar arquivos de saudação do Linux Azure Diagnostics (LAD) toocollect e colocá-los em sua conta de armazenamento. Esse processo é explicado como cenário 3 ("carregar seus próprios arquivos de log") no artigo Olá [LAD usando toomonitor e diagnosticar VMs do Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). A seguir obtém esse processo que você acessar toohello rastreamentos. Você pode carregar o Visualizador de tooa Olá rastreamentos de sua escolha.

Você também pode implantar a extensão de diagnóstico hello usando o Gerenciador de recursos do Azure. Olá processo é semelhante para o Windows e Linux e está documentado para clusters do Windows no [como toocollect registra com o Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).

Você também pode usar o Operations Management Suite, conforme descrito em [Análise de Log do Operations Management Suite com o Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Depois de concluir essa configuração, Olá LAD agent monitora Olá arquivos de log especificado. Sempre que uma nova linha é acrescentado toohello arquivo, ele cria uma entrada de syslog que é enviada toohello de armazenamento que você especificou.

## <a name="next-steps"></a>Próximas etapas
toounderstand mais detalhadamente os eventos que você deve examinar durante a solução de problemas, consulte [LTTng documentação](http://lttng.org/docs) e [LAD usando](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

