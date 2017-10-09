---
title: "página aaaApplication não será exibido corretamente para um aplicativo de Proxy de aplicativo | Microsoft Docs"
description: "Diretrizes de quando a página de saudação não estiver exibindo corretamente em um aplicativo de Proxy de aplicativo integrado com o Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="9d86f-103">Página de aplicativo não exibe corretamente para um aplicativo de Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="9d86f-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="9d86f-104">Este artigo ajuda tootroubleshoot problemas com aplicativos de Proxy de aplicativo do Azure Active Directory quando você navegar toohello página, mas algo na página de saudação não parece estar correto.</span><span class="sxs-lookup"><span data-stu-id="9d86f-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="9d86f-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9d86f-105">Overview</span></span>
<span data-ttu-id="9d86f-106">Quando você publica um aplicativo de Proxy de aplicativo, somente as páginas em sua raiz são acessíveis ao acessar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9d86f-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="9d86f-107">Se a página de saudação não estiver exibindo corretamente, Olá raiz URL interna usada para o aplicativo hello pode estar faltando alguns recursos da página.</span><span class="sxs-lookup"><span data-stu-id="9d86f-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="9d86f-108">tooresolve, verifique se você publicou *todos os* Olá recursos para página hello como parte do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9d86f-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="9d86f-109">Você pode verificar esse é o problema de saudação abrindo o controlador de rede (como o Fiddler ou F12 ferramentas no Internet Explorer/borda), carregar página hello e procurando 404 erros.</span><span class="sxs-lookup"><span data-stu-id="9d86f-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="9d86f-110">Que indica as páginas de saudação que atualmente não podem ser encontradas e talvez ainda precise toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="9d86f-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="9d86f-111">Como um exemplo de nesse caso, suponha que você tenha publicado um aplicativo de despesas usando uma URL interna de <http://myapps/expenses>, mas usa o aplicativo hello folha de estilos de saudação <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="9d86f-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="9d86f-112">Nesse caso, Olá folha de estilos não está publicada no seu aplicativo, para carregar o aplicativo de despesas Olá lançar um erro 404 ao tentar tooload Style. CSS.</span><span class="sxs-lookup"><span data-stu-id="9d86f-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="9d86f-113">Neste exemplo, o problema de Olá deve ser resolvido publicando o aplicativo hello com uma URL interna de <http://myapp/> em vez disso.</span><span class="sxs-lookup"><span data-stu-id="9d86f-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="9d86f-114">Problemas com a publicação como um aplicativo</span><span class="sxs-lookup"><span data-stu-id="9d86f-114">Problems with publishing as one application</span></span>

<span data-ttu-id="9d86f-115">Se não for possível toopublish Olá a todos os recursos no mesmo aplicativo, você precisa toopublish vários aplicativos e habilitar links entre eles.</span><span class="sxs-lookup"><span data-stu-id="9d86f-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="9d86f-116">toodo assim, recomendamos o uso de saudação [domínios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solução.</span><span class="sxs-lookup"><span data-stu-id="9d86f-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="9d86f-117">No entanto, essa solução requer que você possui o certificado de saudação para seu domínio e seus aplicativos usam nomes de domínio totalmente qualificados (FQDNs).</span><span class="sxs-lookup"><span data-stu-id="9d86f-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="9d86f-118">Para outras opções, consulte Olá [solucionar problemas de links desfeitos documentação](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="9d86f-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d86f-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d86f-119">Next steps</span></span>
[<span data-ttu-id="9d86f-120">Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9d86f-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
