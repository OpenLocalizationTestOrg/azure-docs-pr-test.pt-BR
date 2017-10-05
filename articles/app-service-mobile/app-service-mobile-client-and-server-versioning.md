---
title: "Controle de versão de cliente e servidor SDK em Aplicativos Móveis e Serviços Móveis | Microsoft Docs"
description: "Lista dos SDKs clientes e compatibilidade com versões do SDK do servidor para os Serviços Móveis e Aplicativos Móveis do Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: f79e819b1547f81498ea213858faf3c75e374782
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="0ca11-103">Controle de versão de cliente e servidor em Aplicativos Móveis e Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="0ca11-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="0ca11-104">A versão mais recente dos Serviços Móveis do Azure é o recurso **Aplicativos Móveis** do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ca11-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="0ca11-105">Os SDKs de cliente e servidor de Aplicativos Móveis são baseados originalmente nos Serviços Móveis, mas *não* são compatíveis entre si.</span><span class="sxs-lookup"><span data-stu-id="0ca11-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="0ca11-106">Ou seja, você deve usar um SDK de cliente de *Aplicativos Móveis* com SDK de servidor de *Aplicativos Móveis* e da mesma forma para *Serviços Móveis*.</span><span class="sxs-lookup"><span data-stu-id="0ca11-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="0ca11-107">Esse contrato é imposto por meio de um valor de cabeçalho especial usado pelos SDKs de cliente e servidor, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="0ca11-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="0ca11-108">Observação: sempre que este documento se refere a um back-end de *Serviços Móveis* , ele não necessariamente precisa estar hospedados nos Serviços Móveis.</span><span class="sxs-lookup"><span data-stu-id="0ca11-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span></span> <span data-ttu-id="0ca11-109">Agora é possível migrar um serviço móvel para ser executado em um Serviço de Aplicativo sem qualquer alteração de código, mas o serviço ainda estaria usando versões de SDK de *Serviços Móveis*.</span><span class="sxs-lookup"><span data-stu-id="0ca11-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="0ca11-110">Para saber mais sobre a migração para o Serviço de Aplicativo sem qualquer alteração de código, consulte o artigo [Migrar um Serviço Móvel para o Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="0ca11-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="0ca11-111">Especificação de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="0ca11-111">Header specification</span></span>
<span data-ttu-id="0ca11-112">A chave `ZUMO-API-VERSION` pode ser especificada no cabeçalho HTTP ou na cadeia de consulta.</span><span class="sxs-lookup"><span data-stu-id="0ca11-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span></span> <span data-ttu-id="0ca11-113">O valor é uma cadeia de caracteres de versão no formulário **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="0ca11-113">The value is a version string in the form **x.y.z**.</span></span>

<span data-ttu-id="0ca11-114">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ca11-114">For example:</span></span>

<span data-ttu-id="0ca11-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="0ca11-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="0ca11-116">CABEÇALHOS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="0ca11-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="0ca11-118">Recusando a verificação de versão</span><span class="sxs-lookup"><span data-stu-id="0ca11-118">Opting out of version checking</span></span>
<span data-ttu-id="0ca11-119">Você pode recusar a verificação de versão definindo um valor **verdadeiro** para a configuração do aplicativo **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="0ca11-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="0ca11-120">Especifique isso no seu web.config ou na seção Configurações do Aplicativo do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ca11-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0ca11-121">Há algumas alterações de comportamento entre os Serviços Móveis e os Aplicativos Móveis, especialmente nas áreas de sincronização offline, autenticação e notificações por push.</span><span class="sxs-lookup"><span data-stu-id="0ca11-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="0ca11-122">Você deve recusar verificação somente após o teste completo para garantir que essas alterações de comportamento não interrompam a funcionalidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ca11-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="0ca11-123">Resumo de compatibilidade para todas as versões</span><span class="sxs-lookup"><span data-stu-id="0ca11-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="0ca11-124">A tabela abaixo mostra a compatibilidade entre todos os tipos de cliente e de servidor.</span><span class="sxs-lookup"><span data-stu-id="0ca11-124">The chart below shows the compatibility between all client and server types.</span></span> <span data-ttu-id="0ca11-125">Um back-end é classificado como **Serviços** Móveis ou **Aplicativos** Móveis com base no SDK de servidor que ele usa.</span><span class="sxs-lookup"><span data-stu-id="0ca11-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span></span>

|  | <span data-ttu-id="0ca11-126">**Serviços Móveis** </span><span class="sxs-lookup"><span data-stu-id="0ca11-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="0ca11-127">**Aplicativos Móveis** </span><span class="sxs-lookup"><span data-stu-id="0ca11-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ca11-128">[Clientes de Serviços Móveis]</span><span class="sxs-lookup"><span data-stu-id="0ca11-128">[Mobile Services clients]</span></span> |<span data-ttu-id="0ca11-129">OK</span><span class="sxs-lookup"><span data-stu-id="0ca11-129">Ok</span></span> |<span data-ttu-id="0ca11-130">Erro\*</span><span class="sxs-lookup"><span data-stu-id="0ca11-130">Error\*</span></span> |
| <span data-ttu-id="0ca11-131">[Clientes de Aplicativos Móveis]</span><span class="sxs-lookup"><span data-stu-id="0ca11-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="0ca11-132">Erro\*</span><span class="sxs-lookup"><span data-stu-id="0ca11-132">Error\*</span></span> |<span data-ttu-id="0ca11-133">OK</span><span class="sxs-lookup"><span data-stu-id="0ca11-133">Ok</span></span> |

<span data-ttu-id="0ca11-134">\*Isso pode ser controlado especificando**MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="0ca11-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="0ca11-135"><a name="1.0.0"></a>Servidor e cliente de Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="0ca11-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="0ca11-136">Os SDKs de cliente na tabela a seguir são compatíveis com **Serviços Móveis**.</span><span class="sxs-lookup"><span data-stu-id="0ca11-136">The client SDKs in the table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="0ca11-137">Observação: os SDKs do cliente dos Serviços Móveis *não* enviam um valor de cabeçalho para `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="0ca11-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="0ca11-138">Se o serviço receber esse cabeçalho ou o valor de cadeia de consulta, um erro será retornado, a menos que você tenha recusado expressamente conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="0ca11-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="0ca11-139"><a name="MobileServicesClients"></a> SDKs de clientes de *Serviços* Móveis</span><span class="sxs-lookup"><span data-stu-id="0ca11-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="0ca11-140">Plataforma cliente</span><span class="sxs-lookup"><span data-stu-id="0ca11-140">Client platform</span></span> | <span data-ttu-id="0ca11-141">Versão</span><span class="sxs-lookup"><span data-stu-id="0ca11-141">Version</span></span> | <span data-ttu-id="0ca11-142">Valor de cabeçalho de versão</span><span class="sxs-lookup"><span data-stu-id="0ca11-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ca11-143">Cliente gerenciado (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="0ca11-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="0ca11-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="0ca11-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="0ca11-145">n/d</span><span class="sxs-lookup"><span data-stu-id="0ca11-145">n/a</span></span> |
| <span data-ttu-id="0ca11-146">iOS</span><span class="sxs-lookup"><span data-stu-id="0ca11-146">iOS</span></span> |[<span data-ttu-id="0ca11-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="0ca11-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="0ca11-148">n/d</span><span class="sxs-lookup"><span data-stu-id="0ca11-148">n/a</span></span> |
| <span data-ttu-id="0ca11-149">Android</span><span class="sxs-lookup"><span data-stu-id="0ca11-149">Android</span></span> |[<span data-ttu-id="0ca11-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="0ca11-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="0ca11-151">n/d</span><span class="sxs-lookup"><span data-stu-id="0ca11-151">n/a</span></span> |
| <span data-ttu-id="0ca11-152">HTML</span><span class="sxs-lookup"><span data-stu-id="0ca11-152">HTML</span></span> |[<span data-ttu-id="0ca11-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="0ca11-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="0ca11-154">n/d</span><span class="sxs-lookup"><span data-stu-id="0ca11-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="0ca11-155">SDKs de servidor de *Serviços* Móveis</span><span class="sxs-lookup"><span data-stu-id="0ca11-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="0ca11-156">Plataforma servidor</span><span class="sxs-lookup"><span data-stu-id="0ca11-156">Server platform</span></span> | <span data-ttu-id="0ca11-157">Versão</span><span class="sxs-lookup"><span data-stu-id="0ca11-157">Version</span></span> | <span data-ttu-id="0ca11-158">Cabeçalho de versão aceito</span><span class="sxs-lookup"><span data-stu-id="0ca11-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ca11-159">.NET</span><span class="sxs-lookup"><span data-stu-id="0ca11-159">.NET</span></span> |[<span data-ttu-id="0ca11-160">WindowsAzure.MobileServices.Backend.* versão 1.0. x</span><span class="sxs-lookup"><span data-stu-id="0ca11-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="0ca11-161">* * Nenhum cabeçalho de versão * *</span><span class="sxs-lookup"><span data-stu-id="0ca11-161">**No version header **</span></span> |
| <span data-ttu-id="0ca11-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="0ca11-162">Node.js</span></span> |<span data-ttu-id="0ca11-163">(em breve)</span><span class="sxs-lookup"><span data-stu-id="0ca11-163">(coming soon)</span></span> |<span data-ttu-id="0ca11-164">**Nenhum cabeçalho de versão**</span><span class="sxs-lookup"><span data-stu-id="0ca11-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="0ca11-165">Comportamento dos back-ends de Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="0ca11-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="0ca11-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="0ca11-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="0ca11-167">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="0ca11-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="0ca11-168">Resposta</span><span class="sxs-lookup"><span data-stu-id="0ca11-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ca11-169">Não especificado</span><span class="sxs-lookup"><span data-stu-id="0ca11-169">Not specified</span></span> |<span data-ttu-id="0ca11-170">Qualquer</span><span class="sxs-lookup"><span data-stu-id="0ca11-170">Any</span></span> |<span data-ttu-id="0ca11-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0ca11-171">200 - OK</span></span> |
| <span data-ttu-id="0ca11-172">Qualquer valor</span><span class="sxs-lookup"><span data-stu-id="0ca11-172">Any value</span></span> |<span data-ttu-id="0ca11-173">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="0ca11-173">True</span></span> |<span data-ttu-id="0ca11-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0ca11-174">200 - OK</span></span> |
| <span data-ttu-id="0ca11-175">Qualquer valor</span><span class="sxs-lookup"><span data-stu-id="0ca11-175">Any value</span></span> |<span data-ttu-id="0ca11-176">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0ca11-176">False/Not Specified</span></span> |<span data-ttu-id="0ca11-177">400 - solicitação inválida</span><span class="sxs-lookup"><span data-stu-id="0ca11-177">400 - Bad Request</span></span> |

## <span data-ttu-id="0ca11-178"><a name="2.0.0"></a>Servidor e cliente de Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="0ca11-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="0ca11-179"><a name="MobileAppsClients"></a> SDKs de cliente de *Aplicativos* Móveis</span><span class="sxs-lookup"><span data-stu-id="0ca11-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="0ca11-180">A verificação de versão foi introduzida começando com as seguintes versões do SDK do cliente para **Aplicativos Móveis do Azure**:</span><span class="sxs-lookup"><span data-stu-id="0ca11-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="0ca11-181">Plataforma cliente</span><span class="sxs-lookup"><span data-stu-id="0ca11-181">Client platform</span></span> | <span data-ttu-id="0ca11-182">Versão</span><span class="sxs-lookup"><span data-stu-id="0ca11-182">Version</span></span> | <span data-ttu-id="0ca11-183">Valor de cabeçalho de versão</span><span class="sxs-lookup"><span data-stu-id="0ca11-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ca11-184">Cliente gerenciado (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="0ca11-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="0ca11-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="0ca11-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-186">2.0.0</span></span> |
| <span data-ttu-id="0ca11-187">iOS</span><span class="sxs-lookup"><span data-stu-id="0ca11-187">iOS</span></span> |[<span data-ttu-id="0ca11-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="0ca11-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-189">2.0.0</span></span> |
| <span data-ttu-id="0ca11-190">Android</span><span class="sxs-lookup"><span data-stu-id="0ca11-190">Android</span></span> |[<span data-ttu-id="0ca11-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="0ca11-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="0ca11-193">SDKs de servidor dos *Aplicativos* Móveis</span><span class="sxs-lookup"><span data-stu-id="0ca11-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="0ca11-194">A verificação de versão está incluída nas seguintes versões do SDK do servidor:</span><span class="sxs-lookup"><span data-stu-id="0ca11-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="0ca11-195">Plataforma servidor</span><span class="sxs-lookup"><span data-stu-id="0ca11-195">Server platform</span></span> | <span data-ttu-id="0ca11-196">.</span><span class="sxs-lookup"><span data-stu-id="0ca11-196">SDK</span></span> | <span data-ttu-id="0ca11-197">Cabeçalho de versão aceito</span><span class="sxs-lookup"><span data-stu-id="0ca11-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ca11-198">.NET</span><span class="sxs-lookup"><span data-stu-id="0ca11-198">.NET</span></span> |[<span data-ttu-id="0ca11-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="0ca11-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="0ca11-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-200">2.0.0</span></span> |
| <span data-ttu-id="0ca11-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="0ca11-201">Node.js</span></span> |[<span data-ttu-id="0ca11-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="0ca11-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="0ca11-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0ca11-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="0ca11-204">Comportamento dos back-ends de Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="0ca11-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="0ca11-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="0ca11-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="0ca11-206">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="0ca11-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="0ca11-207">Resposta</span><span class="sxs-lookup"><span data-stu-id="0ca11-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ca11-208">x.y.z ou Null</span><span class="sxs-lookup"><span data-stu-id="0ca11-208">x.y.z or Null</span></span> |<span data-ttu-id="0ca11-209">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="0ca11-209">True</span></span> |<span data-ttu-id="0ca11-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0ca11-210">200 - OK</span></span> |
| <span data-ttu-id="0ca11-211">Nulo</span><span class="sxs-lookup"><span data-stu-id="0ca11-211">Null</span></span> |<span data-ttu-id="0ca11-212">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0ca11-212">False/Not Specified</span></span> |<span data-ttu-id="0ca11-213">400 - solicitação inválida</span><span class="sxs-lookup"><span data-stu-id="0ca11-213">400 - Bad Request</span></span> |
| <span data-ttu-id="0ca11-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="0ca11-214">1.x.y</span></span> |<span data-ttu-id="0ca11-215">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0ca11-215">False/Not Specified</span></span> |<span data-ttu-id="0ca11-216">400 - solicitação inválida</span><span class="sxs-lookup"><span data-stu-id="0ca11-216">400 - Bad Request</span></span> |
| <span data-ttu-id="0ca11-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="0ca11-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="0ca11-218">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0ca11-218">False/Not Specified</span></span> |<span data-ttu-id="0ca11-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0ca11-219">200 - OK</span></span> |
| <span data-ttu-id="0ca11-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="0ca11-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="0ca11-221">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0ca11-221">False/Not Specified</span></span> |<span data-ttu-id="0ca11-222">400 - solicitação inválida</span><span class="sxs-lookup"><span data-stu-id="0ca11-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0ca11-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ca11-223">Next Steps</span></span>
* <span data-ttu-id="0ca11-224">[Migrar um Serviço Móvel para o Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="0ca11-224">[Migrate a Mobile Service to Azure App Service]</span></span>

<span data-ttu-id="0ca11-225">[Clientes de Serviços Móveis]: #MobileServicesClients</span><span class="sxs-lookup"><span data-stu-id="0ca11-225">[Mobile Services clients]: #MobileServicesClients</span></span>
<span data-ttu-id="0ca11-226">[Clientes de Aplicativos Móveis]: #MobileAppsClients</span><span class="sxs-lookup"><span data-stu-id="0ca11-226">[Mobile Apps clients]: #MobileAppsClients</span></span>


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
<span data-ttu-id="0ca11-227">[Migrar um Serviço Móvel para o Serviço de Aplicativo do Azure]: app-service-mobile-migrating-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="0ca11-227">[Migrate a Mobile Service to Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span></span>
