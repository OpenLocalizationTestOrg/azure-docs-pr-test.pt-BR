---
title: "aaaAzure agregação de eventos do serviço de malha com o diagnóstico do Windows Azure | Microsoft Docs"
description: "Saiba mais sobre a agregação e coleta de eventos utilizando o WAD para monitoramento e diagnóstico de clusters do Azure Service Fabric."
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
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Coleta e agregação de eventos utilizando o Diagnóstico do Windows Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Quando você estiver executando um cluster do Service Fabric do Azure, é logs de Olá de toocollect uma boa ideia de todos os nós de saudação em um local central. Ter Olá logs em um local central ajuda a analisar e solucionar problemas no seu cluster, ou em aplicativos de saudação e serviços em execução no cluster.

Tooupload uma forma e coletar logs é extensão de Windows Azure WAD (Diagnóstico) de saudação toouse, que carrega logs tooAzure armazenamento e também tem Olá opção toosend logs tooAzure Application Insights ou Hubs de eventos. Você também pode usar um processo externo tooread Olá de eventos do armazenamento e colocá-los em um produto de plataforma de análise, como [análise de logs do OMS](../log-analytics/log-analytics-service-fabric.md) ou outra solução de análise de log.

## <a name="prerequisites"></a>Pré-requisitos
Essas ferramentas são usada tooperform algumas das operações de saudação neste documento:

* [Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionado tooAzure serviços de nuvem, mas tem boas informações e exemplos)
* [Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-overview.md)
* [PowerShell do Azure](/powershell/azure/overview)
* [Cliente do Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>Origem do evento e log

### <a name="service-fabric-platform-events"></a>Eventos de plataforma do Service Fabric
Conforme discutido em [neste artigo](service-fabric-diagnostics-event-generation-infra.md)Service Fabric configura você com alguns canais de registro de fora da caixa, do qual Olá canais a seguir facilmente configurados com WAD toosend monitoramento e diagnóstico tooa armazenamento tabela de dados ou em outro lugar:
  * Eventos operacionais: operações de nível mais alto que Olá executa a plataforma do Service Fabric. Os exemplos incluem criação de aplicativos e serviços, alterações de estado do nó e informações de atualização. Eles são emitidos como eventos de Rastreamento de Eventos para Windows (ETW)
  * [Eventos do modelo de programação Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
  * [Eventos do modelo de programação Reliable Services](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>Eventos de aplicativo
 Eventos emitidas a partir de seus aplicativos e serviços de código e gravadas usando a classe de auxiliar de EventSource Olá fornecidas Olá modelos do Visual Studio. Para obter mais informações sobre como toowrite EventSource logs de seu aplicativo, consulte [monitorar e diagnosticar os serviços em uma instalação de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Implantar a extensão de diagnóstico Olá
Olá primeira etapa na coleta de logs é extensão de diagnóstico Olá toodeploy em cada uma das VMs Olá no cluster do Service Fabric hello. Olá extensão de diagnóstico coleta logs em cada VM e os carrega toohello conta de armazenamento que você especificar. etapas de saudação variam um pouco com base em se você usar Olá portal do Azure ou o Gerenciador de recursos do Azure. etapas de saudação também variam com base na implantação Olá faz parte da criação do cluster ou para um cluster que já existe. Vamos dar uma olhada em etapas Olá para cada cenário.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Implantar a extensão de diagnóstico hello como parte da criação de cluster por meio do portal do Azure
toodeploy Olá diagnóstico extensão toohello VMs no cluster hello como parte da criação do cluster, que você usar o painel de configurações de diagnóstico Olá mostrado na seguinte Olá imagem - Verifique se o diagnóstico está definido muito**em** (Olá a configuração padrão) . Depois de criar o cluster hello, você não pode alterar essas configurações usando o portal de saudação.

![Configurações de diagnóstico do Azure no portal de saudação para criação de cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

Quando você estiver criando um cluster usando o portal de Olá, é altamente recomendável que você baixe o modelo de saudação **antes de clicar em Okey** toocreate cluster de saudação. Para obter detalhes, consulte muito[configurar um cluster do Service Fabric usando um modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Será necessário toomake alterações do modelo de hello mais tarde, porque você não pode fazer algumas alterações usando o portal de saudação.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Implantar a extensão de diagnóstico hello como parte da criação de cluster usando o Gerenciador de recursos do Azure
toocreate um cluster usando o Gerenciador de recursos, é necessário tooadd Olá diagnóstico JSON toohello completo do cluster Resource Manager modelo de configuração antes de criar o cluster de saudação. Fornecemos um modelo de Gerenciador de recursos de cluster de cinco VM de exemplo com a configuração de diagnóstico adicionada tooit como parte de nossos exemplos de modelo do Gerenciador de recursos. Você pode vê-lo nesse local na Galeria de exemplos do Azure Olá: [cluster de cinco nós com exemplo de modelo do Gerenciador de recursos de diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).

configuração de diagnóstico de Olá toosee no modelo do Gerenciador de recursos de saudação, arquivo de azuredeploy.json Olá aberto e procure **IaaSDiagnostics**. toocreate um cluster usando esse modelo, selecione Olá **implantar tooAzure** disponíveis no link anterior de saudação do botão.

Como alternativa, você pode baixar o exemplo do Gerenciador de recursos de hello, fazer alterações tooit e criar um cluster com o modelo modificado hello usando Olá `New-AzureRmResourceGroupDeployment` comando em uma janela do PowerShell do Azure. Consulte Olá código para hello parâmetros que você passa no toohello comando a seguir. Para obter informações detalhadas sobre como toodeploy um recurso de grupo usando o PowerShell, consulte o artigo Olá [implantar um grupo de recursos com o modelo do Azure Resource Manager Olá](../azure-resource-manager/resource-group-template-deploy.md).

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>Implantar um cluster existente do hello diagnóstico extensão tooan
Se você tiver um cluster existente que não tem o diagnóstico de implantado, ou se você quiser toomodify uma configuração existente, você pode adicionar ou atualizá-lo. Modificar o modelo do Gerenciador de recursos de saudação que é usado toocreate Olá existente cluster ou baixar o modelo de saudação do portal Olá conforme descrito anteriormente. Modificar o arquivo de template.json de saudação executando Olá tarefas a seguir.

Adicione um novo modelo de toohello de recursos de armazenamento adicionando toohello seção de recursos.

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 Em seguida, adicione a seção parâmetros toohello depois de definições de conta de armazenamento hello, entre `supportLogStorageAccountName` e `vmNodeType0Name`. Substitua o texto do espaço reservado Olá *o nome de conta de armazenamento aqui* com nome Olá Olá da conta de armazenamento.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
Em seguida, atualizar Olá `VirtualMachineProfile` seção do arquivo de template.json Olá adicionando Olá código dentro do conjunto de extensões de saudação a seguir. Ser tooadd se uma vírgula no início de saudação ou no final de hello, dependendo de onde será inserido.

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

Depois de modificar o arquivo de template.json Olá conforme descrito, republicar o modelo do Gerenciador de recursos de saudação. Se o modelo de saudação foi exportado, executando o arquivo hello deploy.ps1 republica modelo hello. Após implantar, verifique se o status de **ProvisioningState** é **Com êxito**.

## <a name="collect-health-and-load-events"></a>Coletar eventos de integridade e de carga

A partir da versão de hello 5.4 da malha do serviço, eventos de métrica de integridade e de carga estão disponíveis para coleção. Esses eventos refletir os eventos gerados pelo sistema hello ou seu código usando a integridade de saudação ou carregar relatórios APIs como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Isso permite agregar e exibir a integridade do sistema ao longo do tempo e para alertas com base em eventos de integridade ou de carga. tooview adicionar esses eventos no Visualizador de eventos diagnóstico do Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello lista de provedores do ETW.

eventos de saudação toocollect, modificar tooinclude de modelo do Gerenciador de recursos de saudação

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>Coletar eventos de proxy reverso

Versão de hello 5.7 do Service Fabric [proxy reverso](service-fabric-reverseproxy.md) eventos estão disponíveis para a coleção.
Proxy reverso emite eventos em dois canais, um erro que contém eventos refletindo falhas de processamento de solicitação e Olá outros uma que contém eventos detalhados sobre todas as solicitações de saudação processados no proxy reverso hello. 

1. Coletar eventos de erro: tooview adicionar esses eventos no Visualizador de eventos diagnóstico do Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000010" toohello lista de provedores do ETW.
eventos de saudação toocollect de clusters do Azure, modifique tooinclude de modelo do Gerenciador de recursos de saudação

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. Coletar todos os eventos de processamento de solicitação: visualizador no Visual Studio de eventos diagnóstico, entrada hello ServiceFabric do Microsoft update Olá lista de provedor ETW muito "Microsoft-ServiceFabric:4:0x4000000000000020".
Para clusters de malha do serviço do Azure, modifique Olá tooinclude de modelo de Gerenciador de recursos

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> É recomendável toojudiciously habilitar coleta de eventos deste canal como isso coleta todo o tráfego por meio do proxy reverso hello e pode consumir rapidamente a capacidade de armazenamento.

Para clusters de malha do serviço do Azure, os eventos de saudação de todos os nós de saudação são coletados e agregados em Olá SystemEventTable.
Para obter a solução de problemas de eventos de proxy reverso hello, consulte Olá [guia de diagnóstico de proxy reverso](service-fabric-reverse-proxy-diagnostics.md).

## <a name="collect-from-new-eventsource-channels"></a>Coletar a partir de novos canais EventSource

logs de toocollect tooupdate diagnóstico de novos canais de EventSource que representam um novo aplicativo que você está prestes a toodeploy, executar Olá mesmas etapas conforme descritas anteriormente para a configuração de saudação do diagnóstico para um cluster existente.

Atualizar Olá `EtwEventSourceProviderConfiguration` seção nas entradas de tooadd Olá template.json arquivo hello novos EventSource canais antes de aplicar a configuração de saudação atualizar usando Olá `New-AzureRmResourceGroupDeployment` comando do PowerShell. nome de saudação da origem de eventos de saudação é definido como parte do seu código no arquivo do hello ServiceEventSource.cs gerado pelo Visual Studio.

Por exemplo, se a origem do evento é denominada Meu Eventsource, adicione Olá após eventos de saudação do código tooplace do meu Eventsource em uma tabela nomeada MyDestinationTableName.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

contadores de desempenho de toocollect ou logs de eventos, modificar o modelo de Gerenciador de recursos de saudação usando exemplos Olá fornecidos [criar uma máquina virtual do Windows com o monitoramento e diagnóstico usando um modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Em seguida, republicar o modelo do Gerenciador de recursos de saudação.

## <a name="collect-performance-counters"></a>Coletar contadores de desempenho

toocollect métricas de desempenho do seu cluster, adicione tooyour de contadores de desempenho do hello "WadCfg > DiagnosticMonitorConfiguration" no modelo do Gerenciador de recursos de saudação para seu cluster. Consulte [Contadores de desempenho do Service Fabric](service-fabric-diagnostics-event-generation-perf.md) para contadores de desempenho que recomendamos para coleta.

Por exemplo, aqui vamos definir um contador de desempenho, a cada 15 segundos de amostra (Isso pode ser alterado e segue Olá formato de "PT\<tempo >\<unidade >", por exemplo, PT3M seria amostragem em três minutos) e transferida toohello tabela de armazenamento apropriado cada um minuto.

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
Se você estiver usando um coletor do Application Insights, conforme descrito na seção de saudação abaixo e deseja tooshow essas métricas para cima no Application Insights, faça-se de nome de coletor de saudação tooadd na seção de "coletores" hello como mostrado acima. Além disso, considere a criação de uma tabela separada toosend seus contadores de desempenho, para que eles não prejudique out Olá dados provenientes do hello outros canais de registro que você tiver habilitado.


## <a name="send-logs-tooapplication-insights"></a>Enviar logs tooApplication Insights

Enviar dados de monitoramento e diagnóstico tooApplication Insights (AI) pode ser feito como parte da configuração do WAD hello. Se você decidir toouse AI para visualização e análise de eventos, leia [visualização com o Application Insights e análise de eventos](service-fabric-diagnostics-event-analysis-appinsights.md) tooset a um coletor AI como parte da "WadCfg".

## <a name="next-steps"></a>Próximas etapas

Depois que você configurou corretamente o diagnóstico do Azure, você verá os dados nas tabelas de armazenamento dos logs de EventSource e Olá ETW. Se você escolher toouse OMS, Kibana, ou outros dados análise e visualização de plataforma que não é configurada diretamente no modelo do Gerenciador de recursos de saudação, verifique tooset-se de que a plataforma de saudação do tooread sua escolha nos dados Olá dessas tabelas de armazenamento. Fazer isso para OMS é relativamente simples e é explicado em [Análise de eventos e logs no OMS](service-fabric-diagnostics-event-analysis-oms.md). O Application Insights é um pouco de um caso especial nesse sentido, pois ele pode ser configurado como parte da configuração de extensão de diagnóstico hello, então consulte toohello [apropriado](service-fabric-diagnostics-event-analysis-appinsights.md) se você escolher toouse AI.

>[!NOTE]
>Atualmente, não há nenhuma maneira toofilter ou limpar Olá eventos enviados toohello tabela. Se você não implementa um tooremove de processar eventos de tabela hello, tabela Olá continuará toogrow. Atualmente, há um exemplo de um serviço de manutenção de dados em execução no hello [exemplo Watchdog](https://github.com/Azure-Samples/service-fabric-watchdog-service), e é recomendável que você escreva uma para você mesmo assim, a menos que haja uma boa razão para você toostore logs além de um período de 30 ou 90 dias.

* [Saiba como os contadores de desempenho de toocollect ou logs usando Olá extensão de diagnóstico](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Visualização e Análise de Eventos com o Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Visualização e Análise de Eventos com o OMS](service-fabric-diagnostics-event-analysis-oms.md)