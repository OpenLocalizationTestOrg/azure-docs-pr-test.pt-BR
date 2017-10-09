---
title: "monitoramento e diagnóstico de aaaAdd tooan máquina virtual do Azure | Microsoft Docs"
description: "Use um toocreate de modelo do Gerenciador de recursos do Azure nova máquina virtual do Windows com a extensão de diagnóstico do Azure."
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Usar monitoramento e diagnóstico com uma VM Windows e modelos do Azure Resource Manager
Olá extensão de diagnóstico do Azure fornece monitoramento de saudação e recursos de diagnóstico em um Windows com base em máquina virtual do Azure. Você pode habilitar esses recursos na máquina virtual de hello, incluindo a extensão de saudação como parte do modelo do Gerenciador de recursos do azure hello. Para saber mais sobre como incluir extensões como parte de um modelo de máquina virtual, confira [Criando modelos do Gerenciador de Recursos do Azure com extensões de VM](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) . Este artigo descreve como você pode adicionar um modelo de máquina virtual do windows hello diagnóstico do Azure extensão tooa.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Adicionar definição de recurso VM Olá diagnóstico do Azure extensão toohello
extensão de diagnóstico Olá tooenable em uma máquina Virtual do Windows precisa de extensão de saudação tooadd como um recurso VM no hello modelo do Gerenciador de recursos.

Para um Gerenciador de recursos simples baseado em máquina de Virtual adicionar Olá extensão configuração toohello *recursos* matriz para Olá Máquina Virtual: 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


Outra convenção comum é adicionar configuração da extensão Olá no nó de recursos Olá raiz do modelo de saudação em vez de defini-lo no nó de recursos da máquina virtual hello. Com essa abordagem, você tem tooexplicitly especificar uma relação hierárquica entre extensão hello e máquina virtual de saudação com hello *nome* e *tipo* valores. Por exemplo: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

extensão Olá é sempre associada a máquina virtual de saudação, você poderá diretamente defini-lo diretamente no nó de recurso da máquina de virtual Olá ou defini-lo no nível de base de saudação e usar Olá tooassociate de convenção de nomenclatura hierárquica com hello virtual máquina.

Para extensões de saudação de conjuntos de escala de máquina Virtual configuração é especificada em Olá *extensionProfile* propriedade Olá *VirtualMachineProfile*.

Olá *publicador* propriedade com valor de saudação do **Microsoft.Azure.Diagnostics** e hello *tipo* propriedade com valor de saudação do **IaaSDiagnostics** identificar exclusivamente Olá extensão de diagnóstico do Azure.

Olá valor Olá *nome* propriedade pode ser usado toorefer toohello extensão no grupo de recursos de saudação. Configurá-lo especificamente muito**Microsoft.Insights.VMDiagnosticsSettings** habilitará toobe facilmente identificado por hello garantindo portal do Azure, Olá monitoramento gráficos aparecem corretamente Olá portal do Azure.

Olá *typeHandlerVersion* Especifica Olá versão da extensão Olá você gostaria que toouse. Configuração *autoUpgradeMinorVersion* muito a versão secundária**true** garante que você obterá a versão secundária mais recente de saudação de extensão de saudação que está disponível. É altamente recomendável que você sempre defina *autoUpgradeMinorVersion* tooalways ser **true** para que você obtenha sempre toouse hello mais recente disponível extensão de diagnóstico com todos os novos recursos do hello e bug correções. 

Olá *configurações* elemento contém propriedades de configurações de extensão de saudação que podem ser definidas e ler da extensão de saudação (às vezes chamado de tooas configuração pública). Olá *xmlcfg* propriedade contém a configuração baseada em xml para logs de diagnóstico hello, contadores de desempenho que serão coletadas pelo agente de diagnóstico Olá etc. Consulte [esquema de configuração de diagnóstico](https://msdn.microsoft.com/library/azure/dn782207.aspx) para obter mais informações sobre o próprio esquema de xml hello. Uma prática comum é a configuração de xml real de saudação toostore como uma variável no modelo do Azure Resource Manager hello e, em seguida, concatenar e base64 codificação-los o valor Olá tooset *xmlcfg*. Consulte a seção de saudação em [variáveis de configuração de diagnóstico](#diagnostics-configuration-variables) toounderstand mais informações sobre como toostore Olá xml em variáveis. Olá *storageAccount* propriedade especifica o nome de Olá Olá armazenamento conta toowhich de dados de diagnóstico será transferido. 

Olá propriedades em *protectedSettings* (às vezes chamado de tooas configuração privada) podem ser definida, mas não podem ser lidos após sendo definido. Olá natureza somente gravação do *protectedSettings* é útil para armazenar segredos como chave de conta de armazenamento Olá onde os dados de diagnóstico hello serão gravados.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Especificando uma conta de armazenamento de diagnóstico como parâmetro
Olá diagnóstico extensão trecho json a acima assume dois parâmetros *existingdiagnosticsStorageAccountName* e *existingdiagnosticsStorageResourceGroup* toospecify diagnóstico de saudação conta de armazenamento onde serão armazenados os dados de diagnóstico. Especificar a conta de armazenamento de diagnóstico de saudação como um parâmetro torna fácil toochange conta de armazenamento de diagnóstico de saudação entre ambientes diferentes, por exemplo, talvez queira toouse uma conta de armazenamento de diagnóstico diferentes para teste e outro para o implantação de produção.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

É uma conta de armazenamento de diagnóstico em um grupo de recursos diferente de grupo de recursos de saudação para a máquina virtual de saudação toospecify de melhor prática. Um grupo de recursos pode ser considerado toobe com seu próprio tempo de vida de uma unidade de implantação, uma máquina virtual pode ser implantada e reimplantada conforme novas atualizações de configurações ficam tooit, mas você pode querer toocontinue armazenar dados de diagnóstico de saudação em Olá mesma conta de armazenamento entre essas implantações de máquina virtual. Com a conta de armazenamento Olá em um recurso diferente habilita Olá armazenamento conta tooaccept de dados de várias implantações de máquina virtual, tornando fácil tootroubleshoot problemas em Olá várias versões.

> [!NOTE]
> Se você criar um modelo de máquina virtual do windows do Visual Studio pode ser definida a conta de armazenamento padrão de saudação toouse Olá a mesma conta de armazenamento onde o VHD da máquina virtual Olá é carregado. Isso é a configuração inicial de saudação VM toosimplify. Novamente, você deverá considerar Olá modelo toouse outra conta de armazenamento que pode ser passada como um parâmetro. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>Variáveis de configuração de diagnóstico
Olá diagnóstico extensão trecho json a acima define uma *accountid* toosimplify variável obtendo chave de conta de armazenamento Olá para o armazenamento de diagnóstico hello:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Olá *xmlcfg* propriedade de extensão de diagnóstico de saudação é definida usando diversas variáveis que são concatenados. os valores dessas variáveis Olá estão em xml necessidade toobe escape corretamente ao definir variáveis de json hello.

Olá informações a seguir descrevem Olá xml de configuração de diagnóstico que coleta os contadores de desempenho de nível de sistema padrão juntamente com alguns logs de eventos do windows e logs de infraestrutura de diagnóstico. Ele foi escape e formatado corretamente para que hello configuração diretamente colá-los na seção de variáveis de saudação do seu modelo. Consulte Olá [esquema de configuração de diagnóstico](https://msdn.microsoft.com/library/azure/dn782207.aspx) para obter um exemplo mais humano legível do xml de configuração de saudação.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

Olá métricas definição o nó xml no hello acima de configuração é um elemento de configuração importantes que define como os contadores de desempenho de saudação definida anteriormente Olá xml no *PerformanceCounter* nó será agregado e armazenados. 

> [!IMPORTANT]
> Essas métricas unidade Olá monitoramento gráficos e alertas no hello portal do Azure.  Olá **métricas** nó com hello *resourceID* e **MetricAggregation** devem ser incluídos na configuração de diagnóstico Olá para sua VM se você quiser toosee Olá VM dados de monitoramento no hello portal do Azure. 
> 
> 

a seguir Olá é um exemplo de xml Olá definições de métricas: 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Olá *resourceID* atributo identifica exclusivamente a máquina virtual de saudação em sua assinatura. Verifique se subscription() de saudação toouse e resourceGroup() funções para que hello modelo atualiza automaticamente esses valores com base no grupo de assinatura e do recurso de saudação que você está implantando.

Se você estiver criando várias máquinas virtuais em um loop, você terá Olá toopopulate *resourceID* valor com um toocorrectly de função copyIndex() diferenciar cada VM individual. Olá *xmlCfg* valor pode ser atualizada toosupport isso da seguinte maneira:  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

Olá valor MetricAggregation *PT1H* e *PT1M* representar uma agregação em um minuto e uma agregação em uma hora.

## <a name="wadmetrics-tables-in-storage"></a>Tabelas WADMetrics no armazenamento
configuração de métricas de Olá acima irá gerar tabelas na sua conta de armazenamento de diagnóstico com hello convenções de nomenclatura a seguir:

* **WADMetrics** : prefixo padrão para todas as tabelas WADMetrics
* **PT1H** ou **PT1M** : significa que essa tabela Olá contém dados de agregação em 1 hora ou 1 minuto
* **P10D** : significa tabela Olá conterá dados para 10 dias a partir de quando tabela Olá começar a coletar os dados
* **V2S** : constante de cadeia de caracteres
* **AAAAMMDD** : data de saudação no qual Olá tabela começar a coletar os dados

Exemplo: *WADMetricsPT1HP10DV2S20151108* inclui dados agregados das métricas para o período de uma hora durante 10 dias, com início em 11 de novembro de 2015    

Cada tabela WADMetrics conterá Olá colunas a seguir:

* **PartitionKey**: partitionkey Olá é construído com base em Olá *resourceID* toouniquely valor identificar Olá de recursos VM. por exemplo: 002Fsubscriptions:<subscriptionID>:002FresourceGroups:002F<ResourceGroupName>:002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : formato de saudação de maneira <Descending time tick>:<Performance Counter Name>. Olá decrescente cálculo de escala de tempo é escalas de tempo máximo menos tempo de saudação do início de saudação do período de agregação de saudação. Por exemplo Se o período de exemplo hello iniciado em 10 de novembro de 2015 e cálculo de UTC, em seguida, Olá 00:00Hrs seria: ticks - (DateTime(2015,11,10,0,0,0,DateTimeKind.Utc) novo. Tiques). Para Olá memória bytes disponíveis chave contador de desempenho Olá linha aparecerá como: 2519551871999999999__:005CMemory:005CAvailable:0020 Bytes
* **CounterName** : É nome Olá Olá do contador de desempenho. Isso corresponde a saudação *counterSpecifier* definido na configuração do xml de saudação.
* **Máximo** : Olá valor máximo do contador de desempenho de saudação em período de agregação de saudação.
* **Mínimo** : Olá valor mínimo saudação do contador de desempenho por período de agregação de saudação.
* **Total** : soma de saudação de todos os valores de contador de desempenho Olá informado por período de agregação de saudação.
* **Contagem de** : número total de saudação de valores relatados para o contador de desempenho hello.
* **Médio** : Olá valor médio (total/contagem) saudação do contador de desempenho por período de agregação de saudação.

## <a name="next-steps"></a>Próximas etapas
* Para obter um modelo de exemplo completo de uma máquina virtual do Windows com extensão de diagnóstico, confira [201-vm-monitoring-diagnostics-extension](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Implantar o modelo de Gerenciador de recursos de saudação usando [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [linha de comando do Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Saiba mais sobre a [Criação de modelos do Gerenciador de Recursos do Azure](../../resource-group-authoring-templates.md)

