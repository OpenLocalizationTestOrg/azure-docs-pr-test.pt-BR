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
ms.openlocfilehash: d34ccd40082edbe036d963ad548bff648119bdd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="d67c4-105">Autenticação de Passagem do Azure Active Directory: aprofundamento técnico</span><span class="sxs-lookup"><span data-stu-id="d67c4-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="d67c4-106">A autenticação de passagem do Azure AD está atualmente na versão prévia.</span><span class="sxs-lookup"><span data-stu-id="d67c4-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="d67c4-107">Como a Autenticação de Passagem do Azure Active Directory funciona?</span><span class="sxs-lookup"><span data-stu-id="d67c4-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="d67c4-108">Quando um usuário tenta entrar em um aplicativo protegido pelo Azure AD (Azure Active Directory) e se a Autenticação de Passagem está habilitada no locatário, ocorrem as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d67c4-108">When a user attempts to sign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on the tenant, the following steps occur:</span></span>

1. <span data-ttu-id="d67c4-109">O usuário tenta acessar um aplicativo (por exemplo, o Outlook Web App – https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="d67c4-109">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="d67c4-110">Se o usuário ainda não tiver entrado, ele será redirecionado para a página de entrada do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d67c4-110">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>
3. <span data-ttu-id="d67c4-111">O usuário insere o nome de usuário e a senha na página de entrada do Azure AD e clica no botão "Entrar".</span><span class="sxs-lookup"><span data-stu-id="d67c4-111">The user enters their username and password into the Azure AD sign-in page and clicks the "Sign in" button.</span></span>
4. <span data-ttu-id="d67c4-112">O Azure AD, ao receber a solicitação de entrada, coloca o nome de usuário e a senha (criptografada com o uso de uma chave pública) em uma fila.</span><span class="sxs-lookup"><span data-stu-id="d67c4-112">Azure AD, on receiving the sign-in request, places the username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="d67c4-113">Um agente de Autenticação de Passagem local faz uma chamada de saída à fila e recupera o nome de usuário e a senha criptografada.</span><span class="sxs-lookup"><span data-stu-id="d67c4-113">An on-premises Pass-through Authentication agent makes an outbound call to the queue and retrieves the username and encrypted password.</span></span>
6. <span data-ttu-id="d67c4-114">O agente descriptografa a senha usando sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="d67c4-114">The agent decrypts the password using its private key.</span></span>
7. <span data-ttu-id="d67c4-115">Em seguida, o agente valida o nome de usuário e a senha no Active Directory usando APIs padrão do Windows (um mecanismo semelhante ao que é usado pelos Serviços de Federação do Active Directory (AD FS)).</span><span class="sxs-lookup"><span data-stu-id="d67c4-115">The agent then validates the username and password against Active Directory using standard Windows APIs (a similar mechanism to what is used by Active Directory Federation Services).</span></span> <span data-ttu-id="d67c4-116">O nome de usuário pode ser o nome de usuário local padrão (normalmente `userPrincipalName`) ou outro atributo configurado no Azure AD Connect (também conhecido como `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="d67c4-116">The username can be either the on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="d67c4-117">Em seguida, o DC (Controlador de Domínio) do Active Directory local avalia a solicitação e retorna a resposta apropriada (êxito, falha, senha expirada ou usuário bloqueado) para o agente.</span><span class="sxs-lookup"><span data-stu-id="d67c4-117">The on-premises Active Directory Domain Controller (DC) then evaluates the request and returns the appropriate response (success, failure, password expired or user locked out) to the agent.</span></span>
9. <span data-ttu-id="d67c4-118">O agente, por sua vez, envia essa resposta de volta ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d67c4-118">The agent, in turn, returns this response back to Azure AD.</span></span>
10. <span data-ttu-id="d67c4-119">O Azure AD avalia a resposta e responde ao usuário conforme apropriado – por exemplo, ele conecta o usuário imediatamente ou solicita a MFA (Autenticação Multifator).</span><span class="sxs-lookup"><span data-stu-id="d67c4-119">Azure AD evaluates the response and responds to the user as appropriate - for example, it either signs the user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="d67c4-120">Se a entrada do usuário for bem-sucedida, ele será capaz de acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d67c4-120">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="d67c4-121">O diagrama a seguir ilustra a todos os componentes e as etapas envolvidas.</span><span class="sxs-lookup"><span data-stu-id="d67c4-121">The following diagram illustrates all the components and the steps involved.</span></span>

![Autenticação de Passagem](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="d67c4-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d67c4-123">Next steps</span></span>
- <span data-ttu-id="d67c4-124">[**Limitações atuais**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) – esse recurso está na versão prévia no momento.</span><span class="sxs-lookup"><span data-stu-id="d67c4-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="d67c4-125">Saiba quais cenários têm suporte e quais não têm.</span><span class="sxs-lookup"><span data-stu-id="d67c4-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="d67c4-126">[**Início rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md) – instale e execute a autenticação de passagem do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d67c4-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="d67c4-127">[**Perguntas frequentes**](active-directory-aadconnect-pass-through-authentication-faq.md) – respostas para perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="d67c4-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="d67c4-128">[**Solução de problemas**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) – Saiba como resolver problemas comuns do recurso.</span><span class="sxs-lookup"><span data-stu-id="d67c4-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="d67c4-129">[**SSO contínuo do Azure AD**](active-directory-aadconnect-sso.md) – Saiba mais sobre esse recurso complementar.</span><span class="sxs-lookup"><span data-stu-id="d67c4-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="d67c4-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="d67c4-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
