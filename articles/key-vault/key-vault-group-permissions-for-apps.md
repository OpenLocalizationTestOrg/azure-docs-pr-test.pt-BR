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
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a>Conceder permissão toomany aplicativos tooaccess um cofre de chaves

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a>P: posso ter vários aplicativos (mais de 16) que precisam tooaccess um cofre de chaves. Como o Key Vault permite apenas 16 entradas de controle de acesso, como posso fazer isso?

A política de controle de acesso do Key Vault dá suporte apenas a 16 entradas. No entanto, você pode criar um grupo de segurança do Azure Active Directory. Adicione todos os hello associado do grupo de segurança de toothis de entidades de serviço e, em seguida, concede acesso toothis segurança grupo tooKey cofre.

Aqui estão os pré-requisitos de saudação:
* [Instalar o módulo do PowerShell do Azure Active Directory V2](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).
* [Instale o Azure PowerShell](/powershell/azure/overview).
* a seguir Olá toorun comandos, você precisar de permissões toocreate/editar grupos no locatário do Active Directory do Azure hello. Se você não tiver permissões, talvez seja necessário toocontact o administrador do Active Directory do Azure.

Agora execute Olá comandos do PowerShell a seguir.

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

Se você precisar toogrant um conjunto diferente de grupo de tooa de permissões de aplicativos, crie um grupo de segurança do Active Directory do Azure separado para esses aplicativos.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como muito[proteger seu Cofre de chaves](key-vault-secure-your-key-vault.md).
