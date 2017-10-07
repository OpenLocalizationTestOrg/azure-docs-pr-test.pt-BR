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
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>Alterar a ID de locatário do cofre de chaves depois de mover uma assinatura
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>P: minha assinatura foi movida de locatário A tootenant B. Como alterar a ID de locatário Olá para o Cofre de chaves existente e definir as ACLs corretas para entidades no locatário B?
Quando você cria um novo cofre de chave em uma assinatura, é associado automaticamente toohello ID de locatário de Active Directory do Azure padrão para essa assinatura. Todas as entradas de política de acesso também são toothis empatados ID de locatário. Quando você mover sua assinatura do Azure de locatário um tootenant B, a chave existente cofres não podem ser acessados por Olá entidades (usuários e aplicativos) toofix locatário B. esse problema, você precisa:

* Alterar a ID de locatário Olá associado a todos os cofres de chave existentes no tootenant assinatura B.
* Remover todas as entradas de política de acesso existentes.
* Adicionar novas entradas de política de acesso que estão associadas ao locatário B.

Por exemplo, se você tiver o Cofre de chaves 'myvault' em uma assinatura que foi movida de locatário A tootenant B, aqui como toochange hello ID do locatário para este cofre de chaves e remover as políticas de acesso antigo.

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

Como este cofre no locatário A antes de mover hello, Olá valor original de **$vault. Properties.TenantId** é um locatário, enquanto **(Get-AzureRmContext). Tenant.TenantId** é locatário B.

Agora que o cofre é associado com a ID de locatário correto do hello e entradas de política de acesso antigas são removidas, definir o acesso de novas entradas de diretiva com [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).

## <a name="next-steps"></a>Próximas etapas
Se você tiver dúvidas sobre o Cofre de chaves do Azure, visite Olá [fóruns do Azure Key Vault](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

