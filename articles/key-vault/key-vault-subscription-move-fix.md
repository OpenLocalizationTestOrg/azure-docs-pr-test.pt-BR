---
title: "Alterar a ID de locatário do cofre de chaves de depois de mover uma assinatura | Microsoft Docs"
description: "Saiba como mudar a ID de locatário para um cofre de chaves depois que uma assinatura é movida para um locatário diferente"
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
ms.openlocfilehash: 2f007dd4f877b48003cddcefa5f4321049853361
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="9d81b-103">Alterar a ID de locatário do cofre de chaves depois de mover uma assinatura</span><span class="sxs-lookup"><span data-stu-id="9d81b-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-to-tenant-b-how-do-i-change-the-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="9d81b-104">P: minha assinatura foi movida do locatário A para o locatário B. Como posso alterar a ID do locatário para o cofre de chaves existente e definir ACLs corretas para as entidades no locatário B?</span><span class="sxs-lookup"><span data-stu-id="9d81b-104">Q: My subscription was moved from tenant A to tenant B. How do I change the tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="9d81b-105">Quando você cria um novo cofre de chaves em uma assinatura, ele é vinculado automaticamente à ID de locatário do Azure Active Directory padrão para essa assinatura.</span><span class="sxs-lookup"><span data-stu-id="9d81b-105">When you create a new key vault in a subscription, it is automatically tied to the default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="9d81b-106">Todas as entradas de política de acesso também são vinculadas a essa ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="9d81b-106">All access policy entries are also tied to this tenant ID.</span></span> <span data-ttu-id="9d81b-107">Quando você move a assinatura do Azure do locatário A para o locatário B, os cofres de chaves existentes ficam inacessíveis para as entidades (usuários e aplicativos) no locatário B. Para corrigir esse problema, você precisa:</span><span class="sxs-lookup"><span data-stu-id="9d81b-107">When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. To fix this issue, you need to:</span></span>

* <span data-ttu-id="9d81b-108">Alterar a ID do locatário associada a todos os cofres de chaves existentes nessa assinatura para o locatário B.</span><span class="sxs-lookup"><span data-stu-id="9d81b-108">Change the tenant ID associated with all existing key vaults in this subscription to tenant B.</span></span>
* <span data-ttu-id="9d81b-109">Remover todas as entradas de política de acesso existentes.</span><span class="sxs-lookup"><span data-stu-id="9d81b-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="9d81b-110">Adicionar novas entradas de política de acesso que estão associadas ao locatário B.</span><span class="sxs-lookup"><span data-stu-id="9d81b-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="9d81b-111">Por exemplo, se você tiver o cofre de chaves 'myvault' em uma assinatura que foi movida do locatário A para o B, veja como mudar a ID de locatário para o cofre de chaves e remover as antigas políticas de acesso.</span><span class="sxs-lookup"><span data-stu-id="9d81b-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A to tenant B, here's how to change the tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="9d81b-112">Já que o cofre estava no locatário A antes da mudança, o valor original de **$vault. Properties.TenantId** é locatário A e **(Get-AzureRmContext).Tenant.TenantId** é locatário B.</span><span class="sxs-lookup"><span data-stu-id="9d81b-112">Because this vault was in tenant A before the move, the original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="9d81b-113">Agora que o cofre está associado à ID de locatário correta e as entradas de política de acesso antigas foram removidas, defina novas entradas de política de acesso com [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d81b-113">Now that your vault is associated with the correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d81b-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d81b-114">Next steps</span></span>
<span data-ttu-id="9d81b-115">Se você tiver dúvidas sobre o Cofre de Chaves do Azure, visite os [Fóruns do Cofre de Chaves do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="9d81b-115">If you have questions about Azure Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

