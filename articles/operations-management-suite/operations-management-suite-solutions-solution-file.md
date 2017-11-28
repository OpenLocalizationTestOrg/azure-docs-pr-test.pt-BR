---
title: "soluções de gerenciamento de aaaCreating no OMS Operations Management Suite () | Microsoft Docs"
description: "Soluções de gerenciamento de estendem a funcionalidade de saudação do Operations Management Suite (OMS), fornecendo os cenários de pacotes de gerenciamento que os clientes podem adicionar tootheir espaço de trabalho do OMS.  Este artigo fornece detalhes sobre como você pode criar toobe de soluções de gerenciamento usados em seu próprio ambiente ou feitas clientes tooyour disponíveis."
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
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="0201a-104">Criando um arquivo de solução de gerenciamento no OMS (Operations Management Suite) (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="0201a-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="0201a-105">Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="0201a-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="0201a-106">Qualquer esquema descrita abaixo é toochange de assunto.</span><span class="sxs-lookup"><span data-stu-id="0201a-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="0201a-107">As soluções de gerenciamento do OMS (Operations Management Suite) são implementadas como [modelos do Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="0201a-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="0201a-108">tarefa principal de saudação em aprender como soluções de gerenciamento tooauthor é necessário saber como muito[criar um modelo de](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0201a-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="0201a-109">Este artigo fornece detalhes exclusivos dos modelos usados para soluções e como recursos de solução típica tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="0201a-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="0201a-110">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="0201a-110">Tools</span></span>

<span data-ttu-id="0201a-111">Você pode usar qualquer toowork do editor de texto com arquivos de solução, mas é recomendável aproveitar os recursos de saudação fornecidos no Visual Studio ou o código do Visual Studio, conforme descrito em Olá artigos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0201a-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="0201a-112">Criando e implantando grupos de recursos do Azure por meio do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0201a-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="0201a-113">Trabalhando com Modelos do Azure Resource Manager no Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0201a-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="0201a-114">Estrutura</span><span class="sxs-lookup"><span data-stu-id="0201a-114">Structure</span></span>
<span data-ttu-id="0201a-115">estrutura básica de saudação de um arquivo de solução de gerenciamento é Olá mesmo que um [Gerenciador de recursos de modelo](../azure-resource-manager/resource-group-authoring-templates.md#template-format) que é da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="0201a-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="0201a-116">Cada uma das seções de saudação abaixo descreve os elementos de nível superior de saudação e e seu conteúdo em uma solução.</span><span class="sxs-lookup"><span data-stu-id="0201a-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="0201a-117">parâmetros</span><span class="sxs-lookup"><span data-stu-id="0201a-117">Parameters</span></span>
<span data-ttu-id="0201a-118">[Parâmetros](../azure-resource-manager/resource-group-authoring-templates.md#parameters) são valores que você precisa de usuário Olá ao instalar a solução de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="0201a-119">Eles são parâmetros padrão que todas as soluções terão; além disso, você pode adicionar parâmetros adicionais conforme necessário para sua solução específica.</span><span class="sxs-lookup"><span data-stu-id="0201a-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="0201a-120">Como os usuários fornecerá valores de parâmetro ao instalar a solução dependem parâmetro específico hello e como solução hello está sendo instalada.</span><span class="sxs-lookup"><span data-stu-id="0201a-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="0201a-121">Quando um usuário instala a solução de gerenciamento por meio de saudação [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) ou [modelos de início rápido do Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) são solicitada tooselect um [OMS espaço de trabalho e a conta de automação ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="0201a-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="0201a-122">Estes são valores de saudação toopopulate usados de cada um dos parâmetros de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="0201a-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="0201a-123">não é solicitado ao usuário de saudação toodirectly fornecer valores para parâmetros de saudação padrão, mas são solicitadas tooprovide valores para parâmetros adicionais.</span><span class="sxs-lookup"><span data-stu-id="0201a-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="0201a-124">Quando o usuário Olá instala sua solução [outro método](operations-management-suite-solutions.md#finding-and-installing-management-solutions), eles devem fornecer um valor para todos os parâmetros padrão e todos os parâmetros adicionais.</span><span class="sxs-lookup"><span data-stu-id="0201a-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="0201a-125">Um parâmetro de exemplo é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="0201a-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="0201a-126">Olá, a tabela a seguir descreve os atributos de saudação de um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="0201a-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="0201a-127">Atributo</span><span class="sxs-lookup"><span data-stu-id="0201a-127">Attribute</span></span> | <span data-ttu-id="0201a-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="0201a-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0201a-129">type</span><span class="sxs-lookup"><span data-stu-id="0201a-129">type</span></span> |<span data-ttu-id="0201a-130">Tipo de dados para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="0201a-130">Data type for hello parameter.</span></span> <span data-ttu-id="0201a-131">controle de entrada Hello exibido para o usuário Olá depende Olá tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="0201a-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="0201a-132">bool – Caixa suspensa</span><span class="sxs-lookup"><span data-stu-id="0201a-132">bool - Drop down box</span></span><br><span data-ttu-id="0201a-133">cadeia de caracteres – caixa de texto</span><span class="sxs-lookup"><span data-stu-id="0201a-133">string - Text box</span></span><br><span data-ttu-id="0201a-134">int – Caixa de texto</span><span class="sxs-lookup"><span data-stu-id="0201a-134">int - Text box</span></span><br><span data-ttu-id="0201a-135">securestring – Campo de senha</span><span class="sxs-lookup"><span data-stu-id="0201a-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="0201a-136">categoria</span><span class="sxs-lookup"><span data-stu-id="0201a-136">category</span></span> |<span data-ttu-id="0201a-137">Categoria opcional para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="0201a-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="0201a-138">Parâmetros no hello mesma categoria são agrupados juntos.</span><span class="sxs-lookup"><span data-stu-id="0201a-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="0201a-139">controle</span><span class="sxs-lookup"><span data-stu-id="0201a-139">control</span></span> |<span data-ttu-id="0201a-140">Funcionalidade adicional para parâmetros de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0201a-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="0201a-141">datetime – O controle datetime é exibido.</span><span class="sxs-lookup"><span data-stu-id="0201a-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="0201a-142">GUID - valor Guid é gerado automaticamente e o parâmetro hello não é exibido.</span><span class="sxs-lookup"><span data-stu-id="0201a-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="0201a-143">description</span><span class="sxs-lookup"><span data-stu-id="0201a-143">description</span></span> |<span data-ttu-id="0201a-144">Descrição opcional para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="0201a-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="0201a-145">Exibido em um parâmetro de toohello informações balão Avançar.</span><span class="sxs-lookup"><span data-stu-id="0201a-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="0201a-146">Parâmetros padrão</span><span class="sxs-lookup"><span data-stu-id="0201a-146">Standard parameters</span></span>
<span data-ttu-id="0201a-147">Olá tabela a seguir lista os parâmetros padrão do hello todas as soluções de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0201a-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="0201a-148">Esses valores são populados para usuário Olá em vez de solicitar para eles quando sua solução é instalada da saudação Azure Marketplace ou Quickstart modelos.</span><span class="sxs-lookup"><span data-stu-id="0201a-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="0201a-149">usuário Olá deve fornecer valores para que eles se solução Olá é instalada com o outro método.</span><span class="sxs-lookup"><span data-stu-id="0201a-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="0201a-150">interface do usuário Olá em modelos do Azure Marketplace e Quickstart hello está esperando nomes de parâmetro hello na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="0201a-151">Se você usar nomes de parâmetros diferentes, em seguida, Olá usuário será solicitado para eles, e eles não serão preenchidos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0201a-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="0201a-152">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0201a-152">Parameter</span></span> | <span data-ttu-id="0201a-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="0201a-153">Type</span></span> | <span data-ttu-id="0201a-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="0201a-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0201a-155">accountName</span><span class="sxs-lookup"><span data-stu-id="0201a-155">accountName</span></span> |<span data-ttu-id="0201a-156">string</span><span class="sxs-lookup"><span data-stu-id="0201a-156">string</span></span> |<span data-ttu-id="0201a-157">Nome da conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0201a-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="0201a-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="0201a-158">pricingTier</span></span> |<span data-ttu-id="0201a-159">string</span><span class="sxs-lookup"><span data-stu-id="0201a-159">string</span></span> |<span data-ttu-id="0201a-160">Tipo de preço do espaço de trabalho do Log Analytics e da conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0201a-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="0201a-161">regionId</span><span class="sxs-lookup"><span data-stu-id="0201a-161">regionId</span></span> |<span data-ttu-id="0201a-162">string</span><span class="sxs-lookup"><span data-stu-id="0201a-162">string</span></span> |<span data-ttu-id="0201a-163">Região do hello conta de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0201a-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="0201a-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="0201a-164">solutionName</span></span> |<span data-ttu-id="0201a-165">string</span><span class="sxs-lookup"><span data-stu-id="0201a-165">string</span></span> |<span data-ttu-id="0201a-166">Nome da solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-166">Name of hello solution.</span></span>  <span data-ttu-id="0201a-167">Se você estiver implantando sua solução por meio de modelos de início rápido, em seguida, você deve definir solutionName como um parâmetro para que você pode definir uma cadeia de caracteres em vez disso, exigindo Olá usuário toospecify um.</span><span class="sxs-lookup"><span data-stu-id="0201a-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="0201a-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="0201a-168">workspaceName</span></span> |<span data-ttu-id="0201a-169">string</span><span class="sxs-lookup"><span data-stu-id="0201a-169">string</span></span> |<span data-ttu-id="0201a-170">O nome do espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0201a-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="0201a-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="0201a-171">workspaceRegionId</span></span> |<span data-ttu-id="0201a-172">string</span><span class="sxs-lookup"><span data-stu-id="0201a-172">string</span></span> |<span data-ttu-id="0201a-173">Região do espaço de trabalho de análise de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="0201a-174">A seguir está a estrutura Olá Olá padrão de parâmetros de que você pode copiar e colar no arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="0201a-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

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
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="0201a-175">Consulte tooparameter valores em outros elementos de solução de saudação com sintaxe Olá **parâmetros ('nome do parâmetro')**.</span><span class="sxs-lookup"><span data-stu-id="0201a-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="0201a-176">Por exemplo, tooaccess Olá nome do espaço de trabalho, você usaria **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="0201a-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="0201a-177">variáveis</span><span class="sxs-lookup"><span data-stu-id="0201a-177">Variables</span></span>
<span data-ttu-id="0201a-178">[Variáveis](../azure-resource-manager/resource-group-authoring-templates.md#variables) são valores que você usará no restante da saudação de solução de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="0201a-179">Esses valores não são toohello exposto usuário instalar Olá solução.</span><span class="sxs-lookup"><span data-stu-id="0201a-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="0201a-180">Eles são autor, Olá tooprovide pretendida com um único local onde eles podem gerenciar os valores que podem ser usados várias vezes em toda a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="0201a-181">Você deve colocar qualquer solução de tooyour específico de valores em variáveis como toohard contrário codificá-los em Olá **recursos** elemento.</span><span class="sxs-lookup"><span data-stu-id="0201a-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="0201a-182">Isso torna o código hello mais legível e permite que você tooeasily alterar esses valores em versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="0201a-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="0201a-183">A seguir está um exemplo de um elemento **variables** com parâmetros típicos usado em soluções.</span><span class="sxs-lookup"><span data-stu-id="0201a-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="0201a-184">Consulte toovariable valores por meio da solução de saudação com sintaxe Olá **variáveis ('nome da variável')**.</span><span class="sxs-lookup"><span data-stu-id="0201a-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="0201a-185">Por exemplo, tooaccess Olá SolutionName variável, você usaria **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="0201a-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="0201a-186">Você também pode definir variáveis complexas que têm vários conjuntos de valores.</span><span class="sxs-lookup"><span data-stu-id="0201a-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="0201a-187">Elas são particularmente úteis em soluções de gerenciamento, quando você estiver definindo várias propriedades para diferentes tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0201a-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="0201a-188">Por exemplo, você poderia reestruturar variáveis de solução Olá mostrados acima toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="0201a-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="0201a-189">Nesse caso, você pode consultar toovariable valores por meio da solução de saudação com sintaxe Olá **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="0201a-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="0201a-190">Por exemplo, tooaccess Olá variável do nome da solução, você usaria **variables('Solution'). Nome**.</span><span class="sxs-lookup"><span data-stu-id="0201a-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="0201a-191">Recursos</span><span class="sxs-lookup"><span data-stu-id="0201a-191">Resources</span></span>
<span data-ttu-id="0201a-192">[Recursos](../azure-resource-manager/resource-group-authoring-templates.md#resources) definir Olá recursos diferentes que instalará e configurará sua solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0201a-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="0201a-193">Isso será Olá maior e mais complexo parte do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="0201a-194">Você pode obter estrutura hello e uma descrição completa dos elementos de recurso no [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="0201a-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="0201a-195">Recursos diferentes que normalmente são definidos são detalhados em outros artigos desta documentação.</span><span class="sxs-lookup"><span data-stu-id="0201a-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="0201a-196">Dependências</span><span class="sxs-lookup"><span data-stu-id="0201a-196">Dependencies</span></span>
<span data-ttu-id="0201a-197">Olá **dependsOn** elementos especifica um [dependência](../azure-resource-manager/resource-group-define-dependencies.md) em outro recurso.</span><span class="sxs-lookup"><span data-stu-id="0201a-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="0201a-198">Quando Olá solução estiver instalada, um recurso não é criado até que todas as suas dependências foram criadas.</span><span class="sxs-lookup"><span data-stu-id="0201a-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="0201a-199">Por exemplo, sua solução pode [iniciar um runbook](operations-management-suite-solutions-resources-automation.md#runbooks) quando ele é instalado usando um [recurso de trabalho](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="0201a-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="0201a-200">recursos de trabalho Olá são dependentes Olá runbook recurso toomake se que esse runbook Olá foi criado antes de saudação trabalho é criado.</span><span class="sxs-lookup"><span data-stu-id="0201a-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="0201a-201">Espaço de trabalho do OMS e Conta de automação</span><span class="sxs-lookup"><span data-stu-id="0201a-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="0201a-202">Soluções de gerenciamento exigem um [espaço de trabalho do OMS](../log-analytics/log-analytics-manage-access.md) toocontain modos de exibição e um [conta de automação](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks e recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0201a-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="0201a-203">Eles devem estar disponíveis antes Olá recursos na solução de saudação são criados e não devem ser definidos na solução de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="0201a-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="0201a-204">usuário Olá será [especificar um espaço de trabalho e a conta](operations-management-suite-solutions.md#oms-workspace-and-automation-account) quando eles implantar sua solução, mas como autor hello, você deve considerar Olá pontos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0201a-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="0201a-205">Recurso da solução</span><span class="sxs-lookup"><span data-stu-id="0201a-205">Solution resource</span></span>
<span data-ttu-id="0201a-206">Cada solução requer uma entrada de recurso no hello **recursos** elemento que define a solução de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="0201a-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="0201a-207">Isso terá um tipo de **Microsoft.OperationsManagement/solutions** e ter Olá estrutura a seguir.</span><span class="sxs-lookup"><span data-stu-id="0201a-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="0201a-208">Isso inclui [parâmetros padrão](#parameters) e [variáveis](#variables) que são propriedades de toodefine geralmente usados da solução hello.</span><span class="sxs-lookup"><span data-stu-id="0201a-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


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




### <a name="dependencies"></a><span data-ttu-id="0201a-209">Dependências</span><span class="sxs-lookup"><span data-stu-id="0201a-209">Dependencies</span></span>
<span data-ttu-id="0201a-210">recursos de solução de saudação devem ter uma [dependência](../azure-resource-manager/resource-group-define-dependencies.md) em todos os outros recursos na solução Olá porque eles precisão tooexist antes da criação de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="0201a-211">Faça isso adicionando uma entrada para cada recurso no hello **dependsOn** elemento.</span><span class="sxs-lookup"><span data-stu-id="0201a-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="0201a-212">Propriedades</span><span class="sxs-lookup"><span data-stu-id="0201a-212">Properties</span></span>
<span data-ttu-id="0201a-213">recursos de solução de saudação tem propriedades de saudação em Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="0201a-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="0201a-214">Isso inclui recursos de saudação referenciado e contido por solução Olá que define como os recursos de saudação é gerenciado depois Olá solução estiver instalada.</span><span class="sxs-lookup"><span data-stu-id="0201a-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="0201a-215">Cada recurso na solução Olá deve ser listado na qualquer Olá **referencedResources** ou hello **containedResources** propriedade.</span><span class="sxs-lookup"><span data-stu-id="0201a-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="0201a-216">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0201a-216">Property</span></span> | <span data-ttu-id="0201a-217">Descrição</span><span class="sxs-lookup"><span data-stu-id="0201a-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0201a-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="0201a-218">workspaceResourceId</span></span> |<span data-ttu-id="0201a-219">ID do espaço de trabalho de análise de Log de saudação na forma de saudação  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nome do espaço de trabalho\>*.</span><span class="sxs-lookup"><span data-stu-id="0201a-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="0201a-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="0201a-220">referencedResources</span></span> |<span data-ttu-id="0201a-221">Lista de recursos na solução de saudação que não devem ser removidos quando Olá solução é removida.</span><span class="sxs-lookup"><span data-stu-id="0201a-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="0201a-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="0201a-222">containedResources</span></span> |<span data-ttu-id="0201a-223">Lista de recursos na solução de saudação que deve ser removido quando a solução de saudação é removida.</span><span class="sxs-lookup"><span data-stu-id="0201a-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="0201a-224">exemplo Hello acima é uma solução com um runbook, um agendamento e exibição.</span><span class="sxs-lookup"><span data-stu-id="0201a-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="0201a-225">agenda Hello e runbook são *referenciado* em Olá **propriedades** elemento para que eles não são removidos quando Olá solução é removida.</span><span class="sxs-lookup"><span data-stu-id="0201a-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="0201a-226">Olá exibição é *contidos* para que ele será removido quando a solução de saudação é removida.</span><span class="sxs-lookup"><span data-stu-id="0201a-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="0201a-227">Plano</span><span class="sxs-lookup"><span data-stu-id="0201a-227">Plan</span></span>
<span data-ttu-id="0201a-228">Olá **plano** entidade do recurso de solução de saudação tem propriedades de saudação em Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="0201a-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="0201a-229">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0201a-229">Property</span></span> | <span data-ttu-id="0201a-230">Descrição</span><span class="sxs-lookup"><span data-stu-id="0201a-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0201a-231">name</span><span class="sxs-lookup"><span data-stu-id="0201a-231">name</span></span> |<span data-ttu-id="0201a-232">Nome da solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-232">Name of hello solution.</span></span> |
| <span data-ttu-id="0201a-233">version</span><span class="sxs-lookup"><span data-stu-id="0201a-233">version</span></span> |<span data-ttu-id="0201a-234">Versão da solução Olá conforme determinado pelo autor da saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="0201a-235">product</span><span class="sxs-lookup"><span data-stu-id="0201a-235">product</span></span> |<span data-ttu-id="0201a-236">Solução de saudação do tooidentify de cadeia de caracteres exclusiva.</span><span class="sxs-lookup"><span data-stu-id="0201a-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="0201a-237">publicador</span><span class="sxs-lookup"><span data-stu-id="0201a-237">publisher</span></span> |<span data-ttu-id="0201a-238">Editor do Gerenciador de saudação.</span><span class="sxs-lookup"><span data-stu-id="0201a-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="0201a-239">Amostra</span><span class="sxs-lookup"><span data-stu-id="0201a-239">Sample</span></span>
<span data-ttu-id="0201a-240">Você pode exibir exemplos de arquivos de solução com um recurso de solução a saudação locais a seguir.</span><span class="sxs-lookup"><span data-stu-id="0201a-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="0201a-241">Recursos de automação</span><span class="sxs-lookup"><span data-stu-id="0201a-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="0201a-242">Recursos de pesquisa e alerta</span><span class="sxs-lookup"><span data-stu-id="0201a-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="0201a-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0201a-243">Next steps</span></span>
* <span data-ttu-id="0201a-244">[Adicionar alertas e pesquisas salvas](operations-management-suite-solutions-resources-searches-alerts.md) tooyour solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0201a-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="0201a-245">[Adicionar modos de exibição](operations-management-suite-solutions-resources-views.md) tooyour solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0201a-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="0201a-246">[Adicionar runbooks e outros recursos de automação](operations-management-suite-solutions-resources-automation.md) tooyour solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0201a-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="0201a-247">Obter detalhes de saudação do [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0201a-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="0201a-248">Pesquise entre os [Modelos de Início Rápido do Azure](https://azure.microsoft.com/documentation/templates) para obter exemplos de diferentes modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0201a-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
