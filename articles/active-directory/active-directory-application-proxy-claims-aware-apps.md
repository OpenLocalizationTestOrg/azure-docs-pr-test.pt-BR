---
title: aplicativos com reconhecimento de aaaClaims - Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Como toopublish local aplicativos ASP.NET que aceitam declarações do ADFS para acesso remoto seguro pelos usuários."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="b7455-103">Trabalho com aplicativos com reconhecimento de declarações no Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b7455-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="b7455-104">[Aplicativos com reconhecimento de declarações](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) executar um serviço de Token de segurança (STS) de toohello de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="b7455-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="b7455-105">Olá STS solicita as credenciais do usuário de saudação em troca de um token e, em seguida, redireciona o aplicativo de toohello usuário hello.</span><span class="sxs-lookup"><span data-stu-id="b7455-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="b7455-106">Há algumas maneiras tooenable Proxy de aplicativo toowork com esses redirecionamentos.</span><span class="sxs-lookup"><span data-stu-id="b7455-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="b7455-107">Use este artigo tooconfigure sua implantação para aplicativos com reconhecimento de declarações.</span><span class="sxs-lookup"><span data-stu-id="b7455-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b7455-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b7455-108">Prerequisites</span></span>
<span data-ttu-id="b7455-109">Certifique-se de que Olá STS que Olá aplicativo com reconhecimento de declarações redireciona toois disponível fora de sua rede local.</span><span class="sxs-lookup"><span data-stu-id="b7455-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="b7455-110">Você pode disponibilizar Olá STS, expondo-lo por meio de um proxy ou permitindo fora de conexões.</span><span class="sxs-lookup"><span data-stu-id="b7455-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="b7455-111">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b7455-111">Publish your application</span></span>

1. <span data-ttu-id="b7455-112">Publicar seu aplicativo de acordo com as instruções de toohello descritas em [publicar aplicativos com Proxy de aplicativo](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b7455-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="b7455-113">Navegue toohello página de aplicativo no hello portal e selecione **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b7455-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="b7455-114">Se você tiver escolhido **Azure Active Directory** como seu **Método de Pré-autenticação**, selecione **Logon único do Azure AD desabilitado** como seu **Método de Autenticação Interno**.</span><span class="sxs-lookup"><span data-stu-id="b7455-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="b7455-115">Se você escolheu **passagem** como seu **método de pré-autenticação**, você não precisa toochange nada.</span><span class="sxs-lookup"><span data-stu-id="b7455-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="b7455-116">Configurar o ADFS</span><span class="sxs-lookup"><span data-stu-id="b7455-116">Configure ADFS</span></span>

<span data-ttu-id="b7455-117">Você pode configurar o ADFS para aplicativos com reconhecimento de declarações de uma de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="b7455-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="b7455-118">Olá primeiro é usar domínios personalizados.</span><span class="sxs-lookup"><span data-stu-id="b7455-118">hello first is by using custom domains.</span></span> <span data-ttu-id="b7455-119">Olá segundo é com o WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="b7455-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="b7455-120">Opção 1: Domínios personalizados</span><span class="sxs-lookup"><span data-stu-id="b7455-120">Option 1: Custom domains</span></span>

<span data-ttu-id="b7455-121">Se todos Olá URLs internas para seus aplicativos são totalmente qualificados (FQDNs) de nomes de domínio, você pode configurar [domínios personalizados](active-directory-application-proxy-custom-domains.md) para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b7455-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="b7455-122">Use Olá domínios personalizados toocreate URLs externas que são Olá mesmo Olá URLs internas.</span><span class="sxs-lookup"><span data-stu-id="b7455-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="b7455-123">Quando suas URLs externas correspondem as URLs internas, redirecionamentos de STS Olá funcionam se os usuários estão no local ou remoto.</span><span class="sxs-lookup"><span data-stu-id="b7455-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="b7455-124">Opção 2: especificação Web Services Federation</span><span class="sxs-lookup"><span data-stu-id="b7455-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="b7455-125">Abra o Gerenciamento de ADFS.</span><span class="sxs-lookup"><span data-stu-id="b7455-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="b7455-126">Vá muito**terceira parte confiável**, clique no aplicativo hello está sendo publicado com Proxy de aplicativo e escolha **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b7455-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Confianças em Terceiras Partes Confiáveis, clique com o botão direito do mouse no nome do aplicativo - captura de tela](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="b7455-128">Em Olá **pontos de extremidade** guia em **tipo de ponto de extremidade**, selecione **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="b7455-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="b7455-129">Em **confiável URL**, digite Olá URL inserida em Olá Proxy de aplicativo em **URL externa** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b7455-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Adicionar um ponto de extremidade - definir valor de URL Confiável - captura de tela](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="b7455-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7455-131">Next steps</span></span>
* <span data-ttu-id="b7455-132">[Habilitar logon único](application-proxy-sso-overview.md) para aplicativos sem reconhecimento de declarações</span><span class="sxs-lookup"><span data-stu-id="b7455-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="b7455-133">Habilitar toointeract de aplicativos cliente nativo com aplicativos de proxy</span><span class="sxs-lookup"><span data-stu-id="b7455-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


