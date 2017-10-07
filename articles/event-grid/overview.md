---
title: "Visão geral de grade de eventos aaaAzure"
description: Descreve a Grade de Eventos do Azure e seus conceitos.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="06c7c-103">Uma grade de eventos de tooAzure de Introdução</span><span class="sxs-lookup"><span data-stu-id="06c7c-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="06c7c-104">Grade de eventos do Azure permite que você tooeasily na criação de aplicativos com as arquiteturas de evento.</span><span class="sxs-lookup"><span data-stu-id="06c7c-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="06c7c-105">Selecione o hello recursos do Azure, você deseja toosubscribe para e dar o manipulador de eventos hello ou WebHook ponto de extremidade toosend Olá evento.</span><span class="sxs-lookup"><span data-stu-id="06c7c-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="06c7c-106">A Grade de Eventos tem suporte interno para eventos provenientes de serviços do Azure, como blobs de armazenamento e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="06c7c-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="06c7c-107">A Grade de Eventos também tem suporte personalizado para eventos de aplicativo e de terceiros, usando webhooks e tópicos personalizados.</span><span class="sxs-lookup"><span data-stu-id="06c7c-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="06c7c-108">Você pode usar filtros tooroute eventos específicos toodifferent pontos de extremidade, pontos de extremidade toomultiple multicast e verifique se que os eventos são distribuídos de forma confiável.</span><span class="sxs-lookup"><span data-stu-id="06c7c-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="06c7c-109">A Grade de Eventos também tem suporte interno para eventos personalizados e de terceiros.</span><span class="sxs-lookup"><span data-stu-id="06c7c-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="06c7c-110">Versão de visualização hello, oferece suporte a grade de eventos **westus2** e **westcentralus** locais.</span><span class="sxs-lookup"><span data-stu-id="06c7c-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="06c7c-111">Outras regiões serão adicionadas.</span><span class="sxs-lookup"><span data-stu-id="06c7c-111">Other regions will be added.</span></span>

<span data-ttu-id="06c7c-112">Este artigo fornece uma visão geral da Grade de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="06c7c-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="06c7c-113">Se você quiser tooget iniciado com a grade de eventos, consulte [rota e criar eventos personalizados com a grade de eventos do Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="06c7c-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Modelo funcional da Grade de Eventos](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="06c7c-115">Atualmente, o Armazenamento de Blobs não está disponível publicamente como um publicador.</span><span class="sxs-lookup"><span data-stu-id="06c7c-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="06c7c-116">Conceitos</span><span class="sxs-lookup"><span data-stu-id="06c7c-116">Concepts</span></span>

<span data-ttu-id="06c7c-117">Há cinco conceitos na Grade de Eventos do Azure para sua utilização:</span><span class="sxs-lookup"><span data-stu-id="06c7c-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="06c7c-118">**Eventos**: o que aconteceu.</span><span class="sxs-lookup"><span data-stu-id="06c7c-118">**Events** - What happened.</span></span>
* <span data-ttu-id="06c7c-119">**Fontes de evento/editores** - onde o evento Olá ocorreu.</span><span class="sxs-lookup"><span data-stu-id="06c7c-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="06c7c-120">**Tópicos** -Olá onde Publicadores enviam eventos de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="06c7c-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="06c7c-121">**Assinaturas de evento** -eventos de tooroute de mecanismo de ponto de extremidade ou interna de hello, às vezes, toomultiple manipuladores.</span><span class="sxs-lookup"><span data-stu-id="06c7c-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="06c7c-122">As assinaturas também são usadas pelos eventos de entrada manipuladores toointelligently filtro.</span><span class="sxs-lookup"><span data-stu-id="06c7c-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="06c7c-123">**Manipuladores de eventos** - Olá aplicativo ou serviço reagindo toohello eventos.</span><span class="sxs-lookup"><span data-stu-id="06c7c-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="06c7c-124">Para saber mais sobre esses conceitos, confira [Conceitos na Grade de Eventos do Azure](concepts.md).</span><span class="sxs-lookup"><span data-stu-id="06c7c-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="06c7c-125">Funcionalidades</span><span class="sxs-lookup"><span data-stu-id="06c7c-125">Capabilities</span></span>

<span data-ttu-id="06c7c-126">Aqui estão alguns dos principais recursos Olá da grade de eventos do Azure:</span><span class="sxs-lookup"><span data-stu-id="06c7c-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="06c7c-127">**Simplicidade** -ponto e clique em eventos de tooaim do seu manipulador de eventos de tooany de recursos do Azure ou o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="06c7c-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="06c7c-128">**Filtragem avançada** -filtro de evento de tipo ou evento publicar caminho tooensure manipuladores de eventos somente recebem eventos relevantes.</span><span class="sxs-lookup"><span data-stu-id="06c7c-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="06c7c-129">**Fan-out** -assinar toohello de vários pontos de extremidade toosend do mesmo evento copia de saudação evento tooas em muitos lugares conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="06c7c-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="06c7c-130">**Confiabilidade** -utilizar 24 horas de repetição com retirada exponencial tooensure eventos são entregues.</span><span class="sxs-lookup"><span data-stu-id="06c7c-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="06c7c-131">**Pagamento por evento** - pagar apenas para a quantidade de saudação você usar a grade de eventos.</span><span class="sxs-lookup"><span data-stu-id="06c7c-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="06c7c-132">**Alta taxa de transferência**: crie cargas de trabalho de alto volume na Grade de Eventos com suporte para milhões de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="06c7c-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="06c7c-133">**Eventos internos**: comece a executar rapidamente com eventos internos definidos pelo recurso.</span><span class="sxs-lookup"><span data-stu-id="06c7c-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="06c7c-134">**Eventos personalizados**: use eventos personalizados de rota, filtro e entrega confiável da de Grade de Eventos em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="06c7c-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="06c7c-135">Integração interna entre publicador e manipulador</span><span class="sxs-lookup"><span data-stu-id="06c7c-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="06c7c-136">O Azure oferece suporte interno a eventos usando vários serviços, incluindo publicadores e manipuladores.</span><span class="sxs-lookup"><span data-stu-id="06c7c-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="06c7c-137">Publicadores</span><span class="sxs-lookup"><span data-stu-id="06c7c-137">Publishers</span></span>

<span data-ttu-id="06c7c-138">No momento, hello seguintes serviços do Azure tem suporte do publicador internos para grade de eventos:</span><span class="sxs-lookup"><span data-stu-id="06c7c-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="06c7c-139">Grupos de recursos (operações de gerenciamento)</span><span class="sxs-lookup"><span data-stu-id="06c7c-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="06c7c-140">Assinaturas do Azure (operações de gerenciamento)</span><span class="sxs-lookup"><span data-stu-id="06c7c-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="06c7c-141">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="06c7c-141">Event Hubs</span></span>
* <span data-ttu-id="06c7c-142">Tópicos personalizados</span><span class="sxs-lookup"><span data-stu-id="06c7c-142">Custom Topics</span></span>

<span data-ttu-id="06c7c-143">Outros serviços do Azure serão adicionados neste ano.</span><span class="sxs-lookup"><span data-stu-id="06c7c-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="06c7c-144">Manipuladores</span><span class="sxs-lookup"><span data-stu-id="06c7c-144">Handlers</span></span>

<span data-ttu-id="06c7c-145">No momento, hello seguintes serviços do Azure tem suporte para grade de eventos internos do manipulador:</span><span class="sxs-lookup"><span data-stu-id="06c7c-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="06c7c-146">Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="06c7c-146">Azure Functions</span></span>
* <span data-ttu-id="06c7c-147">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="06c7c-147">Logic Apps</span></span>
* <span data-ttu-id="06c7c-148">Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="06c7c-148">Azure Automation</span></span>
* <span data-ttu-id="06c7c-149">WebHooks</span><span class="sxs-lookup"><span data-stu-id="06c7c-149">WebHooks</span></span>

<span data-ttu-id="06c7c-150">Outros serviços do Azure serão adicionados neste ano.</span><span class="sxs-lookup"><span data-stu-id="06c7c-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="06c7c-151">O que posso fazer com a Grade de Eventos?</span><span class="sxs-lookup"><span data-stu-id="06c7c-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="06c7c-152">A Grade de Eventos do Azure fornece vários recursos que melhoram muito o trabalho sem servidor, de automação de operações e de integração:</span><span class="sxs-lookup"><span data-stu-id="06c7c-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="06c7c-153">Arquiteturas de aplicativo sem servidor</span><span class="sxs-lookup"><span data-stu-id="06c7c-153">Serverless application architectures</span></span>

![Aplicativo sem servidor](./media/overview/serverless_web_app.png)

<span data-ttu-id="06c7c-155">A Grade de Eventos conecta fontes de dados e manipuladores de eventos.</span><span class="sxs-lookup"><span data-stu-id="06c7c-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="06c7c-156">Por exemplo, o gatilho do evento grade tooinstantly use uma análise de imagem de toorun função sem servidor cada vez que uma nova foto é adicionado tooa contêiner de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="06c7c-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="06c7c-157">Automação de operações</span><span class="sxs-lookup"><span data-stu-id="06c7c-157">Ops Automation</span></span>

![Automação de operações](./media/overview/Ops_automation.png)

<span data-ttu-id="06c7c-159">Grade de eventos permite automação toospeed e simplificar a imposição de política.</span><span class="sxs-lookup"><span data-stu-id="06c7c-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="06c7c-160">Por exemplo, a Grade de Eventos pode notificar a Automação do Azure quando uma máquina virtual é criada ou um Banco de Dados SQL é criado.</span><span class="sxs-lookup"><span data-stu-id="06c7c-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="06c7c-161">Esses eventos podem ser usados tooautomatically Verifique se as configurações de serviço são compatíveis, colocar metadados em ferramentas de operações, máquinas virtuais de marca ou itens de trabalho do arquivo.</span><span class="sxs-lookup"><span data-stu-id="06c7c-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="06c7c-162">Integração de aplicativos</span><span class="sxs-lookup"><span data-stu-id="06c7c-162">Application integration</span></span>

![Integração de aplicativos](./media/overview/app_integration.png)

<span data-ttu-id="06c7c-164">A Grade de Eventos conecta seu aplicativo a outros serviços.</span><span class="sxs-lookup"><span data-stu-id="06c7c-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="06c7c-165">Por exemplo, criar um tópico personalizado toosend tooEvent de dados de eventos do aplicativo grade e aproveitar sua entrega confiável, avançada de roteamento e a integração direta com o Azure.</span><span class="sxs-lookup"><span data-stu-id="06c7c-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="06c7c-166">Como alternativa, você pode usar a grade de eventos com os dados de tooprocess aplicativos lógicos em qualquer lugar, sem escrever código.</span><span class="sxs-lookup"><span data-stu-id="06c7c-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="06c7c-167">Qual é a diferente entre a Grade de Eventos e outros serviços de integração do Azure?</span><span class="sxs-lookup"><span data-stu-id="06c7c-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="06c7c-168">A Grade de Eventos é um backplane de eventos que permite a programação reativa e controlada por evento.</span><span class="sxs-lookup"><span data-stu-id="06c7c-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="06c7c-169">Ela está profundamente integrada aos serviços do Azure e pode ser integrada aos serviços de terceiros.</span><span class="sxs-lookup"><span data-stu-id="06c7c-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="06c7c-170">mensagem de saudação do evento contém informações de saudação necessárias toochanges tooreact em serviços e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="06c7c-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="06c7c-171">Grade de eventos não é um pipeline de dados e não fornecer Olá real do objeto que foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="06c7c-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="06c7c-172">O Barramento de Serviço é adequado para aplicativos corporativos tradicionais que exigem transações, ordenação, detecção de duplicidades e consistência instantânea.</span><span class="sxs-lookup"><span data-stu-id="06c7c-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="06c7c-173">A Grade de Eventos foi desenvolvida para proporcionar velocidade, escala, amplitude e baixo custo em um modelo reativo.</span><span class="sxs-lookup"><span data-stu-id="06c7c-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="06c7c-174">É mais adequado tooserverless arquitetura.</span><span class="sxs-lookup"><span data-stu-id="06c7c-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="06c7c-175">A Grade de Eventos complementa outros serviços do Azure como Aplicativos Lógicos e Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="06c7c-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="06c7c-176">Os disparadores de evento grade Olá lógica aplicativo toobegin seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="06c7c-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="06c7c-177">Hubs de evento funciona com a grade de eventos, permitindo que você tooevents tooreact de Hubs de evento captura e pipelines de ingresso e transformação de dados de compilação.</span><span class="sxs-lookup"><span data-stu-id="06c7c-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="06c7c-178">Quanto custa a Grade de Eventos?</span><span class="sxs-lookup"><span data-stu-id="06c7c-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="06c7c-179">A Grade de Eventos do Azure usa um modelo de preço de pagamento por evento, para que você pague só pelo que usa.</span><span class="sxs-lookup"><span data-stu-id="06c7c-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="06c7c-180">Grade de eventos custa US $0,60 por milhão de operações (US $0,30 durante a visualização) e Olá primeiro 100.000 operação por mês são gratuitos.</span><span class="sxs-lookup"><span data-stu-id="06c7c-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="06c7c-181">As operações são definidas como ingresso de evento, correspondência avançada, tentativa de entrega e chamadas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="06c7c-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="06c7c-182">Mais detalhes podem ser encontrados em Olá [página de preços](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="06c7c-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="06c7c-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06c7c-183">Next steps</span></span>

* <span data-ttu-id="06c7c-184">[Criar e assinar eventos toocustom](custom-event-quickstart.md) imediatamente e começar a enviar seu próprio ponto de extremidade de tooany eventos personalizados usando o início rápido do hello grade de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="06c7c-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="06c7c-185">[Usando a lógica de aplicativos como um manipulador de eventos](monitor-virtual-machine-changes-event-grid-logic-app.md) um tutorial sobre como criar um aplicativo usando aplicativos lógicos tooreact tooevents enviada por grade de eventos.</span><span class="sxs-lookup"><span data-stu-id="06c7c-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="06c7c-186">Referência da API REST da Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="06c7c-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="06c7c-187">Fornece mais informações técnicas sobre Olá grade de eventos do Azure e uma referência para o gerenciamento de assinaturas de evento de roteamento e filtragem.</span><span class="sxs-lookup"><span data-stu-id="06c7c-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
