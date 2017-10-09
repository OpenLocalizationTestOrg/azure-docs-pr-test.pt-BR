---
title: "aaaCollect logs usando o diagnóstico do Azure | Microsoft Docs"
description: "Este artigo descreve como tooset o diagnóstico do Azure toocollect logs de um cluster de malha do serviço em execução no Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
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

Quando você estiver executando um cluster do Service Fabric do Azure, é logs de Olá de toocollect uma boa ideia de todos os nós de saudação em um local central. Ter Olá logs em um local central ajuda a analisar e solucionar problemas no seu cluster, ou em aplicativos de saudação e serviços em execução no cluster.

Tooupload uma forma e coletar logs é a extensão de diagnóstico do Azure Olá toouse, quais carregamentos logs tooAzure armazenamento, informações de aplicativo do Azure ou Hubs de eventos do Azure. Olá logs não são úteis diretamente no armazenamento ou em Hubs de eventos. Mas você pode usar um processo externo tooread Olá de eventos do armazenamento e colocá-los em um produto como [análise de Log](../log-analytics/log-analytics-service-fabric.md) ou outra solução de análise de log. O [Application Insights do Azure](https://azure.microsoft.com/services/application-insights/) apresenta um serviço abrangente interno de pesquisa e análise de logs.

## <a name="prerequisites"></a>Pré-requisitos
Use essas ferramentas tooperform algumas das operações de saudação neste documento:

* [Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionado tooAzure serviços de nuvem, mas tem boas informações e exemplos)
* [Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-overview.md)
* [PowerShell do Azure](/powershell/azure/overview)
* [Cliente do Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a>Fontes de log que convém toocollect
* **Logs do Service Fabric**: emitido de canais de rastreamento de eventos para Windows (ETW) e EventSource de toostandard de plataforma do hello. Os logs podem ser de vários tipos:
  * Eventos operacionais: Logs de operações que Olá executa a plataforma do Service Fabric. Os exemplos incluem criação de aplicativos e serviços, alterações de estado do nó e informações de atualização.
  * [Eventos do modelo de programação Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
  * [Eventos do modelo de programação Reliable Services](service-fabric-reliable-services-diagnostics.md)
* **Eventos de aplicativo**: eventos emitidas a partir de código do serviço e gravadas usando Olá EventSource auxiliar classe fornecido em modelos do Visual Studio hello. Para obter mais informações sobre como toowrite logs de seu aplicativo, consulte [monitorar e diagnosticar os serviços em uma instalação de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Implantar a extensão de diagnóstico Olá
Olá primeira etapa na coleta de logs é extensão de diagnóstico Olá toodeploy em cada uma das VMs Olá no cluster do Service Fabric hello. Olá extensão de diagnóstico coleta logs em cada VM e os carrega toohello conta de armazenamento que você especificar. etapas de saudação variam um pouco com base em se você usar Olá portal do Azure ou o Gerenciador de recursos do Azure. etapas de saudação também variam com base na implantação Olá faz parte da criação do cluster ou para um cluster que já existe. Vamos dar uma olhada em etapas Olá para cada cenário.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a>Implantar a extensão de diagnóstico hello como parte da criação de cluster por meio do portal Olá
toodeploy Olá diagnóstico extensão toohello VMs no cluster hello como parte da criação do cluster, você usar o painel de configurações de diagnóstico Olá Olá a imagem a seguir mostrada. tooenable Reliable Actors ou serviços confiáveis coleta de eventos, verifique se o diagnóstico está definido muito**em** (Olá a configuração padrão). Depois de criar o cluster hello, você não pode alterar essas configurações usando o portal de saudação.

![Configurações de diagnóstico do Azure no portal de saudação para criação de cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

Olá a equipe de suporte do Azure *requer* suporte logs toohelp resolver as solicitações de suporte que você criar. Esses logs são coletados em tempo real e são armazenados em uma saudação contas de armazenamento criadas no grupo de recursos de saudação. as configurações de diagnóstico Olá configuram eventos em nível de aplicativo. Esses eventos incluem [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) eventos, [serviços confiáveis](service-fabric-reliable-services-diagnostics.md) eventos e alguns toobe de eventos do nível de sistema do Service Fabric no armazenamento do Azure.

Produtos como [Elasticsearch](https://www.elastic.co/guide/index.html) ou seu próprio processo pode obter eventos Olá Olá da conta de armazenamento. Atualmente, não há nenhuma maneira toofilter ou limpar Olá eventos enviados toohello tabela. Se você não implementa um tooremove de processar eventos de tabela hello, tabela Olá continuará toogrow.

Quando você estiver criando um cluster usando o portal de Olá, é altamente recomendável que você baixe o modelo de saudação **antes de clicar em Okey** toocreate cluster de saudação. Para obter detalhes, consulte muito[configurar um cluster do Service Fabric usando um modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Será necessário toomake alterações do modelo de hello mais tarde, porque você não pode fazer algumas alterações usando o portal de saudação.

Você pode exportar modelos do portal Olá Olá etapas a seguir. No entanto, esses modelos podem ser mais difícil toouse porque eles podem ter valores nulos que estão faltando informações necessárias.

1. Abra seu grupo de recursos.
2. Selecione **configurações** toodisplay painel de configurações de saudação.
3. Selecione **implantações** toodisplay painel de histórico de implantação de saudação.
4. Selecione detalhes implantação toodisplay Olá de implantação de saudação.
5. Selecione **exportar modelo** toodisplay painel de modelo de saudação.
6. Selecione **salvar toofile** tooexport um arquivo. zip que contém o modelo de hello, parâmetro e arquivos do PowerShell.

Depois de exportar arquivos Olá, é necessário toomake uma modificação. Editar o arquivo de parameters.json hello e remover Olá **adminPassword** elemento. Isso fará com que um prompt de senha hello quando Olá script de implantação é executado. Quando você estiver executando o script de implantação hello, você pode ter valores de parâmetro nulo toofix.

Olá toouse baixado modelo tooupdate uma configuração:

1. Extraia a pasta de tooa Olá conteúdo no computador local.
2. Modificar Olá conteúdo tooreflect Olá nova configuração.
3. Inicie o PowerShell e alterar pasta toohello onde você extraiu o conteúdo de saudação.
4. Executar **deploy.ps1** e preencha a ID da assinatura Olá, nome do grupo de recursos de saudação (use Olá mesma configuração do nome tooupdate Olá) e um nome de implantação exclusiva.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Implantar a extensão de diagnóstico hello como parte da criação de cluster usando o Gerenciador de recursos do Azure
toocreate um cluster usando o Gerenciador de recursos, é necessário tooadd Olá diagnóstico JSON toohello completo do cluster Resource Manager modelo de configuração antes de criar o cluster de saudação. Fornecemos um modelo de Gerenciador de recursos de cluster de cinco VM de exemplo com a configuração de diagnóstico adicionada tooit como parte de nossos exemplos de modelo do Gerenciador de recursos. Você pode vê-lo nesse local na Galeria de exemplos do Azure Olá: [cluster de cinco nós com exemplo de modelo do Gerenciador de recursos de diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

configuração de diagnóstico de Olá toosee no modelo do Gerenciador de recursos de saudação, arquivo de azuredeploy.json Olá aberto e procure **IaaSDiagnostics**. toocreate um cluster usando esse modelo, selecione Olá **implantar tooAzure** disponíveis no link anterior de saudação do botão.

Como alternativa, você pode baixar o exemplo do Gerenciador de recursos de hello, fazer alterações tooit e criar um cluster com o modelo modificado hello usando Olá `New-AzureRmResourceGroupDeployment` comando em uma janela do PowerShell do Azure. Consulte Olá código para hello parâmetros que você passa no toohello comando a seguir. Para obter informações detalhadas sobre como toodeploy um recurso de grupo usando o PowerShell, consulte o artigo Olá [implantar um grupo de recursos com o modelo do Azure Resource Manager Olá](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

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

## <a name="update-diagnostics-toocollect-health-and-load-events"></a>Atualizar diagnóstico toocollect eventos de integridade e de carga

A partir da versão de hello 5.4 da malha do serviço, eventos de métrica de integridade e de carga estão disponíveis para coleção. Esses eventos refletir os eventos gerados pelo sistema hello ou seu código usando a integridade de saudação ou carregar relatórios APIs como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Isso permite agregar e exibir a integridade do sistema ao longo do tempo e para alertas com base em eventos de integridade ou de carga. tooview adicionar esses eventos no Visualizador de eventos diagnóstico do Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello lista de provedores do ETW.

eventos de saudação toocollect, modificar Olá tooinclude de modelo de Gerenciador de recursos

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a>Atualizar toocollect de diagnóstico e carregar os logs de novos canais de EventSource
logs de toocollect tooupdate diagnóstico de novos canais de EventSource que representam um novo aplicativo que você está prestes a toodeploy, executar Olá mesmo etapas como Olá [seção anterior](#deploywadarm) para configuração de diagnóstico para um existente cluster.

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

## <a name="next-steps"></a>Próximas etapas
toounderstand mais detalhadamente os eventos que você deve procurar na solução de problemas, consulte os eventos de diagnóstico Olá emitidos para [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) e [serviços confiáveis](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>Artigos relacionados
* [Saiba como os contadores de desempenho de toocollect ou logs usando Olá extensão de diagnóstico](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Solução do Service Fabric no Log Analytics](../log-analytics/log-analytics-service-fabric.md)

