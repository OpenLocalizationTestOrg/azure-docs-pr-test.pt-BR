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
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="4df19-103">Como a vida útil do token Olá toochange padrões para um aplicativo personalizado</span><span class="sxs-lookup"><span data-stu-id="4df19-103">How toochange hello token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="4df19-104">O Azure AD Premium permite que os desenvolvedores de aplicativos e tempo de vida do locatário administradores tooconfigure Olá de tokens emitidos para clientes não-confidencial.</span><span class="sxs-lookup"><span data-stu-id="4df19-104">Azure AD Premium allows app developers and tenant admins tooconfigure hello lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="4df19-105">Vida útil do token políticas é definidas em uma base de todo o locatário ou recursos de saudação que está sendo acessados.</span><span class="sxs-lookup"><span data-stu-id="4df19-105">Token lifetime policies are set on a tenant-wide basis or hello resources being accessed.</span></span>

 * <span data-ttu-id="4df19-106">tooset uma política de vida útil do token, você precisa Olá toodownload [módulo PowerShell do AD do Azure](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="4df19-106">tooset a token lifetime policy, you need toodownload hello [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="4df19-107">Executar Olá **AzureAD Connect-confirmar** comando.</span><span class="sxs-lookup"><span data-stu-id="4df19-107">Run hello **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="4df19-108">Aqui está um exemplo de política que define o token de atualização de fator único Olá idade máxima.</span><span class="sxs-lookup"><span data-stu-id="4df19-108">Here’s an example policy that sets hello max age single factor refresh token.</span></span> <span data-ttu-id="4df19-109">Crie política hello:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="4df19-109">Create hello policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="4df19-110">Saudação de check-out [vida útil do token configurando](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) documento toolearn como toocreate outros personalizado.</span><span class="sxs-lookup"><span data-stu-id="4df19-110">Checkout hello [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document toolearn how toocreate other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4df19-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4df19-111">Next steps</span></span>
[<span data-ttu-id="4df19-112">Configurando o tempo de vida do token</span><span class="sxs-lookup"><span data-stu-id="4df19-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="4df19-113">Referência de token do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4df19-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

