---
title: "recursos de automação de aaaAzure em soluções do OMS | Microsoft Docs"
description: "Soluções do OMS normalmente incluirá runbooks na automação do Azure tooautomate processos, como a coleta e processamento de dados de monitoramento.  Este artigo descreve como tooinclude runbooks e seus recursos relacionados em uma solução."
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
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="21ebc-104">Adicionando a solução de gerenciamento de OMS para tooan de recursos automação do Azure (visualização)</span><span class="sxs-lookup"><span data-stu-id="21ebc-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="21ebc-105">Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="21ebc-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="21ebc-106">Qualquer esquema descrita abaixo é toochange de assunto.</span><span class="sxs-lookup"><span data-stu-id="21ebc-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="21ebc-107">[Soluções de gerenciamento do OMS](operations-management-suite-solutions.md) geralmente inclui runbooks na automação do Azure tooautomate processos, como a coleta e processamento de dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="21ebc-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="21ebc-108">Além disso toorunbooks, contas de automação inclui ativos como variáveis e agendas que dão suporte a runbooks Olá usado na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="21ebc-109">Este artigo descreve como tooinclude runbooks e seus recursos relacionados em uma solução.</span><span class="sxs-lookup"><span data-stu-id="21ebc-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="21ebc-110">Olá exemplos neste artigo usam parâmetros e variáveis que são ambos soluções toomanagement necessárias ou comuns e descritos na [criando soluções de gerenciamento no OMS Operations Management Suite ()](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="21ebc-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="21ebc-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="21ebc-111">Prerequisites</span></span>
<span data-ttu-id="21ebc-112">Este artigo pressupõe que você já estiver familiarizado com hello informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="21ebc-113">Como muito[criar uma solução de gerenciamento](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="21ebc-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="21ebc-114">Olá a estrutura de um [arquivo de solução](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="21ebc-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="21ebc-115">Como muito[criar modelos do Gerenciador de recursos](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="21ebc-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="21ebc-116">Conta de automação</span><span class="sxs-lookup"><span data-stu-id="21ebc-116">Automation account</span></span>
<span data-ttu-id="21ebc-117">Todos os recursos na Automação do Azure estão contidos em um [Conta de automação](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="21ebc-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="21ebc-118">Conforme descrito em [OMS espaço de trabalho e a conta de automação](operations-management-suite-solutions.md#oms-workspace-and-automation-account) Olá conta de automação não está incluído na solução de gerenciamento de hello, mas deve existir antes de saudação solução estiver instalada.</span><span class="sxs-lookup"><span data-stu-id="21ebc-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="21ebc-119">Se não estiver disponível, Olá solução instalação falhará.</span><span class="sxs-lookup"><span data-stu-id="21ebc-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="21ebc-120">nome de saudação de cada recurso de automação inclui nome de saudação de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="21ebc-121">Isso é feito na solução de saudação com hello **accountName** parâmetro como Olá exemplo de um recurso de runbook a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="21ebc-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="21ebc-122">Runbooks</span></span>
<span data-ttu-id="21ebc-123">Você deve incluir todos os runbooks usados pela solução de saudação no arquivo de solução Olá para que eles são criados quando Olá solução estiver instalada.</span><span class="sxs-lookup"><span data-stu-id="21ebc-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="21ebc-124">Você não pode conter o corpo de saudação do runbook Olá no modelo de saudação, para que você deve publicar Olá runbook tooa local público em que ele possa ser acessado por qualquer usuário que instalar sua solução.</span><span class="sxs-lookup"><span data-stu-id="21ebc-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="21ebc-125">[Runbook de automação do Azure](../automation/automation-runbook-types.md) recursos têm um tipo de **Microsoft.Automation/automationAccounts/runbooks** e ter Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="21ebc-126">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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


<span data-ttu-id="21ebc-127">Propriedades de saudação para runbooks são descritas Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="21ebc-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21ebc-128">Property</span></span> | <span data-ttu-id="21ebc-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="21ebc-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21ebc-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="21ebc-130">runbookType</span></span> |<span data-ttu-id="21ebc-131">Especifica os tipos de saudação de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="21ebc-132">Script – Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="21ebc-132">Script - PowerShell script</span></span> <br><span data-ttu-id="21ebc-133">PowerShell – Fluxo de trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="21ebc-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="21ebc-134">GraphPowerShell – Runbook de script do PowerShell gráfico</span><span class="sxs-lookup"><span data-stu-id="21ebc-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="21ebc-135">GraphPowerShellWorkflow – Runbook de fluxo de trabalho do PowerShell gráfico</span><span class="sxs-lookup"><span data-stu-id="21ebc-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="21ebc-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="21ebc-136">logProgress</span></span> |<span data-ttu-id="21ebc-137">Especifica se [registros de progresso](../automation/automation-runbook-output-and-messages.md) devem ser gerados para Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="21ebc-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="21ebc-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="21ebc-138">logVerbose</span></span> |<span data-ttu-id="21ebc-139">Especifica se [registros detalhados](../automation/automation-runbook-output-and-messages.md) devem ser gerados para Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="21ebc-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="21ebc-140">description</span><span class="sxs-lookup"><span data-stu-id="21ebc-140">description</span></span> |<span data-ttu-id="21ebc-141">Descrição opcional para o runbook hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="21ebc-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="21ebc-142">publishContentLink</span></span> |<span data-ttu-id="21ebc-143">Especifica o conteúdo de saudação do runbook hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="21ebc-144">URI - Uri toohello conteúdo de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="21ebc-145">Ele será um arquivo .ps1 para runbooks do PowerShell e Script e um arquivo de runbook gráfico exportado para um runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="21ebc-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="21ebc-146">versão - versão de runbook Olá para o seu próprio controle.</span><span class="sxs-lookup"><span data-stu-id="21ebc-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="21ebc-147">Trabalhos de automação</span><span class="sxs-lookup"><span data-stu-id="21ebc-147">Automation jobs</span></span>
<span data-ttu-id="21ebc-148">Quando você inicia um runbook na Automação do Azure, isso cria um trabalho de automação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="21ebc-149">Você pode adicionar um automação trabalho tooyour solução tooautomatically início um runbook quando a solução de gerenciamento de saudação está instalada.</span><span class="sxs-lookup"><span data-stu-id="21ebc-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="21ebc-150">Esse método é geralmente usados toostart runbooks que são usados para a configuração inicial de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="21ebc-151">toostart um runbook em intervalos regulares, criar um [agenda](#schedules) e um [agenda de trabalho](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="21ebc-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="21ebc-152">Recursos de trabalho têm um tipo de **Microsoft.Automation/automationAccounts/jobs** e ter Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="21ebc-153">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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

<span data-ttu-id="21ebc-154">Propriedades de saudação para trabalhos de automação são descritas Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="21ebc-155">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21ebc-155">Property</span></span> | <span data-ttu-id="21ebc-156">Descrição</span><span class="sxs-lookup"><span data-stu-id="21ebc-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21ebc-157">runbook</span><span class="sxs-lookup"><span data-stu-id="21ebc-157">runbook</span></span> |<span data-ttu-id="21ebc-158">Entidade de nome único com o nome de saudação do hello runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="21ebc-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="21ebc-159">parâmetros</span><span class="sxs-lookup"><span data-stu-id="21ebc-159">parameters</span></span> |<span data-ttu-id="21ebc-160">Entidade para cada valor de parâmetro exigido pelo runbook hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="21ebc-161">trabalho de saudação inclui nome do runbook hello e qualquer toobe de valores de parâmetro enviado toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="21ebc-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="21ebc-162">trabalho de saudação deve [dependem](operations-management-suite-solutions-solution-file.md#resources) runbook Olá que ele está sendo iniciado desde Olá runbook deve ser criado antes do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="21ebc-163">Caso tenha vários runbooks que devam ser iniciados, você pode definir a ordem deles com um trabalho que dependa de qualquer outro trabalho que deva ser executado primeiro.</span><span class="sxs-lookup"><span data-stu-id="21ebc-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="21ebc-164">nome de saudação de um recurso de trabalho deve conter um GUID que normalmente é atribuído por um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="21ebc-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="21ebc-165">Você pode ler mais sobre os parâmetros GUID em [Criando soluções no OMS (Operations Management Suite)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="21ebc-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="21ebc-166">Certificados</span><span class="sxs-lookup"><span data-stu-id="21ebc-166">Certificates</span></span>
<span data-ttu-id="21ebc-167">[Certificados de automação do Azure](../automation/automation-certificates.md) têm um tipo de **Microsoft.Automation/automationAccounts/certificates** e ter Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="21ebc-168">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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



<span data-ttu-id="21ebc-169">Propriedades de saudação para recursos de certificados são descritas Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="21ebc-170">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21ebc-170">Property</span></span> | <span data-ttu-id="21ebc-171">Descrição</span><span class="sxs-lookup"><span data-stu-id="21ebc-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21ebc-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="21ebc-172">base64Value</span></span> |<span data-ttu-id="21ebc-173">Valor de base 64 para o certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="21ebc-174">impressão digital</span><span class="sxs-lookup"><span data-stu-id="21ebc-174">thumbprint</span></span> |<span data-ttu-id="21ebc-175">Impressão digital do certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="21ebc-176">Credenciais</span><span class="sxs-lookup"><span data-stu-id="21ebc-176">Credentials</span></span>
<span data-ttu-id="21ebc-177">[As credenciais de automação do Azure](../automation/automation-credentials.md) têm um tipo de **Microsoft.Automation/automationAccounts/credentials** e ter Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="21ebc-178">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


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

<span data-ttu-id="21ebc-179">Propriedades de saudação para recursos de credencial são descritas Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="21ebc-180">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21ebc-180">Property</span></span> | <span data-ttu-id="21ebc-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="21ebc-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21ebc-182">userName</span><span class="sxs-lookup"><span data-stu-id="21ebc-182">userName</span></span> |<span data-ttu-id="21ebc-183">Nome de usuário para credencial hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-183">User name for hello credential.</span></span> |
| <span data-ttu-id="21ebc-184">Senha</span><span class="sxs-lookup"><span data-stu-id="21ebc-184">password</span></span> |<span data-ttu-id="21ebc-185">Senha da credencial de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="21ebc-186">Agendas</span><span class="sxs-lookup"><span data-stu-id="21ebc-186">Schedules</span></span>
<span data-ttu-id="21ebc-187">[Agendas de automação do Azure](../automation/automation-schedules.md) têm um tipo de **Microsoft.Automation/automationAccounts/schedules** e ter Olá Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="21ebc-188">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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

<span data-ttu-id="21ebc-189">Propriedades de saudação para recursos de agendamento são descritas Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="21ebc-190">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21ebc-190">Property</span></span> | <span data-ttu-id="21ebc-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="21ebc-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21ebc-192">description</span><span class="sxs-lookup"><span data-stu-id="21ebc-192">description</span></span> |<span data-ttu-id="21ebc-193">Descrição opcional para a agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="21ebc-194">startTime</span><span class="sxs-lookup"><span data-stu-id="21ebc-194">startTime</span></span> |<span data-ttu-id="21ebc-195">Especifica a hora de início de saudação de uma agenda como um objeto DateTime.</span><span class="sxs-lookup"><span data-stu-id="21ebc-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="21ebc-196">Uma cadeia de caracteres pode ser fornecida se ele puder ser convertido tooa DateTime válido.</span><span class="sxs-lookup"><span data-stu-id="21ebc-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="21ebc-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="21ebc-197">isEnabled</span></span> |<span data-ttu-id="21ebc-198">Especifica se Olá agenda está habilitada.</span><span class="sxs-lookup"><span data-stu-id="21ebc-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="21ebc-199">intervalo</span><span class="sxs-lookup"><span data-stu-id="21ebc-199">interval</span></span> |<span data-ttu-id="21ebc-200">tipo de saudação do intervalo de agendamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="21ebc-201">dia</span><span class="sxs-lookup"><span data-stu-id="21ebc-201">day</span></span><br><span data-ttu-id="21ebc-202">hora</span><span class="sxs-lookup"><span data-stu-id="21ebc-202">hour</span></span> |
| <span data-ttu-id="21ebc-203">frequência</span><span class="sxs-lookup"><span data-stu-id="21ebc-203">frequency</span></span> |<span data-ttu-id="21ebc-204">Frequência de Olá agenda deve ser disparada no número de dias ou horas.</span><span class="sxs-lookup"><span data-stu-id="21ebc-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="21ebc-205">As agendas devem ter uma hora de início com um valor maior que Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="21ebc-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="21ebc-206">Você não pode fornecer esse valor com uma variável, desde que você teria que não há como saber quando ele é toobe será instalado.</span><span class="sxs-lookup"><span data-stu-id="21ebc-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="21ebc-207">Use uma das duas estratégias a seguir ao usar os recursos de agendamento em uma solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="21ebc-208">Use um parâmetro de hora de início de saudação da agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="21ebc-209">Essa ação solicitará Olá usuário tooprovide um valor ao instalar a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="21ebc-210">Caso tenha vários agendamentos, você poderá usar um único valor de parâmetro para mais de um deles.</span><span class="sxs-lookup"><span data-stu-id="21ebc-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="21ebc-211">Crie agendas hello usando um runbook que é iniciado quando Olá solução estiver instalada.</span><span class="sxs-lookup"><span data-stu-id="21ebc-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="21ebc-212">Isso elimina a necessidade de saudação do hello usuário toospecify uma hora, mas você não pode conter agenda Olá em sua solução para que ela será removida quando a solução de saudação é removida.</span><span class="sxs-lookup"><span data-stu-id="21ebc-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="21ebc-213">Agendas de trabalho</span><span class="sxs-lookup"><span data-stu-id="21ebc-213">Job schedules</span></span>
<span data-ttu-id="21ebc-214">Os recursos de agendamento vinculam um runbook a um agendamento.</span><span class="sxs-lookup"><span data-stu-id="21ebc-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="21ebc-215">Eles têm um tipo de **Microsoft.Automation/automationAccounts/jobSchedules** e ter Olá Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="21ebc-216">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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


<span data-ttu-id="21ebc-217">Propriedades de saudação para agendas de trabalho são descritas Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="21ebc-218">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21ebc-218">Property</span></span> | <span data-ttu-id="21ebc-219">Descrição</span><span class="sxs-lookup"><span data-stu-id="21ebc-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21ebc-220">nome do agendamento</span><span class="sxs-lookup"><span data-stu-id="21ebc-220">schedule name</span></span> |<span data-ttu-id="21ebc-221">Único **nome** entidade com o nome de saudação da agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="21ebc-222">nome do runbook</span><span class="sxs-lookup"><span data-stu-id="21ebc-222">runbook name</span></span>  |<span data-ttu-id="21ebc-223">Único **nome** entidade com o nome de saudação do runbook hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="21ebc-224">variáveis</span><span class="sxs-lookup"><span data-stu-id="21ebc-224">Variables</span></span>
<span data-ttu-id="21ebc-225">[As variáveis de automação do Azure](../automation/automation-variables.md) têm um tipo de **Microsoft.Automation/automationAccounts/variables** e ter Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="21ebc-226">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

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

<span data-ttu-id="21ebc-227">Propriedades de saudação para recursos variáveis são descritas Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="21ebc-228">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21ebc-228">Property</span></span> | <span data-ttu-id="21ebc-229">Descrição</span><span class="sxs-lookup"><span data-stu-id="21ebc-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21ebc-230">description</span><span class="sxs-lookup"><span data-stu-id="21ebc-230">description</span></span> | <span data-ttu-id="21ebc-231">Descrição opcional para a variável de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="21ebc-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="21ebc-232">isEncrypted</span></span> | <span data-ttu-id="21ebc-233">Especifica se a variável de saudação deve ser criptografado.</span><span class="sxs-lookup"><span data-stu-id="21ebc-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="21ebc-234">type</span><span class="sxs-lookup"><span data-stu-id="21ebc-234">type</span></span> | <span data-ttu-id="21ebc-235">Essa propriedade atualmente está sem efeito.</span><span class="sxs-lookup"><span data-stu-id="21ebc-235">This property currently has no effect.</span></span>  <span data-ttu-id="21ebc-236">tipo de dados de saudação da variável Olá será determinado pelo valor de saudação inicial.</span><span class="sxs-lookup"><span data-stu-id="21ebc-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="21ebc-237">valor</span><span class="sxs-lookup"><span data-stu-id="21ebc-237">value</span></span> | <span data-ttu-id="21ebc-238">Valor de variável de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="21ebc-239">Olá **tipo** propriedade atualmente não tem nenhum efeito na variável hello está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="21ebc-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="21ebc-240">saudação de tipo de dados para a variável de saudação será determinado pelo valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="21ebc-241">Se você definir o valor inicial de saudação de variável Olá, ela deve ser definida como Olá tipo de dados correto.</span><span class="sxs-lookup"><span data-stu-id="21ebc-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="21ebc-242">Olá, a tabela a seguir fornece Olá diferentes tipos de dados permitidos e sua sintaxe.</span><span class="sxs-lookup"><span data-stu-id="21ebc-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="21ebc-243">Observe que os valores em JSON são esperados tooalways ser colocado entre aspas com caracteres especiais entre aspas hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="21ebc-244">Por exemplo, um valor de cadeia de caracteres deve ser especificado pela cadeia de caracteres hello aspas (usando o caractere de escape de saudação (\\)) enquanto um valor numérico deve ser especificado com um conjunto de aspas.</span><span class="sxs-lookup"><span data-stu-id="21ebc-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="21ebc-245">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="21ebc-245">Data type</span></span> | <span data-ttu-id="21ebc-246">Descrição</span><span class="sxs-lookup"><span data-stu-id="21ebc-246">Description</span></span> | <span data-ttu-id="21ebc-247">Exemplo</span><span class="sxs-lookup"><span data-stu-id="21ebc-247">Example</span></span> | <span data-ttu-id="21ebc-248">Resolve muito</span><span class="sxs-lookup"><span data-stu-id="21ebc-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="21ebc-249">string</span><span class="sxs-lookup"><span data-stu-id="21ebc-249">string</span></span>   | <span data-ttu-id="21ebc-250">Coloque o valor entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="21ebc-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="21ebc-251">"\"Olá, Mundo\""</span><span class="sxs-lookup"><span data-stu-id="21ebc-251">"\"Hello world\""</span></span> | <span data-ttu-id="21ebc-252">"Olá, Mundo"</span><span class="sxs-lookup"><span data-stu-id="21ebc-252">"Hello world"</span></span> |
| <span data-ttu-id="21ebc-253">numérico</span><span class="sxs-lookup"><span data-stu-id="21ebc-253">numeric</span></span>  | <span data-ttu-id="21ebc-254">Valor numérico com aspas simples.</span><span class="sxs-lookup"><span data-stu-id="21ebc-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="21ebc-255">"64"</span><span class="sxs-lookup"><span data-stu-id="21ebc-255">"64"</span></span> | <span data-ttu-id="21ebc-256">64</span><span class="sxs-lookup"><span data-stu-id="21ebc-256">64</span></span> |
| <span data-ttu-id="21ebc-257">Booliano</span><span class="sxs-lookup"><span data-stu-id="21ebc-257">boolean</span></span>  | <span data-ttu-id="21ebc-258">**true** ou **false** entre aspas.</span><span class="sxs-lookup"><span data-stu-id="21ebc-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="21ebc-259">Observe que esse valor deve estar em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="21ebc-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="21ebc-260">"true"</span><span class="sxs-lookup"><span data-stu-id="21ebc-260">"true"</span></span> | <span data-ttu-id="21ebc-261">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="21ebc-261">true</span></span> |
| <span data-ttu-id="21ebc-262">datetime</span><span class="sxs-lookup"><span data-stu-id="21ebc-262">datetime</span></span> | <span data-ttu-id="21ebc-263">Valor de data serializada.</span><span class="sxs-lookup"><span data-stu-id="21ebc-263">Serialized date value.</span></span><br><span data-ttu-id="21ebc-264">Você pode usar o cmdlet ConvertTo-Json Olá toogenerate PowerShell esse valor para uma determinada data.</span><span class="sxs-lookup"><span data-stu-id="21ebc-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="21ebc-265">Exemplo: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="21ebc-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="21ebc-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="21ebc-266">ConvertTo-Json</span></span> | <span data-ttu-id="21ebc-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="21ebc-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="21ebc-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="21ebc-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="21ebc-269">Módulos</span><span class="sxs-lookup"><span data-stu-id="21ebc-269">Modules</span></span>
<span data-ttu-id="21ebc-270">Sua solução de gerenciamento não precisa toodefine [módulos global](../automation/automation-integration-modules.md) usado por seus runbooks porque sempre estarão disponíveis em sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="21ebc-271">É necessário tooinclude um recurso para qualquer outro módulo usado por seus runbooks.</span><span class="sxs-lookup"><span data-stu-id="21ebc-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="21ebc-272">[Módulos de integração](../automation/automation-integration-modules.md) têm um tipo de **Microsoft.Automation/automationAccounts/modules** e ter Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="21ebc-273">Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

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


<span data-ttu-id="21ebc-274">Propriedades de saudação para recursos do módulo são descritas Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="21ebc-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="21ebc-275">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21ebc-275">Property</span></span> | <span data-ttu-id="21ebc-276">Descrição</span><span class="sxs-lookup"><span data-stu-id="21ebc-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21ebc-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="21ebc-277">contentLink</span></span> |<span data-ttu-id="21ebc-278">Especifica o conteúdo de saudação do módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="21ebc-279">URI - Uri toohello conteúdo Olá módulo.</span><span class="sxs-lookup"><span data-stu-id="21ebc-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="21ebc-280">Ele será um arquivo .ps1 para runbooks do PowerShell e Script e um arquivo de runbook gráfico exportado para um runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="21ebc-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="21ebc-281">versão - versão do módulo de saudação para seu próprio controle.</span><span class="sxs-lookup"><span data-stu-id="21ebc-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="21ebc-282">Olá runbook deve depender Olá tooensure de recurso de módulo que foi criado antes de runbook hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="21ebc-283">Atualizando módulos</span><span class="sxs-lookup"><span data-stu-id="21ebc-283">Updating modules</span></span>
<span data-ttu-id="21ebc-284">Se você atualizar uma solução de gerenciamento que inclui um runbook que usa uma agenda e Olá nova versão da solução tem um novo módulo usado por esse runbook, runbook Olá pode usar a versão antiga saudação do módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="21ebc-285">Você deve incluir Olá runbooks em sua solução a seguir e criar um trabalho toorun-as antes de quaisquer outros runbooks.</span><span class="sxs-lookup"><span data-stu-id="21ebc-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="21ebc-286">Isso garantirá que todos os módulos são atualizados como Olá necessária antes de carregar os runbooks.</span><span class="sxs-lookup"><span data-stu-id="21ebc-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="21ebc-287">[Atualização ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) garantirá que todos os módulos de saudação usados por runbooks em sua solução estão na versão mais recente hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="21ebc-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) registrar novamente todos Olá agenda recursos tooensure Olá runbooks vinculados toothem com módulos mais recentes do uso hello.</span><span class="sxs-lookup"><span data-stu-id="21ebc-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="21ebc-289">Amostra</span><span class="sxs-lookup"><span data-stu-id="21ebc-289">Sample</span></span>
<span data-ttu-id="21ebc-290">A seguir está um exemplo de uma solução que incluem que inclui Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="21ebc-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="21ebc-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="21ebc-291">Runbook.</span></span>  <span data-ttu-id="21ebc-292">É um exemplo de runbook armazenado em um repositório público do GitHub.</span><span class="sxs-lookup"><span data-stu-id="21ebc-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="21ebc-293">Trabalho de automação que inicia o runbook hello quando Olá solução estiver instalada.</span><span class="sxs-lookup"><span data-stu-id="21ebc-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="21ebc-294">Agenda e trabalho de agendamento toostart Olá runbook em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="21ebc-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="21ebc-295">Certificado.</span><span class="sxs-lookup"><span data-stu-id="21ebc-295">Certificate.</span></span>
- <span data-ttu-id="21ebc-296">Credencial.</span><span class="sxs-lookup"><span data-stu-id="21ebc-296">Credential.</span></span>
- <span data-ttu-id="21ebc-297">Variável.</span><span class="sxs-lookup"><span data-stu-id="21ebc-297">Variable.</span></span>
- <span data-ttu-id="21ebc-298">Módulo.</span><span class="sxs-lookup"><span data-stu-id="21ebc-298">Module.</span></span>  <span data-ttu-id="21ebc-299">Isso é hello [OMSIngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) para gravar dados tooLog análise.</span><span class="sxs-lookup"><span data-stu-id="21ebc-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="21ebc-300">Olá exemplo usa [parâmetros de solução padrão](operations-management-suite-solutions-solution-file.md#parameters) variáveis que normalmente seriam usados em uma solução como oposição toohardcoding valores nas definições de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="21ebc-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


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
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
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




## <a name="next-steps"></a><span data-ttu-id="21ebc-301">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21ebc-301">Next steps</span></span>
* <span data-ttu-id="21ebc-302">[Adicionar uma solução do modo de exibição tooyour](operations-management-suite-solutions-resources-views.md) toovisualize coletados dados.</span><span class="sxs-lookup"><span data-stu-id="21ebc-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
