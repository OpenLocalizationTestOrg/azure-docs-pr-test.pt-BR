---
title: aaaMonitor e gerenciar trabalhos do Stream Analytics com o PowerShell | Microsoft Docs
description: Saiba como toouse toomonitor de PowerShell do Azure e cmdlets e gerenciar trabalhos do Stream Analytics.
keywords: azure powershell, cmdlets do azure powershell, comando do powershell, scripts do powershell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="970cf-104">Monitorar e gerenciar trabalhos do Stream Analytics usando cmdlets do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="970cf-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="970cf-105">Saiba como toomonitor e gerenciar recursos de análise de fluxo com cmdlets do PowerShell do Azure e o script do powershell que execute tarefas básicas de análise de fluxo.</span><span class="sxs-lookup"><span data-stu-id="970cf-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="970cf-106">Pré-requisitos para a execução de cmdlets do PowerShell do Azure para Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="970cf-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="970cf-107">Crie um grupo de recursos do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="970cf-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="970cf-108">a seguir Olá é um exemplo de script do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="970cf-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="970cf-109">Para obter mais informações sobre o PowerShell do Azure, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="970cf-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="970cf-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="970cf-111">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="970cf-112">Os trabalhos do Stream Analytics criados programaticamente não têm monitoramento habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="970cf-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="970cf-113">Você pode habilitar manualmente o monitoramento no hello Portal do Azure navegando página Monitor de toohello do trabalho e clicar o botão de habilitar hello, ou você pode fazer isso programaticamente, seguindo os passos de saudação localizados em [Stream Analytics do Azure - fluxo de Monitor Trabalhos de análise de maneira programática](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="970cf-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="970cf-114">Cmdlets do PowerShell do Azure para Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="970cf-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="970cf-115">Olá cmdlets do Azure PowerShell a seguir pode ser usado toomonitor e gerenciar trabalhos do Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="970cf-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="970cf-116">Observe que o Azure PowerShell tem diferentes versões.</span><span class="sxs-lookup"><span data-stu-id="970cf-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="970cf-117">**Exemplos de Olá Olá listados primeiro comando é para o Azure PowerShell 0.9.8, Olá segundo comando é para o Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="970cf-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="970cf-118">comandos de saudação do Azure PowerShell 1.0 sempre terá "AzureRM" no comando hello.</span><span class="sxs-lookup"><span data-stu-id="970cf-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="970cf-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="970cf-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="970cf-120">Lista todos os trabalhos de análise de fluxo definidos em Olá assinatura do Azure ou o grupo de recursos especificado, ou obtém informações sobre um trabalho específico dentro de um grupo de recursos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="970cf-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="970cf-121">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-121">**Example 1**</span></span>

<span data-ttu-id="970cf-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="970cf-123">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="970cf-124">Este comando do PowerShell retorna informações sobre todos os trabalhos do Stream Analytics Olá no hello assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="970cf-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="970cf-125">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="970cf-125">**Example 2**</span></span>

<span data-ttu-id="970cf-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="970cf-127">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="970cf-128">Este comando do PowerShell retorna informações sobre todos os trabalhos do Stream Analytics Olá no grupo de recursos de saudação StreamAnalytics-padrão-Centro dos EUA.</span><span class="sxs-lookup"><span data-stu-id="970cf-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="970cf-129">**Exemplo 3**</span><span class="sxs-lookup"><span data-stu-id="970cf-129">**Example 3**</span></span>

<span data-ttu-id="970cf-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="970cf-131">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="970cf-132">Este comando do PowerShell retorna informações sobre o trabalho de análise de fluxo de saudação StreamingJob no grupo de recursos de saudação StreamAnalytics-padrão-Centro dos EUA.</span><span class="sxs-lookup"><span data-stu-id="970cf-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="970cf-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="970cf-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="970cf-134">Lista todas as entradas de saudação que são definidas em um trabalho de análise de fluxo especificado ou obtém informações sobre uma entrada específica.</span><span class="sxs-lookup"><span data-stu-id="970cf-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="970cf-135">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-135">**Example 1**</span></span>

<span data-ttu-id="970cf-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="970cf-137">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="970cf-138">Este comando do PowerShell retorna informações sobre todas as entradas de saudação definido no trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="970cf-139">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="970cf-139">**Example 2**</span></span>

<span data-ttu-id="970cf-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="970cf-141">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="970cf-142">Este comando do PowerShell retorna informações sobre entrada hello denominada EntryStream definido no trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="970cf-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="970cf-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="970cf-144">Lista todas as saídas de saudação que são definidas em um trabalho de análise de fluxo especificado ou obtém informações sobre uma saída específica.</span><span class="sxs-lookup"><span data-stu-id="970cf-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="970cf-145">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-145">**Example 1**</span></span>

<span data-ttu-id="970cf-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="970cf-147">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="970cf-148">Este comando do PowerShell retorna informações sobre saídas de saudação definidas no trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="970cf-149">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="970cf-149">**Example 2**</span></span>

<span data-ttu-id="970cf-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="970cf-151">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="970cf-152">Este comando do PowerShell retorna informações sobre a saída Olá chamada de saída definida no trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="970cf-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="970cf-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="970cf-154">Obtém informações sobre cota de saudação do streaming unidades em uma região especificada.</span><span class="sxs-lookup"><span data-stu-id="970cf-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="970cf-155">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-155">**Example 1**</span></span>

<span data-ttu-id="970cf-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="970cf-157">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="970cf-158">Este comando do PowerShell retorna informações sobre cota de saudação e o uso de unidades de streaming na região do hello centro dos EUA.</span><span class="sxs-lookup"><span data-stu-id="970cf-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="970cf-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="970cf-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="970cf-160">Obtém informações sobre uma transformação específica definida no trabalho de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="970cf-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="970cf-161">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-161">**Example 1**</span></span>

<span data-ttu-id="970cf-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="970cf-163">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="970cf-164">Este comando do PowerShell retorna informações sobre transformação Olá chamada StreamingJob no trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="970cf-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="970cf-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="970cf-166">Cria uma nova entrada dentro do trabalho do Stream Analytics ou atualiza uma entrada existente especificada.</span><span class="sxs-lookup"><span data-stu-id="970cf-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="970cf-167">Olá nome de entrada hello pode ser especificado no arquivo. JSON de saudação ou na linha de comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="970cf-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="970cf-168">Se ambos forem especificados, nome hello na linha de comando Olá deve Olá igual a saudação no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="970cf-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="970cf-169">Se você especificar uma entrada que já existe e não especificar hello – o parâmetro Force, Olá cmdlet perguntará se ou não tooreplace Olá entrada existente.</span><span class="sxs-lookup"><span data-stu-id="970cf-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="970cf-170">Se você especificar hello – o parâmetro Force e especifique uma existente de nome de entrada, entrada hello será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="970cf-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="970cf-171">Para obter informações detalhadas sobre a estrutura do arquivo hello JSON e o conteúdo, consulte toohello [criar entrada (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] seção Olá [API de REST de gerenciamento de análise de fluxo Biblioteca de referência][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="970cf-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="970cf-172">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-172">**Example 1**</span></span>

<span data-ttu-id="970cf-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="970cf-174">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="970cf-175">Este comando do PowerShell cria uma nova entrada de arquivo hello Input.json.</span><span class="sxs-lookup"><span data-stu-id="970cf-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="970cf-176">Se uma entrada existente com o nome de saudação especificado no arquivo de definição de entrada hello já estiver definida, Olá cmdlet perguntará se ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="970cf-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="970cf-177">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="970cf-177">**Example 2**</span></span>

<span data-ttu-id="970cf-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="970cf-179">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="970cf-180">Este comando do PowerShell cria uma nova entrada no trabalho Olá chamado EntryStream.</span><span class="sxs-lookup"><span data-stu-id="970cf-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="970cf-181">Se uma entrada existente com esse nome já está definida, Olá cmdlet perguntará se ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="970cf-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="970cf-182">**Exemplo 3**</span><span class="sxs-lookup"><span data-stu-id="970cf-182">**Example 3**</span></span>

<span data-ttu-id="970cf-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="970cf-184">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="970cf-185">Esse comando do PowerShell substitui a definição Olá Olá existente da fonte de entrada chamado EntryStream com definição de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="970cf-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="970cf-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="970cf-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="970cf-187">Cria um novo trabalho do Stream Analytics no Microsoft Azure ou atualiza a definição de saudação do trabalho especificado existente.</span><span class="sxs-lookup"><span data-stu-id="970cf-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="970cf-188">nome de saudação do trabalho Olá pode ser especificado no arquivo. JSON de saudação ou na linha de comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="970cf-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="970cf-189">Se ambos forem especificados, nome hello na linha de comando Olá deve Olá igual a saudação no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="970cf-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="970cf-190">Se você especificar um nome de trabalho que já existe e não especificar hello – o parâmetro Force, Olá cmdlet perguntará se ou não tooreplace Olá trabalho existente.</span><span class="sxs-lookup"><span data-stu-id="970cf-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="970cf-191">Se você especificar hello – o parâmetro Force e especifique um nome de trabalho existente, definição de trabalho Olá será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="970cf-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="970cf-192">Para obter informações detalhadas sobre a estrutura do arquivo hello JSON e o conteúdo, consulte toohello [criar o trabalho do Stream Analytics] [ msdn-rest-api-create-stream-analytics-job] seção Olá [referência de API de REST de gerenciamento de análise de fluxo Biblioteca][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="970cf-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="970cf-193">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-193">**Example 1**</span></span>

<span data-ttu-id="970cf-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="970cf-195">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="970cf-196">Este comando do PowerShell cria um novo trabalho de definição de saudação em JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="970cf-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="970cf-197">Se um trabalho existente com o nome hello especificada no arquivo de definição de trabalho Olá já estiver definido, Olá cmdlet perguntará se ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="970cf-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="970cf-198">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="970cf-198">**Example 2**</span></span>

<span data-ttu-id="970cf-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="970cf-200">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="970cf-201">Este comando do PowerShell substitui a definição de trabalho Olá para StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="970cf-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="970cf-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="970cf-203">Cria uma nova saída dentro de um trabalho de Stream Analytics ou atualiza uma saída existente.</span><span class="sxs-lookup"><span data-stu-id="970cf-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="970cf-204">nome de saudação da saída de hello pode ser especificado no arquivo. JSON de saudação ou na linha de comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="970cf-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="970cf-205">Se ambos forem especificados, nome hello na linha de comando Olá deve Olá igual a saudação no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="970cf-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="970cf-206">Se você especificar uma saída que já existe e não especificar hello – o parâmetro Force, Olá cmdlet perguntará se ou não tooreplace Olá saída existente.</span><span class="sxs-lookup"><span data-stu-id="970cf-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="970cf-207">Se você especificar hello – o parâmetro Force e especifique o nome de saída existente, saída de hello será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="970cf-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="970cf-208">Para obter informações detalhadas sobre a estrutura do arquivo hello JSON e o conteúdo, consulte toohello [criar saída (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] seção Olá [API de REST de gerenciamento de análise de fluxo Biblioteca de referência][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="970cf-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="970cf-209">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-209">**Example 1**</span></span>

<span data-ttu-id="970cf-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="970cf-211">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="970cf-212">Este comando do PowerShell cria uma nova saída chamada "saída" trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="970cf-213">Se uma saída existente com esse nome já está definida, Olá cmdlet perguntará se ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="970cf-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="970cf-214">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="970cf-214">**Example 2**</span></span>

<span data-ttu-id="970cf-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="970cf-216">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="970cf-217">Este comando do PowerShell substitui a definição de saudação de "saída" no trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="970cf-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="970cf-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="970cf-219">Cria uma nova transformação dentro de um trabalho do Stream Analytics ou atualiza a transformação de saudação existente.</span><span class="sxs-lookup"><span data-stu-id="970cf-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="970cf-220">nome de saudação da transformação Olá pode ser especificado no arquivo. JSON de saudação ou na linha de comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="970cf-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="970cf-221">Se ambos forem especificados, nome hello na linha de comando Olá deve Olá igual a saudação no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="970cf-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="970cf-222">Se você especificar uma transformação que já existe e não especificar hello – o parâmetro Force, Olá cmdlet perguntará se ou não tooreplace Olá transformação existente.</span><span class="sxs-lookup"><span data-stu-id="970cf-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="970cf-223">Se você especificar hello – o parâmetro Force e especifique um nome de transformação existente, transformação Olá será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="970cf-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="970cf-224">Para obter informações detalhadas sobre a estrutura do arquivo hello JSON e o conteúdo, consulte toohello [criar transformação (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] seção Olá [gerenciamento de análise de fluxo Biblioteca de referência de API REST][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="970cf-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="970cf-225">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-225">**Example 1**</span></span>

<span data-ttu-id="970cf-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="970cf-227">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="970cf-228">Este comando do PowerShell cria uma nova transformação chamada StreamingJobTransform no trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="970cf-229">Se uma transformação existente já está definida com esse nome, Olá cmdlet perguntará se ou não tooreplace-lo.</span><span class="sxs-lookup"><span data-stu-id="970cf-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="970cf-230">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="970cf-230">**Example 2**</span></span>

<span data-ttu-id="970cf-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="970cf-232">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="970cf-233">Este comando do PowerShell substitui a definição de saudação do StreamingJobTransform trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="970cf-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="970cf-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="970cf-235">Exclui de maneira assíncrona uma entrada específica de um trabalho do Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="970cf-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="970cf-236">Se você especificar hello – parâmetro Force, Olá de entrada será excluído sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="970cf-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="970cf-237">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-237">**Example 1**</span></span>

<span data-ttu-id="970cf-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="970cf-239">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="970cf-240">Esse comando do PowerShell remove Olá entrada EventStream trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="970cf-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="970cf-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="970cf-242">Exclui de maneira assíncrona um trabalho específico do Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="970cf-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="970cf-243">Se você especificar hello – o parâmetro Force, Olá trabalho será excluída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="970cf-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="970cf-244">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-244">**Example 1**</span></span>

<span data-ttu-id="970cf-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="970cf-246">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="970cf-247">Este comando do PowerShell remove o trabalho de saudação StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="970cf-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="970cf-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="970cf-249">Exclui de maneira assíncrona uma saída específica de um trabalho do Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="970cf-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="970cf-250">Se você especificar hello – o parâmetro Force, Olá saída será excluída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="970cf-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="970cf-251">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-251">**Example 1**</span></span>

<span data-ttu-id="970cf-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="970cf-253">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="970cf-254">Essa saudação do PowerShell comando remove saída saída no trabalho Olá StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="970cf-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="970cf-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="970cf-256">Implanta de maneira assíncrona e inicia um trabalho do Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="970cf-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="970cf-257">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-257">**Example 1**</span></span>

<span data-ttu-id="970cf-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="970cf-259">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="970cf-260">Esse comando do PowerShell inicia Olá trabalho StreamingJob com uma hora de início de saída personalizado definido tooDecember 12, 2012, 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="970cf-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="970cf-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="970cf-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="970cf-262">Interrompe de maneira assíncrona um trabalho do Stream Analytics para que não seja executado no Microsoft Azure e desaloca os recursos que estavam sendo usados.</span><span class="sxs-lookup"><span data-stu-id="970cf-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="970cf-263">Olá metadados e definição de trabalho permanecerão disponíveis dentro de sua assinatura por meio de saudação portal do Azure e APIs de gerenciamento, que hello trabalho pode ser editado e reiniciado.</span><span class="sxs-lookup"><span data-stu-id="970cf-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="970cf-264">Você não será cobrado por um trabalho no estado de saudação interrompido.</span><span class="sxs-lookup"><span data-stu-id="970cf-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="970cf-265">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-265">**Example 1**</span></span>

<span data-ttu-id="970cf-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="970cf-267">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="970cf-268">Este comando do PowerShell para o trabalho de saudação StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="970cf-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="970cf-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="970cf-270">Capacidade de saudação de testes de análise de fluxo tooconnect tooa especificado de entrada.</span><span class="sxs-lookup"><span data-stu-id="970cf-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="970cf-271">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-271">**Example 1**</span></span>

<span data-ttu-id="970cf-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="970cf-273">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="970cf-274">Esse status de conexão do PowerShell comando testes Olá de saudação EntryStream no StreamingJob de entrada.</span><span class="sxs-lookup"><span data-stu-id="970cf-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="970cf-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="970cf-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="970cf-276">Capacidade de saudação de testes de análise de fluxo tooconnect tooa especificado de saída.</span><span class="sxs-lookup"><span data-stu-id="970cf-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="970cf-277">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="970cf-277">**Example 1**</span></span>

<span data-ttu-id="970cf-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="970cf-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="970cf-279">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="970cf-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="970cf-280">Esse status de conexão do PowerShell comando testes Olá de saudação saída saída em StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="970cf-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="970cf-281">Obtenha suporte</span><span class="sxs-lookup"><span data-stu-id="970cf-281">Get support</span></span>
<span data-ttu-id="970cf-282">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="970cf-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="970cf-283">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="970cf-283">Next steps</span></span>
* [<span data-ttu-id="970cf-284">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="970cf-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="970cf-285">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="970cf-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="970cf-286">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="970cf-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="970cf-287">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="970cf-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="970cf-288">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="970cf-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

