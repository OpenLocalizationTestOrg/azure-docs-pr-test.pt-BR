---
title: "Página de aplicativo não exibe corretamente para um aplicativo de Proxy de aplicativo | Microsoft Docs"
description: "Diretrizes quando a página não está sendo exibida corretamente em um Aplicativo de Proxy de Aplicativo que você integrou com o Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: cac4c333e59ef9a0f28a2f93a7afee22eeafd54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="999de-103">Página de aplicativo não exibe corretamente para um aplicativo de Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="999de-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="999de-104">Este artigo irá ajudá-lo a solucionar problemas com aplicativos de Proxy de Aplicativo do Azure Active Directory quando você navegar para a página, mas algo na página não parece correto.</span><span class="sxs-lookup"><span data-stu-id="999de-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="999de-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="999de-105">Overview</span></span>
<span data-ttu-id="999de-106">Quando você publica um aplicativo de Proxy de aplicativo, apenas as páginas em sua raiz são acessíveis ao acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="999de-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="999de-107">Se a página não estiver exibindo corretamente, a URL interna raiz usada para o aplicativo pode estar em falta de alguns recursos de página.</span><span class="sxs-lookup"><span data-stu-id="999de-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="999de-108">Para resolver, certifique-se de ter publicado *todos* os recursos da página como parte do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="999de-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="999de-109">Você pode verificar se esse é o problema, abrindo o rastreador de rede (como o Fiddler ou ferramentas F12 no Internet Explorer/Edge), carregando a página e procurando por erros 404.</span><span class="sxs-lookup"><span data-stu-id="999de-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="999de-110">Esses indicam as páginas que atualmente não podem ser encontradas e ainda podem ser publicadas.</span><span class="sxs-lookup"><span data-stu-id="999de-110">That indicates the pages that currently cannot be found and may still need to be published.</span></span>

<span data-ttu-id="999de-111">Como um exemplo desse caso, suponha que você tenha publicado um aplicativo de despesas usando uma URL interna de <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="999de-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="999de-112">Nesse caso, a folha de estilo não é publicada em seu aplicativo, portanto, carregar o aplicativo de despesas gera um erro 404 ao tentar carregar style.css.</span><span class="sxs-lookup"><span data-stu-id="999de-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="999de-113">Nesse exemplo, o problema é resolvido ao publicar o aplicativo com uma URL interna de <http://myapp/>.</span><span class="sxs-lookup"><span data-stu-id="999de-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="999de-114">Problemas com a publicação como um aplicativo</span><span class="sxs-lookup"><span data-stu-id="999de-114">Problems with publishing as one application</span></span>

<span data-ttu-id="999de-115">Se não for possível publicar todos os recursos dentro do mesmo aplicativo, será necessário publicar vários aplicativos e habilitar links entre eles.</span><span class="sxs-lookup"><span data-stu-id="999de-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="999de-116">Para fazer isso, é recomendável usar a solução de [domínios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="999de-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="999de-117">No entanto, essa solução requer que você tenha o certificado para seu domínio e que seus aplicativos usem nomes de domínio totalmente qualificados (FQDNs).</span><span class="sxs-lookup"><span data-stu-id="999de-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="999de-118">Para outras opções, consulte a [documentação solucionar problemas de links desfeitos](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="999de-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="999de-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="999de-119">Next steps</span></span>
[<span data-ttu-id="999de-120">Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="999de-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
