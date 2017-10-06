---
title: aaaAzure modelo de dados de telemetria do Application Insights - contexto de telemetria | Microsoft Docs
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
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="31ce6-103">Contexto de telemetria: modelo de dados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="31ce6-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="31ce6-104">Cada item de telemetria pode ter campos de contexto fortemente tipados.</span><span class="sxs-lookup"><span data-stu-id="31ce6-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="31ce6-105">Cada campo habilita um cenário de monitoramento específico.</span><span class="sxs-lookup"><span data-stu-id="31ce6-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="31ce6-106">Use Olá propriedades personalizadas coleção toostore personalizados ou específicos ao aplicativo informações contextuais.</span><span class="sxs-lookup"><span data-stu-id="31ce6-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="31ce6-107">Versão do aplicativo</span><span class="sxs-lookup"><span data-stu-id="31ce6-107">Application version</span></span>

<span data-ttu-id="31ce6-108">As informações nos campos de contexto de aplicativo hello estão sempre sobre o aplicativo hello que está enviando a telemetria de saudação.</span><span class="sxs-lookup"><span data-stu-id="31ce6-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="31ce6-109">Versão do aplicativo é usado tooanalyze tendência alterações no comportamento do aplicativo hello e suas implantações de toohello de correlação.</span><span class="sxs-lookup"><span data-stu-id="31ce6-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="31ce6-110">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="31ce6-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="31ce6-111">Endereço IP do cliente</span><span class="sxs-lookup"><span data-stu-id="31ce6-111">Client IP address</span></span>

<span data-ttu-id="31ce6-112">endereço IP Olá Olá de dispositivo de cliente.</span><span class="sxs-lookup"><span data-stu-id="31ce6-112">hello IP address of hello client device.</span></span> <span data-ttu-id="31ce6-113">Há suporte para IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="31ce6-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="31ce6-114">Quando a telemetria é enviada de um serviço, o contexto de local de Olá é sobre o usuário Olá que iniciou a operação Olá no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="31ce6-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="31ce6-115">Extrair informações de localização geográfica de saudação do IP do cliente de saudação do Application Insights e, em seguida, Trunque-o.</span><span class="sxs-lookup"><span data-stu-id="31ce6-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="31ce6-116">Portanto, o IP do cliente por si só não pode ser usado como informações de identificação do usuário final.</span><span class="sxs-lookup"><span data-stu-id="31ce6-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="31ce6-117">Comprimento máximo: 46</span><span class="sxs-lookup"><span data-stu-id="31ce6-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="31ce6-118">Tipo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="31ce6-118">Device type</span></span>

<span data-ttu-id="31ce6-119">Esse campo foi usado originalmente tooindicate Olá tipo de usuário do hello dispositivo Olá final do aplicativo hello está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="31ce6-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="31ce6-120">Hoje usado principalmente telemetria de JavaScript toodistinguish com hello dispositivo tipo 'Browser' de telemetria do lado do servidor com o tipo de dispositivo de saudação 'Computador'.</span><span class="sxs-lookup"><span data-stu-id="31ce6-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="31ce6-121">Comprimento máximo: 64</span><span class="sxs-lookup"><span data-stu-id="31ce6-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="31ce6-122">ID da operação</span><span class="sxs-lookup"><span data-stu-id="31ce6-122">Operation id</span></span>

<span data-ttu-id="31ce6-123">Um identificador exclusivo da operação de raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="31ce6-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="31ce6-124">Esse identificador permite toogroup telemetria entre vários componentes.</span><span class="sxs-lookup"><span data-stu-id="31ce6-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="31ce6-125">Confira [correlação de telemetria](application-insights-correlation.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="31ce6-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="31ce6-126">id da operação Olá é criado por uma solicitação ou um modo de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="31ce6-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="31ce6-127">Todos os outros telemetria define o valor deste campo toohello para Olá que contém a exibição de página ou solicitação.</span><span class="sxs-lookup"><span data-stu-id="31ce6-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="31ce6-128">Comprimento máximo: 128</span><span class="sxs-lookup"><span data-stu-id="31ce6-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="31ce6-129">ID de operação pai</span><span class="sxs-lookup"><span data-stu-id="31ce6-129">Parent operation ID</span></span>

<span data-ttu-id="31ce6-130">Olá identificador exclusivo do pai imediato do item de telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="31ce6-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="31ce6-131">Confira [correlação de telemetria](application-insights-correlation.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="31ce6-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="31ce6-132">Comprimento máximo: 128</span><span class="sxs-lookup"><span data-stu-id="31ce6-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="31ce6-133">Nome da operação</span><span class="sxs-lookup"><span data-stu-id="31ce6-133">Operation name</span></span>

<span data-ttu-id="31ce6-134">nome da saudação (grupo) da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="31ce6-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="31ce6-135">nome da operação Olá é criado por uma solicitação ou um modo de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="31ce6-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="31ce6-136">Todos os outros itens de telemetria definir esse valor de toohello de campo para Olá que contém o modo de solicitação ou de página.</span><span class="sxs-lookup"><span data-stu-id="31ce6-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="31ce6-137">Nome da operação é usado para localizar todos os itens de telemetria Olá para um grupo de operações (por exemplo ' inicial de GET/Index').</span><span class="sxs-lookup"><span data-stu-id="31ce6-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="31ce6-138">Essa propriedade de contexto é usado tooanswer perguntas como "quais são exceções típico de saudação geradas nesta página."</span><span class="sxs-lookup"><span data-stu-id="31ce6-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="31ce6-139">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="31ce6-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="31ce6-140">Sintética fonte da operação de saudação</span><span class="sxs-lookup"><span data-stu-id="31ce6-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="31ce6-141">Nome da origem sintética.</span><span class="sxs-lookup"><span data-stu-id="31ce6-141">Name of synthetic source.</span></span> <span data-ttu-id="31ce6-142">Alguns telemetria do aplicativo hello pode representar o tráfego sintético.</span><span class="sxs-lookup"><span data-stu-id="31ce6-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="31ce6-143">Pode ser o site da web hello, indexação rastreador, testes de disponibilidade do site ou rastreamentos de diagnósticos bibliotecas como o SDK do Application Insights em si.</span><span class="sxs-lookup"><span data-stu-id="31ce6-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="31ce6-144">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="31ce6-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="31ce6-145">Id da sessão</span><span class="sxs-lookup"><span data-stu-id="31ce6-145">Session id</span></span>

<span data-ttu-id="31ce6-146">ID de sessão - instância Olá Olá de interação do usuário com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="31ce6-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="31ce6-147">As informações nos campos de contexto de sessão Olá estão sempre sobre o usuário final de saudação.</span><span class="sxs-lookup"><span data-stu-id="31ce6-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="31ce6-148">Quando a telemetria é enviada de um serviço, contexto de sessão Olá é sobre o usuário Olá que iniciou a operação Olá no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="31ce6-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="31ce6-149">Comprimento máximo: 64</span><span class="sxs-lookup"><span data-stu-id="31ce6-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="31ce6-150">Id de usuário anônimo</span><span class="sxs-lookup"><span data-stu-id="31ce6-150">Anonymous user id</span></span>

<span data-ttu-id="31ce6-151">Id de usuário anônimo. Representa o usuário final de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="31ce6-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="31ce6-152">Quando a telemetria é enviada de um serviço, o contexto de usuário de saudação está sobre o usuário Olá que iniciou a operação Olá no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="31ce6-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="31ce6-153">[Amostragem](app-insights-sampling.md) é um valor de saudação do hello técnicas toominimize de telemetria coletada.</span><span class="sxs-lookup"><span data-stu-id="31ce6-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="31ce6-154">Exemplo in ou out Olá todos os tooeither de tentativas de algoritmo de amostragem correlacionados telemetria.</span><span class="sxs-lookup"><span data-stu-id="31ce6-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="31ce6-155">A id de usuário anônimo é usado para a geração de pontuação de amostragem.</span><span class="sxs-lookup"><span data-stu-id="31ce6-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="31ce6-156">A id de usuário anônimo deve ser um valor suficientemente aleatório.</span><span class="sxs-lookup"><span data-stu-id="31ce6-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="31ce6-157">Usar o nome de usuário de toostore de id de usuário anônimo é um uso indevido do campo hello.</span><span class="sxs-lookup"><span data-stu-id="31ce6-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="31ce6-158">Usar id de usuário Autenticado.</span><span class="sxs-lookup"><span data-stu-id="31ce6-158">Use Authenticated user id.</span></span>

<span data-ttu-id="31ce6-159">Comprimento máximo: 128</span><span class="sxs-lookup"><span data-stu-id="31ce6-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="31ce6-160">Id de usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="31ce6-160">Authenticated user id</span></span>

<span data-ttu-id="31ce6-161">Id de usuário autenticado. Olá oposta da id de usuário anônimo, este campo representa o usuário Olá com um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="31ce6-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="31ce6-162">As informações de PII não são coletadas por padrão pela maioria dos SDKs.</span><span class="sxs-lookup"><span data-stu-id="31ce6-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="31ce6-163">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="31ce6-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="31ce6-164">Id de conta</span><span class="sxs-lookup"><span data-stu-id="31ce6-164">Account id</span></span>

<span data-ttu-id="31ce6-165">Em aplicativos de multilocação é Olá ID da conta ou nome de usuário hello está agindo com.</span><span class="sxs-lookup"><span data-stu-id="31ce6-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="31ce6-166">Exemplos podem ser a ID da assinatura do Portal do Azure ou a plataforma de blogs de nome de blog.</span><span class="sxs-lookup"><span data-stu-id="31ce6-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="31ce6-167">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="31ce6-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="31ce6-168">Função de nuvem</span><span class="sxs-lookup"><span data-stu-id="31ce6-168">Cloud role</span></span>

<span data-ttu-id="31ce6-169">Nome do aplicativo de saudação do hello função é uma parte do.</span><span class="sxs-lookup"><span data-stu-id="31ce6-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="31ce6-170">Mapeia diretamente toohello nome da função no azure.</span><span class="sxs-lookup"><span data-stu-id="31ce6-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="31ce6-171">Também é possível toodistinguish usado micro serviços, que fazem parte de um único aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31ce6-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="31ce6-172">Comprimento máximo: 256</span><span class="sxs-lookup"><span data-stu-id="31ce6-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="31ce6-173">Instância de função de nuvem</span><span class="sxs-lookup"><span data-stu-id="31ce6-173">Cloud role instance</span></span>

<span data-ttu-id="31ce6-174">Nome da instância de saudação onde o aplicativo hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="31ce6-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="31ce6-175">Nome do computador para o nome de instância local do Azure.</span><span class="sxs-lookup"><span data-stu-id="31ce6-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="31ce6-176">Comprimento máximo: 256</span><span class="sxs-lookup"><span data-stu-id="31ce6-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="31ce6-177">Interno: versão de SDK</span><span class="sxs-lookup"><span data-stu-id="31ce6-177">Internal: SDK version</span></span>

<span data-ttu-id="31ce6-178">Versão do SDK.</span><span class="sxs-lookup"><span data-stu-id="31ce6-178">SDK version.</span></span> <span data-ttu-id="31ce6-179">Veja https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification para saber mais.</span><span class="sxs-lookup"><span data-stu-id="31ce6-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="31ce6-180">Comprimento máximo: 64</span><span class="sxs-lookup"><span data-stu-id="31ce6-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="31ce6-181">Interno: nome do nó</span><span class="sxs-lookup"><span data-stu-id="31ce6-181">Internal: Node name</span></span>

<span data-ttu-id="31ce6-182">Este campo representa o nome do nó Olá usado para fins de cobrança.</span><span class="sxs-lookup"><span data-stu-id="31ce6-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="31ce6-183">Use-toooverride saudação padrão a detecção de nós.</span><span class="sxs-lookup"><span data-stu-id="31ce6-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="31ce6-184">Comprimento máximo: 256</span><span class="sxs-lookup"><span data-stu-id="31ce6-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="31ce6-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31ce6-185">Next steps</span></span>

- <span data-ttu-id="31ce6-186">Saiba como muito[estender e filtrar telemetria](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="31ce6-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="31ce6-187">Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="31ce6-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="31ce6-188">Confira a coleção de propriedades de contexto padrão [configuração](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span><span class="sxs-lookup"><span data-stu-id="31ce6-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
