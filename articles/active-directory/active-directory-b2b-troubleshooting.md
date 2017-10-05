---
title: "Solução de problemas de colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "Correções para problemas comuns com a colaboração B2B do Azure Active Directory"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 2009cfc956a2703e268c9364996aa2d0fbd8f279
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="351ce-103">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="351ce-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="351ce-104">Confira aqui algumas correções para problemas comuns da colaboração B2B do Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="351ce-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="351ce-105">Adicionei um usuário externo, mas não consigo vê-lo em meu Catálogo de Endereços Global ou no seletor de pessoas</span><span class="sxs-lookup"><span data-stu-id="351ce-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="351ce-106">Para casos nos quais os usuários externos não são preenchidos na lista, o objeto pode demorar alguns minutos para replicar.</span><span class="sxs-lookup"><span data-stu-id="351ce-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="351ce-107">Um usuário convidado de B2B não está aparecendo no seletor de pessoas do SharePoint Online/OneDrive</span><span class="sxs-lookup"><span data-stu-id="351ce-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="351ce-108">A capacidade de pesquisar por usuários convidados existentes no seletor de pessoas do SharePoint Online (SPO) está desativado por padrão para coincidir com o comportamento herdado.</span><span class="sxs-lookup"><span data-stu-id="351ce-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="351ce-109">Esse recurso pode ser habilitado usando a configuração 'ShowPeoplePickerSuggestionsForGuestUsers' na coleta do site e do locatário.</span><span class="sxs-lookup"><span data-stu-id="351ce-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="351ce-110">Defina esse recurso usando os cmdlets Set-SPOTenant e SPOSite, que permitem aos membros pesquisar todos os usuários convidados existentes no diretório.</span><span class="sxs-lookup"><span data-stu-id="351ce-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="351ce-111">Alterações no escopo de locatário não afetam sites SPO já provisionados.</span><span class="sxs-lookup"><span data-stu-id="351ce-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="351ce-112">Os convites foram desabilitados para o diretório</span><span class="sxs-lookup"><span data-stu-id="351ce-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="351ce-113">Se você receber uma notificação indicando que você não tem permissões para convidar usuários, verifique se a sua conta de usuário tem autorização para convidar usuários externos em Configurações do Usuário:</span><span class="sxs-lookup"><span data-stu-id="351ce-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="351ce-114">Se você tiver modificado essas configurações recentemente ou se tiver atribuído a função Emissor de convite convidado a um usuário, talvez ocorra um atraso de 15 a 60 minutos até que as alterações tenham efeito.</span><span class="sxs-lookup"><span data-stu-id="351ce-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="351ce-115">O usuário que eu convidei está recebendo um erro durante o resgate</span><span class="sxs-lookup"><span data-stu-id="351ce-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="351ce-116">Os erros comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="351ce-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="351ce-117">O Admin do convidado não permite a criação de Usuários Verificados por Email em seu locatário</span><span class="sxs-lookup"><span data-stu-id="351ce-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="351ce-118">Ao convidar usuários cuja organização está usando o Azure Active Directory onde a conta do usuário específico não existe (por exemplo, o usuário não existe no Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="351ce-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="351ce-119">O administrador de contoso.com pode ter uma política em vigor para impedir a criação de usuários.</span><span class="sxs-lookup"><span data-stu-id="351ce-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="351ce-120">O usuário deve verificar com o administrador para determinar se os usuários externos são permitidos.</span><span class="sxs-lookup"><span data-stu-id="351ce-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="351ce-121">A administração de usuário externo pode ter que permitir usuários verificados por email em seu domínio (consulte este [artigo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) sobre como permitir Usuários de Email Verificados).</span><span class="sxs-lookup"><span data-stu-id="351ce-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="351ce-122">O usuário externo ainda não existe em um domínio federado</span><span class="sxs-lookup"><span data-stu-id="351ce-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="351ce-123">Se você estiver usando a autenticação de Federação e o usuário ainda não existir no Azure Active Directory, o usuário não poderá ser convidado.</span><span class="sxs-lookup"><span data-stu-id="351ce-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="351ce-124">Para resolver esse problema, o administrador do usuário externo deve sincronizar a conta do usuário ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="351ce-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="351ce-125">Como ‘\#’, que normalmente não é um caractere válido, é sincronizado com o Azure AD?</span><span class="sxs-lookup"><span data-stu-id="351ce-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="351ce-126">"\#" é um caractere reservado no UPNs para colaboração B2B do Azure AD ou usuários externos, pois a conta convidada user@contoso.com se torna user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="351ce-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="351ce-127">Portanto, não há permissão para \# em UPNs provenientes do local entrar no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="351ce-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="351ce-128">Recebo um erro ao adicionar usuários externos a um grupo sincronizado</span><span class="sxs-lookup"><span data-stu-id="351ce-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="351ce-129">Os usuários externos podem ser adicionados apenas a grupos de "Segurança" ou "atribuído", e não a grupos que são masterizados localmente.</span><span class="sxs-lookup"><span data-stu-id="351ce-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="351ce-130">Meu usuário externo não recebeu um email para o resgate</span><span class="sxs-lookup"><span data-stu-id="351ce-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="351ce-131">O convidado deve verificar com seu ISP ou o filtro de spam para garantir que o seguinte endereço tem permissão: Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="351ce-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="351ce-132">Observei que, às vezes, a mensagem personalizada não é incluída nas mensagens de convite</span><span class="sxs-lookup"><span data-stu-id="351ce-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="351ce-133">Para cumprir as leis de privacidade, nossas APIs não incluem mensagens personalizadas no convite por email quando:</span><span class="sxs-lookup"><span data-stu-id="351ce-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="351ce-134">O emissor do convite não tem um endereço de email no locatário que está convidando</span><span class="sxs-lookup"><span data-stu-id="351ce-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="351ce-135">Quando uma entidade do serviço de aplicativo envia o convite</span><span class="sxs-lookup"><span data-stu-id="351ce-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="351ce-136">Se esse cenário for importante para você, suprima nosso email de convite de API e envie-o por meio de um mecanismo de email de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="351ce-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="351ce-137">Consulte o departamento jurídico de sua organização para verificar se todo email enviado dessa forma também está em conformidade com as leis de privacidade.</span><span class="sxs-lookup"><span data-stu-id="351ce-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="351ce-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="351ce-138">Next steps</span></span>

<span data-ttu-id="351ce-139">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="351ce-139">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="351ce-140">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="351ce-140">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="351ce-141">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="351ce-141">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="351ce-142">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="351ce-142">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* <span data-ttu-id="351ce-143">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md) (Os elementos do email de convite para colaboração B2B)</span><span class="sxs-lookup"><span data-stu-id="351ce-143">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md)</span></span>
* [<span data-ttu-id="351ce-144">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="351ce-144">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="351ce-145">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="351ce-145">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="351ce-146">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="351ce-146">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="351ce-147">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="351ce-147">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="351ce-148">Autenticação multifator para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="351ce-148">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="351ce-149">Adicionar usuários de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="351ce-149">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="351ce-150">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="351ce-150">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
