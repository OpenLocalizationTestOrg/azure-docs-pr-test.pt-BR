---
title: "parâmetros de entrada aaaRunbook | Microsoft Docs"
description: "Parâmetros de entrada do runbook aumentam a flexibilidade de saudação de runbooks, permitindo-lhe toopass dados tooa runbook quando ele for iniciado. Este artigo descreve os diferentes cenários em que os parâmetros de entrada são usados em runbooks."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="b12ab-104">Parâmetros de entrada do Runbook</span><span class="sxs-lookup"><span data-stu-id="b12ab-104">Runbook input parameters</span></span>
<span data-ttu-id="b12ab-105">Parâmetros de entrada do runbook aumentam a flexibilidade de saudação de runbooks, permitindo-lhe toopass dados tooit quando ele for iniciado.</span><span class="sxs-lookup"><span data-stu-id="b12ab-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="b12ab-106">Olá permitem Olá runbook ações toobe direcionado para ambientes e cenários específicos.</span><span class="sxs-lookup"><span data-stu-id="b12ab-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="b12ab-107">Neste artigo, vamos orientá-lo quanto aos diferentes cenários em que os parâmetros de entrada são usados em runbooks.</span><span class="sxs-lookup"><span data-stu-id="b12ab-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="b12ab-108">Como configurar parâmetros de entrada</span><span class="sxs-lookup"><span data-stu-id="b12ab-108">Configure input parameters</span></span>
<span data-ttu-id="b12ab-109">Parâmetros de entrada podem ser configurados no PowerShell, no Fluxo de Trabalho do PowerShell e em runbooks gráficos.</span><span class="sxs-lookup"><span data-stu-id="b12ab-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="b12ab-110">Um runbook pode ter vários parâmetros com tipos de dados diferentes, ou não ter nenhum parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b12ab-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="b12ab-111">Os parâmetros de entrada podem ser obrigatório ou opcionais, e você pode atribuir um valor padrão para parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="b12ab-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="b12ab-112">Você pode atribuir valores toohello parâmetros de entrada para um runbook quando você iniciá-lo por meio de um dos métodos disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="b12ab-113">Esses métodos incluem iniciando um runbook do portal de saudação ou um serviço da web.</span><span class="sxs-lookup"><span data-stu-id="b12ab-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="b12ab-114">Você também pode iniciá-lo como um runbook filho, que é chamado de embutido em outro runbook.</span><span class="sxs-lookup"><span data-stu-id="b12ab-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="b12ab-115">Como configurar parâmetros de entrada no PowerShell e em runbooks do Fluxo de Trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b12ab-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="b12ab-116">PowerShell e [runbooks do fluxo de trabalho do PowerShell](automation-first-runbook-textual.md) na automação do Azure oferecem suporte a parâmetros de entrada que são definidos por meio de saudação atributos a seguir.</span><span class="sxs-lookup"><span data-stu-id="b12ab-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="b12ab-117">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="b12ab-117">**Property**</span></span> | <span data-ttu-id="b12ab-118">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="b12ab-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="b12ab-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="b12ab-119">Type</span></span> |<span data-ttu-id="b12ab-120">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b12ab-120">Required.</span></span> <span data-ttu-id="b12ab-121">tipo de dados Olá esperado para o valor do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="b12ab-122">Qualquer tipo .NET é válido.</span><span class="sxs-lookup"><span data-stu-id="b12ab-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="b12ab-123">Nome</span><span class="sxs-lookup"><span data-stu-id="b12ab-123">Name</span></span> |<span data-ttu-id="b12ab-124">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b12ab-124">Required.</span></span> <span data-ttu-id="b12ab-125">nome de saudação do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-125">hello name of hello parameter.</span></span> <span data-ttu-id="b12ab-126">Isso deve ser exclusivo dentro de runbook Olá e pode conter apenas letras, números ou caracteres de sublinhado.</span><span class="sxs-lookup"><span data-stu-id="b12ab-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="b12ab-127">Deve começar com uma letra.</span><span class="sxs-lookup"><span data-stu-id="b12ab-127">It must start with a letter.</span></span> |
| <span data-ttu-id="b12ab-128">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b12ab-128">Mandatory</span></span> |<span data-ttu-id="b12ab-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-129">Optional.</span></span> <span data-ttu-id="b12ab-130">Especifica se deve ser fornecido um valor para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="b12ab-131">Se você definir esta opção muito**$true**, em seguida, um valor deve ser fornecido quando Olá runbook for iniciado.</span><span class="sxs-lookup"><span data-stu-id="b12ab-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="b12ab-132">Se você definir esta opção muito**$false**, em seguida, um valor é opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="b12ab-133">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="b12ab-133">Default value</span></span> |<span data-ttu-id="b12ab-134">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-134">Optional.</span></span>  <span data-ttu-id="b12ab-135">Especifica um valor que será usado para o parâmetro hello se um valor não for passado quando Olá runbook for iniciado.</span><span class="sxs-lookup"><span data-stu-id="b12ab-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="b12ab-136">Um valor padrão pode ser definido para qualquer parâmetro e fará automaticamente parâmetro hello opcional independentemente Olá configuração obrigatória.</span><span class="sxs-lookup"><span data-stu-id="b12ab-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="b12ab-137">O Windows PowerShell dá suporte a mais atributos de parâmetros de entrada do que aqueles listados aqui, como validação, aliases e conjuntos de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b12ab-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="b12ab-138">No entanto, automação do Azure atualmente suporta apenas Olá parâmetros de entrada listados acima.</span><span class="sxs-lookup"><span data-stu-id="b12ab-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="b12ab-139">Uma definição de parâmetro no fluxo de trabalho do PowerShell runbooks tem Olá seguindo o formato geral, onde vários parâmetros são separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="b12ab-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="b12ab-140">Quando você está definindo parâmetros, se você não especificar Olá **obrigatório** atributo, em seguida, por padrão, o parâmetro hello é considerado opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="b12ab-141">Além disso, se você definir um valor padrão para um parâmetro em runbooks de fluxo de trabalho do PowerShell, ele será tratado pelo PowerShell como um parâmetro opcional, independentemente de saudação **obrigatório** valor do atributo.</span><span class="sxs-lookup"><span data-stu-id="b12ab-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="b12ab-142">Por exemplo, vamos configurar parâmetros de entrada hello para um runbook de fluxo de trabalho do PowerShell que gera os detalhes sobre as máquinas virtuais, uma única VM ou todas as máquinas virtuais dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b12ab-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="b12ab-143">Este runbook tem dois parâmetros, conforme mostrado no hello captura de tela a seguir: nome de saudação da máquina virtual e o nome de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b12ab-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![Fluxo de trabalho do PowerShell de automação](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="b12ab-145">Nesta definição de parâmetro, Olá parâmetros **$VMName** e **$resourceGroupName** são parâmetros simples do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="b12ab-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="b12ab-146">No entanto, o PowerShell e os runbooks do Fluxo de Trabalho do PowerShell dão suporte a todos os tipos simples e complexos, como **objeto** ou **PSCredential** para parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="b12ab-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="b12ab-147">Se seu runbook tem um parâmetro de entrada de tipo de objeto, em seguida, use uma tabela de hash com (nome, valor) do PowerShell pares toopass em um valor.</span><span class="sxs-lookup"><span data-stu-id="b12ab-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="b12ab-148">Por exemplo, se você tiver Olá parâmetro em um runbook a seguir:</span><span class="sxs-lookup"><span data-stu-id="b12ab-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="b12ab-149">Em seguida, você pode passar Olá parâmetro toohello de valor a seguir:</span><span class="sxs-lookup"><span data-stu-id="b12ab-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="b12ab-150">Como configurar parâmetros de entrada em runbooks gráficos</span><span class="sxs-lookup"><span data-stu-id="b12ab-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="b12ab-151">muito[configurar um runbook gráfico](automation-first-runbook-graphical.md) com parâmetros de entrada, vamos criar um runbook gráfico que gera os detalhes sobre as máquinas virtuais, ou uma única VM ou todas as máquinas virtuais dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b12ab-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="b12ab-152">A configuração de um runbook consiste em duas atividades principais, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="b12ab-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="b12ab-153">[**Autenticar Runbooks com a conta executar como do Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate com o Azure.</span><span class="sxs-lookup"><span data-stu-id="b12ab-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="b12ab-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget propriedades de saudação de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b12ab-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="b12ab-155">Você pode usar o hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) nomes de hello atividade toooutput de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="b12ab-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="b12ab-156">Hello atividade **Get-AzureRmVm** aceita dois parâmetros, hello **nome da máquina virtual** e hello **nome do grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="b12ab-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="b12ab-157">Como esses parâmetros podem exigir valores diferentes cada vez que iniciar o runbook hello, você pode adicionar parâmetros de entrada tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="b12ab-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="b12ab-158">Aqui estão os parâmetros de entrada hello etapas tooadd:</span><span class="sxs-lookup"><span data-stu-id="b12ab-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="b12ab-159">Selecione Olá runbook gráfico de saudação **Runbooks** folha e depois clique em [ **editar** ](automation-graphical-authoring-intro.md) -lo.</span><span class="sxs-lookup"><span data-stu-id="b12ab-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="b12ab-160">No editor de runbook hello, clique em **de entrada e saída** tooopen Olá **de entrada e saída** folha.</span><span class="sxs-lookup"><span data-stu-id="b12ab-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![Runbook gráfico de automação](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="b12ab-162">Olá **de entrada e saída** folha exibe uma lista de parâmetros de entrada que são definidos para o runbook hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="b12ab-163">Nesta folha, você pode adicionar um novo parâmetro de entrada ou Editar configuração de saudação de um parâmetro de entrada existente.</span><span class="sxs-lookup"><span data-stu-id="b12ab-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="b12ab-164">tooadd um novo parâmetro hello runbook, clique em **Adicionar entrada** tooopen Olá **parâmetro de entrada do Runbook** folha.</span><span class="sxs-lookup"><span data-stu-id="b12ab-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="b12ab-165">Lá, você pode configurar Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="b12ab-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="b12ab-166">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="b12ab-166">**Property**</span></span> | <span data-ttu-id="b12ab-167">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="b12ab-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b12ab-168">Nome</span><span class="sxs-lookup"><span data-stu-id="b12ab-168">Name</span></span> |<span data-ttu-id="b12ab-169">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b12ab-169">Required.</span></span>  <span data-ttu-id="b12ab-170">nome de saudação do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-170">hello name of hello parameter.</span></span> <span data-ttu-id="b12ab-171">Isso deve ser exclusivo dentro de runbook Olá e pode conter apenas letras, números ou caracteres de sublinhado.</span><span class="sxs-lookup"><span data-stu-id="b12ab-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="b12ab-172">Deve começar com uma letra.</span><span class="sxs-lookup"><span data-stu-id="b12ab-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="b12ab-173">Descrição</span><span class="sxs-lookup"><span data-stu-id="b12ab-173">Description</span></span> |<span data-ttu-id="b12ab-174">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-174">Optional.</span></span> <span data-ttu-id="b12ab-175">Descrição sobre a finalidade de saudação do parâmetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="b12ab-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="b12ab-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="b12ab-176">Type</span></span> |<span data-ttu-id="b12ab-177">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-177">Optional.</span></span> <span data-ttu-id="b12ab-178">tipo de dados de saudação esperada para o valor do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="b12ab-179">Os tipos de parâmetro com suporte são **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** e **Object**.</span><span class="sxs-lookup"><span data-stu-id="b12ab-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="b12ab-180">Se um tipo de dados não estiver selecionado, o padrão é muito**cadeia de caracteres**.</span><span class="sxs-lookup"><span data-stu-id="b12ab-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="b12ab-181">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b12ab-181">Mandatory</span></span> |<span data-ttu-id="b12ab-182">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-182">Optional.</span></span> <span data-ttu-id="b12ab-183">Especifica se deve ser fornecido um valor para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="b12ab-184">Se você escolher **Sim**, em seguida, um valor deve ser fornecido quando Olá runbook for iniciado.</span><span class="sxs-lookup"><span data-stu-id="b12ab-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="b12ab-185">Se você escolher **sem**, em seguida, um valor não é necessário quando Olá runbook for iniciado, e um valor padrão pode ser definido.</span><span class="sxs-lookup"><span data-stu-id="b12ab-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="b12ab-186">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="b12ab-186">Default Value</span></span> |<span data-ttu-id="b12ab-187">Opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-187">Optional.</span></span> <span data-ttu-id="b12ab-188">Especifica um valor que será usado para o parâmetro hello se um valor não for passado quando Olá runbook for iniciado.</span><span class="sxs-lookup"><span data-stu-id="b12ab-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="b12ab-189">Um valor padrão pode ser definido para um parâmetro que não é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b12ab-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="b12ab-190">tooset um valor padrão, escolha **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="b12ab-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="b12ab-191">Esse valor é usado, a menos que outro valor seja fornecido quando Olá runbook for iniciado.</span><span class="sxs-lookup"><span data-stu-id="b12ab-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="b12ab-192">Escolha **nenhum** se você não quiser tooprovide qualquer valor padrão.</span><span class="sxs-lookup"><span data-stu-id="b12ab-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![Como adicionar nova entrada](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="b12ab-194">Crie dois parâmetros com hello seguintes propriedades que serão usadas pelo Olá **AzureRmVm Get** atividade:</span><span class="sxs-lookup"><span data-stu-id="b12ab-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="b12ab-195">**Parameter1:**</span><span class="sxs-lookup"><span data-stu-id="b12ab-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="b12ab-196">Nome - VMName</span><span class="sxs-lookup"><span data-stu-id="b12ab-196">Name - VMName</span></span>
     * <span data-ttu-id="b12ab-197">Tipo - String</span><span class="sxs-lookup"><span data-stu-id="b12ab-197">Type - String</span></span>
     * <span data-ttu-id="b12ab-198">Obrigatório - Não</span><span class="sxs-lookup"><span data-stu-id="b12ab-198">Mandatory - No</span></span>
   * <span data-ttu-id="b12ab-199">**Parameter2:**</span><span class="sxs-lookup"><span data-stu-id="b12ab-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="b12ab-200">Nome - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b12ab-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="b12ab-201">Tipo - String</span><span class="sxs-lookup"><span data-stu-id="b12ab-201">Type - String</span></span>
     * <span data-ttu-id="b12ab-202">Obrigatório - Não</span><span class="sxs-lookup"><span data-stu-id="b12ab-202">Mandatory - No</span></span>
     * <span data-ttu-id="b12ab-203">Valor padrão - Personalizado</span><span class="sxs-lookup"><span data-stu-id="b12ab-203">Default value - Custom</span></span>
     * <span data-ttu-id="b12ab-204">O valor padrão personalizado - \<nome saudação do grupo de recursos que contém máquinas virtuais de hello ></span><span class="sxs-lookup"><span data-stu-id="b12ab-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="b12ab-205">Depois de adicionar parâmetros de saudação, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b12ab-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="b12ab-206">Agora você pode exibi-las no hello **entrada e saída blade**.</span><span class="sxs-lookup"><span data-stu-id="b12ab-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="b12ab-207">Clique em **OK** novamente e clique em **Salvar** e **Publicar** o runbook.</span><span class="sxs-lookup"><span data-stu-id="b12ab-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="b12ab-208">Atribuir valores de parâmetros de tooinput em runbooks</span><span class="sxs-lookup"><span data-stu-id="b12ab-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="b12ab-209">Você pode passar valores tooinput parâmetros em runbooks em Olá cenários a seguir.</span><span class="sxs-lookup"><span data-stu-id="b12ab-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="b12ab-210">Iniciar um runbook e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="b12ab-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="b12ab-211">Um runbook pode ser iniciado de várias maneiras: por meio de saudação portal do Azure, com um webhook, com os cmdlets do PowerShell, com hello API REST ou com hello SDK.</span><span class="sxs-lookup"><span data-stu-id="b12ab-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="b12ab-212">A seguir, discutiremos diferentes métodos para iniciar um runbook e atribuir parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b12ab-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="b12ab-213">Iniciar um runbook publicado usando Olá portal do Azure e atribuir os parâmetros</span><span class="sxs-lookup"><span data-stu-id="b12ab-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="b12ab-214">Quando você [iniciar runbook Olá](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), Olá **iniciar Runbook** folha é aberto e você pode configurar valores de parâmetros de saudação que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="b12ab-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Começar a usar o portal de saudação](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="b12ab-216">Em rótulo Olá abaixo da caixa de entrada hello, você pode ver atributos Olá que foram definidos para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="b12ab-217">Os atributos incluem obrigatório ou opcional, tipo e valor padrão.</span><span class="sxs-lookup"><span data-stu-id="b12ab-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="b12ab-218">No hello ajuda balão próxima toohello nome de parâmetro, você pode ver todas as informações de chave Olá necessário toomake decisões sobre valores de entrada de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b12ab-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="b12ab-219">Essas informações incluem se um parâmetro é obrigatório ou opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="b12ab-220">Ele também inclui Olá tipo e valor padrão (se houver) e outras observações úteis.</span><span class="sxs-lookup"><span data-stu-id="b12ab-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![Balão de ajuda](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="b12ab-222">Parâmetros do tipo String dão suporte a valores de Cadeia de Caracteres **Vazia** .</span><span class="sxs-lookup"><span data-stu-id="b12ab-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="b12ab-223">Inserir **[EmptyString]** no parâmetro de entrada hello caixa passará um parâmetro de toohello de cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="b12ab-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="b12ab-224">Além disso, parâmetros do tipo de cadeia de caracteres não dão suporte à passagem de valores **Nulos** .</span><span class="sxs-lookup"><span data-stu-id="b12ab-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="b12ab-225">Se não passar qualquer parâmetro de cadeia de caracteres do valor toohello, em seguida, PowerShell interpretará como nulo.</span><span class="sxs-lookup"><span data-stu-id="b12ab-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="b12ab-226">Como iniciar um runbook publicado usando cmdlets do PowerShell e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="b12ab-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="b12ab-227">**Cmdlets do Azure Resource Manager:** você pode iniciar um runbook de Automação criado em um grupo de recursos usando [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="b12ab-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="b12ab-228">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="b12ab-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="b12ab-229">**Cmdlets de gerenciamento de serviços do azure:** você pode iniciar um runbook de automação criado em um grupo de recursos padrão usando [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx)</span><span class="sxs-lookup"><span data-stu-id="b12ab-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="b12ab-230">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="b12ab-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="b12ab-231">Quando você inicia um runbook usando cmdlets do PowerShell, um parâmetro padrão, **MicrosoftApplicationManagementStartedBy** é criado com o valor de saudação **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b12ab-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="b12ab-232">Você pode exibir esse parâmetro no hello **detalhes do trabalho** folha.</span><span class="sxs-lookup"><span data-stu-id="b12ab-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="b12ab-233">Como uniciar um runbook usando o SDK e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="b12ab-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="b12ab-234">**Método do Gerenciador de recursos do Azure:** pode iniciar um runbook usando Olá SDK de uma linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="b12ab-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="b12ab-235">Abaixo está um trecho de código em C# para iniciar um runbook em sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="b12ab-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="b12ab-236">Você pode exibir todos os códigos de saudação em nosso [repositório GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="b12ab-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="b12ab-237">**Método de gerenciamento de serviços do Azure:** pode iniciar um runbook usando Olá SDK de uma linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="b12ab-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="b12ab-238">Abaixo está um trecho de código em C# para iniciar um runbook em sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="b12ab-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="b12ab-239">Você pode exibir todos os códigos de saudação em nosso [repositório GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="b12ab-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="b12ab-240">toostart esse método, crie uma saudação do dicionário toostore parâmetros de runbook, **VMName** e **resourceGroupName**e seus valores.</span><span class="sxs-lookup"><span data-stu-id="b12ab-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="b12ab-241">Em seguida, inicie o runbook de hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-241">Then start hello runbook.</span></span> <span data-ttu-id="b12ab-242">Abaixo está o trecho de Olá c# código para chamar o método hello definida acima.</span><span class="sxs-lookup"><span data-stu-id="b12ab-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="b12ab-243">Iniciar um runbook usando a API REST de saudação e atribuir os parâmetros</span><span class="sxs-lookup"><span data-stu-id="b12ab-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="b12ab-244">Um trabalho de runbook pode ser criado e iniciado com hello API de REST de automação do Azure usando Olá **colocar** URI de solicitação do método com hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="b12ab-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="b12ab-245">No URI de solicitação hello, substitua Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="b12ab-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="b12ab-246">**subscription-id:** a ID de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12ab-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="b12ab-247">**nome do serviço de nuvem:** nome Olá Olá nuvem toowhich Olá de solicitação do serviço deve ser enviada.</span><span class="sxs-lookup"><span data-stu-id="b12ab-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="b12ab-248">**nome da conta de automação:** Olá sua conta de automação que está hospedada dentro de saudação especificado de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b12ab-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="b12ab-249">**id do trabalho:** hello GUID para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="b12ab-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="b12ab-250">GUIDs no PowerShell podem ser criados usando Olá **[GUID]::NewGuid(). ToString ()** comando.</span><span class="sxs-lookup"><span data-stu-id="b12ab-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="b12ab-251">No trabalho de runbook do toohello ordem toopass parâmetros, use o corpo da solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="b12ab-252">Ele usa Olá duas propriedades fornecidas no formato JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="b12ab-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="b12ab-253">**Nome do Runbook:** Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b12ab-253">**Runbook name:** Required.</span></span> <span data-ttu-id="b12ab-254">Olá nome do runbook Olá Olá toostart de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b12ab-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="b12ab-255">**Parâmetros do Runbook:** Opcional.</span><span class="sxs-lookup"><span data-stu-id="b12ab-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="b12ab-256">Um dicionário de lista de parâmetros de saudação (nome, valor) Formatar onde nome deve ser do tipo cadeia de caracteres e o valor pode ser qualquer valor JSON válido.</span><span class="sxs-lookup"><span data-stu-id="b12ab-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="b12ab-257">Se você quiser Olá toostart **Get-AzureVMTextual** runbook criado anteriormente com **VMName** e **resourceGroupName** como parâmetros, use Olá seguindo o formato JSON para o corpo da solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="b12ab-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="b12ab-258">Um código de status HTTP 201 será retornado se o trabalho de saudação é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="b12ab-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="b12ab-259">Para obter mais informações sobre cabeçalhos de resposta e o corpo da resposta hello, consulte o artigo toohello sobre como muito[criar um trabalho de runbook usando Olá API REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="b12ab-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="b12ab-260">Testar um runbook e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="b12ab-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="b12ab-261">Quando você [teste Olá versão de rascunho do runbook](automation-testing-runbook.md) usando a opção de teste hello, Olá **teste** folha é aberto e você pode configurar valores de parâmetros de saudação que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="b12ab-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Como testar e atribuir parâmetros](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="b12ab-263">Vincula um runbook tooa de agenda e atribuir os parâmetros</span><span class="sxs-lookup"><span data-stu-id="b12ab-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="b12ab-264">Você pode [vincular um agendamento](automation-schedules.md) tooyour runbook para esse runbook Olá inicia em um momento específico.</span><span class="sxs-lookup"><span data-stu-id="b12ab-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="b12ab-265">Você atribui parâmetros de entrada quando você criar agenda de saudação e Olá runbook usará esses valores quando ele for iniciado por agendamento Olá.</span><span class="sxs-lookup"><span data-stu-id="b12ab-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="b12ab-266">Você não pode salvar a agenda de saudação até que todos os valores de parâmetro obrigatório são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="b12ab-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![Como agendar e atribuir parâmetros](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="b12ab-268">Criar um webhook de um runbook e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="b12ab-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="b12ab-269">Você pode criar um [webhook](automation-webhooks.md) para seu runbook e configurar parâmetros de entrada do runbook.</span><span class="sxs-lookup"><span data-stu-id="b12ab-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="b12ab-270">Você não pode salvar o webhook Olá até que todos os valores de parâmetro obrigatório são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="b12ab-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![Como criar o webhook e atribuir parâmetros](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="b12ab-272">Quando você executar um runbook usando um webhook, Olá predefinidos de parâmetro de entrada  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  é enviada, juntamente com os parâmetros de entrada hello que você definiu.</span><span class="sxs-lookup"><span data-stu-id="b12ab-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="b12ab-273">Você pode clicar em Olá tooexpand **WebhookData** parâmetro para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="b12ab-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![Parâmetro WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="b12ab-275">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b12ab-275">Next steps</span></span>
* <span data-ttu-id="b12ab-276">Para obter mais informações sobre a entrada e a saída do runbook, consulte [Automação do Azure: entrada do runbook, saída e runbooks aninhados](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span><span class="sxs-lookup"><span data-stu-id="b12ab-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="b12ab-277">Para obter detalhes sobre as diferentes maneiras toostart um runbook, consulte [iniciando um runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b12ab-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="b12ab-278">tooedit um runbook textual, consulte muito[edição textual runbooks](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b12ab-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="b12ab-279">tooedit um runbook gráfico, consulte muito[criação gráfica na automação do Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b12ab-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

