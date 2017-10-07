---
title: "aaaClient e o servidor de controle de versão SDK de aplicativos móveis e serviços móveis | Microsoft Docs"
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
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="0063c-103">Controle de versão de cliente e servidor em Aplicativos Móveis e Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="0063c-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="0063c-104">a versão mais recente Olá de serviços móveis do Azure é hello **aplicativos móveis** recurso de serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="0063c-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="0063c-105">Olá cliente de aplicativos móveis e SDKs de servidor originalmente são baseadas nos serviços móveis, mas são *não* compatíveis entre si.</span><span class="sxs-lookup"><span data-stu-id="0063c-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="0063c-106">Ou seja, você deve usar um SDK de cliente de *Aplicativos Móveis* com SDK de servidor de *Aplicativos Móveis* e da mesma forma para *Serviços Móveis*.</span><span class="sxs-lookup"><span data-stu-id="0063c-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="0063c-107">Este contrato é imposto por meio de um valor de cabeçalho especial usado pelo cliente hello e servidor SDKs, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="0063c-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="0063c-108">Observação: sempre que este documento se refere tooa *serviços móveis* back-end, ele não necessariamente precisa toobe hospedado em serviços móveis.</span><span class="sxs-lookup"><span data-stu-id="0063c-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="0063c-109">Agora é possível toomigrate um toorun de serviço móvel no serviço de aplicativo sem alterações de código, mas o serviço de saudação ainda usa *serviços móveis* versões do SDK.</span><span class="sxs-lookup"><span data-stu-id="0063c-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="0063c-110">toolearn mais sobre migração tooApp serviço sem quaisquer alterações de código, consulte o artigo de saudação [migrar tooAzure um serviço móvel do serviço de aplicativo].</span><span class="sxs-lookup"><span data-stu-id="0063c-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="0063c-111">Especificação de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="0063c-111">Header specification</span></span>
<span data-ttu-id="0063c-112">chave de saudação `ZUMO-API-VERSION` pode ser especificado no cabeçalho HTTP de saudação ou cadeia de caracteres de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="0063c-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="0063c-113">valor de saudação é uma cadeia de caracteres de versão no formulário Olá **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="0063c-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="0063c-114">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0063c-114">For example:</span></span>

<span data-ttu-id="0063c-115">GET https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="0063c-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="0063c-116">CABEÇALHOS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="0063c-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="0063c-118">Recusando a verificação de versão</span><span class="sxs-lookup"><span data-stu-id="0063c-118">Opting out of version checking</span></span>
<span data-ttu-id="0063c-119">Você pode recusar a verificação, definindo um valor de versão **true** para configuração de aplicativo hello **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="0063c-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="0063c-120">Especifique isso na Web. config ou em Olá seção configurações do aplicativo de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0063c-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0063c-121">Há um número de alterações de comportamento entre serviços móveis e aplicativos móveis, especialmente nas áreas de saudação da sincronização offline, autenticação e notificações por push.</span><span class="sxs-lookup"><span data-stu-id="0063c-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="0063c-122">Você só deve recusar versão verificação após a conclusão tooensure teste que essas alterações de comportamento não prejudicam a funcionalidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0063c-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="0063c-123">Resumo de compatibilidade para todas as versões</span><span class="sxs-lookup"><span data-stu-id="0063c-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="0063c-124">Olá gráfico a seguir mostra a compatibilidade de saudação entre todos os tipos de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="0063c-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="0063c-125">Um back-end é classificado como qualquer Mobile **serviços** ou Mobile **aplicativos** com base no servidor de saudação SDK que ele usa.</span><span class="sxs-lookup"><span data-stu-id="0063c-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="0063c-126">**Serviços Móveis** </span><span class="sxs-lookup"><span data-stu-id="0063c-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="0063c-127">**Aplicativos Móveis** </span><span class="sxs-lookup"><span data-stu-id="0063c-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0063c-128">[Clientes de Serviços Móveis]</span><span class="sxs-lookup"><span data-stu-id="0063c-128">[Mobile Services clients]</span></span> |<span data-ttu-id="0063c-129">OK</span><span class="sxs-lookup"><span data-stu-id="0063c-129">Ok</span></span> |<span data-ttu-id="0063c-130">Erro\*</span><span class="sxs-lookup"><span data-stu-id="0063c-130">Error\*</span></span> |
| <span data-ttu-id="0063c-131">[Clientes de Aplicativos Móveis]</span><span class="sxs-lookup"><span data-stu-id="0063c-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="0063c-132">Erro\*</span><span class="sxs-lookup"><span data-stu-id="0063c-132">Error\*</span></span> |<span data-ttu-id="0063c-133">OK</span><span class="sxs-lookup"><span data-stu-id="0063c-133">Ok</span></span> |

<span data-ttu-id="0063c-134">\*Isso pode ser controlado especificando**MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="0063c-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="0063c-135"><a name="1.0.0"></a>Servidor e cliente de Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="0063c-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="0063c-136">cliente Olá SDKs na tabela de saudação abaixo são compatíveis com **serviços móveis**.</span><span class="sxs-lookup"><span data-stu-id="0063c-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="0063c-137">Observação: Olá SDKs de cliente de serviços móveis *não* enviar um valor de cabeçalho `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="0063c-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="0063c-138">Se o serviço de saudação receber este cabeçalho ou o valor de cadeia de caracteres de consulta, um erro será retornado, a menos que explicitamente incluído como descrito acima.</span><span class="sxs-lookup"><span data-stu-id="0063c-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="0063c-139"><a name="MobileServicesClients"></a> SDKs de clientes de *Serviços* Móveis</span><span class="sxs-lookup"><span data-stu-id="0063c-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="0063c-140">Plataforma cliente</span><span class="sxs-lookup"><span data-stu-id="0063c-140">Client platform</span></span> | <span data-ttu-id="0063c-141">Versão</span><span class="sxs-lookup"><span data-stu-id="0063c-141">Version</span></span> | <span data-ttu-id="0063c-142">Valor de cabeçalho de versão</span><span class="sxs-lookup"><span data-stu-id="0063c-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0063c-143">Cliente gerenciado (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="0063c-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="0063c-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="0063c-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="0063c-145">n/d</span><span class="sxs-lookup"><span data-stu-id="0063c-145">n/a</span></span> |
| <span data-ttu-id="0063c-146">iOS</span><span class="sxs-lookup"><span data-stu-id="0063c-146">iOS</span></span> |[<span data-ttu-id="0063c-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="0063c-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="0063c-148">n/d</span><span class="sxs-lookup"><span data-stu-id="0063c-148">n/a</span></span> |
| <span data-ttu-id="0063c-149">Android</span><span class="sxs-lookup"><span data-stu-id="0063c-149">Android</span></span> |[<span data-ttu-id="0063c-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="0063c-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="0063c-151">n/d</span><span class="sxs-lookup"><span data-stu-id="0063c-151">n/a</span></span> |
| <span data-ttu-id="0063c-152">HTML</span><span class="sxs-lookup"><span data-stu-id="0063c-152">HTML</span></span> |[<span data-ttu-id="0063c-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="0063c-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="0063c-154">n/d</span><span class="sxs-lookup"><span data-stu-id="0063c-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="0063c-155">SDKs de servidor de *Serviços* Móveis</span><span class="sxs-lookup"><span data-stu-id="0063c-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="0063c-156">Plataforma servidor</span><span class="sxs-lookup"><span data-stu-id="0063c-156">Server platform</span></span> | <span data-ttu-id="0063c-157">Versão</span><span class="sxs-lookup"><span data-stu-id="0063c-157">Version</span></span> | <span data-ttu-id="0063c-158">Cabeçalho de versão aceito</span><span class="sxs-lookup"><span data-stu-id="0063c-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0063c-159">.NET</span><span class="sxs-lookup"><span data-stu-id="0063c-159">.NET</span></span> |[<span data-ttu-id="0063c-160">WindowsAzure.MobileServices.Backend.* versão 1.0. x</span><span class="sxs-lookup"><span data-stu-id="0063c-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="0063c-161">* * Nenhum cabeçalho de versão * *</span><span class="sxs-lookup"><span data-stu-id="0063c-161">**No version header **</span></span> |
| <span data-ttu-id="0063c-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="0063c-162">Node.js</span></span> |<span data-ttu-id="0063c-163">(em breve)</span><span class="sxs-lookup"><span data-stu-id="0063c-163">(coming soon)</span></span> |<span data-ttu-id="0063c-164">**Nenhum cabeçalho de versão**</span><span class="sxs-lookup"><span data-stu-id="0063c-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="0063c-165">Comportamento dos back-ends de Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="0063c-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="0063c-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="0063c-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="0063c-167">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="0063c-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="0063c-168">Resposta</span><span class="sxs-lookup"><span data-stu-id="0063c-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0063c-169">Não especificado</span><span class="sxs-lookup"><span data-stu-id="0063c-169">Not specified</span></span> |<span data-ttu-id="0063c-170">Qualquer</span><span class="sxs-lookup"><span data-stu-id="0063c-170">Any</span></span> |<span data-ttu-id="0063c-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0063c-171">200 - OK</span></span> |
| <span data-ttu-id="0063c-172">Qualquer valor</span><span class="sxs-lookup"><span data-stu-id="0063c-172">Any value</span></span> |<span data-ttu-id="0063c-173">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="0063c-173">True</span></span> |<span data-ttu-id="0063c-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0063c-174">200 - OK</span></span> |
| <span data-ttu-id="0063c-175">Qualquer valor</span><span class="sxs-lookup"><span data-stu-id="0063c-175">Any value</span></span> |<span data-ttu-id="0063c-176">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0063c-176">False/Not Specified</span></span> |<span data-ttu-id="0063c-177">400 - solicitação inválida</span><span class="sxs-lookup"><span data-stu-id="0063c-177">400 - Bad Request</span></span> |

## <span data-ttu-id="0063c-178"><a name="2.0.0"></a>Servidor e cliente de Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="0063c-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="0063c-179"><a name="MobileAppsClients"></a> SDKs de cliente de *Aplicativos* Móveis</span><span class="sxs-lookup"><span data-stu-id="0063c-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="0063c-180">A verificação de versão foi introduzida Olá seguintes versões do SDK do cliente Olá para **aplicativos móveis do Azure**:</span><span class="sxs-lookup"><span data-stu-id="0063c-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="0063c-181">Plataforma cliente</span><span class="sxs-lookup"><span data-stu-id="0063c-181">Client platform</span></span> | <span data-ttu-id="0063c-182">Versão</span><span class="sxs-lookup"><span data-stu-id="0063c-182">Version</span></span> | <span data-ttu-id="0063c-183">Valor de cabeçalho de versão</span><span class="sxs-lookup"><span data-stu-id="0063c-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0063c-184">Cliente gerenciado (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="0063c-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="0063c-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="0063c-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-186">2.0.0</span></span> |
| <span data-ttu-id="0063c-187">iOS</span><span class="sxs-lookup"><span data-stu-id="0063c-187">iOS</span></span> |[<span data-ttu-id="0063c-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="0063c-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-189">2.0.0</span></span> |
| <span data-ttu-id="0063c-190">Android</span><span class="sxs-lookup"><span data-stu-id="0063c-190">Android</span></span> |[<span data-ttu-id="0063c-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="0063c-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="0063c-193">SDKs de servidor dos *Aplicativos* Móveis</span><span class="sxs-lookup"><span data-stu-id="0063c-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="0063c-194">A verificação de versão está incluída nas seguintes versões do SDK do servidor:</span><span class="sxs-lookup"><span data-stu-id="0063c-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="0063c-195">Plataforma servidor</span><span class="sxs-lookup"><span data-stu-id="0063c-195">Server platform</span></span> | <span data-ttu-id="0063c-196">.</span><span class="sxs-lookup"><span data-stu-id="0063c-196">SDK</span></span> | <span data-ttu-id="0063c-197">Cabeçalho de versão aceito</span><span class="sxs-lookup"><span data-stu-id="0063c-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0063c-198">.NET</span><span class="sxs-lookup"><span data-stu-id="0063c-198">.NET</span></span> |[<span data-ttu-id="0063c-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="0063c-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="0063c-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-200">2.0.0</span></span> |
| <span data-ttu-id="0063c-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="0063c-201">Node.js</span></span> |[<span data-ttu-id="0063c-202">azure-mobile-apps)</span><span class="sxs-lookup"><span data-stu-id="0063c-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="0063c-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0063c-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="0063c-204">Comportamento dos back-ends de Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="0063c-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="0063c-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="0063c-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="0063c-206">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="0063c-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="0063c-207">Resposta</span><span class="sxs-lookup"><span data-stu-id="0063c-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0063c-208">x.y.z ou Null</span><span class="sxs-lookup"><span data-stu-id="0063c-208">x.y.z or Null</span></span> |<span data-ttu-id="0063c-209">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="0063c-209">True</span></span> |<span data-ttu-id="0063c-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0063c-210">200 - OK</span></span> |
| <span data-ttu-id="0063c-211">Nulo</span><span class="sxs-lookup"><span data-stu-id="0063c-211">Null</span></span> |<span data-ttu-id="0063c-212">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0063c-212">False/Not Specified</span></span> |<span data-ttu-id="0063c-213">400 - solicitação inválida</span><span class="sxs-lookup"><span data-stu-id="0063c-213">400 - Bad Request</span></span> |
| <span data-ttu-id="0063c-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="0063c-214">1.x.y</span></span> |<span data-ttu-id="0063c-215">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0063c-215">False/Not Specified</span></span> |<span data-ttu-id="0063c-216">400 - solicitação inválida</span><span class="sxs-lookup"><span data-stu-id="0063c-216">400 - Bad Request</span></span> |
| <span data-ttu-id="0063c-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="0063c-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="0063c-218">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0063c-218">False/Not Specified</span></span> |<span data-ttu-id="0063c-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="0063c-219">200 - OK</span></span> |
| <span data-ttu-id="0063c-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="0063c-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="0063c-221">Falso/não especificado</span><span class="sxs-lookup"><span data-stu-id="0063c-221">False/Not Specified</span></span> |<span data-ttu-id="0063c-222">400 - solicitação inválida</span><span class="sxs-lookup"><span data-stu-id="0063c-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0063c-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0063c-223">Next Steps</span></span>
* <span data-ttu-id="0063c-224">[migrar tooAzure um serviço móvel do serviço de aplicativo]</span><span class="sxs-lookup"><span data-stu-id="0063c-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[Clientes de Serviços Móveis]: #MobileServicesClients
[Clientes de Aplicativos Móveis]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migrar tooAzure um serviço móvel do serviço de aplicativo]: app-service-mobile-migrating-from-mobile-services.md
