---
title: "Modelo de dados do Azure Application Insights Telemetry – contexto de telemetria | Microsoft Docs"
description: Modelo de dados de contexto do Application Insights Telemetry
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: d6a0cad8bda6ca68aa691867e84f540c5ac9f6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="cb6ab-103">Contexto de telemetria: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="cb6ab-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="cb6ab-104">Cada item de telemetria pode ter campos de contexto fortemente tipados.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="cb6ab-105">Cada campo habilita um cenário de monitoramento específico.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="cb6ab-106">Use a coleção de propriedades personalizadas para armazenar informações contextuais personalizadas ou específicas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="cb6ab-107">Versão do aplicativo</span><span class="sxs-lookup"><span data-stu-id="cb6ab-107">Application version</span></span>

<span data-ttu-id="cb6ab-108">As informações nos campos de contexto de aplicativo sempre são sobre o aplicativo que está enviando a telemetria.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="cb6ab-109">A versão do aplicativo é usada para analisar as alterações de tendências no comportamento do aplicativo e sua correlação com as implantações.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="cb6ab-110">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="cb6ab-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="cb6ab-111">Endereço IP do cliente</span><span class="sxs-lookup"><span data-stu-id="cb6ab-111">Client IP address</span></span>

<span data-ttu-id="cb6ab-112">O endereço IP do dispositivo cliente.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-112">The IP address of the client device.</span></span> <span data-ttu-id="cb6ab-113">Há suporte para IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="cb6ab-114">Quando a telemetria é enviada de um serviço, o contexto de local é sobre o usuário que iniciou a operação no serviço.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="cb6ab-115">O Application Insights extrai as informações de localização geográfica do IP do cliente e as trunca.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="cb6ab-116">Portanto, o IP do cliente por si só não pode ser usado como informações de identificação do usuário final.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="cb6ab-117">Comprimento máximo: 46</span><span class="sxs-lookup"><span data-stu-id="cb6ab-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="cb6ab-118">Tipo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="cb6ab-118">Device type</span></span>

<span data-ttu-id="cb6ab-119">Originalmente, esse campo era usado para indicar o tipo do dispositivo que o usuário final do aplicativo estava usando.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="cb6ab-120">Hoje, é usado principalmente para distinguir a telemetria JavaScript com o tipo de dispositivo 'Navegador' da telemetria do lado do servidor com o tipo de dispositivo 'PC'.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="cb6ab-121">Comprimento máximo: 64</span><span class="sxs-lookup"><span data-stu-id="cb6ab-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="cb6ab-122">ID da operação</span><span class="sxs-lookup"><span data-stu-id="cb6ab-122">Operation id</span></span>

<span data-ttu-id="cb6ab-123">Um identificador exclusivo da operação raiz.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="cb6ab-124">Esse identificador permite a telemetria de grupo em vários componentes.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="cb6ab-125">Confira [correlação de telemetria](application-insights-correlation.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="cb6ab-126">A id da operação é criada por uma solicitação ou uma exibição de página.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="cb6ab-127">Toda a outra telemetria define esse campo como o valor para a solicitação que a contém ou a exibição de página.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="cb6ab-128">Comprimento máximo: 128</span><span class="sxs-lookup"><span data-stu-id="cb6ab-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="cb6ab-129">ID de operação pai</span><span class="sxs-lookup"><span data-stu-id="cb6ab-129">Parent operation ID</span></span>

<span data-ttu-id="cb6ab-130">O identificador exclusivo do pai imediato do item de telemetria.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="cb6ab-131">Confira [correlação de telemetria](application-insights-correlation.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="cb6ab-132">Comprimento máximo: 128</span><span class="sxs-lookup"><span data-stu-id="cb6ab-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="cb6ab-133">Nome da operação</span><span class="sxs-lookup"><span data-stu-id="cb6ab-133">Operation name</span></span>

<span data-ttu-id="cb6ab-134">O nome (grupo) da operação.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-134">The name (group) of the operation.</span></span> <span data-ttu-id="cb6ab-135">O nome da operação é criado por uma solicitação ou uma exibição de página.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="cb6ab-136">Todos os outros itens de telemetria definem esse campo como o valor para a solicitação que a contém ou uma exibição de página.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="cb6ab-137">O nome da operação é usado para localizar todos os itens de telemetria de um grupo de operações (por exemplo 'GET Home/Index').</span><span class="sxs-lookup"><span data-stu-id="cb6ab-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="cb6ab-138">Essa propriedade de contexto é usada para responder a perguntas como "quais são as exceções típica lançadas nesta página".</span><span class="sxs-lookup"><span data-stu-id="cb6ab-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="cb6ab-139">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="cb6ab-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-the-operation"></a><span data-ttu-id="cb6ab-140">Origem sintética da operação</span><span class="sxs-lookup"><span data-stu-id="cb6ab-140">Synthetic source of the operation</span></span>

<span data-ttu-id="cb6ab-141">Nome da origem sintética.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-141">Name of synthetic source.</span></span> <span data-ttu-id="cb6ab-142">Parte da telemetria do aplicativo pode representar o tráfego sintético.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="cb6ab-143">Pode ser o rastreador da Web que está indexando o site, testes de disponibilidade de site ou rastreamentos de bibliotecas de diagnóstico como o SDK do Application Insights em si.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="cb6ab-144">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="cb6ab-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="cb6ab-145">Id da sessão</span><span class="sxs-lookup"><span data-stu-id="cb6ab-145">Session id</span></span>

<span data-ttu-id="cb6ab-146">ID da sessão – a instância de interação do usuário com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="cb6ab-147">As informações nos campos de contexto de sessão sempre são sobre o usuário final.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="cb6ab-148">Quando a telemetria é enviada de um serviço, o contexto de sessão é sobre o usuário que iniciou a operação no serviço.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="cb6ab-149">Comprimento máximo: 64</span><span class="sxs-lookup"><span data-stu-id="cb6ab-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="cb6ab-150">Id de usuário anônimo</span><span class="sxs-lookup"><span data-stu-id="cb6ab-150">Anonymous user id</span></span>

<span data-ttu-id="cb6ab-151">Id de usuário anônimo.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-151">Anonymous user id.</span></span> <span data-ttu-id="cb6ab-152">Representa o usuário final do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-152">Represents the end user of the application.</span></span> <span data-ttu-id="cb6ab-153">Quando a telemetria é enviada de um serviço, o contexto de usuário é sobre o usuário que iniciou a operação no serviço.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-153">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="cb6ab-154">A [Amostragem](app-insights-sampling.md) é uma das técnicas para minimizar a quantidade de telemetria coletada.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-154">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="cb6ab-155">O algoritmo de amostragem tenta fazer a amostragem de toda a telemetria correlacionada.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-155">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="cb6ab-156">A id de usuário anônimo é usado para a geração de pontuação de amostragem.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-156">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="cb6ab-157">A id de usuário anônimo deve ser um valor suficientemente aleatório.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-157">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="cb6ab-158">O uso da id de usuário anônimo para armazenar o nome de usuário é um uso indevido do campo.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-158">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="cb6ab-159">Usar id de usuário Autenticado.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-159">Use Authenticated user id.</span></span>

<span data-ttu-id="cb6ab-160">Comprimento máximo: 128</span><span class="sxs-lookup"><span data-stu-id="cb6ab-160">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="cb6ab-161">Id de usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="cb6ab-161">Authenticated user id</span></span>

<span data-ttu-id="cb6ab-162">Id de usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-162">Authenticated user id.</span></span> <span data-ttu-id="cb6ab-163">O oposto da id de usuário anônimo, esse campo representa o usuário com um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-163">The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="cb6ab-164">As informações de PII não são coletadas por padrão pela maioria dos SDKs.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-164">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="cb6ab-165">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="cb6ab-165">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="cb6ab-166">Id de conta</span><span class="sxs-lookup"><span data-stu-id="cb6ab-166">Account id</span></span>

<span data-ttu-id="cb6ab-167">Em aplicativos multilocatário, é a ID da conta ou o nome com o qual o usuário está agindo.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-167">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="cb6ab-168">Exemplos podem ser a ID da assinatura do Portal do Azure ou a plataforma de blogs de nome de blog.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-168">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="cb6ab-169">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="cb6ab-169">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="cb6ab-170">Função de nuvem</span><span class="sxs-lookup"><span data-stu-id="cb6ab-170">Cloud role</span></span>

<span data-ttu-id="cb6ab-171">Nome da função da qual o aplicativo faz parte.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-171">Name of the role the application is a part of.</span></span> <span data-ttu-id="cb6ab-172">É mapeada diretamente para o nome da função no Azure.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-172">Maps directly to the role name in azure.</span></span> <span data-ttu-id="cb6ab-173">Também pode ser usado para distinguir microsserviços, que fazem parte de um único aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-173">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="cb6ab-174">Comprimento máximo: 256</span><span class="sxs-lookup"><span data-stu-id="cb6ab-174">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="cb6ab-175">Instância de função de nuvem</span><span class="sxs-lookup"><span data-stu-id="cb6ab-175">Cloud role instance</span></span>

<span data-ttu-id="cb6ab-176">Nome da instância em que o aplicativo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-176">Name of the instance where the application is running.</span></span> <span data-ttu-id="cb6ab-177">Nome do computador para o nome de instância local do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-177">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="cb6ab-178">Comprimento máximo: 256</span><span class="sxs-lookup"><span data-stu-id="cb6ab-178">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="cb6ab-179">Interno: versão de SDK</span><span class="sxs-lookup"><span data-stu-id="cb6ab-179">Internal: SDK version</span></span>

<span data-ttu-id="cb6ab-180">Versão do SDK.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-180">SDK version.</span></span> <span data-ttu-id="cb6ab-181">Veja https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification para saber mais.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-181">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="cb6ab-182">Comprimento máximo: 64</span><span class="sxs-lookup"><span data-stu-id="cb6ab-182">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="cb6ab-183">Interno: nome do nó</span><span class="sxs-lookup"><span data-stu-id="cb6ab-183">Internal: Node name</span></span>

<span data-ttu-id="cb6ab-184">Este campo representa o nome do nó usado para fins de cobrança.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-184">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="cb6ab-185">Usado para substituir a detecção padrão de nós.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-185">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="cb6ab-186">Comprimento máximo: 256</span><span class="sxs-lookup"><span data-stu-id="cb6ab-186">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="cb6ab-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb6ab-187">Next steps</span></span>

- <span data-ttu-id="cb6ab-188">Saiba como [estender e filtrar a telemetria](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="cb6ab-188">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="cb6ab-189">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cb6ab-189">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="cb6ab-190">Confira a coleção de propriedades de contexto padrão [configuração](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span><span class="sxs-lookup"><span data-stu-id="cb6ab-190">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
