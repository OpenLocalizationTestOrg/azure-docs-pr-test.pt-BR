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
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>Habilitar o diagnóstico nos Serviços de Nuvem do Azure usando o PowerShell
Você pode coletar dados de diagnóstico como logs de aplicativos, etc. de um serviço de nuvem usando os contadores de desempenho Olá extensão de diagnóstico do Azure. Este artigo descreve como tooenable Olá extensão de diagnóstico do Azure para um serviço de nuvem usando o PowerShell.  Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) pré-requisitos Olá necessários para este artigo.

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Habilitar a extensão de diagnóstico como parte da implantação de um Serviço de Nuvem
Essa abordagem é o tipo de integração toocontinuous aplicáveis de cenários onde o diagnóstico Olá extensão pode ser habilitada como parte da implantação de Olá serviço de nuvem. Ao criar uma nova implantação do serviço de nuvem você pode habilitar a extensão de diagnóstico Olá passando Olá *ExtensionConfiguration* parâmetro toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet. Olá *ExtensionConfiguration* parâmetro pega uma matriz de configurações de diagnóstico que podem ser criados usando Olá [AzureServiceDiagnosticsExtensionConfig novo](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.

Olá exemplo a seguir mostra como você pode habilitar o diagnóstico para um serviço de nuvem com um WebRole e WorkerRole, cada um tendo uma configuração de diagnóstico diferentes.

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

Se o arquivo de configuração de diagnóstico de saudação especifica um `StorageAccount` elemento com um nome de conta de armazenamento, em seguida, Olá `New-AzureServiceDiagnosticsExtensionConfig` cmdlet usará automaticamente a conta de armazenamento. Para este toowork, conta de armazenamento Olá precisa toobe em Olá a mesma assinatura conforme Olá serviço de nuvem que está sendo implantado.

Do SDK 2.6 do Azure, arquivos de configuração de extensão de saudação daí gerados pelo Olá MSBuild publicar a saída de destino incluirá o nome de conta de armazenamento Olá com base na cadeia de configuração de diagnóstico de saudação especificada no arquivo de configuração de serviço hello (. cscfg). script de saudação abaixo mostra como arquivos de configuração de extensão tooparse Olá de saudação saída de destino de publicação e configurar a extensão de diagnóstico para cada função ao implantar o serviço de nuvem hello.

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

Visual Studio Online usa uma abordagem semelhante para implantações automatizadas de serviços de nuvem com a extensão de diagnóstico de saudação. Confira [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) para obter um exemplo completo.

Se nenhum `StorageAccount` foi especificado na configuração de diagnóstico Olá, é necessário toopass em Olá *StorageAccountName* parâmetro toohello cmdlet. Se hello *StorageAccountName* parâmetro for especificado, então Olá cmdlet sempre usar a conta de armazenamento de saudação que é especificada no parâmetro hello e não Olá que é especificado no arquivo de configuração de diagnóstico de saudação.

Se passar Olá Olá diagnóstico conta de armazenamento está em uma assinatura diferente da saudação serviço de nuvem, em seguida, você precisa tooexplicitly *StorageAccountName* e *StorageAccountKey* parâmetros toohello cmdlet. Olá *StorageAccountKey* parâmetro não é necessária ao diagnóstico Olá conta de armazenamento está em Olá mesma assinatura, como o cmdlet Olá automaticamente pode consultar e definir o valor da chave Olá ao habilitar a extensão de diagnóstico de saudação. No entanto, se hello conta de armazenamento de diagnóstico está em uma assinatura diferente, e em seguida, Olá cmdlet pode não ser capaz de tooget chave de saudação automaticamente e é necessário tooexplicitly especificar chave Olá por meio de saudação *StorageAccountKey* parâmetro.

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Habilitar extensão de diagnóstico em um Serviço de Nuvem existente
Você pode usar o hello [AzureServiceDiagnosticsExtension conjunto](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable ou atualização de configuração de diagnóstico em um serviço de nuvem que já está em execução.

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>Obter a configuração de extensão de diagnóstico atual
Saudação de uso [AzureServiceDiagnosticsExtension Get](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget Olá configuração de diagnóstico atual para um serviço de nuvem.

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>Remover extensão de diagnóstico
tooturn desativar o diagnóstico em uma nuvem de serviço você pode usar o hello [AzureServiceDiagnosticsExtension remover](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Se você habilitou a extensão de diagnóstico hello usando *conjunto AzureServiceDiagnosticsExtension* ou hello *novo AzureServiceDiagnosticsExtensionConfig* sem Olá *função* parâmetro, em seguida, você pode remover Olá extensão usando *remover AzureServiceDiagnosticsExtension* sem Olá *função* parâmetro. Se hello *função* parâmetro foi utilizado ao habilitar extensão hello, em seguida, ele também deve ser usado ao remover a extensão de saudação.

extensão de diagnóstico tooremove saudação de cada função individual:

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>Próximas etapas
* Para obter orientação adicional sobre como usar o diagnóstico do Azure e outros problemas de tootroubleshoot técnicas, consulte [habilitando o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](cloud-services-dotnet-diagnostics.md).
* Olá [esquema de configuração de diagnóstico](https://msdn.microsoft.com/library/azure/dn782207.aspx) explica Olá opções de várias configurações de xml para extensão de diagnóstico de saudação.
* toolearn como extensão de diagnóstico tooenable Olá para máquinas virtuais, consulte [criar uma máquina Virtual do Windows com o monitoramento e diagnóstico usando o modelo do Gerenciador de recursos do Azure](../virtual-machines/windows/extensions-diagnostics-template.md)
