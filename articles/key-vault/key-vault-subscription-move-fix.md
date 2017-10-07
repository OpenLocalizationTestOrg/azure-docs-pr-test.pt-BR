---
title: "aaaChange o ID de locatário Olá cofre da chave depois de mover uma assinatura | Microsoft Docs"
description: "Saiba como ID de locatário Olá tooswitch para um cofre da chave depois que uma assinatura é movido locatário diferente tooa"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="4849d-103">Alterar a ID de locatário do cofre de chaves depois de mover uma assinatura</span><span class="sxs-lookup"><span data-stu-id="4849d-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="4849d-104">P: minha assinatura foi movida de locatário A tootenant B. Como alterar a ID de locatário Olá para o Cofre de chaves existente e definir as ACLs corretas para entidades no locatário B?</span><span class="sxs-lookup"><span data-stu-id="4849d-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="4849d-105">Quando você cria um novo cofre de chave em uma assinatura, é associado automaticamente toohello ID de locatário de Active Directory do Azure padrão para essa assinatura.</span><span class="sxs-lookup"><span data-stu-id="4849d-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="4849d-106">Todas as entradas de política de acesso também são toothis empatados ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="4849d-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="4849d-107">Quando você mover sua assinatura do Azure de locatário um tootenant B, a chave existente cofres não podem ser acessados por Olá entidades (usuários e aplicativos) toofix locatário B. esse problema, você precisa:</span><span class="sxs-lookup"><span data-stu-id="4849d-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="4849d-108">Alterar a ID de locatário Olá associado a todos os cofres de chave existentes no tootenant assinatura B.</span><span class="sxs-lookup"><span data-stu-id="4849d-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="4849d-109">Remover todas as entradas de política de acesso existentes.</span><span class="sxs-lookup"><span data-stu-id="4849d-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="4849d-110">Adicionar novas entradas de política de acesso que estão associadas ao locatário B.</span><span class="sxs-lookup"><span data-stu-id="4849d-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="4849d-111">Por exemplo, se você tiver o Cofre de chaves 'myvault' em uma assinatura que foi movida de locatário A tootenant B, aqui como toochange hello ID do locatário para este cofre de chaves e remover as políticas de acesso antigo.</span><span class="sxs-lookup"><span data-stu-id="4849d-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="4849d-112">Como este cofre no locatário A antes de mover hello, Olá valor original de **$vault. Properties.TenantId** é um locatário, enquanto **(Get-AzureRmContext). Tenant.TenantId** é locatário B.</span><span class="sxs-lookup"><span data-stu-id="4849d-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="4849d-113">Agora que o cofre é associado com a ID de locatário correto do hello e entradas de política de acesso antigas são removidas, definir o acesso de novas entradas de diretiva com [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="4849d-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4849d-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4849d-114">Next steps</span></span>
<span data-ttu-id="4849d-115">Se você tiver dúvidas sobre o Cofre de chaves do Azure, visite Olá [fóruns do Azure Key Vault](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="4849d-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

