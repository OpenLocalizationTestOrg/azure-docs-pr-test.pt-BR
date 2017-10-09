---
title: "Azure AD Connect: Autenticação de Passagem – como ela funciona? | Microsoft Docs"
description: "Este artigo descreve como a Autenticação de Passagem do Azure Active Directory funciona."
services: active-directory
keywords: "Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="51e65-105">Autenticação de Passagem do Azure Active Directory: aprofundamento técnico</span><span class="sxs-lookup"><span data-stu-id="51e65-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="51e65-106">A autenticação de passagem do Azure AD está atualmente na versão prévia.</span><span class="sxs-lookup"><span data-stu-id="51e65-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="51e65-107">Como a Autenticação de Passagem do Azure Active Directory funciona?</span><span class="sxs-lookup"><span data-stu-id="51e65-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="51e65-108">Quando um usuário tenta toosign em um aplicativo protegido pelo Azure Active Directory (AD do Azure) e se a autenticação de passagem está habilitada no locatário hello, Olá ocorrem as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="51e65-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="51e65-109">usuário de saudação tenta tooaccess um aplicativo (por exemplo, Olá Outlook Web App - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="51e65-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="51e65-110">Se o usuário Olá não tiver entrado, usuário Olá é redirecionado toohello AD do Azure-página de entrada.</span><span class="sxs-lookup"><span data-stu-id="51e65-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="51e65-111">usuário Olá insere seu nome de usuário e senha na página de entrada do AD do Azure de saudação e clica em botão de "Entrar" hello.</span><span class="sxs-lookup"><span data-stu-id="51e65-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="51e65-112">AD do Azure, durante o recebimento de saudação solicitação de entrada, coloca Olá nome de usuário e senha (criptografada usando uma chave pública) em uma fila.</span><span class="sxs-lookup"><span data-stu-id="51e65-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="51e65-113">Um agente de autenticação de passagem do local faz com que uma fila de toohello de chamada de saída e recupera Olá nome de usuário e a senha criptografada.</span><span class="sxs-lookup"><span data-stu-id="51e65-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="51e65-114">Agente de saudação descriptografa senha hello usando sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="51e65-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="51e65-115">Agente de Hello, em seguida, valida a saudação de nome de usuário e senha no Active Directory usando APIs padrão do Windows (um toowhat mecanismo semelhante é usado pelos serviços de Federação do Active Directory).</span><span class="sxs-lookup"><span data-stu-id="51e65-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="51e65-116">Olá nome de usuário pode ser qualquer nome de usuário Olá no local padrão (geralmente `userPrincipalName`) ou outro atributo configurado no Azure AD Connect (conhecido como `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="51e65-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="51e65-117">Olá Active Directory Domain Controller (DC) local, em seguida, avalia Olá solicitação e retorna Olá resposta apropriada (êxito, falha, a senha expirou ou usuário bloqueado) toohello agente.</span><span class="sxs-lookup"><span data-stu-id="51e65-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="51e65-118">Agente de Hello, por sua vez, retorna esse tooAzure voltar de resposta AD.</span><span class="sxs-lookup"><span data-stu-id="51e65-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="51e65-119">AD do Azure avalia resposta hello e responde toohello usuário conforme apropriado - por exemplo, ele entra usuário Olá imediatamente ou solicitações de autenticação multifator (MFA).</span><span class="sxs-lookup"><span data-stu-id="51e65-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="51e65-120">Se Olá usuário entrar for bem-sucedida, o usuário de saudação é tooaccess capaz de aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="51e65-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="51e65-121">Olá diagrama a seguir ilustra todos os componentes de saudação e etapas de saudação envolvidos.</span><span class="sxs-lookup"><span data-stu-id="51e65-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Autenticação de Passagem](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="51e65-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51e65-123">Next steps</span></span>
- <span data-ttu-id="51e65-124">[**Limitações atuais**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) – esse recurso está na versão prévia no momento.</span><span class="sxs-lookup"><span data-stu-id="51e65-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="51e65-125">Saiba quais cenários têm suporte e quais não têm.</span><span class="sxs-lookup"><span data-stu-id="51e65-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="51e65-126">[**Início rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md) – instale e execute a autenticação de passagem do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51e65-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="51e65-127">[**Perguntas frequentes sobre** ](active-directory-aadconnect-pass-through-authentication-faq.md) -respostas toofrequently perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="51e65-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="51e65-128">[**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Saiba como tooresolve comum problemas com o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="51e65-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="51e65-129">[**SSO contínuo do Azure AD**](active-directory-aadconnect-sso.md) – Saiba mais sobre esse recurso complementar.</span><span class="sxs-lookup"><span data-stu-id="51e65-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="51e65-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="51e65-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
