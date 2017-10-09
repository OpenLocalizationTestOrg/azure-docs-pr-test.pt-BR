---
title: "aaaUse diagnóstico do Azure PowerShell tooenable em uma VM do Windows | Microsoft Docs"
services: virtual-machines-windows
documentationcenter: 
description: "Saiba como toouse PowerShell tooenable diagnóstico do Azure em uma máquina virtual que executa o Windows"
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Use o diagnóstico do Azure PowerShell tooenable em uma máquina virtual que executa o Windows
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Diagnóstico do Azure é a capacidade de saudação dentro do Azure que habilita a coleta de saudação de dados de diagnóstico em um aplicativo implantado. Você pode usar o hello diagnóstico extensão toocollect dados de diagnóstico como logs de aplicativos ou contadores de desempenho de uma máquina virtual do Azure (VM) que esteja executando o Windows. Este artigo descreve como toouse do Windows PowerShell tooenable Olá extensão de diagnóstico para uma máquina virtual. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) pré-requisitos Olá necessários para este artigo.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Habilitar a extensão de diagnóstico Olá se você usar o modelo de implantação do Gerenciador de recursos de saudação
Você pode habilitar a extensão de diagnóstico Olá durante a criação de uma VM do Windows por meio do modelo de implantação do Azure Resource Manager Olá adicionando o modelo do Gerenciador de recursos do hello extensão configuração toohello. Consulte [criar uma máquina virtual do Windows com o monitoramento e diagnóstico usando o modelo do Azure Resource Manager Olá](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

extensão de diagnóstico tooenable Olá em uma VM existente que foi criada por meio do modelo de implantação do Gerenciador de recursos de saudação, você pode usar o hello [AzureRMVMDiagnosticsExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) cmdlet do PowerShell, conforme mostrado abaixo.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* é Olá caminho toohello arquivo que contém a configuração de diagnóstico de saudação em XML, conforme descrito em Olá [exemplo](#sample-diagnostics-configuration) abaixo.  

Se o arquivo de configuração de diagnóstico de saudação especifica um **StorageAccount** elemento com um nome de conta de armazenamento, em seguida, Olá *AzureRMVMDiagnosticsExtension conjunto* script definirá automaticamente Olá conta de armazenamento do toothat dados de diagnóstico do diagnóstico extensão toosend. Para este toowork, conta de armazenamento Olá precisa toobe em Olá a mesma assinatura conforme Olá VM.

Se nenhum **StorageAccount** foi especificado na configuração de diagnóstico Olá, é necessário toopass em Olá *StorageAccountName* parâmetro toohello cmdlet. Se hello *StorageAccountName* parâmetro for especificado, então Olá cmdlet sempre usar a conta de armazenamento de saudação que é especificada no parâmetro hello e não Olá que é especificado no arquivo de configuração de diagnóstico de saudação.

Se passar Olá Olá diagnóstico conta de armazenamento está em uma assinatura diferente da saudação VM, em seguida, você precisa tooexplicitly *StorageAccountName* e *StorageAccountKey* parâmetros toohello cmdlet. Olá *StorageAccountKey* parâmetro não é necessária ao diagnóstico Olá conta de armazenamento está em Olá mesma assinatura, como o cmdlet Olá automaticamente pode consultar e definir o valor da chave Olá ao habilitar a extensão de diagnóstico de saudação. No entanto, se hello conta de armazenamento de diagnóstico está em uma assinatura diferente, e em seguida, Olá cmdlet pode não ser capaz de tooget chave de saudação automaticamente e é necessário tooexplicitly especificar chave Olá por meio de saudação *StorageAccountKey* parâmetro.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Depois que a extensão de diagnóstico de saudação é habilitada em uma máquina virtual, você pode obter as configurações atuais de saudação usando Olá [AzureRMVmDiagnosticsExtension Get](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Olá cmdlet retorna *PublicSettings*, que contém a configuração de diagnóstico de saudação. Há dois tipos de configuração com suporte, WadCfg e xmlCfg. WadCfg é a configuração JSON e xmlCfg é a configuração XML em um formato codificado na Base64. tooread Olá XML, você precisa toodecode-lo.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Olá [AzureRMVmDiagnosticsExtension remover](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet pode ser tooremove usado Olá extensão de diagnóstico de saudação VM.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Habilitar a extensão de diagnóstico Olá se você usar o modelo de implantação clássico Olá
Você pode usar o hello [AzureVMDiagnosticsExtension conjunto](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable uma extensão de diagnóstico em uma máquina virtual que você cria por meio do modelo de implantação clássico hello. Olá exemplo a seguir mostra como toocreate uma nova VM por meio do modelo de implantação clássico Olá com extensão de diagnóstico Olá habilitado.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

extensão de diagnóstico Olá tooenable em uma VM existente que foi criada por meio do modelo de implantação clássico hello, primeiro Olá de uso [Get-AzureVM](/powershell/module/azure/get-azurevm) configuração da VM cmdlet tooget hello. Em seguida, atualize a extensão de diagnóstico de Olá Olá VM configuração tooinclude usando Olá [AzureVMDiagnosticsExtension conjunto](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet. Por fim, aplicar Olá atualizado configuração toohello VM por meio de [Update-AzureVM](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>Exemplo de configuração de diagnóstico
Olá que XML a seguir pode ser usado para configuração pública do diagnóstico Olá com hello acima scripts. Nesta configuração de exemplo transferirá vários desempenho contadores toohello diagnóstico conta de armazenamento, juntamente com erros de aplicativo hello, segurança e canais de sistema em logs de eventos do Windows hello e quaisquer erros de diagnóstico Olá logs de infraestrutura.

configuração de saudação precisa seguinte de saudação do toobe tooinclude atualizado:

* Olá *resourceID* atributo de saudação **métricas** elemento precisa toobe atualizada com ID de recurso de saudação do hello VM.
  
  * Olá recurso ID pode ser construído usando o saudação padrão a seguir: "assinaturas / {*ID da assinatura para a assinatura de saudação com hello VM*} /resourceGroups/ {*nome resourcegroup Olá Olá VM*} / providers/Microsoft.Compute/virtualMachines/ {*Olá nome da VM*} ".
  * Por exemplo, se hello ID de assinatura para a assinatura de saudação onde hello VM está em execução é **11111111-1111-1111-1111-111111111111**, nome do grupo de recursos Olá Olá para grupo de recursos é **MyResourceGroup**, e hello nome da VM é **MyWindowsVM**, Olá, em seguida, o valor para *resourceID* seria:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Para obter mais informações sobre como as métricas são os contadores de desempenho gerados Olá com base no e a configuração de métricas, consulte [tabela de métricas de diagnóstico do Azure no armazenamento](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* Olá **StorageAccount** elemento precisa toobe atualizada com nome Olá Olá diagnóstico da conta de armazenamento.
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for hello VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a>Próximas etapas
* Para obter orientação adicional sobre como usar o recurso de diagnóstico do Azure hello e outros problemas de tootroubleshoot técnicas, consulte [habilitando o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [Esquema de configurações de diagnóstico](https://msdn.microsoft.com/library/azure/mt634524.aspx) explica Olá opções de várias configurações de XML para extensão de diagnóstico de saudação.

