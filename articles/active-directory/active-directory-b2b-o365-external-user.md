---
title: "aaaOffice 365 compartilhamento externo e colaboração B2B do Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="4fcaa-103">Compartilhamento externo do Office 365 e colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fcaa-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="4fcaa-104">Externa de compartilhamento no Office 365 (OneDrive, o SharePoint Online, grupos unificados, etc.) e o Azure Active Directory (AD do Azure) B2B colaboração são tecnicamente Olá mesmo significado.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="4fcaa-105">Compartilhamento externo todos (exceto OneDrive/SharePoint Online), inclusive convidados em grupos do Office 365, já usa o convite de colaboração de saudação do Azure AD B2B APIs para o compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="4fcaa-106">O OneDrive/SharePoint Online tem um gerenciador de convite separado.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="4fcaa-107">Suporte para compartilhamento externo no OneDrive/SharePoint Online iniciado antes de o Azure AD ter desenvolvido o suporte.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="4fcaa-108">Ao longo do tempo, o compartilhamento externo OneDrive/SharePoint Online tem acumulada vários recursos e muitos milhões de usuários que usam o produto de saudação do interno padrão de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="4fcaa-109">No entanto, há algumas diferenças sutis entre o funcionamento do compartilhamento externo do OneDrive/SharePoint Online e a colaboração do Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="4fcaa-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="4fcaa-110">OneDrive/SharePoint Online adiciona diretório de toohello usuários depois que os usuários têm resgatado seus convites.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="4fcaa-111">Portanto, antes de resgate, você não vir o usuário Olá no portal do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="4fcaa-112">Se outro site convida um usuário no hello enquanto isso, é gerado um novo convite.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="4fcaa-113">No entanto, quando você usa a colaboração B2B do Azure AD, os usuários são adicionados imediatamente no convite para que eles apareçam em todos os lugares.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="4fcaa-114">Olá resgate experiência no OneDrive/SharePoint Online é diferente da saudação experiência em colaboração B2B do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="4fcaa-115">Depois que um usuário resgata um convite, Olá experiências parecem.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="4fcaa-116">A colaboração B2B do Azure AD convidou usuários que possam ser escolhidos das caixas de diálogo de compartilhamento do OneDrive/SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="4fcaa-117">Os usuários convidados do OneDrive/SharePoint Online também aparecem no Azure AD após o resgate do convite.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="4fcaa-118">toomanage externo de compartilhamento no OneDrive/SharePoint Online com colaboração B2B do Azure AD, definir Olá OneDrive/SharePoint Online externo de compartilhamento de configuração muito**apenas permitir compartilhamento com usuários externos já no diretório Olá**.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="4fcaa-119">Os usuários podem acessar sites tooexternally compartilhado e escolha de parceiros externos que Olá administrador tenha adicionado.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="4fcaa-120">Olá administrador pode adicionar parceiros externos de saudação por meio de saudação convite de colaboração B2B APIs.</span><span class="sxs-lookup"><span data-stu-id="4fcaa-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![Olá externo de configuração de compartilhamento OneDrive/SharePoint Online](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="4fcaa-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4fcaa-122">Next steps</span></span>

<span data-ttu-id="4fcaa-123">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="4fcaa-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="4fcaa-124">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="4fcaa-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="4fcaa-125">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4fcaa-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="4fcaa-126">Adicionando uma função de tooa de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4fcaa-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="4fcaa-127">Delegação de convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4fcaa-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="4fcaa-128">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4fcaa-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="4fcaa-129">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fcaa-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="4fcaa-130">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4fcaa-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="4fcaa-131">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4fcaa-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="4fcaa-132">Mapeamento de declarações do usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4fcaa-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="4fcaa-133">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="4fcaa-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
