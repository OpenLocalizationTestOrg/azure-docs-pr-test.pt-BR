---
title: Monitorar e gerenciar trabalhos do Stream Analytics com o PowerShell | Microsoft Docs
description: PowerShell dSaiba como usar os cmdlets do Azure PowerShell para monitorar e gerenciar trabalhos do Stream Analytics.
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
ms.openlocfilehash: e3449ee90cc83c5e823e5948a2a2e7e633c454f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="9b3ec-104">Monitorar e gerenciar trabalhos do Stream Analytics usando cmdlets do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b3ec-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="9b3ec-105">Saiba como monitorar e gerenciar os recursos do Stream Analytics com os cmdlets do Azure PowerShell e script do PowerShell que executam tarefas básicas de análise de fluxo.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-105">Learn how to monitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="9b3ec-106">Pré-requisitos para a execução de cmdlets do PowerShell do Azure para Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9b3ec-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="9b3ec-107">Crie um grupo de recursos do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="9b3ec-108">O seguinte é um exemplo de script do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-108">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="9b3ec-109">Para obter mais informações sobre o PowerShell do Azure, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b3ec-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="9b3ec-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="9b3ec-111">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-111">Azure PowerShell 1.0:</span></span>  

         # Log in to your Azure account
        Login-AzureRmAccount

        # Select the Azure subscription you want to use to create the resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="9b3ec-112">Os trabalhos do Stream Analytics criados programaticamente não têm monitoramento habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="9b3ec-113">Você pode habilitar manualmente o monitoramento no Portal do Azure, navegando até a página de monitoramento do trabalho e clicando no botão Ativar ou você pode fazer isso programaticamente, seguindo as etapas em [Stream Analytics do Azure - Monitorar programaticamente os trabalhos de Stream Analytics](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="9b3ec-113">You can manually enable monitoring in the Azure Portal by navigating to the job’s Monitor page and clicking the Enable button or you can do this programmatically by following the steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="9b3ec-114">Cmdlets do PowerShell do Azure para Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9b3ec-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="9b3ec-115">Os seguintes cmdlets do PowerShell do Azure podem ser usados para monitorar e gerenciar trabalhos de Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-115">The following Azure PowerShell cmdlets can be used to monitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="9b3ec-116">Observe que o Azure PowerShell tem diferentes versões.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="9b3ec-117">**Nos exemplos listados, o primeiro comando é para o Azure PowerShell 0.9.8 e o segundo comando é para o Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-117">**In the examples listed the first command is for Azure PowerShell 0.9.8, the second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="9b3ec-118">Os comandos do Azure PowerShell 1.0 sempre terão "AzureRM".</span><span class="sxs-lookup"><span data-stu-id="9b3ec-118">The Azure PowerShell 1.0 commands will always have "AzureRM" in the command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="9b3ec-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9b3ec-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9b3ec-120">Lista todas os trabalhos de Stream Analytics definidos na assinatura do Azure ou especificados no grupo de recursos ou obtém informações sobre um trabalho específico dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-120">Lists all Stream Analytics jobs defined in the Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="9b3ec-121">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-121">**Example 1**</span></span>

<span data-ttu-id="9b3ec-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="9b3ec-123">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="9b3ec-124">Esse comando do PowerShell retorna informações sobre todos os trabalhos do Stream Analytics na assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-124">This PowerShell command returns information about all the Stream Analytics jobs in the Azure subscription.</span></span>

<span data-ttu-id="9b3ec-125">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-125">**Example 2**</span></span>

<span data-ttu-id="9b3ec-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="9b3ec-127">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="9b3ec-128">Esse comando do PowerShell retorna informações sobre todos os trabalhos de Stream Analytics no grupo de recursos StreamAnalytics-Default-Central-US.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-128">This PowerShell command returns information about all the Stream Analytics jobs in the resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="9b3ec-129">**Exemplo 3**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-129">**Example 3**</span></span>

<span data-ttu-id="9b3ec-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="9b3ec-131">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="9b3ec-132">Esse comando do PowerShell retorna informações sobre o trabalho StreamingJob do Stream Analytics no grupo de recursos StreamAnalytics-Default-Central-US.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-132">This PowerShell command returns information about the Stream Analytics job StreamingJob in the resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="9b3ec-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="9b3ec-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="9b3ec-134">Lista todas as entradas que são definidas em um trabalho específico de Stream Analytics ou obtém informações sobre uma entrada específica.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-134">Lists all of the inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="9b3ec-135">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-135">**Example 1**</span></span>

<span data-ttu-id="9b3ec-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="9b3ec-137">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="9b3ec-138">Esse comando do PowerShell retorna informações sobre todas as entradas definidas no trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-138">This PowerShell command returns information about all the inputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="9b3ec-139">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-139">**Example 2**</span></span>

<span data-ttu-id="9b3ec-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="9b3ec-141">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="9b3ec-142">Esse comando do PowerShell retorna informações sobre a entrada denominada EntryStream definida no trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-142">This PowerShell command returns information about the input named EntryStream defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="9b3ec-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="9b3ec-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="9b3ec-144">Lista todas as saídas que são definidas em um trabalho específico de Stream Analytics ou obtém informações sobre uma saída específica.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-144">Lists all of the outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="9b3ec-145">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-145">**Example 1**</span></span>

<span data-ttu-id="9b3ec-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="9b3ec-147">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="9b3ec-148">Esse comando do PowerShell retorna informações sobre as saídas definidas no trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-148">This PowerShell command returns information about the outputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="9b3ec-149">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-149">**Example 2**</span></span>

<span data-ttu-id="9b3ec-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="9b3ec-151">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="9b3ec-152">Esse comando do PowerShell retorna informações sobre a saída denominada Output definida no trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-152">This PowerShell command returns information about the output named Output defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="9b3ec-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="9b3ec-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="9b3ec-154">Obtém informações sobre a cota de streaming de unidades em uma região especificada.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-154">Gets information about the quota of streaming units in a specified region.</span></span>

<span data-ttu-id="9b3ec-155">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-155">**Example 1**</span></span>

<span data-ttu-id="9b3ec-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="9b3ec-157">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="9b3ec-158">Esse comando do PowerShell retorna informações sobre a cota e o uso de unidades de streaming na região Central dos Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-158">This PowerShell command returns information about the quota and usage of streaming units in the Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="9b3ec-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="9b3ec-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="9b3ec-160">Obtém informações sobre uma transformação específica definida no trabalho de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="9b3ec-161">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-161">**Example 1**</span></span>

<span data-ttu-id="9b3ec-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="9b3ec-163">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="9b3ec-164">Esse comando do PowerShell retorna informações sobre a transformação chamada StreamingJob no trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-164">This PowerShell command returns information about the transformation called StreamingJob in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="9b3ec-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="9b3ec-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="9b3ec-166">Cria uma nova entrada dentro do trabalho do Stream Analytics ou atualiza uma entrada existente especificada.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="9b3ec-167">O nome da entrada pode ser especificado no arquivo .json ou na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-167">The name of the input can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="9b3ec-168">Se ambos forem especificados, o nome na linha de comando deve ser o mesmo que o do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-168">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="9b3ec-169">Se você especificar uma entrada que já existe e não especificar o parâmetro –Force, o cmdlet perguntará se deseja ou não substituir a entrada existente.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-169">If you specify an input that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing input.</span></span>

<span data-ttu-id="9b3ec-170">Se você especificar o parâmetro –Force e especificar um nome de entrada existente, a entrada será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-170">If you specify the –Force parameter and specify an existing input name, the input will be replaced without confirmation.</span></span>

<span data-ttu-id="9b3ec-171">Para obter informações detalhadas sobre a estrutura do arquivo JSON e o conteúdo, consulte a seção [Criar entrada (Stream Analytics do Azure)][msdn-rest-api-create-stream-analytics-input] da [Biblioteca de referência de API REST de gerenciamento de Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="9b3ec-171">For detailed information on the JSON file structure and contents, refer to the [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="9b3ec-172">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-172">**Example 1**</span></span>

<span data-ttu-id="9b3ec-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="9b3ec-174">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="9b3ec-175">Esse comando do PowerShell cria uma nova entrada do arquivo Input.json.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-175">This PowerShell command creates a new input from the file Input.json.</span></span> <span data-ttu-id="9b3ec-176">Se uma entrada existente com o nome especificado no arquivo de definição de entrada já estiver definida, o cmdlet perguntará se deseja ou não substituí-la.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-176">If an existing input with the name specified in the input definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="9b3ec-177">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-177">**Example 2**</span></span>

<span data-ttu-id="9b3ec-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="9b3ec-179">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="9b3ec-180">Esse comando do PowerShell cria uma nova entrada no trabalho chamado EntryStream.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-180">This PowerShell command creates a new input in the job called EntryStream.</span></span> <span data-ttu-id="9b3ec-181">Se uma entrada existente com esse nome já estiver definida, o cmdlet perguntará se deseja ou não substituí-la.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-181">If an existing input with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="9b3ec-182">**Exemplo 3**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-182">**Example 3**</span></span>

<span data-ttu-id="9b3ec-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="9b3ec-184">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="9b3ec-185">Esse comando do PowerShell substitui a definição da fonte de entrada existente chamada EntryStream com a definição do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-185">This PowerShell command replaces the definition of the existing input source called EntryStream with the definition from the file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="9b3ec-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9b3ec-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9b3ec-187">Cria um novo trabalho de Stream Analytics no Microsoft Azure ou atualiza a definição de um trabalho existente especificado.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-187">Creates a new Stream Analytics job in Microsoft Azure, or updates the definition of an existing specified job.</span></span>

<span data-ttu-id="9b3ec-188">O nome do trabalho pode ser especificado no arquivo .json ou na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-188">The name of the job can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="9b3ec-189">Se ambos forem especificados, o nome na linha de comando deve ser o mesmo que o do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-189">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="9b3ec-190">Se você especificar um nome de trabalho que já existe e não especificar o parâmetro –Force, o cmdlet perguntará se deseja ou não substituir o trabalho existente.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-190">If you specify a job name that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing job.</span></span>

<span data-ttu-id="9b3ec-191">Se você especificar o parâmetro –Force e especificar um nome de trabalho existente, a definição do trabalho será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-191">If you specify the –Force parameter and specify an existing job name, the job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="9b3ec-192">Para obter informações detalhadas sobre a estrutura do arquivo JSON e o conteúdo, consulte a seção [Criar trabalho de Stream Analytics][msdn-rest-api-create-stream-analytics-job] da [Biblioteca de referência de API REST de gerenciamento de Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="9b3ec-192">For detailed information on the JSON file structure and contents, refer to the [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="9b3ec-193">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-193">**Example 1**</span></span>

<span data-ttu-id="9b3ec-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="9b3ec-195">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="9b3ec-196">Esse comando do PowerShell cria um novo trabalho por meio da definição em JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-196">This PowerShell command creates a new job from the definition in JobDefinition.json.</span></span> <span data-ttu-id="9b3ec-197">Se um trabalho existente com o nome especificado no arquivo de definição de trabalho já estiver definido, o cmdlet perguntará se deseja ou não substituí-lo.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-197">If an existing job with the name specified in the job definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="9b3ec-198">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-198">**Example 2**</span></span>

<span data-ttu-id="9b3ec-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="9b3ec-200">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="9b3ec-201">Esse comando do PowerShell substitui a definição de trabalho para StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-201">This PowerShell command replaces the job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="9b3ec-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="9b3ec-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="9b3ec-203">Cria uma nova saída dentro de um trabalho de Stream Analytics ou atualiza uma saída existente.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="9b3ec-204">O nome da saída pode ser especificado no arquivo .json ou na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-204">The name of the output can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="9b3ec-205">Se ambos forem especificados, o nome na linha de comando deve ser o mesmo que o do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-205">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="9b3ec-206">Se você especificar uma saída que já existe e não especificar o parâmetro –Force, o cmdlet perguntará se deseja ou não substituir a saída existente.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-206">If you specify an output that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing output.</span></span>

<span data-ttu-id="9b3ec-207">Se você especificar o parâmetro –Force e especificar um nome de saída existente, a saída será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-207">If you specify the –Force parameter and specify an existing output name, the output will be replaced without confirmation.</span></span>

<span data-ttu-id="9b3ec-208">Para obter informações detalhadas sobre a estrutura do arquivo JSON e o conteúdo, consulte a seção [Criar Saída (Stream Analytics do Azure)][msdn-rest-api-create-stream-analytics-output] da [Biblioteca de referência de API REST de gerenciamento de Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="9b3ec-208">For detailed information on the JSON file structure and contents, refer to the [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="9b3ec-209">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-209">**Example 1**</span></span>

<span data-ttu-id="9b3ec-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="9b3ec-211">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="9b3ec-212">Esse comando do PowerShell cria uma nova saída chamada "output" no trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-212">This PowerShell command creates a new output called "output" in the job StreamingJob.</span></span> <span data-ttu-id="9b3ec-213">Se uma saída existente com esse nome já estiver definida, o cmdlet perguntará se deseja ou não substituí-la.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-213">If an existing output with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="9b3ec-214">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-214">**Example 2**</span></span>

<span data-ttu-id="9b3ec-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="9b3ec-216">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="9b3ec-217">Esse comando do PowerShell substitui a definição de “output" no trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-217">This PowerShell command replaces the definition for "output" in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="9b3ec-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="9b3ec-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="9b3ec-219">Cria uma nova transformação dentro de um trabalho de Stream Analytics ou atualiza uma transformação existente.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-219">Creates a new transformation within a Stream Analytics job, or updates the existing transformation.</span></span>

<span data-ttu-id="9b3ec-220">O nome da transformação pode ser especificado no arquivo .json ou na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-220">The name of the transformation can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="9b3ec-221">Se ambos forem especificados, o nome na linha de comando deve ser o mesmo que o do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-221">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="9b3ec-222">Se você especificar uma transformação que já existe e não especificar o parâmetro –Force, o cmdlet perguntará se deseja ou não substituir a transformação existente.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-222">If you specify a transformation that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing transformation.</span></span>

<span data-ttu-id="9b3ec-223">Se você especificar o parâmetro –Force e especificar um nome de transformação existente, a transformação será substituída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-223">If you specify the –Force parameter and specify an existing transformation name, the transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="9b3ec-224">Para obter informações detalhadas sobre a estrutura do arquivo JSON e o conteúdo, consulte a seção [Criar transformação (Stream Analytics do Azure)][msdn-rest-api-create-stream-analytics-transformation] da [Biblioteca de referência de API REST de gerenciamento de Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="9b3ec-224">For detailed information on the JSON file structure and contents, refer to the [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="9b3ec-225">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-225">**Example 1**</span></span>

<span data-ttu-id="9b3ec-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="9b3ec-227">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="9b3ec-228">Esse comando do PowerShell cria uma nova transformação chamada StreamingJobTransform no trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-228">This PowerShell command creates a new transformation called StreamingJobTransform in the job StreamingJob.</span></span> <span data-ttu-id="9b3ec-229">Se uma transformação existente com esse nome já estiver definida, o cmdlet perguntará se deseja ou não substituí-la.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-229">If an existing transformation is already defined with this name, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="9b3ec-230">**Exemplo 2**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-230">**Example 2**</span></span>

<span data-ttu-id="9b3ec-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="9b3ec-232">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="9b3ec-233">Esse comando do PowerShell substitui a definição de StreamingJobTransform no trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-233">This PowerShell command replaces the definition of StreamingJobTransform in the job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="9b3ec-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="9b3ec-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="9b3ec-235">Exclui de maneira assíncrona uma entrada específica de um trabalho do Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="9b3ec-236">Se você especificar o parâmetro –Force, a entrada será excluída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-236">If you specify the –Force parameter, the input will be deleted without confirmation.</span></span>

<span data-ttu-id="9b3ec-237">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-237">**Example 1**</span></span>

<span data-ttu-id="9b3ec-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="9b3ec-239">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="9b3ec-240">Esse comando do PowerShell remove a entrada EventStream do trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-240">This PowerShell command removes the input EventStream in the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="9b3ec-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9b3ec-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9b3ec-242">Exclui de maneira assíncrona um trabalho específico do Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="9b3ec-243">Se você especificar o parâmetro –Force, o trabalho será excluído sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-243">If you specify the –Force parameter, the job will be deleted without confirmation.</span></span>

<span data-ttu-id="9b3ec-244">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-244">**Example 1**</span></span>

<span data-ttu-id="9b3ec-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="9b3ec-246">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="9b3ec-247">Esse comando do PowerShell remove o trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-247">This PowerShell command removes the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="9b3ec-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="9b3ec-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="9b3ec-249">Exclui de maneira assíncrona uma saída específica de um trabalho do Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="9b3ec-250">Se você especificar o parâmetro –Force, a saída será excluída sem confirmação.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-250">If you specify the –Force parameter, the output will be deleted without confirmation.</span></span>

<span data-ttu-id="9b3ec-251">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-251">**Example 1**</span></span>

<span data-ttu-id="9b3ec-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="9b3ec-253">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="9b3ec-254">Esse comando do PowerShell remove a saída Output do trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-254">This PowerShell command removes the output Output in the job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="9b3ec-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9b3ec-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9b3ec-256">Implanta de maneira assíncrona e inicia um trabalho do Stream Analytics no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="9b3ec-257">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-257">**Example 1**</span></span>

<span data-ttu-id="9b3ec-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="9b3ec-259">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="9b3ec-260">Esse comando do PowerShell inicia o trabalho StreamingJob com uma hora personalizada de início de saída definida como 12 de dezembro de 2012, 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-260">This PowerShell command starts the job StreamingJob with a custom output start time set to December 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="9b3ec-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="9b3ec-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="9b3ec-262">Interrompe de maneira assíncrona um trabalho do Stream Analytics para que não seja executado no Microsoft Azure e desaloca os recursos que estavam sendo usados.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="9b3ec-263">A definição de trabalho e os metadados permanecerão disponíveis dentro da sua assinatura por meio de APIs de gerenciamento e do Portal do Azure, de modo que o trabalho possa ser editado e reiniciado.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-263">The job definition and metadata will remain available within your subscription through both the Azure portal and management APIs, such that the job can be edited and restarted.</span></span> <span data-ttu-id="9b3ec-264">Você não será cobrado por um trabalho no estado Interrompido.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-264">You will not be charged for a job in the stopped state.</span></span>

<span data-ttu-id="9b3ec-265">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-265">**Example 1**</span></span>

<span data-ttu-id="9b3ec-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="9b3ec-267">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="9b3ec-268">Esse comando do PowerShell para o trabalho StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-268">This PowerShell command stops the job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="9b3ec-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="9b3ec-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="9b3ec-270">Testa a capacidade do Stream Analytics de se conectar a uma entrada especificada.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-270">Tests the ability of Stream Analytics to connect to a specified input.</span></span>

<span data-ttu-id="9b3ec-271">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-271">**Example 1**</span></span>

<span data-ttu-id="9b3ec-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="9b3ec-273">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="9b3ec-274">Esse comando do PowerShell testa o status de conexão da entrada EntryStream no StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-274">This PowerShell command tests the connection status of the input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="9b3ec-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="9b3ec-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="9b3ec-276">Testa a capacidade do Stream Analytics de se conectar a uma saída especificada.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-276">Tests the ability of Stream Analytics to connect to a specified output.</span></span>

<span data-ttu-id="9b3ec-277">**Exemplo 1**</span><span class="sxs-lookup"><span data-stu-id="9b3ec-277">**Example 1**</span></span>

<span data-ttu-id="9b3ec-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="9b3ec-279">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="9b3ec-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="9b3ec-280">Esse comando do PowerShell testa o status de conexão da entrada Output no StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="9b3ec-280">This PowerShell command tests the connection status of the output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="9b3ec-281">Obtenha suporte</span><span class="sxs-lookup"><span data-stu-id="9b3ec-281">Get support</span></span>
<span data-ttu-id="9b3ec-282">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="9b3ec-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9b3ec-283">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b3ec-283">Next steps</span></span>
* [<span data-ttu-id="9b3ec-284">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3ec-284">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9b3ec-285">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3ec-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="9b3ec-286">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3ec-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="9b3ec-287">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3ec-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="9b3ec-288">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9b3ec-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

