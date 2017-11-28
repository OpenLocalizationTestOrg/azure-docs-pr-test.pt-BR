---
title: "Azure AD Connect: Logon Único Contínuo – como ele funciona | Microsoft Docs"
description: "Este artigo descreve como funciona hello Azure Active Directory perfeita logon único no recurso."
services: active-directory
keywords: "o que é o Azure AD Connect, instalar o Active Directory, componentes necessários do Azure AD, SSO, Logon Único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="f881c-104">Logon Único Contínuo do Azure Active Directory: aprofundamento técnico</span><span class="sxs-lookup"><span data-stu-id="f881c-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="f881c-105">Este artigo fornece detalhes técnicos em como funciona o recurso de saudação do Azure Active Directory perfeita-logon único (SSO contínuo).</span><span class="sxs-lookup"><span data-stu-id="f881c-105">This article gives you technical details into how hello Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f881c-106">recurso de SSO contínuo Hello está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="f881c-106">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="f881c-107">Como o SSO contínuo funciona?</span><span class="sxs-lookup"><span data-stu-id="f881c-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="f881c-108">Esta seção tem tooit de duas partes:</span><span class="sxs-lookup"><span data-stu-id="f881c-108">This section has two parts tooit:</span></span>
1. <span data-ttu-id="f881c-109">instalação de saudação do recurso de SSO contínuo hello.</span><span class="sxs-lookup"><span data-stu-id="f881c-109">hello setup of hello Seamless SSO feature.</span></span>
2. <span data-ttu-id="f881c-110">Como uma transação única de entrada de usuário funciona com o SSO Contínuo.</span><span class="sxs-lookup"><span data-stu-id="f881c-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="f881c-111">Como funciona a configuração?</span><span class="sxs-lookup"><span data-stu-id="f881c-111">How does set up work?</span></span>

<span data-ttu-id="f881c-112">O SSO Contínuo é habilitado por meio do Azure AD Connect, conforme mostrado [aqui](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="f881c-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="f881c-113">Ao habilitar o recurso de hello, Olá etapas a seguir ocorre:</span><span class="sxs-lookup"><span data-stu-id="f881c-113">While enabling hello feature, hello following steps occur:</span></span>
- <span data-ttu-id="f881c-114">Uma conta de computador denominada `AZUREADSSOACCT` (que representa o Azure AD) é criada em seu AD (Active Directory) local.</span><span class="sxs-lookup"><span data-stu-id="f881c-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="f881c-115">chave de descriptografia do Kerberos da conta do computador Olá é compartilhado com segurança com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f881c-115">hello computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="f881c-116">Além disso, dois Kerberos nomes principais de serviço (SPNs) são criados toorepresent duas URLs são usadas durante a entrada do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f881c-116">In addition, two Kerberos service principal names (SPNs) are created toorepresent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="f881c-117">conta de computador Hello e SPNs do Kerberos Olá são criados em cada floresta do AD sincronizar tooAzure AD (usando o Azure AD Connect) e cujos usuários você deseja SSO contínuo.</span><span class="sxs-lookup"><span data-stu-id="f881c-117">hello computer account and hello Kerberos SPNs are created in each AD forest you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="f881c-118">Mover Olá `AZUREADSSOACCT` tooan de conta de computador UO (unidade organizacional) em que outras contas de computador são armazenado tooensure que ele é gerenciado no hello mesmo maneira e não será excluído.</span><span class="sxs-lookup"><span data-stu-id="f881c-118">Move hello `AZUREADSSOACCT` computer account tooan Organization Unit (OU) where other computer accounts are stored tooensure that it is managed in hello same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f881c-119">É altamente recomendável que você [sobrepor a chave de descriptografia de Kerberos Olá](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) de saudação `AZUREADSSOACCT` conta de computador pelo menos a cada 30 dias.</span><span class="sxs-lookup"><span data-stu-id="f881c-119">We highly recommend that you [roll over hello Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of hello `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="f881c-120">Como a entrada com o SSO Contínuo funciona?</span><span class="sxs-lookup"><span data-stu-id="f881c-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="f881c-121">Após a conclusão da instalação hello, SSO contínuo funciona Olá mesma maneira como qualquer outra entrada que usa autenticação do Windows integrada (IWA).</span><span class="sxs-lookup"><span data-stu-id="f881c-121">Once hello set-up is complete, Seamless SSO works hello same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="f881c-122">fluxo de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f881c-122">hello flow is as follows:</span></span>

1. <span data-ttu-id="f881c-123">usuário de saudação tenta tooaccess um aplicativo (por exemplo, Olá Outlook Web App - https://outlook.office365.com/owa/) de um dispositivo corporativo domínio dentro da rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="f881c-123">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="f881c-124">Se o usuário Olá não tiver entrado, usuário Olá é redirecionado toohello AD do Azure-página de entrada.</span><span class="sxs-lookup"><span data-stu-id="f881c-124">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="f881c-125">Se a solicitação de entrada hello AD do Azure inclui um `domain_hint` (identifica o locatário - por exemplo, contoso.onmicrosoft.com) ou `login_hint` (identificação de usuário Olá - por exemplo, user@contoso.onmicrosoft.com ou user@contoso.com) parâmetro e, em seguida, etapa 2 é ignorada.</span><span class="sxs-lookup"><span data-stu-id="f881c-125">If hello Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying hello user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="f881c-126">tipos de usuário Olá em seu nome de usuário na página de entrada hello AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f881c-126">hello user types in their user name into hello Azure AD sign-in page.</span></span>
4. <span data-ttu-id="f881c-127">Usando JavaScript no plano de fundo hello, o AD do Azure desafios navegador hello, por meio de uma resposta 401 não autorizado, tooprovide um tíquete Kerberos.</span><span class="sxs-lookup"><span data-stu-id="f881c-127">Using JavaScript in hello background, Azure AD challenges hello browser, via a 401 Unauthorized response, tooprovide a Kerberos ticket.</span></span>
5. <span data-ttu-id="f881c-128">navegador Hello, por sua vez, solicita um tíquete do Active Directory para Olá `AZUREADSSOACCT` conta de computador (que representa o AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f881c-128">hello browser, in turn, requests a ticket from Active Directory for hello `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="f881c-129">Active Directory localiza a conta de computador hello e retorna um navegador de toohello de tíquete Kerberos criptografado com o segredo da conta de computador hello.</span><span class="sxs-lookup"><span data-stu-id="f881c-129">Active Directory locates hello computer account and returns a Kerberos ticket toohello browser encrypted with hello computer account's secret.</span></span>
7. <span data-ttu-id="f881c-130">navegador de saudação encaminha o tíquete do Kerberos Olá adquiriu a tooAzure do Active Directory AD (em uma saudação [URLs do AD do Azure adicionados anteriormente as configurações de zona de Intranet do navegador toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="f881c-130">hello browser forwards hello Kerberos ticket it acquired from Active Directory tooAzure AD (on one of hello [Azure AD URLs previously added toohello browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="f881c-131">Azure AD descriptografa Olá tíquete Kerberos, que inclui a identidade de saudação do usuário Olá conectado ao dispositivo corporativo hello, usar Olá anteriormente chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="f881c-131">Azure AD decrypts hello Kerberos ticket, which includes hello identity of hello user signed into hello corporate device, using hello previously shared key.</span></span>
9. <span data-ttu-id="f881c-132">Após a avaliação, AD do Azure retorna um aplicativo de token toohello back ou solicita Olá usuário tooperform provas adicionais, como autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="f881c-132">After evaluation, Azure AD either returns a token back toohello application or asks hello user tooperform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="f881c-133">Se Olá usuário entrar for bem-sucedida, o usuário de saudação é tooaccess capaz de aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="f881c-133">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="f881c-134">Olá diagrama a seguir ilustra todos os componentes de saudação e etapas de saudação envolvidos.</span><span class="sxs-lookup"><span data-stu-id="f881c-134">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Logon Único Contínuo](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="f881c-136">SSO contínuo é oportunista, o que significa que se ele falhar, a experiência de entrada hello reverterá ser tooits comportamento normal - ou seja, Olá usuário precisa tooenter toosign sua senha no.</span><span class="sxs-lookup"><span data-stu-id="f881c-136">Seamless SSO is opportunistic, which means if it fails, hello sign-in experience falls back tooits regular behavior - i.e, hello user needs tooenter their password toosign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f881c-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f881c-137">Next steps</span></span>

- <span data-ttu-id="f881c-138">[**Início Rápido** ](active-directory-aadconnect-sso-quick-start.md) – colocar o SSO Contínuo do Azure AD em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="f881c-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="f881c-139">[**Perguntas frequentes sobre** ](active-directory-aadconnect-sso-faq.md) -respostas toofrequently perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="f881c-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="f881c-140">[**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Saiba como tooresolve comum problemas com o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f881c-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="f881c-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="f881c-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
