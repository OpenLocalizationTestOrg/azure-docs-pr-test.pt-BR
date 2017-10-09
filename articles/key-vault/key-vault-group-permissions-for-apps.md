---
title: "aaaGrant permissão toomany aplicativos tooaccess um cofre de chaves do Azure | Microsoft Docs"
description: "Saiba como toogrant permissão toomany aplicativos tooaccess uma chave de cofre"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="9176a-103">Conceder permissão toomany aplicativos tooaccess um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="9176a-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="9176a-104">P: posso ter vários aplicativos (mais de 16) que precisam tooaccess um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="9176a-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="9176a-105">Como o Key Vault permite apenas 16 entradas de controle de acesso, como posso fazer isso?</span><span class="sxs-lookup"><span data-stu-id="9176a-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="9176a-106">A política de controle de acesso do Key Vault dá suporte apenas a 16 entradas.</span><span class="sxs-lookup"><span data-stu-id="9176a-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="9176a-107">No entanto, você pode criar um grupo de segurança do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9176a-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="9176a-108">Adicione todos os hello associado do grupo de segurança de toothis de entidades de serviço e, em seguida, concede acesso toothis segurança grupo tooKey cofre.</span><span class="sxs-lookup"><span data-stu-id="9176a-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="9176a-109">Aqui estão os pré-requisitos de saudação:</span><span class="sxs-lookup"><span data-stu-id="9176a-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="9176a-110">[Instalar o módulo do PowerShell do Azure Active Directory V2](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="9176a-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="9176a-111">[Instale o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9176a-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="9176a-112">a seguir Olá toorun comandos, você precisar de permissões toocreate/editar grupos no locatário do Active Directory do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9176a-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="9176a-113">Se você não tiver permissões, talvez seja necessário toocontact o administrador do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="9176a-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="9176a-114">Agora execute Olá comandos do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="9176a-114">Now run hello following commands in PowerShell.</span></span>

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

<span data-ttu-id="9176a-115">Se você precisar toogrant um conjunto diferente de grupo de tooa de permissões de aplicativos, crie um grupo de segurança do Active Directory do Azure separado para esses aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9176a-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9176a-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9176a-116">Next steps</span></span>

<span data-ttu-id="9176a-117">Saiba mais sobre como muito[proteger seu Cofre de chaves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="9176a-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
