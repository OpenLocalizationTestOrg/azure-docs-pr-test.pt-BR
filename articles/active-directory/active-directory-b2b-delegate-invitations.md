---
title: "Delegar convites para a colaboração do Azure Active Directory B2B | Microsoft Docs"
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="d9ad8-103">Delegar convites para a colaboração do Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d9ad8-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="d9ad8-104">Com a colaboração B2B (entre empresas) do Azure AD (Azure Active Directory), você não precisa ser um administrador global para enviar convites.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="d9ad8-105">Em vez disso, use políticas e delegue convites aos usuários cujas funções permitem o envio de convites.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="d9ad8-106">Uma nova maneira importante de delegar convites de usuário convidado é por meio da função Emissor do convite para convidado.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="d9ad8-107">Função Emissor do convite para convidado</span><span class="sxs-lookup"><span data-stu-id="d9ad8-107">Guest Inviter role</span></span>
<span data-ttu-id="d9ad8-108">Podemos atribuir o usuário à função Emissor do convite para convidado para enviar convites.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="d9ad8-109">Você não precisa ser membro da função de administrador global para enviar convites.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="d9ad8-110">Por padrão, usuários regulares também podem chamar a API de convite, a menos que os convites tenham sido desabilitados pelo administrador global para usuários regulares.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="d9ad8-111">Um usuário também pode chamar a API usando o Portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="d9ad8-112">Veja um exemplo que mostra como usar o PowerShell para adicionar um usuário à função Emissor de convite para convidado:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="d9ad8-113">Controle quem pode convidar</span><span class="sxs-lookup"><span data-stu-id="d9ad8-113">Control who can invite</span></span>

![Controle como convidar](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="d9ad8-115">Com a colaboração B2B do Azure AD, um administrador de locatário pode definir as seguintes políticas de convite:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="d9ad8-116">Desativar convites</span><span class="sxs-lookup"><span data-stu-id="d9ad8-116">Turn off invitations</span></span>
- <span data-ttu-id="d9ad8-117">Somente administradores e usuários na função Emissor de convite para convidado podem convidar</span><span class="sxs-lookup"><span data-stu-id="d9ad8-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="d9ad8-118">Administradores, a função Emissor de convite para convidado e membros podem convidar</span><span class="sxs-lookup"><span data-stu-id="d9ad8-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="d9ad8-119">Todos os usuários, incluindo convidados, podem convidar</span><span class="sxs-lookup"><span data-stu-id="d9ad8-119">All users, including guests, can invite</span></span>

<span data-ttu-id="d9ad8-120">Por padrão, os locatários são definidos como #4.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="d9ad8-121">(Todos os usuários, incluindo convidados, podem convidar usuários B2B).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9ad8-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9ad8-122">Next steps</span></span>

<span data-ttu-id="d9ad8-123">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d9ad8-124">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="d9ad8-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d9ad8-125">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d9ad8-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="d9ad8-126">Adicionar um usuário de colaboração B2B a uma função</span><span class="sxs-lookup"><span data-stu-id="d9ad8-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="d9ad8-127">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d9ad8-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="d9ad8-128">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9ad8-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="d9ad8-129">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d9ad8-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="d9ad8-130">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d9ad8-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="d9ad8-131">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d9ad8-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="d9ad8-132">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="d9ad8-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="d9ad8-133">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d9ad8-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
