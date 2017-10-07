---
title: "aaaVirtual computador extensões e recursos do Windows no Azure | Microsoft Docs"
description: "Saiba quais extensões estão disponíveis para as máquinas virtuais do Azure, agrupadas pelas funcionalidades fornecidas ou aperfeiçoadas."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a>Recursos e extensões da máquina virtual para Windows

Extensões da máquina virtual do Azure são pequenos aplicativos que fornecem tarefas de configuração e automação pós-implantação nas máquinas virtuais do Azure. Por exemplo, se uma máquina virtual requer a instalação de software, proteção contra vírus ou a configuração do Docker, uma extensão de VM pode ser usado toocomplete essas tarefas. Extensões VM do Azure podem ser executadas usando Olá CLI do Azure, o PowerShell, modelos do Gerenciador de recursos do Azure e Olá portal do Azure. Extensões podem ser agrupadas com uma nova implantação de máquina virtual ou executar qualquer sistema existente.

Este documento fornece uma visão geral de extensões de máquina virtual, pré-requisitos para usar extensões de máquina virtual e orientação sobre como toodetect, gerenciar e remover extensões de máquina virtual. Este documento fornece informações generalizadas, pois há muitas extensões de VM disponíveis e cada uma delas tem uma configuração possivelmente exclusiva. Detalhes de extensão podem ser encontrados em cada extensão individuais do documento toohello específico.

## <a name="use-cases-and-samples"></a>Casos de uso e exemplos

Há várias extensões de VM do Azure diferentes disponíveis, cada uma com um caso de uso específico. Alguns exemplos de caso de uso são:

- Se aplicam a máquina virtual do PowerShell Desired estado configurações tooa usando a extensão de saudação DSC para Windows. Para saber mais, confira [Extensão de configuração de Estado Desejado do Azure](extensions-dsc-overview.md).
- Configure o monitoramento de máquina virtual usando a extensão de VM do agente de monitoramento Microsoft hello. Para obter mais informações, consulte [tooLog de máquinas virtuais do Azure conectar análise](../../log-analytics/log-analytics-azure-vm-extension.md).
- Configure o monitoramento da infra-estrutura do Azure com hello Datadog extensão. Para obter mais informações, consulte Olá [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Configure uma máquina virtual do Azure usando o Chef. Para saber mais, veja [Automatizar a implantação de máquina virtual do Azure com o Chef](chef-automation.md).

Além disso extensões específicas de tooprocess, uma extensão de Script personalizado está disponível para máquinas virtuais Windows e Linux. Olá extensão de Script personalizado para o Windows permite que qualquer toobe de script do PowerShell executado em uma máquina virtual. Isso é útil para a criação de implantações do Azure que exigem uma configurações que vão além da capacidade das ferramentas nativas do Azure. Para saber mais, veja [Extensão de Script personalizado de VM do Windows](extensions-customscript.md).


## <a name="prerequisites"></a>Pré-requisitos

Cada extensão da máquina virtual pode ter seu próprio conjunto de pré-requisitos. Por exemplo, Olá extensão da VM Docker tem um pré-requisito de uma distribuição de Linux com suporte. Requisitos das extensões individuais são detalhados na documentação do hello específicas da extensão.

### <a name="azure-vm-agent"></a>Agente de VM do Azure
Agente de VM do Azure Olá gerencia a interação entre uma máquina virtual do Azure e o controlador de malha do Azure hello. Olá VM agent é responsável por muitos aspectos funcionais de implantação e gerenciamento de máquinas virtuais do Azure, incluindo a execução de extensões de VM. Agente de VM do Azure Olá foi pré-instalado no imagens do Azure Marketplace e pode ser instalado em sistemas operacionais com suporte.

Para saber mais sobre os sistemas operacionais com suporte e as instruções de instalação, confira [Agente de máquina virtual do Azure](agent-user-guide.md).

## <a name="discover-vm-extensions"></a>Descobrir extensões de VM
Muitas extensões de VM diferentes estão disponíveis para uso com as máquinas virtuais do Azure. toosee uma lista completa, execute Olá comando com o módulo do PowerShell do Azure Resource Manager Olá a seguir. Tornar-se de local de saudação desejada de toospecify quando você estiver executando este comando.

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>Executar extensões de VM

Extensões de máquina virtual do Azure podem ser executadas em máquinas virtuais existentes, que é útil quando você precisa toomake alterações de configuração ou recuperar de conectividade em uma VM já implantada. As extensões de VM também podem ser agrupadas com implantações de modelo do Azure Resource Manager. Usando extensões com modelos do Gerenciador de recursos, você pode habilitar toobe de máquinas virtuais do Azure implantadas e configuradas sem necessidade de saudação de intervenção de pós-implantação.

Olá métodos a seguir pode ser usado toorun uma extensão em uma máquina virtual existente.

### <a name="powershell"></a>PowerShell

Há vários comandos do PowerShell para a execução de extensões individuais. toosee executar Olá comandos do PowerShell a seguir uma lista.

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

Isso fornece o seguinte de toohello semelhante de saída:

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

Hello exemplo a seguir usa toodownload de extensão de Script personalizado Olá um script de um repositório GitHub em Olá máquina de virtual de destino e, em seguida, execute o script hello. Para obter mais informações sobre Olá extensão de Script personalizado, consulte [visão geral de extensões de Script personalizado](extensions-customscript.md).

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

Neste exemplo, Olá extensão de acesso da máquina virtual é a senha administrativa do hello tooreset usados de uma máquina virtual do Windows. Para obter mais informações sobre Olá extensão de acesso da máquina virtual, consulte [serviço de redefinição de área de trabalho remota em uma VM do Windows](reset-rdp.md).

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

Olá `Set-AzureRmVMExtension` comando pode ser usado toostart qualquer extensão VM. Para obter mais informações, consulte Olá [referência de conjunto AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).


### <a name="azure-portal"></a>Portal do Azure

Uma extensão de VM pode ser aplicado tooan de máquina virtual existente por meio de saudação portal do Azure. toodo portanto, selecione a máquina virtual de saudação deseja toouse, escolha **extensões**e clique em **adicionar**. Isso fornece uma lista de extensões disponíveis. Selecione Olá desejada e siga as etapas de saudação do Assistente de saudação.

Olá imagem a seguir mostra instalação Olá Olá extensão Antimalware da Microsoft da saudação portal do Azure.

![Instalar a extensão de antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Modelos do Gerenciador de Recursos do Azure

Extensões de VM podem ser adicionado tooan Azure Resource Manager modelo e executado com a implantação de saudação do modelo de saudação. Implantar extensões com um modelo é útil para a criação de implantações do Azure totalmente configuradas. Por exemplo, hello que JSON a seguir é obtido de um modelo do Gerenciador de recursos que implanta um conjunto de VMs com balanceamento de carga e um banco de dados do SQL Azure e, em seguida, instala um aplicativo .NET Core em cada VM. Olá extensão de VM cuida Olá da instalação do software.

Para obter mais informações, consulte Olá [modelo completo do Gerenciador de recursos](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Para saber mais, veja [Criação de modelos do Azure Resource Manager com extensões de VM do Windows](template-description.md#extensions).

## <a name="secure-vm-extension-data"></a>Proteger dados de extensão da VM

Quando você estiver executando uma extensão de VM, talvez seja necessário tooinclude informações confidenciais, como as credenciais, nomes de conta de armazenamento e chaves de acesso da conta de armazenamento. Muitas extensões VM incluem uma configuração protegida que criptografa os dados e a descriptografa apenas dentro de saudação máquina de virtual de destino. Cada extensão tem um esquema específico de configuração protegida, e cada um é detalhado na documentação específica associada à extensão.

saudação de exemplo a seguir mostra uma instância do hello extensão de Script personalizado para o Windows. Observe que tooexecute de comando Olá inclui um conjunto de credenciais. Neste exemplo, a saudação comando tooexecute não será criptografado.


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Proteger a cadeia de caracteres de execução de saudação movendo Olá **comando tooexecute** propriedade toohello **protegido** configuração.

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a>Solucionar problemas de extensões de VM

Cada extensão de VM pode ter etapas de solução de problemas específicas. Por exemplo, quando você estiver usando a extensão de Script personalizado hello, detalhes de execução de script podem ser encontrados localmente na Olá máquina virtual no qual a extensão de saudação foi executado. As etapas de solução de problemas específicas à extensão são detalhadas na documentação associada.

Olá etapas de solução de problemas a seguir se aplicam a tooall extensões de máquina virtual.

### <a name="view-extension-status"></a>Exibir o status da extensão

Depois que uma extensão de máquina virtual tiver sido executada em uma máquina virtual, use Olá status da extensão de tooreturn comando PowerShell a seguir. Substitua os nomes de parâmetro de exemplo por seus próprios valores. Olá `Name` parâmetro aceita nome hello dado toohello extensão em tempo de execução.

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

saída de Hello semelhante ao seguinte hello:

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

Status da extensão de execução também podem ser encontradas no hello portal do Azure. status de saudação tooview de uma extensão, a máquina virtual de select Olá, escolha **extensões**, e selecione Olá extensão desejado.

### <a name="rerun-vm-extensions"></a>Executar extensões de VM novamente

Pode haver casos em que uma extensão de máquina virtual deve toobe novamente. Você pode fazer isso, removendo a extensão hello e, em seguida, executar novamente a extensão de saudação com um método de execução de sua escolha. tooremove uma extensão, executar Olá comando com o módulo do PowerShell do Azure Olá a seguir. Substitua os nomes de parâmetro de exemplo por seus próprios valores.

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Uma extensão também pode ser removida usando Olá portal do Azure. toodo para:

1. Selecione uma máquina virtual.
2. Selecione **Extensões**.
3. Escolha a extensão de saudação desejada.
4. Selecione **Desinstalar**.

## <a name="common-vm-extensions-reference"></a>Referência a extensões de VM comuns
| Nome da extensão | Descrição | Mais informações |
| --- | --- | --- |
| Extensão de script personalizado para o Windows |Executar scripts em uma máquina virtual do Azure |[Extensão de script personalizado para o Windows](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Extensão de DSC para o Windows |Extensão PowerShell DSC (Configuração de Estado Desejado) |[Extensão DSC para Windows](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Extensão de Diagnóstico do Azure |Gerenciar Diagnóstico do Azure |[Extensão de Diagnóstico do Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Extensão de acesso à VM do Azure |Gerenciar usuários e credenciais |[Extensão de Acesso à VM para Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
