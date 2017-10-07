---
title: "vida útil do token de saudação de toochange do aaaHow padrões para um aplicativo personalizado | Microsoft Docs"
description: "Como as políticas de vida útil do Token tooupdate para seu aplicativo que você está desenvolvendo no AD do Azure"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a>Como a vida útil do token Olá toochange padrões para um aplicativo personalizado

O Azure AD Premium permite que os desenvolvedores de aplicativos e tempo de vida do locatário administradores tooconfigure Olá de tokens emitidos para clientes não-confidencial. Vida útil do token políticas é definidas em uma base de todo o locatário ou recursos de saudação que está sendo acessados.

 * tooset uma política de vida útil do token, você precisa Olá toodownload [módulo PowerShell do AD do Azure](https://www.powershellgallery.com/packages/AzureADPreview).

 * Executar Olá **AzureAD Connect-confirmar** comando.

 * Aqui está um exemplo de política que define o token de atualização de fator único Olá idade máxima. Crie política hello:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Saudação de check-out [vida útil do token configurando](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) documento toolearn como toocreate outros personalizado.

## <a name="next-steps"></a>Próximas etapas
[Configurando o tempo de vida do token](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Referência de token do Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

