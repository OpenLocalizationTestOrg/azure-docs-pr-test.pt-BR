---
title: "Habilitar o diagnóstico nos Serviços de Nuvem do Azure usando o PowerShell | Microsoft Docs"
description: "Saiba como habilitar o diagnóstico nos serviços de nuvem usando o PowerShell"
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
ms.openlocfilehash: 8dd9724981860c9cd4ccc443cc2bfdc465811e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="ff67f-103">Habilitar o diagnóstico nos Serviços de Nuvem do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff67f-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="ff67f-104">Você pode coletar dados de diagnóstico, como logs de aplicativo, contador de desempenho, etc., a partir de um Serviço de Nuvem usando a extensão de Diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff67f-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using the Azure Diagnostics extension.</span></span> <span data-ttu-id="ff67f-105">Este artigo descreve como habilitar a extensão de Diagnóstico do Azure para um Serviço de Nuvem usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff67f-105">This article describes how to enable the Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="ff67f-106">Consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) para os pré-requisitos necessários para este artigo.</span><span class="sxs-lookup"><span data-stu-id="ff67f-106">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="ff67f-107">Habilitar a extensão de diagnóstico como parte da implantação de um Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="ff67f-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="ff67f-108">Essa abordagem é aplicável ao tipo de cenários de integração contínua no qual a extensão de diagnóstico pode ser habilitada como parte da implantação do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ff67f-108">This approach is applicable to continuous integration type of scenarios, where the diagnostics extension can be enabled as part of deploying the cloud service.</span></span> <span data-ttu-id="ff67f-109">Ao criar uma nova implantação de Serviço de Nuvem, você pode habilitar a extensão do diagnóstico passando o parâmetro *ExtensionConfiguration* para o cmdlet [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="ff67f-109">When creating a new Cloud Service deployment you can enable the diagnostics extension by passing in the *ExtensionConfiguration* parameter to the [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="ff67f-110">O parâmetro *ExtensionConfiguration* obtém uma série de configurações de diagnóstico que podem ser criadas usando o cmdlet [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="ff67f-110">The *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using the [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="ff67f-111">O exemplo a seguir mostra como você pode habilitar o diagnóstico para um serviço de nuvem com um WebRole e WorkerRole, cada um com uma configuração de diagnóstico diferente.</span><span class="sxs-lookup"><span data-stu-id="ff67f-111">The following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="ff67f-112">Se o arquivo de configuração do diagnóstico especificar um elemento `StorageAccount` com um nome de conta de armazenamento, o cmdlet `New-AzureServiceDiagnosticsExtensionConfig` usará automaticamente essa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ff67f-112">If the diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="ff67f-113">Para que isso funcione, a conta de armazenamento precisa estar na mesma assinatura que o Serviço de Nuvem que está sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="ff67f-113">For this to work, the storage account needs to be in the same subscription as the Cloud Service being deployed.</span></span>

<span data-ttu-id="ff67f-114">A partir do SDK 2.6 do Azure, os arquivos de configuração de extensão gerados pela saída de destino de publicação do MSBuild incluirá o nome da conta de armazenamento, com base na cadeia de configuração de diagnóstico especificada no arquivo de configuração de serviço (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="ff67f-114">From Azure SDK 2.6 onward the extension configuration files generated by the MSBuild publish target output will include the storage account name based on the diagnostics configuration string specified in the service configuration file (.cscfg).</span></span> <span data-ttu-id="ff67f-115">O script a seguir mostra como analisar os arquivos de configuração de extensão da saída de destino de publicação, e como configurar a extensão de diagnóstico para cada função durante a implantação do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ff67f-115">The script below shows you how to parse the Extension configuration files from the publish target output and configure diagnostics extension for each role when deploying the cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find the Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find the RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
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

<span data-ttu-id="ff67f-116">O Visual Studio Online usa uma abordagem parecida para implantações automatizadas dos Serviços de Nuvem com a extensão de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ff67f-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with the diagnostics extension.</span></span> <span data-ttu-id="ff67f-117">Confira [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) para obter um exemplo completo.</span><span class="sxs-lookup"><span data-stu-id="ff67f-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="ff67f-118">Se nenhuma `StorageAccount` tiver sido especificada na configuração de diagnóstico, você precisará passar o parâmetro *StorageAccountName* para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ff67f-118">If no `StorageAccount` was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="ff67f-119">Se o parâmetro *StorageAccountName* for especificado, o cmdlet sempre usará a conta de armazenamento que está especificada no parâmetro, não aquela que está especificada no arquivo de configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ff67f-119">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="ff67f-120">Se a conta de armazenamento de diagnóstico estiver em uma assinatura diferente do Serviço de Nuvem, será necessário transmitir explicitamente os parâmetros *StorageAccountName* e *StorageAccountKey* para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ff67f-120">If the diagnostics storage account is in a different subscription from the Cloud Service, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="ff67f-121">O parâmetro *StorageAccountKey* não é necessário quando a conta de armazenamento de diagnóstico está na mesma assinatura, uma vez que o cmdlet pode consultar e definir automaticamente o valor de chave ao habilitar a extensão de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ff67f-121">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="ff67f-122">No entanto, se a conta de armazenamento de diagnóstico estiver em uma assinatura diferente, o cmdlet talvez não consiga obter a chave automaticamente e você precisará especificá-la explicitamente por meio do parâmetro *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="ff67f-122">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="ff67f-123">Habilitar extensão de diagnóstico em um Serviço de Nuvem existente</span><span class="sxs-lookup"><span data-stu-id="ff67f-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="ff67f-124">Você pode usar o cmdlet [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) para habilitar ou atualizar a configuração do diagnóstico em um Serviço de Nuvem que já está em execução.</span><span class="sxs-lookup"><span data-stu-id="ff67f-124">You can use the [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to enable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="ff67f-125">Obter a configuração de extensão de diagnóstico atual</span><span class="sxs-lookup"><span data-stu-id="ff67f-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="ff67f-126">Usar o cmdlet [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) para obter a configuração de diagnóstico atual para um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ff67f-126">Use the [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to get the current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="ff67f-127">Remover extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ff67f-127">Remove diagnostics extension</span></span>
<span data-ttu-id="ff67f-128">Para desativar o diagnóstico em um serviço de nuvem, você pode usar o cmdlet [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="ff67f-128">To turn off diagnostics on a cloud service you can use the [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="ff67f-129">Se você tiver habilitado a extensão de diagnóstico usando o *Set-AzureServiceDiagnosticsExtension* ou o *New-AzureServiceDiagnosticsExtensionConfig* sem o parâmetro *Função*, pode remover a extensão usando *Remove-AzureServiceDiagnosticsExtension* sem o parâmetro *Função*.</span><span class="sxs-lookup"><span data-stu-id="ff67f-129">If you enabled the diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or the *New-AzureServiceDiagnosticsExtensionConfig* without the *Role* parameter then you can remove the extension using *Remove-AzureServiceDiagnosticsExtension* without the *Role* parameter.</span></span> <span data-ttu-id="ff67f-130">Se o parâmetro *Função* tiver sido usado ao habilitar a extensão, ele também deverá ser usado ao removê-la.</span><span class="sxs-lookup"><span data-stu-id="ff67f-130">If the *Role* parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="ff67f-131">Para remover a extensão de diagnóstico de cada função individual:</span><span class="sxs-lookup"><span data-stu-id="ff67f-131">To remove the diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="ff67f-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff67f-132">Next Steps</span></span>
* <span data-ttu-id="ff67f-133">Para obter orientação adicional sobre como usar o diagnóstico do Azure e outras técnicas para solucionar problemas, consulte [Habilitar o Diagnóstico nos Serviços de Nuvem do Azure e Máquinas Virtuais](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ff67f-133">For additional guidance on using Azure diagnostics and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="ff67f-134">O [Esquema de Configuração de Diagnóstico](https://msdn.microsoft.com/library/azure/dn782207.aspx) explica as várias opções de configurações de XML para a extensão de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ff67f-134">The [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains the various xml configurations options for the diagnostics extension.</span></span>
* <span data-ttu-id="ff67f-135">Para saber como habilitar a extensão de diagnóstico para Máquinas Virtuais, consulte [Criar uma Máquina Virtual do Windows com monitoramento e diagnóstico usando o Modelo do Gerenciador de Recursos do Azure](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="ff67f-135">To learn how to enable the diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
