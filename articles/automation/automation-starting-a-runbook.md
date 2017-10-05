---
title: "Como iniciar um runbook na Automação do Azure | Microsoft Docs"
description: "Resume os métodos diferentes que podem ser usados para iniciar um runbook na Automação do Azure e fornece detalhes sobre como usar o portal do Azure e o Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 844831b63d5263987ed05370125fbe9f01913ab9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="d2cb9-103">Como iniciar um Runbook na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="d2cb9-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="d2cb9-104">A tabela a seguir o ajuda a determinar o método de inicialização de runbook na Automação do Azure mais adequado ao seu cenário específico.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="d2cb9-105">Este artigo inclui detalhes sobre como iniciar um runbook com o portal do Azure e com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="d2cb9-106">Detalhes sobre outros métodos são fornecidos em outros documentos que você pode acessar através dos links abaixo.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="d2cb9-107">**MÉTODO**</span><span class="sxs-lookup"><span data-stu-id="d2cb9-107">**METHOD**</span></span> | <span data-ttu-id="d2cb9-108">**CARACTERÍSTICAS**</span><span class="sxs-lookup"><span data-stu-id="d2cb9-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="d2cb9-109">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2cb9-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="d2cb9-110">Método mais simples com interface do usuário interativa.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="d2cb9-111">Formulário para fornecer valores de parâmetro simples.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="d2cb9-112">Controle facilmente o estado do trabalho.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-112">Easily track job state.</span></span><br> <li><span data-ttu-id="d2cb9-113">Acesso autenticado com o logon do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="d2cb9-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2cb9-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="d2cb9-115">Chame da linha de comando com os cmdlets do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="d2cb9-116">Pode ser incluído em uma solução automatizada com várias etapas.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="d2cb9-117">A solicitação é autenticada com certificado ou entidade de usuário/entidade de serviço OAuth.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="d2cb9-118">Fornece valores de parâmetro simples e complexos.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="d2cb9-119">Acompanhe o estado do trabalho.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-119">Track job state.</span></span><br> <li><span data-ttu-id="d2cb9-120">É necessário um cliente para dar suporte a cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="d2cb9-121">API de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="d2cb9-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="d2cb9-122">Método mais flexível, mas também o mais complexo.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="d2cb9-123">Chame de qualquer código personalizado que possa fazer solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="d2cb9-124">A solicitação autenticada com certificado ou entidade de usuário/entidade de serviço OAuth.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="d2cb9-125">Fornece valores de parâmetro simples e complexos.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="d2cb9-126">Acompanhe o estado do trabalho.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-126">Track job state.</span></span> |
| [<span data-ttu-id="d2cb9-127">Webhooks</span><span class="sxs-lookup"><span data-stu-id="d2cb9-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="d2cb9-128">Inicie o runbook de uma solicitação HTTP única.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="d2cb9-129">Autenticado com token de segurança na URL.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="d2cb9-130">O cliente não pode substituir valores de parâmetro especificados quando o webhook foi criado.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="d2cb9-131">O runbook pode definir um único parâmetro que é preenchido com os detalhes da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="d2cb9-132">Sem capacidade de acompanhar o estado do trabalho por meio da URL do webhook.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="d2cb9-133">Responder a um Alerta do Azure</span><span class="sxs-lookup"><span data-stu-id="d2cb9-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="d2cb9-134">Inicie um runbook em resposta a um alerta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="d2cb9-135">Configure o webhook para o runbook e vincule ao alerta.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="d2cb9-136">Autenticado com token de segurança na URL.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="d2cb9-137">Agenda</span><span class="sxs-lookup"><span data-stu-id="d2cb9-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="d2cb9-138">Inicie automaticamente o runbook em um cronograma horário, diário, semanal ou mensal.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="d2cb9-139">Manipule a agenda pelo portal do Azure, por cmdlets do PowerShell ou pela a API do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="d2cb9-140">Fornece os valores de parâmetro a serem usados com a agenda.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-140">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="d2cb9-141">De Outro Runbook</span><span class="sxs-lookup"><span data-stu-id="d2cb9-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="d2cb9-142">Use um runbook como uma atividade em outro runbook.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="d2cb9-143">É útil para funcionalidades usadas por vários runbooks.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="d2cb9-144">Forneça valores de parâmetro para o runbook filho e use a saída no runbook pai.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-144">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="d2cb9-145">A imagem a seguir ilustra o processo passo a passo detalhado no ciclo de vida de um runbook.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-145">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="d2cb9-146">Isso inclui as diferentes formas como um runbook é iniciado na Automação do Azure, os componentes necessários para que o Hybrid Runbook Worker execute runbooks da Automação do Azure e as interações entre diferentes componentes.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="d2cb9-147">Para saber mais sobre a execução de runbooks de Automação em seu datacenter, veja [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="d2cb9-147">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Arquitetura do runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="d2cb9-149">Iniciando um runbook com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2cb9-149">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="d2cb9-150">No portal do Azure, selecione **Automação** e clique no nome de uma conta de automação.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-150">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="d2cb9-151">No menu Hub, selecione **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-151">On the Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="d2cb9-152">Na folha **Runbooks**, selecione um runbook e clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-152">On the **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="d2cb9-153">Se o runbook tiver parâmetros, você deverá fornecer valores com uma caixa de texto para cada parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-153">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="d2cb9-154">Confira [Parâmetros de runbook](#Runbook-parameters) abaixo para mais detalhes sobre os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="d2cb9-155">Na folha **Trabalho**, você pode exibir o status do trabalho de runbook.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-155">On the **Job** blade, you can view the status of the runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="d2cb9-156">Iniciando um runbook com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2cb9-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="d2cb9-157">Você pode usar [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) para iniciar um runbook com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-157">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="d2cb9-158">O código de exemplo a seguir inicia um runbook chamado Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-158">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="d2cb9-159">Start-AzureRmAutomationRunbook retorna um objeto de trabalho que você pode usar para controlar seu status quando o runbook é iniciado.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-159">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="d2cb9-160">Você pode usar esse objeto de trabalho com [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) para determinar o status do trabalho e [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) para obter sua saída.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="d2cb9-161">O código de exemplo a seguir inicia um runbook chamado Test-Runbook, aguarda até que ele seja concluído e exibe a sua saída.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-161">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="d2cb9-162">Se o runbook exigir parâmetros, você deve fornecê-los como uma [hashtable](http://technet.microsoft.com/library/hh847780.aspx) , em que a chave da hashtable corresponde ao nome do parâmetro e o valor é o valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-162">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="d2cb9-163">O exemplo a seguir mostra como iniciar um runbook com dois parâmetros de cadeia de caracteres chamados FirstName e LastName, um número inteiro denominado RepeatCount e um parâmetro booliano denominado Show.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-163">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="d2cb9-164">Para saber mais sobre parâmetros, confira [Parâmetros de runbook](#Runbook-parameters) abaixo.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="d2cb9-165">Parâmetros de runbook</span><span class="sxs-lookup"><span data-stu-id="d2cb9-165">Runbook parameters</span></span>
<span data-ttu-id="d2cb9-166">Quando você inicia um runbook do Portal do Azure ou do Windows PowerShell, a instrução é enviada pelo serviço Web da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-166">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="d2cb9-167">Esse serviço não dá suporte a parâmetros com tipos de dados complexos.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="d2cb9-168">Se você precisa fornecer um valor para um parâmetro complexo, você deve chamá-lo embutido de outro runbook, como descrito em [Runbooks filho na Automação do Azure](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="d2cb9-168">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="d2cb9-169">O serviço Web da Automação do Azure fornece uma funcionalidade especial para os parâmetros usando certos tipos de dados, conforme descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-169">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="d2cb9-170">Valores nomeados</span><span class="sxs-lookup"><span data-stu-id="d2cb9-170">Named values</span></span>
<span data-ttu-id="d2cb9-171">Se o parâmetro é do tipo de dados [object], você pode usar o seguinte formato JSON para enviar-lhe uma lista de valores nomeados: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-171">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="d2cb9-172">Esses valores devem ser tipos simples.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-172">These values must be simple types.</span></span> <span data-ttu-id="d2cb9-173">O runbook receberá o parâmetro como um [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) com propriedades que correspondem a cada valor nomeado.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-173">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="d2cb9-174">Considere o runbook de teste a seguir que aceita um parâmetro chamado user.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-174">Consider the following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="d2cb9-175">O texto a seguir pode ser usado para o parâmetro user.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-175">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="d2cb9-176">Isso resulta na saída abaixo.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-176">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="d2cb9-177">Matrizes</span><span class="sxs-lookup"><span data-stu-id="d2cb9-177">Arrays</span></span>
<span data-ttu-id="d2cb9-178">Se o parâmetro for uma matriz, como [array] ou [string[]], você poderá usar o seguinte formato JSON para enviar-lhe uma lista de valores: *[Value1,Value2,Value3]*.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-178">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="d2cb9-179">Esses valores devem ser tipos simples.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-179">These values must be simple types.</span></span>

<span data-ttu-id="d2cb9-180">Considere o runbook de teste a seguir que aceita um parâmetro chamado *user*.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-180">Consider the following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="d2cb9-181">O texto a seguir pode ser usado para o parâmetro user.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-181">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="d2cb9-182">Isso resulta na saída abaixo.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-182">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="d2cb9-183">Credenciais</span><span class="sxs-lookup"><span data-stu-id="d2cb9-183">Credentials</span></span>
<span data-ttu-id="d2cb9-184">Se o parâmetro é do tipo de dados **PSCredential**, você pode fornecer o nome de um [ativo de credenciais](automation-credentials.md)da Automação do Azure .</span><span class="sxs-lookup"><span data-stu-id="d2cb9-184">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="d2cb9-185">O runbook irá recuperar as credenciais com o nome que você especificar.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-185">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="d2cb9-186">Considere o runbook de teste a seguir que aceita um parâmetro chamado credential.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-186">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="d2cb9-187">O texto a seguir pode ser usado para o parâmetro user supondo que havia um ativo de credenciais chamado *Minhas credenciais*.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-187">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="d2cb9-188">Supondo que o nome de usuário nas credenciais foi *vmonte*, isso resulta na saída abaixo.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-188">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="d2cb9-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2cb9-189">Next steps</span></span>
* <span data-ttu-id="d2cb9-190">A arquitetura de runbook no artigo atual oferece uma visão geral de alto nível do gerenciamento de recursos de runbooks no Azure e localmente com o Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="d2cb9-190">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="d2cb9-191">Para saber mais sobre a execução de runbooks de Automação em seu datacenter, consulte [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="d2cb9-191">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="d2cb9-192">Para saber mais sobre a criação de runbooks modulares a serem usados em outros runbooks para funções específicas ou comuns, consulte [Runbooks filho](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="d2cb9-192">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>

