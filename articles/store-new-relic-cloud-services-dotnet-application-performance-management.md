---
title: aaaUsing New Relic com o Azure | Microsoft Docs
description: "Saiba como toouse Olá toomanage de serviço New Relic e monitorar seu aplicativo do Azure."
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="01aee-103">Gerenciamento de desempenho do aplicativo New Relic no Azure</span><span class="sxs-lookup"><span data-stu-id="01aee-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="01aee-104">Você pode adicionar o desempenho de classe mundial do New Relic monitoramento tooyour Azure aplicativos hospedados.</span><span class="sxs-lookup"><span data-stu-id="01aee-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="01aee-105">Juntamente com recursos abrangentes de monitoramento, solução de problemas e ajuste dos aplicativos do Azure, você também está qualificado para um preço com desconto para produtos do New Relic usando o Azure.</span><span class="sxs-lookup"><span data-stu-id="01aee-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="01aee-106">O que há de novo Relíquia?</span><span class="sxs-lookup"><span data-stu-id="01aee-106">What is New Relic?</span></span>
<span data-ttu-id="01aee-107">Com [produtos New Relic](https://newrelic.com/products), resolver erros de aplicativo, se manter à frente de possíveis problemas e entender o desempenho de saudação de todo o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="01aee-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="01aee-108">É projetado toosave tempo quando identificar e diagnosticar problemas de desempenho, e ele coloca informações Olá necessárias toosolve esses problemas ao seu alcance.</span><span class="sxs-lookup"><span data-stu-id="01aee-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="01aee-109">Saudação de rastreia New Relic carregar o tempo e a taxa de transferência para as transações da web, tanto do servidor de saudação e navegadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="01aee-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="01aee-110">Ele mostra o tempo gasto no banco de dados Olá analisa consultas lentas e solicitações da web, fornece o tempo de atividade de monitoramento e alertas, rastreia exceções de aplicativo e muito mais.</span><span class="sxs-lookup"><span data-stu-id="01aee-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="01aee-111">Preço especial</span><span class="sxs-lookup"><span data-stu-id="01aee-111">Special pricing</span></span>
<span data-ttu-id="01aee-112">New Relic padrão é livre tooAzure usuários.</span><span class="sxs-lookup"><span data-stu-id="01aee-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="01aee-113">Nova Relíquia Pro é oferecido com base no tamanho da instância para os serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="01aee-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="01aee-114">Para obter informações sobre preços, consulte Olá [página New Relic](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) em hello Azure Marketplace ou entre em contato com o New Relic (sales@newrelic.com) para preços de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="01aee-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="01aee-115">Clientes do Azure recebem uma assinatura de avaliação de duas semanas do New Relic Pro ao implantar um agente do New Relic hello.</span><span class="sxs-lookup"><span data-stu-id="01aee-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="01aee-116">Inscreva-se para o New Relic usando hello Azure Store</span><span class="sxs-lookup"><span data-stu-id="01aee-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="01aee-117">Relíquia nova integra-se perfeitamente com funções de funções do Azure da Web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="01aee-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="01aee-118">Você pode rapidamente e facilmente inscrever-se para o New Relic diretamente do hello Azure Store.</span><span class="sxs-lookup"><span data-stu-id="01aee-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="01aee-119">Para obter instruções, consulte Olá [Azure armazena instruções de inscrição](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) do New Relic.</span><span class="sxs-lookup"><span data-stu-id="01aee-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="01aee-120">Ver seus dados</span><span class="sxs-lookup"><span data-stu-id="01aee-120">View your data</span></span>
<span data-ttu-id="01aee-121">Depois de se inscrever, você pode tirar proveito do incrível monitoramento de aplicativo e análise orientado a dados do New Relic.</span><span class="sxs-lookup"><span data-stu-id="01aee-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="01aee-122">toocheck o desempenho do seu aplicativo no New Relic:</span><span class="sxs-lookup"><span data-stu-id="01aee-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="01aee-123">De Olá Portal do Azure, selecione Gerenciar.</span><span class="sxs-lookup"><span data-stu-id="01aee-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="01aee-124">Entrar com seu e-mail do Relíquia nova conta e senha.</span><span class="sxs-lookup"><span data-stu-id="01aee-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="01aee-125">Selecione seu aplicativo hello aplicativo índice tooview todos os dados de seu aplicativo no hello [página de visão geral do APM](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="01aee-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="01aee-126">Como usar o New Relic com o Azure</span><span class="sxs-lookup"><span data-stu-id="01aee-126">Using New Relic with Azure</span></span>
<span data-ttu-id="01aee-127">Para saber mais sobre como usar o New Relic e o Azure, consulte [site de documentação do New Relic](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), incluindo:</span><span class="sxs-lookup"><span data-stu-id="01aee-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="01aee-128">New Relic para .NET</span><span class="sxs-lookup"><span data-stu-id="01aee-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="01aee-129">Instrumentar uma função de trabalho do .NET no Serviço de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="01aee-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="01aee-130">New Relic para a plataforma de nuvem do Microsoft Azure Olá</span><span class="sxs-lookup"><span data-stu-id="01aee-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="01aee-131">New Relic para Olá serviços de aplicativos do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="01aee-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="01aee-132">Solução de problemas do New Relic/Azure</span><span class="sxs-lookup"><span data-stu-id="01aee-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

