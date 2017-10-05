---
title: "Como criar soluções de gerenciamento no OMS (Operations Management Suite) | Microsoft Docs"
description: "As soluções de gerenciamento estendem a funcionalidade do OMS (Operations Management Suite), fornecendo cenários de gerenciamento empacotados que os clientes podem adicionar ao seu espaço de trabalho do OMS.  Este artigo fornece detalhes sobre como criar soluções de gerenciamento para usar em seu próprio ambiente ou disponibilizar para os clientes."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee3462c13101d18921dc488b08c79e1e4e02ff3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="af663-104">Criando um arquivo de solução de gerenciamento no OMS (Operations Management Suite) (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="af663-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="af663-105">Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="af663-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="af663-106">Os esquemas descritos a seguir estão sujeitos a alterações.</span><span class="sxs-lookup"><span data-stu-id="af663-106">Any schema described below is subject to change.</span></span>  

<span data-ttu-id="af663-107">As soluções de gerenciamento do OMS (Operations Management Suite) são implementadas como [modelos do Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="af663-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="af663-108">A principal tarefa ao aprender a criar soluções personalizadas é aprender como [criar um modelo](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="af663-108">The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="af663-109">Este artigo fornece detalhes exclusivos sobre os modelos usados para as soluções e como configurar recursos típicos de soluções.</span><span class="sxs-lookup"><span data-stu-id="af663-109">This article provides unique details of templates used for solutions and how to configure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="af663-110">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="af663-110">Tools</span></span>

<span data-ttu-id="af663-111">É possível usar qualquer editor de texto para trabalhar com arquivos de solução, mas recomendamos aproveitar os recursos fornecidos no Visual Studio ou no Visual Studio Code, conforme descrito nos próximos artigos.</span><span class="sxs-lookup"><span data-stu-id="af663-111">You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.</span></span>

- [<span data-ttu-id="af663-112">Criando e implantando grupos de recursos do Azure por meio do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af663-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="af663-113">Trabalhando com Modelos do Azure Resource Manager no Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="af663-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="af663-114">Estrutura</span><span class="sxs-lookup"><span data-stu-id="af663-114">Structure</span></span>
<span data-ttu-id="af663-115">A estrutura básica de um arquivo de solução de gerenciamento é a mesma que um [modelo do Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#template-format), que é da maneira demonstrada a seguir.</span><span class="sxs-lookup"><span data-stu-id="af663-115">The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="af663-116">Cada uma das seções abaixo descreve os elementos de nível superior e seu conteúdo em uma solução.</span><span class="sxs-lookup"><span data-stu-id="af663-116">Each of the sections below describes the top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="af663-117">parâmetros</span><span class="sxs-lookup"><span data-stu-id="af663-117">Parameters</span></span>
<span data-ttu-id="af663-118">[Parâmetros](../azure-resource-manager/resource-group-authoring-templates.md#parameters) são valores que exige dos usuários quando eles instalam a solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="af663-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.</span></span>  <span data-ttu-id="af663-119">Eles são parâmetros padrão que todas as soluções terão; além disso, você pode adicionar parâmetros adicionais conforme necessário para sua solução específica.</span><span class="sxs-lookup"><span data-stu-id="af663-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="af663-120">O modo como os usuários fornecerão valores de parâmetro quando instalarem sua solução dependerá do parâmetro específico e do modo como a solução estiver sendo instalada.</span><span class="sxs-lookup"><span data-stu-id="af663-120">How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.</span></span>

<span data-ttu-id="af663-121">Quando um usuário instala a solução de gerenciamento por meio do [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) ou dos [Modelos de Início Rápido do Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions), será solicitado que ele selecione uma [Conta de automação e um Espaço de trabalho do OMS](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="af663-121">When a user installs your management solution through the [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted to select an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="af663-122">Eles são usados para preencher os valores de cada um dos parâmetros padrão.</span><span class="sxs-lookup"><span data-stu-id="af663-122">These are used to populate the values of each of the standard parameters.</span></span>  <span data-ttu-id="af663-123">Não é solicitado que o usuário forneça diretamente os valores dos parâmetros padrão, mas será solicitado que ele forneça valores para eventuais parâmetros adicionais.</span><span class="sxs-lookup"><span data-stu-id="af663-123">The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.</span></span>

<span data-ttu-id="af663-124">Quando o usuário instalar a solução por [outro método](operations-management-suite-solutions.md#finding-and-installing-management-solutions), ele deverá fornecer um valor para todos os parâmetros padrão e todos os parâmetros adicionais.</span><span class="sxs-lookup"><span data-stu-id="af663-124">When the user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="af663-125">Um parâmetro de exemplo é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="af663-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="af663-126">A tabela a seguir descreve os atributos de um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="af663-126">The following table describes the attributes of a parameter.</span></span>

| <span data-ttu-id="af663-127">Atributo</span><span class="sxs-lookup"><span data-stu-id="af663-127">Attribute</span></span> | <span data-ttu-id="af663-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="af663-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="af663-129">type</span><span class="sxs-lookup"><span data-stu-id="af663-129">type</span></span> |<span data-ttu-id="af663-130">Tipo de dados para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="af663-130">Data type for the parameter.</span></span> <span data-ttu-id="af663-131">O controle de entrada exibido para o usuário depende do tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="af663-131">The input control displayed for the user depends on the data type.</span></span><br><br><span data-ttu-id="af663-132">bool – Caixa suspensa</span><span class="sxs-lookup"><span data-stu-id="af663-132">bool - Drop down box</span></span><br><span data-ttu-id="af663-133">cadeia de caracteres – caixa de texto</span><span class="sxs-lookup"><span data-stu-id="af663-133">string - Text box</span></span><br><span data-ttu-id="af663-134">int – Caixa de texto</span><span class="sxs-lookup"><span data-stu-id="af663-134">int - Text box</span></span><br><span data-ttu-id="af663-135">securestring – Campo de senha</span><span class="sxs-lookup"><span data-stu-id="af663-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="af663-136">categoria</span><span class="sxs-lookup"><span data-stu-id="af663-136">category</span></span> |<span data-ttu-id="af663-137">Categoria opcional para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="af663-137">Optional category for the parameter.</span></span>  <span data-ttu-id="af663-138">Parâmetros na mesma categoria são agrupados.</span><span class="sxs-lookup"><span data-stu-id="af663-138">Parameters in the same category are grouped together.</span></span> |
| <span data-ttu-id="af663-139">controle</span><span class="sxs-lookup"><span data-stu-id="af663-139">control</span></span> |<span data-ttu-id="af663-140">Funcionalidade adicional para parâmetros de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="af663-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="af663-141">datetime – O controle datetime é exibido.</span><span class="sxs-lookup"><span data-stu-id="af663-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="af663-142">GUID – O valor de GUID é gerado automaticamente e o parâmetro não é exibido.</span><span class="sxs-lookup"><span data-stu-id="af663-142">guid - Guid value is automatically generated, and the parameter is not displayed.</span></span> |
| <span data-ttu-id="af663-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="af663-143">description</span></span> |<span data-ttu-id="af663-144">Descrição opcional para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="af663-144">Optional description for the parameter.</span></span>  <span data-ttu-id="af663-145">Exibido em um balão de informações ao lado do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="af663-145">Displayed in an information balloon next to the parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="af663-146">Parâmetros padrão</span><span class="sxs-lookup"><span data-stu-id="af663-146">Standard parameters</span></span>
<span data-ttu-id="af663-147">A tabela a seguir lista os parâmetros padrão para todas as soluções de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="af663-147">The following table lists the standard parameters for all management solutions.</span></span>  <span data-ttu-id="af663-148">Esses valores são populados para o usuário em vez de solicitados a eles quando a solução é instalada dos modelos do Azure Marketplace ou de Início Rápido.</span><span class="sxs-lookup"><span data-stu-id="af663-148">These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="af663-149">Se a solução for instalada com outro método, o usuário deverá fornecer valores para eles.</span><span class="sxs-lookup"><span data-stu-id="af663-149">The user must provide values for them if the solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="af663-150">A interface do usuário nos modelos do Azure Marketplace e de Início Rápido espera os nomes de parâmetro na tabela.</span><span class="sxs-lookup"><span data-stu-id="af663-150">The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.</span></span>  <span data-ttu-id="af663-151">Se você usar nomes de parâmetro diferentes, será solicitado que o usuário os forneça e eles não serão automaticamente populados.</span><span class="sxs-lookup"><span data-stu-id="af663-151">If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="af663-152">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="af663-152">Parameter</span></span> | <span data-ttu-id="af663-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="af663-153">Type</span></span> | <span data-ttu-id="af663-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="af663-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="af663-155">accountName</span><span class="sxs-lookup"><span data-stu-id="af663-155">accountName</span></span> |<span data-ttu-id="af663-156">string</span><span class="sxs-lookup"><span data-stu-id="af663-156">string</span></span> |<span data-ttu-id="af663-157">Nome da conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="af663-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="af663-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="af663-158">pricingTier</span></span> |<span data-ttu-id="af663-159">string</span><span class="sxs-lookup"><span data-stu-id="af663-159">string</span></span> |<span data-ttu-id="af663-160">Tipo de preço do espaço de trabalho do Log Analytics e da conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="af663-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="af663-161">regionId</span><span class="sxs-lookup"><span data-stu-id="af663-161">regionId</span></span> |<span data-ttu-id="af663-162">string</span><span class="sxs-lookup"><span data-stu-id="af663-162">string</span></span> |<span data-ttu-id="af663-163">Região da conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="af663-163">Region of the Azure Automation account.</span></span> |
| <span data-ttu-id="af663-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="af663-164">solutionName</span></span> |<span data-ttu-id="af663-165">string</span><span class="sxs-lookup"><span data-stu-id="af663-165">string</span></span> |<span data-ttu-id="af663-166">O nome da solução.</span><span class="sxs-lookup"><span data-stu-id="af663-166">Name of the solution.</span></span>  <span data-ttu-id="af663-167">Se você estiver implantando a solução por meio de modelos de Início Rápido, defina solutionName como um parâmetro para que seja possível definir uma cadeia de caracteres, em vez de exigir que o usuário especifique um.</span><span class="sxs-lookup"><span data-stu-id="af663-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one.</span></span> |
| <span data-ttu-id="af663-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="af663-168">workspaceName</span></span> |<span data-ttu-id="af663-169">string</span><span class="sxs-lookup"><span data-stu-id="af663-169">string</span></span> |<span data-ttu-id="af663-170">O nome do espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="af663-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="af663-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="af663-171">workspaceRegionId</span></span> |<span data-ttu-id="af663-172">string</span><span class="sxs-lookup"><span data-stu-id="af663-172">string</span></span> |<span data-ttu-id="af663-173">A região do espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="af663-173">Region of the Log Analytics workspace.</span></span> |


<span data-ttu-id="af663-174">A seguir está a estrutura dos parâmetros padrão que você pode copiar e colar em seu arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="af663-174">Following is the structure of the standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of the Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of the Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="af663-175">Consulte os valores de parâmetro em outros elementos da solução com a sintaxe **parameters('nome do parâmetro')**.</span><span class="sxs-lookup"><span data-stu-id="af663-175">You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="af663-176">Por exemplo, para acessar o nome do espaço de trabalho, você usaria **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="af663-176">For example, to access the workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="af663-177">Variáveis</span><span class="sxs-lookup"><span data-stu-id="af663-177">Variables</span></span>
<span data-ttu-id="af663-178">[Variáveis](../azure-resource-manager/resource-group-authoring-templates.md#variables) são valores que serão usados no restante da solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="af663-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.</span></span>  <span data-ttu-id="af663-179">Esses valores não são expostos ao usuário que instala a solução.</span><span class="sxs-lookup"><span data-stu-id="af663-179">These values are not exposed to the user installing the solution.</span></span>  <span data-ttu-id="af663-180">Eles se destinam a fornecer ao autor um único local onde ele pode gerenciar os valores que podem ser usados várias vezes em toda a solução.</span><span class="sxs-lookup"><span data-stu-id="af663-180">They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution.</span></span> <span data-ttu-id="af663-181">É necessário colocar os valores específicos à solução em variáveis, em vez de embuti-los em código no elemento **resources**.</span><span class="sxs-lookup"><span data-stu-id="af663-181">You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.</span></span>  <span data-ttu-id="af663-182">Isso torna o código mais legível e permite que você altere esses valores facilmente em versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="af663-182">This makes the code more readable and allows you to easily change these values in later versions.</span></span>

<span data-ttu-id="af663-183">A seguir está um exemplo de um elemento **variables** com parâmetros típicos usado em soluções.</span><span class="sxs-lookup"><span data-stu-id="af663-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="af663-184">Você consulta os valores de variáveis por toda a solução com a sintaxe **variables('nome da variável')**.</span><span class="sxs-lookup"><span data-stu-id="af663-184">You refer to variable values through the solution with the syntax **variables('variable name')**.</span></span>  <span data-ttu-id="af663-185">Por exemplo, para acessar a variável SolutionName, você usará **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="af663-185">For example, to access the SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="af663-186">Você também pode definir variáveis complexas que têm vários conjuntos de valores.</span><span class="sxs-lookup"><span data-stu-id="af663-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="af663-187">Elas são particularmente úteis em soluções de gerenciamento, quando você estiver definindo várias propriedades para diferentes tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="af663-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="af663-188">Por exemplo, é possível reestruturar as variáveis da solução mostradas acima, conforme indicado a seguir.</span><span class="sxs-lookup"><span data-stu-id="af663-188">For example, you could restructure the solution variables shown above to the following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="af663-189">Nesse caso, você consulta os valores de variáveis por meio da solução com a sintaxe **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="af663-189">In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="af663-190">Por exemplo, para acessar a variável Solution Name, você usará **variables('Solution').Name**.</span><span class="sxs-lookup"><span data-stu-id="af663-190">For example, to access the Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="af663-191">Recursos</span><span class="sxs-lookup"><span data-stu-id="af663-191">Resources</span></span>
<span data-ttu-id="af663-192">Os [recursos](../azure-resource-manager/resource-group-authoring-templates.md#resources) definem os diferentes recursos que a solução de gerenciamento instalará e configurará.</span><span class="sxs-lookup"><span data-stu-id="af663-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="af663-193">Essa será a maior e mais complexa parte do modelo.</span><span class="sxs-lookup"><span data-stu-id="af663-193">This will be the largest and most complex portion of the template.</span></span>  <span data-ttu-id="af663-194">É possível obter a estrutura e a descrição completa dos elementos de recursos em [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="af663-194">You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="af663-195">Recursos diferentes que normalmente são definidos são detalhados em outros artigos desta documentação.</span><span class="sxs-lookup"><span data-stu-id="af663-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="af663-196">Dependências</span><span class="sxs-lookup"><span data-stu-id="af663-196">Dependencies</span></span>
<span data-ttu-id="af663-197">O elemento **dependsOn** especifica uma [dependência](../azure-resource-manager/resource-group-define-dependencies.md) de outro recurso.</span><span class="sxs-lookup"><span data-stu-id="af663-197">The **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="af663-198">Quando a solução é instalada, um recurso não é criado até que todas as suas dependências tenham sido criadas.</span><span class="sxs-lookup"><span data-stu-id="af663-198">When the solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="af663-199">Por exemplo, sua solução pode [iniciar um runbook](operations-management-suite-solutions-resources-automation.md#runbooks) quando ele é instalado usando um [recurso de trabalho](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="af663-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="af663-200">O recurso de trabalho seria dependente do recurso de runbook para assegurar que o runbook fosse criado antes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="af663-200">The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="af663-201">Espaço de trabalho do OMS e Conta de automação</span><span class="sxs-lookup"><span data-stu-id="af663-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="af663-202">Soluções de gerenciamento exigem que um [espaço de trabalho do OMS](../log-analytics/log-analytics-manage-access.md) contenha modos de exibição e que uma [conta de automação](../automation/automation-security-overview.md#automation-account-overview) contenha runbooks e recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="af663-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span>  <span data-ttu-id="af663-203">Eles devem estar disponíveis antes que os recursos na solução sejam criados e não devem ser definidos na solução em si.</span><span class="sxs-lookup"><span data-stu-id="af663-203">These must be available before the resources in the solution are created and should not be defined in the solution itself.</span></span>  <span data-ttu-id="af663-204">O usuário [especificará uma conta e espaço de trabalho](operations-management-suite-solutions.md#oms-workspace-and-automation-account) quando implantar a sua solução mas, na condição de autor, você deve considerar os pontos a seguir.</span><span class="sxs-lookup"><span data-stu-id="af663-204">The user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="af663-205">Recurso da solução</span><span class="sxs-lookup"><span data-stu-id="af663-205">Solution resource</span></span>
<span data-ttu-id="af663-206">Cada solução exige uma entrada de recurso no elemento **resources** que define a solução em si.</span><span class="sxs-lookup"><span data-stu-id="af663-206">Each solution requires a resource entry in the **resources** element that defines the solution itself.</span></span>  <span data-ttu-id="af663-207">Isso terá um tipo **Microsoft.OperationsManagement/solutions** e terá a estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="af663-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure.</span></span> <span data-ttu-id="af663-208">Isso inclui [parâmetros padrão](#parameters) e [variáveis](#variables) que normalmente são usados para definir propriedades da solução.</span><span class="sxs-lookup"><span data-stu-id="af663-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="af663-209">Dependências</span><span class="sxs-lookup"><span data-stu-id="af663-209">Dependencies</span></span>
<span data-ttu-id="af663-210">O recurso da solução deve ter uma [dependência](../azure-resource-manager/resource-group-define-dependencies.md) em todos os outros recursos da solução, pois precisam existir antes que a solução possa ser criada.</span><span class="sxs-lookup"><span data-stu-id="af663-210">The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.</span></span>  <span data-ttu-id="af663-211">Você pode fazer isso adicionando uma entrada para cada recurso no elemento **dependsOn**.</span><span class="sxs-lookup"><span data-stu-id="af663-211">You do this by adding an entry for each resource in the **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="af663-212">Propriedades</span><span class="sxs-lookup"><span data-stu-id="af663-212">Properties</span></span>
<span data-ttu-id="af663-213">O recurso da solução tem as propriedades na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="af663-213">The solution resource has the properties in the following table.</span></span>  <span data-ttu-id="af663-214">Isso inclui os recursos referenciados e contidos pela solução que define como os recursos são gerenciados após a instalação da solução.</span><span class="sxs-lookup"><span data-stu-id="af663-214">This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.</span></span>  <span data-ttu-id="af663-215">Cada recurso na solução deve ser listado na propriedade **referencedResources** ou **containedResources**.</span><span class="sxs-lookup"><span data-stu-id="af663-215">Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.</span></span>

| <span data-ttu-id="af663-216">Propriedade</span><span class="sxs-lookup"><span data-stu-id="af663-216">Property</span></span> | <span data-ttu-id="af663-217">Descrição</span><span class="sxs-lookup"><span data-stu-id="af663-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="af663-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="af663-218">workspaceResourceId</span></span> |<span data-ttu-id="af663-219">ID do espaço de trabalho do Log Analytics no formato *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Nome do Espaço de Trabalho\>*.</span><span class="sxs-lookup"><span data-stu-id="af663-219">ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="af663-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="af663-220">referencedResources</span></span> |<span data-ttu-id="af663-221">Lista de recursos na solução que não deverão ser removidos quando a solução for removida.</span><span class="sxs-lookup"><span data-stu-id="af663-221">List of resources in the solution that should not be removed when the solution is removed.</span></span> |
| <span data-ttu-id="af663-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="af663-222">containedResources</span></span> |<span data-ttu-id="af663-223">Lista de recursos na solução que deverão ser removidos quando a solução for removida.</span><span class="sxs-lookup"><span data-stu-id="af663-223">List of resources in the solution that should be removed when the solution is removed.</span></span> |

<span data-ttu-id="af663-224">O exemplo acima é uma solução com um runbook, um cronograma e uma exibição.</span><span class="sxs-lookup"><span data-stu-id="af663-224">The example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="af663-225">O agendamento e o runbook são *referenciados* no elemento **properties** para que eles não sejam removidos quando a solução for removida.</span><span class="sxs-lookup"><span data-stu-id="af663-225">The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.</span></span>  <span data-ttu-id="af663-226">A exibição é *contida* para que ela seja removido quando a solução for removida.</span><span class="sxs-lookup"><span data-stu-id="af663-226">The view is *contained* so it is removed when the solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="af663-227">Plano</span><span class="sxs-lookup"><span data-stu-id="af663-227">Plan</span></span>
<span data-ttu-id="af663-228">A entidade **plano** do recurso da solução tem as propriedades na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="af663-228">The **plan** entity of the solution resource has the properties in the following table.</span></span>

| <span data-ttu-id="af663-229">Propriedade</span><span class="sxs-lookup"><span data-stu-id="af663-229">Property</span></span> | <span data-ttu-id="af663-230">Descrição</span><span class="sxs-lookup"><span data-stu-id="af663-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="af663-231">name</span><span class="sxs-lookup"><span data-stu-id="af663-231">name</span></span> |<span data-ttu-id="af663-232">O nome da solução.</span><span class="sxs-lookup"><span data-stu-id="af663-232">Name of the solution.</span></span> |
| <span data-ttu-id="af663-233">version</span><span class="sxs-lookup"><span data-stu-id="af663-233">version</span></span> |<span data-ttu-id="af663-234">Versão da solução conforme determinado pelo autor.</span><span class="sxs-lookup"><span data-stu-id="af663-234">Version of the solution as determined by the author.</span></span> |
| <span data-ttu-id="af663-235">product</span><span class="sxs-lookup"><span data-stu-id="af663-235">product</span></span> |<span data-ttu-id="af663-236">Cadeia de caracteres exclusiva para identificar a solução.</span><span class="sxs-lookup"><span data-stu-id="af663-236">Unique string to identify the solution.</span></span> |
| <span data-ttu-id="af663-237">publicador</span><span class="sxs-lookup"><span data-stu-id="af663-237">publisher</span></span> |<span data-ttu-id="af663-238">O publicador da solução.</span><span class="sxs-lookup"><span data-stu-id="af663-238">Publisher of the solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="af663-239">Amostra</span><span class="sxs-lookup"><span data-stu-id="af663-239">Sample</span></span>
<span data-ttu-id="af663-240">É possível exibir amostras de arquivos de solução com um recurso de solução nas localizações a seguir.</span><span class="sxs-lookup"><span data-stu-id="af663-240">You can view samples of solution files with a solution resource at the following locations.</span></span>

- [<span data-ttu-id="af663-241">Recursos de automação</span><span class="sxs-lookup"><span data-stu-id="af663-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="af663-242">Recursos de pesquisa e alerta</span><span class="sxs-lookup"><span data-stu-id="af663-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="af663-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af663-243">Next steps</span></span>
* <span data-ttu-id="af663-244">[Adicionar alertas e pesquisas salvas](operations-management-suite-solutions-resources-searches-alerts.md) à sua solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="af663-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) to your management solution.</span></span>
* <span data-ttu-id="af663-245">[Adicionar exibições](operations-management-suite-solutions-resources-views.md) à sua solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="af663-245">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="af663-246">[Adicionar runbooks e outros recursos da Automação](operations-management-suite-solutions-resources-automation.md) à solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="af663-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>
* <span data-ttu-id="af663-247">Aprenda os detalhes da [Criação de modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="af663-247">Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="af663-248">Pesquise entre os [Modelos de Início Rápido do Azure](https://azure.microsoft.com/documentation/templates) para obter exemplos de diferentes modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="af663-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
