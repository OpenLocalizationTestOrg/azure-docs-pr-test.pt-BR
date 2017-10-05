---
title: "Compartilhamento externo do Office 365 e colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "referência ao mapeamento de declarações para colaboração B2B do Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="4f9db-103">Compartilhamento externo do Office 365 e colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f9db-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="4f9db-104">O compartilhamento externo no Office 365 (OneDrive, SharePoint Online, Unified Groups etc.) e a colaboração B2B do Azure AD (Azure Active Directory) são tecnicamente a mesma coisa.</span><span class="sxs-lookup"><span data-stu-id="4f9db-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="4f9db-105">Todo compartilhamento externo, (com exceção do OneDrive/SharePoint Online), incluindo convidados em Grupos do Office 365, já usa as APIs de convite de colaboração B2B do Azure AD para compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="4f9db-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="4f9db-106">O OneDrive/SharePoint Online tem um gerenciador de convite separado.</span><span class="sxs-lookup"><span data-stu-id="4f9db-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="4f9db-107">Suporte para compartilhamento externo no OneDrive/SharePoint Online iniciado antes de o Azure AD ter desenvolvido o suporte.</span><span class="sxs-lookup"><span data-stu-id="4f9db-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="4f9db-108">Ao longo do tempo, o compartilhamento externo do OneDrive/SharePoint Online acumulou vários recursos e muitos milhões de usuários que usam o padrão de compartilhamento interno do produto.</span><span class="sxs-lookup"><span data-stu-id="4f9db-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="4f9db-109">No entanto, há algumas diferenças sutis entre o funcionamento do compartilhamento externo do OneDrive/SharePoint Online e a colaboração do Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="4f9db-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="4f9db-110">O OneDrive/SharePoint Online adiciona usuários ao diretório depois que os usuários tiverem resgatado seus convites.</span><span class="sxs-lookup"><span data-stu-id="4f9db-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="4f9db-111">Portanto, antes de resgate, você não vê o usuário no Portal do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f9db-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="4f9db-112">Se outro site convidar um usuário durante esse período, um novo convite será gerado.</span><span class="sxs-lookup"><span data-stu-id="4f9db-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="4f9db-113">No entanto, quando você usa a colaboração B2B do Azure AD, os usuários são adicionados imediatamente no convite para que eles apareçam em todos os lugares.</span><span class="sxs-lookup"><span data-stu-id="4f9db-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="4f9db-114">A experiência de resgate no OneDrive/SharePoint Online tem uma aparência diferente da experiência na colaboração B2B do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f9db-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="4f9db-115">Depois que um usuário resgata um convite, as experiências são parecidas.</span><span class="sxs-lookup"><span data-stu-id="4f9db-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="4f9db-116">A colaboração B2B do Azure AD convidou usuários que possam ser escolhidos das caixas de diálogo de compartilhamento do OneDrive/SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="4f9db-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="4f9db-117">Os usuários convidados do OneDrive/SharePoint Online também aparecem no Azure AD após o resgate do convite.</span><span class="sxs-lookup"><span data-stu-id="4f9db-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="4f9db-118">Para gerenciar o compartilhamento externo no OneDrive/SharePoint Online junto com a colaboração B2B do Azure AD, defina a configuração do compartilhamento externo do OneDrive/SharePoint Online como **Permitir apenas o compartilhamento com usuários externos que já estão no diretório**.</span><span class="sxs-lookup"><span data-stu-id="4f9db-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="4f9db-119">Os usuários podem acessar sites compartilhados externamente e escolher colaboradores externos adicionados pelo administrador.</span><span class="sxs-lookup"><span data-stu-id="4f9db-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="4f9db-120">O administrador pode adicionar os colaboradores externos por meio de APIs de convite de colaboração B2B.</span><span class="sxs-lookup"><span data-stu-id="4f9db-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![As configurações de compartilhamento externo do OneDrive/SharePoint Online](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="4f9db-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4f9db-122">Next steps</span></span>

<span data-ttu-id="4f9db-123">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="4f9db-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="4f9db-124">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="4f9db-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="4f9db-125">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4f9db-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="4f9db-126">Como adicionar um usuário de colaboração B2B a uma função</span><span class="sxs-lookup"><span data-stu-id="4f9db-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="4f9db-127">Delegação de convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4f9db-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="4f9db-128">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4f9db-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="4f9db-129">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f9db-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="4f9db-130">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4f9db-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="4f9db-131">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4f9db-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="4f9db-132">Mapeamento de declarações do usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4f9db-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="4f9db-133">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4f9db-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
