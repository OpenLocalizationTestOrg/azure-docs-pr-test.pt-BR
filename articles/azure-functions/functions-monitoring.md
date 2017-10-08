---
title: "aaaMonitoring funções do Azure | Microsoft Docs"
description: "Saiba como toomonitor as funções do Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="192af-104">Monitoramento do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="192af-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="192af-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="192af-105">Overview</span></span> 


<span data-ttu-id="192af-106">Olá **Monitor** guia para cada função permite que você tooreview cada execução de uma função.</span><span class="sxs-lookup"><span data-stu-id="192af-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![guia Monitorar do Azure Functions](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="192af-108">Clicando em uma execução permite que você tooreview Olá duração, dados de entrada, erros e arquivos de log associados.</span><span class="sxs-lookup"><span data-stu-id="192af-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="192af-109">Tudo isso é útil na depuração e no ajuste de desempenho de suas funções.</span><span class="sxs-lookup"><span data-stu-id="192af-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="192af-110">Ao usar o hello [consumo de plano de hospedagem](functions-overview.md#pricing) para funções do Azure, Olá **monitoramento** lado a lado na folha de visão geral do aplicativo de função hello não mostrarão nenhum dado.</span><span class="sxs-lookup"><span data-stu-id="192af-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="192af-111">Isso ocorre porque a plataforma de saudação dimensiona dinamicamente e gerencia instâncias de computação, portanto, essas métricas não são significativas em um plano de consumo.</span><span class="sxs-lookup"><span data-stu-id="192af-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="192af-112">uso de saudação toomonitor de seus aplicativos de função, você deve usar em vez disso, as diretrizes de Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="192af-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="192af-113">Olá captura de tela a seguir mostra um exemplo:</span><span class="sxs-lookup"><span data-stu-id="192af-113">hello following screen-shot shows an example:</span></span>
> 
> ![Monitoramento na folha de recursos principais de saudação](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="192af-115">Monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="192af-115">Real-time monitoring</span></span>

<span data-ttu-id="192af-116">Para acessar o monitoramento em tempo real, clique na **transmissão de evento ao vivo**, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="192af-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Opção de fluxo de evento para o guia do monitor de saudação de Live](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="192af-118">fluxo de evento ao vivo Hello serão colocados no gráfico em uma nova guia do navegador conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="192af-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Exemplo de transmissão de evento ao vivo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="192af-120">Há um problema conhecido que pode fazer com que seu toobe de toofail dados preenchido.</span><span class="sxs-lookup"><span data-stu-id="192af-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="192af-121">Se você enfrentar isso, talvez seja necessário tooclose Olá navegador guia contendo Olá ao vivo fluxo de eventos e clique **fluxo de evento ao vivo** novamente tooallow-tooproperly popular com seus dados de fluxo de evento.</span><span class="sxs-lookup"><span data-stu-id="192af-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="192af-122">fluxo de evento ao vivo Hello serão graph Olá estatísticas para a função a seguir:</span><span class="sxs-lookup"><span data-stu-id="192af-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="192af-123">Execuções iniciadas por segundo</span><span class="sxs-lookup"><span data-stu-id="192af-123">Executions started per second</span></span>
* <span data-ttu-id="192af-124">Execuções concluídas por segundo</span><span class="sxs-lookup"><span data-stu-id="192af-124">Executions completed per second</span></span>
* <span data-ttu-id="192af-125">Execuções com falha por segundo</span><span class="sxs-lookup"><span data-stu-id="192af-125">Executions failed per second</span></span>
* <span data-ttu-id="192af-126">Tempo médio de execução em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="192af-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="192af-127">Essas estatísticas são em tempo real, mas Olá real de gráficos de dados de execução Olá pode ter cerca de 10 segundos de latência.</span><span class="sxs-lookup"><span data-stu-id="192af-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="192af-128">Monitoramento de arquivos de log de uma linha de comando</span><span class="sxs-lookup"><span data-stu-id="192af-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="192af-129">Você pode transmitir uma sessão de linha de comando de tooa de arquivos de log em uma estação de trabalho local usando hello Azure Interface de linha de comando (CLI) ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="192af-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="192af-130">Monitoramento de arquivos de log de aplicativo de função com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="192af-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="192af-131">tooget iniciado, [instalar Olá CLI do Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="192af-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="192af-132">Efetue login em sua conta do Azure usando os seguintes Olá comando ou qualquer Olá outras opções abordadas, [login tooAzure de saudação CLI do Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="192af-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="192af-133">Modo de gerenciamento de serviço de CLI do Azure (ASM) tooenable do comando de uso a seguir de saudação:.</span><span class="sxs-lookup"><span data-stu-id="192af-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="192af-134">Se você tiver várias assinaturas, use Olá toolist comandos a seguir, suas assinaturas e o conjunto Olá assinatura toohello assinatura atual que contém seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="192af-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="192af-135">Olá comando a seguir será de fluxo de arquivos de log Olá sua função aplicativo toohello da linha de comando:</span><span class="sxs-lookup"><span data-stu-id="192af-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="192af-136">Monitoramento de arquivos de log do aplicativo de funções com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="192af-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="192af-137">tooget iniciado, [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="192af-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="192af-138">Adicione sua conta do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="192af-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="192af-139">Se você tiver várias assinaturas, você pode listá-los por nome com hello toosee de comando a seguir se Olá correto de assinatura é hello atualmente selecionado com base em `IsCurrent` propriedade:</span><span class="sxs-lookup"><span data-stu-id="192af-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="192af-140">Se você precisar tooset Olá assinatura ativa toohello uma que contém seu aplicativo de função, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="192af-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="192af-141">Fluxo de sessão do PowerShell Olá logs tooyour com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="192af-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="192af-142">Para obter mais informações, consulte muito[como: fluxo de logs para aplicativos web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="192af-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="192af-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="192af-143">Next steps</span></span>
<span data-ttu-id="192af-144">Para obter mais informações, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="192af-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="192af-145">Testando uma função</span><span class="sxs-lookup"><span data-stu-id="192af-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="192af-146">Dimensionar uma função</span><span class="sxs-lookup"><span data-stu-id="192af-146">Scale a function</span></span>](functions-scale.md)

