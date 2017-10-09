---
title: "aaaEnable diagnóstico nos serviços de nuvem do Azure usando o PowerShell | Microsoft Docs"
description: "Saiba como o diagnóstico tooenable para nuvem services usando o PowerShell"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="685cc-103">Habilitar o diagnóstico nos Serviços de Nuvem do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="685cc-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="685cc-104">Você pode coletar dados de diagnóstico como logs de aplicativos, etc. de um serviço de nuvem usando os contadores de desempenho Olá extensão de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="685cc-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="685cc-105">Este artigo descreve como tooenable Olá extensão de diagnóstico do Azure para um serviço de nuvem usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="685cc-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="685cc-106">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) pré-requisitos Olá necessários para este artigo.</span><span class="sxs-lookup"><span data-stu-id="685cc-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="685cc-107">Habilitar a extensão de diagnóstico como parte da implantação de um Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="685cc-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="685cc-108">Essa abordagem é o tipo de integração toocontinuous aplicáveis de cenários onde o diagnóstico Olá extensão pode ser habilitada como parte da implantação de Olá serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="685cc-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="685cc-109">Ao criar uma nova implantação do serviço de nuvem você pode habilitar a extensão de diagnóstico Olá passando Olá *ExtensionConfiguration* parâmetro toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="685cc-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="685cc-110">Olá *ExtensionConfiguration* parâmetro pega uma matriz de configurações de diagnóstico que podem ser criados usando Olá [AzureServiceDiagnosticsExtensionConfig novo](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="685cc-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="685cc-111">Olá exemplo a seguir mostra como você pode habilitar o diagnóstico para um serviço de nuvem com um WebRole e WorkerRole, cada um tendo uma configuração de diagnóstico diferentes.</span><span class="sxs-lookup"><span data-stu-id="685cc-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

<span data-ttu-id="685cc-112">Se o arquivo de configuração de diagnóstico de saudação especifica um `StorageAccount` elemento com um nome de conta de armazenamento, em seguida, Olá `New-AzureServiceDiagnosticsExtensionConfig` cmdlet usará automaticamente a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="685cc-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="685cc-113">Para este toowork, conta de armazenamento Olá precisa toobe em Olá a mesma assinatura conforme Olá serviço de nuvem que está sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="685cc-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="685cc-114">Do SDK 2.6 do Azure, arquivos de configuração de extensão de saudação daí gerados pelo Olá MSBuild publicar a saída de destino incluirá o nome de conta de armazenamento Olá com base na cadeia de configuração de diagnóstico de saudação especificada no arquivo de configuração de serviço hello (. cscfg).</span><span class="sxs-lookup"><span data-stu-id="685cc-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="685cc-115">script de saudação abaixo mostra como arquivos de configuração de extensão tooparse Olá de saudação saída de destino de publicação e configurar a extensão de diagnóstico para cada função ao implantar o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="685cc-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

<span data-ttu-id="685cc-116">Visual Studio Online usa uma abordagem semelhante para implantações automatizadas de serviços de nuvem com a extensão de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="685cc-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="685cc-117">Confira [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) para obter um exemplo completo.</span><span class="sxs-lookup"><span data-stu-id="685cc-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="685cc-118">Se nenhum `StorageAccount` foi especificado na configuração de diagnóstico Olá, é necessário toopass em Olá *StorageAccountName* parâmetro toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="685cc-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="685cc-119">Se hello *StorageAccountName* parâmetro for especificado, então Olá cmdlet sempre usar a conta de armazenamento de saudação que é especificada no parâmetro hello e não Olá que é especificado no arquivo de configuração de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="685cc-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="685cc-120">Se passar Olá Olá diagnóstico conta de armazenamento está em uma assinatura diferente da saudação serviço de nuvem, em seguida, você precisa tooexplicitly *StorageAccountName* e *StorageAccountKey* parâmetros toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="685cc-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="685cc-121">Olá *StorageAccountKey* parâmetro não é necessária ao diagnóstico Olá conta de armazenamento está em Olá mesma assinatura, como o cmdlet Olá automaticamente pode consultar e definir o valor da chave Olá ao habilitar a extensão de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="685cc-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="685cc-122">No entanto, se hello conta de armazenamento de diagnóstico está em uma assinatura diferente, e em seguida, Olá cmdlet pode não ser capaz de tooget chave de saudação automaticamente e é necessário tooexplicitly especificar chave Olá por meio de saudação *StorageAccountKey* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="685cc-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="685cc-123">Habilitar extensão de diagnóstico em um Serviço de Nuvem existente</span><span class="sxs-lookup"><span data-stu-id="685cc-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="685cc-124">Você pode usar o hello [AzureServiceDiagnosticsExtension conjunto](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable ou atualização de configuração de diagnóstico em um serviço de nuvem que já está em execução.</span><span class="sxs-lookup"><span data-stu-id="685cc-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="685cc-125">Obter a configuração de extensão de diagnóstico atual</span><span class="sxs-lookup"><span data-stu-id="685cc-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="685cc-126">Saudação de uso [AzureServiceDiagnosticsExtension Get](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget Olá configuração de diagnóstico atual para um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="685cc-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="685cc-127">Remover extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="685cc-127">Remove diagnostics extension</span></span>
<span data-ttu-id="685cc-128">tooturn desativar o diagnóstico em uma nuvem de serviço você pode usar o hello [AzureServiceDiagnosticsExtension remover](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="685cc-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="685cc-129">Se você habilitou a extensão de diagnóstico hello usando *conjunto AzureServiceDiagnosticsExtension* ou hello *novo AzureServiceDiagnosticsExtensionConfig* sem Olá *função* parâmetro, em seguida, você pode remover Olá extensão usando *remover AzureServiceDiagnosticsExtension* sem Olá *função* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="685cc-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="685cc-130">Se hello *função* parâmetro foi utilizado ao habilitar extensão hello, em seguida, ele também deve ser usado ao remover a extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="685cc-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="685cc-131">extensão de diagnóstico tooremove saudação de cada função individual:</span><span class="sxs-lookup"><span data-stu-id="685cc-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="685cc-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="685cc-132">Next Steps</span></span>
* <span data-ttu-id="685cc-133">Para obter orientação adicional sobre como usar o diagnóstico do Azure e outros problemas de tootroubleshoot técnicas, consulte [habilitando o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="685cc-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="685cc-134">Olá [esquema de configuração de diagnóstico](https://msdn.microsoft.com/library/azure/dn782207.aspx) explica Olá opções de várias configurações de xml para extensão de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="685cc-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="685cc-135">toolearn como extensão de diagnóstico tooenable Olá para máquinas virtuais, consulte [criar uma máquina Virtual do Windows com o monitoramento e diagnóstico usando o modelo do Gerenciador de recursos do Azure](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="685cc-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
