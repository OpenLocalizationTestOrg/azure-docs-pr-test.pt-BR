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
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="ca08a-103">Use o diagnóstico do Azure PowerShell tooenable em uma máquina virtual que executa o Windows</span><span class="sxs-lookup"><span data-stu-id="ca08a-103">Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ca08a-104">Diagnóstico do Azure é a capacidade de saudação dentro do Azure que habilita a coleta de saudação de dados de diagnóstico em um aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="ca08a-104">Azure Diagnostics is hello capability within Azure that enables hello collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="ca08a-105">Você pode usar o hello diagnóstico extensão toocollect dados de diagnóstico como logs de aplicativos ou contadores de desempenho de uma máquina virtual do Azure (VM) que esteja executando o Windows.</span><span class="sxs-lookup"><span data-stu-id="ca08a-105">You can use hello diagnostics extension toocollect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="ca08a-106">Este artigo descreve como toouse do Windows PowerShell tooenable Olá extensão de diagnóstico para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ca08a-106">This article describes how toouse Windows PowerShell tooenable hello diagnostics extension for a VM.</span></span> <span data-ttu-id="ca08a-107">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) pré-requisitos Olá necessários para este artigo.</span><span class="sxs-lookup"><span data-stu-id="ca08a-107">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a><span data-ttu-id="ca08a-108">Habilitar a extensão de diagnóstico Olá se você usar o modelo de implantação do Gerenciador de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="ca08a-108">Enable hello diagnostics extension if you use hello Resource Manager deployment model</span></span>
<span data-ttu-id="ca08a-109">Você pode habilitar a extensão de diagnóstico Olá durante a criação de uma VM do Windows por meio do modelo de implantação do Azure Resource Manager Olá adicionando o modelo do Gerenciador de recursos do hello extensão configuração toohello.</span><span class="sxs-lookup"><span data-stu-id="ca08a-109">You can enable hello diagnostics extension while you create a Windows VM through hello Azure Resource Manager deployment model by adding hello extension configuration toohello Resource Manager template.</span></span> <span data-ttu-id="ca08a-110">Consulte [criar uma máquina virtual do Windows com o monitoramento e diagnóstico usando o modelo do Azure Resource Manager Olá](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ca08a-110">See [Create a Windows virtual machine with monitoring and diagnostics by using hello Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ca08a-111">extensão de diagnóstico tooenable Olá em uma VM existente que foi criada por meio do modelo de implantação do Gerenciador de recursos de saudação, você pode usar o hello [AzureRMVMDiagnosticsExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) cmdlet do PowerShell, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ca08a-111">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="ca08a-112">*$diagnosticsconfig_path* é Olá caminho toohello arquivo que contém a configuração de diagnóstico de saudação em XML, conforme descrito em Olá [exemplo](#sample-diagnostics-configuration) abaixo.</span><span class="sxs-lookup"><span data-stu-id="ca08a-112">*$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML, as described in hello [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="ca08a-113">Se o arquivo de configuração de diagnóstico de saudação especifica um **StorageAccount** elemento com um nome de conta de armazenamento, em seguida, Olá *AzureRMVMDiagnosticsExtension conjunto* script definirá automaticamente Olá conta de armazenamento do toothat dados de diagnóstico do diagnóstico extensão toosend.</span><span class="sxs-lookup"><span data-stu-id="ca08a-113">If hello diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then hello *Set-AzureRMVMDiagnosticsExtension* script will automatically set hello diagnostics extension toosend diagnostic data toothat storage account.</span></span> <span data-ttu-id="ca08a-114">Para este toowork, conta de armazenamento Olá precisa toobe em Olá a mesma assinatura conforme Olá VM.</span><span class="sxs-lookup"><span data-stu-id="ca08a-114">For this toowork, hello storage account needs toobe in hello same subscription as hello VM.</span></span>

<span data-ttu-id="ca08a-115">Se nenhum **StorageAccount** foi especificado na configuração de diagnóstico Olá, é necessário toopass em Olá *StorageAccountName* parâmetro toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca08a-115">If no **StorageAccount** was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="ca08a-116">Se hello *StorageAccountName* parâmetro for especificado, então Olá cmdlet sempre usar a conta de armazenamento de saudação que é especificada no parâmetro hello e não Olá que é especificado no arquivo de configuração de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca08a-116">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="ca08a-117">Se passar Olá Olá diagnóstico conta de armazenamento está em uma assinatura diferente da saudação VM, em seguida, você precisa tooexplicitly *StorageAccountName* e *StorageAccountKey* parâmetros toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca08a-117">If hello diagnostics storage account is in a different subscription from hello VM, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="ca08a-118">Olá *StorageAccountKey* parâmetro não é necessária ao diagnóstico Olá conta de armazenamento está em Olá mesma assinatura, como o cmdlet Olá automaticamente pode consultar e definir o valor da chave Olá ao habilitar a extensão de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca08a-118">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="ca08a-119">No entanto, se hello conta de armazenamento de diagnóstico está em uma assinatura diferente, e em seguida, Olá cmdlet pode não ser capaz de tooget chave de saudação automaticamente e é necessário tooexplicitly especificar chave Olá por meio de saudação *StorageAccountKey* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ca08a-119">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="ca08a-120">Depois que a extensão de diagnóstico de saudação é habilitada em uma máquina virtual, você pode obter as configurações atuais de saudação usando Olá [AzureRMVmDiagnosticsExtension Get](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca08a-120">Once hello diagnostics extension is enabled on a VM, you can get hello current settings by using hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="ca08a-121">Olá cmdlet retorna *PublicSettings*, que contém a configuração de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca08a-121">hello cmdlet returns *PublicSettings*, which contains hello diagnostics configuration.</span></span> <span data-ttu-id="ca08a-122">Há dois tipos de configuração com suporte, WadCfg e xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="ca08a-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="ca08a-123">WadCfg é a configuração JSON e xmlCfg é a configuração XML em um formato codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="ca08a-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="ca08a-124">tooread Olá XML, você precisa toodecode-lo.</span><span class="sxs-lookup"><span data-stu-id="ca08a-124">tooread hello XML, you need toodecode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="ca08a-125">Olá [AzureRMVmDiagnosticsExtension remover](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet pode ser tooremove usado Olá extensão de diagnóstico de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="ca08a-125">hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used tooremove hello diagnostics extension from hello VM.</span></span>  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a><span data-ttu-id="ca08a-126">Habilitar a extensão de diagnóstico Olá se você usar o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="ca08a-126">Enable hello diagnostics extension if you use hello classic deployment model</span></span>
<span data-ttu-id="ca08a-127">Você pode usar o hello [AzureVMDiagnosticsExtension conjunto](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable uma extensão de diagnóstico em uma máquina virtual que você cria por meio do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="ca08a-127">You can use hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable a diagnostics extension on a VM that you create through hello classic deployment model.</span></span> <span data-ttu-id="ca08a-128">Olá exemplo a seguir mostra como toocreate uma nova VM por meio do modelo de implantação clássico Olá com extensão de diagnóstico Olá habilitado.</span><span class="sxs-lookup"><span data-stu-id="ca08a-128">hello following example shows how toocreate a new VM through hello classic deployment model with hello diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="ca08a-129">extensão de diagnóstico Olá tooenable em uma VM existente que foi criada por meio do modelo de implantação clássico hello, primeiro Olá de uso [Get-AzureVM](/powershell/module/azure/get-azurevm) configuração da VM cmdlet tooget hello.</span><span class="sxs-lookup"><span data-stu-id="ca08a-129">tooenable hello diagnostics extension on an existing VM that was created through hello classic deployment model, first use hello [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM configuration.</span></span> <span data-ttu-id="ca08a-130">Em seguida, atualize a extensão de diagnóstico de Olá Olá VM configuração tooinclude usando Olá [AzureVMDiagnosticsExtension conjunto](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca08a-130">Then update hello VM configuration tooinclude hello diagnostics extension by using hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="ca08a-131">Por fim, aplicar Olá atualizado configuração toohello VM por meio de [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="ca08a-131">Finally, apply hello updated configuration toohello VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="ca08a-132">Exemplo de configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ca08a-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="ca08a-133">Olá que XML a seguir pode ser usado para configuração pública do diagnóstico Olá com hello acima scripts.</span><span class="sxs-lookup"><span data-stu-id="ca08a-133">hello following XML can be used for hello diagnostics public configuration with hello above scripts.</span></span> <span data-ttu-id="ca08a-134">Nesta configuração de exemplo transferirá vários desempenho contadores toohello diagnóstico conta de armazenamento, juntamente com erros de aplicativo hello, segurança e canais de sistema em logs de eventos do Windows hello e quaisquer erros de diagnóstico Olá logs de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="ca08a-134">This sample configuration will transfer various performance counters toohello diagnostics storage account, along with errors from hello application, security, and system channels in hello Windows event logs and any errors from hello diagnostics infrastructure logs.</span></span>

<span data-ttu-id="ca08a-135">configuração de saudação precisa seguinte de saudação do toobe tooinclude atualizado:</span><span class="sxs-lookup"><span data-stu-id="ca08a-135">hello configuration needs toobe updated tooinclude hello following:</span></span>

* <span data-ttu-id="ca08a-136">Olá *resourceID* atributo de saudação **métricas** elemento precisa toobe atualizada com ID de recurso de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="ca08a-136">hello *resourceID* attribute of hello **Metrics** element needs toobe updated with hello resource ID for hello VM.</span></span>
  
  * <span data-ttu-id="ca08a-137">Olá recurso ID pode ser construído usando o saudação padrão a seguir: "assinaturas / {*ID da assinatura para a assinatura de saudação com hello VM*} /resourceGroups/ {*nome resourcegroup Olá Olá VM*} / providers/Microsoft.Compute/virtualMachines/ {*Olá nome da VM*} ".</span><span class="sxs-lookup"><span data-stu-id="ca08a-137">hello resource ID can be constructed by using hello following pattern: "/subscriptions/{*subscription ID for hello subscription with hello VM*}/resourceGroups/{*hello resourcegroup name for hello VM*}/providers/Microsoft.Compute/virtualMachines/{*hello VM Name*}".</span></span>
  * <span data-ttu-id="ca08a-138">Por exemplo, se hello ID de assinatura para a assinatura de saudação onde hello VM está em execução é **11111111-1111-1111-1111-111111111111**, nome do grupo de recursos Olá Olá para grupo de recursos é **MyResourceGroup**, e hello nome da VM é **MyWindowsVM**, Olá, em seguida, o valor para *resourceID* seria:</span><span class="sxs-lookup"><span data-stu-id="ca08a-138">For example, if hello subscription ID for hello subscription where hello VM is running is **11111111-1111-1111-1111-111111111111**, hello resource group name for hello resource group is **MyResourceGroup**, and hello VM Name is **MyWindowsVM**, then hello value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="ca08a-139">Para obter mais informações sobre como as métricas são os contadores de desempenho gerados Olá com base no e a configuração de métricas, consulte [tabela de métricas de diagnóstico do Azure no armazenamento](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="ca08a-139">For more information on how metrics are generated based on hello performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="ca08a-140">Olá **StorageAccount** elemento precisa toobe atualizada com nome Olá Olá diagnóstico da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ca08a-140">hello **StorageAccount** element needs toobe updated with hello name of hello diagnostics storage account.</span></span>
  
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

## <a name="next-steps"></a><span data-ttu-id="ca08a-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca08a-141">Next steps</span></span>
* <span data-ttu-id="ca08a-142">Para obter orientação adicional sobre como usar o recurso de diagnóstico do Azure hello e outros problemas de tootroubleshoot técnicas, consulte [habilitando o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ca08a-142">For additional guidance on using hello Azure Diagnostics capability and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="ca08a-143">[Esquema de configurações de diagnóstico](https://msdn.microsoft.com/library/azure/mt634524.aspx) explica Olá opções de várias configurações de XML para extensão de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca08a-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains hello various XML configurations options for hello diagnostics extension.</span></span>

