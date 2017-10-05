---
title: "Alterar o algoritmo de hash da assinatura para o objeto de confiança de terceira parte confiável do Office 365 | Microsoft Docs"
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
ms.openlocfilehash: c581b1468630a9f28204592c936360b72f42f0d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="580a0-104">Alterar o algoritmo de hash de assinatura para o objeto de confiança de terceira parte confiável Office 365</span><span class="sxs-lookup"><span data-stu-id="580a0-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="580a0-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="580a0-105">Overview</span></span>
<span data-ttu-id="580a0-106">O AD FS (Serviços de Federação do Azure Active Directory) assina seus tokens para o Microsoft Azure Active Directory para garantir que eles não possam ser violados.</span><span class="sxs-lookup"><span data-stu-id="580a0-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="580a0-107">Essa assinatura pode ser baseada em SHA1 ou em SHA256.</span><span class="sxs-lookup"><span data-stu-id="580a0-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="580a0-108">O Azure Active Directory agora dá suporte para tokens assinados com um algoritmo SHA256, e recomendamos configurar o algoritmo de assinatura do token para SHA256 no nível mais alto de segurança.</span><span class="sxs-lookup"><span data-stu-id="580a0-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="580a0-109">Este artigo descreve as etapas necessárias para definir o algoritmo de assinatura de token para o nível SHA256 mais seguro.</span><span class="sxs-lookup"><span data-stu-id="580a0-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="580a0-110">A Microsoft recomenda o uso do SHA256 como o algoritmo de assinatura de tokens, pois ele é mais seguro do que o SHA1; no entanto, o SHA1 ainda é uma opção com suporte.</span><span class="sxs-lookup"><span data-stu-id="580a0-110">Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="580a0-111">Alterar o algoritmo de assinatura de token</span><span class="sxs-lookup"><span data-stu-id="580a0-111">Change the token-signing algorithm</span></span>
<span data-ttu-id="580a0-112">Depois que você define o algoritmo de assinatura com um dos dois processos abaixo, o AD FS assina os tokens para o objeto de confiança de terceira parte confiável do Office 365 com SHA256.</span><span class="sxs-lookup"><span data-stu-id="580a0-112">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="580a0-113">Você não precisa fazer alterações de configuração adicionais, e essa alteração não tem nenhum impacto sobre a capacidade de acessar o Office 365 ou outros aplicativos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="580a0-113">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="580a0-114">Console de gerenciamento do AD FS</span><span class="sxs-lookup"><span data-stu-id="580a0-114">AD FS management console</span></span>
1. <span data-ttu-id="580a0-115">Abra o console de gerenciamento do AD FS no servidor primário do AD FS.</span><span class="sxs-lookup"><span data-stu-id="580a0-115">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="580a0-116">Expanda o nó do AD FS e clique em **Objetos de Confiança de Terceira Parte Confiável**.</span><span class="sxs-lookup"><span data-stu-id="580a0-116">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="580a0-117">Clique com o botão direito do mouse no Office 365/objeto de confiança de terceira parte confiável e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="580a0-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="580a0-118">Selecione a guia **Avançado** e o Secure Hash Algorithm SHA256.</span><span class="sxs-lookup"><span data-stu-id="580a0-118">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="580a0-119">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="580a0-119">Click **OK**.</span></span>

![Algoritmo de assinatura SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="580a0-121">Cmdlets do PowerShell do AD FS</span><span class="sxs-lookup"><span data-stu-id="580a0-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="580a0-122">Em qualquer servidor do AD FS, abra o PowerShell com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="580a0-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="580a0-123">Definir o algoritmo de hash seguro usando o cmdlet **Set-AdfsRelyingPartyTrust** .</span><span class="sxs-lookup"><span data-stu-id="580a0-123">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="580a0-124">Leia também</span><span class="sxs-lookup"><span data-stu-id="580a0-124">Also read</span></span>
* [<span data-ttu-id="580a0-125">Reparar a confiança do Office 365 com o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="580a0-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

