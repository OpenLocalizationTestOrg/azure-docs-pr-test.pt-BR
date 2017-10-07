---
title: "aaaDelegate convites para colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "As propriedades do usuário de colaboração B2B do Azure Active Directory podem ser configuradas"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="69ba2-103">Delegar convites para a colaboração do Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="69ba2-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="69ba2-104">Com a colaboração de business-to-business (B2B) do Azure Active Directory (AD do Azure), você não tem toobe convites de toosend um administrador global.</span><span class="sxs-lookup"><span data-stu-id="69ba2-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="69ba2-105">Em vez disso, você pode usar as políticas e delegar toousers convites cujas funções permitir que eles toosend convites.</span><span class="sxs-lookup"><span data-stu-id="69ba2-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="69ba2-106">É um importante novo modo toodelegate convidado usuário convites por meio da função de emissor do convite convidado hello.</span><span class="sxs-lookup"><span data-stu-id="69ba2-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="69ba2-107">Função Emissor do convite para convidado</span><span class="sxs-lookup"><span data-stu-id="69ba2-107">Guest Inviter role</span></span>
<span data-ttu-id="69ba2-108">Podemos atribuir Olá usuário tooGuest convites de toosend de função do emissor do convite.</span><span class="sxs-lookup"><span data-stu-id="69ba2-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="69ba2-109">Você não tem membro toobe de convites de toosend de função de administrador global hello.</span><span class="sxs-lookup"><span data-stu-id="69ba2-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="69ba2-110">Por padrão, usuários regulares também podem chamar a API de convite Olá a menos que um administrador global desabilitado convites para usuários regulares.</span><span class="sxs-lookup"><span data-stu-id="69ba2-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="69ba2-111">Um usuário também pode chamar a API de saudação usando Olá portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69ba2-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="69ba2-112">Aqui está um exemplo que mostra como toouse PowerShell tooadd uma função do usuário toohello emissor do convite convidado:</span><span class="sxs-lookup"><span data-stu-id="69ba2-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="69ba2-113">Controle quem pode convidar</span><span class="sxs-lookup"><span data-stu-id="69ba2-113">Control who can invite</span></span>

![Controle como tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="69ba2-115">Com colaboração B2B do Azure AD, um administrador de locatários pode definir Olá políticas de convite a seguir:</span><span class="sxs-lookup"><span data-stu-id="69ba2-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="69ba2-116">Desativar convites</span><span class="sxs-lookup"><span data-stu-id="69ba2-116">Turn off invitations</span></span>
- <span data-ttu-id="69ba2-117">Somente administradores e usuários na função de emissor do convite convidado Olá podem convidar</span><span class="sxs-lookup"><span data-stu-id="69ba2-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="69ba2-118">Podem convidar administradores, Olá emissor do convite convidado e membros</span><span class="sxs-lookup"><span data-stu-id="69ba2-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="69ba2-119">Todos os usuários, incluindo convidados, podem convidar</span><span class="sxs-lookup"><span data-stu-id="69ba2-119">All users, including guests, can invite</span></span>

<span data-ttu-id="69ba2-120">Por padrão, os locatários são definidos muito n º 4.</span><span class="sxs-lookup"><span data-stu-id="69ba2-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="69ba2-121">(Todos os usuários, incluindo convidados, podem convidar usuários B2B).</span><span class="sxs-lookup"><span data-stu-id="69ba2-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="69ba2-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69ba2-122">Next steps</span></span>

<span data-ttu-id="69ba2-123">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="69ba2-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="69ba2-124">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="69ba2-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="69ba2-125">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="69ba2-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="69ba2-126">Adicionando uma função de tooa de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="69ba2-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="69ba2-127">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="69ba2-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="69ba2-128">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="69ba2-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="69ba2-129">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="69ba2-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="69ba2-130">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="69ba2-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="69ba2-131">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="69ba2-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="69ba2-132">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="69ba2-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="69ba2-133">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="69ba2-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
