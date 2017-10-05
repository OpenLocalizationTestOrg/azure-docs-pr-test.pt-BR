---
title: Criar um novo recurso do Azure Application Insights | Microsoft Docs
description: Configure manualmente o monitoramento do Application Insights para um novo aplicativo em tempo real.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 5f8814ee943424c1c278ab3732129d4459f83819
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="e9d99-103">Criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="e9d99-103">Create an Application Insights resource</span></span>
<span data-ttu-id="e9d99-104">O Azure Application Insights exibe dados sobre o seu aplicativo em um *recurso* do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e9d99-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="e9d99-105">Por isso, criar um novo recurso faz parte da [configuração do Application Insights para monitorar um novo aplicativo][start].</span><span class="sxs-lookup"><span data-stu-id="e9d99-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="e9d99-106">Em muitos casos, criar um recurso pode ser feito automaticamente pelo IDE.</span><span class="sxs-lookup"><span data-stu-id="e9d99-106">In many cases, creating a resource can be done automatically by the IDE.</span></span> <span data-ttu-id="e9d99-107">Porém, em alguns casos, você criará um recurso manualmente, por exemplo, para ter recursos separados para versões de desenvolvimento e produção do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9d99-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="e9d99-108">Depois de criar o recurso, você pode obter sua chave de instrumentação e usá-la para configurar o SDK no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9d99-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="e9d99-109">A chave de recurso vincula a telemetria para o recurso.</span><span class="sxs-lookup"><span data-stu-id="e9d99-109">The resource key links the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="e9d99-110">Inscreva-se no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e9d99-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="e9d99-111">Se você ainda não tiver uma [conta da Microsoft, obtenha uma agora mesmo](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="e9d99-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="e9d99-112">(Se usar serviços como Outlook.com, OneDrive, Windows Phone ou XBox Live, você já tem uma conta da Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="e9d99-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="e9d99-113">Você também precisa de uma assinatura do [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9d99-113">You also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="e9d99-114">Se sua equipe ou organização tem uma assinatura do Azure, o proprietário pode adicioná-lo a ela usando seu Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="e9d99-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="e9d99-115">Você será cobrado apenas pelo que usa.</span><span class="sxs-lookup"><span data-stu-id="e9d99-115">You're only charged for what you use.</span></span> <span data-ttu-id="e9d99-116">Permite que o plano básico padrão para uma determinada quantidade de uso experimental gratuita.</span><span class="sxs-lookup"><span data-stu-id="e9d99-116">The default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="e9d99-117">Quando você tem acesso a uma assinatura, entre no Application Insights em [http://portal.azure.com](https://portal.azure.com) e use sua Live ID para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="e9d99-117">When you've got access to a subscription, log in to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="e9d99-118">Criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="e9d99-118">Create an Application Insights resource</span></span>
<span data-ttu-id="e9d99-119">No [portal.azure.com](https://portal.azure.com), adicione um recurso do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="e9d99-119">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Clique em Novo, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="e9d99-121">O **tipo de aplicativo** afeta o que você vê na folha de visão geral e as propriedades disponíveis no [explorador de métricas][metrics].</span><span class="sxs-lookup"><span data-stu-id="e9d99-121">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="e9d99-122">Se você não vir seu tipo de aplicativo, selecione Geral.</span><span class="sxs-lookup"><span data-stu-id="e9d99-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="e9d99-123">**Assinatura** é a sua conta de pagamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="e9d99-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="e9d99-124">**Grupo de recursos** é uma conveniência para o gerenciamento de propriedades, como controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="e9d99-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="e9d99-125">Se você já criou outros recursos do Azure, poderá optar por colocar esse novo recurso no mesmo grupo.</span><span class="sxs-lookup"><span data-stu-id="e9d99-125">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="e9d99-126">**Local** é onde podemos manter seus dados.</span><span class="sxs-lookup"><span data-stu-id="e9d99-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="e9d99-127">**Adicionar ao painel** coloca um bloco de acesso rápido para o recurso em sua Página Inicial do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9d99-127">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="e9d99-128">Recomendável.</span><span class="sxs-lookup"><span data-stu-id="e9d99-128">Recommended.</span></span>

<span data-ttu-id="e9d99-129">Quando seu aplicativo tiver sido criado, uma nova folha será aberta.</span><span class="sxs-lookup"><span data-stu-id="e9d99-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="e9d99-130">Essa folha mostra os dados de uso e de desempenho do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9d99-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="e9d99-131">Para retornar a ele na próxima vez que fizer logon no Azure, procure pelo bloco de início rápido do aplicativo na Tela Inicial.</span><span class="sxs-lookup"><span data-stu-id="e9d99-131">To get back to it next time you log in to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="e9d99-132">Ou então, clique em Procurar para localizá-lo.</span><span class="sxs-lookup"><span data-stu-id="e9d99-132">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="e9d99-133">Copiar a chave de instrumentação</span><span class="sxs-lookup"><span data-stu-id="e9d99-133">Copy the instrumentation key</span></span>
<span data-ttu-id="e9d99-134">A chave de instrumentação identifica o recurso que você criou.</span><span class="sxs-lookup"><span data-stu-id="e9d99-134">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="e9d99-135">É preciso fornecê-la ao SDK.</span><span class="sxs-lookup"><span data-stu-id="e9d99-135">You need it to give to the SDK.</span></span>

![Clique em Essentials, clique na Chave de Instrumentação, CTRL+C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="e9d99-137">Instalar o SDK em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e9d99-137">Install the SDK in your app</span></span>
<span data-ttu-id="e9d99-138">Instale o SDK do Application Insights SDK no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9d99-138">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="e9d99-139">Esta etapa depende muito do tipo do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9d99-139">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="e9d99-140">Use a chave de instrumentação para configurar o [SDK instalado no seu aplicativo][start].</span><span class="sxs-lookup"><span data-stu-id="e9d99-140">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="e9d99-141">O SDK inclui módulos padrão que enviam telemetria sem precisar escrever nenhum código.</span><span class="sxs-lookup"><span data-stu-id="e9d99-141">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="e9d99-142">Para rastrear ações do usuário ou diagnosticar problemas mais detalhadamente, [use a API][api] para enviar sua própria telemetria.</span><span class="sxs-lookup"><span data-stu-id="e9d99-142">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <span data-ttu-id="e9d99-143"><a name="monitor"></a>Consultar os dados de telemetria</span><span class="sxs-lookup"><span data-stu-id="e9d99-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="e9d99-144">Feche a folha de início rápido para retornar para a folha de aplicativo no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9d99-144">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="e9d99-145">Clique no bloco Pesquisa para ver a [Pesquisa de Diagnóstico][diagnostic], onde os primeiros eventos serão exibidos.</span><span class="sxs-lookup"><span data-stu-id="e9d99-145">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events appear.</span></span> 

<span data-ttu-id="e9d99-146">Se você estiver esperando mais dados, clique em **Atualizar** depois de alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="e9d99-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="e9d99-147">Criando um recurso automaticamente</span><span class="sxs-lookup"><span data-stu-id="e9d99-147">Creating a resource automatically</span></span>
<span data-ttu-id="e9d99-148">Você pode escrever um [script do PowerShell](app-insights-powershell.md) para criar um recurso automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e9d99-148">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9d99-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9d99-149">Next steps</span></span>
* [<span data-ttu-id="e9d99-150">Criar um painel</span><span class="sxs-lookup"><span data-stu-id="e9d99-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="e9d99-151">Pesquisa de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e9d99-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="e9d99-152">Explorar métricas</span><span class="sxs-lookup"><span data-stu-id="e9d99-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="e9d99-153">Escrever consultas do Analytics</span><span class="sxs-lookup"><span data-stu-id="e9d99-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

