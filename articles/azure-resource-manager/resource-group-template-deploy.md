---
title: recursos de aaaDeploy com o PowerShell e o modelo | Microsoft Docs
description: "Use o Gerenciador de recursos do Azure e o Azure PowerShell toodeploy um tooAzure de recursos. Olá recursos são definidos em um modelo do Gerenciador de recursos."
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
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="b7e4b-104">Implantar recursos com modelos do Resource Manager e o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7e4b-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="b7e4b-105">Este tópico explica como toouse PowerShell do Azure com o Gerenciador de recursos modelos toodeploy tooAzure seus recursos.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="b7e4b-106">Se você não estiver familiarizado com conceitos de saudação de implantar e gerenciar suas soluções do Azure, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="b7e4b-107">modelo do Gerenciador de recursos de saudação implantar pode ser um arquivo local no seu computador ou um arquivo externo que está localizado em um repositório como GitHub.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="b7e4b-108">modelo de saudação implantar neste artigo está disponível no hello [modelo](#sample-template) seção, ou como [modelo de conta de armazenamento no GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="b7e4b-109">Implantar um modelo do computador local</span><span class="sxs-lookup"><span data-stu-id="b7e4b-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="b7e4b-110">Ao implantar recursos tooAzure, você:</span><span class="sxs-lookup"><span data-stu-id="b7e4b-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="b7e4b-111">Faça logon no tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="b7e4b-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="b7e4b-112">Crie um grupo de recursos que funciona como contêiner Olá para recursos de saudação implantado.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="b7e4b-113">nome de Olá saudação do grupo de recursos pode incluir somente caracteres alfanuméricos, períodos, sublinhados, hifens e parênteses.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="b7e4b-114">Ele pode ser too90 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-114">It can be up too90 characters.</span></span> <span data-ttu-id="b7e4b-115">Não pode terminar com um ponto.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="b7e4b-116">Implantar o modelo Olá de grupo de recursos de toohello que define Olá recursos toocreate</span><span class="sxs-lookup"><span data-stu-id="b7e4b-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="b7e4b-117">Um modelo pode incluir parâmetros que permitem a implantação de saudação toocustomize.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="b7e4b-118">Por exemplo, você pode fornecer valores que são personalizados para um determinado ambiente (como desenvolvimento, teste e produção).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="b7e4b-119">modelo de exemplo Hello define um parâmetro para a conta de armazenamento Olá SKU.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="b7e4b-120">saudação de exemplo a seguir cria um grupo de recursos e implanta um modelo do computador local:</span><span class="sxs-lookup"><span data-stu-id="b7e4b-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="b7e4b-121">implantação de saudação pode levar toocomplete de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="b7e4b-122">Quando terminar, você verá uma mensagem que contém o resultado de saudação:</span><span class="sxs-lookup"><span data-stu-id="b7e4b-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="b7e4b-123">Implantar um modelo de uma fonte externa</span><span class="sxs-lookup"><span data-stu-id="b7e4b-123">Deploy a template from an external source</span></span>

<span data-ttu-id="b7e4b-124">Em vez de armazenar modelos do Gerenciador de recursos em seu computador local, você pode preferir toostore-los em um local externo.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="b7e4b-125">É possível armazenar modelos em um repositório de controle de código-fonte (como o GitHub).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="b7e4b-126">Ou ainda armazená-los em uma conta de armazenamento do Azure para acesso compartilhado na sua organização.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="b7e4b-127">toodeploy um modelo externo, use Olá **TemplateUri** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="b7e4b-128">Use Olá URI no modelo de exemplo hello exemplo toodeploy saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="b7e4b-129">Olá exemplo anterior requer um URI acessível publicamente para modelo de saudação, que funciona na maioria dos cenários, porque o modelo não deve incluir dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="b7e4b-130">Se você precisar toospecify os dados confidenciais (como uma senha de administrador), passe esse valor como um parâmetro seguro.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="b7e4b-131">No entanto, se você não quiser que seu modelo toobe publicamente acessível, você pode protegê-los, armazenando-o em um contêiner de armazenamento privado.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="b7e4b-132">Para obter informações sobre como implantar um modelo que exige um token SAS (assinatura de acesso compartilhado), confira [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="b7e4b-133">Arquivos de parâmetros</span><span class="sxs-lookup"><span data-stu-id="b7e4b-133">Parameter files</span></span>

<span data-ttu-id="b7e4b-134">Em vez de passar parâmetros como valores embutido em seu script, talvez seja mais fácil toouse um arquivo JSON que contém os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="b7e4b-135">arquivo de parâmetro Hello deve ser Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7e4b-135">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="b7e4b-136">Observe que a seção de parâmetros de saudação inclui um nome de parâmetro que coincide com o parâmetro hello definido no modelo (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="b7e4b-137">arquivo de parâmetro Hello contém um valor para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="b7e4b-138">Esse valor é automaticamente passado toohello modelo durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="b7e4b-139">Você pode criar vários arquivos de parâmetro para diferentes cenários de implantação e, em seguida, passe no arquivo de parâmetro apropriado de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="b7e4b-140">Copie Olá anterior de exemplo e salve-o como um arquivo chamado `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="b7e4b-141">toopass um arquivo de parâmetro de local, use Olá **TemplateParameterFile** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="b7e4b-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="b7e4b-142">toopass um arquivo de parâmetro externo, use Olá **TemplateParameterUri** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="b7e4b-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="b7e4b-143">Você pode usar parâmetros embutido e um parâmetro de local de arquivo por Olá mesma operação de implantação.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="b7e4b-144">Por exemplo, você pode especificar alguns valores no arquivo de parâmetro local hello e adicionar outros valores embutido durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="b7e4b-145">Se você fornecer valores para um parâmetro no arquivo de parâmetro local hello e embutido, o valor de embutido de saudação terá precedência.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="b7e4b-146">No entanto, quando você usa um arquivo de parâmetro externo, não é possível passar outros valores embutidos ou de um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="b7e4b-147">Quando você especifica um arquivo de parâmetro no hello **TemplateParameterUri** parâmetro, embutidas todos os parâmetros são ignorados.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="b7e4b-148">Forneça todos os valores de parâmetro no arquivo externo hello.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="b7e4b-149">Se seu modelo incluir um valor confidencial que você não pode incluir no arquivo de parâmetro hello, adicionar esse Cofre de chaves do valor tooa ou fornecer dinamicamente em linha todos os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="b7e4b-150">Se seu modelo incluir um parâmetro com o mesmo nome como um dos parâmetros Olá Olá comando do PowerShell de saudação, PowerShell apresenta o parâmetro hello de seu modelo com sufixo Olá **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="b7e4b-151">Por exemplo, um parâmetro denominado **ResourceGroupName** em seu modelo está em conflito com hello **ResourceGroupName** parâmetro hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="b7e4b-152">Você está tooprovide solicitado um valor para **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="b7e4b-153">Em geral, você deve evitar essa confusão ao não nomear parâmetros com o mesmo nome como parâmetros usados para operações de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="b7e4b-154">Testar uma implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="b7e4b-154">Test a template deployment</span></span>

<span data-ttu-id="b7e4b-155">tootest seus valores de parâmetro e de modelo sem realmente implantar qualquer recurso, use [AzureRmResourceGroupDeployment teste](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="b7e4b-156">Se nenhum erro for detectado, o comando Olá termina sem uma resposta.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="b7e4b-157">Se um erro for detectado, o comando Olá retorna uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="b7e4b-158">Por exemplo, a tentativa de toopass um valor incorreto para a conta de armazenamento Olá SKU, retorna Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7e4b-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="b7e4b-159">Se seu modelo tem um erro de sintaxe, o comando Olá retorna um erro indicando que ele não foi possível analisar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="b7e4b-160">mensagem de saudação indica o número de linha de saudação e a posição do erro de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="b7e4b-161">toouse completa modo, use Olá `Mode` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="b7e4b-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="b7e4b-162">Modelo de exemplo</span><span class="sxs-lookup"><span data-stu-id="b7e4b-162">Sample template</span></span>

<span data-ttu-id="b7e4b-163">Olá modelo a seguir é usado para obter exemplos de saudação neste tópico.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="b7e4b-164">Copie-o e salve-o como um arquivo chamado storage.json.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="b7e4b-165">toounderstand como toocreate esse modelo, consulte [criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="b7e4b-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7e4b-166">Next steps</span></span>
* <span data-ttu-id="b7e4b-167">exemplos de saudação neste artigo implantar grupo de recursos de tooa de recursos em sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="b7e4b-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="b7e4b-168">toouse uma assinatura diferente, consulte [gerenciar várias assinaturas do Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="b7e4b-169">Para um script de exemplo completo que implanta um modelo, veja [Script de implantação do modelo do Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="b7e4b-170">toounderstand como toodefine parâmetros em seu modelo, consulte [entender a estrutura de saudação e a sintaxe de modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="b7e4b-171">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="b7e4b-172">Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="b7e4b-173">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="b7e4b-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

