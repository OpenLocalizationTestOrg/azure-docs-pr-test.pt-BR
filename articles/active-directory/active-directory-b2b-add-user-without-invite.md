---
title: "aaaAdd B2B colaboração usuários tooAzure do Active Directory sem um convite | Microsoft Docs"
description: "Você pode permitir que um usuário convidado adicionar outros usuários de convidado tooyour AD do Azure sem resgatar um convite em colaboração B2B do Azure Active Directory."
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="ec431-103">Adicionar usuários convidados da colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="ec431-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="ec431-104">Você pode permitir que um usuário, como um parceiro, tooadd usuários da organização do hello parceiro tooyour sem a necessidade de convites toobe resgatado.</span><span class="sxs-lookup"><span data-stu-id="ec431-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="ec431-105">Tudo o que você deve fazer é conceder privilégios de enumeração no diretório Olá que você está usando para Olá parceiro org de usuário</span><span class="sxs-lookup"><span data-stu-id="ec431-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="ec431-106">Conceda esses privilégios quando:</span><span class="sxs-lookup"><span data-stu-id="ec431-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="ec431-107">Um usuário de organização de host da saudação (por exemplo, o WoodGrove) convida um usuário da organização do parceiro de saudação (por exemplo, Sam@litware.com) como convidado.</span><span class="sxs-lookup"><span data-stu-id="ec431-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="ec431-108">Olá administrador na organização do host Olá define as políticas que permitem Sam tooidentify e adicionar outros usuários da organização do parceiro de saudação (Litware).</span><span class="sxs-lookup"><span data-stu-id="ec431-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="ec431-109">Agora o Sam pode adicionar outros usuários da Litware toohello WoodGrove diretório, grupos ou aplicativos sem a necessidade de convites toobe resgatado.</span><span class="sxs-lookup"><span data-stu-id="ec431-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="ec431-110">Se o Sam tem privilégios de enumeração apropriado Olá no Litware, isso acontece automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ec431-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="ec431-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ec431-111">Next steps</span></span>

<span data-ttu-id="ec431-112">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="ec431-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="ec431-113">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="ec431-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="ec431-114">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="ec431-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="ec431-115">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="ec431-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="ec431-116">elementos de saudação do hello email de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ec431-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="ec431-117">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ec431-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="ec431-118">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec431-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="ec431-119">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec431-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="ec431-120">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec431-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="ec431-121">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec431-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="ec431-122">Autenticação Multifator para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="ec431-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="ec431-123">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ec431-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)