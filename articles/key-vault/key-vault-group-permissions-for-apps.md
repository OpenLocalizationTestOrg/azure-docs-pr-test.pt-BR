---
title: "Conceder permissão para vários aplicativos acessarem um Azure Key Vault | Microsoft Docs"
description: "Saiba como conceder permissão para vários aplicativos acessarem um Key Vault"
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
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="d45a0-103">Conceder permissão para vários aplicativos acessarem um Key Vault</span><span class="sxs-lookup"><span data-stu-id="d45a0-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="d45a0-104">P: Eu tenho vários aplicativos (mais de 16) que precisam acessar um Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d45a0-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="d45a0-105">Como o Key Vault permite apenas 16 entradas de controle de acesso, como posso fazer isso?</span><span class="sxs-lookup"><span data-stu-id="d45a0-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="d45a0-106">A política de controle de acesso do Key Vault dá suporte apenas a 16 entradas.</span><span class="sxs-lookup"><span data-stu-id="d45a0-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="d45a0-107">No entanto, você pode criar um grupo de segurança do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d45a0-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="d45a0-108">Adicione todas as entidades de serviço associadas a esse grupo de segurança e, em seguida, conceda acesso a esse grupo de segurança para o Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d45a0-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="d45a0-109">Veja os pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="d45a0-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="d45a0-110">[Instalar o módulo do PowerShell do Azure Active Directory V2](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="d45a0-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="d45a0-111">[Instalar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d45a0-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d45a0-112">Para executar os comandos a seguir, você precisa ter permissões para criar/editar grupos no locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d45a0-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="d45a0-113">Se não tiver permissões, você poderá precisar entrar em contato com o administrador do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d45a0-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="d45a0-114">Agora, execute os seguintes comandos no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d45a0-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="d45a0-115">Se você precisar conceder um conjunto diferente de permissões para um grupo de aplicativos, crie um grupo de segurança do Azure Active Directory separado para tais aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d45a0-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d45a0-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d45a0-116">Next steps</span></span>

<span data-ttu-id="d45a0-117">Saiba mais sobre como [Proteger seu Key Vault](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d45a0-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
