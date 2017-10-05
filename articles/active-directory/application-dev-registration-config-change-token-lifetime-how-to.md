---
title: "Como alterar os padrões de tempo de vida do token para um aplicativo personalizado | Microsoft Docs"
description: "Como atualizar as políticas de tempo de vida do token para o aplicativo que você está desenvolvendo no Azure AD"
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
ms.openlocfilehash: a28eacd820ed28a6470992ce86b060e886c00bcb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="9fe85-103">Como alterar os padrões de tempo de vida do token para um aplicativo personalizado</span><span class="sxs-lookup"><span data-stu-id="9fe85-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="9fe85-104">O Azure AD Premium permite que desenvolvedores de aplicativos e administradores de locatários configurem o tempo de vida de tokens emitidos para clientes não confidenciais.</span><span class="sxs-lookup"><span data-stu-id="9fe85-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="9fe85-105">As políticas de tempo de vida do token são definidas com base em todos os locatários ou nos recursos que estão sendo acessados.</span><span class="sxs-lookup"><span data-stu-id="9fe85-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="9fe85-106">Para definir uma política de tempo de vida do token, você precisa baixar o [Módulo PowerShell do Azure AD](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="9fe85-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="9fe85-107">Execute o comando **Connect-AzureAD -Confirm**.</span><span class="sxs-lookup"><span data-stu-id="9fe85-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="9fe85-108">Veja um exemplo de política que define o token de atualização de fator único de idade máxima.</span><span class="sxs-lookup"><span data-stu-id="9fe85-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="9fe85-109">Crie a política: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="9fe85-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="9fe85-110">Veja o documento [Configurando tempo de vida do token](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) para saber como criar outro personalizado.</span><span class="sxs-lookup"><span data-stu-id="9fe85-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fe85-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9fe85-111">Next steps</span></span>
[<span data-ttu-id="9fe85-112">Configurando o tempo de vida do token</span><span class="sxs-lookup"><span data-stu-id="9fe85-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="9fe85-113">Referência de token do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fe85-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

