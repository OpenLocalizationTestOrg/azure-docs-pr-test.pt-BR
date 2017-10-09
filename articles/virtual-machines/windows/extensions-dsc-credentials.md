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
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a><span data-ttu-id="cefee-103">Passando o manipulador de extensão de DSC do Azure credenciais toohello</span><span class="sxs-lookup"><span data-stu-id="cefee-103">Passing credentials toohello Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="cefee-104">Este artigo aborda a extensão de configuração de estado desejado de saudação do Azure.</span><span class="sxs-lookup"><span data-stu-id="cefee-104">This article covers hello Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="cefee-105">Uma visão geral do manipulador de extensão Olá DSC pode ser encontrada em [manipulador de extensão de configuração de estado desejado do Azure Introdução toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cefee-105">An overview of hello DSC extension handler can be found at [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="cefee-106">Passagem de credenciais</span><span class="sxs-lookup"><span data-stu-id="cefee-106">Passing in credentials</span></span>
<span data-ttu-id="cefee-107">Como parte do processo de configuração de saudação, talvez seja necessário tooset as contas de usuário, acessar os serviços ou instalar um programa em um contexto de usuário.</span><span class="sxs-lookup"><span data-stu-id="cefee-107">As a part of hello configuration process, you may need tooset up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="cefee-108">toodo essas coisas, você precisa ter credenciais de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="cefee-108">toodo these things, you need tooprovide credentials.</span></span> 

<span data-ttu-id="cefee-109">DSC permite configurações com parâmetros de credenciais são passadas para a configuração de saudação e armazenadas com segurança em arquivos MOF.</span><span class="sxs-lookup"><span data-stu-id="cefee-109">DSC allows for parameterized configurations in which credentials are passed into hello configuration and securely stored in MOF files.</span></span> <span data-ttu-id="cefee-110">Olá manipulador de extensão do Azure simplifica o gerenciamento de credenciais, fornecendo um gerenciamento automático de certificados.</span><span class="sxs-lookup"><span data-stu-id="cefee-110">hello Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="cefee-111">Considere Olá script de configuração de DSC que cria uma conta de usuário local com a senha especificada Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cefee-111">Consider hello following DSC configuration script that creates a local user account with hello specified password:</span></span>

<span data-ttu-id="cefee-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="cefee-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="cefee-113">É importante tooinclude *nó localhost* como parte da configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cefee-113">It is important tooinclude *node localhost* as part of hello configuration.</span></span> <span data-ttu-id="cefee-114">Se essa instrução estiver ausente, hello etapas a seguir não funcionam como manipulador de extensão Olá especificamente procura instrução do hello nó localhost.</span><span class="sxs-lookup"><span data-stu-id="cefee-114">If this statement is missing, hello following steps do not work as hello extension handler specifically looks for hello node localhost statement.</span></span> <span data-ttu-id="cefee-115">Também é importante de conversão de tipo hello tooinclude *[PsCredential]*, como a credencial de Olá Olá extensão tooencrypt dispara a esse tipo específico.</span><span class="sxs-lookup"><span data-stu-id="cefee-115">It is also important tooinclude hello typecast *[PsCredential]*, as this specific type triggers hello extension tooencrypt hello credential.</span></span> 

<span data-ttu-id="cefee-116">Publica este armazenamento tooblob de script:</span><span class="sxs-lookup"><span data-stu-id="cefee-116">Publish this script tooblob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="cefee-117">Definir a extensão de DSC do Azure hello e forneça a credencial de saudação:</span><span class="sxs-lookup"><span data-stu-id="cefee-117">Set hello Azure DSC extension and provide hello credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="cefee-118">Como as credenciais são protegidas</span><span class="sxs-lookup"><span data-stu-id="cefee-118">How credentials are secured</span></span>
<span data-ttu-id="cefee-119">Executar esse código solicita uma credencial.</span><span class="sxs-lookup"><span data-stu-id="cefee-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="cefee-120">Assim que ela for fornecida, ela será armazenada na memória por pouco tempo.</span><span class="sxs-lookup"><span data-stu-id="cefee-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="cefee-121">Quando ele é publicado com `Set-AzureVmDscExtension` cmdlet, ele são transmitidos por HTTPS toohello VM, em que o Azure armazena criptografado no disco, usando certificados de máquina virtual local hello.</span><span class="sxs-lookup"><span data-stu-id="cefee-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS toohello VM, where Azure stores it encrypted on disk, using hello local VM certificate.</span></span> <span data-ttu-id="cefee-122">É brevemente descriptografada na memória e criptografada novamente toopass-tooDSC.</span><span class="sxs-lookup"><span data-stu-id="cefee-122">Then it is briefly decrypted in memory and re-encrypted toopass it tooDSC.</span></span>

<span data-ttu-id="cefee-123">Esse comportamento é diferente de [usando as configurações de seguras sem o manipulador de extensão de saudação](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="cefee-123">This behavior is different than [using secure configurations without hello extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="cefee-124">Olá ambiente do Azure fornece dados de configuração de tootransmit uma maneira com segurança por meio de certificados.</span><span class="sxs-lookup"><span data-stu-id="cefee-124">hello Azure environment gives a way tootransmit configuration data securely via certificates.</span></span> <span data-ttu-id="cefee-125">Ao usar o manipulador de extensão Olá DSC, não há nenhum tooprovide necessidade $CertificatePath ou um $CertificateID / entrada $Thumbprint ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="cefee-125">When using hello DSC extension handler, there is no need tooprovide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cefee-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cefee-126">Next steps</span></span>
<span data-ttu-id="cefee-127">Para obter mais informações sobre o manipulador de extensão de DSC do Azure hello, consulte [manipulador de extensão de configuração de estado desejado do Azure Introdução toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cefee-127">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="cefee-128">Examine Olá [modelo do Azure Resource Manager para extensão Olá DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cefee-128">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="cefee-129">Para obter mais informações sobre o PowerShell DSC, [visite o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="cefee-129">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="cefee-130">toofind funcionalidade adicional que você pode gerenciar com o PowerShell DSC, [procurar a Galeria do PowerShell Olá](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) para obter mais recursos de DSC.</span><span class="sxs-lookup"><span data-stu-id="cefee-130">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

