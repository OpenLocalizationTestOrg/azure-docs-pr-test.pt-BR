---
title: "aaaAzure B2B do Active Directory personalização e colaboração API | Microsoft Docs"
description: "As relações entre empresas dá suporte à colaboração B2B do Active Directory do Azure, permitindo que os aplicativos corporativos tooselectively de parceiros de negócios acesso"
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
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="17b87-103">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17b87-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="17b87-104">Tivemos muitos clientes Conte-nos se quiserem que o processo de convite Olá toocustomize de maneira que funciona melhor para suas organizações.</span><span class="sxs-lookup"><span data-stu-id="17b87-104">We've had many customers tell us that they want toocustomize hello invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="17b87-105">Com nossa API, você pode fazer exatamente isso.</span><span class="sxs-lookup"><span data-stu-id="17b87-105">With our API, you can do just that.</span></span> [<span data-ttu-id="17b87-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="17b87-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a><span data-ttu-id="17b87-107">Recursos do convite Olá API</span><span class="sxs-lookup"><span data-stu-id="17b87-107">Capabilities of hello invitation API</span></span>
<span data-ttu-id="17b87-108">Olá API oferece Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="17b87-108">hello API offers hello following capabilities:</span></span>

1. <span data-ttu-id="17b87-109">Convidar um usuário com *qualquer* endereço de email.</span><span class="sxs-lookup"><span data-stu-id="17b87-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="17b87-110">Personalize onde deseja que seus usuários tooland depois de aceitar o convite.</span><span class="sxs-lookup"><span data-stu-id="17b87-110">Customize where you want your users tooland after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="17b87-111">Escolha o email de convite padrão toosend hello através de nós</span><span class="sxs-lookup"><span data-stu-id="17b87-111">Choose toosend hello standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="17b87-112">com um destinatário da mensagem toohello que você pode personalizar</span><span class="sxs-lookup"><span data-stu-id="17b87-112">with a message toohello recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="17b87-113">E escolha toocc: pessoas que você deseja tookeep em Olá loop sobre o seu convite a esse parceiro.</span><span class="sxs-lookup"><span data-stu-id="17b87-113">And choose toocc: people you want tookeep in hello loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="17b87-114">Ou, personalize o convite e o fluxo de trabalho de integração escolhendo não toosend notificações por meio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="17b87-114">Or completely customize your invitation and onboarding workflow by choosing not toosend notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="17b87-115">Nesse caso, é obtido um URL de resgate da saudação API que você pode inserir em um modelo de email, mensagem Instantânea ou outro método de distribuição de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="17b87-115">In this case, you get back a redemption URL from hello API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="17b87-116">Por fim, se você for um administrador, você pode escolher o usuário de saudação tooinvite como membro.</span><span class="sxs-lookup"><span data-stu-id="17b87-116">Finally, if you are an admin, you can choose tooinvite hello user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="17b87-117">Modelo de autorização</span><span class="sxs-lookup"><span data-stu-id="17b87-117">Authorization model</span></span>
<span data-ttu-id="17b87-118">Olá API pode ser executado em Olá modos de autorização a seguir:</span><span class="sxs-lookup"><span data-stu-id="17b87-118">hello API can be run in hello following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="17b87-119">Modo Aplicativo + Usuário</span><span class="sxs-lookup"><span data-stu-id="17b87-119">App + User mode</span></span>
<span data-ttu-id="17b87-120">Nesse modo, quem está usando Olá API necessidades toohave Olá permissões toobe criar convites de B2B.</span><span class="sxs-lookup"><span data-stu-id="17b87-120">In this mode, whoever is using hello API needs toohave hello permissions toobe create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="17b87-121">Modo Somente aplicativo</span><span class="sxs-lookup"><span data-stu-id="17b87-121">App only mode</span></span>
<span data-ttu-id="17b87-122">No contexto do aplicativo somente, Olá aplicativo precisa ser User.ReadWrite.All ou Directory.ReadWrite.All escopos para toosucceed de convite Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="17b87-122">In app only context, hello app needs hello User.ReadWrite.All or Directory.ReadWrite.All scopes for hello invitation toosucceed.</span></span>

<span data-ttu-id="17b87-123">Para obter mais informações, consulte: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="17b87-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="17b87-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="17b87-124">PowerShell</span></span>
<span data-ttu-id="17b87-125">É agora possíveis toouse PowerShell tooadd e convidar usuários externos tooan organização facilmente.</span><span class="sxs-lookup"><span data-stu-id="17b87-125">It is now possible toouse PowerShell tooadd and invite external users tooan organization easily.</span></span> <span data-ttu-id="17b87-126">Crie um convite usando o cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="17b87-126">Create an invitation using hello cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="17b87-127">Você pode usar o hello as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="17b87-127">You can use hello following options:</span></span>

* <span data-ttu-id="17b87-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="17b87-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="17b87-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="17b87-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="17b87-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="17b87-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="17b87-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="17b87-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="17b87-132">Você pode conferir as referência de API do convite Olá em [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="17b87-132">You can also check out hello invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="17b87-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="17b87-133">Next steps</span></span>

<span data-ttu-id="17b87-134">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="17b87-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="17b87-135">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="17b87-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="17b87-136">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="17b87-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="17b87-137">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="17b87-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="17b87-138">elementos de saudação do hello email de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="17b87-138">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="17b87-139">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="17b87-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="17b87-140">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="17b87-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="17b87-141">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17b87-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="17b87-142">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17b87-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="17b87-143">Autenticação multifator para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="17b87-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="17b87-144">Adicionar usuários de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="17b87-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="17b87-145">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="17b87-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
