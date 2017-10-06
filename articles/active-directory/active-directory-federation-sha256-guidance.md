---
title: "algoritmo de hash de assinatura aaaChange da terceira parte confiável do Office 365 | Microsoft Docs"
description: "Esta página fornece diretrizes para alterar o algoritmo SHA para confiança de federação com o Office 365"
keywords: "SHA1, SHA256, O365, federação, aadconnect, adfs, ad fs, alterar o sha, confiança de federação, objeto de confiança de terceira parte confiável"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="f6e06-104">Alterar o algoritmo de hash de assinatura para o objeto de confiança de terceira parte confiável Office 365</span><span class="sxs-lookup"><span data-stu-id="f6e06-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="f6e06-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f6e06-105">Overview</span></span>
<span data-ttu-id="f6e06-106">Os serviços de Federação do Active Directory (AD FS) assina seu tooensure Active Directory do Azure tooMicrosoft de tokens que não pode ser violados.</span><span class="sxs-lookup"><span data-stu-id="f6e06-106">Active Directory Federation Services (AD FS) signs its tokens tooMicrosoft Azure Active Directory tooensure that they cannot be tampered with.</span></span> <span data-ttu-id="f6e06-107">Essa assinatura pode ser baseada em SHA1 ou em SHA256.</span><span class="sxs-lookup"><span data-stu-id="f6e06-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="f6e06-108">Active Directory do Azure agora oferece suporte a tokens assinados com um algoritmo SHA256 e é recomendável definir tooSHA256 de algoritmo de assinatura de token Olá para o nível mais alto de saudação de segurança.</span><span class="sxs-lookup"><span data-stu-id="f6e06-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting hello token-signing algorithm tooSHA256 for hello highest level of security.</span></span> <span data-ttu-id="f6e06-109">Este artigo descreve etapas Olá necessário toohello de algoritmo de assinatura de token do tooset hello mais seguras nível SHA256.</span><span class="sxs-lookup"><span data-stu-id="f6e06-109">This article describes hello steps needed tooset hello token-signing algorithm toohello more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="f6e06-110">A Microsoft recomenda o uso de SHA256 como algoritmo de saudação para assinar tokens como SHA1 ainda é uma opção com suporte, mas é mais seguro do que SHA1.</span><span class="sxs-lookup"><span data-stu-id="f6e06-110">Microsoft recommends usage of SHA256 as hello algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-hello-token-signing-algorithm"></a><span data-ttu-id="f6e06-111">Alterar o algoritmo de assinatura de token Olá</span><span class="sxs-lookup"><span data-stu-id="f6e06-111">Change hello token-signing algorithm</span></span>
<span data-ttu-id="f6e06-112">Depois que você configurou o algoritmo de assinatura de saudação com uma saudação dois processos abaixo, o AD FS assina os tokens de saudação para o Office 365 terceira parte confiável com SHA256.</span><span class="sxs-lookup"><span data-stu-id="f6e06-112">After you have set hello signature algorithm with one of hello two processes below, AD FS signs hello tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="f6e06-113">Você não precisa toomake as alterações de configuração adicional, e essa alteração não tem nenhum impacto em sua capacidade tooaccess Office 365 ou outros aplicativos do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e06-113">You don't need toomake any extra configuration changes, and this change has no impact on your ability tooaccess Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="f6e06-114">Console de gerenciamento do AD FS</span><span class="sxs-lookup"><span data-stu-id="f6e06-114">AD FS management console</span></span>
1. <span data-ttu-id="f6e06-115">Abra o console de gerenciamento do hello AD FS no servidor do hello primário AD FS.</span><span class="sxs-lookup"><span data-stu-id="f6e06-115">Open hello AD FS management console on hello primary AD FS server.</span></span>
2. <span data-ttu-id="f6e06-116">Expanda o nó do hello AD FS e clique em **terceira parte confiável**.</span><span class="sxs-lookup"><span data-stu-id="f6e06-116">Expand hello AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="f6e06-117">Clique com o botão direito do mouse no Office 365/objeto de confiança de terceira parte confiável e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f6e06-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="f6e06-118">Selecione Olá **avançado** guia e o algoritmo de hash seguro Olá selecione SHA256.</span><span class="sxs-lookup"><span data-stu-id="f6e06-118">Select hello **Advanced** tab and select hello secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="f6e06-119">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6e06-119">Click **OK**.</span></span>

![Algoritmo de assinatura SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="f6e06-121">Cmdlets do PowerShell do AD FS</span><span class="sxs-lookup"><span data-stu-id="f6e06-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="f6e06-122">Em qualquer servidor do AD FS, abra o PowerShell com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="f6e06-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="f6e06-123">Algoritmo de hash seguro conjunto hello usando Olá **Set-AdfsRelyingPartyTrust** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f6e06-123">Set hello secure hash algorithm by using hello **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="f6e06-124">Leia também</span><span class="sxs-lookup"><span data-stu-id="f6e06-124">Also read</span></span>
* [<span data-ttu-id="f6e06-125">Reparar a confiança do Office 365 com o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f6e06-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

