---
title: "Azure AD Connect: Logon Único Contínuo – como ele funciona | Microsoft Docs"
description: "Este artigo descreve como o recurso Logon Único Contínuo do Azure Active Directory funciona."
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
ms.openlocfilehash: f0bcbdb03fbb70ff91ac3a56974a88eb1b26c245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="086e5-104">Logon Único Contínuo do Azure Active Directory: aprofundamento técnico</span><span class="sxs-lookup"><span data-stu-id="086e5-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="086e5-105">Este artigo fornece detalhes técnicos sobre como o recurso SSO Contínuo (Logon único contínuo) do Azure Active Directory funciona.</span><span class="sxs-lookup"><span data-stu-id="086e5-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="086e5-106">Atualmente, o recurso SSO Contínuo está em visualização.</span><span class="sxs-lookup"><span data-stu-id="086e5-106">The Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="086e5-107">Como o SSO contínuo funciona?</span><span class="sxs-lookup"><span data-stu-id="086e5-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="086e5-108">Esta seção tem duas partes:</span><span class="sxs-lookup"><span data-stu-id="086e5-108">This section has two parts to it:</span></span>
1. <span data-ttu-id="086e5-109">A instalação do recurso de SSO Contínuo.</span><span class="sxs-lookup"><span data-stu-id="086e5-109">The setup of the Seamless SSO feature.</span></span>
2. <span data-ttu-id="086e5-110">Como uma transação única de entrada de usuário funciona com o SSO Contínuo.</span><span class="sxs-lookup"><span data-stu-id="086e5-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="086e5-111">Como funciona a configuração?</span><span class="sxs-lookup"><span data-stu-id="086e5-111">How does set up work?</span></span>

<span data-ttu-id="086e5-112">O SSO Contínuo é habilitado por meio do Azure AD Connect, conforme mostrado [aqui](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="086e5-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="086e5-113">Ao habilitar o recurso, ocorrem as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="086e5-113">While enabling the feature, the following steps occur:</span></span>
- <span data-ttu-id="086e5-114">Uma conta de computador denominada `AZUREADSSOACCT` (que representa o Azure AD) é criada em seu AD (Active Directory) local.</span><span class="sxs-lookup"><span data-stu-id="086e5-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="086e5-115">A chave de descriptografia Kerberos da conta do computador é compartilhada com segurança com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="086e5-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="086e5-116">Além disso, os dois SPNs (nomes de entidade de serviço) Kerberos são criados para representar duas URLs que são usadas durante a entrada no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="086e5-116">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="086e5-117">A conta do computador e os SPNs Kerberos são criados em cada floresta do AD que você sincroniza com o Azure AD (usando o Azure AD Connect) e para cujos usuários você deseja o SSO Contínuo.</span><span class="sxs-lookup"><span data-stu-id="086e5-117">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="086e5-118">Mova a conta do computador `AZUREADSSOACCT` para uma UO (unidade organizacional) em que outras contas de computador são armazenadas para garantir que ela seja gerenciada da mesma maneira e não seja excluída.</span><span class="sxs-lookup"><span data-stu-id="086e5-118">Move the `AZUREADSSOACCT` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="086e5-119">É altamente recomendável que você [sobreponha a chave de descriptografia do Kerberos](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) da conta do computador `AZUREADSSOACCT` pelo menos a cada 30 dias.</span><span class="sxs-lookup"><span data-stu-id="086e5-119">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of the `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="086e5-120">Como a entrada com o SSO Contínuo funciona?</span><span class="sxs-lookup"><span data-stu-id="086e5-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="086e5-121">Quando essa configuração estiver concluída, o SSO Contínuo funcionará da mesma maneira que qualquer outra entrada que use a IWA (Autenticação Integrada do Windows).</span><span class="sxs-lookup"><span data-stu-id="086e5-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="086e5-122">O fluxo é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="086e5-122">The flow is as follows:</span></span>

1. <span data-ttu-id="086e5-123">O usuário tenta acessar um aplicativo (por exemplo, o Outlook Web App – https://outlook.office365.com/owa/) por meio de um dispositivo corporativo ingressado no domínio na sua rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="086e5-123">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="086e5-124">Se o usuário ainda não tiver entrado, ele será redirecionado para a página de entrada do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="086e5-124">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="086e5-125">Se a solicitação de entrada do Azure AD incluir um parâmetro `domain_hint` (identificando o seu locatário, por exemplo, contoso.onmicrosoft.com) ou `login_hint` (identificando o usuário, por exemplo, user@contoso.onmicrosoft.com ou user@contoso.com), a etapa 2 será ignorada.</span><span class="sxs-lookup"><span data-stu-id="086e5-125">If the Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying the user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="086e5-126">O usuário digita o nome de usuário na página de entrada do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="086e5-126">The user types in their user name into the Azure AD sign-in page.</span></span>
4. <span data-ttu-id="086e5-127">Usando JavaScript em segundo plano, o Azure AD desafia o navegador, por meio de uma resposta 401 Não autorizado, para fornecer um tíquete Kerberos.</span><span class="sxs-lookup"><span data-stu-id="086e5-127">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span></span>
5. <span data-ttu-id="086e5-128">O navegador, por sua vez, solicita um tíquete do Active Directory para a conta do computador `AZUREADSSOACCT` (que representa o Azure AD).</span><span class="sxs-lookup"><span data-stu-id="086e5-128">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="086e5-129">O Active Directory localiza a conta do computador e retorna um tíquete Kerberos para o navegador criptografado com o segredo da conta do computador.</span><span class="sxs-lookup"><span data-stu-id="086e5-129">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span></span>
7. <span data-ttu-id="086e5-130">O navegador encaminha o tíquete Kerberos que adquiriu do Active Directory para o Azure AD (em uma das [URLs do Azure AD adicionadas anteriormente às configurações de zona de Intranet do navegador](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="086e5-130">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD (on one of the [Azure AD URLs previously added to the browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="086e5-131">O Azure AD descriptografa o tíquete Kerberos, que inclui a identidade do usuário conectado ao dispositivo corporativo, usando a chave compartilhada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="086e5-131">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span></span>
9. <span data-ttu-id="086e5-132">Após a avaliação, o Azure AD retorna um token ao aplicativo ou solicita que o usuário realize provas adicionais, como a Autenticação Multifator.</span><span class="sxs-lookup"><span data-stu-id="086e5-132">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="086e5-133">Se a entrada do usuário for bem-sucedida, ele será capaz de acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="086e5-133">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="086e5-134">O diagrama a seguir ilustra a todos os componentes e as etapas envolvidas.</span><span class="sxs-lookup"><span data-stu-id="086e5-134">The following diagram illustrates all the components and the steps involved.</span></span>

![Logon Único Contínuo](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="086e5-136">O SSO Contínuo é oportunista, o que significa que, se ele falhar, a experiência de entrada retornará ao comportamento normal, ou seja, o usuário precisará inserir a senha para entrar.</span><span class="sxs-lookup"><span data-stu-id="086e5-136">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="086e5-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="086e5-137">Next steps</span></span>

- <span data-ttu-id="086e5-138">[**Início Rápido** ](active-directory-aadconnect-sso-quick-start.md) – colocar o SSO Contínuo do Azure AD em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="086e5-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="086e5-139">[**Perguntas frequentes**](active-directory-aadconnect-sso-faq.md) – respostas para perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="086e5-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="086e5-140">[**Solução de problemas**](active-directory-aadconnect-troubleshoot-sso.md) – Saiba como resolver problemas comuns do recurso.</span><span class="sxs-lookup"><span data-stu-id="086e5-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="086e5-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="086e5-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
