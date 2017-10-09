---
title: aaaSingle logon tooapps com Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Ative logon único para seus aplicativos publicados no local com o Proxy de aplicativo do Azure AD em Olá portal do Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="f6fe9-103">Compartimentação de senhas para logon único com o Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="f6fe9-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="f6fe9-104">O Proxy de Aplicativo do Azure Active Directory o ajuda a aprimorar a produtividade ao publicar aplicativos locais de forma que funcionários remotos também possam acessá-los com segurança.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="f6fe9-105">Em Olá portal do Azure, você também pode configurar único (SSO) toothese aplicativos de logon.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-105">In hello Azure portal, you can also set up single sign-on (SSO) toothese apps.</span></span> <span data-ttu-id="f6fe9-106">Os usuários só precisam tooauthenticate com o Azure AD e eles podem acessar seu aplicativo empresarial sem ter toosign novamente.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-106">Your users only need tooauthenticate with Azure AD, and they can access your enterprise application without having toosign in again.</span></span>

<span data-ttu-id="f6fe9-107">O Proxy de Aplicativo dá suporte a vários [modos de logon único](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6fe9-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="f6fe9-108">O logon único baseado em senha destina-se a aplicativos que usam uma combinação de nome de usuário e senha para autenticação.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="f6fe9-109">Quando você configura com base em senha de logon para o seu aplicativo, seus usuários têm toosign no aplicativo do local toohello uma vez.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-109">When you configure password-based sign-on for your application, your users have toosign in toohello on-premises application once.</span></span> <span data-ttu-id="f6fe9-110">Depois disso, o Active Directory do Azure armazena informações de entrada hello e automaticamente fornece toohello aplicativo quando os usuários acessam remotamente.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-110">After that, Azure Active Directory stores hello sign-in information and automatically provides it toohello application when your users access it remotely.</span></span> 

<span data-ttu-id="f6fe9-111">Você já deve ter publicado e testado seu aplicativo com o Proxy de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="f6fe9-112">Se não, siga as etapas de saudação em [publicar aplicativos usando o Proxy de aplicativo do Azure AD](application-proxy-publish-azure-portal.md) , em seguida, volte aqui.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-112">If not, follow hello steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="f6fe9-113">Definir o cofre de senha para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f6fe9-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="f6fe9-114">Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-114">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="f6fe9-115">Selecione **Azure Active Directory** > **Aplicativos Empresariais** > **Todos os Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="f6fe9-116">Na lista de saudação, selecione o aplicativo hello que você deseja tooset backup com o SSO.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-116">From hello list, select hello app that you want tooset up with SSO.</span></span>  
4. <span data-ttu-id="f6fe9-117">Selecione **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-117">Select **Single sign-on**.</span></span>

   ![Selecione Logon único](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="f6fe9-119">Para o modo SSO hello, escolha **baseada em senha logon**.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-119">For hello SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="f6fe9-120">Para Olá URL de logon, insira Olá URL para página Olá onde os usuários digitarão seu nome de usuário e senha toosign no aplicativo tooyour fora da rede corporativa hello.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-120">For hello Sign-on URL, enter hello URL for hello page where users enter their username and password toosign in tooyour app outside of hello corporate network.</span></span> <span data-ttu-id="f6fe9-121">Isso pode ser Olá URL externa que você criou quando você publicou o aplicativo hello por meio do Proxy de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-121">This may be hello External URL that you created when you published hello app through Application Proxy.</span></span> 

   ![Escolha Logon Único Baseado em Senha e digite a URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="f6fe9-123">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-123">Select **Save**.</span></span>

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="f6fe9-124">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f6fe9-124">Test your app</span></span>

<span data-ttu-id="f6fe9-125">Vá tooexternal URL que você configurou para acesso remoto tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-125">Go tooexternal URL that you configured for remote access tooyour application.</span></span> <span data-ttu-id="f6fe9-126">Entre com suas credenciais para esse aplicativo (ou credenciais Olá para uma conta de teste que você configurou com acesso).</span><span class="sxs-lookup"><span data-stu-id="f6fe9-126">Sign in with your credentials for that app (or hello credentials for a test account that you set up with access).</span></span> <span data-ttu-id="f6fe9-127">Depois que você entrar com êxito, você deve ser capaz de tooleave Olá aplicativo e voltar sem inserir suas credenciais novamente.</span><span class="sxs-lookup"><span data-stu-id="f6fe9-127">Once you sign in successfully, you should be able tooleave hello app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f6fe9-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6fe9-128">Next steps</span></span>

- <span data-ttu-id="f6fe9-129">Leia sobre outra maneiras tooimplement [logon único com o Proxy de aplicativo](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f6fe9-129">Read about other ways tooimplement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="f6fe9-130">Saiba mais sobre [Considerações de segurança para acessar aplicativos remotamente com o Proxy de Aplicativo do Azure AD](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="f6fe9-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>