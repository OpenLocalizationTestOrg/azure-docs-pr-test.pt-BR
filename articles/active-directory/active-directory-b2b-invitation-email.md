---
title: "Os elementos do email de convite para colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "Modelo de email de convite para colaboração B2B do Azure Active Directory"
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
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="d9e77-103">Os elementos do email de convite para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d9e77-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="d9e77-104">Emails de convite são um componente essencial para ingressar parceiros como usuários de colaboração B2B no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9e77-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="d9e77-105">Você pode usá-los para aumentar a confiança do destinatário.</span><span class="sxs-lookup"><span data-stu-id="d9e77-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="d9e77-106">Você pode adicionar a legitimidade e a comprovação social ao email, para certificar-se de que o destinatário sinta-se confortável com a seleção do botão **Introdução** para aceitar o convite.</span><span class="sxs-lookup"><span data-stu-id="d9e77-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="d9e77-107">Essa confiança é uma maneira importante de reduzir o atrito de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="d9e77-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="d9e77-108">E o email fica ótimo dessa maneira!</span><span class="sxs-lookup"><span data-stu-id="d9e77-108">And you also want to make the email look great!</span></span>

![Email de convite de B2b do AD do Azure](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="d9e77-110">Explicação do email</span><span class="sxs-lookup"><span data-stu-id="d9e77-110">Explaining the email</span></span>
<span data-ttu-id="d9e77-111">Vamos examinar alguns elementos do email para que você conheça a melhor maneira de usar esses recursos.</span><span class="sxs-lookup"><span data-stu-id="d9e77-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="d9e77-112">Subject</span><span class="sxs-lookup"><span data-stu-id="d9e77-112">Subject</span></span>
<span data-ttu-id="d9e77-113">O assunto do email segue o seguinte padrão: você foi convidado para a organização &lt;nomedolocatário&gt;</span><span class="sxs-lookup"><span data-stu-id="d9e77-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="d9e77-114">Do endereço</span><span class="sxs-lookup"><span data-stu-id="d9e77-114">From address</span></span>
<span data-ttu-id="d9e77-115">Usamos um padrão parecido com o do LinkedIn para o endereço De.</span><span class="sxs-lookup"><span data-stu-id="d9e77-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="d9e77-116">Você deve deixar claro quem é o emissor do convite e de qual empresa, e também esclarecer que o email é proveniente de um endereço de email da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d9e77-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="d9e77-117">O formato é: &lt;Nome de exibição do emissor do convite&gt; de &lt;nome do locatário&gt; (via Microsoft) <invites@microsoft.com&gt;</span><span class="sxs-lookup"><span data-stu-id="d9e77-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="d9e77-118">Responder Para</span><span class="sxs-lookup"><span data-stu-id="d9e77-118">Reply To</span></span>
<span data-ttu-id="d9e77-119">O email para resposta é definido como o email do emissor do convite, quando houver um disponível, para que a resposta envie um email ao emissor do convite.</span><span class="sxs-lookup"><span data-stu-id="d9e77-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="d9e77-120">Identidade visual</span><span class="sxs-lookup"><span data-stu-id="d9e77-120">Branding</span></span>
<span data-ttu-id="d9e77-121">Os emails de convite de seu locatário usam a identidade visual da empresa configurada para o locatário.</span><span class="sxs-lookup"><span data-stu-id="d9e77-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="d9e77-122">Se você quiser aproveitar esse recurso, [estes](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) são os detalhes da configuração.</span><span class="sxs-lookup"><span data-stu-id="d9e77-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="d9e77-123">O logotipo da faixa é exibido no email.</span><span class="sxs-lookup"><span data-stu-id="d9e77-123">The banner logo appears in the email.</span></span> <span data-ttu-id="d9e77-124">Siga as instruções de tamanho e qualidade da imagem [aqui](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) para obter os melhores resultados.</span><span class="sxs-lookup"><span data-stu-id="d9e77-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="d9e77-125">Além disso, o nome da empresa também aparece no plano de ação.</span><span class="sxs-lookup"><span data-stu-id="d9e77-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="d9e77-126">Plano de ação</span><span class="sxs-lookup"><span data-stu-id="d9e77-126">Call to action</span></span>
<span data-ttu-id="d9e77-127">O plano de ação é composto por duas partes: explicação do motivo de o destinatário ter recebido o email, e o que o destinatário deve fazer a respeito.</span><span class="sxs-lookup"><span data-stu-id="d9e77-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="d9e77-128">A seção "motivo" pode ter o seguinte padrão: Você foi convidado(a) para acessar aplicativos na organização &lt;nomedolocatário&gt;</span><span class="sxs-lookup"><span data-stu-id="d9e77-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="d9e77-129">E a seção "o que você deve fazer" é indicada pela presença do botão **Introdução**.</span><span class="sxs-lookup"><span data-stu-id="d9e77-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="d9e77-130">Quando o destinatário tiver sido adicionado sem a necessidade de convites, esse botão não aparecerá.</span><span class="sxs-lookup"><span data-stu-id="d9e77-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="d9e77-131">Informações sobre o emissor do convite</span><span class="sxs-lookup"><span data-stu-id="d9e77-131">Inviter's information</span></span>
<span data-ttu-id="d9e77-132">O nome de exibição do emissor do convite está incluído no email.</span><span class="sxs-lookup"><span data-stu-id="d9e77-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="d9e77-133">E, além disso, se você tiver configurado uma foto de perfil para sua conta do Azure AD, o email do convite também incluirá a imagem.</span><span class="sxs-lookup"><span data-stu-id="d9e77-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="d9e77-134">Ambos servem para aumentar a confiança do destinatário do email.</span><span class="sxs-lookup"><span data-stu-id="d9e77-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="d9e77-135">Se você ainda não tiver configurado uma imagem de perfil, um ícone com as iniciais do emissor do convite no lugar da imagem, conforme mostra a imagem:</span><span class="sxs-lookup"><span data-stu-id="d9e77-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![exibição das iniciais do emissor do convite](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="d9e77-137">Corpo</span><span class="sxs-lookup"><span data-stu-id="d9e77-137">Body</span></span>
<span data-ttu-id="d9e77-138">O corpo conterá a mensagem que o emissor compõe ou a passada na API do convite.</span><span class="sxs-lookup"><span data-stu-id="d9e77-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="d9e77-139">Como é uma área de texto, ela não processa marcas HTML por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="d9e77-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="d9e77-140">Seção de rodapé</span><span class="sxs-lookup"><span data-stu-id="d9e77-140">Footer section</span></span>
<span data-ttu-id="d9e77-141">O rodapé contém a marca da empresa Microsoft e informará ao destinatário se o email foi enviado de um alias não monitorado.</span><span class="sxs-lookup"><span data-stu-id="d9e77-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="d9e77-142">Casos especiais:</span><span class="sxs-lookup"><span data-stu-id="d9e77-142">Special cases:</span></span>

- <span data-ttu-id="d9e77-143">O emissor do convite não tem um endereço de email no locatário que está convidando</span><span class="sxs-lookup"><span data-stu-id="d9e77-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![imagem do emissor do convite não tem um endereço de email no locatário que está convidando](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="d9e77-145">O destinatário não precisa resgatar o convite</span><span class="sxs-lookup"><span data-stu-id="d9e77-145">The recipient doesn't need to redeem the invitation</span></span>

  ![quando o destinatário não precisa resgatar o convite](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="d9e77-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9e77-147">Next steps</span></span>

<span data-ttu-id="d9e77-148">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="d9e77-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d9e77-149">O que é a colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9e77-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d9e77-150">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="d9e77-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="d9e77-151">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="d9e77-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="d9e77-152">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d9e77-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="d9e77-153">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9e77-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="d9e77-154">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9e77-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="d9e77-155">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9e77-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="d9e77-156">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9e77-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="d9e77-157">Autenticação multifator para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="d9e77-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="d9e77-158">Adicionar usuários de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="d9e77-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="d9e77-159">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d9e77-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
