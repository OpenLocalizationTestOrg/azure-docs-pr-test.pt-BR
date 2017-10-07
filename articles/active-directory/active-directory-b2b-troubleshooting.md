---
title: "aaaTroubleshooting colaboração B2B do Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="09dec-103">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09dec-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="09dec-104">Confira aqui algumas correções para problemas comuns da colaboração B2B do Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="09dec-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="09dec-105">Adicionar um usuário externo, mas não vê-los no meu Catálogo de endereços Global ou no seletor de pessoas Olá</span><span class="sxs-lookup"><span data-stu-id="09dec-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="09dec-106">Em casos em que os usuários externos não são preenchidos na lista hello, objeto Olá pode levar tooreplicate de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="09dec-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="09dec-107">Um usuário convidado de B2B não está aparecendo no seletor de pessoas do SharePoint Online/OneDrive</span><span class="sxs-lookup"><span data-stu-id="09dec-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="09dec-108">Olá toosearch de capacidade para os usuários existentes de convidado no seletor de pessoas saudação do SharePoint Online (SPO) é desativado por comportamento herdado de toomatch padrão.</span><span class="sxs-lookup"><span data-stu-id="09dec-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="09dec-109">Você pode habilitar esse recurso usando Olá a definição 'ShowPeoplePickerSuggestionsForGuestUsers' na coleção de locatário e site Olá nível.</span><span class="sxs-lookup"><span data-stu-id="09dec-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="09dec-110">Você pode definir o recurso de saudação usando Olá conjunto SPOTenant e SPOSite do conjunto de cmdlets, que permitem aos membros toosearch todos os usuários convidados existentes no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="09dec-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="09dec-111">Alterações no escopo de locatário Olá não afetam a sites SPO já provisionados.</span><span class="sxs-lookup"><span data-stu-id="09dec-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="09dec-112">Os convites foram desabilitados para o diretório</span><span class="sxs-lookup"><span data-stu-id="09dec-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="09dec-113">Se você será notificado de que você não tem permissões tooinvite os usuários, verifique se sua conta de usuário está autorizado tooinvite a usuários externos em configurações de usuário:</span><span class="sxs-lookup"><span data-stu-id="09dec-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="09dec-114">Se você modificou essas configurações ou Olá emissor do convite convidado função tooa usuário atribuído recentemente, pode haver um atraso de 15 a 60 minutos antes de saudação alterações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="09dec-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="09dec-115">usuário Hello, convidado está recebendo um erro durante o resgate</span><span class="sxs-lookup"><span data-stu-id="09dec-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="09dec-116">Os erros comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="09dec-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="09dec-117">O Admin do convidado não permite a criação de Usuários Verificados por Email em seu locatário</span><span class="sxs-lookup"><span data-stu-id="09dec-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="09dec-118">Quando convidar usuários cuja organização está usando o Active Directory do Azure, mas Olá onde a conta de usuário específica não existe (por exemplo, Olá usuário não existe no AD do Azure contoso.com).</span><span class="sxs-lookup"><span data-stu-id="09dec-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="09dec-119">administrador de saudação de contoso.com pode ter uma política em vigor para impedir que usuários que está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="09dec-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="09dec-120">usuário Olá deve verificar com toodetermine seu administrador se os usuários externos são permitidos.</span><span class="sxs-lookup"><span data-stu-id="09dec-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="09dec-121">Olá administrador do usuário externo pode ser necessário tooallow usuários de Email é verificado em seu domínio (consulte este [artigo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) em permitir que os usuários verificado de Email).</span><span class="sxs-lookup"><span data-stu-id="09dec-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="09dec-122">O usuário externo ainda não existe em um domínio federado</span><span class="sxs-lookup"><span data-stu-id="09dec-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="09dec-123">Se você estiver usando a autenticação de Federação e usuário Olá ainda não existir no Active Directory do Azure, o usuário Olá não pode ser convidado.</span><span class="sxs-lookup"><span data-stu-id="09dec-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="09dec-124">tooresolve esse problema, Olá administrador de usuário externo deve sincronizar tooAzure de conta do usuário de saudação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="09dec-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="09dec-125">Como ‘\#’, que normalmente não é um caractere válido, é sincronizado com o Azure AD?</span><span class="sxs-lookup"><span data-stu-id="09dec-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="09dec-126">"\#" é um caractere reservado no UPNs para colaboração B2B do Azure AD ou usuários externos, porque a conta de convidado Olá user@contoso.com se torna user_contoso.com#EXT@fabrikam.onmicrosoft.com. Portanto, \# em UPNs provenientes de locais não são permitidas toosign em toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="09dec-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="09dec-127">Recebo um erro ao adicionar usuários externos tooa sincronizados grupo</span><span class="sxs-lookup"><span data-stu-id="09dec-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="09dec-128">Os usuários externos podem ser adicionados somente muito "atribuído" ou grupos de "Segurança" e não toogroups que são dominados local.</span><span class="sxs-lookup"><span data-stu-id="09dec-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="09dec-129">Meu usuário externo não recebeu um email tooredeem</span><span class="sxs-lookup"><span data-stu-id="09dec-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="09dec-130">Verifique com seu ISP convidado Hello ou tooensure de filtro de spam Olá endereço a seguir é permitido:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="09dec-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="09dec-131">Observem que essa mensagem de saudação personalizada não obtém incluída com mensagens de convite às vezes</span><span class="sxs-lookup"><span data-stu-id="09dec-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="09dec-132">toocomply com as leis de privacidade, nossas APIs não incluem mensagens personalizadas no convite por email hello quando:</span><span class="sxs-lookup"><span data-stu-id="09dec-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="09dec-133">emissor do convite Olá não tem um endereço de email no hello convidar locatário</span><span class="sxs-lookup"><span data-stu-id="09dec-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="09dec-134">Quando uma entidade de serviço de aplicativo envia o convite Olá</span><span class="sxs-lookup"><span data-stu-id="09dec-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="09dec-135">Se esse cenário é importante tooyou, suprimir nosso email de convite de API e enviá-lo por meio do mecanismo de email de saudação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="09dec-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="09dec-136">Consulte toomake de departamento jurídico da sua organização se nenhum email que enviar dessa forma também está em conformidade com as leis de privacidade.</span><span class="sxs-lookup"><span data-stu-id="09dec-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09dec-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09dec-137">Next steps</span></span>

<span data-ttu-id="09dec-138">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="09dec-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="09dec-139">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="09dec-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="09dec-140">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="09dec-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="09dec-141">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="09dec-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="09dec-142">elementos de saudação do hello email de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="09dec-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="09dec-143">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="09dec-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="09dec-144">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="09dec-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="09dec-145">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09dec-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="09dec-146">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09dec-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="09dec-147">Autenticação multifator para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="09dec-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="09dec-148">Adicionar usuários de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="09dec-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="09dec-149">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="09dec-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
