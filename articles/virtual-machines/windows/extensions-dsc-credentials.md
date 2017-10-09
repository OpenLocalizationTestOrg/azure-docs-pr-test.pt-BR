---
title: aaaPassing credenciais tooAzure usando a DSC | Microsoft Docs
description: "Visão geral sobre como passar com segurança as credenciais de máquinas virtuais de tooAzure usando a configuração de estado desejado do PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>Passando o manipulador de extensão de DSC do Azure credenciais toohello
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Este artigo aborda a extensão de configuração de estado desejado de saudação do Azure. Uma visão geral do manipulador de extensão Olá DSC pode ser encontrada em [manipulador de extensão de configuração de estado desejado do Azure Introdução toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="passing-in-credentials"></a>Passagem de credenciais
Como parte do processo de configuração de saudação, talvez seja necessário tooset as contas de usuário, acessar os serviços ou instalar um programa em um contexto de usuário. toodo essas coisas, você precisa ter credenciais de tooprovide. 

DSC permite configurações com parâmetros de credenciais são passadas para a configuração de saudação e armazenadas com segurança em arquivos MOF. Olá manipulador de extensão do Azure simplifica o gerenciamento de credenciais, fornecendo um gerenciamento automático de certificados. 

Considere Olá script de configuração de DSC que cria uma conta de usuário local com a senha especificada Olá a seguir:

*user_configuration.ps1*

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

É importante tooinclude *nó localhost* como parte da configuração de saudação. Se essa instrução estiver ausente, hello etapas a seguir não funcionam como manipulador de extensão Olá especificamente procura instrução do hello nó localhost. Também é importante de conversão de tipo hello tooinclude *[PsCredential]*, como a credencial de Olá Olá extensão tooencrypt dispara a esse tipo específico. 

Publica este armazenamento tooblob de script:

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Definir a extensão de DSC do Azure hello e forneça a credencial de saudação:

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>Como as credenciais são protegidas
Executar esse código solicita uma credencial. Assim que ela for fornecida, ela será armazenada na memória por pouco tempo. Quando ele é publicado com `Set-AzureVmDscExtension` cmdlet, ele são transmitidos por HTTPS toohello VM, em que o Azure armazena criptografado no disco, usando certificados de máquina virtual local hello. É brevemente descriptografada na memória e criptografada novamente toopass-tooDSC.

Esse comportamento é diferente de [usando as configurações de seguras sem o manipulador de extensão de saudação](https://msdn.microsoft.com/powershell/dsc/securemof). Olá ambiente do Azure fornece dados de configuração de tootransmit uma maneira com segurança por meio de certificados. Ao usar o manipulador de extensão Olá DSC, não há nenhum tooprovide necessidade $CertificatePath ou um $CertificateID / entrada $Thumbprint ConfigurationData.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o manipulador de extensão de DSC do Azure hello, consulte [manipulador de extensão de configuração de estado desejado do Azure Introdução toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Examine Olá [modelo do Azure Resource Manager para extensão Olá DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para obter mais informações sobre o PowerShell DSC, [visite o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview). 

toofind funcionalidade adicional que você pode gerenciar com o PowerShell DSC, [procurar a Galeria do PowerShell Olá](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) para obter mais recursos de DSC.

