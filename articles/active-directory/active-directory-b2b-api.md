---
title: "API e personalização da colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "A colaboração B2B do Active Directory do Azure dá suporte a relações entre empresas, permitindo que os parceiros de negócios acessem de maneira seletiva seus aplicativos corporativos"
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="343e1-103">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="343e1-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="343e1-104">Muitos clientes nos disseram que desejam personalizar o processo de convite de forma que funcione melhor para suas organizações.</span><span class="sxs-lookup"><span data-stu-id="343e1-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="343e1-105">Com nossa API, você pode fazer exatamente isso.</span><span class="sxs-lookup"><span data-stu-id="343e1-105">With our API, you can do just that.</span></span> [<span data-ttu-id="343e1-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="343e1-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="343e1-107">Recursos da API de convite</span><span class="sxs-lookup"><span data-stu-id="343e1-107">Capabilities of the invitation API</span></span>
<span data-ttu-id="343e1-108">A API oferece os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="343e1-108">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="343e1-109">Convidar um usuário com *qualquer* endereço de email.</span><span class="sxs-lookup"><span data-stu-id="343e1-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="343e1-110">Personalizar onde você deseja que os usuários cheguem depois de aceitar o convite.</span><span class="sxs-lookup"><span data-stu-id="343e1-110">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="343e1-111">Optar por enviar o email de convite padrão por nosso intermédio</span><span class="sxs-lookup"><span data-stu-id="343e1-111">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="343e1-112">com uma mensagem para o destinatário que você pode personalizar</span><span class="sxs-lookup"><span data-stu-id="343e1-112">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="343e1-113">E escolher copiar (cc:) as pessoas que você deseja manter no loop sobre o seu convite a esse colaborador.</span><span class="sxs-lookup"><span data-stu-id="343e1-113">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="343e1-114">Ou personalizar completamente seu convite e o fluxo de integração ao optar por não enviar notificações por meio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="343e1-114">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="343e1-115">Nesse caso, você obtém novamente uma URL de resgate da API, que pode ser inserida em um modelo de email, mensagem instantânea ou outro método de distribuição de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="343e1-115">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="343e1-116">Por fim, se você for administrador, poderá convidar o usuário como membro.</span><span class="sxs-lookup"><span data-stu-id="343e1-116">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="343e1-117">Modelo de autorização</span><span class="sxs-lookup"><span data-stu-id="343e1-117">Authorization model</span></span>
<span data-ttu-id="343e1-118">A API pode ser executada nos seguintes modos de autorização:</span><span class="sxs-lookup"><span data-stu-id="343e1-118">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="343e1-119">Modo Aplicativo + Usuário</span><span class="sxs-lookup"><span data-stu-id="343e1-119">App + User mode</span></span>
<span data-ttu-id="343e1-120">Nesse modo, a pessoa que está usando a API precisa ter as permissões para criar convites de B2B.</span><span class="sxs-lookup"><span data-stu-id="343e1-120">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="343e1-121">Modo Somente aplicativo</span><span class="sxs-lookup"><span data-stu-id="343e1-121">App only mode</span></span>
<span data-ttu-id="343e1-122">No contexto somente aplicativo, o aplicativo precisa dos escopos User.ReadWrite.All ou Directory.ReadWrite.All para que o convite tenha êxito.</span><span class="sxs-lookup"><span data-stu-id="343e1-122">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="343e1-123">Para obter mais informações, consulte: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="343e1-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="343e1-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="343e1-124">PowerShell</span></span>
<span data-ttu-id="343e1-125">Agora é possível usar o PowerShell para adicionar e convidar facilmente usuários externos à organização.</span><span class="sxs-lookup"><span data-stu-id="343e1-125">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="343e1-126">Crie um convite usando o cmdlet:</span><span class="sxs-lookup"><span data-stu-id="343e1-126">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="343e1-127">É possível usar as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="343e1-127">You can use the following options:</span></span>

* <span data-ttu-id="343e1-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="343e1-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="343e1-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="343e1-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="343e1-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="343e1-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="343e1-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="343e1-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="343e1-132">Confira também a referência da API de convite em [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="343e1-132">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="343e1-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="343e1-133">Next steps</span></span>

<span data-ttu-id="343e1-134">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="343e1-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="343e1-135">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="343e1-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="343e1-136">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="343e1-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="343e1-137">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="343e1-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* <span data-ttu-id="343e1-138">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md) (Os elementos do email de convite para colaboração B2B)</span><span class="sxs-lookup"><span data-stu-id="343e1-138">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md)</span></span>
* [<span data-ttu-id="343e1-139">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="343e1-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="343e1-140">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="343e1-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="343e1-141">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="343e1-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="343e1-142">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="343e1-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="343e1-143">Autenticação multifator para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="343e1-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="343e1-144">Adicionar usuários de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="343e1-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="343e1-145">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="343e1-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
