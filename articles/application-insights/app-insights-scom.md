---
title: "Integração do SCOM com o Application Insights | Microsoft Docs"
description: "Se você for um usuário do SCOM, monitore o desempenho e diagnostique problemas com o Application Insights. Painéis abrangentes, alertas inteligentes, poderosas ferramentas de diagnóstico e de consultas de análise."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: 9c205465981fabdbb696cdc44f765532bbb992b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="3a7bf-104">Monitoramento de desempenho de aplicativos usando o Application Insights para SCOM</span><span class="sxs-lookup"><span data-stu-id="3a7bf-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="3a7bf-105">Se você usar o SCOM (System Center Operations Manager) para gerenciar seus servidores, poderá monitorar o desempenho e diagnosticar os problemas de desempenho com a ajuda do [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="3a7bf-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="3a7bf-106">O Application Insights monitora solicitações de entrada do seu aplicativo Web, chamadas REST e SQL de saída, exceções e rastreamentos de log.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="3a7bf-107">Ele fornece painéis com gráficos de métricas e alertas inteligentes, bem como poderosas consultas analíticas e pesquisa de diagnóstico sobre essa telemetria.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="3a7bf-108">Você pode ativar o monitoramento do Application Insights usando um pacote de gerenciamento do SCOM.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3a7bf-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3a7bf-109">Before you start</span></span>
<span data-ttu-id="3a7bf-110">Supomos que:</span><span class="sxs-lookup"><span data-stu-id="3a7bf-110">We assume:</span></span>

* <span data-ttu-id="3a7bf-111">Você esteja familiarizado com o SCOM e use o SCOM 2012 R2 ou 2016 para gerenciar os servidores Web do IIS.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="3a7bf-112">Você já tenha instalado nos servidores um aplicativo Web que você deseja monitorar com o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="3a7bf-113">A versão da estrutura de aplicativo seja o .NET 4.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="3a7bf-114">Você tem acesso a uma assinatura no [Microsoft Azure](https://azure.com) e pode entrar no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3a7bf-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3a7bf-115">Se sua organização já tiver uma assinatura, sua conta da Microsoft poderá ser adicionada.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="3a7bf-116">(A equipe de desenvolvimento pode criar o [SDK do Application Insights](app-insights-asp-net.md) no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="3a7bf-117">Essa instrumentação do tempo de compilação dá maior flexibilidade na escrita de telemetria personalizada.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="3a7bf-118">No entanto, não importa: você pode seguir as etapas descritas aqui, com ou sem o SDK interno).</span><span class="sxs-lookup"><span data-stu-id="3a7bf-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="3a7bf-119">(Uma vez) Instalar o pacote de gerenciamento do Application Insights</span><span class="sxs-lookup"><span data-stu-id="3a7bf-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="3a7bf-120">No computador em que você executa o Operations Manager:</span><span class="sxs-lookup"><span data-stu-id="3a7bf-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="3a7bf-121">Desinstale qualquer versão antiga do pacote de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="3a7bf-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="3a7bf-122">No Operations Manager, abra Administração, Pacotes de Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="3a7bf-123">Exclua a versão antiga.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-123">Delete the old version.</span></span>
2. <span data-ttu-id="3a7bf-124">Baixe e instale o pacote de gerenciamento do catálogo.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="3a7bf-125">Reinicie o Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="3a7bf-126">Criar um pacote de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="3a7bf-126">Create a management pack</span></span>
1. <span data-ttu-id="3a7bf-127">No Operations Manager, abra **Criação**, **.NET... com Application Insights**, **Assistente para Adicionar Monitoramento** e escolha novamente **.NET... com Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="3a7bf-128">Dê à configuração o nome do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-128">Name the configuration after your app.</span></span> <span data-ttu-id="3a7bf-129">(Você precisa instrumentar um aplicativo por vez).</span><span class="sxs-lookup"><span data-stu-id="3a7bf-129">(You have to instrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="3a7bf-130">Na mesma página do assistente, crie um novo pacote de gerenciamento ou selecione um pacote criado anteriormente para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="3a7bf-131">(O [pacote de gerenciamento](https://technet.microsoft.com/library/cc974491.aspx) do Application Insights é um modelo no qual você cria uma instância.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="3a7bf-132">Você pode reutilizar a mesma instância posteriormente).</span><span class="sxs-lookup"><span data-stu-id="3a7bf-132">You can reuse the same instance later.)</span></span>

    ![Na guia Propriedades Gerais, digite o nome do aplicativo.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="3a7bf-136">Escolha um aplicativo que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="3a7bf-137">O recurso de pesquisa procura entre aplicativos instalados nos servidores.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![Na guia O Que Monitorar, clique em Adicionar, digite parte do nome do aplicativo, clique em Pesquisar, escolha o aplicativo e, então, Adicionar, OK.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="3a7bf-139">O campo Escopo de monitoramento opcional pode ser usado para especificar um subconjunto de seus servidores se você não quiser monitorar o aplicativo em todos os servidores.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="3a7bf-140">Na próxima página do assistente, forneça suas credenciais para entrar no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="3a7bf-141">Nessa página, você deve escolher o recurso Application Insights onde deseja que os dados de telemetria sejam analisados e exibidos.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="3a7bf-142">Se o aplicativo tiver sido configurado para o Application Insights durante o desenvolvimento, selecione o recurso existente.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="3a7bf-143">Caso contrário, crie um novo recurso nomeado para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="3a7bf-144">Se houver outros aplicativos que sejam componentes do mesmo sistema, coloque-os no mesmo grupo de recursos para facilitar o gerenciamento da telemetria.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="3a7bf-145">Você pode alterar essas configurações posteriormente.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-145">You can change these settings later.</span></span>
     
     ![Na guia de configurações do Application Insights, clique em 'entrar' e forneça suas credenciais de conta da Microsoft para o Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="3a7bf-148">Conclua o assistente.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-148">Complete the wizard.</span></span>
   
    ![Clicar em Criar](./media/app-insights-scom/070.png)

<span data-ttu-id="3a7bf-150">Repita esse procedimento para cada aplicativo que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="3a7bf-151">Se você precisar alterar as configurações mais tarde, abra as propriedades do monitor na janela de criação novamente.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![Em Criação, selecione Monitoramento de Desempenho de Aplicativo .NET com o Application Insights, selecione o monitor e clique em Propriedades.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="3a7bf-153">Verificar o monitoramento</span><span class="sxs-lookup"><span data-stu-id="3a7bf-153">Verify monitoring</span></span>
<span data-ttu-id="3a7bf-154">O monitor instalado procura seu aplicativo em todos os servidores.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="3a7bf-155">Onde ele encontrar o aplicativo, configurará o Application Insights Status Monitor para monitorar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="3a7bf-156">Se necessário, primeiro ele instala o Monitor de Status no servidor.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="3a7bf-157">Você pode verificar quais instâncias do aplicativo encontrado:</span><span class="sxs-lookup"><span data-stu-id="3a7bf-157">You can verify which instances of the app it has found:</span></span>

![Em Monitoramento, abra o Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="3a7bf-159">Exibir a telemetria no Application Insights</span><span class="sxs-lookup"><span data-stu-id="3a7bf-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="3a7bf-160">No [portal do Azure](https://portal.azure.com), navegue até o recurso para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="3a7bf-161">Você [vê gráficos mostrando telemetria](app-insights-dashboards.md) do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="3a7bf-162">(Se ele ainda não tiver sido mostrado na página principal, clique no Live Metrics Stream).</span><span class="sxs-lookup"><span data-stu-id="3a7bf-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a7bf-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3a7bf-163">Next steps</span></span>
* <span data-ttu-id="3a7bf-164">[Configure um painel](app-insights-dashboards.md) para reunir os gráficos mais importantes que monitoram esse e outros aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3a7bf-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="3a7bf-165">Saiba mais sobre métricas</span><span class="sxs-lookup"><span data-stu-id="3a7bf-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="3a7bf-166">Configurar alertas</span><span class="sxs-lookup"><span data-stu-id="3a7bf-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="3a7bf-167">Diagnosticar problemas de desempenho</span><span class="sxs-lookup"><span data-stu-id="3a7bf-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="3a7bf-168">Consultas de análise poderosas</span><span class="sxs-lookup"><span data-stu-id="3a7bf-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="3a7bf-169">Testes de disponibilidade na Web</span><span class="sxs-lookup"><span data-stu-id="3a7bf-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

