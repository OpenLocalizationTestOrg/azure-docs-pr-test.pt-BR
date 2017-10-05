---
title: "Parâmetros de entrada de runbook| Microsoft Docs"
description: "Os parâmetros de entrada do runbook aumentam a flexibilidade dos runbooks permitindo transmitir dados para um runbook quando ele é iniciado. Este artigo descreve os diferentes cenários em que os parâmetros de entrada são usados em runbooks."
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
ms.openlocfilehash: 1ebf32338f5242e72eb2e2daa2da50d231f4b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="3ecb7-104">Parâmetros de entrada do Runbook</span><span class="sxs-lookup"><span data-stu-id="3ecb7-104">Runbook input parameters</span></span>
<span data-ttu-id="3ecb7-105">Os parâmetros de entrada do runbook aumentam a flexibilidade dos runbooks permitindo transmitir dados para este quando ele é iniciado.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span></span> <span data-ttu-id="3ecb7-106">Os parâmetros permitem que as ações de runbook sejam direcionadas para ambientes e cenários específicos.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span></span> <span data-ttu-id="3ecb7-107">Neste artigo, vamos orientá-lo quanto aos diferentes cenários em que os parâmetros de entrada são usados em runbooks.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="3ecb7-108">Como configurar parâmetros de entrada</span><span class="sxs-lookup"><span data-stu-id="3ecb7-108">Configure input parameters</span></span>
<span data-ttu-id="3ecb7-109">Parâmetros de entrada podem ser configurados no PowerShell, no Fluxo de Trabalho do PowerShell e em runbooks gráficos.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="3ecb7-110">Um runbook pode ter vários parâmetros com tipos de dados diferentes, ou não ter nenhum parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="3ecb7-111">Os parâmetros de entrada podem ser obrigatório ou opcionais, e você pode atribuir um valor padrão para parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="3ecb7-112">Você pode atribuir valores aos parâmetros de entrada para um runbook ao iniciá-lo por meio de um dos métodos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span></span> <span data-ttu-id="3ecb7-113">Esses métodos incluem a inicialização de um runbook a partir do portal ou de um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-113">These methods include starting  a runbook from the portal  or a web service.</span></span> <span data-ttu-id="3ecb7-114">Você também pode iniciá-lo como um runbook filho, que é chamado de embutido em outro runbook.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="3ecb7-115">Como configurar parâmetros de entrada no PowerShell e em runbooks do Fluxo de Trabalho do PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ecb7-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="3ecb7-116">O PowerShell e [runbooks de Fluxo de Trabalho do PowerShell](automation-first-runbook-textual.md) na Automação do Azure dão suporte a parâmetros de entrada definidos usando os atributos a seguir.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span></span>  

| <span data-ttu-id="3ecb7-117">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="3ecb7-117">**Property**</span></span> | <span data-ttu-id="3ecb7-118">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="3ecb7-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="3ecb7-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="3ecb7-119">Type</span></span> |<span data-ttu-id="3ecb7-120">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-120">Required.</span></span> <span data-ttu-id="3ecb7-121">O tipo de dados esperado para o valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-121">The data type expected for the parameter value.</span></span> <span data-ttu-id="3ecb7-122">Qualquer tipo .NET é válido.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="3ecb7-123">Nome</span><span class="sxs-lookup"><span data-stu-id="3ecb7-123">Name</span></span> |<span data-ttu-id="3ecb7-124">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-124">Required.</span></span> <span data-ttu-id="3ecb7-125">O nome do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-125">The name of the parameter.</span></span> <span data-ttu-id="3ecb7-126">Deve ser exclusivo no runbook e pode conter apenas letras, números ou caracteres de sublinhado.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="3ecb7-127">Deve começar com uma letra.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-127">It must start with a letter.</span></span> |
| <span data-ttu-id="3ecb7-128">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3ecb7-128">Mandatory</span></span> |<span data-ttu-id="3ecb7-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-129">Optional.</span></span> <span data-ttu-id="3ecb7-130">Especifica se deve ser fornecido um valor para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-130">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="3ecb7-131">Se você definir isso como **$true**, um valor deverá ser fornecido quando o runbook for iniciado.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="3ecb7-132">Se você definir isso como **$false**, um valor será opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-132">If you set this to **$false**, then a value is optional.</span></span> |
| <span data-ttu-id="3ecb7-133">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="3ecb7-133">Default value</span></span> |<span data-ttu-id="3ecb7-134">Opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-134">Optional.</span></span>  <span data-ttu-id="3ecb7-135">Especifica um valor que será usado para o parâmetro se um valor não for transmitido ao iniciar o runbook.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="3ecb7-136">Um valor padrão pode ser definido para qualquer parâmetro e tornará automaticamente o parâmetro opcional, independentemente da configuração obrigatória.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span></span> |

<span data-ttu-id="3ecb7-137">O Windows PowerShell dá suporte a mais atributos de parâmetros de entrada do que aqueles listados aqui, como validação, aliases e conjuntos de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="3ecb7-138">No entanto, a Automação do Azure atualmente dá suporte apenas aos parâmetros de entrada listados acima.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-138">However, Azure Automation currently supports only the input parameters listed above.</span></span>

<span data-ttu-id="3ecb7-139">Uma definição de parâmetro nos runbooks de Fluxo de Trabalho do PowerShell tem o formato geral a seguir, em que vários parâmetros são separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span></span>

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
> <span data-ttu-id="3ecb7-140">Ao definir parâmetros, se você não especificar o atributo **Mandatory** , por padrão, o parâmetro será considerado opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span></span> <span data-ttu-id="3ecb7-141">Além disso, se você definir um valor padrão para um parâmetro em runbooks de Fluxo de Trabalho do PowerShell, ele será tratado pelo PowerShell como um parâmetro opcional, independentemente do valor do atributo **Mandatory** .</span><span class="sxs-lookup"><span data-stu-id="3ecb7-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="3ecb7-142">Por exemplo, vamos configurar os parâmetros de entrada para um runbook do Fluxo de Trabalho do PowerShell que gera detalhes sobre máquinas virtuais, seja uma única VM ou todas as VMs em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="3ecb7-143">Esse runbook tem dois parâmetros, conforme mostrado na captura de tela a seguir: o nome da máquina virtual e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span></span>

![Fluxo de trabalho do PowerShell de automação](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="3ecb7-145">Nessa definição de parâmetro, os parâmetros **$VMName** e **$resourceGroupName** são parâmetros simples do tipo cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="3ecb7-146">No entanto, o PowerShell e os runbooks do Fluxo de Trabalho do PowerShell dão suporte a todos os tipos simples e complexos, como **objeto** ou **PSCredential** para parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="3ecb7-147">Se o runbook tiver um parâmetro de entrada de tipo objeto, use uma tabela de hash do PowerShell com pares (nome, valor) para passar um valor.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span></span> <span data-ttu-id="3ecb7-148">Por exemplo, se você tiver o seguinte parâmetro em um runbook:</span><span class="sxs-lookup"><span data-stu-id="3ecb7-148">For example, if you have the following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="3ecb7-149">Poderá passar o seguinte valor para o parâmetro:</span><span class="sxs-lookup"><span data-stu-id="3ecb7-149">Then you can pass the following value to the parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="3ecb7-150">Como configurar parâmetros de entrada em runbooks gráficos</span><span class="sxs-lookup"><span data-stu-id="3ecb7-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="3ecb7-151">Para [configurar um runbook gráfico](automation-first-runbook-graphical.md) com parâmetros de entrada, vamos criar um runbook gráfico que gera detalhes sobre máquinas virtuais, seja uma única VM ou todas as VMs em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="3ecb7-152">A configuração de um runbook consiste em duas atividades principais, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="3ecb7-153">[**Autenticar runbooks com uma conta Executar como do Azure**](automation-sec-configure-azure-runas-account.md) para autenticar com o Azure.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span></span>

<span data-ttu-id="3ecb7-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) para obter as propriedades de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span></span>

<span data-ttu-id="3ecb7-155">Você pode usar a atividade [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) para gerar os nomes das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span></span> <span data-ttu-id="3ecb7-156">A atividade **Get-AzureRmVm** aceitará dois parâmetros: o **nome da máquina virtual** e o **nome do grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span></span> <span data-ttu-id="3ecb7-157">Uma vez que esses parâmetros exigiriam valores diferentes sempre que você iniciasse o runbook, você pode adicionar parâmetros de entrada ao runbook.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span></span> <span data-ttu-id="3ecb7-158">Aqui estão as etapas para adicionar parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="3ecb7-158">Here are the steps to add input parameters:</span></span>

1. <span data-ttu-id="3ecb7-159">Selecione o runbook gráfico na folha **Runbooks** e então clique em [**Editar**](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="3ecb7-160">No editor de runbook, clique em **Entrada e saída** para abrir a folha **Entrada e saída**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span></span>
   
    ![Runbook gráfico de automação](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="3ecb7-162">A folha **Entrada e saída** exibe uma lista de parâmetros de entrada definidos para o runbook.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span></span> <span data-ttu-id="3ecb7-163">Nessa folha, você pode adicionar um novo parâmetro de entrada ou editar a configuração de um parâmetro de entrada existente.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span></span> <span data-ttu-id="3ecb7-164">Para adicionar um novo parâmetro ao runbook, clique **Adicionar entrada** para abrir a folha **Parâmetro de Entrada do Runbook**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span></span> <span data-ttu-id="3ecb7-165">Nela, você pode configurar os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="3ecb7-165">There, you can configure the following parameters:</span></span>
   
   | <span data-ttu-id="3ecb7-166">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="3ecb7-166">**Property**</span></span> | <span data-ttu-id="3ecb7-167">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="3ecb7-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="3ecb7-168">Nome</span><span class="sxs-lookup"><span data-stu-id="3ecb7-168">Name</span></span> |<span data-ttu-id="3ecb7-169">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-169">Required.</span></span>  <span data-ttu-id="3ecb7-170">O nome do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-170">The name of the parameter.</span></span> <span data-ttu-id="3ecb7-171">Deve ser exclusivo no runbook e pode conter apenas letras, números ou caracteres de sublinhado.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="3ecb7-172">Deve começar com uma letra.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="3ecb7-173">Descrição</span><span class="sxs-lookup"><span data-stu-id="3ecb7-173">Description</span></span> |<span data-ttu-id="3ecb7-174">Opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-174">Optional.</span></span> <span data-ttu-id="3ecb7-175">Descrição da finalidade do parâmetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-175">Description about the purpose of input parameter.</span></span> |
   | <span data-ttu-id="3ecb7-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="3ecb7-176">Type</span></span> |<span data-ttu-id="3ecb7-177">Opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-177">Optional.</span></span> <span data-ttu-id="3ecb7-178">O tipo de dados esperado para o valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-178">The data type that's expected for the parameter value.</span></span> <span data-ttu-id="3ecb7-179">Os tipos de parâmetro com suporte são **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** e **Object**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="3ecb7-180">Se um tipo de dados não estiver selecionado, será usado **String**por padrão.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-180">If a data type is not selected, it defaults to **String**.</span></span> |
   | <span data-ttu-id="3ecb7-181">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="3ecb7-181">Mandatory</span></span> |<span data-ttu-id="3ecb7-182">Opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-182">Optional.</span></span> <span data-ttu-id="3ecb7-183">Especifica se deve ser fornecido um valor para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-183">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="3ecb7-184">Se você escolher **sim**, um valor deverá ser fornecido quando o runbook for iniciado.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-184">If you choose **yes**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="3ecb7-185">Se você escolher **não**, um valor não será necessário quando o runbook for iniciado, e um valor padrão poderá ser definido.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="3ecb7-186">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="3ecb7-186">Default Value</span></span> |<span data-ttu-id="3ecb7-187">Opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-187">Optional.</span></span> <span data-ttu-id="3ecb7-188">Especifica um valor que será usado para o parâmetro se um valor não for transmitido ao iniciar o runbook.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="3ecb7-189">Um valor padrão pode ser definido para um parâmetro que não é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="3ecb7-190">Para definir um valor padrão, escolha **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-190">To set a default value, choose **Custom**.</span></span> <span data-ttu-id="3ecb7-191">Esse valor será usado a menos que outro valor seja fornecido quando o runbook for iniciado.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-191">This value is used unless another value is provided when the runbook is started.</span></span> <span data-ttu-id="3ecb7-192">Escolha **Nenhum** se não quiser fornecer nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-192">Choose **None** if you don’t want to provide any default value.</span></span> |
   
    ![Como adicionar nova entrada](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="3ecb7-194">Crie dois parâmetros com as seguintes propriedades que serão usadas pela atividade **Get-AzureRmVm** :</span><span class="sxs-lookup"><span data-stu-id="3ecb7-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="3ecb7-195">**Parameter1:**</span><span class="sxs-lookup"><span data-stu-id="3ecb7-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="3ecb7-196">Nome - VMName</span><span class="sxs-lookup"><span data-stu-id="3ecb7-196">Name - VMName</span></span>
     * <span data-ttu-id="3ecb7-197">Tipo - String</span><span class="sxs-lookup"><span data-stu-id="3ecb7-197">Type - String</span></span>
     * <span data-ttu-id="3ecb7-198">Obrigatório - Não</span><span class="sxs-lookup"><span data-stu-id="3ecb7-198">Mandatory - No</span></span>
   * <span data-ttu-id="3ecb7-199">**Parameter2:**</span><span class="sxs-lookup"><span data-stu-id="3ecb7-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="3ecb7-200">Nome - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3ecb7-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="3ecb7-201">Tipo - String</span><span class="sxs-lookup"><span data-stu-id="3ecb7-201">Type - String</span></span>
     * <span data-ttu-id="3ecb7-202">Obrigatório - Não</span><span class="sxs-lookup"><span data-stu-id="3ecb7-202">Mandatory - No</span></span>
     * <span data-ttu-id="3ecb7-203">Valor padrão - Personalizado</span><span class="sxs-lookup"><span data-stu-id="3ecb7-203">Default value - Custom</span></span>
     * <span data-ttu-id="3ecb7-204">Valor padrão personalizado - \<Nome do grupo de recursos que contém as máquinas virtuais></span><span class="sxs-lookup"><span data-stu-id="3ecb7-204">Custom default value - \<Name of the resource group that contains the virtual machines></span></span>
5. <span data-ttu-id="3ecb7-205">Depois de adicionar os parâmetros, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-205">Once you add the parameters, click **OK**.</span></span>  <span data-ttu-id="3ecb7-206">Agora você pode exibi-los na **folha Entrada e saída**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-206">You can now view them in the **Input and output blade**.</span></span> <span data-ttu-id="3ecb7-207">Clique em **OK** novamente e clique em **Salvar** e **Publicar** o runbook.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-to-input-parameters-in-runbooks"></a><span data-ttu-id="3ecb7-208">Como atribuir valores a parâmetros de entrada em runbooks</span><span class="sxs-lookup"><span data-stu-id="3ecb7-208">Assign values to input parameters in runbooks</span></span>
<span data-ttu-id="3ecb7-209">Você pode passar valores para parâmetros de entrada em runbooks nos cenários a seguir</span><span class="sxs-lookup"><span data-stu-id="3ecb7-209">You can pass values to input parameters in runbooks in the following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="3ecb7-210">Iniciar um runbook e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="3ecb7-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="3ecb7-211">Um runbook pode ser iniciado de diversas maneiras: por meio do portal do Azure, com um webhook, com cmdlets do PowerShell, com a API REST ou com o SDK.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span></span> <span data-ttu-id="3ecb7-212">A seguir, discutiremos diferentes métodos para iniciar um runbook e atribuir parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-the-azure-portal-and-assign-parameters"></a><span data-ttu-id="3ecb7-213">Como iniciar um runbook publicado usando o portal do Azure e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="3ecb7-213">Start a published runbook by using the Azure portal and assign parameters</span></span>
<span data-ttu-id="3ecb7-214">Quando você [inicia o runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), a folha **Iniciar Runbook** é aberta e você pode configurar valores para os parâmetros que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span></span>

![Como começar a usar o portal](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="3ecb7-216">No rótulo abaixo da caixa de entrada, você pode ver os atributos que foram definidos para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span></span> <span data-ttu-id="3ecb7-217">Os atributos incluem obrigatório ou opcional, tipo e valor padrão.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="3ecb7-218">No balão de ajuda ao lado do nome de parâmetro, você pode ver todas as informações principais necessárias para tomar decisões sobre os valores de entrada de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span></span> <span data-ttu-id="3ecb7-219">Essas informações incluem se um parâmetro é obrigatório ou opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="3ecb7-220">Também incluem o tipo e o valor padrão (se houver) e outras observações úteis.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-220">It also includes the type and default value (if any), and other helpful notes.</span></span>

![Balão de ajuda](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="3ecb7-222">Parâmetros do tipo String dão suporte a valores de Cadeia de Caracteres **Vazia** .</span><span class="sxs-lookup"><span data-stu-id="3ecb7-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="3ecb7-223">Se você inserir **[EmptyString]** na caixa do parâmetro de entrada, uma cadeia de caracteres vazia será passada para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span></span> <span data-ttu-id="3ecb7-224">Além disso, parâmetros do tipo de cadeia de caracteres não dão suporte à passagem de valores **Nulos** .</span><span class="sxs-lookup"><span data-stu-id="3ecb7-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="3ecb7-225">Se você não passar um valor para o parâmetro de Cadeia de Caracteres, o PowerShell o interpretará como nulo.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="3ecb7-226">Como iniciar um runbook publicado usando cmdlets do PowerShell e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="3ecb7-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="3ecb7-227">**Cmdlets do Azure Resource Manager:** você pode iniciar um runbook de Automação criado em um grupo de recursos usando [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="3ecb7-228">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="3ecb7-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="3ecb7-229">**Cmdlets de gerenciamento de serviços do azure:** você pode iniciar um runbook de automação criado em um grupo de recursos padrão usando [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx)</span><span class="sxs-lookup"><span data-stu-id="3ecb7-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="3ecb7-230">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="3ecb7-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="3ecb7-231">Quando você inicia um runbook usando cmdlets do PowerShell, um parâmetro padrão, **MicrosoftApplicationManagementStartedBy**, é criado com o valor **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span></span> <span data-ttu-id="3ecb7-232">Você pode exibir esse parâmetro na folha **Detalhes do trabalho** .</span><span class="sxs-lookup"><span data-stu-id="3ecb7-232">You can view this parameter in the **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="3ecb7-233">Como uniciar um runbook usando o SDK e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="3ecb7-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="3ecb7-234">**Método do Gerenciador de recursos do Azure:** você pode iniciar um runbook usando o SDK de uma linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="3ecb7-235">Abaixo está um trecho de código em C# para iniciar um runbook em sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="3ecb7-236">Você pode exibir todo o código em nosso [repositório do GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
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
* <span data-ttu-id="3ecb7-237">**Método de Gerenciamento de Serviço do Azure:** você pode iniciar um runbook usando o SDK de uma linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="3ecb7-238">Abaixo está um trecho de código em C# para iniciar um runbook em sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="3ecb7-239">Você pode exibir todo o código em nosso [repositório do GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
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
  
  <span data-ttu-id="3ecb7-240">Para iniciar esse método, crie um dicionário para armazenar os parâmetros de runbook, **VMName** e **resourceGroupName**, e seus valores.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="3ecb7-241">Em seguida, inicie o runbook.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-241">Then start the runbook.</span></span> <span data-ttu-id="3ecb7-242">Abaixo está o trecho de código em C# para chamar o método definido acima.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-242">Below is the C# code snippet for calling the method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters to the dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call the StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-the-rest-api-and-assign-parameters"></a><span data-ttu-id="3ecb7-243">Como iniciar um runbook usando a API REST e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="3ecb7-243">Start a runbook by using the REST API and assign parameters</span></span>
<span data-ttu-id="3ecb7-244">Um trabalho de runbook pode ser criado e iniciado com a API REST de Automação do Azure usando o método **PUT** com o URI de solicitação a seguir.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="3ecb7-245">No URI de solicitação, substitua os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="3ecb7-245">In the request URI, replace the following parameters:</span></span>

* <span data-ttu-id="3ecb7-246">**subscription-id:** a ID de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="3ecb7-247">**cloud-service-name:** o nome do serviço de nuvem ao qual a solicitação deve ser enviada.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span></span>  
* <span data-ttu-id="3ecb7-248">**automation-account-name:** o nome de sua conta de automação hospedada no serviço de nuvem especificado.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span></span>  
* <span data-ttu-id="3ecb7-249">**id do trabalho:** o GUID para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-249">**job-id:** The GUID for the job.</span></span> <span data-ttu-id="3ecb7-250">Os GUIDs do PowerShell pode ser criados usando o cmdlet **[GUID]::NewGuid().ToString ()** .</span><span class="sxs-lookup"><span data-stu-id="3ecb7-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="3ecb7-251">Para passar parâmetros para o trabalho de runbook, use o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-251">In order to pass parameters to the runbook job, use the request body.</span></span> <span data-ttu-id="3ecb7-252">Ele usa as duas seguintes propriedades fornecidas no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="3ecb7-252">It takes the following two properties provided in JSON format:</span></span>

* <span data-ttu-id="3ecb7-253">**Nome do Runbook:** Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-253">**Runbook name:** Required.</span></span> <span data-ttu-id="3ecb7-254">O nome do runbook para que o trabalho seja iniciado.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-254">The name of the runbook for the job to start.</span></span>  
* <span data-ttu-id="3ecb7-255">**Parâmetros do Runbook:** Opcional.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="3ecb7-256">Um dicionário da lista de parâmetros no formato (nome, valor) em que o nome deve ser do tipo cadeia de caracteres e o valor pode ser qualquer valor JSON válido.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="3ecb7-257">Se você quiser iniciar o runbook **Get-AzureVMTextual** criado anteriormente com **VMName** e **resourceGroupName** como parâmetros, use o formato JSON a seguir para o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span></span>

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

<span data-ttu-id="3ecb7-258">Um código de status HTTP 201 será retornado se o trabalho for criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-258">A HTTP status code 201 is returned if the job is successfully created.</span></span> <span data-ttu-id="3ecb7-259">Para obter mais informações sobre cabeçalhos de resposta e o corpo da resposta, consulte o artigo sobre como [criar um trabalho de runbook usando a API REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="3ecb7-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="3ecb7-260">Testar um runbook e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="3ecb7-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="3ecb7-261">Quando você [testa a versão de rascunho do runbook](automation-testing-runbook.md) usando a opção de teste, é aberta a folha **Teste** , e você pode configurar valores para os parâmetros que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span></span>

![Como testar e atribuir parâmetros](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-to-a-runbook-and-assign-parameters"></a><span data-ttu-id="3ecb7-263">Vincular um agendamento para um runbook e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="3ecb7-263">Link a schedule to a runbook and assign parameters</span></span>
<span data-ttu-id="3ecb7-264">Você pode [vincular uma agenda](automation-schedules.md) ao runbook para que ele seja iniciado em um momento específico.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span></span> <span data-ttu-id="3ecb7-265">Você atribui parâmetros de entrada ao criar a agenda. O runbook usará esses valores quando for iniciado pela agenda.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span></span> <span data-ttu-id="3ecb7-266">Não é possível salvar a agenda até que todos os valores de parâmetro obrigatório sejam fornecidos.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-266">You can’t save the schedule until all mandatory parameter values are provided.</span></span>

![Como agendar e atribuir parâmetros](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="3ecb7-268">Criar um webhook de um runbook e atribuir parâmetros</span><span class="sxs-lookup"><span data-stu-id="3ecb7-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="3ecb7-269">Você pode criar um [webhook](automation-webhooks.md) para seu runbook e configurar parâmetros de entrada do runbook.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="3ecb7-270">Não é possível salvar o webhook até que todos os valores de parâmetro obrigatório sejam fornecidos.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-270">You can’t save the webhook until all mandatory parameter values are provided.</span></span>

![Como criar o webhook e atribuir parâmetros](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="3ecb7-272">Quando você executa um runbook usando um webhook, o parâmetro de entrada predefinido **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** é enviado junto com os parâmetros de entrada que você definiu.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span></span> <span data-ttu-id="3ecb7-273">Você pode clicar para expandir o parâmetro **WebhookData** para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="3ecb7-273">You can click to expand the **WebhookData** parameter for more details.</span></span>

![Parâmetro WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="3ecb7-275">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ecb7-275">Next steps</span></span>
* <span data-ttu-id="3ecb7-276">Para obter mais informações sobre a entrada e a saída do runbook, consulte [Automação do Azure: entrada do runbook, saída e runbooks aninhados](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="3ecb7-277">Para obter detalhes sobre diferentes maneiras de iniciar um runbook, consulte [Como iniciar um runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="3ecb7-278">Para editar um runbook textual, consulte [Como editar runbooks textuais](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="3ecb7-279">Para editar um runbook gráfico, consulte [Criação gráfica na Automação do Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="3ecb7-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

