---
title: "aaaStarting um runbook na automação do Azure | Microsoft Docs"
description: "Resume Olá métodos diferentes que podem ser usado toostart um runbook na automação do Azure e fornece detalhes sobre o uso de ambos Olá portal do Azure e o Windows PowerShell."
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
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="772df-103">Como iniciar um Runbook na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="772df-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="772df-104">Olá, a tabela a seguir ajudará você a determinar Olá método toostart um runbook na automação do Azure que é mais adequado tooyour cenário em particular.</span><span class="sxs-lookup"><span data-stu-id="772df-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="772df-105">Este artigo inclui detalhes sobre como iniciar um runbook com hello portal do Azure e com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="772df-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="772df-106">Detalhes no hello outros métodos são fornecidos em outra documentação que você pode acessar de links de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="772df-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="772df-107">**MÉTODO**</span><span class="sxs-lookup"><span data-stu-id="772df-107">**METHOD**</span></span> | <span data-ttu-id="772df-108">**CARACTERÍSTICAS**</span><span class="sxs-lookup"><span data-stu-id="772df-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="772df-109">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="772df-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="772df-110">Método mais simples com interface do usuário interativa.</span><span class="sxs-lookup"><span data-stu-id="772df-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="772df-111">Valores de parâmetro simples de tooprovide do formulário.</span><span class="sxs-lookup"><span data-stu-id="772df-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="772df-112">Controle facilmente o estado do trabalho.</span><span class="sxs-lookup"><span data-stu-id="772df-112">Easily track job state.</span></span><br> <li><span data-ttu-id="772df-113">Acesso autenticado com o logon do Azure.</span><span class="sxs-lookup"><span data-stu-id="772df-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="772df-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="772df-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="772df-115">Chame da linha de comando com os cmdlets do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="772df-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="772df-116">Pode ser incluído em uma solução automatizada com várias etapas.</span><span class="sxs-lookup"><span data-stu-id="772df-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="772df-117">A solicitação é autenticada com certificado ou entidade de usuário/entidade de serviço OAuth.</span><span class="sxs-lookup"><span data-stu-id="772df-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="772df-118">Fornece valores de parâmetro simples e complexos.</span><span class="sxs-lookup"><span data-stu-id="772df-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="772df-119">Acompanhe o estado do trabalho.</span><span class="sxs-lookup"><span data-stu-id="772df-119">Track job state.</span></span><br> <li><span data-ttu-id="772df-120">Cliente necessário toosupport cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="772df-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="772df-121">API de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="772df-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="772df-122">Método mais flexível, mas também o mais complexo.</span><span class="sxs-lookup"><span data-stu-id="772df-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="772df-123">Chame de qualquer código personalizado que possa fazer solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="772df-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="772df-124">A solicitação autenticada com certificado ou entidade de usuário/entidade de serviço OAuth.</span><span class="sxs-lookup"><span data-stu-id="772df-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="772df-125">Fornece valores de parâmetro simples e complexos.</span><span class="sxs-lookup"><span data-stu-id="772df-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="772df-126">Acompanhe o estado do trabalho.</span><span class="sxs-lookup"><span data-stu-id="772df-126">Track job state.</span></span> |
| [<span data-ttu-id="772df-127">Webhooks</span><span class="sxs-lookup"><span data-stu-id="772df-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="772df-128">Inicie o runbook de uma solicitação HTTP única.</span><span class="sxs-lookup"><span data-stu-id="772df-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="772df-129">Autenticado com token de segurança na URL.</span><span class="sxs-lookup"><span data-stu-id="772df-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="772df-130">O cliente não pode substituir valores de parâmetro especificados quando o webhook foi criado.</span><span class="sxs-lookup"><span data-stu-id="772df-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="772df-131">Runbook pode definir um único parâmetro que é preenchido com os detalhes da solicitação HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="772df-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="772df-132">Nenhum estado de trabalho tootrack de capacidade por meio de URL de webhook.</span><span class="sxs-lookup"><span data-stu-id="772df-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="772df-133">Responder tooAzure alerta</span><span class="sxs-lookup"><span data-stu-id="772df-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="772df-134">Inicie um runbook no alerta de tooAzure de resposta.</span><span class="sxs-lookup"><span data-stu-id="772df-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="772df-135">Configurar um webhook de runbook e vincular tooalert.</span><span class="sxs-lookup"><span data-stu-id="772df-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="772df-136">Autenticado com token de segurança na URL.</span><span class="sxs-lookup"><span data-stu-id="772df-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="772df-137">Agenda</span><span class="sxs-lookup"><span data-stu-id="772df-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="772df-138">Inicie automaticamente o runbook em um cronograma horário, diário, semanal ou mensal.</span><span class="sxs-lookup"><span data-stu-id="772df-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="772df-139">Manipule a agenda pelo portal do Azure, por cmdlets do PowerShell ou pela a API do Azure.</span><span class="sxs-lookup"><span data-stu-id="772df-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="772df-140">Fornece toobe de valores de parâmetro usado com a agenda.</span><span class="sxs-lookup"><span data-stu-id="772df-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="772df-141">De Outro Runbook</span><span class="sxs-lookup"><span data-stu-id="772df-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="772df-142">Use um runbook como uma atividade em outro runbook.</span><span class="sxs-lookup"><span data-stu-id="772df-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="772df-143">É útil para funcionalidades usadas por vários runbooks.</span><span class="sxs-lookup"><span data-stu-id="772df-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="772df-144">Forneça o runbook de toochild de valores de parâmetro e use a saída no runbook pai.</span><span class="sxs-lookup"><span data-stu-id="772df-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="772df-145">Olá imagem a seguir ilustra processo passo a passo detalhado Olá ciclo de vida de um runbook.</span><span class="sxs-lookup"><span data-stu-id="772df-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="772df-146">Ele inclui formas diferentes que um runbook for iniciado na automação do Azure, os componentes necessários para runbooks de automação do Azure tooexecute Hybrid Runbook Worker e as interações entre diferentes componentes.</span><span class="sxs-lookup"><span data-stu-id="772df-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="772df-147">toolearn sobre a execução de runbooks de automação em seu data center, consulte muito[operadores de runbook híbrido](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="772df-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Arquitetura do runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="772df-149">Iniciando um runbook com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="772df-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="772df-150">No portal do Azure de Olá, selecione **automação** e, em seguida, clique em nome de saudação de uma conta de automação.</span><span class="sxs-lookup"><span data-stu-id="772df-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="772df-151">No menu de Hub hello, selecione **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="772df-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="772df-152">Em Olá **Runbooks** folha, selecione um runbook e, em seguida, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="772df-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="772df-153">Se Olá runbook tiver parâmetros, será solicitado tooprovide valores com uma caixa de texto para cada parâmetro.</span><span class="sxs-lookup"><span data-stu-id="772df-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="772df-154">Confira [Parâmetros de runbook](#Runbook-parameters) abaixo para mais detalhes sobre os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="772df-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="772df-155">Em Olá **trabalho** folha, você pode exibir o status de Olá Olá do trabalho de runbook.</span><span class="sxs-lookup"><span data-stu-id="772df-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="772df-156">Iniciando um runbook com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="772df-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="772df-157">Você pode usar o hello [AzureRmAutomationRunbook início](https://msdn.microsoft.com/library/mt603661.aspx) toostart um runbook com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="772df-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="772df-158">Olá, código de exemplo seguinte inicia um runbook chamado Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="772df-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="772df-159">Retorna AzureRmAutomationRunbook iniciar um trabalho do objeto que você pode usar tootrack seu status depois Olá runbook for iniciado.</span><span class="sxs-lookup"><span data-stu-id="772df-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="772df-160">Você pode usar esse objeto de trabalho com [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine status de saudação do trabalho hello e [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget sua saída.</span><span class="sxs-lookup"><span data-stu-id="772df-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="772df-161">Olá, código de exemplo a seguir inicia um runbook chamado Test-Runbook, aguarda até que ele seja concluído e exibe seu resultado.</span><span class="sxs-lookup"><span data-stu-id="772df-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="772df-162">Se Olá runbook exigir parâmetros, você deve fornecê-los como um [hashtable](http://technet.microsoft.com/library/hh847780.aspx) onde correspondências de chave de saudação da tabela de hash Olá Olá parâmetro e valor Olá são o valor do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="772df-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="772df-163">Olá exemplo a seguir mostra como toostart um runbook com dois parâmetros de cadeia de caracteres chamado FirstName e LastName, um número inteiro denominado RepeatCount e um parâmetro booleano denominado Show.</span><span class="sxs-lookup"><span data-stu-id="772df-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="772df-164">Para saber mais sobre parâmetros, confira [Parâmetros de runbook](#Runbook-parameters) abaixo.</span><span class="sxs-lookup"><span data-stu-id="772df-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="772df-165">Parâmetros de runbook</span><span class="sxs-lookup"><span data-stu-id="772df-165">Runbook parameters</span></span>
<span data-ttu-id="772df-166">Quando você inicia um runbook de saudação Portal do Azure ou o Windows PowerShell, a instrução de saudação é enviada pelo Olá serviço da web de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="772df-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="772df-167">Esse serviço não dá suporte a parâmetros com tipos de dados complexos.</span><span class="sxs-lookup"><span data-stu-id="772df-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="772df-168">Se você precisar tooprovide um valor para um parâmetro complexo, é necessário chamá-lo embutido de outro runbook conforme descrito em [filho runbooks na automação do Azure](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="772df-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="772df-169">saudação de serviço da web de automação do Azure fornecerá uma funcionalidade especial para parâmetros usando certos tipos de dados, conforme descrito nas seções a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="772df-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="772df-170">Valores nomeados</span><span class="sxs-lookup"><span data-stu-id="772df-170">Named values</span></span>
<span data-ttu-id="772df-171">Se parâmetro hello é do tipo de dados [object], você pode usar o hello após toosend do formato JSON ele uma lista de valores nomeados: *{Nome1: 'Valor1', Name2: 'Value2', nome3: 'Value3'}*.</span><span class="sxs-lookup"><span data-stu-id="772df-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="772df-172">Esses valores devem ser tipos simples.</span><span class="sxs-lookup"><span data-stu-id="772df-172">These values must be simple types.</span></span> <span data-ttu-id="772df-173">Olá runbook receberá o parâmetro hello como um [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) com propriedades que correspondem a tooeach valor nomeado.</span><span class="sxs-lookup"><span data-stu-id="772df-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="772df-174">Considere Olá runbook de teste que aceita um parâmetro chamado de usuário a seguir.</span><span class="sxs-lookup"><span data-stu-id="772df-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="772df-175">Olá seguinte texto pode ser usado para o parâmetro de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="772df-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="772df-176">Isso resulta em Olá saída a seguir.</span><span class="sxs-lookup"><span data-stu-id="772df-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="772df-177">Matrizes</span><span class="sxs-lookup"><span data-stu-id="772df-177">Arrays</span></span>
<span data-ttu-id="772df-178">Se o parâmetro hello é uma matriz, como [matriz] ou [string []], em seguida, você pode usar Olá toosend do formato JSON a seguir ele uma lista de valores: *[Value1, Value2, Value3]*.</span><span class="sxs-lookup"><span data-stu-id="772df-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="772df-179">Esses valores devem ser tipos simples.</span><span class="sxs-lookup"><span data-stu-id="772df-179">These values must be simple types.</span></span>

<span data-ttu-id="772df-180">Considere Olá seguinte runbook de teste que aceita um parâmetro chamado *usuário*.</span><span class="sxs-lookup"><span data-stu-id="772df-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="772df-181">Olá seguinte texto pode ser usado para o parâmetro de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="772df-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="772df-182">Isso resulta em Olá saída a seguir.</span><span class="sxs-lookup"><span data-stu-id="772df-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="772df-183">Credenciais</span><span class="sxs-lookup"><span data-stu-id="772df-183">Credentials</span></span>
<span data-ttu-id="772df-184">Se o parâmetro hello é o tipo de dados **PSCredential**, em seguida, você pode fornecer o nome de saudação de um objeto de automação do Azure [ativo de credencial](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="772df-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="772df-185">Olá runbook recuperará credencial Olá com nome hello que você especificar.</span><span class="sxs-lookup"><span data-stu-id="772df-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="772df-186">Considere Olá runbook de teste que aceita um parâmetro chamado credencial a seguir.</span><span class="sxs-lookup"><span data-stu-id="772df-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="772df-187">Olá seguinte texto pode ser usado para o parâmetro de usuário Olá supondo que havia um ativo de credencial chamado *minhas credenciais*.</span><span class="sxs-lookup"><span data-stu-id="772df-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="772df-188">Supondo que tenha sido Olá nome de usuário na credencial Olá *jsmith*, isso resulta em Olá saída a seguir.</span><span class="sxs-lookup"><span data-stu-id="772df-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="772df-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="772df-189">Next steps</span></span>
* <span data-ttu-id="772df-190">arquitetura de runbook Olá no artigo atual fornece uma visão geral do gerenciamento de recursos no Azure e local com hello Hybrid Runbook Worker runbooks.</span><span class="sxs-lookup"><span data-stu-id="772df-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="772df-191">toolearn sobre a execução de runbooks de automação em seu data center, consulte muito[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="772df-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="772df-192">toolearn mais sobre Olá criar runbooks modular toobe usada por outros runbooks para funções específicas ou comuns, consulte muito[Runbooks filho](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="772df-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>

