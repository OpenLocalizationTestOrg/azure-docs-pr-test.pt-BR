---
title: Implantar recursos com o PowerShell e o modelo | Microsoft Docs
description: "Use o Azure Resource Manager e o Azure PowerShell para implantar recursos no Azure. Os recursos são definidos em um modelo do Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="824da-104">Implantar recursos com modelos do Resource Manager e o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="824da-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="824da-105">Este tópico explica como usar o Azure PowerShell com modelos do Resource Manager para implantar seus recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="824da-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="824da-106">Caso não esteja familiarizado com os conceitos de implantação e gerenciamento das suas soluções Azure, consulte [Visão geral do Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="824da-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="824da-107">O modelo do Resource Manager que você implanta pode ser um arquivo local do seu computador ou um arquivo externo que está localizado em um repositório como o GitHub.</span><span class="sxs-lookup"><span data-stu-id="824da-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="824da-108">O modelo que você implanta neste artigo está disponível na seção [Modelo de exemplo](#sample-template) ou como [modelo de conta de armazenamento no GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="824da-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="824da-109">Implantar um modelo do computador local</span><span class="sxs-lookup"><span data-stu-id="824da-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="824da-110">Ao implantar recursos no Azure, você:</span><span class="sxs-lookup"><span data-stu-id="824da-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="824da-111">Fazer logon na sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="824da-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="824da-112">Crie um grupo de recursos que atue como o contêiner para os recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="824da-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="824da-113">O nome do grupo de recursos pode incluir somente caracteres alfanuméricos, pontos, sublinhados, hifens e parênteses.</span><span class="sxs-lookup"><span data-stu-id="824da-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="824da-114">Pode ter até 90 caracteres.</span><span class="sxs-lookup"><span data-stu-id="824da-114">It can be up to 90 characters.</span></span> <span data-ttu-id="824da-115">Não pode terminar com um ponto.</span><span class="sxs-lookup"><span data-stu-id="824da-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="824da-116">Implanta no grupo de recursos o modelo que define os recursos a serem criados</span><span class="sxs-lookup"><span data-stu-id="824da-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="824da-117">Um modelo pode incluir parâmetros que permitem personalizar a implantação.</span><span class="sxs-lookup"><span data-stu-id="824da-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="824da-118">Por exemplo, você pode fornecer valores que são personalizados para um determinado ambiente (como desenvolvimento, teste e produção).</span><span class="sxs-lookup"><span data-stu-id="824da-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="824da-119">O modelo de exemplo define um parâmetro para o SKU da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="824da-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="824da-120">O exemplo a seguir cria um grupo de recursos e implanta um modelo do computador local:</span><span class="sxs-lookup"><span data-stu-id="824da-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="824da-121">A implantação pode levar alguns minutos para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="824da-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="824da-122">Quando ela for concluída, você verá uma mensagem que inclui o resultado:</span><span class="sxs-lookup"><span data-stu-id="824da-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="824da-123">Implantar um modelo de uma fonte externa</span><span class="sxs-lookup"><span data-stu-id="824da-123">Deploy a template from an external source</span></span>

<span data-ttu-id="824da-124">Em vez de armazenar modelos do Resource Manager no computador local, talvez você prefira armazená-los em um local externo.</span><span class="sxs-lookup"><span data-stu-id="824da-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="824da-125">É possível armazenar modelos em um repositório de controle de código-fonte (como o GitHub).</span><span class="sxs-lookup"><span data-stu-id="824da-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="824da-126">Ou ainda armazená-los em uma conta de armazenamento do Azure para acesso compartilhado na sua organização.</span><span class="sxs-lookup"><span data-stu-id="824da-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="824da-127">Para implantar um modelo externo, use o parâmetro **TemplateUri**.</span><span class="sxs-lookup"><span data-stu-id="824da-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="824da-128">Use o URI do exemplo para implantar o modelo de exemplo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="824da-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="824da-129">O exemplo anterior requer um URI acessível publicamente para o modelo, que funciona na maioria dos cenários, pois o modelo não deve incluir dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="824da-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="824da-130">Se você precisar especificar dados confidenciais (como uma senha de administrador), passe esse valor como um parâmetro seguro.</span><span class="sxs-lookup"><span data-stu-id="824da-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="824da-131">No entanto, se não quiser que o modelo seja acessível publicamente, você pode protegê-lo armazenando-o em um contêiner de armazenamento privado.</span><span class="sxs-lookup"><span data-stu-id="824da-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="824da-132">Para obter informações sobre como implantar um modelo que exige um token SAS (assinatura de acesso compartilhado), confira [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="824da-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="824da-133">Arquivos de parâmetros</span><span class="sxs-lookup"><span data-stu-id="824da-133">Parameter files</span></span>

<span data-ttu-id="824da-134">Em vez de passar parâmetros como valores embutidos no script, talvez seja mais fácil usar um arquivo JSON que contenha os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="824da-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="824da-135">O arquivo de parâmetro deve estar no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="824da-135">The parameter file must be in the following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="824da-136">Observe que a seção de parâmetros inclui um nome de parâmetro que corresponde ao parâmetro definido no seu modelo (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="824da-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="824da-137">O arquivo de parâmetros contém um valor para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="824da-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="824da-138">Esse valor é passado automaticamente ao modelo durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="824da-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="824da-139">Você pode criar vários arquivos de parâmetros para diferentes cenários de implantação e, em seguida, passar o arquivo de parâmetros apropriado.</span><span class="sxs-lookup"><span data-stu-id="824da-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="824da-140">Copie o exemplo anterior e salve-o como um arquivo chamado `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="824da-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="824da-141">Para passar um arquivo de parâmetro local, use o **TemplateParameterFile**:</span><span class="sxs-lookup"><span data-stu-id="824da-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="824da-142">Para passar um arquivo de parâmetro externo, use o **TemplateParameterUri**:</span><span class="sxs-lookup"><span data-stu-id="824da-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="824da-143">Você pode usar parâmetros embutidos e um arquivo de parâmetro local na mesma operação de implantação.</span><span class="sxs-lookup"><span data-stu-id="824da-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="824da-144">Por exemplo, você pode especificar alguns valores no arquivo de parâmetro local e adicionar outros valores embutidos durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="824da-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="824da-145">Se você fornecer valores para um parâmetro no arquivo de parâmetros local e embutido, o valor embutido terá precedência.</span><span class="sxs-lookup"><span data-stu-id="824da-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="824da-146">No entanto, quando você usa um arquivo de parâmetro externo, não é possível passar outros valores embutidos ou de um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="824da-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="824da-147">Quando você especificar um arquivo de parâmetro no parâmetro **TemplateParameterUri**, todos os parâmetros embutidos serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="824da-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="824da-148">Forneça todos os valores de parâmetro no arquivo externo.</span><span class="sxs-lookup"><span data-stu-id="824da-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="824da-149">Se o seu modelo incluir um valor confidencial que não podem ser incluído no arquivo de parâmetros, adicione esse valor em um cofre de chaves ou forneça dinamicamente todos os valores de parâmetro embutidos.</span><span class="sxs-lookup"><span data-stu-id="824da-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="824da-150">Se o modelo incluir um parâmetro com o mesmo nome que um dos parâmetros no comando do PowerShell, o PowerShell apresentará o parâmetro do modelo com o postfix **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="824da-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="824da-151">Por exemplo, um parâmetro chamado **ResourceGroupName** em seu modelo entra em conflito com o parâmetro **ResourceGroupName** no cmdlet [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="824da-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="824da-152">Você recebe uma solicitação para fornecer um valor para **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="824da-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="824da-153">Em geral, você deve evitar essa confusão não dando aos parâmetros o mesmo nome dos parâmetros usados para operações de implantação.</span><span class="sxs-lookup"><span data-stu-id="824da-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="824da-154">Testar uma implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="824da-154">Test a template deployment</span></span>

<span data-ttu-id="824da-155">Para testar seus valores de parâmetro e modelo sem realmente implantar os recursos, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="824da-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="824da-156">Se nenhum erro for detectado, o comando será concluído sem uma resposta.</span><span class="sxs-lookup"><span data-stu-id="824da-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="824da-157">Se um erro for detectado, o comando retornará uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="824da-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="824da-158">Por exemplo, tentar passar um valor incorreto para o SKU da conta de armazenamento, retornará o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="824da-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="824da-159">Se o modelo tiver um erro de sintaxe, o comando retornará um erro indicando que não foi possível analisar o modelo.</span><span class="sxs-lookup"><span data-stu-id="824da-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="824da-160">A mensagem indica o número da linha e a posição do erro de análise.</span><span class="sxs-lookup"><span data-stu-id="824da-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="824da-161">Para usar o modo completo, use o parâmetro `Mode`:</span><span class="sxs-lookup"><span data-stu-id="824da-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="824da-162">Modelo de exemplo</span><span class="sxs-lookup"><span data-stu-id="824da-162">Sample template</span></span>

<span data-ttu-id="824da-163">O modelo a seguir é usado para os exemplos deste tópico.</span><span class="sxs-lookup"><span data-stu-id="824da-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="824da-164">Copie-o e salve-o como um arquivo chamado storage.json.</span><span class="sxs-lookup"><span data-stu-id="824da-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="824da-165">Para entender como criar esse modelo, confira [Criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="824da-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="824da-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="824da-166">Next steps</span></span>
* <span data-ttu-id="824da-167">Os exemplos deste artigo implantam recursos em um grupo de recursos na sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="824da-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="824da-168">Para usar outra assinatura, confira [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps) (Gerenciar várias assinaturas do Azure).</span><span class="sxs-lookup"><span data-stu-id="824da-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="824da-169">Para um script de exemplo completo que implanta um modelo, veja [Script de implantação do modelo do Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="824da-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="824da-170">Para entender como definir parâmetros em seu modelo, confira [Noções básicas de estrutura e sintaxe dos modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="824da-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="824da-171">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="824da-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="824da-172">Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="824da-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="824da-173">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="824da-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

