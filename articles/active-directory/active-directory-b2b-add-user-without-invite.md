---
title: "Adicionar usuários de colaboração B2B ao Azure Active Directory sem um convite | Microsoft Docs"
description: "É possível permitir que um usuário convidado adicione outros usuários convidados ao Azure AD sem resgatar um convite na colaboração B2B do Azure Active Directory."
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
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="498a8-103">Adicionar usuários convidados da colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="498a8-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="498a8-104">É possível permitir que um usuário, como um representante do parceiro, adicione usuários do parceiro à organização sem a necessidade de resgatar convites.</span><span class="sxs-lookup"><span data-stu-id="498a8-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="498a8-105">Basta conceder a esse usuário privilégios de enumeração no diretório que está sendo usado para a organização do parceiro.</span><span class="sxs-lookup"><span data-stu-id="498a8-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="498a8-106">Conceda esses privilégios quando:</span><span class="sxs-lookup"><span data-stu-id="498a8-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="498a8-107">Um usuário na organização host (por exemplo, WoodGrove) convida um usuário da organização parceira (por exemplo, Sam@litware.com) como Convidado.</span><span class="sxs-lookup"><span data-stu-id="498a8-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="498a8-108">O administrador da organização host define as políticas que permitem ao Sam identificar e adicionar outros usuários da organização parceira (Litware).</span><span class="sxs-lookup"><span data-stu-id="498a8-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="498a8-109">Agora, Davi pode adicionar outros usuários da Litware ao diretório, grupos ou aplicativos da WoodGrove sem a necessidade de resgatar os convites.</span><span class="sxs-lookup"><span data-stu-id="498a8-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="498a8-110">Se Davi tiver os privilégios apropriados de enumeração na Litware, isso ocorrerá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="498a8-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="498a8-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="498a8-111">Next steps</span></span>

<span data-ttu-id="498a8-112">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="498a8-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="498a8-113">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="498a8-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="498a8-114">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="498a8-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="498a8-115">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="498a8-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* <span data-ttu-id="498a8-116">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md) (Os elementos do email de convite para colaboração B2B)</span><span class="sxs-lookup"><span data-stu-id="498a8-116">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md)</span></span>
* [<span data-ttu-id="498a8-117">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="498a8-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="498a8-118">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="498a8-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="498a8-119">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="498a8-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="498a8-120">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="498a8-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="498a8-121">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="498a8-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="498a8-122">Autenticação Multifator para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="498a8-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="498a8-123">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="498a8-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)