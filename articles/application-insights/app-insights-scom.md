---
title: "a integração com o Application Insights aaaSCOM | Microsoft Docs"
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
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="03fde-104">Monitoramento de desempenho de aplicativos usando o Application Insights para SCOM</span><span class="sxs-lookup"><span data-stu-id="03fde-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="03fde-105">Se você usar o System Center Operations Manager (SCOM) toomanage seus servidores, você pode monitorar o desempenho e diagnosticar problemas de desempenho com a Ajuda de saudação do [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="03fde-105">If you use System Center Operations Manager (SCOM) toomanage your servers, you can monitor performance and diagnose performance issues with hello help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="03fde-106">O Application Insights monitora solicitações de entrada do seu aplicativo Web, chamadas REST e SQL de saída, exceções e rastreamentos de log.</span><span class="sxs-lookup"><span data-stu-id="03fde-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="03fde-107">Ele fornece painéis com gráficos de métricas e alertas inteligentes, bem como poderosas consultas analíticas e pesquisa de diagnóstico sobre essa telemetria.</span><span class="sxs-lookup"><span data-stu-id="03fde-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="03fde-108">Você pode ativar o monitoramento do Application Insights usando um pacote de gerenciamento do SCOM.</span><span class="sxs-lookup"><span data-stu-id="03fde-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="03fde-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="03fde-109">Before you start</span></span>
<span data-ttu-id="03fde-110">Supomos que:</span><span class="sxs-lookup"><span data-stu-id="03fde-110">We assume:</span></span>

* <span data-ttu-id="03fde-111">Você está familiarizado com o SCOM e usar o SCOM 2012 R2 ou 2016 toomanage o IIS servidores da web.</span><span class="sxs-lookup"><span data-stu-id="03fde-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 toomanage your IIS web servers.</span></span>
* <span data-ttu-id="03fde-112">Você já tiver instalado nos servidores de um aplicativo web que você deseja toomonitor com o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="03fde-112">You have already installed on your servers a web application that you want toomonitor with Application Insights.</span></span>
* <span data-ttu-id="03fde-113">A versão da estrutura de aplicativo seja o .NET 4.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="03fde-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="03fde-114">Você tem acesso tooa assinatura em [Microsoft Azure](https://azure.com) e pode entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03fde-114">You have access tooa subscription in [Microsoft Azure](https://azure.com) and can sign in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="03fde-115">Sua organização pode ter uma assinatura e pode adicionar sua tooit de conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="03fde-115">Your organization may have a subscription, and can add your Microsoft account tooit.</span></span>

<span data-ttu-id="03fde-116">(equipe de desenvolvimento Olá pode criar hello [SDK do Application Insights](app-insights-asp-net.md) no aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="03fde-116">(hello development team might build hello [Application Insights SDK](app-insights-asp-net.md) into hello web app.</span></span> <span data-ttu-id="03fde-117">Essa instrumentação do tempo de compilação dá maior flexibilidade na escrita de telemetria personalizada.</span><span class="sxs-lookup"><span data-stu-id="03fde-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="03fde-118">No entanto, não importa: você pode seguir etapas Olá descritas aqui, com ou sem Olá SDK incorporado.)</span><span class="sxs-lookup"><span data-stu-id="03fde-118">However, it doesn't matter: you can follow hello steps described here either with or without hello SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="03fde-119">(Uma vez) Instalar o pacote de gerenciamento do Application Insights</span><span class="sxs-lookup"><span data-stu-id="03fde-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="03fde-120">Na máquina de saudação onde você executa o Operations Manager:</span><span class="sxs-lookup"><span data-stu-id="03fde-120">On hello machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="03fde-121">Desinstale qualquer versão antiga do pacote de gerenciamento de saudação:</span><span class="sxs-lookup"><span data-stu-id="03fde-121">Uninstall any old version of hello management pack:</span></span>
   1. <span data-ttu-id="03fde-122">No Operations Manager, abra Administração, Pacotes de Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="03fde-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="03fde-123">Exclua a versão antiga do hello.</span><span class="sxs-lookup"><span data-stu-id="03fde-123">Delete hello old version.</span></span>
2. <span data-ttu-id="03fde-124">Baixe e instale o pacote de gerenciamento de saudação do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="03fde-124">Download and install hello management pack from hello catalog.</span></span>
3. <span data-ttu-id="03fde-125">Reinicie o Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="03fde-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="03fde-126">Criar um pacote de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="03fde-126">Create a management pack</span></span>
1. <span data-ttu-id="03fde-127">No Operations Manager, abra **Criação**, **.NET... com Application Insights**, **Assistente para Adicionar Monitoramento** e escolha novamente **.NET... com Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="03fde-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="03fde-128">Configuração de saudação do nome depois de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03fde-128">Name hello configuration after your app.</span></span> <span data-ttu-id="03fde-129">(Necessário tooinstrument um aplicativo por vez.)</span><span class="sxs-lookup"><span data-stu-id="03fde-129">(You have tooinstrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="03fde-130">Olá na mesma página do assistente, crie um novo gerenciamento de pacote, ou selecione um pacote que você criou anteriormente para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="03fde-130">On hello same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="03fde-131">(Olá Application Insights [pacote de gerenciamento](https://technet.microsoft.com/library/cc974491.aspx) é um modelo, na qual você cria uma instância.</span><span class="sxs-lookup"><span data-stu-id="03fde-131">(hello Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="03fde-132">Você pode reutilizar Olá mesmo instância mais tarde.)</span><span class="sxs-lookup"><span data-stu-id="03fde-132">You can reuse hello same instance later.)</span></span>

    ![Na guia Propriedades gerais de Olá, digite o nome de saudação do aplicativo hello.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="03fde-136">Escolha um aplicativo que você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="03fde-136">Choose one app that you want toomonitor.</span></span> <span data-ttu-id="03fde-137">o recurso de pesquisa Olá pesquisa entre aplicativos instalados em seus servidores.</span><span class="sxs-lookup"><span data-stu-id="03fde-137">hello search feature searches among apps installed on your servers.</span></span>
   
    ![Na guia que tooMonitor, clique em Adicionar, digite parte do nome do aplicativo hello, clique em Pesquisar, escolha o aplicativo hello e, em seguida, adicionar, Okey.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="03fde-139">campo de escopo de monitoramento opcional Olá pode ser usado toospecify um subconjunto dos seus servidores, se você não quiser toomonitor Olá aplicativo em todos os servidores.</span><span class="sxs-lookup"><span data-stu-id="03fde-139">hello optional Monitoring scope field can be used toospecify a subset of your servers, if you don't want toomonitor hello app in all servers.</span></span>
2. <span data-ttu-id="03fde-140">Na próxima página do assistente hello, primeiro você deve fornecer toosign suas credenciais no tooMicrosoft do Azure.</span><span class="sxs-lookup"><span data-stu-id="03fde-140">On hello next wizard page, you must first provide your credentials toosign in tooMicrosoft Azure.</span></span>
   
    <span data-ttu-id="03fde-141">Nessa página, você escolher o recurso do Application Insights Olá onde você deseja toobe de dados de telemetria Olá analisados e exibidos.</span><span class="sxs-lookup"><span data-stu-id="03fde-141">On this page, you choose hello Application Insights resource where you want hello telemetry data toobe analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="03fde-142">Se o aplicativo hello foi configurado para o Application Insights durante o desenvolvimento, selecione o recurso existente.</span><span class="sxs-lookup"><span data-stu-id="03fde-142">If hello application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="03fde-143">Caso contrário, crie um novo recurso chamado para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="03fde-143">Otherwise, create a new resource named for hello app.</span></span> <span data-ttu-id="03fde-144">Se houver outros aplicativos que são componentes de saudação mesmo sistema, colocá-los em Olá mesmo grupo de recursos, toomake acesso toohello telemetria mais fácil toomanage.</span><span class="sxs-lookup"><span data-stu-id="03fde-144">If there are other apps that are components of hello same system, put them in hello same resource group, toomake access toohello telemetry easier toomanage.</span></span>
     
     <span data-ttu-id="03fde-145">Você pode alterar essas configurações posteriormente.</span><span class="sxs-lookup"><span data-stu-id="03fde-145">You can change these settings later.</span></span>
     
     ![Na guia de configurações do Application Insights, clique em 'entrar' e forneça suas credenciais de conta da Microsoft para o Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="03fde-148">Assistente de saudação concluída.</span><span class="sxs-lookup"><span data-stu-id="03fde-148">Complete hello wizard.</span></span>
   
    ![Clicar em Criar](./media/app-insights-scom/070.png)

<span data-ttu-id="03fde-150">Repita esse procedimento para cada aplicativo que você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="03fde-150">Repeat this procedure for each app that you want toomonitor.</span></span>

<span data-ttu-id="03fde-151">Se você precisar de configurações de toochange mais tarde, abra novamente as propriedades de saudação do monitor de saudação da janela de criação de saudação.</span><span class="sxs-lookup"><span data-stu-id="03fde-151">If you need toochange settings later, re-open hello properties of hello monitor from hello Authoring window.</span></span>

![Em Criação, selecione Monitoramento de Desempenho de Aplicativo .NET com o Application Insights, selecione o monitor e clique em Propriedades.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="03fde-153">Verificar o monitoramento</span><span class="sxs-lookup"><span data-stu-id="03fde-153">Verify monitoring</span></span>
<span data-ttu-id="03fde-154">monitor de saudação que você instalou pesquisas para seu aplicativo em todos os servidores.</span><span class="sxs-lookup"><span data-stu-id="03fde-154">hello monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="03fde-155">Onde encontrar o aplicativo hello, ele configura o Application Insights Status Monitor toomonitor Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03fde-155">Where it finds hello app, it configures Application Insights Status Monitor toomonitor hello app.</span></span> <span data-ttu-id="03fde-156">Se necessário, ele instala primeiro Status Monitor no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="03fde-156">If necessary, it first installs Status Monitor on hello server.</span></span>

<span data-ttu-id="03fde-157">Você pode verificar quais instâncias do aplicativo hello encontrado:</span><span class="sxs-lookup"><span data-stu-id="03fde-157">You can verify which instances of hello app it has found:</span></span>

![Em Monitoramento, abra o Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="03fde-159">Exibir a telemetria no Application Insights</span><span class="sxs-lookup"><span data-stu-id="03fde-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="03fde-160">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello recursos para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03fde-160">In hello [Azure portal](https://portal.azure.com), browse toohello resource for your app.</span></span> <span data-ttu-id="03fde-161">Você [vê gráficos mostrando telemetria](app-insights-dashboards.md) do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03fde-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="03fde-162">(Se ele ainda não mostrado para cima na página principal do hello ainda, clique em fluxo ao vivo de métricas.)</span><span class="sxs-lookup"><span data-stu-id="03fde-162">(If it hasn't shown up on hello main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="03fde-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03fde-163">Next steps</span></span>
* <span data-ttu-id="03fde-164">[Configurar um painel](app-insights-dashboards.md) gráficos mais importantes do hello juntos toobring este e outros aplicativos de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="03fde-164">[Set up a dashboard](app-insights-dashboards.md) toobring together hello most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="03fde-165">Saiba mais sobre métricas</span><span class="sxs-lookup"><span data-stu-id="03fde-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="03fde-166">Configurar alertas</span><span class="sxs-lookup"><span data-stu-id="03fde-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="03fde-167">Diagnosticar problemas de desempenho</span><span class="sxs-lookup"><span data-stu-id="03fde-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="03fde-168">Consultas de análise poderosas</span><span class="sxs-lookup"><span data-stu-id="03fde-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="03fde-169">Testes de disponibilidade na Web</span><span class="sxs-lookup"><span data-stu-id="03fde-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

