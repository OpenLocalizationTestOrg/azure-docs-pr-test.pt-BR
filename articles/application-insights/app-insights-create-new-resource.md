---
title: aaaCreate um novo recurso do Application Insights do Azure | Microsoft Docs
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
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="6487a-103">Criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="6487a-103">Create an Application Insights resource</span></span>
<span data-ttu-id="6487a-104">O Azure Application Insights exibe dados sobre o seu aplicativo em um *recurso* do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6487a-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="6487a-105">Criando um novo recurso, portanto, é parte de [Configurando um novo aplicativo Application Insights toomonitor][start].</span><span class="sxs-lookup"><span data-stu-id="6487a-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="6487a-106">Em muitos casos, criar um recurso pode ser feito automaticamente pelo Olá IDE.</span><span class="sxs-lookup"><span data-stu-id="6487a-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="6487a-107">Mas em alguns casos, você cria um recurso manualmente - por exemplo, toohave de recursos separado para desenvolvimento e produção compilações do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6487a-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="6487a-108">Depois que você criou o recurso hello, você obter sua chave de instrumentação e usa esse Olá tooconfigure SDK no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6487a-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="6487a-109">links de chave de recurso Olá Olá recursos de toohello de telemetria.</span><span class="sxs-lookup"><span data-stu-id="6487a-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="6487a-110">Inscreva-se tooMicrosoft do Azure</span><span class="sxs-lookup"><span data-stu-id="6487a-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="6487a-111">Se você ainda não tiver uma [conta da Microsoft, obtenha uma agora mesmo](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="6487a-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="6487a-112">(Se usar serviços como Outlook.com, OneDrive, Windows Phone ou XBox Live, você já tem uma conta da Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="6487a-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="6487a-113">Você também precisa de uma assinatura muito[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="6487a-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="6487a-114">Se sua equipe ou organização tiver uma assinatura do Azure, Olá proprietário pode adicionar você tooit, usando seu Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="6487a-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="6487a-115">Você será cobrado apenas pelo que usa.</span><span class="sxs-lookup"><span data-stu-id="6487a-115">You're only charged for what you use.</span></span> <span data-ttu-id="6487a-116">plano básico do saudação padrão permite que uma determinada quantidade de uso experimental gratuita.</span><span class="sxs-lookup"><span data-stu-id="6487a-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="6487a-117">Quando você tem acesso tooa assinatura, faça logon no Insights tooApplication em [http://portal.azure.com](https://portal.azure.com)e usar toologin seu Live ID.</span><span class="sxs-lookup"><span data-stu-id="6487a-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="6487a-118">Criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="6487a-118">Create an Application Insights resource</span></span>
<span data-ttu-id="6487a-119">Em Olá [portal.azure.com](https://portal.azure.com), adicionar um recurso do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="6487a-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Clique em Novo, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="6487a-121">**Tipo de aplicativo** afeta o que você vê na folha de visão geral de saudação e as propriedades de saudação disponíveis no [explorer métrica][metrics].</span><span class="sxs-lookup"><span data-stu-id="6487a-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="6487a-122">Se você não vir seu tipo de aplicativo, selecione Geral.</span><span class="sxs-lookup"><span data-stu-id="6487a-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="6487a-123">**Assinatura** é a sua conta de pagamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="6487a-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="6487a-124">**Grupo de recursos** é uma conveniência para o gerenciamento de propriedades, como controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="6487a-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="6487a-125">Se você já criou outros recursos do Azure, você pode escolher tooput este novo recurso Olá mesmo grupo.</span><span class="sxs-lookup"><span data-stu-id="6487a-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="6487a-126">**Local** é onde podemos manter seus dados.</span><span class="sxs-lookup"><span data-stu-id="6487a-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="6487a-127">**PIN toodashboard** coloca um bloco de acesso rápido para o recurso em sua Home page do Azure.</span><span class="sxs-lookup"><span data-stu-id="6487a-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="6487a-128">Recomendável.</span><span class="sxs-lookup"><span data-stu-id="6487a-128">Recommended.</span></span>

<span data-ttu-id="6487a-129">Quando seu aplicativo tiver sido criado, uma nova folha será aberta.</span><span class="sxs-lookup"><span data-stu-id="6487a-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="6487a-130">Essa folha mostra os dados de uso e de desempenho do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6487a-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="6487a-131">tooit back tooget próxima vez que você fizer logon no tooAzure, procure o bloco de início rápido do aplicativo em Olá iniciar placa (tela inicial).</span><span class="sxs-lookup"><span data-stu-id="6487a-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="6487a-132">Ou clique em Procurar toofind-lo.</span><span class="sxs-lookup"><span data-stu-id="6487a-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="6487a-133">Copie a chave de instrumentação Olá</span><span class="sxs-lookup"><span data-stu-id="6487a-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="6487a-134">chave de instrumentação Olá identifica o recurso de saudação que você criou.</span><span class="sxs-lookup"><span data-stu-id="6487a-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="6487a-135">Necessário toogive toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="6487a-135">You need it toogive toohello SDK.</span></span>

![Clique em Essentials, Olá chave de instrumentação, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="6487a-137">Instalar Olá SDK em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="6487a-137">Install hello SDK in your app</span></span>
<span data-ttu-id="6487a-138">Instale SDK do Application Insights de saudação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6487a-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="6487a-139">Esta etapa depende muito do tipo de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6487a-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="6487a-140">Use Olá instrumentação chave tooconfigure [Olá SDK que você instala em seu aplicativo][start].</span><span class="sxs-lookup"><span data-stu-id="6487a-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="6487a-141">Olá SDK inclui módulos padrão que enviar telemetria sem a necessidade de toowrite qualquer código.</span><span class="sxs-lookup"><span data-stu-id="6487a-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="6487a-142">ações do usuário tootrack ou diagnosticar problemas em mais detalhes, [usar Olá API] [ api] toosend sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="6487a-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="6487a-143"><a name="monitor"></a>Consultar os dados de telemetria</span><span class="sxs-lookup"><span data-stu-id="6487a-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="6487a-144">Fechar Olá rápido iniciar folha de aplicativos folha tooreturn tooyour Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6487a-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="6487a-145">Clique em Olá pesquisa bloco toosee [pesquisa diagnóstico][diagnostic], onde os eventos primeiro Olá aparecem.</span><span class="sxs-lookup"><span data-stu-id="6487a-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="6487a-146">Se você estiver esperando mais dados, clique em **Atualizar** depois de alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="6487a-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="6487a-147">Criando um recurso automaticamente</span><span class="sxs-lookup"><span data-stu-id="6487a-147">Creating a resource automatically</span></span>
<span data-ttu-id="6487a-148">Você pode escrever um [script do PowerShell](app-insights-powershell.md) toocreate um recurso automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6487a-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6487a-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6487a-149">Next steps</span></span>
* [<span data-ttu-id="6487a-150">Criar um painel</span><span class="sxs-lookup"><span data-stu-id="6487a-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="6487a-151">Pesquisa de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="6487a-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="6487a-152">Explorar métricas</span><span class="sxs-lookup"><span data-stu-id="6487a-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="6487a-153">Escrever consultas do Analytics</span><span class="sxs-lookup"><span data-stu-id="6487a-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

