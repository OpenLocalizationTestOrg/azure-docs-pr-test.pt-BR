---
title: Monitoramento do Azure Functions | Microsoft Docs
description: Saiba como monitorar o Azure Functions.
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
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="c761c-104">Monitoramento do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c761c-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="c761c-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c761c-105">Overview</span></span> 


<span data-ttu-id="c761c-106">A guia **Monitorar** de cada função permite revisar cada execução de uma função.</span><span class="sxs-lookup"><span data-stu-id="c761c-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![guia Monitorar do Azure Functions](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="c761c-108">Ao clicar em uma execução, é possível rever a duração, os dados de entrada, os erros e os arquivos de log associados.</span><span class="sxs-lookup"><span data-stu-id="c761c-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="c761c-109">Tudo isso é útil na depuração e no ajuste de desempenho de suas funções.</span><span class="sxs-lookup"><span data-stu-id="c761c-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="c761c-110">Ao usar o [Plano de hospedagem de consumo](functions-overview.md#pricing) do Azure Functions, o bloco **Monitoramento** na folha de visão geral do Aplicativo de Funções não mostrará dados.</span><span class="sxs-lookup"><span data-stu-id="c761c-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="c761c-111">Isso porque a plataforma escala e gerencia dinamicamente instâncias de computação para você, de modo que essas métricas não são significativas em um plano de consumo.</span><span class="sxs-lookup"><span data-stu-id="c761c-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="c761c-112">Para monitorar o uso dos Aplicativos de Funções, você deve usar as orientações neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c761c-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="c761c-113">A captura de tela a seguir mostra um exemplo:</span><span class="sxs-lookup"><span data-stu-id="c761c-113">The following screen-shot shows an example:</span></span>
> 
> ![Monitoramento na folha de recursos principais](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="c761c-115">Monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="c761c-115">Real-time monitoring</span></span>

<span data-ttu-id="c761c-116">Para acessar o monitoramento em tempo real, clique na **transmissão de evento ao vivo**, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c761c-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Opção de transmissão de evento ao vivo para a guia monitorar](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="c761c-118">A transmissão de evento ao vivo será mostrada em gráfico em uma nova guia do navegador, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c761c-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Exemplo de transmissão de evento ao vivo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="c761c-120">Há um problema conhecido que pode causar falha na população dos dados.</span><span class="sxs-lookup"><span data-stu-id="c761c-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="c761c-121">Caso você enfrente esse problema, talvez seja preciso fechar a guia do navegador que contém a transmissão de evento ao vivo e clicar na **transmissão de evento ao vivo** novamente para permitir que os dados da transmissão do evento sejam populados corretamente.</span><span class="sxs-lookup"><span data-stu-id="c761c-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="c761c-122">A transmissão de evento ao vivo apresentará em gráfico as seguintes estatísticas para sua função:</span><span class="sxs-lookup"><span data-stu-id="c761c-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="c761c-123">Execuções iniciadas por segundo</span><span class="sxs-lookup"><span data-stu-id="c761c-123">Executions started per second</span></span>
* <span data-ttu-id="c761c-124">Execuções concluídas por segundo</span><span class="sxs-lookup"><span data-stu-id="c761c-124">Executions completed per second</span></span>
* <span data-ttu-id="c761c-125">Execuções com falha por segundo</span><span class="sxs-lookup"><span data-stu-id="c761c-125">Executions failed per second</span></span>
* <span data-ttu-id="c761c-126">Tempo médio de execução em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="c761c-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="c761c-127">Essas estatísticas são em tempo real, mas o gráfico real dos dados de execução pode ter aproximadamente 10 segundos de latência.</span><span class="sxs-lookup"><span data-stu-id="c761c-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="c761c-128">Monitoramento de arquivos de log de uma linha de comando</span><span class="sxs-lookup"><span data-stu-id="c761c-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="c761c-129">Você pode transmitir arquivos de log para uma sessão de linha de comando em uma estação de trabalho local usando a CLI (Interface de Linha de Comando) do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c761c-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="c761c-130">Monitoramento de arquivos de log do aplicativo de funções com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c761c-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="c761c-131">Para começar, [instale a CLI do Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="c761c-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="c761c-132">Faça logon na sua conta do Azure usando o comando a seguir, ou qualquer uma das outras opções abordadas em [Fazer logon no Azure usando a CLI do Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c761c-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="c761c-133">Use o comando a seguir para habilitar o modo ASM (Gerenciamento de Serviço da CLI do Azure):</span><span class="sxs-lookup"><span data-stu-id="c761c-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="c761c-134">Se você tiver várias assinaturas, use os comandos a seguir para listá-las e definir a assinatura atual para aquela que contém seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="c761c-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="c761c-135">O seguinte comando transmitirá os arquivos de log do seu aplicativo de funções para a linha de comando:</span><span class="sxs-lookup"><span data-stu-id="c761c-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="c761c-136">Monitoramento de arquivos de log do aplicativo de funções com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c761c-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="c761c-137">Para começar, [instale e configure o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c761c-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="c761c-138">Adicione a conta do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c761c-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="c761c-139">Se você tiver várias assinaturas, liste-as pelo nome com o seguinte comando para ver se a assinatura correta é a atualmente selecionada com base na propriedade `IsCurrent`:</span><span class="sxs-lookup"><span data-stu-id="c761c-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="c761c-140">Se precisar definir a assinatura ativa para aquela que contém seu aplicativo de funções, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c761c-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="c761c-141">Transmita os logs para sua sessão do PowerShell com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c761c-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="c761c-142">Para obter mais informações, veja [Como transmitir logs para aplicativos Web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="c761c-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c761c-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c761c-143">Next steps</span></span>
<span data-ttu-id="c761c-144">Para saber mais, consulte os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c761c-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="c761c-145">Testando uma função</span><span class="sxs-lookup"><span data-stu-id="c761c-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="c761c-146">Dimensionar uma função</span><span class="sxs-lookup"><span data-stu-id="c761c-146">Scale a function</span></span>](functions-scale.md)

