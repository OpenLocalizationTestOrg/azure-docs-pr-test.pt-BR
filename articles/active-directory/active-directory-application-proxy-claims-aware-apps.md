---
title: "Aplicativos com reconhecimento de declarações - Proxy de aplicativo do Azure AD | Microsoft Docs"
description: "Como publicar aplicativos ASP.NET locais que aceitam declarações do ADFS para acesso remoto seguro por seus usuários."
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
ms.openlocfilehash: 5784222608b01509fc4ff84b1a8792cbcfea89e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="27106-103">Trabalho com aplicativos com reconhecimento de declarações no Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="27106-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="27106-104">Os [aplicativos com reconhecimento de declarações](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) executam um redirecionamento para o STS (Serviço de Token de Segurança).</span><span class="sxs-lookup"><span data-stu-id="27106-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="27106-105">O STS solicita as credenciais do usuário em troca de um token e, em seguida, redireciona o usuário para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27106-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="27106-106">Há algumas maneiras de habilitar o Proxy de Aplicativo para que ele funcione com esses redirecionamentos.</span><span class="sxs-lookup"><span data-stu-id="27106-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="27106-107">Use este artigo para configurar sua implantação de aplicativos com reconhecimento de declarações.</span><span class="sxs-lookup"><span data-stu-id="27106-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="27106-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="27106-108">Prerequisites</span></span>
<span data-ttu-id="27106-109">Certifique-se de que o STS para o qual o aplicativo com reconhecimento de declarações seja redirecionado está disponível fora da sua rede local.</span><span class="sxs-lookup"><span data-stu-id="27106-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="27106-110">Você pode disponibilizar o STS, expondo-o por meio de um proxy ou permitindo conexões externas.</span><span class="sxs-lookup"><span data-stu-id="27106-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="27106-111">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="27106-111">Publish your application</span></span>

1. <span data-ttu-id="27106-112">Publique seu aplicativo seguindo as instruções descritas em [Publicar aplicativos com o Proxy de Aplicativo](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="27106-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="27106-113">Navegue até a página de aplicativo no portal e selecione **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="27106-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="27106-114">Se você tiver escolhido **Azure Active Directory** como seu **Método de Pré-autenticação**, selecione **Logon único do Azure AD desabilitado** como seu **Método de Autenticação Interno**.</span><span class="sxs-lookup"><span data-stu-id="27106-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="27106-115">Se você tiver escolhido **Passagem** como seu **método de pré-autenticação**, não precisará alterar nada.</span><span class="sxs-lookup"><span data-stu-id="27106-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="27106-116">Configurar o ADFS</span><span class="sxs-lookup"><span data-stu-id="27106-116">Configure ADFS</span></span>

<span data-ttu-id="27106-117">Você pode configurar o ADFS para aplicativos com reconhecimento de declarações de uma de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="27106-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="27106-118">A primeira é por meio de domínios personalizados.</span><span class="sxs-lookup"><span data-stu-id="27106-118">The first is by using custom domains.</span></span> <span data-ttu-id="27106-119">A segunda é com a especificação Web Services Federation.</span><span class="sxs-lookup"><span data-stu-id="27106-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="27106-120">Opção 1: Domínios personalizados</span><span class="sxs-lookup"><span data-stu-id="27106-120">Option 1: Custom domains</span></span>

<span data-ttu-id="27106-121">Se todas as URLs internas para seus aplicativos forem nomes de domínio totalmente qualificados (FQDNs), você poderá configurar [domínios personalizados](active-directory-application-proxy-custom-domains.md) para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="27106-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="27106-122">Use os domínios personalizados para criar URLs externas que são iguais às URLs internas.</span><span class="sxs-lookup"><span data-stu-id="27106-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="27106-123">Quando suas URLs externas corresponderem às URLs internas, os redirecionamentos de STS funcionarão se os usuários estiverem no local ou remotos.</span><span class="sxs-lookup"><span data-stu-id="27106-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="27106-124">Opção 2: especificação Web Services Federation</span><span class="sxs-lookup"><span data-stu-id="27106-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="27106-125">Abra o Gerenciamento de ADFS.</span><span class="sxs-lookup"><span data-stu-id="27106-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="27106-126">Acesse **Terceiras Partes Confiáveis**, clique com o botão direito do mouse no aplicativo que você está publicando com o Proxy de Aplicativo e escolha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="27106-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Confianças em Terceiras Partes Confiáveis, clique com o botão direito do mouse no nome do aplicativo - captura de tela](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="27106-128">Na guia **Pontos de Extremidade**, em **Tipo de ponto de extremidade**, selecione **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="27106-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="27106-129">Em **URL Confiável**, insira a URL fornecida no Proxy de Aplicativo em **URL Externa** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27106-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Adicionar um ponto de extremidade - definir valor de URL Confiável - captura de tela](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="27106-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27106-131">Next steps</span></span>
* <span data-ttu-id="27106-132">[Habilitar logon único](application-proxy-sso-overview.md) para aplicativos sem reconhecimento de declarações</span><span class="sxs-lookup"><span data-stu-id="27106-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="27106-133">Habilitar aplicativos clientes nativos para interagir com aplicativos de proxy</span><span class="sxs-lookup"><span data-stu-id="27106-133">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


