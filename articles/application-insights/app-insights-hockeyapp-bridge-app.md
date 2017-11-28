---
title: aaaExploring HockeyApp dados no Azure Application Insights | Microsoft Docs
description: Analise o uso e o desempenho de seu aplicativo do Azure com o Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="d6a20-103">Exploração de dados do HockeyApp no Application Insights</span><span class="sxs-lookup"><span data-stu-id="d6a20-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="d6a20-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) Olá recomenda plataforma para monitoramento de aplicativos móveis e desktop ao vivo.</span><span class="sxs-lookup"><span data-stu-id="d6a20-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="d6a20-105">Do HockeyApp, você pode enviar personalizado e uso de toomonitor de telemetria de rastreamento e auxiliar no diagnóstico (em adição toogetting falha de dados).</span><span class="sxs-lookup"><span data-stu-id="d6a20-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="d6a20-106">Este fluxo de telemetria pode ser consultado usando Olá poderoso [análise](app-insights-analytics.md) recurso de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6a20-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="d6a20-107">Além disso, você pode [exportar hello personalizado e telemetria de rastreamento](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="d6a20-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="d6a20-108">tooenable esses recursos, você configurar uma ponte que retransmite HockeyApp dados personalizados tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="d6a20-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="d6a20-109">aplicativo de ponte HockeyApp Olá</span><span class="sxs-lookup"><span data-stu-id="d6a20-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="d6a20-110">Olá HockeyApp ponte aplicativo é Olá dos principais recursos que permite que você tooaccess o HockeyApp personalizado e telemetria de rastreamento no Application Insights por meio de saudação análise e os recursos de exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="d6a20-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="d6a20-111">Eventos de rastreamento e personalizados coletados por HockeyApp após a criação de saudação do hello HockeyApp ponte aplicativo poderá ser acessados desses recursos.</span><span class="sxs-lookup"><span data-stu-id="d6a20-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="d6a20-112">Vamos ver como tooset um desses aplicativos de ponte.</span><span class="sxs-lookup"><span data-stu-id="d6a20-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="d6a20-113">No HockeyApp, abra Configurações de Conta, [Tokens de API](https://rink.hockeyapp.net/manage/auth_tokens).</span><span class="sxs-lookup"><span data-stu-id="d6a20-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="d6a20-114">Crie um novo token ou reutilize um existente.</span><span class="sxs-lookup"><span data-stu-id="d6a20-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="d6a20-115">direitos mínimos Olá necessárias são "somente leitura".</span><span class="sxs-lookup"><span data-stu-id="d6a20-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="d6a20-116">Faça uma cópia da saudação API token.</span><span class="sxs-lookup"><span data-stu-id="d6a20-116">Take a copy of hello API token.</span></span>

![Obter um token da API do HockeyApp](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="d6a20-118">Portal do Microsoft Azure Olá aberto e [criar um recurso do Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d6a20-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="d6a20-119">Defina o tipo de aplicativo muito "Aplicativo de ponte HockeyApp":</span><span class="sxs-lookup"><span data-stu-id="d6a20-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![Novo recurso do Application Insights](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="d6a20-121">Não é necessário tooset um nome - isso será definido automaticamente do nome do HockeyApp hello.</span><span class="sxs-lookup"><span data-stu-id="d6a20-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="d6a20-122">Olá HockeyApp ponte campos são exibidos.</span><span class="sxs-lookup"><span data-stu-id="d6a20-122">hello HockeyApp bridge fields appear.</span></span> 

![Inserir campos de ponte](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="d6a20-124">Insira o token do HockeyApp Olá que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d6a20-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="d6a20-125">Essa ação preenche o menu de lista suspensa "HockeyApp aplicativo" hello com todos os seus aplicativos de HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="d6a20-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="d6a20-126">Selecione Olá um deseja toouse e restante Olá completa dos campos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6a20-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="d6a20-127">Abra o novo recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6a20-127">Open hello new resource.</span></span> 

<span data-ttu-id="d6a20-128">Observe que os dados de saudação leva um tempo toostart fluindo.</span><span class="sxs-lookup"><span data-stu-id="d6a20-128">Note that hello data takes a while toostart flowing.</span></span>

![Recurso do Application Insights aguardando os dados](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="d6a20-130">É isso!</span><span class="sxs-lookup"><span data-stu-id="d6a20-130">That’s it!</span></span> <span data-ttu-id="d6a20-131">Dados de rastreamento e personalizados coletados em seu aplicativo instrumentado HockeyApp daqui em diante agora também estão tooyou disponível no hello análise e recursos de exportação contínua do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d6a20-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="d6a20-132">Vamos examinar rapidamente cada um desses tooyou de recursos agora disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d6a20-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="d6a20-133">Análise</span><span class="sxs-lookup"><span data-stu-id="d6a20-133">Analytics</span></span>
<span data-ttu-id="d6a20-134">Análise é uma ferramenta poderosa para ad-hoc consultar seus dados, permitindo que você toodiagnose e analisar a telemetria e rapidamente descobre padrões e causas raiz.</span><span class="sxs-lookup"><span data-stu-id="d6a20-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Análise](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="d6a20-136">Saiba mais sobre o Analytics</span><span class="sxs-lookup"><span data-stu-id="d6a20-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="d6a20-137">Exportação contínua</span><span class="sxs-lookup"><span data-stu-id="d6a20-137">Continuous export</span></span>
<span data-ttu-id="d6a20-138">A exportação contínua permite tooexport seus dados em um contêiner de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6a20-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="d6a20-139">Isso é muito útil se você precisar tookeep seus dados por mais de um período de retenção Olá oferecido atualmente pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d6a20-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="d6a20-140">Você pode manter dados saudação no armazenamento de blob, processá-lo em um banco de dados SQL ou seu preferencial solução do data warehouse.</span><span class="sxs-lookup"><span data-stu-id="d6a20-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="d6a20-141">Saiba mais sobre a Exportação Contínua</span><span class="sxs-lookup"><span data-stu-id="d6a20-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="d6a20-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6a20-142">Next steps</span></span>
* [<span data-ttu-id="d6a20-143">Aplique a análise de dados de tooyour</span><span class="sxs-lookup"><span data-stu-id="d6a20-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

