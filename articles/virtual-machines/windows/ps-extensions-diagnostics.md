---
title: "Usar o Azure PowerShell para habilitar o diagnóstico em uma máquina virtual Windows | Microsoft Docs"
services: virtual-machines-windows
documentationcenter: 
description: "Usar o PowerShell para habilitar o Diagnóstico do Azure em uma máquina virtual que executa o Windows"
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
ms.openlocfilehash: d0be4a712657edfc516c5f32e66519f5d9486728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="46fbe-103">Usar o PowerShell para habilitar o Diagnóstico do Azure em uma máquina virtual que executa o Windows</span><span class="sxs-lookup"><span data-stu-id="46fbe-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="46fbe-104">O Diagnóstico do Azure é a capacidade do Azure que habilita a coleta de dados de diagnóstico em um aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="46fbe-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="46fbe-105">Você pode usar a extensão de diagnóstico para coletar dados de diagnóstico como logs de aplicativo ou contadores de desempenho de uma máquina virtual (VM) do Azure que executa o Windows.</span><span class="sxs-lookup"><span data-stu-id="46fbe-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="46fbe-106">Este artigo descreve como usar o Windows PowerShell para habilitar a extensão de diagnóstico para uma VM.</span><span class="sxs-lookup"><span data-stu-id="46fbe-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span></span> <span data-ttu-id="46fbe-107">Consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) para os pré-requisitos necessários para este artigo.</span><span class="sxs-lookup"><span data-stu-id="46fbe-107">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a><span data-ttu-id="46fbe-108">Habilitar a extensão de diagnóstico se você usar o modelo de implantação do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="46fbe-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span></span>
<span data-ttu-id="46fbe-109">Você pode habilitar a extensão de diagnóstico enquanto cria uma VM do Windows por meio do modelo de implantação do Gerenciador de Recursos do Azure adicionando a configuração da extensão ao modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="46fbe-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span></span> <span data-ttu-id="46fbe-110">Consulte [Criar uma máquina virtual do Windows com monitoramento e diagnóstico usando o modelo do Azure Resource Manager](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="46fbe-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="46fbe-111">Para habilitar a extensão de diagnóstico em uma VM existente criada por meio do modelo de implantação do Resource Manager, é possível usar o cmdlet do PowerShell [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="46fbe-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="46fbe-112">*$diagnosticsconfig_path* é o caminho para o arquivo que contém a configuração de diagnóstico em XML, conforme descrito no [exemplo](#sample-diagnostics-configuration) abaixo.</span><span class="sxs-lookup"><span data-stu-id="46fbe-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="46fbe-113">Se o arquivo de configuração de diagnóstico especificar um elemento **StorageAccount** com um nome de conta de armazenamento, o script *Set-AzureRMVMDiagnosticsExtension* definirá automaticamente a extensão de diagnóstico para enviar dados de diagnóstico para essa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="46fbe-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span></span> <span data-ttu-id="46fbe-114">Para isso funcionar, a conta de armazenamento precisa estar na mesma assinatura que a VM.</span><span class="sxs-lookup"><span data-stu-id="46fbe-114">For this to work, the storage account needs to be in the same subscription as the VM.</span></span>

<span data-ttu-id="46fbe-115">Se nenhuma **StorageAccount** tiver sido especificada na configuração de diagnóstico, você precisará passar o parâmetro *StorageAccountName* para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="46fbe-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="46fbe-116">Se o parâmetro *StorageAccountName* for especificado, o cmdlet sempre usará a conta de armazenamento que está especificada no parâmetro, não aquela que está especificada no arquivo de configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="46fbe-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="46fbe-117">Se a conta de armazenamento de diagnóstico estiver em uma assinatura diferente da assinatura da VM, você precisará passar explicitamente os parâmetros *StorageAccountName* e *StorageAccountKey* para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="46fbe-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="46fbe-118">O parâmetro *StorageAccountKey* não é necessário quando a conta de armazenamento de diagnóstico está na mesma assinatura, uma vez que o cmdlet pode consultar e definir automaticamente o valor de chave ao habilitar a extensão de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="46fbe-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="46fbe-119">No entanto, se a conta de armazenamento de diagnóstico estiver em uma assinatura diferente, o cmdlet talvez não consiga obter a chave automaticamente e você precisará especificá-la explicitamente por meio do parâmetro *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="46fbe-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="46fbe-120">Depois que a extensão de diagnóstico estiver habilitada em uma VM, você poderá obter as configurações atuais usando o cmdlet [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="46fbe-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="46fbe-121">O cmdlet retorna *PublicSettings*, que contém a configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="46fbe-121">The cmdlet returns *PublicSettings*, which contains the diagnostics configuration.</span></span> <span data-ttu-id="46fbe-122">Há dois tipos de configuração com suporte, WadCfg e xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="46fbe-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="46fbe-123">WadCfg é a configuração JSON e xmlCfg é a configuração XML em um formato codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="46fbe-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="46fbe-124">Para ler o XML, você precisa decodificá-lo.</span><span class="sxs-lookup"><span data-stu-id="46fbe-124">To read the XML, you need to decode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="46fbe-125">O cmdlet [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) pode ser usado para remover a extensão de diagnóstico da VM.</span><span class="sxs-lookup"><span data-stu-id="46fbe-125">The [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used to remove the diagnostics extension from the VM.</span></span>  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a><span data-ttu-id="46fbe-126">Habilitar a extensão de diagnóstico se você usar o modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="46fbe-126">Enable the diagnostics extension if you use the classic deployment model</span></span>
<span data-ttu-id="46fbe-127">É possível usar o cmdlet [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) para habilitar a extensão de diagnóstico em uma VM criada usando o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="46fbe-127">You can use the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span></span> <span data-ttu-id="46fbe-128">O exemplo a seguir mostra como criar uma nova VM por meio do modelo de implantação clássico com a extensão de diagnóstico habilitada.</span><span class="sxs-lookup"><span data-stu-id="46fbe-128">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="46fbe-129">Para habilitar a extensão de diagnóstico em uma VM existente que foi criada por meio do modelo de implantação clássico, primeiramente use o cmdlet [Get-AzureVM](/powershell/module/azure/get-azurevm) para obter a configuração da VM.</span><span class="sxs-lookup"><span data-stu-id="46fbe-129">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet to get the VM configuration.</span></span> <span data-ttu-id="46fbe-130">Em seguida, atualize a configuração de VM para incluir a extensão de diagnóstico usando o cmdlet [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="46fbe-130">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="46fbe-131">Por fim, aplique a configuração atualizada à VM usando [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="46fbe-131">Finally, apply the updated configuration to the VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="46fbe-132">Exemplo de configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="46fbe-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="46fbe-133">O XML a seguir pode ser usado para a configuração de diagnóstico público com os scripts acima.</span><span class="sxs-lookup"><span data-stu-id="46fbe-133">The following XML can be used for the diagnostics public configuration with the above scripts.</span></span> <span data-ttu-id="46fbe-134">Este exemplo de configuração transferirá vários contadores de desempenho para a conta de armazenamento de diagnóstico junto com erros de aplicativo, segurança e canais do sistema nos logs de eventos do Windows e quaisquer erros dos logs de infraestrutura do diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="46fbe-134">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span></span>

<span data-ttu-id="46fbe-135">A configuração precisa ser atualizada para incluir o seguinte:</span><span class="sxs-lookup"><span data-stu-id="46fbe-135">The configuration needs to be updated to include the following:</span></span>

* <span data-ttu-id="46fbe-136">O atributo *resourceID* do elemento **Métricas** precisa ser atualizado com a ID de recurso para a VM.</span><span class="sxs-lookup"><span data-stu-id="46fbe-136">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span></span>
  
  * <span data-ttu-id="46fbe-137">A ID do recurso pode ser criada usando o seguinte padrão: "/subscriptions/{*ID da assinatura para a assinatura com a VM*}/resourceGroups/{*O nome do grupo de recursos para a VM*}/providers/Microsoft.Compute/virtualMachines/{*O nome da VM*}".</span><span class="sxs-lookup"><span data-stu-id="46fbe-137">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span></span>
  * <span data-ttu-id="46fbe-138">Por exemplo, se a ID de assinatura para a assinatura em que a VM está em execução for **11111111-1111-1111-1111-111111111111**, o nome do grupo de recursos para o grupo de recursos for **MyResourceGroup** e o nome da VM for **MyWindowsVM**, o valor de *resourceID* será:</span><span class="sxs-lookup"><span data-stu-id="46fbe-138">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="46fbe-139">Para obter mais informações sobre como as métricas são geradas com base na configuração de métricas e contadores de desempenho, veja a [Tabela de métricas do Diagnóstico do Azure no armazenamento](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="46fbe-139">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="46fbe-140">O elemento **StorageAccount** precisa ser atualizado com o nome da conta de armazenamento de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="46fbe-140">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span></span>
  
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
        <Metrics resourceId="(Update with resource ID for the VM)" >
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

## <a name="next-steps"></a><span data-ttu-id="46fbe-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46fbe-141">Next steps</span></span>
* <span data-ttu-id="46fbe-142">Para obter orientações adicionais sobre como usar a funcionalidade do Diagnóstico do Azure e outras técnicas para solucionar problemas, consulte [Habilitar o diagnóstico nos Serviços de Nuvem e nas Máquinas Virtuais do Azure](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="46fbe-142">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="46fbe-143">[esquema de configuração de diagnóstico](https://msdn.microsoft.com/library/azure/mt634524.aspx) explica as várias opções de configurações de XML para a extensão de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="46fbe-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span></span>

