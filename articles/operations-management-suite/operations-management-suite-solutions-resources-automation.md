---
title: "Recursos de Automação do Azure em soluções do OMS | Microsoft Docs"
description: "Soluções em OMS normalmente incluirão runbooks na automação do Azure para automatizar processos, como a coleta e o processamento de dados de monitoramento.  Este artigo descreve como incluir runbooks e seus recursos relacionados em uma solução."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c1909183a33ed03d8165671cff25cc8b83b77733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="3fa3a-104">Adição de recursos de Automação do Azure a uma solução de gerenciamento do OMS (Preview)</span><span class="sxs-lookup"><span data-stu-id="3fa3a-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="3fa3a-105">Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="3fa3a-106">Os esquemas descritos a seguir estão sujeitos a alterações.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="3fa3a-107">[Soluções de gerenciamento em OMS](operations-management-suite-solutions.md) normalmente incluirão runbooks na automação do Azure para automatizar processos, como a coleta e o processamento de dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="3fa3a-108">Além de runbooks, contas de automação incluem ativos, como variáveis e agendas que dão suporte a runbooks usados na solução.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="3fa3a-109">Este artigo descreve como incluir runbooks e seus recursos relacionados em uma solução.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="3fa3a-110">Os exemplos neste artigo usam parâmetros e variáveis que são necessários ou comuns para as soluções de gerenciamento e estão descritos em [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md) (Criando soluções de gerenciamento no OMS (Operations Management Suite))</span><span class="sxs-lookup"><span data-stu-id="3fa3a-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="3fa3a-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3fa3a-111">Prerequisites</span></span>
<span data-ttu-id="3fa3a-112">Este artigo pressupõe que você já esteja familiarizado com as informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="3fa3a-113">Como [criar uma solução de gerenciamento](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="3fa3a-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="3fa3a-114">A estrutura de um [arquivo de solução](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="3fa3a-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="3fa3a-115">Como [criar modelos do Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="3fa3a-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="3fa3a-116">Conta de automação</span><span class="sxs-lookup"><span data-stu-id="3fa3a-116">Automation account</span></span>
<span data-ttu-id="3fa3a-117">Todos os recursos na Automação do Azure estão contidos em um [Conta de automação](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="3fa3a-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="3fa3a-118">Conforme descrito no [espaço de trabalho OMS e conta de automação](operations-management-suite-solutions.md#oms-workspace-and-automation-account), a conta de automação não está incluída na solução de gerenciamento, mas deve existir antes que a solução seja instalada.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="3fa3a-119">Se ela não estiver disponível, a instalação da solução falhará.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="3fa3a-120">O nome de cada recurso de Automação inclui o nome de sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="3fa3a-121">Isso é feito na solução com o parâmetro **accountName**, conforme descrito no exemplo a seguir de um recurso de runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="3fa3a-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="3fa3a-122">Runbooks</span></span>
<span data-ttu-id="3fa3a-123">Você deve incluir todos os runbooks usados pela solução no arquivo de solução para que eles sejam criados quando a solução for instalada.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="3fa3a-124">No entanto, você não pode incluir o corpo do runbook no modelo, de modo que é preciso publicar o runbook em um local público onde ele possa ser acessado por qualquer usuário que esteja instalando sua solução.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="3fa3a-125">Os recursos do [runbook de Automação do Azure](../automation/automation-runbook-types.md) têm o tipo **Microsoft.Automation/automationAccounts/runbooks** e a estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="3fa3a-126">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="3fa3a-127">As propriedades dos runbooks são descritas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="3fa3a-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3fa3a-128">Property</span></span> | <span data-ttu-id="3fa3a-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fa3a-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="3fa3a-130">runbookType</span></span> |<span data-ttu-id="3fa3a-131">Especifica os tipos de runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="3fa3a-132">Script – Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fa3a-132">Script - PowerShell script</span></span> <br><span data-ttu-id="3fa3a-133">PowerShell – Fluxo de trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fa3a-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="3fa3a-134">GraphPowerShell – Runbook de script do PowerShell gráfico</span><span class="sxs-lookup"><span data-stu-id="3fa3a-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="3fa3a-135">GraphPowerShellWorkflow – Runbook de fluxo de trabalho do PowerShell gráfico</span><span class="sxs-lookup"><span data-stu-id="3fa3a-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="3fa3a-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="3fa3a-136">logProgress</span></span> |<span data-ttu-id="3fa3a-137">Especifica se [registros de progresso](../automation/automation-runbook-output-and-messages.md) devem ser gerados para o runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="3fa3a-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="3fa3a-138">logVerbose</span></span> |<span data-ttu-id="3fa3a-139">Especifica se [registros detalhados](../automation/automation-runbook-output-and-messages.md) devem ser gerados para o runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="3fa3a-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-140">description</span></span> |<span data-ttu-id="3fa3a-141">Descrição opcional para o runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="3fa3a-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="3fa3a-142">publishContentLink</span></span> |<span data-ttu-id="3fa3a-143">Especifica o conteúdo do runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="3fa3a-144">uri – URI do conteúdo do runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="3fa3a-145">Ele será um arquivo .ps1 para runbooks do PowerShell e Script e um arquivo de runbook gráfico exportado para um runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="3fa3a-146">versão – a versão do runbook para seu próprio acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="3fa3a-147">Trabalhos de automação</span><span class="sxs-lookup"><span data-stu-id="3fa3a-147">Automation jobs</span></span>
<span data-ttu-id="3fa3a-148">Quando você inicia um runbook na Automação do Azure, isso cria um trabalho de automação.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="3fa3a-149">Você pode adicionar um recurso de trabalho de automação à solução para iniciar um runbook automaticamente quando a solução de gerenciamento for instalada.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="3fa3a-150">Esse método normalmente é usado para iniciar runbooks que são usados para a configuração inicial da solução.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="3fa3a-151">Para iniciar um runbook em intervalos regulares, crie um [agendamento](#schedules) e um [agendamento de trabalho](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="3fa3a-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="3fa3a-152">Os recursos de trabalho têm o tipo **Microsoft.Automation/automationAccounts/jobs** e a estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="3fa3a-153">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="3fa3a-154">As propriedades dos trabalhos de automação são descritas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="3fa3a-155">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3fa3a-155">Property</span></span> | <span data-ttu-id="3fa3a-156">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fa3a-157">runbook</span><span class="sxs-lookup"><span data-stu-id="3fa3a-157">runbook</span></span> |<span data-ttu-id="3fa3a-158">Entidade de único nome com o nome do runbook a ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="3fa3a-159">parameters</span><span class="sxs-lookup"><span data-stu-id="3fa3a-159">parameters</span></span> |<span data-ttu-id="3fa3a-160">Entidade para cada valor de parâmetro exigido pelo runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="3fa3a-161">O trabalho inclui o nome do runbook e valores de parâmetro a ser enviado para o runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="3fa3a-162">O trabalho deve [depender](operations-management-suite-solutions-solution-file.md#resources) do runbook que está sendo iniciado, uma vez que o runbook deve ser criado antes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="3fa3a-163">Caso tenha vários runbooks que devam ser iniciados, você pode definir a ordem deles com um trabalho que dependa de qualquer outro trabalho que deva ser executado primeiro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="3fa3a-164">O nome de um recurso de trabalho deve conter um GUID que normalmente é atribuído por um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="3fa3a-165">Você pode ler mais sobre os parâmetros GUID em [Criando soluções no OMS (Operations Management Suite)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="3fa3a-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="3fa3a-166">Certificados</span><span class="sxs-lookup"><span data-stu-id="3fa3a-166">Certificates</span></span>
<span data-ttu-id="3fa3a-167">Os [certificados de Automação do Azure](../automation/automation-certificates.md) têm o tipo **Microsoft.Automation/automationAccounts/certificates** e a estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="3fa3a-168">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="3fa3a-169">As propriedades dos recursos de Certificado são descritas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="3fa3a-170">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3fa3a-170">Property</span></span> | <span data-ttu-id="3fa3a-171">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fa3a-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="3fa3a-172">base64Value</span></span> |<span data-ttu-id="3fa3a-173">O valor de base 64 do certificado.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="3fa3a-174">impressão digital</span><span class="sxs-lookup"><span data-stu-id="3fa3a-174">thumbprint</span></span> |<span data-ttu-id="3fa3a-175">A impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="3fa3a-176">Credenciais</span><span class="sxs-lookup"><span data-stu-id="3fa3a-176">Credentials</span></span>
<span data-ttu-id="3fa3a-177">As [credenciais de Automação do Azure](../automation/automation-credentials.md) têm o tipo **Microsoft.Automation/automationAccounts/credentials** e a estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="3fa3a-178">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="3fa3a-179">As propriedades dos recursos de Credencial são descritas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="3fa3a-180">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3fa3a-180">Property</span></span> | <span data-ttu-id="3fa3a-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fa3a-182">userName</span><span class="sxs-lookup"><span data-stu-id="3fa3a-182">userName</span></span> |<span data-ttu-id="3fa3a-183">Nome de usuário da credencial.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-183">User name for the credential.</span></span> |
| <span data-ttu-id="3fa3a-184">Senha</span><span class="sxs-lookup"><span data-stu-id="3fa3a-184">password</span></span> |<span data-ttu-id="3fa3a-185">Senha da credencial.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="3fa3a-186">Agendas</span><span class="sxs-lookup"><span data-stu-id="3fa3a-186">Schedules</span></span>
<span data-ttu-id="3fa3a-187">Os [agendamentos de Automação do Azure](../automation/automation-schedules.md) têm o tipo **Microsoft.Automation/automationAccounts/schedules** e a estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="3fa3a-188">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="3fa3a-189">As propriedades de recursos de agendamento são descritas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="3fa3a-190">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3fa3a-190">Property</span></span> | <span data-ttu-id="3fa3a-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fa3a-192">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-192">description</span></span> |<span data-ttu-id="3fa3a-193">Descrição opcional para o agendamento.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="3fa3a-194">startTime</span><span class="sxs-lookup"><span data-stu-id="3fa3a-194">startTime</span></span> |<span data-ttu-id="3fa3a-195">Especifica a hora de início de uma agenda como um objeto DateTime.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="3fa3a-196">Uma cadeia de caracteres pode ser fornecida se ele for convertido em um DateTime válido.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="3fa3a-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="3fa3a-197">isEnabled</span></span> |<span data-ttu-id="3fa3a-198">Especifica se o agendamento está habilitado.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="3fa3a-199">intervalo</span><span class="sxs-lookup"><span data-stu-id="3fa3a-199">interval</span></span> |<span data-ttu-id="3fa3a-200">O tipo de intervalo para o agendamento.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="3fa3a-201">dia</span><span class="sxs-lookup"><span data-stu-id="3fa3a-201">day</span></span><br><span data-ttu-id="3fa3a-202">hora</span><span class="sxs-lookup"><span data-stu-id="3fa3a-202">hour</span></span> |
| <span data-ttu-id="3fa3a-203">frequência</span><span class="sxs-lookup"><span data-stu-id="3fa3a-203">frequency</span></span> |<span data-ttu-id="3fa3a-204">Frequência em que o agendamento deve ser disparado em número de dias ou horas.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="3fa3a-205">Os agendamentos devem ter um horário de início com um valor posterior ao horário atual.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="3fa3a-206">Você não pode fornecer esse valor com uma variável, uma vez que não teria como saber quando ele vai ser instalado.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="3fa3a-207">Use uma das duas estratégias a seguir ao usar os recursos de agendamento em uma solução.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="3fa3a-208">Use um parâmetro para o horário de início do agendamento.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="3fa3a-209">Essa ação solicitará que o usuário forneça um valor quando instalar a solução.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="3fa3a-210">Caso tenha vários agendamentos, você poderá usar um único valor de parâmetro para mais de um deles.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="3fa3a-211">Crie os agendamentos usando um runbook que comece quando a solução é instalada.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="3fa3a-212">Isso elimina a necessidade de o usuário especificar um horário, mas você não pode incluir o agendamento na sua solução, de modo que ele será removido quando a solução for removida.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="3fa3a-213">Agendas de trabalho</span><span class="sxs-lookup"><span data-stu-id="3fa3a-213">Job schedules</span></span>
<span data-ttu-id="3fa3a-214">Os recursos de agendamento vinculam um runbook a um agendamento.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="3fa3a-215">Eles têm o tipo **Microsoft.Automation/automationAccounts/jobSchedules** e a estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="3fa3a-216">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="3fa3a-217">As propriedades dos agendamentos de trabalho são descritas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="3fa3a-218">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3fa3a-218">Property</span></span> | <span data-ttu-id="3fa3a-219">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fa3a-220">nome do agendamento</span><span class="sxs-lookup"><span data-stu-id="3fa3a-220">schedule name</span></span> |<span data-ttu-id="3fa3a-221">Entidade de único **nome** com o nome do agendamento.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="3fa3a-222">nome do runbook</span><span class="sxs-lookup"><span data-stu-id="3fa3a-222">runbook name</span></span>  |<span data-ttu-id="3fa3a-223">Uma entidade com **nome** único com o nome do runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="3fa3a-224">Variáveis</span><span class="sxs-lookup"><span data-stu-id="3fa3a-224">Variables</span></span>
<span data-ttu-id="3fa3a-225">As [variáveis de Automação do Azure](../automation/automation-variables.md) têm o tipo **Microsoft.Automation/automationAccounts/variables** e a estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="3fa3a-226">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="3fa3a-227">As propriedades dos recursos de variáveis são descritas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="3fa3a-228">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3fa3a-228">Property</span></span> | <span data-ttu-id="3fa3a-229">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fa3a-230">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-230">description</span></span> | <span data-ttu-id="3fa3a-231">Descrição opcional para a variável.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="3fa3a-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="3fa3a-232">isEncrypted</span></span> | <span data-ttu-id="3fa3a-233">Especifica se a variável deve ser criptografada.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="3fa3a-234">Tipo</span><span class="sxs-lookup"><span data-stu-id="3fa3a-234">type</span></span> | <span data-ttu-id="3fa3a-235">Essa propriedade atualmente está sem efeito.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-235">This property currently has no effect.</span></span>  <span data-ttu-id="3fa3a-236">O tipo de dados da variável será determinado pelo valor inicial.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="3fa3a-237">value</span><span class="sxs-lookup"><span data-stu-id="3fa3a-237">value</span></span> | <span data-ttu-id="3fa3a-238">Valor da variável.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="3fa3a-239">Atualmente, a propriedade **type** não tem efeito sobre a variável que está sendo criada.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="3fa3a-240">O tipo de dados para a variável será determinado pelo valor.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="3fa3a-241">Se você definir o valor inicial da variável, ele deverá ser definido como o tipo de dados correto.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="3fa3a-242">A tabela a seguir fornece os diferentes tipos de dados permitidos e sua sintaxe.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="3fa3a-243">Observe que os valores em JSON devem sempre ser colocados entre aspas com caracteres especiais entre aspas.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="3fa3a-244">Por exemplo, um valor de cadeia de caracteres deve ser especificado por aspas em volta da cadeia de caracteres (usando o caractere de escape \\) enquanto um valor numérico deve ser especificado por um conjunto de aspas.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="3fa3a-245">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="3fa3a-245">Data type</span></span> | <span data-ttu-id="3fa3a-246">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-246">Description</span></span> | <span data-ttu-id="3fa3a-247">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3fa3a-247">Example</span></span> | <span data-ttu-id="3fa3a-248">É resolvido desta forma</span><span class="sxs-lookup"><span data-stu-id="3fa3a-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="3fa3a-249">string</span><span class="sxs-lookup"><span data-stu-id="3fa3a-249">string</span></span>   | <span data-ttu-id="3fa3a-250">Coloque o valor entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="3fa3a-251">"\"Olá, Mundo\""</span><span class="sxs-lookup"><span data-stu-id="3fa3a-251">"\"Hello world\""</span></span> | <span data-ttu-id="3fa3a-252">"Olá, Mundo"</span><span class="sxs-lookup"><span data-stu-id="3fa3a-252">"Hello world"</span></span> |
| <span data-ttu-id="3fa3a-253">numérico</span><span class="sxs-lookup"><span data-stu-id="3fa3a-253">numeric</span></span>  | <span data-ttu-id="3fa3a-254">Valor numérico com aspas simples.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="3fa3a-255">"64"</span><span class="sxs-lookup"><span data-stu-id="3fa3a-255">"64"</span></span> | <span data-ttu-id="3fa3a-256">64</span><span class="sxs-lookup"><span data-stu-id="3fa3a-256">64</span></span> |
| <span data-ttu-id="3fa3a-257">Booliano</span><span class="sxs-lookup"><span data-stu-id="3fa3a-257">boolean</span></span>  | <span data-ttu-id="3fa3a-258">**true** ou **false** entre aspas.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="3fa3a-259">Observe que esse valor deve estar em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="3fa3a-260">"true"</span><span class="sxs-lookup"><span data-stu-id="3fa3a-260">"true"</span></span> | <span data-ttu-id="3fa3a-261">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="3fa3a-261">true</span></span> |
| <span data-ttu-id="3fa3a-262">datetime</span><span class="sxs-lookup"><span data-stu-id="3fa3a-262">datetime</span></span> | <span data-ttu-id="3fa3a-263">Valor de data serializada.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-263">Serialized date value.</span></span><br><span data-ttu-id="3fa3a-264">Você pode usar o cmdlet ConvertTo-Json no PowerShell para gerar esse valor para uma determinada data.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="3fa3a-265">Exemplo: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="3fa3a-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="3fa3a-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="3fa3a-266">ConvertTo-Json</span></span> | <span data-ttu-id="3fa3a-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="3fa3a-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="3fa3a-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="3fa3a-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="3fa3a-269">Módulos</span><span class="sxs-lookup"><span data-stu-id="3fa3a-269">Modules</span></span>
<span data-ttu-id="3fa3a-270">Sua solução de gerenciamento não precisa definir [módulos globais](../automation/automation-integration-modules.md) usados pelos seus runbooks porque eles sempre estarão disponíveis na conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-270">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="3fa3a-271">Você precisa incluir um recurso para qualquer outro módulo usado pelos seus runbooks.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-271">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="3fa3a-272">Os [módulos de integração](../automation/automation-integration-modules.md) têm o tipo **Microsoft.Automation/automationAccounts/modules** e a estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="3fa3a-273">Isso inclui variáveis e parâmetros comuns para que você possa copiar e colar este trecho de código em seu arquivo de solução e alterar os nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="3fa3a-274">As propriedades dos recursos de módulo são descritas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-274">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="3fa3a-275">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3fa3a-275">Property</span></span> | <span data-ttu-id="3fa3a-276">Descrição</span><span class="sxs-lookup"><span data-stu-id="3fa3a-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3fa3a-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="3fa3a-277">contentLink</span></span> |<span data-ttu-id="3fa3a-278">Especifica o conteúdo do módulo.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-278">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="3fa3a-279">uri – Uri para o conteúdo do módulo.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-279">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="3fa3a-280">Ele será um arquivo .ps1 para runbooks do PowerShell e Script e um arquivo de runbook gráfico exportado para um runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="3fa3a-281">version – a versão do módulo para seu próprio acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-281">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="3fa3a-282">O runbook deve depender do recurso de módulo para garantir que ele seja criado antes do runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-282">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="3fa3a-283">Atualizando módulos</span><span class="sxs-lookup"><span data-stu-id="3fa3a-283">Updating modules</span></span>
<span data-ttu-id="3fa3a-284">Se você atualizar uma solução de gerenciamento que inclui um runbook que usa um agendamento e a nova versão da solução tiver um novo módulo usado pelo runbook, o runbook poderá usar a versão antiga do módulo.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-284">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="3fa3a-285">Você deve incluir os seguintes runbooks em sua solução e criar um trabalho para executá-los antes de quaisquer outros runbooks.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-285">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="3fa3a-286">Isso garantirá que todos os módulos estejam atualizados como necessário antes que os runbooks sejam carregados.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-286">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="3fa3a-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) garantirá que todos os módulos usados por runbooks em sua solução tenham a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="3fa3a-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) registrará novamente todos os recursos de agendamento para garantir que os runbooks vinculados a eles usem os módulos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="3fa3a-289">Amostra</span><span class="sxs-lookup"><span data-stu-id="3fa3a-289">Sample</span></span>
<span data-ttu-id="3fa3a-290">A seguir está um exemplo de uma solução que inclua que inclui os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="3fa3a-290">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="3fa3a-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-291">Runbook.</span></span>  <span data-ttu-id="3fa3a-292">É um exemplo de runbook armazenado em um repositório público do GitHub.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="3fa3a-293">O trabalho de Automação que inicia o runbook quando a solução é instalada.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-293">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="3fa3a-294">O agendamento e o agendamento de trabalho para iniciar o runbook em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-294">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="3fa3a-295">Certificado.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-295">Certificate.</span></span>
- <span data-ttu-id="3fa3a-296">Credencial.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-296">Credential.</span></span>
- <span data-ttu-id="3fa3a-297">Variável.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-297">Variable.</span></span>
- <span data-ttu-id="3fa3a-298">Módulo.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-298">Module.</span></span>  <span data-ttu-id="3fa3a-299">Esse é o [módulo OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) para gravar dados no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-299">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="3fa3a-300">O exemplo usa [parâmetros de solução padrão](operations-management-suite-solutions-solution-file.md#parameters) variáveis que normalmente seriam usados em uma solução em vez de embutir valores nas definições de recurso.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-300">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="3fa3a-301">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3fa3a-301">Next steps</span></span>
* <span data-ttu-id="3fa3a-302">[Adicione um modo de exibição à sua solução](operations-management-suite-solutions-resources-views.md) para visualizar os dados coletados.</span><span class="sxs-lookup"><span data-stu-id="3fa3a-302">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
